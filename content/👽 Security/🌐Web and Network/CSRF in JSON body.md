Usually, JSON is CSRF-safe, but only when requests with content-type other than application/json gets rejected or additional CSRF protection is in place (Authorization headers/API keys). In another case, JSON CSRF can be achieved using the form with text/plain content-type, and well-formatted JSON request.

https://hackerone.com/reports/245346

grok
---

## CSRF Basics
First, a quick refresher: CSRF is an attack where a malicious site tricks a user’s browser into making an unintended request to a trusted site where the user is authenticated. Think of it like a forged letter with your signature—your bank trusts it because it came from *you*, but you didn’t write it. The classic example is a hidden `<form>` on `evil.com` that submits to `bank.com/transfer-money` using your logged-in session cookie.

Browsers make this possible because they automatically send cookies with requests to the target domain, and many sites rely on cookies for authentication. If the request is something simple like a `GET` or a `POST` with form data (`application/x-www-form-urlencoded`), it’s easy for an attacker to craft.

## JSON and CSRF: The Twist
Now, when you’re sending a JSON body (e.g., `Content-Type: application/json`), things get trickier for CSRF—but not impossible. The key question is: *Can an attacker forge a request with a JSON payload using a browser’s default behavior?* Let’s break it down.

### Why JSON Might Seem Safe
At first glance, JSON requests feel less vulnerable to CSRF because:
1. **HTML Forms Can’t Send JSON Directly**: A basic `<form>` tag submits data as `application/x-www-form-urlencoded` or `multipart/form-data`, not `application/json`. So, an attacker can’t just use `<form action="https://api.example.com/endpoint" method="POST">` to send `{"transfer": 1000}`.
2. **JavaScript Needed**: To send a JSON payload, you typically need an `XMLHttpRequest` (XHR) or `fetch()` call with a custom `Content-Type` header. Browsers enforce the Same-Origin Policy, meaning `evil.com` can’t directly use JS to send a request to `api.example.com` *and* include your cookies—unless something’s misconfigured (more on that later).

So, in a naive CSRF attack, an attacker can’t easily replicate an API call like:
```javascript
fetch("https://api.example.com/transfer", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ amount: 1000, to: "attacker" })
});
```
The Same-Origin Policy blocks `evil.com` from making this request to `api.example.com` outright.

### When JSON Requests *Are* Vulnerable
But here’s where it gets spicy—JSON requests *can* still be vulnerable to CSRF under specific conditions:
1. **Simple Requests and CORS Misconfiguration**:
   - Browsers classify some requests as “simple” (e.g., `GET`, `POST` with certain `Content-Type` values like `application/x-www-form-urlencoded`). These don’t trigger a CORS preflight (`OPTIONS`) check and send cookies automatically.
   - `application/json` isn’t a “simple” `Content-Type`, so a `POST` with JSON usually triggers a preflight. If the server responds to `OPTIONS` with `Access-Control-Allow-Origin: *` and `Access-Control-Allow-Credentials: true`, it’s game over. The attacker can craft a request from `evil.com`, and the browser will happily send your cookies along.
   - Example attack:
     ```html
     <script>
       fetch("https://api.example.com/transfer", {
         method: "POST",
         headers: { "Content-Type": "application/json" },
         body: '{"amount": 1000, "to": "attacker"}',
         credentials: "include"
       });
     </script>
     ```
     If the server’s CORS is too permissive, this works.

2. **Server Accepts Non-JSON as JSON**:
   - Some APIs are sloppy and parse `application/x-www-form-urlencoded` or plain text as JSON if it “looks” like it. An attacker could send:
     ```html
     <form action="https://api.example.com/transfer" method="POST">
       <input name="data" value='{"amount": 1000, "to": "attacker"}'>
       <input type="submit">
     </form>
     ```
     If the server interprets `data={"amount": 1000, "to": "attacker"}` as valid JSON, the CSRF succeeds with a simple form—no JS required.

3. **GET Requests with JSON in Query Params**:
   - If your API allows actions via `GET` (bad practice, but it happens), like `GET /transfer?data={"amount": 1000, "to": "attacker"}`, an attacker can use a simple `<img src="https://api.example.com/transfer?data=...">`. The browser sends the request with cookies, no preflight needed.

4. **Custom Headers Ignored**:
   - If your API doesn’t strictly enforce `Content-Type: application/json` and processes the request anyway, an attacker can dodge the JSON-specific hurdles with a form-based attack.

## Real-World Angle
Take a poorly configured API server. It uses cookies for auth (common in legacy systems or hybrid apps) and has a `POST /update-profile` endpoint expecting:
```json
{"name": "NewName"}
```
An attacker finds the server accepts `name={"name": "NewName"}` as form data and processes it. They host:
```html
<form action="https://api.example.com/update-profile" method="POST" enctype="application/x-www-form-urlencoded">
  <input name="name" value='{"name": "Hacked"}'>
</form>
<script>document.forms[0].submit();</script>
```
Your browser sends the request with your session cookie, and the profile’s updated. If the endpoint had scarier side effects (e.g., transferring funds), you’re toast.

## Protecting JSON APIs from CSRF
Here’s how to harden it:
1. **Use Anti-CSRF Tokens**: Require a unique, unpredictable token (e.g., in a header like `X-CSRF-Token`) that `evil.com` can’t guess. Check it server-side.
2. **Strict CORS**: Set `Access-Control-Allow-Origin` to specific domains, not `*`, when credentials are involved.
3. **Enforce Content-Type**: Reject requests unless `Content-Type: application/json` is present and correct.
4. **Avoid Cookie Auth**: Use token-based auth (e.g., Bearer tokens in `Authorization` header) instead of cookies—browsers don’t auto-send those.
5. **No GET Mutations**: Ensure state-changing actions require `POST`, `PUT`, etc., not `GET`.

## Bottom Line
A JSON-bodied request isn’t inherently vulnerable to CSRF because of the `Content-Type` hurdle, but sloppy server config or lax parsing can open the door. Classic CSRF loves forms; JSON CSRF needs either CORS missteps or server-side leniency. Lock down your API’s boundaries—tokens, headers, and CORS—and you’ll keep the forged requests at bay.