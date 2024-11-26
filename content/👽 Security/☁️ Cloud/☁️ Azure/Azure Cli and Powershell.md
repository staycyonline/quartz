https://learn.microsoft.com/en-us/cli/azure/get-started-with-azure-cli

Logged in using provided creds Using Azure Cli

```sh
az login
```

![[Pasted image 20240611212248.png]]

```sh
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "1e3500cc-d08f-42c8-8678-ce352b7de55e",
    "id": "7417f1f8-3d91-451a-a354-966c173efb48",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Mega Multinational",
    "state": "Enabled",
    "tenantId": "1e3500cc-d08f-42c8-8678-ce352b7de55e",
    "user": {
      "name": "ryan_3592@megamultinational.com",
      "type": "user"
    }
  }
]

```



### Azure powershell module
---
installation, Login and basic enum
![[Pasted image 20240612214620.png]]

```powershell
PowerShell 7.4.2
PS C:\Program Files\PowerShell\7> Get-ExecutionPolicy -List

        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process       Undefined
  CurrentUser       Undefined
 LocalMachine    RemoteSigned

PS C:\Program Files\PowerShell\7> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
PS C:\Program Files\PowerShell\7> Install-Module -Name Az -Repository PSGallery -Force
PS C:\Program Files\PowerShell\7> Connect-AzAccount
Please select the account you want to login with.

Retrieving subscriptions for the selection...

[Announcements]
With the new Azure PowerShell login experience, you can select the subscription you want to use more easily. Learn more about it and its configuration at https://go.microsoft.com/fwlink/?linkid=2271909.

If you encounter any problem, please open an issue at: https://aka.ms/azpsissue

Subscription name  Tenant
-----------------  ------
Mega Multinational Mega Multinational

PS C:\Program Files\PowerShell\7> az
az: The term 'az' is not recognized as a name of a cmdlet, function, script file, or executable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
PS C:\Program Files\PowerShell\7> Get-AzSubscription

   TenantId: 1e3500cc-d08f-42c8-8678-ce352b7de55e

Name               Id                                   State
----               --                                   -----
Mega Multinational 7417f1f8-3d91-451a-a354-966c173efb48 Enabled
```


**Check for resources associated with the azure account**

![[Pasted image 20240612211804.png]]

```powershell
PS C:\Program Files\PowerShell\7> Get-AzResource

Name              : financemegamultinational
ResourceGroupName : MegaMultinational
ResourceType      : Microsoft.Storage/storageAccounts
Location          : eastus
ResourceId        : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational
Tags              :

Name              : DemoAutomation-3592
ResourceGroupName : MegaMultinational-3592
ResourceType      : Microsoft.Automation/automationAccounts
Location          : westus
ResourceId        : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592
Tags              :

Name              : DemoAutomation-3592/NewDomain
ResourceGroupName : MegaMultinational-3592
ResourceType      : Microsoft.Automation/automationAccounts/configurations
Location          : westus
ResourceId        : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/configurations/
                    NewDomain
Tags              :

Name              : DemoAutomation-3592/Get-Credential
ResourceGroupName : MegaMultinational-3592
ResourceType      : Microsoft.Automation/automationAccounts/runbooks
Location          : westus
ResourceId        : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/runbooks/Get-Credential
Tags              :

```

**Check for roleassignment associated with the each resource**

Storage account 

