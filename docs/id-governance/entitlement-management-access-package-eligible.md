---
title: Assign eligible group membership and ownership in access packages via PIM for Groups
description: This how-to article describes how to assign eligible membership and ownership to a group via pim in an access package.
author: owinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
ms.subservice: entitlement-management
ms.topic: how-to #Required; leave this attribute/value as-is
ms.date: 05/21/2025

#CustomerIntent: As an IT Administrator I want to assign eligible roles for a group within an access package.
---

# Assign eligible group membership and ownership in access packages via PIM for Groups

As an access package manager, you can assign which role you want to provide a user for a group within an access package. By [managing groups with Privileged Identity Management](../id-governance/privileged-identity-management/groups-discover-groups.md), you're able to enhance security by designating that group access happens just-in-time. This article describes how to enable pim for a group, adding the group to an access package, and verifying eligible assignments are available.

<!---Avoid notes, tips, and important boxes. Readers tend to skip over them. Better to put that info directly into the article text.

-->

<!-- 3. Prerequisites --------------------------------------------------------------------

Required: Make Prerequisites the first H2 after the H1. 

* Provide a bulleted list of items that the user needs.
* Omit any preliminary text to the list.
* If there aren't any prerequisites, list "None" in plain text, not as a bulleted item.

-->

## Prerequisites

[!INCLUDE [Microsoft Entra ID Governance license](../includes/entra-entra-governance-license.md)]

## Create a group

The following steps walk you through creating the group that you'll enable to be managed by PIM:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [User Administrator](~/identity/role-based-access-control/permissions-reference.md#user-administrator).

1. Browse to **Entra ID** > **Groups** > **All groups**.

1. Select **New group**.

1. Give the group a name and description and then complete the other required options:
   - **Group Type:** Security
   - **Membership type:** Select *Assigned*.
   :::image type="content" source="media/entitlement-management-access-package-eligible/create-group-eligible.png" alt-text="Picture of creating the group for the access package.":::
1. Select **Create**.



## Enable management of group with PIM

To enable PIM management for the group, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](~/identity/role-based-access-control/permissions-reference.md#privileged-role-administrator).

1. Browse to **ID Governance** > **Privileged Identity Management** > **Groups**.

1. Select **Discover groups** and select a group that you want to bring under management with PIM.

1. Select **Manage groups** and **OK**.

1. Select **Groups** to return to the list of groups enabled in PIM for Groups, and notice the group you added is now on the list.
    :::image type="content" source="media/entitlement-management-access-package-eligible/groups-managed-pim-list.png" alt-text="Screenshot of groups managed by PIM list.":::

> [!IMPORTANT]
> Once a group is managed, it can't be taken out of management. This prevents another resource administrator from removing PIM settings. If a group is deleted from Microsoft Entra ID, it may take up to 24 hours for the group to be removed from the **PIM for Groups** option.

## Add the resource to an access package

Once the resource is managed by PIM, eligible roles can be added as its role assignment in an access package. To verify this, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference.md#identity-governance-administrator).
    > [!TIP]
    > Other least privileged roles that can complete this task include the Catalog owner and the Access package manager.
1. Browse to **ID Governance** > **Entitlement management** > **Access package**.

1. On the **Access packages** page, open the access package you want to add resource roles to.

1. In the left menu, select **Resource roles**.

1. Select **Add resource roles** to open the Add resource roles to access package page.

1. On the resource roles page select **Groups and Teams**.

1. Select the group you want to add, and under roles verify that you can assign both active and eligible roles.
    :::image type="content" source="media/entitlement-management-access-package-eligible/eligible-roles-list.png" alt-text="Screenshot of eligible roles list for a group.":::



## Next steps

- [Review access of access packages](entitlement-management-access-reviews-review-access.md)
- [Change resource roles for an access package in entitlement management](entitlement-management-access-package-resources.md)
