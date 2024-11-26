# Tenten
Tags: #htp #writeup 
Related to: #wordpress #ssh
See also: 

#### Summary
Writeup for ten ten box

#### Steps

- Ran nmap scan to find port 80 and port 22 were open
	- port 80 ran a wordpress site
	- port 22 was ssh
	
- Ran wpscan 
	- discovered a very old plugin jobmanager
	- job manager has idor vulnerability
- Examine site to discover IDOR
	- on inspection we find that http://10.129.1.188/index.php/jobs/apply/8/ - the last number part is the number we can vary to get different titles.
	- We observe the title changes with name
	- we run a simple code in terminal to automate checking the different titles
		- `for i in $(seq 1 20); do echo -n "$i: "; curl http://10.129.1.188/index.php/jobs/apply/$i/ | grep '<title>' ; done`
	- We find different file names including our uploaded file 
	- Another intersting file name was HackerAccessGranted

- Exploit for the CVE was searched and found the exploit can identify file location. We run the exploit to find the HackerAccessGranted.jpg file
- The file upload functionality didn't accept php so we didn't go for shell upload.


- jpg file might contain hidden content so we try `strings` but get gibberish
- use `binwalk` to see anything embedded in image - nothing
- We try `steghide` to find steganography - we extract to get rsa key in image it is encypted.
- 
###### References  (optional )