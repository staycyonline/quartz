# Enumeration Cheatsheet AD
Tags: #Active-Directory #cheatsheet #enumeration  
Related to: #crtp #hacking #oscp 
See also: [[Introduction to Active Directory]]
Index: [[🗂️ Index of CRTP]]

#### Enumeration

Note - `<pipe symbol>` = `|`

**Enumeration of [[Domain Enumeration|Domains]]**

| Function / Action                                                   | Command on Powerview                            | Command on MS AD Module                                      |
| ------------------------------------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| Get current domain                                                  | `Get-NetDomain`                                 | `Get-ADDomain`                                               |
| Get object of the mentioned domain (_where we have trust to do so_) | `Get-NetDomain -Domain <domain name>`           | `Get-ADDomain -Identity <domain name>`                       |
| Get domain SID for current domain                                   | `Get-DomainSID`                                 | `(Get-ADDomain).DomainSID`                                   |
| Displays Domain policies                                            | `Get-DomainPolicy`                              | `-`                                                          |
| Shows system access policy details of our current machine           | `(Get-DomainPolicy)."system access"`            | `-`                                                          |
| Show `<policy name>` policy details of our current machine          | `(Get-DomainPolicy)."<policy name>"`            | `-`                                                          |
| Get domain controller details                                       | `Get-NetDomainController`                       | `Get-ADDomainController`                                     |
| Get domain controller details of particular domain                  | `Get-NetDomainController -Domain <domain name>` | `Get-ADDomainController -DomainName <domain name> -Discover` |

**Enumeration of Users**

| Function/Action                                                           | Command on Powerview                                          | Command on MS AD Module                                                                                                   |
| ------------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Get list of users in the current domain                                   | `Get-NetUser`                                                 | `Get-ADUser -Filter * -Properties *`                                                                                      |
| Get properties of user "student1"                                         | `Get-NetUser -Username student1`                              | `Get-ADUser -Identity student1 -Properties *`                                                                             |
| Get cn property of all users from all properties                          | `Get-NetUser <pipe symbol> select cn `                        | ```Get-ADUser -Filter * -Properties * <pipe symbol> select Name```                                                        |
| List the properties available for users                                   | `Get-UserProperty `                                           | `Get-ADUser -Filter * -Properties * <pipe> select first -1 <pipe> Get-Member - MemberType *Property <pipe> select name`   |
| List password last set property for all users ==(useful to find decoys)== | `Get-UserProperty -Properties pwdlastset `                    | `Get-ADUser -Filter * -Properties * <pipe> select name, @{expression={[datetime]::fromFileTime($_.pwdlastset)}}         ` |
| List bad password count for all users ==(useful to find decoys)==         | `Get-UserProperty -Properties badpwdcount`                    | `Get-ADUser -Filter * -Properties * <pipe> select name, @{expression={[datetime]::fromFileTime($_.badpwdcount)}}        ` |
| Search for a userfield with interesting information (here - description)    | `Find-UserField -SearchField Description -SearchTerm "built"` | ```Get-ADUser -Filter 'Description -like "*built*"' -Properties Description <pipe symbol> select name, Description```                                                                                                                           |

**Enumeration of Computer objects** 

| Function/Action                                                                                                                              | Command on Powerview                               | Command on MS AD Module                                                                                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Get a list of computers in the current domain  ==(Shows computer objects - need not imply there is an actual machine)==                      | `Get-NetComputer`                                  | `Get-ADComputer -Filter * <pipe> select Name`                                                                                            |
| Get a list of computers in the `<target domain>`  ==(Shows computer objects - need not imply there is an actual machine)==                   | `Get-NetComputer -Domain <Target Domain>`          |                                                                                                                                         | 
| Get a list of computers in the current domain having OS Server 2016 ==(Shows computer objects - need not imply there is an actual machine)== | `Get-NetComputer -OperatingSystem "*Server 2016*"` | `Get-ADComputer -Filter 'OperatingSystem -like"*Server2016*"' -Properties Operating System <pipe> select Name, OperatingSystem`         |
| Get all non null properties of computers in current domain                                                                                   | `Get-NetComputer -FullData`                        | `Get-ADComputer -Filter * -Properties *`                                                                                           |
| Ping machines in the domain to check if machine is up ==(ICMP Ping - can return false results if ICMP is filtered out in firewall)==         | `Get-NetComputer -Ping`                            | `Get-ADComputer -Filter * -Properties DNSHostName <pipe> %{Test-Connection -Count 1 -ComputerName $_.DNSHostName}`                     |
                                                                                                                            
