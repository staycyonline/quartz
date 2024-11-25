Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]] 

#### Summary
tshark -r pacap_file.pcap -Y 'http'  - view http traffic alone

tshark -r pacap_file.pcap -Y 'ip.src== ip-address && ip.dst== ip-address' - find traffic from src ip and dst ip

tshark -r pacap_file.pcap -Y 'http.request.method == GET' - get all GET requests

tshark -r pacap_file.pcap -Y 'http.request.method == GET -Tfields -e frame.time -e ip.src -e http.request.full_uri' - get all GET requests and show only time, src ip and full url fields

tshark -r pacap_file.pcap -Y  'http contains password' - shows packets that contains password

tshark -r pacap_file.pcap -Y 'http.request.method == GET && http.host == www.nytimes.com -Tfields -e ip.dst' - show dst address for get requests set to ny times website

tshark -r pacap_file.pcap -Y  'ip contains amazon.in && ip.src=ip-address' -Tfields -e p.src -e http.cookie -  gives out src address and cookie of sessions with amazon.in from given ip address

tshark -r pacap_file.pcap -Y  'ip.src== ipaddress && http' -Tfields -e http.user_agent - shows user agent of IP address