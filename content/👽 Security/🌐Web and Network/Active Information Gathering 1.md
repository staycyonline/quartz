Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]]

#### Summary
Walking through active info gathering tools and methodologies


#### Active Information Gathering

#### DNS Zone transfers

- DNS interrogation - process of interrogating a DNS server to provide DNS records specific domain
- DNS zone fiiles are transfered between form one DNS server to another using zone trasnfered - can be abused if left insecured
- zonetransfer.me can be used for labs
- **dnsenum** - can be used to enumerate dns both passive and active
- hosts file - /etc/hosts - can be used to map any domains to ip addresses

- Zone transfer must be enabled on nameservers to perform zone transfer. Can be done using **dnsenum**

#### Performing zone tranfer with dig
**dig** - perfered tool
Syntax: `dig axfr nameserver domain`

- Zone transfer can reveal details of internal IPs and portals 

#### Fierce tool

**fierce**
fierce -dns example.com

#### Host discovery - nmap

- -sn - ping sweep 

#### Netdiscover - for host discovery

`sudo netdiscover -i interface name -r subnet`

#### Portscanning

nmap 
- normal scan
- tcp full scan
- udp port scan


