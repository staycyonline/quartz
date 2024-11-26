#### Find server version and related vulns
#### Dir bust and see if we can find any interesting pages

Example to hunt for PHP files
```sh
gobuster dir -x php  --url http://url -w /usr/share/wordlists/SecLists/Discovery/Web-Content/PHP.fuzz.txt

```

#### Dirbust for CGI bins(Apache server)

Try Shellshock

#### Try enumerating subdomains

