## What is cloud pentest
---
Pentesting services in cloud that target users.
Good addition with web app pentest .

## Why cloud pentest
---
Even if web app is secure, the cloud may be misconfigured which can lead to compromise

## AWS overview
---
Leading cloud provider 31% share
Has a lot of services

## Common services
---
S3
EC2 
RDS
etc

## Shared responsibility
---
> Platform is responsible for security of the cloud. User is responsible for security in the cloud

## Account ID
---
All resources are associated with the account ID
Helps to corelate results

Root credential compromise - Critical Vulnerability

## AWS regions
---
Regions can help us focus on enumeration

Lot of resources are exposable
with Account ID you can find resources exposed

## Demo 1 - Find Exposed services using AWS 

![[Pasted image 20240601103728.png]]

seach for AMI -> change option to public images and paste the account number or Owner = account number to list resources associated with the Account ID

## AWS IAM
---
IAM Policies - says what is allowed and not allowed
It allows and denies actions and access to resources

AWS does Deny by default

> IAM Access key ID can be used to find target account ID even if key is revoked or no access is to secret key

![[Pasted image 20240601104618.png]]


Most compromise is due to credential leaks

Github gitlab
s3 buckets
js files
 apks
container registeries (very lucrative to find keys) -  dockerhub, public ecr ,quay.io

## How to validate leaked creds
---
Password spraying
```sh
aws sts get-caller-identity
```

Finds permisiions of leaked creds

enumerate-iam - very noisy for red team

## Demo 2
---
**

Permissions of leaked credentials - find the following:

1. Account ID the user belongs to
    
2. Name of the user
    
3. Permissions of the user
    

**

1
![[Pasted image 20240601105414.png]]

2
![[Pasted image 20240601110906.png]]


3
![[Pasted image 20240601105931.png]]

## IAM Roles
---

i am roles are temproary creds
trust relationship

> if you have `iam:PassRole On *` then you can run resources using admin access get priv esc

https://rhinosecuritylabs.com/aws/aws-privilege-escalation-methods-mitigation/

Pro tip: Find roles that are most permissive and see which users can reach it

To lookup - PassRole IAM Roles


## Amazon s3
---
Buckets
Unique name globally
Region specific
Used for - user uploads, static content, serve website, logs etc

bucket url has pattern

s3 bucket should have same name as the dns record

> Public s3 can be used to find which region is the target using 

Greyhat warfare
OSINT Public buckets
IaC in public repora
Google Dorks
Presigned URL - with AKIA (s3 buckets)

Coomon issues
Public list
Public read
Public write

## Demo 3
---
Detecting account id from public bucket

![[Pasted image 20240601120412.png]]

![[Pasted image 20240601120936.png]]

![[Pasted image 20240601120635.png]] 


https://tracebit.com/blog/2024/02/finding-aws-account-id-of-any-s3-bucket/
---
Bucketloot - get sensitive data


---
## EC2
---
Virtual machines
Must be within a VPC
Allows SSH and RDP for windows
Every VM should have 1 private IP

EC2 - AMI (for operating sys), Elastic Block Storage (Persistant storage), Security groups(Like firewall), EC2 Key Pairs, User Data scripts(initialing scripts)

Given an IP we can get if it is  aws
ip-ranges.amazonaws.com/ip-ranges.json 


## IMDS
---
temp creds from IMDS is as dangerous as IAM roles associated with EC2

## Demo 4 - Exploring IMDS v1

![[Pasted image 20240601122427.png]]
![[Pasted image 20240601122404.png]]

![[Pasted image 20240601122813.png]]
![[Pasted image 20240601123022.png]]

## Demo 5 - Exploring IMDS v2
---


## Demo 6 - Exposed AMIs
---

# EBS
---
Storage
has snapshots
can be found using account id
has a lot juicy data like source code, sensitive info

---
![[Pasted image 20240601124617.png]]

not encrypted  - we can use it mostly

## Exploring metadata endpoint in ECS
---
ECS, Fargate



## ECR
---
Compromising container image == compromising the cluster

Public ECR Registries - https://gallery.ecr.aws

AWS Inspector doesn't scan for secrets and sensitive data inside containers


## AWS Lambda
---
Max lifetime is 15 mins

lambda will be kept alive for 15 mins after first call and kills other calls 
no metadata endpoint
read only file system
/tmp is writable

lambda exposed via api gateway - cannot be 100% sure
lambda exposed via lambda url - sure!

lambda has a 1000 concurrent executions - by new accounts only has 10 lambda - no protection against dos. requests can get throttled

![[Pasted image 20240601144107.png]]

temp creds are always avaialble in env varriables during execution phase
no metadata endpoint
## Offensive cloud security
---
Recon
- Account Id and regiom
- Subdomains and domains

Initial Access
- Public resources
- Leaked creds and secrets
- server side vulnerabilities

