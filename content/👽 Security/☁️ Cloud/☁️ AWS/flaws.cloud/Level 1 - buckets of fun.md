Tags: #aws #pentesting 
Related to: #s3-buckets 
See also: [[BlackSky Hailstorm AWS]] 
Index: [[]] - index location 


We have a domain flaws.cloud and all challenges are subdomains of the domain.

Lets subdomain enumeration this domain 

That didn;t work.

I checked the hint to find that when a website is hosted as s3 bucket it should match the domain name

>All S3 buckets, when configured for web hosting, are given an AWS domain you can use to browse to it without setting up your own DNS.

So the format should be http://siteurl.s3-website-aws-region.amazonaws.com

Due to permission issues http://flaws.cloud.s3.amazonaws.com/ can also be accessed

Got this 
![[Pasted image 20230719192503.png]]

The last secret-dd02c7c.html is intriguing 

Lets check file

![[Pasted image 20230719192640.png]]

Read: http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/