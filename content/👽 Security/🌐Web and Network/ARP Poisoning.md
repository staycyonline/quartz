Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

#### ARP poisioning MITM


Open wireshark - select interface- start capture

To ensure that packets are not dropped when they flow through our device, we will activate IP forwarding. This allows each packet to be properly forwarded to its intended destination. Specifically, any packets received from the client will be sent to the router, and any packets received from the router will be transmitted to the client without being discarded by our device. The IP forwarding feature can be enabled using the following command:
echo 1 > /proc/sys/net/ipv4/ip_forward

arpspoof - i interface_name -t ip-address-target -r ip-address-impersonated ip