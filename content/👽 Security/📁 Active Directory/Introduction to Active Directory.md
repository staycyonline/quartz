# Introduction to Active Directory
Tags: #Active-Directory
Related to: #crtp #oscp #hacking #notes #TCM
See also: 
Index: [[📋AD-Index-Work-Log]]

#### Summary
Gives a brief overview about active directory and related concepts.

#### What is AD ?  
- It is a Directory service for  
	- management  
	- security  
	- interoperability of objects  

Directory of objects, everything is an object.

- Stores info on objects on the network  

- Some types of objects : 
	- Win user  
	- Win server  
	- Email server  
  
#### Components of AD 
- Schema  
	 - Defines objects and attributes  
	 - Attributes are properties of the object

- Query and index mechanism  
	- Searching and publication of obj and properties  

- Global catalog (GC)
	- Contains info about every object in directory  
	- Stored in Domain controller

- Replication Sevice  
	- Distributes info across Domain controllers
	- Makes sure GC is synced across DCs
  
#### Structure  of AD

- At least one forest
- Forest has multiple Domains which has multiple organizational units(OU)  
  ![[Pasted image 20260102102306.png]]
- Forest = security boundary - can contain multiple domains - if one domain is compromised the entire forest is 
- All domains within a forest trust each other
- Each domain can contain multiple OUs

###### References
[Active Directory - Microsoft](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)