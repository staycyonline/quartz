# API Passive Recon

Tags: [#api](app://obsidian.md/index.html#api) [#recon](app://obsidian.md/index.html#recon)  
Related to: [#hacking](app://obsidian.md/index.html#hacking)  
See also:  [[API Recon]]
Index: [Index of API Hacking](app://obsidian.md/Index%20of%20API%20Hacking)

#### Summary
Passive recon intro, tools and techniques from [link](https://university.apisec.ai/products/apisec-certified-expert/categories/2150259092/posts/2157852412)

#### Content
- Leverages osint
- Look for endpoints, access tokens,exposed creds,version info, APi documentation.APis business purpose
- creds can help me test as an auth user or admin, version can help me know about improper assets and other past  vuln, documentation csn help me in how to test targets and business logic flaws can be found from business purpose.
- High risk findings
	- JWT
	- Keys and creds
	- Secrets
	- PII
	- SSN, names, emails, CC info

#### Google dorking
Usually quick search can give results

Dorks can get us the info we need 
- Refer [Dork list - Box Piper](https://www.boxpiper.com/posts/google-dork-list)

#### GitDorking
 - use dorks in github to uncover issues in the target apis.
	 - read issues and the fixes they have propsed
	 - look for exposed - harcoded secrets keys
	 - look for new endpoints
	 - review pull requests
	 - use ctrl  + f to search for spicy terms like api_key, key, secret etc
	 - using history button in the code tab to review changes
	 - Files changed tab in pullrequest can reveal information
	 - if no weakness is found use it to find the language used, endpoint info, usage docs etc
	 
#### Shodan
- Can search for internet exposed APIs and get info 
- some shodan queries - https://github.com/jakejarvis/awesome-shodan-queries

#### [TruffleHog](https://github.com/trufflesecurity/trufflehog)

- tool for automatically discovering exposed secrets
- You can simply use the following Docker run to initiate a TruffleHog scan of your target's Github
	 `sudo docker run -it -v "$PWD:/pwd" trufflesecurity/trufflehog:latest github --org=target-name`

#### API Directories
- Programmableweb.com is a go-to source for API-related information ([https://www.programmableweb.com/apis/directory](https://www.programmableweb.com/apis/directory)).
-  To gather information about your target, use the API Directory, a searchable database of over 23,000 APIs. Expect to find API endpoints, version information, business logic information, the status of the API, source code, SDKs, articles, API documentation, and a changelog.

#### Wayback Machine 
 - great way to check historical changes to API
 - Zombie APIs - retired endpoints still in use - can be found in old docs or improperly managed docs - can be reported as improper asset management.
 - Make sure to note and test old API endpoints
 
###### References  (optional )