Priv esc and lateral movement
 - Private resources in VPC
 - Priv esc techniques (metadata, secrets,linux priv esc, etc)

Data Exfiltration
 - Data from private repos

# What to do
---
Try to read secrets
- secrets manager
- ssm param store

Scan internal VPCs

Get admin account
If compromised non prod? try for prod access

## Tools
---
Scoutsuite by ncc group - pentesters' friend
prowler - more defensive friendly
pacu - aws expoitation framework - like metasploit for aws


Mitre attack cloud matrix - going deep

setup vulnerablre machines and hack

---
terraform


ctf
---
![[Pasted image 20240601161820.png]]
![[Pasted image 20240601161900.png]]
---
![[Pasted image 20240601170801.png]]


create a volume from snapshot, find using acc id then mount and find flag

https://medium.com/@mudasirhaji/step-by-step-process-of-how-to-add-and-mount-ebs-volume-on-ubuntu-ec2-linux-instance-a4be8870a4dd
https://docs.aws.amazon.com/ebs/latest/userguide/ebs-using-volumes.html

![[Pasted image 20240601170719.png]]
---
![[Pasted image 20240601171338.png]]

![[Pasted image 20240601171259.png]]

![[Pasted image 20240602152719.png]]

![[Pasted image 20240602155327.png]]


---
![[Pasted image 20240601174613.png]]
![[Pasted image 20240601174636.png]]

----
![[Pasted image 20240601212532.png]]



Find associated AMI using account id discovered in the previous challenge

![[Pasted image 20240601222101.png]]

Spin the instance with the AMI as base

![[Pasted image 20240601222143.png]]

---
![[Pasted image 20240602012319.png]]

https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/directory-list-lowercase-2.3-small.txt

![[Pasted image 20240602012006.png]]

try browsing browser

![[Pasted image 20240602014540.png]]

try ssrf in this endpoint

user-data endpoint has file which contains flag
![[Pasted image 20240602014624.png]]

---

![[Pasted image 20240602020046.png]]
![[Pasted image 20240602152249.png]]

![[Pasted image 20240602015953.png]]

![[Pasted image 20240602015931.png]]

```sh
{
  "Code" : "Success",
  "LastUpdated" : "2024-06-01T20:16:48Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "ASIAYS2NTMFYVQ3POKNP",
  "SecretAccessKey" : "HO1zRjOmE4K/15Nq09BImwASgVP0S6A+ithhp7cj",
  "Token" : "IQoJb3JpZ2luX2VjENz//////////wEaCmFwLXNvdXRoLTEiSDBGAiEAqoRbujYr4PaCZU2ynFvVjfIQRDV8NTxcsZv7QCBwwocCIQCGKfcaK950QwoSo4oeqtV+3Q+9fHcyq1+6jlHLm/bYUCrKBAhlEAAaDDU5MDE4Mzg4MzEyMSIMTtFUZpICEsnjZmU7KqcESKfGRXuas2/IZkzJqa2VncLpJQka0WdrIEXIDjlOrPCRtWoCOhzh5a+rZj3Nm9b2AplN9LBpFR8R65qTadFo8IJLIG2dKjpeWx2NzI1j2mQrZE2g79WRXZ15ewyOidpJGjNLd77kFx8BVz4RuRRldXX3sFYbylXlpVJvsSToi19fs9il0TCX3GJCFf3E36mJNaGxfynwhmSsvoEY2tODSVQTqF0dDpMzS7r5/+lg1iuoXXSqcDokkN4CbmFh/LVhy0LW8GvBN8mYjVA/2SKAtvVtGGjSfpsS7YjegvDx9Rp3uWgAyjekgQsyHUtPw3ds6kjlr1KHsgli4U3l9YoEq0afpzeBa4gzsiAdwLPqo6oTAUiB5E4ZOWeRcJ59kmvZ/UH6jf7cPCIoqztpcA+cmnlkachdtakMLIPLbbPY5J22ZW/8NXzDE6XO2bTR/ZbjMxsd4jDvUVz1AZBbWjBhLA7bD0VyHlL93JCKS8v0jC991EBWnLP9NpIPGyzDnoEAiA46oD4C+etgDbsflPL82RfM7zfPfP6nLqc16/Dquf4R7+GWrMimdWTagkeupB3NLQ1fWXlyhZ+bEFOSfKfOkB9Q8eyuEKM5EAwAKhWAYKnQiVjQPpA9N8YTF+6S7naZeBogpHrNNLGO0Q6ricfG9OaOfLhMwXrgG1drOe6nvwkcKcKl0YWxJ4wMLIN9gkL83Kr4CPV+Zq2vainOd5lW0+dHurFE5jAwjoPusgY6kgJHiVarIRJWOZIZK8/LBThS2IRB6FBTD246eXkrkLblYXZDbhhdMoZlA14mEVOhEotk5MZvz5TvlElKLmwTPJk7gd7iTtiacr4ZF4BHhX2YpwFywt/EGHSyTpRIFObyQAZnOg5Fs5cveI1YUdih3CO2FxzSvItZ4K3QAaEPz0vj7bndHGb+xBEfcmlBq8UCKtWlxUQZcDWkeuVsL2fQ0S+yL6XGLk7h2Mo1vYHzB/kPADf3w+A2OkD4tz49FvVHu1BfXoGUTkv0v2QKBdHH0UDc8RfsY7y4PS58O6c6Ky4YF+KFQuDpwGfbYzBnKP+1kyHLAWN99zu0Sl8oWHS+aTDpEYWitcS9+VzaR4XvXmRkP/nA",
  "Expiration" : "2024-06-02T02:27:37Z"
}
```

