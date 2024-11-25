A common vulnerability where concurrent process leads to uninted behaviour,


## Limit overrun race conditions 
Enables you to exceed some kind of limit imposed by the business logic of the application.

What would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

https://portswigger.net/web-security/learning-paths/race-conditions/race-conditions-limit-overrun/race-conditions/limit-overrun-race-conditions-r6f5

the application transitions through a temporary sub-state; that is, a state that it enters and then exits again before request processing is complete. In this case, the sub-state begins when the server starts processing the first request, and ends when it updates the database to indicate that you've already used this code. This introduces a small race window during which you can repeatedly claim the discount as many times as you like.

There are many variations of this kind of attack, including:

- Redeeming a gift card multiple times
- Rating a product multiple times
- Withdrawing or transferring cash in excess of your account balance
- Reusing a single CAPTCHA solution
- Bypassing an anti-brute-force rate limit

Repeater can do - using single tcp packet and network jitter - 2023.9
# Sending grouped HTTP requests
https://portswigger.net/burp/documentation/desktop/tools/repeater/send-group


# Turbo intruder
---

https://portswigger.net/web-security/learning-paths/race-conditions/race-conditions-detecting-and-exploiting-with-turbo-intruder/race-conditions/detecting-and-exploiting-limit-overrun-race-conditions-with-turbo-intruder-c3d4


https://portswigger.net/web-security/race-conditions/lab-race-conditions-limit-overrun ✅
