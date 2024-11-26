# AD Defense
Tags: #Active-Directory #defense #enumeration  
Related to: #crtp #hacking #oscp 
See also: [[Introduction to Active Directory]] [[Enumeration Cheatsheet AD]]
Index: [[CRTP/🗂️ Index of CRTP]]


#### Denfense against Enumeration

Note - `<pipe symbol>` = `|`

Most of enumeration is similar to normal traffic but **User Hunting** is bit intrusive and noisy in nature.

This can be defended using `NetCease.ps1` 

This script changes permission on NetSessionEnum method by removing permission for Authenticated Users group.

Another script is SAMRi 10 whoch hardens Win 10 and Server 2016 against enumeration which uses SAMR protocol