```powershell
PS C:\Program Files\PowerShell\7> Get-AzRoleAssignment -Scope '/subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational'

RoleAssignmentName : 4468225b-3909-431d-b1cc-9909c1bda137
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational/providers/Microsoft
                     .Authorization/roleAssignments/4468225b-3909-431d-b1cc-9909c1bda137
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Storage Blob Data Reader
RoleDefinitionId   : 2a2b9908-6ea1-4ae2-8e65-a410df84e7d1
ObjectId           : 4a488700-33bd-4d99-9796-84253d207cd8
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9c81aee9-b0b9-4936-a4a6-9998cc1dc06a
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational/providers/Microsoft
                     .Authorization/roleAssignments/9c81aee9-b0b9-4936-a4a6-9998cc1dc06a
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Reader
RoleDefinitionId   : acdd72a7-3385-48ef-bd42-f606fba81ae7
ObjectId           : 4a488700-33bd-4d99-9796-84253d207cd8
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a623c0b-34bb-4592-b857-f219c771d4e7
RoleAssignmentId   : /providers/Microsoft.Authorization/roleAssignments/1a623c0b-34bb-4592-b857-f219c771d4e7
Scope              : /
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f019c872-9b47-4b12-8b82-3956c6bf3eed
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f019c872-9b47-4b12-8b82-3956c6bf3eed
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : fb18e957-4f42-44a6-9ad7-67c7a54c0da9
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0f5928a5-7c5f-4cc4-991c-59a07976c92b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0f5928a5-7c5f-4cc4-991c-59a07976c92b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : 05b1a670-437e-4f22-b6b8-4d95090f72df
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7390459b-d1ac-47fc-9990-18e4159a0b5b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7390459b-d1ac-47fc-9990-18e4159a0b5b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9ed82813-855f-404f-a399-9f11dab85a63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9ed82813-855f-404f-a399-9f11dab85a63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : aecad497-4a0e-490d-9a10-2911f6cd950a
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4f40060d-b857-4a20-a380-a41cb00229cd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4f40060d-b857-4a20-a380-a41cb00229cd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 6d041734-354c-43ee-9a23-c90853d60cea
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/6d041734-354c-43ee-9a23-c90853d60cea
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : ba196f96-2f12-43cb-824b-5b71057f3c63
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : e2c05e1e-1295-4b65-a803-7034b02c1d63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/e2c05e1e-1295-4b65-a803-7034b02c1d63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3c1b2801-2296-4a4a-9a82-ac69c3c85942
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3c1b2801-2296-4a4a-9a82-ac69c3c85942
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d822c515-7d70-4477-b966-0ac498f6bc39
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d822c515-7d70-4477-b966-0ac498f6bc39
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ae73cb95-1d36-40fd-9091-b5a5802bcbd5
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ae73cb95-1d36-40fd-9091-b5a5802bcbd5
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 31fa7571-f3d1-4c2b-9fac-6acf513ae034
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/31fa7571-f3d1-4c2b-9fac-6acf513ae034
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 990873c7-81a9-4c7a-a215-75440156330b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/990873c7-81a9-4c7a-a215-75440156330b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Reader
RoleDefinitionId   : acdd72a7-3385-48ef-bd42-f606fba81ae7
ObjectId           : 57234839-911a-464f-9929-e643c25bc53e
ObjectType         : Unknown
CanDelegate        : False
Description        : Allow Managed Identity for CycloneBot Read access Azure Subcription for quota assignments.
ConditionVersion   :
Condition          :

RoleAssignmentName : be630824-1d8a-471d-8664-7482a875c0de
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/be630824-1d8a-471d-8664-7482a875c0de
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3ef186c5-4779-4f6c-add8-a14d310c024c
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/3ef186c5-4779-4f6c-add8-a14d310c024c
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 01ccbe02-638f-4ba5-a18f-6765e7cef751
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/01ccbe02-638f-4ba5-a18f-6765e7cef751
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3be5dd06-0382-4bcb-a7d0-15c616ae77af
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/3be5dd06-0382-4bcb-a7d0-15c616ae77af
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : AdminLevelPrivilege
RoleDefinitionId   : df283025-0517-45a9-a014-4d00275d3b66
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : e3602af5-a5b4-4e79-8b98-47401d171376
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/e3602af5-a5b4-4e79-8b98-47401d171376
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0ae02774-b54e-4ecc-b3e7-81f447d1a661
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0ae02774-b54e-4ecc-b3e7-81f447d1a661
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4396c151-e41e-4295-bf55-817861556c40
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4396c151-e41e-4295-bf55-817861556c40
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : AcrPull
RoleDefinitionId   : 7f951dda-4ed3-4680-a7ca-43fe172d538d
ObjectId           : e2a8c36c-8aa4-46db-a927-7567f006cb43
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : b94838f0-f6f7-4b06-9606-5ca2021a1801
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/b94838f0-f6f7-4b06-9606-5ca2021a1801
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : a2a9c9a1-614e-4d3a-9fdb-5021ef46eedc
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5161080b-ed32-49e8-868d-bb78ebbb41a8
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5161080b-ed32-49e8-868d-bb78ebbb41a8
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 284f4c74-4a61-41e4-b357-193166745fe5
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d548b9a6-ed6f-4613-9e49-9d6c95a4a820
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d548b9a6-ed6f-4613-9e49-9d6c95a4a820
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a77ff56-635b-48c8-9ff8-ef01c6b05de9
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/1a77ff56-635b-48c8-9ff8-ef01c6b05de9
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a737b55a-ff7b-4d14-a0c1-9189422ccc45
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a737b55a-ff7b-4d14-a0c1-9189422ccc45
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Management Group Contributor
RoleDefinitionId   : 5d58bcaf-24a5-4b20-bdb6-eed9f69fbe4c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ceb96903-ace9-41ef-ace0-717b4048de80
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ceb96903-ace9-41ef-ace0-717b4048de80
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 6db80a95-947f-4f45-ba81-27de2d1dddc9
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/6db80a95-947f-4f45-ba81-27de2d1dddc9
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 603d382b-de0d-443a-9590-c8c5334f6f98
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/603d382b-de0d-443a-9590-c8c5334f6f98
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 103f9c11-e56b-4b9c-b51b-1252058cb6b6
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 974b835a-6019-4dc1-a2fe-5e90d210ee20
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/974b835a-6019-4dc1-a2fe-5e90d210ee20
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 103f9c11-e56b-4b9c-b51b-1252058cb6b6
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f44781d7-8a7d-48e1-a66c-185b8e52a562
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f44781d7-8a7d-48e1-a66c-185b8e52a562
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 556512b4-56fb-41d1-a355-0467e5e88503
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7e04f165-6735-4d50-9a46-91c859365fc6
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/7e04f165-6735-4d50-9a46-91c859365fc6
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a21feb0a-6ce1-421d-8d5e-d591fc978cb8
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Authorization/roleAssignments/a21feb0a-6ce1-421d-8d5e-d591fc978cb8
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3dff5477-d9d6-435d-aa89-4cce1cccdacd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3dff5477-d9d6-435d-aa89-4cce1cccdacd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : b492fb13-0a69-4aab-ab31-f7426bf49f48
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a823f7be-1b25-463a-9fa1-e859003d02d0
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a823f7be-1b25-463a-9fa1-e859003d02d0
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : efee41da-a5ed-48b3-9ba2-d54f44d08fef
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3082ac2c-2783-496a-d348-ac0a42d00178
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3082ac2c-2783-496a-d348-ac0a42d00178
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9e17abe0-901d-4ac1-4d3c-49831a8e7592
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9e17abe0-901d-4ac1-4d3c-49831a8e7592
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7c2a8b49-af1f-4df4-30a6-f238e8034829
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7c2a8b49-af1f-4df4-30a6-f238e8034829
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

```

