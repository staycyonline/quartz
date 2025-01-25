
# Words of wisdom
---

The more bug classes you know and the quirks of a language the more likely you might discover issues and recognize patterns

pick one language first

Many issues depend on architecture and operating system

learn from others - find what others have found and understand how it was done at first



# Ways to learn
---
## The github method
---
- search for vulns eg: 'fix sql injection' and look at commits
- different bug classes can be found in in CWE
- focus on the vulnerable candidate and work backwards to understand
- try running the vulnerable functions and supplying user input to see outputs
- When people fix one instance of the bug, the y often leave others open - look for other instances of the the issue
- Check and earlier commit and see if i can spot the vuln without looking the patch
- Also try searching vulnerable code pattern directly in GitHub to find them

## The exploit DB Method
---
- Search for a vuln, download the vulnerable application and explore the code
- If stuck look at the exploit and try to understand how the exploitation works ( check if it works in the first place )

# Bug Class Exploration
---
- CWE has a lot of samples and details
- Create scripts to simulate running of functions

# "Source code security audit speed run" - Eldar Marcussen
---
Execution flow
Data flow
Interuptions to flow

Data Flow
- Source 
- sink
- trust boundaries
- Stage change

Taint analysis

Approaches
 - hotspot checking 
	 - Grepping the keywords 
- Control flow sensitive
	- reading the code the way it is executed  - go from one function to function calll
- data flow sensitive
	- tracking the data - how the data is flowing through the app
- focus oriented
	- looking for a specific component / library
	- used in authentication and authorization 
- forward tracing
- backwards tracing
	- both f/w and backward tracing is starting at a random point and seeing where data came from

Identifying weaknesses
- reading documentation
- recognizing weakness paterns in source code
- recognizing weakness patterns in design or process
- analyze poor decision making
- try writing small scripts to understand how the code handles data - especially for languages you are unfamiliar with
- take breaks 

Issues can be classified as both
Presence of something that shouldn't be there
 - flawed code
 - logical isseus

Absence of something
 - Lack of authentication
 - Lack of authorization

Audit Speed run
 - identify weakness
 - prioritize high impact vulnerabilities
 - check exploitability
 
Tools aren't enough manual labor is required
 - absence of something is very difficult to detect

grep ✨ - a magic tool

quickly build custom scripts
 - use regexes to filter out required data and run through tools

Vuln speed run
-  avoid false positives
- avoid false negatives
- make a shortlist of vuln classes
	- code exec
	-  sqli / injection etc
	- avoid drowning in xss
- tweak the scripts to get developer habits

The higher up in code the issue, the more likely it can be exploited

# References
---
https://www.youtube.com/watch?v=hpYjjj1UAXs&t=0s
https://www.youtube.com/watch?v=b8Xbzer1n94&t=0s
https://trycrack.me/index
https://github.com/awesome-security/awesome-static-analysis
https://github.com/lukehutch/awesome-static-analysis
https://github.com/analysis-tools-dev/static-analysis