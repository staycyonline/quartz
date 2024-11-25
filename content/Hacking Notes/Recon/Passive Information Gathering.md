Tags: #template 
Related to: #note-taking, #notes
See also: 
Index: [[📁EJPTv2 - INDEX]]

#### Summary
Walking through passive info gathering tools and methodologies

#### Information Gathering Types
 - Passive
 - Active

#### Passive Information Gathering
- Gathering information with no interaction with the target
- IP address, Directories hidden from search engines
- PII
- Web technologies

#### Web recon
**Host**
Syntax : `host <web-address>`
Provides IP address via DNS lookup

**robots.txt**
File that tells search engines and crawlers not to look at some endpoints 

**sitemap.xml or sitemaps.xml or sitemap_index.xml**
Meant for serach engines - tells it how to index search engine.
Contains list of pages,authors,categories etc

May contain hidden information

**Wappalyzer(Browser plugin)** or **Builtwith(Browser plugin)** or **whatweb(commandline tool)**
Shows what tech is used in web site

**httrack**
allows to download the entire website - can be used to analyze source code.

#### Whois enumeration

**whois** 
Syntax: `whois <domain-name or ip>`

Gives ownership and other information 

#### Website footprinting with netcraft

www.netcraft.com - can be used to gather info reqarding target domain - gets a lot of info discussed perviously

services -> internet data mining -> scrolldown , what site runs ...

#### DNS Recon

**dnsrecon(cli)**
Syntax: `dnsrecon -d <domain-name>`

**dnsdumpster(website)**
dnsdumpster.com -free

#### Web Firewall detection

**wafw00f**
Used to identify web app firewall

Syntax: `wafw00f <domain-name> -a `

#### Subdomain Enumeration
**subfinder** >>>> **sublist3r**

#### Google Dorks - Google hacking

`site:target.com` - limits results to site and its sub domains
`inurl:<search query>` - limits search to query in url 
`*` - can be used as wild for any parameter
`intitle:<search query>` - limits search to query in title of website
`filetype:<filetype>` -  limits search to sites with particular file type
`cache:<domain-name>` - shows webcache of websites/ can use wayback machine instead

Interesting files
auth_user_file .txt , password.txt

**Reference:** [Google hacking database](https://www.exploit-db.com/google-hacking-database)


#### Email harversting with Harvester

**theHarvester - github**
- very powerful tool
- can gather lot of data

#### Leaked Password DBs

- Have I been pwnd
- Dehashed?
- Seclists?
- rock-you.txt
- 