**Automation account**

```powershell
PS C:\Program Files\PowerShell\7> Get-AzRoleAssignment -Scope '/subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592'

RoleAssignmentName : 49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/providers/Mic
                     rosoft.Authorization/roleAssignments/49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : cc87d59a-4b27-4c27-bba4-f6a6c34bd0cb
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a623c0b-34bb-4592-b857-f219c771d4e7
RoleAssignmentId   : /providers/Microsoft.Authorization/roleAssignments/1a623c0b-34bb-4592-b857-f219c771d4e7
Scope              : /
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f019c872-9b47-4b12-8b82-3956c6bf3eed
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f019c872-9b47-4b12-8b82-3956c6bf3eed
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : fb18e957-4f42-44a6-9ad7-67c7a54c0da9
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0f5928a5-7c5f-4cc4-991c-59a07976c92b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0f5928a5-7c5f-4cc4-991c-59a07976c92b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : 05b1a670-437e-4f22-b6b8-4d95090f72df
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7390459b-d1ac-47fc-9990-18e4159a0b5b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7390459b-d1ac-47fc-9990-18e4159a0b5b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9ed82813-855f-404f-a399-9f11dab85a63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9ed82813-855f-404f-a399-9f11dab85a63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : aecad497-4a0e-490d-9a10-2911f6cd950a
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4f40060d-b857-4a20-a380-a41cb00229cd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4f40060d-b857-4a20-a380-a41cb00229cd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 6d041734-354c-43ee-9a23-c90853d60cea
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/6d041734-354c-43ee-9a23-c90853d60cea
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : ba196f96-2f12-43cb-824b-5b71057f3c63
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : e2c05e1e-1295-4b65-a803-7034b02c1d63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/e2c05e1e-1295-4b65-a803-7034b02c1d63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3c1b2801-2296-4a4a-9a82-ac69c3c85942
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3c1b2801-2296-4a4a-9a82-ac69c3c85942
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d822c515-7d70-4477-b966-0ac498f6bc39
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d822c515-7d70-4477-b966-0ac498f6bc39
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ae73cb95-1d36-40fd-9091-b5a5802bcbd5
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ae73cb95-1d36-40fd-9091-b5a5802bcbd5
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 990873c7-81a9-4c7a-a215-75440156330b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/990873c7-81a9-4c7a-a215-75440156330b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Reader
RoleDefinitionId   : acdd72a7-3385-48ef-bd42-f606fba81ae7
ObjectId           : 57234839-911a-464f-9929-e643c25bc53e
ObjectType         : Unknown
CanDelegate        : False
Description        : Allow Managed Identity for CycloneBot Read access Azure Subcription for quota assignments.
ConditionVersion   :
Condition          :

RoleAssignmentName : 01ccbe02-638f-4ba5-a18f-6765e7cef751
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/01ccbe02-638f-4ba5-a18f-6765e7cef751
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0ae02774-b54e-4ecc-b3e7-81f447d1a661
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0ae02774-b54e-4ecc-b3e7-81f447d1a661
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4396c151-e41e-4295-bf55-817861556c40
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4396c151-e41e-4295-bf55-817861556c40
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : AcrPull
RoleDefinitionId   : 7f951dda-4ed3-4680-a7ca-43fe172d538d
ObjectId           : e2a8c36c-8aa4-46db-a927-7567f006cb43
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : b94838f0-f6f7-4b06-9606-5ca2021a1801
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/b94838f0-f6f7-4b06-9606-5ca2021a1801
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : a2a9c9a1-614e-4d3a-9fdb-5021ef46eedc
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5161080b-ed32-49e8-868d-bb78ebbb41a8
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5161080b-ed32-49e8-868d-bb78ebbb41a8
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 284f4c74-4a61-41e4-b357-193166745fe5
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d548b9a6-ed6f-4613-9e49-9d6c95a4a820
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d548b9a6-ed6f-4613-9e49-9d6c95a4a820
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a77ff56-635b-48c8-9ff8-ef01c6b05de9
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/1a77ff56-635b-48c8-9ff8-ef01c6b05de9
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a737b55a-ff7b-4d14-a0c1-9189422ccc45
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a737b55a-ff7b-4d14-a0c1-9189422ccc45
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Management Group Contributor
RoleDefinitionId   : 5d58bcaf-24a5-4b20-bdb6-eed9f69fbe4c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ceb96903-ace9-41ef-ace0-717b4048de80
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ceb96903-ace9-41ef-ace0-717b4048de80
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 603d382b-de0d-443a-9590-c8c5334f6f98
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/603d382b-de0d-443a-9590-c8c5334f6f98
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 103f9c11-e56b-4b9c-b51b-1252058cb6b6
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f44781d7-8a7d-48e1-a66c-185b8e52a562
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f44781d7-8a7d-48e1-a66c-185b8e52a562
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 556512b4-56fb-41d1-a355-0467e5e88503
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3dff5477-d9d6-435d-aa89-4cce1cccdacd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3dff5477-d9d6-435d-aa89-4cce1cccdacd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : b492fb13-0a69-4aab-ab31-f7426bf49f48
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a823f7be-1b25-463a-9fa1-e859003d02d0
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a823f7be-1b25-463a-9fa1-e859003d02d0
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : efee41da-a5ed-48b3-9ba2-d54f44d08fef
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3082ac2c-2783-496a-d348-ac0a42d00178
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3082ac2c-2783-496a-d348-ac0a42d00178
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9e17abe0-901d-4ac1-4d3c-49831a8e7592
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9e17abe0-901d-4ac1-4d3c-49831a8e7592
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7c2a8b49-af1f-4df4-30a6-f238e8034829
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7c2a8b49-af1f-4df4-30a6-f238e8034829
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :
```

