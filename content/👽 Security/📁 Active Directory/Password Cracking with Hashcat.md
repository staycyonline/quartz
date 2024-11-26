hashcat -m 5600 filename /usr/share/wordlists/rockyou.txt --force -O

-m - Module 
5600 is for NTLM v2 - check help for modules

different wordlists - look for seclists

-O for optimize
--force to force running on CPU (optional)