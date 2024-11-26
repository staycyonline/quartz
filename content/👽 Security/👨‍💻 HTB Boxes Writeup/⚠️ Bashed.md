Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[🗂️Index of HTB Writeups]] 

- Ran normal Nmap Scan
![[Pasted image 20230713230044.png]]

- We have a web service running
- Apache 2.4.18
Full scan also gives same result. 

- Checked for vulns in Apache version - found nothing worthwhile

- Examine the site...

![[Pasted image 20230714071858.png]]

Says that he developed on this **exact same server**. So it should be somewhere here....

I ran dirb with the default wordlist

![[Pasted image 20230714072056.png]]

Found few directories with the directory listing vulnerability....

So I went on to manually check these and voila!

http://10.10.10.68/dev/phpbash.php - we got the shell we were looking for

#### We have a limited user shell

flag was in /home/arexxel

We see the shell breaking at times so it isn't relaible

Tried a bunch of reverse shells on keyboard. Better to upload a reverse shell

using `usr/share/laudanum/php/php-reverse-shell.php

to redo...
`
==Learn to use VI==




###### References  (optional )