automation account / configuration
```powershell
PS C:\Program Files\PowerShell\7> Get-AzRoleAssignment -Scope '/subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/configurations/NewDomain'

RoleAssignmentName : 1a623c0b-34bb-4592-b857-f219c771d4e7
RoleAssignmentId   : /providers/Microsoft.Authorization/roleAssignments/1a623c0b-34bb-4592-b857-f219c771d4e7
Scope              : /
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/providers/Mic
                     rosoft.Authorization/roleAssignments/49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : cc87d59a-4b27-4c27-bba4-f6a6c34bd0cb
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f019c872-9b47-4b12-8b82-3956c6bf3eed
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f019c872-9b47-4b12-8b82-3956c6bf3eed
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : fb18e957-4f42-44a6-9ad7-67c7a54c0da9
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0f5928a5-7c5f-4cc4-991c-59a07976c92b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0f5928a5-7c5f-4cc4-991c-59a07976c92b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : 05b1a670-437e-4f22-b6b8-4d95090f72df
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7390459b-d1ac-47fc-9990-18e4159a0b5b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7390459b-d1ac-47fc-9990-18e4159a0b5b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9ed82813-855f-404f-a399-9f11dab85a63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9ed82813-855f-404f-a399-9f11dab85a63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : aecad497-4a0e-490d-9a10-2911f6cd950a
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4f40060d-b857-4a20-a380-a41cb00229cd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4f40060d-b857-4a20-a380-a41cb00229cd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 6d041734-354c-43ee-9a23-c90853d60cea
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/6d041734-354c-43ee-9a23-c90853d60cea
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : ba196f96-2f12-43cb-824b-5b71057f3c63
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : e2c05e1e-1295-4b65-a803-7034b02c1d63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/e2c05e1e-1295-4b65-a803-7034b02c1d63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3c1b2801-2296-4a4a-9a82-ac69c3c85942
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3c1b2801-2296-4a4a-9a82-ac69c3c85942
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d822c515-7d70-4477-b966-0ac498f6bc39
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d822c515-7d70-4477-b966-0ac498f6bc39
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ae73cb95-1d36-40fd-9091-b5a5802bcbd5
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ae73cb95-1d36-40fd-9091-b5a5802bcbd5
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 990873c7-81a9-4c7a-a215-75440156330b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/990873c7-81a9-4c7a-a215-75440156330b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Reader
RoleDefinitionId   : acdd72a7-3385-48ef-bd42-f606fba81ae7
ObjectId           : 57234839-911a-464f-9929-e643c25bc53e
ObjectType         : Unknown
CanDelegate        : False
Description        : Allow Managed Identity for CycloneBot Read access Azure Subcription for quota assignments.
ConditionVersion   :
Condition          :

RoleAssignmentName : 01ccbe02-638f-4ba5-a18f-6765e7cef751
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/01ccbe02-638f-4ba5-a18f-6765e7cef751
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0ae02774-b54e-4ecc-b3e7-81f447d1a661
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0ae02774-b54e-4ecc-b3e7-81f447d1a661
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4396c151-e41e-4295-bf55-817861556c40
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4396c151-e41e-4295-bf55-817861556c40
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : AcrPull
RoleDefinitionId   : 7f951dda-4ed3-4680-a7ca-43fe172d538d
ObjectId           : e2a8c36c-8aa4-46db-a927-7567f006cb43
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : b94838f0-f6f7-4b06-9606-5ca2021a1801
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/b94838f0-f6f7-4b06-9606-5ca2021a1801
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : a2a9c9a1-614e-4d3a-9fdb-5021ef46eedc
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5161080b-ed32-49e8-868d-bb78ebbb41a8
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5161080b-ed32-49e8-868d-bb78ebbb41a8
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 284f4c74-4a61-41e4-b357-193166745fe5
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d548b9a6-ed6f-4613-9e49-9d6c95a4a820
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d548b9a6-ed6f-4613-9e49-9d6c95a4a820
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a77ff56-635b-48c8-9ff8-ef01c6b05de9
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/1a77ff56-635b-48c8-9ff8-ef01c6b05de9
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a737b55a-ff7b-4d14-a0c1-9189422ccc45
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a737b55a-ff7b-4d14-a0c1-9189422ccc45
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Management Group Contributor
RoleDefinitionId   : 5d58bcaf-24a5-4b20-bdb6-eed9f69fbe4c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ceb96903-ace9-41ef-ace0-717b4048de80
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ceb96903-ace9-41ef-ace0-717b4048de80
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 603d382b-de0d-443a-9590-c8c5334f6f98
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/603d382b-de0d-443a-9590-c8c5334f6f98
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 103f9c11-e56b-4b9c-b51b-1252058cb6b6
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f44781d7-8a7d-48e1-a66c-185b8e52a562
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f44781d7-8a7d-48e1-a66c-185b8e52a562
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 556512b4-56fb-41d1-a355-0467e5e88503
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3dff5477-d9d6-435d-aa89-4cce1cccdacd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3dff5477-d9d6-435d-aa89-4cce1cccdacd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : b492fb13-0a69-4aab-ab31-f7426bf49f48
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a823f7be-1b25-463a-9fa1-e859003d02d0
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a823f7be-1b25-463a-9fa1-e859003d02d0
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : efee41da-a5ed-48b3-9ba2-d54f44d08fef
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3082ac2c-2783-496a-d348-ac0a42d00178
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3082ac2c-2783-496a-d348-ac0a42d00178
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9e17abe0-901d-4ac1-4d3c-49831a8e7592
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9e17abe0-901d-4ac1-4d3c-49831a8e7592
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7c2a8b49-af1f-4df4-30a6-f238e8034829
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7c2a8b49-af1f-4df4-30a6-f238e8034829
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

```

