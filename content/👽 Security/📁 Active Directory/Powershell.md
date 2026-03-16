
 We will use it for Enumeration.  Based on .NET
 Powershell is actually System.Management.Automation.dll not just powershell exe

Loading a script
- Dot sourcing - path of the script
- Import-Module command - can be used for a module or the entire script
- Get Command -Module Module name - will list all commands

Download execute cradle - to get scripts remotely

Interacting with AD using PowerShell 
 - ADSI
 - .NET Classes
 - Native Executable
 - WMI using powershell
 - MS AD Module


Language modes in PowerShell - AD Module only works in CLM

Execution Policy is not a security layer - just preventing accidental execution
Offensive PowerShell is not dead




Load a script from disk
![[Pasted image 20251119055659.png]]

Load remotely

![[Pasted image 20251119055757.png]]

iex is widely abused and hence ms has defenses

![[Pasted image 20251119055900.png]]

![[Pasted image 20251119055929.png]]

We can bypass these

![[Pasted image 20251119060613.png]]



## Invisishell

![[Pasted image 20251119061001.png]]
![[Pasted image 20251119061105.png]]

![[Pasted image 20251119061158.png]]

