EPSS score - for vulns
Hella - open source tool for code review n audit

Source code security
---
White box
See what others cant see usually



---
How to code - want to build something - eg - automation for pentesting , or building a product
Learn to look for issues in popular choices
Rust is good :) - must learn lol
It is not the plane it is the pilot
shvm - HACK - convert to vm - 
Cassandra DB - likes, posts and stuff - 
Be platform neutral
Play around with features for testing
*No need to stick by the rules every time*
Get access to features, apps where most people don't get access.
Look for out of scope places for critical vulns
Passively follow employees

---
Understanding the coder can help - you find more bugs
What if you dont know the dev
 - git blame  - which specific function where written by whom
 - Do recon on the employee on github, and other platforms
 -  understand dangerous functions in programming language
 - How are teams making software - they are never in sync
 - How do they write function
 - Don't query directly always
 - Use a lot of functions so that changes can be done centrally

Issue with github- enterprise - PAT- personal access token - can list all repo of company - issue only fixed only in managed enterprises.  - PATs are leaked and internal repos of multiple companies - github is user friendly hence people don't migrate

Gitlab >> github

---

Always think How to reach the code
How to do white box during blaackbox

checksum based defenses - how to bypass
	- see if checksum is being calculating in frontend?
	- add  breakpoints and change variables to create new checksums

dupe request id - protection against duplication

Learn to write browser extensions
make api inventory

---

SBOM, SAST, SCA, Secret and IaC Scans?
---

SAST - deals with code related to your firm/team
SCA - we focus on 3rd party libraries
Secret and IaC scans - secrets and infrastructure as code scans

---
Hela - https://github.com/rohitcoder/hela
osv scanner - https://github.com/google/osv-scanner
Semgrep - https://semgrep.dev/
Trufflehog - https://github.com/trufflesecurity/trufflehog


---
link for private https://PAT@github.com/repository - if it is cloneable

github actions are stateless
hela-api  - hosted inside kubernetes - takes commands and runs a job - pushes job through defectdojo and slack 

secret/ ci issues

---

CVSS score doesn't have context will give you high score even if exploit was discovered 10 years ago
EPSS score - can predict exploitability in the current environment - exploited on the wild

---
network tab in chrome
identify api - which who calls the api - (initiator) - top most will be the last caller - top 3 are good target files
sources tab and browse the website it will get populated and make a tree 
Frontend is never secure!
use breakpoints

---
Selenium script for automation
look for common patterns in issues.

---
https://github.com/rohitcoder?tab=repositories

fingerprint auth is at OS level

---
code obfiscation - pyarmor - for python
js obfiscator for js - there are many library

get source for any lib in python
`libname.__file__`

---
karkend gateway - https://www.krakend.io/

secret scanners rely on regex (patterns) - what about username pass in base64 - scanner cant find them

2fa may not apply to every end point.

---
attacker made multiple accounts and tried to link phone number with them using their own account.
fix - check domain reputation
v3 captcha - mouse movements - trust score

---
docker repo vulnerables

https://codearsenalcommunity.github.io/

---
out of 10mil usrs 1 mil users jwt got compromised - each token is valid for 3 months

jwt cannot be revoked, they are stateless

change secret - all jwts will be invalid
blacklist 1 million tokens

store session id in jwt - not according to principle of jwt

---
.env files has environment info

---
FIle inclusion fix - whitelist
	.htaccess - url rewrite
		restrict users to pass roots
			always use frameworks - next js - react js
	paramspider
content editable attribute - html 
c,c++,java - memory dafety and memory management issues
	garbage collector - memory cleaning - makes it slower
		c,c++ more efficient than java in garbage collection- but prone to stack overflow

rust - cannot use a variable twice
memory is erased once the variable is used
variable.clone function is used to have multiple copies

Proper unit testing of code to investigate edge cases

---
csrf fixes
same site cookies
jwt in headers
state changes in header

---
SQLI and XSS are difficult to find

map subdomain and understand frameworks to find ones vulnerable to these issues

frameworks has a lot of support and vuln management

---
url signing - required for file uploads

match and replace - response - false to true

---
service accounts and api keys - an old employee can access their cloud docs if they aren't disabled

---

