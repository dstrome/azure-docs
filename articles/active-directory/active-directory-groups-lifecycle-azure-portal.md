﻿---
title: Expiration for Office 365 groups in Azure Active Directory | Microsoft Docs
description: How to set up expiration for Office 365 groups in Azure Active Directory (preview)
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''

ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: curtand                   
ms.reviewer: kairaz.contractor
ms.custom: it-pro

---

# Configure expiration for Office 365 groups (preview)

You can now manage the lifecycle of Office 365 groups by setting expiration features for them. You can set expiration for only Office 365 groups in Azure Active Directory (Azure AD). Once you set a group to expire:
-	Owners of the group are notified to renew the group as the expiration nears
-	Any group that is not renewed is deleted
-	Any Office 365 group that is deleted can be restored within 30 days by the group owners or the administrator

> [!NOTE]
> Setting expiration for Office 365 groups requires an Azure AD Premium license or an Azure AD Basic EDU license for all members of the groups to which expiration settings are applied.
> 
> For Azure AD Basic EDU licensed customers: to configure this policy for the first time, use the Azure Active Directory PowerShell cmdlets. After that, you can update the expiration settings using either PowerShell or the Azure AD portal, with an account that's a User Account Administrator or Global Administrator in your Azure AD tenant.

For information on how to download and install the Azure AD PowerShell cmdlets, see [Azure Active Directory PowerShell for Graph - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

## Set group expiration

1. Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.

2. Open Azure AD, select **Users and groups**.

3. Select **Group settings** and then select **Expiration** to open the expiration settings.
  
  ![Expiration blade](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. On the **Expiration** blade, you can:

  * Set the group lifetime in days. You could select one of the preset values, or a custom value (should be 31 days or more). 
  * Specify an email address where the renewal and expiration notifications should be sent when a group has no owner. 
  * Select which Office 365 groups expire. You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.
  * Save your settings when you're done by selecting **Save**.


Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.

![Expiration email notification](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

The group owner can then select **Renew group** to renew the Office 365
group, or can select **Go to group** to see the members and other details
about the group.

When a group expires, the group is deleted one day after the expiration date. An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.

![Group deletion email notification](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).
    
If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.

> [!NOTE]
> * When you first set up expiration, any groups that are older than the expiration interval are set to 30 days until expiration. The first renewal notification email is sent out within a day. 
>   For example, Group A was created 400 days ago, and the expiration interval is set to 180 days. When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.
> * When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule. This process might take up to 24 hours.

## Next steps
These articles provide additional information on Azure AD groups.

* [See existing groups](active-directory-groups-view-azure-portal.md)
* [Manage settings of a group](active-directory-groups-settings-azure-portal.md)
* [Manage members of a group](active-directory-groups-members-azure-portal.md)
* [Manage memberships of a group](active-directory-groups-membership-azure-portal.md)
* [Manage dynamic rules for users in a group](active-directory-groups-dynamic-membership-azure-portal.md)
