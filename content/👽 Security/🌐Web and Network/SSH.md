Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[]] - index location 

#### Summary
SSH overview

#### SSH Enum

nmap scan can give os version and ssh version

nc ip port couldgive a banner denoting the ssh version and os version

**nmap scripts**

ssh2-enum-algos : gives algos used for key generation

ssh-hostkey: gives ssh rsa host key

ssh-auth-methods: gives ssh authentication methods

ssh-brute


**SSH Dictionary Attack**

hydra -l username -P /lpath/to/password/list

ssh-brute - can be used to brute force 

msfcosole auxiliary/scanner/ssh/login

#### Exploiting SSH

auth using password or key

- SSH bruteforce
	- hydra -L user/list/path -P /lpath/to/password/list ip -t 4 ssh
- 
 