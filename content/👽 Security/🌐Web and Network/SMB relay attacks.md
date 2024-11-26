Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[]] - index location 

#### SMB Relay attacks

Relaying hashes to other devices using SMB and potentially gaining access

#### Pre requsites
- SMB signing must  be disabled on target
- Relayed user should be admin on the machine

#### Performing attack

- In responder.conf(part of impacket) - Turn off SMB and HTTP 
- Start responder
- configure ntmrelayx
- Wait for an event to occur
- We capture the hash when it happens
-  The ntlmrelayx uses the capture creds to login to other machines.
- Once it logins it start dumping sensitive users like  SAM hashes
- 
