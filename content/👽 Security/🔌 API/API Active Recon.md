Tags: [#api](app://obsidian.md/index.html#api) [#recon](app://obsidian.md/index.html#recon)  
Related to: [#hacking](app://obsidian.md/index.html#hacking)  
See also:  [[API Recon]]
Index: [Index of API Hacking](app://obsidian.md/Index%20of%20API%20Hacking)

#### nmap

- for service detection and running default scripts: 
	``$ nmap -sC -sV [target address or network range] -oA nameofoutput
- All port scan
	``$ nmap -p- [target address] -oA allportscan
- perform http enum
	`$ nmap -sV --script=http-enum <target> -p 80,443,8000,8080`

#### OWASP Amass
 - Before diving into using Amass, we should make the most of it by adding API keys to it.
 -  `amass enum -list` this command shows data sourses used for enum
 - `$ sudo curl https://raw.githubusercontent.com/OWASP/Amass/master/examples/config.ini >~/.config/amass/config.ini` to make a config file for amass
 - Get keys from sources like censys and add it to config file.
 - Amass has several useful command-line options. Use the intel command to collect SSL certificates, search reverse Whois records, and find ASN IDs associated with your target. Start by providing the command with target IP addresses

 - `$ amass intel -addr [target IP addresses]`

- If this scan is successful, it will provide you with domain names. These domains can then be passed to intel with the whois option to perform a reverse Whois lookup:

`$ amass intel -d [target domain] –whois`

This could give you a ton of results. Focus on the interesting results that relate to your target organization. Once you have a list of interesting domains, upgrade to the enum subcommand to begin enumerating subdomains. If you specify the *passive option, Amass will refrain from directly interacting with your target*:

`$ amass enum -passive -d [target domain]`

The active enum scan will perform much of the same scan as the passive one, but it will add domain name resolution, attempt DNS zone transfers, and grab SSL certificate information:

`$ amass enum -active -d [target domain]`

To up your game, add the -brute option to brute-force subdomains, -w to specify the API_superlist wordlist, and then the -dir option to send the output to the directory of your choice:

`$ amass enum -active -brute -w /usr/share/wordlists/API_superlist -d [target domain] -dir [directory name]`

#### Directory Brute Force with Gobuster

The following example uses an API-specific wordlist to find the directories on an IP address:

`$ gobuster dir -u target-name.com:8000 -w /home/hapihacker/api/wordlists/common_apis_160`

If you would like to ignore certain response status codes, use the option -b. If you would like to see additional status codes, use -x. You could enhance a Gobuster search with the following:

`$ gobuster dir -u ://targetaddress/ -w /usr/share/wordlists/api_list/common_apis_160 -x 200,202,301 -b 302`

Gobuster provides a quick way to enumerate active URLs find API paths.

#### Kiterunner

While directory brute force tools like Gobuster/Dirbuster/ work to discover URL paths, it typically relies on standard HTTP GET requests. Kiterunner will not only use all HTTP request methods common with APIs (GET, POST, PUT, and DELETE) but also mimic common API path structures.

You can perform a quick scan of your target’s URL or IP address like this:

`$ kr scan HTTP://127.0.0.1 -w ~/api/wordlists/data/kiterunner/routes-large.kite`

If you want to use a text wordlist rather than a .kite file, use the brute option with the text file of your choice:

`$ kr brute <target> -w ~/api/wordlists/data/automated/nameofwordlist.txt`

One of the coolest Kiterunner features is the ability to replay requests. Thus, not only will you have an interesting result to investigate, you will also be able to dissect exactly why that request is interesting. In order to replay a request, copy the entire line of content into Kiterunner, paste it using the kb replay option, and include the wordlist you used:

`$ kr kb replay "GET     414 [    183,    7,   8]https://192.168.50.35:8888/api/privatisations/count0cf6841b1e7ac8badc6e237ab300a90ca873d571" -w ~/api/wordlists/data/kiterunner/routes-large.kite`

#### DevTools

- Most underrated toool
- Use network tab in devtools
- Can be used to change and replay requests, Quickly find endpoints 
- Can copy and send stuff to postman using copy command copy as curl and importing as raw text in  postman
 