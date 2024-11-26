# Domain Enumeration
Tags: #powershell #Active-Directory 
Related to: #hacking #bug-bounty #TCM #crtp #oscp #enumeration
See also: [[Introduction to Active Directory]] [[Enumeration Cheatsheet AD]]
Index: [[CRTP/🗂️ Index of CRTP]]

#### Summary
Introduction and techniques of Domain Enumeration

#### Domain Enumeration
Mapping of various entities, trusts, relationships and privilages for the target domain.

#### Check privileges of current user in Powershell
`whoami /priv`

###### How to enumerate domain? (Method 1 - .NET Classes)
`$ADClass = [System.DirectoryServices.ActiveDirectory.Domain]`
`$ADClass::GetCurrentDomain()`

![[DomainenumAD1.png]]

###### How to enumerate domain? (Using Powerview)
[[Powerview|Refer Powerview Notes]]

###### How to enumerate domain? (Using Microsoft AD Module)
[[Microsoft AD Module|Refer Microsoft AD Module]]

**Advantages of AD Module over Powerview**
1. Less chance of Antivirus detection
2. Works well in constrained-language mode

###### Tips
- Install tools in a folder in C drive (for eg: `C:\AD\Tools`) to prevent Anti Virus detection.
- Microsoft AD Module is preferable over Powerview as AD module is a tool by Microsoft and is less likely to be detected by Anti Virus.
- 
 

###### References  (optional )