**Check for resources associated with the powershell account**

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

We see there is a storage account

We can check for public access

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

Login to azure portal using the supplied creds

![[Pasted image 20240613064048.png]]

Check for storage accounts
![[Pasted image 20240613064134.png]]

Look for containers in the storage account

![[Pasted image 20240613064248.png]]

Finance caught my eye
![[Pasted image 20240613064341.png]]

This is publicly acessible

![[Pasted image 20240613065137.png]]

On investigating we get a file named employees.xlsx which is password protected

![[Pasted image 20240613064426.png]]

I tried 'password' as password

Voila!

![[Pasted image 20240613064457.png]]