**Enumeration of Groups**

*Domain groups*

| Function/Action                                    | Command on Powerview                                     | Command on MS AD Module                                         |
| -------------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------------------- |
| Get all groups in current domain                   | `Get-NetGroup`                                           | `Get-ADGroup -Filter * <pipe> select Name`                      |
| Get all groups in `<target domain>`                | `Get-NetGroup -Domain <targetdomain>`                    |                                                                 |
| Get full data on groups in current domain          | `Get-NetGroup -FullData`                                 | `Get-ADGroup -Filter * -Properties *`                           |
| Get all groups containing word admin in group name | `Get-NetGroup *admin*`                                   | `Get-ADGroup -Filter 'Name -like "*admin*"' <pipe> select Name` |
| Get all members of Domain Admins group(change Domain admin to Enterprise Admin to get enterprise admin)             | `Get-NetGroupMember -GroupName "Domain Admins" -Recurse` | `Get-ADGroupMember -Identity "Domain Admins" -Recursive`        |
| Get all membership details of user "student1"      | `Get-NetGroup -UserName "student1"`                      | `Get-ADPrincipalGroupMembership -Identity student1`             |
                                                   |                                                          |                                                                 |

_Note : Enterprise admins, Schema admins  or any Enterprise groups will be only visible to Forest Root_ 

_Note2 : We can always have groups that are part of a group - check IsGroup Parameter of Group object to confirm_

_Note3 : If Default Admin account is enabled we can identify using the MemberSID which is DomainSID-UniqueNumber which is 500 for default admin_

_Note4 : Recursive keyword instructs the module to look inside groups that are part of the group as mentioned in Note2_

*Local Groups* 

| Function/Action                                                                                             | Command on Powerview                                                    | Command on MS AD Module |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------- |
| List local groups (Needs Admin Priv on non-dc machines)                                                     | `Get-NetLocalGroup -ComputerName dcorp-dc.dollarcorp.local -ListGroups` |                         |
| Get members of all local groups on a machine (Needs Admin Priv on non-dc machines)                          | `Get-NetLocalGroup -ComputerName dcorp-dc.dollarcorp.local -Recurse`    |                         |
| Get actively logged users on a computer (need local admin rights on the target)                             | `Get-NetLoggedon -ComputerName <server name>`                           |                         |
| Get locallly logged users on a computer (needs remote registry on target - started by default on server OS) | `Get-LoggedonLocal -ComputerName dcorp-dc.dollarcorp.moneycorp.local`   |                         |
| Get the Last Logged On on a computer (needs admin priv and remote registry on target)                       | `Get-LastLoggedOn -ComputerName <servername>`                           |                         |
                                                                                                                                                                                                                                                                                                                                                          
**Enumeration of Shares and files** 

| Function/Action                            | Command on Powerview                                                      | Command on MS AD Module |
| ------------------------------------------ | ------------------------------------------------------------------------- | ----------------------- |
| Find shares on hosts in current domain     | `Invoke-ShareFinder -Verbose -ExcludeStandard -ExcludePrint - ExcludeIPC` |                         |
| Find sensitive files on computer in domain | `Invoke-FileFinder -Verbose`                                              |                         |
| Get all fileservers of the domain          | `Get-NetFileServer`                                                       |                         |
                                                                                                                                           

**Enumeration of [[Group Policy|Group Policy Objects(GPO)]]** 

Group policies are applied on Organizational Units (OU)

| Function/Action                                                                                          | Command on Powerview                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Get List of Group policy object(GPO) in current domain                                                   | `Get-NetGPO`                                                                    |
| Get List of Group policy object(GPO) for a particular computer                                           | `Get-NetGPO -ComputerName dcorp-student1.dollarcorp.moneycorp.local`            |
| Get List of Group policy objects(GPOs) which use restricted groups or groups.xml ==(Interesting users)== | `Get-NetGPOGroup`                                                               |
| Get resutant set of policies(RSoP) on current machine                                                    | `gpresult /R`                                                                   |
| Get users which are in local group of a amachine using GPO                                               | `Find-GPOComputerAdmin -Computername dcorp-student1.dollarcorp.moneycorp.local` |
| Get machines where the given user is member of specific group                                            | `Find-GPOLocation -USerName student1 -Verbose`                                  |
| Get data about OUs in the domain                                                                         | `Get-NetOU -FullData`                                                           |
| Get details of GPO applied on an OU (Get gplink attribute using Get-NetOU)                               | `Get-NetGPO -GPOname "{xxx-xxxx-xxx-gplinkattr-xxx-xxx-xxx}"`                   |                                                                                                        |                                                                                 |

