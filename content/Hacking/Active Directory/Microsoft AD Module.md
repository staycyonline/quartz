# Microsoft AD Module
Tags: #tools #scripts #powershell #Active-Directory #Microsoft-AD-Module
Related to: #hacking #bug-bounty #TCM #crtp #oscp #enumeration
See also: [[Introduction to Active Directory]] , [[Powerview]]
Index: [[🗂️ Index of CRTP]]

#### Summary
How to setup and use Microsoft AD Module for AD enumeration

#### Microsoft AD Module

**Where can it be used?**

On a device connected to the AD environment.

**How to setup?**

[Setup File and instructions](https://github.com/samratashok/ADModule)

**Some commands**

_Make sure that you import AD Management.dll and AD.psd1 files using the powershell commands (1 and 2)_

1. `Import-Module .\Microsoft.ActiveDirectory.Management.dll`
2. `Import-Module .\ActiveDirectory\ActiveDirectory.psd1`

`Get-ADDomain` - Get current domain

`Get-ADDomain -Identity <domain name>` - Get object of the mentioned domain (_where we have trust to do so_)

`(Get-ADDomain).DomainSID` - Get domain SID for current domain

`Get-ADDomainController` - Get domain controller details

`Get-ADDomainController -DomainName <domain name> -Discover` - Get domain controller details for particular domain

Refer [[Enumeration Cheatsheet AD]] and [Microsoft Reference Doc](https://docs.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps) for more commands.

###### References
[Active Directory Enumeration AD Module Cheatsheet](https://github.com/S1ckB0y1337/Active-Directory-Exploitation-Cheat-Sheet#using-ad-module)
