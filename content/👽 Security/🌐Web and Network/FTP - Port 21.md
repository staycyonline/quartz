Tags: #concepts #ftp #port21 
Index: [[]] - index location 

 -  FTP - protocol for transfer of file and commands
 - port 21 - default
 - Active and passive FTP
 - active - client opens port and listens and server connect  to it 
 - passive - server opens and listens passively and server connect to it 

--------

**ftp ip-address**

**hydra is your friend for bruteforce**

can also use nmap to bruteforce using ftp-brute script

-------
#### Anonymous login

- ftp-anon - nmap script to find anonymous login


#### Exploiting FTP

^cb7185

- Anonymous login
- Hydra brutefore
	- hydra -L /user/list/path -P /password/liSt/path target-ip -t 4  ftp
- 
