
%%
Tags: #web #attack #methodology #csrf #vulnerability 
See also: 
Index: [[]] - index location 

This is a commented section - wont see in the final render but can add useful info to map and search information
Add Additional Params that can help retrieve/ consolidate information
%%

## Summary  
---
> [! note] This is a sample summary of the page. This page provides an easy to start with template which can be used to record information and additional tags and attributes which link this info with other notes 

## Looking for CSRF
---
- Attacker being able to trick a legitimate user to perform a specific action on a target website
- Look for bugs in highly sensitive functions like email change, checkout where CSRF should be implemented. This can give an idea about CSRF security of the whole site.
- What happens when you send a blank csrf token? Do you get framework info or an error?
- Test the most secure functions and work backwards
- Does some function have a different way of protecting? Why is it so? (Different team, old code, different parameter?) 
- One common approach developers take is checking the referer header value and if it isn't their website, then drop the request. However this backfires because sometimes the checks are only executed if the referer header is actually found, and if it isn't, no checks done.
- Blank refere can be obtaained by
```html
	<meta name="referrer" content="no-referrer" />
	<iframe src=”data:text/html;base64,form_code_here”>
```
- As well as this sometimes they'll only check if their domain is found in the referer, so creating a directory on your site & visiting https://www.yoursite.com/https://www.theirsite.com/ may bypass the checks
- Or what about https://www.theirsite.computer/
- Focus on sensitive areas and see if they have a custom filter
 
> [!tip] Where there is a filter , there is probably a bypass




 