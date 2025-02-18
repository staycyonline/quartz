
Dynamic SSH will be required to tunnel traffic via SSH through a server

dynamic port forward 
ssh -D 127.0.0.1:<local_proxy_port> user@<remote_server_ip> - password based auth

ssh -D 127.0.0.1:<local_proxy_port> -i config_file - key based auth

-D for dynamic port forward
local_proxy_port - port opened on my system for proxying
	Will be using this as proxy in Burp


## Running command line tools via SSH proxy
---
Edit the configuration file, /etc/proxychains4.conf, and give the details of the SOCKS5 proxy on the dynamic SSH tunnel.

[ProxyList]
socks5  127.0.0.1 <local_proxy_port>

use proxychains command before any command line tool to run the command through proxy

eg: proxychains nmap (options)

## Running burp via SSH proxy
---
![[Pasted image 20250218132706.png]]

prxyhost: 127.0.0.1
proxyport  <local_proxy_port>

check use SOCKS proxy and start using as usual
Do DNS lookup over SOCKS in case the site doesn't load.
 