automation account / runbook

```powershell
PS C:\Program Files\PowerShell\7> Get-AzRoleAssignment -Scope '/subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/runbooks/Get-Credential'

RoleAssignmentName : 1a623c0b-34bb-4592-b857-f219c771d4e7
RoleAssignmentId   : /providers/Microsoft.Authorization/roleAssignments/1a623c0b-34bb-4592-b857-f219c771d4e7
Scope              : /
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592/providers/Mic
                     rosoft.Authorization/roleAssignments/49ec0b4b-c4e7-e9c2-e9c5-12c0af598436
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational-3592/providers/Microsoft.Automation/automationAccounts/DemoAutomation-3592
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : cc87d59a-4b27-4c27-bba4-f6a6c34bd0cb
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f019c872-9b47-4b12-8b82-3956c6bf3eed
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f019c872-9b47-4b12-8b82-3956c6bf3eed
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : fb18e957-4f42-44a6-9ad7-67c7a54c0da9
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f1cadb5b-2fd0-445d-bd71-fd32ffeaf6e7
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0f5928a5-7c5f-4cc4-991c-59a07976c92b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0f5928a5-7c5f-4cc4-991c-59a07976c92b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Cost Management Contributor
RoleDefinitionId   : 434105ed-43f6-45c7-a02f-909b2ba83430
ObjectId           : 05b1a670-437e-4f22-b6b8-4d95090f72df
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7390459b-d1ac-47fc-9990-18e4159a0b5b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7390459b-d1ac-47fc-9990-18e4159a0b5b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : afeee881-223b-4cf2-a089-ef578900b20c
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9ed82813-855f-404f-a399-9f11dab85a63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9ed82813-855f-404f-a399-9f11dab85a63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : aecad497-4a0e-490d-9a10-2911f6cd950a
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/c0cdb36a-ef5e-4b65-84bc-a7283a3d26cf
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4f40060d-b857-4a20-a380-a41cb00229cd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4f40060d-b857-4a20-a380-a41cb00229cd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0c1c55cc-b1d8-4d72-9a60-c596fabc71a4
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 6d041734-354c-43ee-9a23-c90853d60cea
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/6d041734-354c-43ee-9a23-c90853d60cea
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : ba196f96-2f12-43cb-824b-5b71057f3c63
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : e2c05e1e-1295-4b65-a803-7034b02c1d63
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/e2c05e1e-1295-4b65-a803-7034b02c1d63
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3c1b2801-2296-4a4a-9a82-ac69c3c85942
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3c1b2801-2296-4a4a-9a82-ac69c3c85942
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : eaaa8e84-0896-4254-b67c-c39659e531db
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d822c515-7d70-4477-b966-0ac498f6bc39
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d822c515-7d70-4477-b966-0ac498f6bc39
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ae73cb95-1d36-40fd-9091-b5a5802bcbd5
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ae73cb95-1d36-40fd-9091-b5a5802bcbd5
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : User Access Administrator
RoleDefinitionId   : 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9
ObjectId           : 0ff00a4b-0156-4327-b245-dba7ebd76f1e
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 990873c7-81a9-4c7a-a215-75440156330b
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/990873c7-81a9-4c7a-a215-75440156330b
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Reader
RoleDefinitionId   : acdd72a7-3385-48ef-bd42-f606fba81ae7
ObjectId           : 57234839-911a-464f-9929-e643c25bc53e
ObjectType         : Unknown
CanDelegate        : False
Description        : Allow Managed Identity for CycloneBot Read access Azure Subcription for quota assignments.
ConditionVersion   :
Condition          :

RoleAssignmentName : 01ccbe02-638f-4ba5-a18f-6765e7cef751
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/01ccbe02-638f-4ba5-a18f-6765e7cef751
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 0ae02774-b54e-4ecc-b3e7-81f447d1a661
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/0ae02774-b54e-4ecc-b3e7-81f447d1a661
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 18cdb6ea-a975-489b-983c-ae0940cff4b2
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 4396c151-e41e-4295-bf55-817861556c40
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/4396c151-e41e-4295-bf55-817861556c40
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : AcrPull
RoleDefinitionId   : 7f951dda-4ed3-4680-a7ca-43fe172d538d
ObjectId           : e2a8c36c-8aa4-46db-a927-7567f006cb43
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : b94838f0-f6f7-4b06-9606-5ca2021a1801
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/b94838f0-f6f7-4b06-9606-5ca2021a1801
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : a2a9c9a1-614e-4d3a-9fdb-5021ef46eedc
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5161080b-ed32-49e8-868d-bb78ebbb41a8
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5161080b-ed32-49e8-868d-bb78ebbb41a8
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 284f4c74-4a61-41e4-b357-193166745fe5
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : d548b9a6-ed6f-4613-9e49-9d6c95a4a820
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/d548b9a6-ed6f-4613-9e49-9d6c95a4a820
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 1a77ff56-635b-48c8-9ff8-ef01c6b05de9
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/1a77ff56-635b-48c8-9ff8-ef01c6b05de9
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a737b55a-ff7b-4d14-a0c1-9189422ccc45
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a737b55a-ff7b-4d14-a0c1-9189422ccc45
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Management Group Contributor
RoleDefinitionId   : 5d58bcaf-24a5-4b20-bdb6-eed9f69fbe4c
ObjectId           : 64fbfea8-d5d4-4cdd-8c55-0d1a81a0df8b
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : ceb96903-ace9-41ef-ace0-717b4048de80
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/ceb96903-ace9-41ef-ace0-717b4048de80
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 3f1227ae-c400-4fd0-b661-644fe394bd79
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 603d382b-de0d-443a-9590-c8c5334f6f98
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/603d382b-de0d-443a-9590-c8c5334f6f98
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 103f9c11-e56b-4b9c-b51b-1252058cb6b6
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : f44781d7-8a7d-48e1-a66c-185b8e52a562
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/f44781d7-8a7d-48e1-a66c-185b8e52a562
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : 556512b4-56fb-41d1-a355-0467e5e88503
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3dff5477-d9d6-435d-aa89-4cce1cccdacd
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3dff5477-d9d6-435d-aa89-4cce1cccdacd
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Contributor
RoleDefinitionId   : b24988ac-6180-42a0-ab88-20f7382dd24c
ObjectId           : b492fb13-0a69-4aab-ab31-f7426bf49f48
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : a823f7be-1b25-463a-9fa1-e859003d02d0
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/a823f7be-1b25-463a-9fa1-e859003d02d0
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Owner
RoleDefinitionId   : 8e3af657-a8ff-443c-a75c-2fe8c4bcb635
ObjectId           : efee41da-a5ed-48b3-9ba2-d54f44d08fef
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 3082ac2c-2783-496a-d348-ac0a42d00178
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/3082ac2c-2783-496a-d348-ac0a42d00178
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/5e1709f0-b7b9-4dce-b10d-55ee9bc9ff81
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 0ab5b9ea-ecd7-42b7-b673-3478aec07335
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 9e17abe0-901d-4ac1-4d3c-49831a8e7592
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/9e17abe0-901d-4ac1-4d3c-49831a8e7592
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Virtual Machine Contributor
RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :

RoleAssignmentName : 7c2a8b49-af1f-4df4-30a6-f238e8034829
RoleAssignmentId   : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/providers/Microsoft.Authorization/roleAssignments/7c2a8b49-af1f-4df4-30a6-f238e8034829
Scope              : /subscriptions/7417f1f8-3d91-451a-a354-966c173efb48
DisplayName        :
SignInName         :
RoleDefinitionName : Log Analytics Contributor
RoleDefinitionId   : 92aaf0da-9dab-42b6-94a3-d43ce8d16293
ObjectId           : 6a3ab014-3cf3-4ec1-b918-15a65bf6d955
ObjectType         : Unknown
CanDelegate        : False
Description        :
ConditionVersion   :
Condition          :
```


