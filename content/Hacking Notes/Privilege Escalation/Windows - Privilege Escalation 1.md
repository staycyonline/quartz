Tags:  #privilege-escalation , #windows  
Index: [[]] - index location 

#### Courses
Windows priv esc TCM

#### Some resources

Fuzzy Security Guide - [https://www.fuzzysecurity.com/tutorials/16.html](https://www.fuzzysecurity.com/tutorials/16.html)

PayloadsAllTheThings Guide - [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)

Absolomb Windows Privilege Escalation Guide - [https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/](https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/)

Sushant 747's Guide (Country dependant - may need VPN) - [https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html)
https://github.com/Gr1mmie/Windows-Priviledge-Escalation-Resources

---
#### Tools

WinPEAS - [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS)

Windows PrivEsc Checklist - [https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation](https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation)

Sherlock - [https://github.com/rasta-mouse/Sherlock](https://github.com/rasta-mouse/Sherlock)

Watson - [https://github.com/rasta-mouse/Watson](https://github.com/rasta-mouse/Watson)

PowerUp - [https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc)

JAWS - [https://github.com/411Hall/JAWS](https://github.com/411Hall/JAWS)

Windows Exploit Suggester - [https://github.com/AonCyberLabs/Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)

Metasploit Local Exploit Suggester - [https://blog.rapid7.com/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/](https://blog.rapid7.com/2015/08/11/metasploit-local-exploit-suggester-do-less-get-more/)

Seatbelt - [https://github.com/GhostPack/Seatbelt](https://github.com/GhostPack/Seatbelt)

SharpUp - [https://github.com/GhostPack/SharpUp](https://github.com/GhostPack/SharpUp)

---
### System enumeration

#### System information

```
systeminfo
```

```sh
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

#### Grepping required data

```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
``` 

```sh
OS Name:                   Microsoft Windows 7 Enterprise 
OS Version:                6.1.7600 N/A Build 7600
System Type:               X86-based PC
```

#### Hostname (Also avaliable in sysinfo)

```sh
hostname
```

```sh
C:\Users>hostname
hostname
devel
```

#### Patch information

```
wmic qfe
```

#### Drives 
```sh
wmic logicaldrives
```

---
#### User enumeration

Know who you are 
```sh
whoami
```

Know your privileges
```sh
/priv
```

Know which groups we belong
```
whoami /groups
```

Know the users in the machine
```
net user
```

Know about a particular user
```sh
net user username
```

Know about local groups
```
net localgroup (localgroupname)
```

---
### Network Enumeration

#### Internet config

```sh
ipconfig
```

```sh

Windows IP Configuration


Ethernet adapter Local Area Connection 3:

   Connection-specific DNS Suffix  . : 
   IPv6 Address. . . . . . . . . . . : dead:beef::58c0:f1cf:abc6:bb9e
   Temporary IPv6 Address. . . . . . : dead:beef::bc80:758f:edf7:1ead
   Link-local IPv6 Address . . . . . : fe80::58c0:f1cf:abc6:bb9e%15
   IPv4 Address. . . . . . . . . . . : 10.10.10.5
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:6ca8%15
                                       10.10.10.2

Tunnel adapter isatap.{C57F02F8-DF4F-40EE-BC21-A206B3F501E4}:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 

Tunnel adapter Local Area Connection* 9:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 

```

#### Internet config - more info

```sh
ipconfig /all
```

```
Windows IP Configuration

   Host Name . . . . . . . . . . . . : devel
   Primary Dns Suffix  . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Local Area Connection 3:

   Connection-specific DNS Suffix  . : 
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-11-22-33-44-55
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::58c0:f1cf:abc6:bb9e(Preferred) 
   Temporary IPv6 Address. . . . . . : dead:beef::bc80:758f:edf7:1ead(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::58c0:f1cf:abc6:bb9e%15(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.10.10.5(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:6ca8%15
                                       10.10.10.2
   DNS Servers . . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBIOS over Tcpip. . . . . . . . : Enabled

Tunnel adapter isatap.{C57F02F8-DF4F-40EE-BC21-A206B3F501E4}:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 
   Description . . . . . . . . . . . : Microsoft ISATAP Adapter
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes

Tunnel adapter Local Area Connection* 9:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : 
   Description . . . . . . . . . . . : Teredo Tunneling Pseudo-Interface
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes

```
#### arp tables

```sh
arp -a
```

```sh
Interface: 10.10.10.5 --- 0xf
  Internet Address      Physical Address      Type
  10.10.10.2            00-50-56-b9-6c-a8     dynamic   
  10.10.10.255          ff-ff-ff-ff-ff-ff     static    
  224.0.0.22            01-00-5e-00-00-16     static    
  224.0.0.252           01-00-5e-00-00-fc     static  
```

#### Routing table

```sh
route print
```

```sh
===========================================================================
Interface List
 15...00 11 22 33 44 55 ......vmxnet3 Ethernet Adapter #3
  1...........................Software Loopback Interface 1
 11...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter
 12...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
===========================================================================

IPv4 Route Table
===========================================================================
Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0       10.10.10.2       10.10.10.5    261
       10.10.10.0    255.255.255.0         On-link        10.10.10.5    261
       10.10.10.5  255.255.255.255         On-link        10.10.10.5    261
     10.10.10.255  255.255.255.255         On-link        10.10.10.5    261
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
        224.0.0.0        240.0.0.0         On-link        10.10.10.5    261
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
  255.255.255.255  255.255.255.255         On-link        10.10.10.5    261
===========================================================================
Persistent Routes:
  Network Address          Netmask  Gateway Address  Metric
          0.0.0.0          0.0.0.0       10.10.10.2  Default 
          0.0.0.0          0.0.0.0       10.10.10.2  Default 
          0.0.0.0          0.0.0.0       10.10.10.2  Default 
===========================================================================

IPv6 Route Table
===========================================================================
Active Routes:
 If Metric Network Destination      Gateway
 15    261 ::/0                     fe80::250:56ff:feb9:6ca8
  1    306 ::1/128                  On-link
 15     13 dead:beef::/64           On-link
 15    261 dead:beef::58c0:f1cf:abc6:bb9e/128
                                    On-link
 15    261 dead:beef::bc80:758f:edf7:1ead/128
                                    On-link
 15    261 fe80::/64                On-link
 15    261 fe80::58c0:f1cf:abc6:bb9e/128
                                    On-link
  1    306 ff00::/8                 On-link
 15    261 ff00::/8                 On-link
===========================================================================
Persistent Routes:
  None
```

#### What ports are open ? (from inside)

```sh
netstat -ano
```

```

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:21             0.0.0.0:0              LISTENING       1384
  TCP    0.0.0.0:80             0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       664
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:5357           0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:49152          0.0.0.0:0              LISTENING       384
  TCP    0.0.0.0:49153          0.0.0.0:0              LISTENING       752
  TCP    0.0.0.0:49154          0.0.0.0:0              LISTENING       824
  TCP    0.0.0.0:49155          0.0.0.0:0              LISTENING       476
  TCP    0.0.0.0:49156          0.0.0.0:0              LISTENING       492
  TCP    10.10.10.5:139         0.0.0.0:0              LISTENING       4
  TCP    10.10.10.5:49168       10.10.16.10:443        CLOSE_WAIT      3176
  TCP    10.10.10.5:49172       10.10.16.10:443        ESTABLISHED     3804
  TCP    10.10.10.5:49207       10.10.16.10:8080       ESTABLISHED     2772
  TCP    10.10.10.5:49213       10.10.14.28:4444       ESTABLISHED     3636
  TCP    [::]:21                [::]:0                 LISTENING       1384
  TCP    [::]:80                [::]:0                 LISTENING       4
  TCP    [::]:135               [::]:0                 LISTENING       664
  TCP    [::]:445               [::]:0                 LISTENING       4
  TCP    [::]:5357              [::]:0                 LISTENING       4
  TCP    [::]:49152             [::]:0                 LISTENING       384
  TCP    [::]:49153             [::]:0                 LISTENING       752
  TCP    [::]:49154             [::]:0                 LISTENING       824
  TCP    [::]:49155             [::]:0                 LISTENING       476
  TCP    [::]:49156             [::]:0                 LISTENING       492
  UDP    0.0.0.0:123            *:*                                    948
  UDP    0.0.0.0:3702           *:*                                    1328
  UDP    0.0.0.0:3702           *:*                                    1328
  UDP    0.0.0.0:5355           *:*                                    1040
  UDP    0.0.0.0:55010          *:*                                    1328
  UDP    10.10.10.5:137         *:*                                    4
  UDP    10.10.10.5:138         *:*                                    4
  UDP    10.10.10.5:1900        *:*                                    1328
  UDP    127.0.0.1:1900         *:*                                    1328
  UDP    127.0.0.1:62425        *:*                                    1328
  UDP    [::]:123               *:*                                    948
  UDP    [::]:3702              *:*                                    1328
  UDP    [::]:3702              *:*                                    1328
  UDP    [::]:5355              *:*                                    1040
  UDP    [::]:55011             *:*                                    1328
  UDP    [::]:56197             *:*                                    1040
  UDP    [::1]:1900             *:*                                    1328
  UDP    [::1]:62424            *:*                                    1328
  UDP    [fe80::58c0:f1cf:abc6:bb9e%15]:1900  *:*                                    1328

```

---
### Password Hunting 

#### Find word password in text, ini and config files

```sh
findstr /si password *.txt *.ini *.config
```

Refer references in the start

---

#### AV Enumeration

Check if windows defender service is running
```sh
sc query windefend
```

Find running services
```sh
sc queryx type=service
```

Check firewall state and info
```sh
netsh advfirewall firewall dump
```


```sh
netsh firewall show state
```

---
#### Automated tools

![[Pasted image 20230818075600.png]]

