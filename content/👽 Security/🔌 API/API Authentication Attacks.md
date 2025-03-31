## Classic Authentication Attacks
---
Used when basic auth is used

- Brute forcing
- Password spraying - when user names are known (see :[[Excessive Data Exposure]])

Usually one portal does the uid pass auth and then issues a token for other requests.

Burp Intruder

wfuzz - fuzzing tool (fuff is a good alternative)
-H used for content type headers
-d include post body data 
hiding responses
-z payload
FUZZ - keyword used to denote fuzz position

## API Token Attacks
---
Intercept auth request - send to sequencer 
live capture request - specify the token location
start live capture
auto analyze check box / analyze now

- Entropy / randomness
- bad tokens
	- https://raw.githubusercontent.com/hAPI-hacker/Hacking-APIs/main/bad_tokens - bad tokens repo
	- If randomness is less - tokens can be brute forced


### JSON Web Tokens - JWT
---
See Also : https://portswigger.net/web-security/jwt

JWT - base64 encoded - 3 parts
- Header
- Payload
- Signature
All separated by a period

jwt.io

### jwt tool
---
automates jwt attacks

As you can see, jwt_tool makes the header and payload values nice and clear. Additionally, jwt_tool has a “Playbook Scan” that can be used to target a web application and scan for common JWT vulnerabilities. You can run this scan by using the following:

**`$ jwt_tool -t http://target-name.com/ -rh "Authorization: Bearer JWT_Token" -M pb`**

-X option for attacks

-C crack attack

crunch tool - to generate paasowrds

if we crack the token - we can sign our own tokens