**Enumeration of [[Access Control Model|Access Control Lists (ACL)]]** 

| Function/Action                                             | Command on Powerview                                                                                                       |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Get ACL associated with specific object                     | `Get-ObjectAcl -SamAccountName student1 -ResolveGUIDs`                                                                     |
| Get ACL associated with specified prefix used for search    | `Get-ObjectAcl -ADSprefix 'CN=Administrator,CN=Users' -Verbose`                                                            |
| Get ACL Associated with specified LDAP path used for search | `Get-ObjectAcl -ADSpath "LDAP://CN=Domain Admins, CN=Users, DC=dollarcorp, DC=moneycorp, DC=local" -ResolveGUIDs -Verbose` |
| Search for interesting ACEs                                 | `Invoke-ACLScanner -ResolveGUIDs`                                                                                          |
| Get ACLs associated with specified path                     | `Get-PathAcl -Path "\\dcorp-dc.dollarcorp.moneycorp.local\sysvol"`                                                         |
|                                                             |                                                                                                                            |

**Enumeration of Trusts**

| Function/Action                                     | Command in Powerview                                     | Command in MS AD Module                             |
| --------------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------- |
| Get a list of domain trusts for the current domain  | `Get-NetDomainTrust`                                       | `Get-ADTrust -Filter * `                            | 
| Get a list of domain trusts for a particular domain | `Get-NetDomainTrust -Domain us.dollarcorp.moneycorp.local` | `Get-ADTrust -Identity us.dollarcorp.moneycorp.local` |

**Enumeration of Forests**

| Function/Action                                  | Command on Powershell                         | Command on AD Module                                          |
| ------------------------------------------------ | --------------------------------------------- | ------------------------------------------------------------- |
| Get details about the current forest             | `Get-NetForest`                               | ` Get-ADForest `                                              |
| Get details about a particular forest            | `Get-NetForest -Forest eurocorp.local`        | `Get-ADForest -Identity eurocorp.local`                       |
| Get details about domains of the current forest  | `Get-NetForestDomain   `                      | `(Get-ADForest).Domains  `                                    |
| Get details about domains of a particular forest | `Get-NetForestDomain -Forest eurocorp.local`  |                                                               |
| Get all global catalogs for the current forest   | `Get-NetForestCatalog `                       | `Get-ADForest <pipe> select -ExpandProperty GlobalCatalogs`   |
| Get all global catalogs for a particular forest  | `Get-NetForestCatalog -Forest eurocorp.local` |                                                               |
| Map trusts of a forest                           | `Get-NetForestTrust`                          | `Get-ADTrust -Filter 'msDS-TrustForestTrustInfo -ne "$null"'` |
| Map trusts of a particular forest                | `Get-NetForestTrust -Forest eurocorp.local`   |                                                               |

_Note: We can run all kinds of enumeration discussed before on a trusted domain from the foothold machine_

**User Hunting (bit intrusive and noisy in nature)**  

| Function/Action                                                                                                        | Command on Powerview                                             | Command on MS AD Module |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ----------------------- |
| Find all machines on current domain where current user local admin access(refer 1)                                     | `Find-LocalAdminAccess -Verbose`                                 |                         |
| Find all local admins on all machines of the domain (need admin priv in non-dc machines) (refer 2)                     | `Invoke-EnumerateLocalAdmin -Verbose`                            |                         |
| Find computers where a domain admin (or specified user/group) has sessions (refer 3)                                   | `Invoke-UserHunter` or `Invoke-UserHunter -GroupName "RDPUsers"` |                         |
| Confirm Admin access                                                                                                   | `Invoke-UserHunter -CheckAccess`                                 |                         |
| Find computers where a domain admin is logged in (Stealth mode - less chance of success also less chance of detection) | `Invoke-UserHunter -Stealth`                                                                 |                         |

1.  ![[localadmin.png]]

This can also be done with remote admin tools like WMI and powershell remoting. Esp. in cases where RPC and SMB used by Find-LocalAdminAccess are blocked.

See script ==Find-WMILocalAdminAccess.ps1==

This script uses WMI query to know if we have local admin access. Local admin priv is needed for running WMI query.

Finding local admin access is very noisy and triggers events 4624(logon event) and 4634(logoff event)

==Run the command in chunks of less than 200==

2. ![[localgroup.png]]
3. ![[invokeuserhunter.png]]
