
Tags: #powershell #Active-Directory 
Related to: #hacking #bug-bounty #TCM #crtp #oscp #enumeration
See also: [[Introduction to Active Directory]] [[Enumeration Cheatsheet AD]] [[Access Control Model]]
Index: [[📋AD-Index-Work-Log]]


PS Remoting 
is set by default in server os
firewall exceptions are already set

### Two types 

One to One 
 - PS Session
 - New-pssession / Enter-psssession - requires local admin priv on target
 - Stateful

whoami /priv

![[Pasted image 20260412174514.png]]

One to Many
 - aka Fan-out remoting
 -  not interactive
 - executes commpands paralelly
 - invoke-command
- can accept commands and scripts

Constrained language mode causes issues

## Mimikatz
---

- dump creds
- uses ps remoting when we use command on multiple device
- use in "over pass the hash"

LO 7 

