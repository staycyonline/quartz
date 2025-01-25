# Flag one
---
Hardcoded string in login activity - check source suing jadx

# Flag two
---
The activity b3nac.injuredandroid.b25lActivity has export set as true - check androidmanifest.xml - this means we can invoke it manually
 
am start b3nac.injuredandroid/.b25lActivity

# Flag three
---
Hardcoded parameter was stored in strings.xml and it was stored in code with an alias cmVzb3VyY2VzX3lv

# Flag four
---

![[Pasted image 20250124165510.png]]

function g() was referenced while initlaizing byte[]

![[Pasted image 20250124165627.png]]

![[Pasted image 20250124165616.png]]
Base 64 decode for flag

# Flag Eight
---
use cloud enum to find buckets for injured android company

we find injuredandroid.s3.amazonaws.com - browse to get flag


# Flag Nine
---
find firebase db url 
there is an encoded part in code that gives out /flag
so in/flag dir .json file is exposed

