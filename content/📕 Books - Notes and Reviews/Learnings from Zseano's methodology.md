

%%
Tags: #book-review #methodology #tools #hacking 
See also: 
Index: [[]] - index location 

This is a commented section - wont see in the final render but can add useful info to map and search information
Add Additional Params that can help retrieve/ consolidate information
%%

## Summary 
---
> [!info] This is a sample summary of the page. This page provides an easy to start with template which can be used to record information and additional tags and attributes which link this info with other notes 

## Hackers Question Everything
---
Hackers are innately curious, every parameter, every function should be curiously looked at. Why does something work the way it is. What could have the developer thought while writing a function. Can we we get more end points or parameters?

Question Everything and keep trying for things

## Note on VDPs
---

>[!info] Use VDPs for testing your skills / research or for the sake of a challenge, Do not give them a full test. Use them but within limits. Do not burnout trying to find bugs for free.

## Basic toolkit
---
- Burp suite
- Amass - for subdomain and content (i feel ffuf, gobuster, dirsearch, subfinder can do better)
- httpprobe (i feel httpx is better) - to probe endpoints and s
- anew - to append new domains to list of existing ones and remove duplicates - [GitHub - tomnomnom/anew: A tool for adding new lines to files, skipping duplicates](https://github.com/tomnomnom/anew/tree/master)
- dnsgen - Generate endpoints and find if they exist-[GitHub - AlephNullSK/dnsgen: Generates combination of domain names from the provided input.](https://github.com/AlephNullSK/dnsgen)
- Aquatone (use gowitness instead) for visual inspection of the target
- ffuf - for finding files and directories
- seclists - (https://github.com/danielmiessler/SecLists/) for wordlists
- https://github.com/tomnomnom - for custom scripts - make your custom scripts
- wayback machine scanner - https://gist.github.com/mhmdiaa
- ParamScanner – A custom tool to scrape each endpoint discovered and search for input names, ids and javascript parameters. The script will look for  and scrape the name & ID and then try it as a parameter. As well as this it will also search for var {name} = “” and try determine parameters referenced in javascript. An old version of this tool can be found here https://github.com/zseano/InputScanner. Similar suchs include LinkFinder by @GerbenJavado which is used to scrape URLs from javascript files here: https://github.com/GerbenJavado/LinkFinder and @CiaranmaK has a tool named parameth used for brute forcing parameters. https://github.com/maK-/parameth 

- AnyChanges – This tool takes a list of URLS and regularly checks for any change

> [!tip] Pro tip : Use tools and scripts to find new parameters, content and functionality to poke at - look for new things - that is where gold is
> 

## Common issues zseano starts with
---
 - **Starts with what he knows best** then go on looking for others
 - Spends months on a target to understand it as deep as possible
 - First primarily looks for filters in place and tries to bypass them

### [[Cross site Scripting - XSS]]
### [[Cross site request forgery - CSRF]]

### [[Open URL Redirects]]
### SSRF
### CORS
### File Uploads for Stored XSS and RCE

