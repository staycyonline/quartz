Tags: #enumeration #ftp #port21 
Index: [[]] - index location 

---
#### Summary
Enumeration Techniques for FTP

---
#### Enumeration using Nmap

###### Service version scan

```sh
nmap -sV -p 21 [target host]
```

###### Aggressive scan ( OS detection, version detection, script scanning, and traceroute)

```sh 
nmap -sV -p 21 -A [target host]
```

###### Nmap Script for checking anonymous login

```sh
nmap -sV -p 21 --script ftp-anon [target host]
```

###### Connecting to ftp host

```sh
ftp [target host]
```
