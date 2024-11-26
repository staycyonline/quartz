# Privilege Escalation using Feature Abuse
Tags: #privilege-escalation 
Related to:  #Active-Directory #crtp 
See also: 
Index: [[CRTP/🗂️ Index of CRTP]] 

#### Summary
We can locally escalate privilages by exploiting features of popular enterprise appilications

#### Jenkins
- CI tools are usually useful for our purpose - they have ability to run OS level commands 
- Jenkins is widely used CI tool
- They usually run with local admin privilages
- We can look at users and get info on build executer
- There is no brute force protection in Jenkins if it is not integrated with other mechanisms such as Azure AD.
- Jenkins provides script console to admin at /script
- We can run arbritary commands
- If we dont have admin access we can check if accounts have configure access to configure a build in some project - by which we can run OS level commands and windows batch commands
- We can reorder build steps to make our script run first before others if build is successful

###### References  (optional )