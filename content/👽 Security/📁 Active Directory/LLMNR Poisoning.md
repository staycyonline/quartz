Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[]] - index location 

#### LLMNR

Link Local Multi Host Name Resolution used when DNS fails

Key flaw is it requires username and password hash to function

#### LLMNR Poisoning
![[Pasted image 20230515081314.png]]

Responder tool is used for the LLMNR Posioning

This is a MiTM Attack

Best time to run is during mornings or after lunch when people are loggin in. 

We will get password hashes which we can crack to get password or use it for other attacks

#### Demo - Capturing NTLMv2 Hash with responder

run `responder -I interface-name -dwv `
on attacker machine

When the victim makes connections to DC - this will collect hashes and give it to us

We can use it for cracking or stuff like pass the hash

#### Defenses

- Disable LLMNR if not required NBT-NS
- If needed to use
	- Require Network Access control
	- Require very strong user passwords >14 chars and limit common word usage so hashes will be complex