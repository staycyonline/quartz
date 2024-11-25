Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

#### Dumping linux password hashes

We cannot do much with dumped hashes apart from cracking

user info is in /etc/passwd

encrypted passwds stored in /etc/shadow


Hashed Pass prefix can tell you what algo is used to hash

- $1 - MD5 - easy to crack
- $2 - Blowfish - easy to crack
- $5 - SHA-256 - difficult
- $6 - SHA-512 - difficult


Get elevated privs on the host

cat /etc/shadow

or 

hashdump metasploit module for linux

