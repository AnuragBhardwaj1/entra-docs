---
title: Fix problems with dynamic membership groups
description: Troubleshooting tips for dynamic membership groups in Microsoft Entra ID

author: barclayn
manager: pmwongera
ms.service: entra-id
ms.subservice: users
ms.topic: troubleshooting
ms.date: 01/15/2025
ms.author: barclayn
ms.reviewer: krbain
ms.custom: it-pro
---

# Troubleshoot and resolve groups issues

This article contains troubleshooting information for groups in Microsoft Entra ID, part of Microsoft Entra.

## Troubleshoot group creation issues

**I disabled security group creation in the Azure portal but groups can still be created via PowerShell**  
The **User can create security groups in Azure portals** setting in the Azure portal controls whether or not non-admin users can create security groups in the Access panel or the Azure portal. It doesn't control security group creation via PowerShell.

To disable group creation for nonadmin users in PowerShell:
1. Verify that nonadmin users are allowed to create groups:

   ```powershell
   Get-MgBetaDirectorySetting | select -ExpandProperty values
   ```

2. If it returns `EnableGroupCreation : True`, then nonadmin users can create groups. To disable this feature:

   ```powershell
   Install-Module Microsoft.Graph.Beta.Identity.DirectoryManagement
   Import-Module Microsoft.Graph.Beta.Identity.DirectoryManagement
   $params = @{
   TemplateId = "62375ab9-6b52-47ed-826b-58e47e0e304b"
   Values = @(    
    @{
      Name = "EnableGroupCreation"
      Value = "false"
    }    
   )
    }
   Connect-MgGraph -Scopes "Directory.ReadWrite.All"
   New-MgBetaDirectorySetting -BodyParameter $params
   ```

**I received a max groups allowed error when trying to create a Dynamic Group in PowerShell**  

The max number of Dynamic groups per organization is 5,000.
When you reach the maximum number of Dynamic groups in your organization, you receive a message in PowerShell that says *Dynamic group policies max allowed groups count reached*. 

If you run into this limit, to create any new Dynamic groups, you first need to delete some existing Dynamic groups. There's no way to increase the limit.

## Troubleshoot dynamic membership groups

**I configured a rule on a group but no memberships get updated in the group**  
1. Verify the values for user or device attributes in the rule. Ensure there are users that satisfy the rule.
For devices, check the device properties to ensure any synced attributes contain the expected values.  
2. Check the membership processing status to confirm if it's complete. You can check the [membership processing status](groups-create-rule.md#check-the-processing-status-for-a-rule) and the last updated date on the **Overview** page for the group.

If everything looks good, allow some time for the group to populate. Depending on the size of your Microsoft Entra organization, the group could take up to 24 hours for populating for the first time or after a rule change.

**I configured a rule, but now the existing members of the rule are removed**  
This is expected behavior. Existing members of the group are removed when a rule is enabled or changed. Not all existing members are deleted, only users who no longer meet the new rule. The users returned from evaluation of the new rule are added as members to the group. 
Users who meet both existing rules and new rules remain in the dynamic group. Their license assignments aren't temporarily deleted and their role assignments aren't removed.

**I don't see membership changes instantly when I add or change a rule, why not?**  

Dedicated membership evaluation is done periodically in an asynchronous background process. Both the number of users in your directory and the size of the resulting group affect processing time. 

Typically, directories with small numbers of users see the dynamic membership group changes in less than a few minutes. Directories with a large number of users can take 30 minutes or longer to populate.

**How can I force the group to be processed now?**  
Currently, there's no way to automatically trigger the group to be processed on demand. However, you can manually trigger the reprocessing by updating the membership rule to add a whitespace at the end.

**I encountered a rule processing error**  
The following table lists common rule errors for dynamic membership groups and how to correct them.

| Rule parser error | Error usage | Corrected usage |
| --- | --- | --- |
| Error: Attribute not supported. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/><br/>Make sure the attribute is on the [supported properties list](groups-dynamic-membership.md#supported-properties). |
| Error: Operator isn't supported on attribute. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/><br/>The operator used isn't supported for the property type (in this example, -contains can't be used on type boolean). Use the correct operators for the property type. |
| Error: Query compilation error. | 1. (user.department -eq "Sales") (user.department -eq "Marketing")<br>2. (user.userPrincipalName -match "\*@domain.ext") | 1. Missing operator. Use -and or -or to join predicates<br>(user.department -eq "Sales") -or (user.department -eq "Marketing")<br>2. Error in regular expression used with -match<br>(user.userPrincipalName -match ".\*@domain.ext")<br>or alternatively: (user.userPrincipalName -match "@domain.ext$") |

## Next steps

These articles provide additional information on Microsoft Entra ID.

* [Managing access to resources with Microsoft Entra groups](~/fundamentals/concept-learn-about-groups.md)
* [Application Management in Microsoft Entra ID](~/identity/enterprise-apps/what-is-application-management.md)
* [What is Microsoft Entra ID?](~/fundamentals/whatis.md)
* [Integrating your on-premises identities with Microsoft Entra ID](~/identity/hybrid/whatis-hybrid-identity.md)
