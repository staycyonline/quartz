# Introduction to Active Directory
Tags: #Active-Directory
Related to: #crtp #oscp #hacking #notes #TCM
See also: 
Index: [[CRTP/🗂️ Index of CRTP]]

#### Summary
Gives a brief overview about active directory and related concepts.

#### What is AD ?  
- It is a Directory service for  
	- management  
	- security  
	- interoperatablilty of objects  

- Stores info on objects on the network  

- Some types of objects : 
	- Win user  
	- Win server  
	- Email server  
  
#### Components of AD 
- Schema  
 - Defines objects and attributes  

- Query and index mechamism  
	- Seraching and publication of objs and properties  

- Global catalog  
	- Contains info about every object in directory  
- Replication Sevice  
	- Distributes info across domain controllers  
  
#### Structure  of AD
- Forest, Domains and organizational units(OU)  
  
- Forest = security boundary - can contain multiple domains  
- Each domain can contain multiple OUs

###### References
[Active Directory - Microsoft](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)