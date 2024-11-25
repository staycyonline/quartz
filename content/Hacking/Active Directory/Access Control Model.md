# Access Control Model
Tags: #Active-Directory #crtp  
Related to: #hacking #bug-bounty #TCM #crtp #oscp #enumeration 
See also: 
Index: [[🗂️ Index of CRTP]]

#### Summary
A brief overview of what the content is

#### Access Control Model
- Enables control on the ability of a process to access resources and objects in AD based on
	- Access Tokens (of process)
		- Consists of Identity and
		- Privilages of user

	- Security Descriptors (of object)
		- SID of owner
		- Discretionary ACL (DACL) - Who has access
		- System ACL (SACL) - Controls logging of success and failure etc

#### Structure of ACL
![[ACL.png]]
- Every object in AD has a security descriptor which consists of SACL DACL and Owner info
- Every DACL contains set of Access Control Entries (ACE) which is known as Access Control List (ACL) 

##### Important Properties
- ObjectDN - Object Distinguished name
- Identity reference - Which users have permissions on the object?
- ActiveDirectoryRights - What permissions do they have?
- InheritedObjectType
- AccessControlType
- InheritanceFlags
- ObjectID - SID of Object
###### References  (optional )