![[Pasted image 20240602024345.png]]

```sh
{
  "Code" : "Success",
  "LastUpdated" : "2024-06-01T20:16:56Z",
  "Type" : "AWS-HMAC",
  "AccessKeyId" : "ASIAYS2NTMFYRTGQ5MS3",
  "SecretAccessKey" : "FAth6aaxr4QLFrKe3cOkB8mfsq7vLvFtjZN7BXFw",
  "Token" : "IQoJb3JpZ2luX2VjENz//////////wEaCmFwLXNvdXRoLTEiRzBFAiAHh3HIq4LMWcUSN1Lh+oDw5znAattbM5Tk3ibpr8BZFwIhAJNY2eXRFoYYVEVrqZ3Of6RZtN4b7C7FJMDTpw5oKa7vKsAFCGUQABoMNTkwMTgzODgzMTIxIgzImaxgGkq3HPFD7oUqnQX7NmOH8qfT5HfwNM4R0RnpP6aP3hP2lbBHOikaayu7dG1zxWdQHQgdWe+Dutxj9KkDxAocoYH+nqm5lBDxat6YliSNMkJyDR4YKcK79KaS/wsta8U+XHsOGUIJslUNnIP49W0/+wYoOJXCJgpxB6zGK6bb4T7kHoNF+q9zcN1IkTwCn5obQrCHHATYKVqRDaGAq7toSOHJjVOzueYNWvtP4pwSTQf8/rkoMT7BuxbObHTxb317YSa+2RNOHZEqk6YYL9Ve6knRO+LnV+tX7qO3vmzwsg6i1rKTkGcbAa/oOiRTgBY4SYFZY4nQItO0pPbYwJ7A/FZFFghtSDXL1zfmz9AmiCJUJgJlg+jiUSrqf0KuN01B6Y3KE+60EUGHzS4VT3EhbKnSAFnS21oRbAQpQRWMUQYJkzoVch4xugRPnDgO4/oYfZB+16WTE7PHm6TtRAuWKiERz5Xi/m+1dDwyCe9aYe8bBfSF0ow4Ao3/D4Ae17Q79dks6aTevdxlVNM9EyHCyhpdas05lWbcb5B5t1n9wPxvC0XX8P1zuIP9O7svSvNllG7SSoGYjUCnU71WLcuvwHmg454TgeBVcfrOLjMIJi5q+3LDnbgMpfwXAOOjXzD5/DpmqsIW24kcXtgatLuKYERrI1UMLIESmU8khJekt8DWL0WCZm+LZljYEHf4rNUyB+71PUIAdQ9i3p+gMudUrmOE5Im7YTZAJ2xUGrJZMWVFuIEknF54CZPK0t3BD8Cmgxta9rlxEfjJxOEzSl2GIEiU5UTTzkkJJvvej+FqCEIabXlyFr3AH6sIhAuLqGPH56CVKxpWgZ9h4tW3eXfiOni4RtPnSnzRMpOgPypo810Jkhhbtjw8nBdLuqxwZD3jEbggiYNOuPYwjoPusgY6sQHjT1I/t5t+D05xsvDVlsHVwBH8gn1Ll7vrmNEJRItOoJqGT1uOoBQaQo1q3qAr7dLloGVu3cR4aWV66xzNjN7gfXyetYi9afdkYyyPXuhahz4NVvAmHOQxL0v+JuXkD+dVi+U01/BLfvSpOqQwrwFvdF0prDnoZSu7rEPDxuf4Td4N1VrEuuYsbTJILN/LL1YiMB+u0YuxqQ/KNwzQNm842A6ickRmMCteY2xBxknVGFQ=",
  "Expiration" : "2024-06-02T02:32:37Z"
}
```

![[Pasted image 20240602024853.png]]


Should probably query something using ssm - https://docs.aws.amazon.com/cli/latest/reference/ssm/

Something like 
```sh
aws ssm get-parameters --name "/config"
```


![[Pasted image 20240602154942.png]]

with decryption gives flag

![[Pasted image 20240602155210.png]]



---
![[Pasted image 20240602151912.png]]
![[Pasted image 20240602151849.png]]

---
