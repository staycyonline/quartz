Anonymous login
```sh
┌──(kali㉿kali)-[~]
└─$ rsync --list-only  10.129.28.121::    #list remote host with anon login
public         	Anonymous Share
                                                                                                         
┌──(kali㉿kali)-[~]
└─$ rsync --list-only  10.129.28.121::public    #list folder within remote host
drwxr-xr-x          4,096 2022/10/24 18:02:23 .
-rw-r--r--             33 2022/10/24 17:32:03 flag.txt
                                                                                                         
┌──(kali㉿kali)-[~]
└─$ rsync 10.129.28.121::public/flag.txt ./flag.txt #download flag.txt to local host
                                                                                                         
┌──(kali㉿kali)-[~]
└─$ cat flag.txt
72eaf5344ebb84908ae543a719830519

```
