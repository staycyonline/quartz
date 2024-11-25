- Identity and access management
- Aws account by default is root  - very powerful should be kept secret

- can create people and group together and set permissions for group

- one person can be part of more than one group

- permissions to resources are given based on org policy 

-----------------

#### Creating IAM users and groups

- Root user has all permissions - best create an  admin account
-  User -> create user  
- Add user to group and use administrator access policy to give admin access to an account
- ![[Pasted image 20230131104348.png]]

------
#### IAM policies

- Group policies - all members inherit the policy
- Individual policy - applies to only that person

##### Policy Structure
Consists of 
- Version - -policy language version - always include 2012-10-17
- Id - identifier for policy - optional
- Statement - required
	-  Statement consists of 
		- Sid - statement identifier - optional
		- Effect - allow or deny access
		- Principal - account or group or role or user the policy is applied to
		- Resource list - list of resources the acctions applied to
		- Conditions - conditions under which it takes effect -opt
		
#### Example admin access policy

![[Pasted image 20230131105552.png]]

---
#### Password Policy

- Min length
- Char types
- Password expiration
- password reuse prevention
- MFA
	- virtual mfa device - authenticator
	- u2F KEY - UBIKEY
	- Hardware key

- IAM - account settings - change password policy 
- Account name- security credentials - MFA