Tags: #htb, #hacking 
Related to: #practice, #htb, #write-up, 
Index: [[🗂️Index of HTB Writeups]] 

#### First things First!

###### Quick fast scan on top 100 ports

```sh
nmap -Pn -F -T4 10.10.11.219
```

```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-01 21:52 EDT
Nmap scan report for 10.10.11.219
Host is up (0.044s latency).
Not shown: 98 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 13.47 seconds

```

We got SSH and Http ports here. Sweet!

Lets run a script and service scan for these two and also run a top 1k port scan

1k port scan gave same results

######  Script and Service scan for the IPs

```sh
nmap -sC -sV -Pn  -p22,80 10.10.11.219
```

```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-01 22:01 EDT
Nmap scan report for 10.10.11.219
Host is up (0.041s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 20be60d295f628c1b7e9e81706f168f3 (RSA)
|   256 0eb6a6a8c99b4173746e70180d5fe0af (ECDSA)
|_  256 d14e293c708669b4d72cc80b486e9804 (ED25519)
80/tcp open  http    nginx 1.18.0
|_http-title: Did not follow redirect to http://pilgrimage.htb/
|_http-server-header: nginx/1.18.0
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.67 seconds

```

We have **nginx 1.18.0** - we can check for vulns
**OpenSSH 8.4p1** - we can check for vulns.

Let us visit the site before that (Browser gave an error page so tried curl)

```sh
curl -v 10.10.11.219
```

```
*   Trying 10.10.11.219:80...
* Connected to 10.10.11.219 (10.10.11.219) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.10.11.219
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 301 Moved Permanently
< Server: nginx/1.18.0
< Date: Wed, 02 Aug 2023 02:08:00 GMT
< Content-Type: text/html
< Content-Length: 169
< Connection: keep-alive
< Location: http://pilgrimage.htb/
< 
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.18.0</center>
</body>
</html>
* Connection #0 to host 10.10.11.219 left intact
 
```
---
#### The hunter of vulns (looking for vulns)

nginx

https://github.com/M507/CVE-2021-23017-PoC


Reference:
https://medium.com/@babayaga00897/pilgrimage-htb-writeup-ae8242270434