To find interesting roles
To find how to read role definitions


## Storage Accounts
---
**Get storage accounts**

![[Pasted image 20240612211550.png]]

```powershell
PS C:\Program Files\PowerShell\7> Get-AzStorageAccount

StorageAccountName       ResourceGroupName PrimaryLocation SkuName        Kind      AccessTier CreationTime        ProvisioningState EnableHttpsTrafficOnly LargeFileShares
------------------       ----------------- --------------- -------        ----      ---------- ------------        ----------------- ---------------------- ---------------
financemegamultinational MegaMultinational eastus          Standard_RAGRS StorageV2 Hot        8/5/2021 2:12:35 PM Succeeded         True

```


**Check Public Access for Azure Storage Accounts**

![[Pasted image 20240612215001.png]]

```powershell
PS C:\Program Files\PowerShell\7> Get-AzStorageAccount | Select-Object -Property StorageAccountName, ResourceGroupName, EnableHttpsTrafficOnly, AllowBlobPublicAccess

StorageAccountName       ResourceGroupName EnableHttpsTrafficOnly AllowBlobPublicAccess
------------------       ----------------- ---------------------- ---------------------
financemegamultinational MegaMultinational                   True                  True
```

We can see that the account can be accessed publicly

**Investigating publicly accessible storage account**

