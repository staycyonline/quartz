Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

#### WINRM
- feature in windoes but not enabled by default
- windows remote mamagement protocol
- remote access to windows via http(s)
- typically 5985 5986
- supports various forms of authentication

#### Exploiting Winrm
- crackmapexec will be used for bruteforce and execucte commands
- evil-winrm ruby script to obtain reverseshell
- or metasploit module

crackmap exec can be used to know if the port runs winrm - `crackmapexec winrm targert-ip -u username -p /password/list`

`crackmapexec winrm targert-ip -u username -p password -x "command "`

evil-winrm ruby script to obtain reverseshell - `evil-winrm -u usernmae -p password -i traget=ip`

or use winrm module in metasploit - needs retrying



###### References  (optional )