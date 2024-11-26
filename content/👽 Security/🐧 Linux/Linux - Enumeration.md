
Tags: #enumeration #linux  
Index: [[]] - index location 

---
#### Summary
Enumeration tools, commands, and techniques to extract data and prepare for Privilege Escalation

---
#### System Enumeration

| Command             | Purpose/Function        |
| ------------------- | ----------------------- |
| `hostname`          | Displays hostname       |
| `uname -a`          | Gets OS, kernel version |
| `cat /proc/version` | Get OS version          |
|         `cat /etc/issue`            |       Get OS Details                  |

---
#### User enumeration

| Command           | Purpose/Function                                    |
| ----------------- | --------------------------------------------------- |
| `whoami`          | Get username                                        |
| `id`              | Gives group info(admin privs)                       |
| `sudo -l`         | Tells us what we can run as root                    |
| `cat /etc/passwd` | Displays all users (passwd file)                    |
| `cat /etc/shadow` | Get password hashes (shadow file)                   |
| `cat /etc/group`  | Get group info                                      |
| `history`         | Shows previous commands entered in terminal by user |
| `sudo su `        | To Switch users                                     |                  |                                                     |

---
#### Network enumeration

| Command                | Purpose/Function                        |
| ---------------------- | --------------------------------------- |
| `ifconfig` or `ip a`   | IP address and interface info           |
| `ip route`             | Identify routes                         |
| `arp -a` or `ip neigh` | Which systems does system interact with |
|        `netstat -ano`                |  Open ports and established connections                                       |

---
#### Password hunting

| Command                                                              | Purpose/Function                                |
| -------------------------------------------------------------------- | ----------------------------------------------- |
| `grep --color=auto -rmw '/' "PASSWORD=" --color=always 2> /dev/null` | Hunt for hardcoded passwords and colour code it |
| `locate password`                                                    | Find files with name password                   |
| `find / -name authorized_keys 2> /dev/null`                          | Hunt for authorized_keys                        |
| `find / -name id_rsa 2> /dev/null`                                   | Hunt for id_rsa rsa private keys                                                |

---
#### Automated Tools

| Command                 | Link                                                                                                                                                                                           |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LinPeas                 | [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) |
| LinEnum                 | [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)                                                                                                                 |
| Linux Exploit Suggester | [https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester)                                                                                           |
| Linux Priv Checker      | [https://github.com/sleventyeleven/linuxprivchecker](https://github.com/sleventyeleven/linuxprivchecker)                                                                                       |


---

#### Search for backup folders

`locate  backup` - Finds files and folders named backup