**Identify containers**
Attempt
![[Pasted image 20240612220838.png]]
```powershell
PS C:\Program Files\PowerShell\7> $storageAccount = Get-AzStorageAccount -ResourceGroupName MegaMultinational -Name financemegamultinational
PS C:\Program Files\PowerShell\7> $ctx = $storageAccount.Context
PS C:\Program Files\PowerShell\7> Get-AzStorageContainer -Context $ctx
Get-AzStorageContainer: The client 'ryan_3592@megamultinational.com' with object id 'cc87d59a-4b27-4c27-bba4-f6a6c34bd0cb' does not have authorization to perform action 'Microsoft.Storage/storageAccounts/listKeys/action' over scope '/subscriptions/7417f1f8-3d91-451a-a354-966c173efb48/resourceGroups/MegaMultinational/providers/Microsoft.Storage/storageAccounts/financemegamultinational' or the scope is invalid. If access was recently granted, please refresh your credentials.
```


```powershell
PS C:\Program Files\PowerShell\7> $ctx

BlobEndPoint       :
TableEndPoint      :
QueueEndPoint      :
FileEndPoint       :
StorageAccount     :
StorageAccountName : financemegamultinational
Context            : Microsoft.WindowsAzure.Commands.Common.Storage.LazyAzureStorageContext
Name               : financemegamultinational
EndPointSuffix     :
ConnectionString   :
ExtendedProperties : {}

```

[[Flag 2 - Data leak🚩]]

**List Shared Access Sinatures(SAS):**

![[Pasted image 20240612213809.png]]

``` powershell
 Get-AzStorageAccountKey -ResourceGroupName MegaMultinational -StorageAccountName financemegamultinational
```

---
