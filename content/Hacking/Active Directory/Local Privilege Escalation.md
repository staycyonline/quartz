# Local Privilege Escalation
Tags: #privilege-escalation  #Active-Directory 
Related to: #hacking, #crtp 
See also: 
Index: [[🗂️ Index of CRTP]]

#### Summary
Add a brief overview of what the content is

#### Introduction
- We are targeting ==Local Admin== and ==Domain Admin== to get higher privilages on the network.
- Although one may be able to complete red team assesment without local privilege escalation, it is always nice to escalate locally
-  Ways of locally escalating in windows
	- Missing Patches
	- Automated deploymeny and AutoLogon passwords in clear text
	- AlwatsInstallElevated(Any user can run MSI files as SYSTEM)
	- Misconfigured Services
	- DLL Hijacking etc
- Tools used
	- [PowerUp](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)
	- [BeRoot](https://github.com/AlessandroZ/BeRoot)
	- [Privesc](https://github.com/enjoiz/Privesc)

###### References  (optional )