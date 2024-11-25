Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

RDP
Can be configured on any port usually 3389

can find if it runs on a port using metasploit module
`auxiliary/scanner/rdp/rdp_scanner`

We need valid creds to get connected with RDP

bruteforce with hydra - `hydra -L user-list -P password-list rdp://host-ip -s port`

use xfreerdp to connect to rdp
`xfreerdp /u:username /p:password /v:host-ip:port` 

See: [[Blue Keep]]