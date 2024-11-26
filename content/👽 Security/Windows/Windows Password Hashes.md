Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] - index location 

#### Summary
Add a brief overview of what the content is

#### Content
Account password in SAM(Security Accounts Manager) database

Authentication and verification is done through Local Security Authority(LSA)

 windows upto 2003 server - LM and NTLM hash

 windows uses NTLM hases from vista

SAM database - database that is responsible for managing all user accounts and passwords in windows 

db cannot be copied while OS is running

kernel keeps the sam db locked, so attackers use in memory techniques to dump SAM hashes from LSASS process

SAMis encrypted with syskey in modern version of windows

We need an elevated session to dump passwords from LSASS

LM hash
- Splits password into two parts convert to uppercase and concatnates

NTLM(NT Hash)
- Makes MD4 hash of password
- Is case sensitive
- Allows spl characters





###### References  (optional )