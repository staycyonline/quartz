# Powerview
Tags: #tools #scripts #powershell #Active-Directory #powerview
Related to: #hacking #bug-bounty #TCM #crtp #oscp #enumeration
See also: [[Introduction to Active Directory]], [[Microsoft AD Module]]
Index: [[CRTP/🗂️ Index of CRTP]]

#### Summary
How to setup and use powerview for AD enumeration

#### Powerview

**Where can it be used?**

On a device connected to the AD environment.

**How to setup?**

1. Download powerview from powerview [github](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1) (in C:\AD\Tools to prevent AV detection) 
2. Open powershell  
3. Change directory to the installed script dir  
4. Run cmd  
5. Disable execution policy using ``powershell -ep bypass``  
6. Run ``. ./powerview.ps1``  
  
You can now use powerview.

**Some commands**

`Get-NetDomain` - Get current domain

`Get-NetDomain -Domain <domain name>` - Get object of the mentioned domain (_where we have trust to do so_)

`Get-DomainSID` - Get domain SID for current domain

`Get-DomainPolicy` - Displays Domain policies

`(Get-DomainPolicy)."system access"` - Shows system access policy details of our current machine

`Get-NetDomainController` - Get domain controller details

`Get-NetDomainController -Domain <domain name>` - Get domain controller details of particular domain

Refer [[Enumeration Cheatsheet AD]] for more commands.



###### References
[Active Directory Enumeration Hacker Notes](https://executeatwill.com/2020/01/06/Active-Directory-Enumeration-Hacker-Notes/)
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993