Tags: #template 
	Related to: #note-taking, #notes, #smb, #eternal-blue #microsoft-ds
See also: 
Index: [[🗂️Index of HTB Writeups]] - index location 


#### Content
Step 1 - Run normal nmap scan, full scan, -sC for default scripts, -sV for service version detection etc

Step 2 - use `-script safe` scripts to run safe tests that may not be default

Here I ran smb-vuln* scripts as I felt SMB could be vulnerable. Found that it is vulnerable to eternal blue MS17-10

![[Pasted image 20230713085602.png]]

The exploit same as [[Legacy✅]]

> Change user name in send and exploit,py to `\\` - But why⁉️


###### References  