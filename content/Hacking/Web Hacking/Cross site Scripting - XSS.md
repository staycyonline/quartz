%%
Tags: #web #attack #methodology #xss #vulnerability 
See also: 
Index: [[]] - index location 

This is a commented section - wont see in the final render but can add useful info to map and search information
Add Additional Params that can help retrieve/ consolidate information
%%
> [! note] Cross site scripting(XSS) is among the most common and most difficult to find in modern we apps also the easiest one to test for. The note discusses the processes, flow and resources for testing XSS 
 
 ---
 - Most common
 - Test every parameter that is reflected for reflected XSS and blind XSS
 - **WAF** - Web application firewall is the most common problem - tricky to bypass
	 - It is always tricky to bypass WAF and https://github.com/0xInfection/Awesome-WAF can give resource on research on WAFs and start from there. They also get patched so we need to try new stuff
- If there is a filter => the parameter is vulnerable to XSS - but dev has a filter to prevent its execution
- XSS is easiest to fix - filters don't always work.

### Process for testing

1. Test different encoding and notice weird behavior
	- How are basic html tags reflected? Are they being filtered? How do they handle double encoding? other encodings? https://d3adend.org/xss/ghettoBypass. 
	- Try to understand what's allowed and what's not and how are our payloads handled

2. Reverse engineering developer's thoughts
	- Why the filter was made? Does it exist everywhere in the webapp?
	- What all do they filter, do they just filter complete tags? Is there something they don't filter like maybe `<svg>`
	
> [!tip ] Pro tip: The more you poke around the more you learn

### Flow of testing

 - How are non malicious html tags handled?
 - What about incomplete tags?
 - How do they handle encoding?
 - Is it just a blacklist of hardcoded strings?  `</script/x>` `<ScRipt>`

Resource - https://github.com/masatokinugawa/filterbypass/wiki/Browser's-XSS-Filter-Bypass-Cheat-Sheet
