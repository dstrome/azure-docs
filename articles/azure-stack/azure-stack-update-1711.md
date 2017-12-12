---
title: Azure Stack 1711 Update | Microsoft Docs
description: Learn about what's in the 1711 update for Azure Stack integrated systems, the known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: andredm7
manager: femila
editor: ''

ms.assetid: 2b66fe05-3655-4f1a-9b30-81bd64ba0013
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: andredm

---

# Azure Stack 1711 update

*Applies to: Azure Stack integrated systems*

This article describes the improvements and fixes in this update package, known issues for this release, and where to download the update. Known issues are divided into known issues directly related to the update process, and known issues with the build (post-installation).

> [!IMPORTANT]
> This update package is only applicable for Azure Stack integrated systems. Do not apply this update package to the Azure Stack Development Kit.

## Build reference

The Azure Stack 1711 update build number is **171201.3**.

## Before you begin

### Prerequisites

You must first install the Azure Stack [1710 Update](https://docs.microsoft.com/azure/azure-stack/azure-stack-update-1710) before applying this update.

### New features and fixes

This update includes the following improvements and fixes for Azure Stack.

#### New features

- Support for Syndicating solution templates
- Updates in the Azure Stack Graph logging and error handling
- Ability to turn hosts on and off
- Users can now activate Windows VMs automatically
- Added privileged endpoint PowerShell cmdlet to retrieve BitLocker recovery keys for retention purposes
- Support for updating the offline images when updating infrastructure

#### Fixes

- Fixed race condition in DNS during field replaceable unit (FRU) and also updated cluster logging
- Fix for restart-ability of disable-host in field replaceable unit (FRU)
- Various other performance, security and stability fixes

#### Windows Server 2016 new features and fixes

- [November 14, 2017—KB4048953 (OS Build 14393.1884) ](https://support.microsoft.com/help/4048953)
 
### Known issues with the update process

This section contains known issues that you may encounter during the 1711 update installation.


1. **Symptom:** Azure Stack operators may see the following error during the update process: *"name:Install Update.", "description": "Install Update on Hosts and Infra VMs.", "errorMessage": "Type 'LiveUpdate' of Role 'VirtualMachines' raised an exception:\n\nThere is not enough space on the disk.\n\nat <ScriptBlock>, <No file>: line22", "status": "Error", "startTimeUtc": "2017-11-10T16:46:59.123Z", "endTimeUtc": "2017-11-10T19:20:29.669Z", "steps": [ ]"*
	2. **Cause:** This issue is caused by a lack of free disk space on one or more virtual machines that are part of the Azure Stack infrastructure
	3. **Resolution:** Contact Microsoft Customer Service and Support (CSS) for assistance.
<br><br>
2. **Symptom:** Azure Stack operators may see the following error during the update process:*Exception calling "ExtractToFile" with "3" argument(s):"The process cannot access the file '<\\<machineName>-ERCS01\C$\Program Files\WindowsPowerShell\Modules\Microsoft.AzureStack.Diagnostics\Microsoft.AzureStack.Common.Tools.Diagnostics.AzureStackDiagnostics.dll>'*
	1. **Cause:** This issue is caused when resuming an update from the portal that was previously resumed using a Privileged End Point (PEP).
	2. **Resolution:** Contact Microsoft Customer Service and Support (CSS) for assistance.
<br><br>
3. **Symptom:**Azure Stack operators may see the following error during the update process:*"Type 'CheckHealth' of Role 'VirtualMachines' raised an exception:\n\nVirtual Machine health check for <machineName>-ACS01 produced the following errors.\nThere was an error getting VM information from hosts. Exception details:\nGet-VM : The operation on computer 'Node03' failed: The WS-Management service cannot process the request. The WMI \nservice or the WMI provider returned an unknown error: HRESULT 0x8004106c".*
	1. **Cause:** This issue is caused by a Windows Server issue that is intended to be addressed in subsequent Window server updates.
	2. **Resolution:** Contact Microsoft Customer Service and Support (CSS) for assistance.
<br><br>
4. **Symptom:**Azure Stack operators may see the following error during the update process:*"Type 'DefenderUpdate' of Role 'URP' raised an exception: Failed getting version from \\SU1FileServer\SU1_Public\DefenderUpdates\x64\{file name}.exe after 60 attempts at Copy-AzSDefenderFiles, C:\Program Files\WindowsPowerShell\Modules\Microsoft.AzureStack.Defender\Microsoft.AzureStack.Defender.psm1: line 262"*
	1. **Cause:** This issue is caused by a failed or incomplete background download of Windows Defender definition updates.
	2. **Resolution:** Please attempt to resume the update after up to 8 hours have passed since the first update try.

### Known issues (post-installation)

This section contains post-installation known issues with build **20171201.3**.

#### Portal

- It may not be possible to view compute or storage resources in the administrator portal. This indicates that an error occurred during the installation of the update and that the update was incorrectly reported as successful. If this issue occurs, please contact Microsoft CSS for assistance.
- You may see a blank dashboard in the portal. To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.
- When you view the properties of a resource group, the **Move** button is disabled. This behavior is expected. Moving resource groups between subscriptions is not currently supported.
- For any workflow where you select a subscription, resource group, or location in a drop-down list, you may experience one or more of the following issues:

   - You may see a blank row at the top of the list. You should still be able to select an item as expected.
   - If the list of items in the drop-down list is short, you may not be able to view any of the item names.
   - If you have multiple user subscriptions, the resource group drop-down list may be empty. 

		> [!NOTE]
		> To work around the last two issues, you can type the name of the subscription or resource group (if you know it), or you can use PowerShell instead.

- Deleting user subscriptions results in orphaned resources. As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.
- You are not able to view permissions to your subscription using the Azure Stack portals. As a workaround, you can verify permissions by using PowerShell.

#### Health and monitoring

- If you reboot an infrastructure role instance, you may receive a message indicating that the reboot failed. However, the reboot actually succeeded.

#### Marketplace
- When you try to add items to the Azure Stack marketplace by using the **Add from Azure** option, not all items may be visible for download.
- Users can browse the full marketplace without a subscription, and can see administrative items like plans and offers. These items are non-functional to users.

#### Compute
- Users are given the option to create a virtual machine with geo-redundant storage. This configuration causes virtual machine creation to fail.
- You can configure a virtual machine availability set only with a fault domain of one, and an update domain of one.
- There is no marketplace experience to create virtual machine scale sets. You can create a scale set by using a template.
- Scaling settings for virtual machine scale sets are not available in the portal. As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set). Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.
 
#### Networking
- You can't create a load balancer with a public IP address by using the portal. As a workaround, you can use PowerShell to create the load balancer.
- You must create a network address translation (NAT) rule when you create a network load balancer. If you don't, you'll receive an error when you try to add a NAT rule after the load balancer is created.
- You can't disassociate a public IP address from a virtual machine (VM) after the VM has been created and associated with that IP address. Disassociation will appear to work, but the previously assigned public IP address remains associated with the original VM. This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*). All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one. Currently, you must only use new public IP addresses for new VM creation.
- Azure Stack operators may be unable to deploy, delete, modify VNETs or Network Security Groups. This issue is primarily seen on subsequent update attempts of the same package. This is caused by a packaging issue with an update which is currently under investigation.
 
#### SQL/MySQL
- It can take up to an hour before tenants can create databases in a new SQL or MySQL SKU. 
- Creation of items directly on SQL and MySQL hosting servers that are not performed by the resource provider is not supported and may result in a mismatched state.
 
#### App Service
- A user must register the storage resource provider before they create their first Azure Function in the subscription.

#### Identity

In Azure Active Directory Federation Services (ADFS) deployed environments, the **azurestack\azurestackadmin** account is no longer the owner of the Default Provider Subscription. Instead of logging into the **Admin portal / adminmanagement endpoint** with the **azurestack\azurestackadmin**, you can use the **azurestack\cloudadmin** account, so that you can manage and use the Default Provider Subscription.

> [!IMPORTANT]
> Even though the **azurestack\cloudadmin** account is the owner of the Default Provider Subscription in ADFS deployed environments, it does not have permissions to RDP into the host. Continue to use the **azurestack\azurestackadmin** account or the local administrator account to login, access and manage the host as needed.

## Download the update

You can download the Azure Stack 1711 update package from [here](https://aka.ms/azurestackupdatedownload).

## More information

Microsoft has provided a way to monitor and resume updates using the Privileged End Point (PEP) installed with Update 1711.

- See the [Monitor updates in Azure Stack using the privileged endpoint documentation](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-update). 

## See also

- See [Manage updates in Azure Stack overview](azure-stack-updates.md) for an overview of the update management in Azure Stack.
- See [Apply updates in Azure Stack](azure-stack-apply-updates.md) for more information about how to apply updates with Azure Stack.
