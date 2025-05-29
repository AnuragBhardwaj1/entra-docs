---
title: Using groups managed Privileged Identity Management with access packages reference
description: This article serves as a reference for Microsoft Entra ID behavior when assignment periods of an access package and PIM policy dont align.
author: owinfreyATL
ms.author: owinfrey
manager: femila
ms.service: entra-id-governance
ms.topic: concept-article
ms.date: 05/27/2025

#CustomerIntent: As a customer, I want to become informed on what happens in the different scenarios when PIM expiration dates differ from the access package expiration date.
---

# Using groups managed by Privileged Identity Management with access packages reference

This article contains Microsoft Entra ID behavior in scenarios where the group managed by PIM, and the access package expiration periods, differ. By assigning a group managed by PIM to an access package, you're able to assign eligible roles when an access package is requested. If you’re looking for a guide on setting up a group to assign eligible roles via access packages, see: [Assign eligible group membership and ownership in access packages via Privileged Identity Management for Groups (Preview)](entitlement-management-access-package-eligible.md).


## Shorter access package expiration

When an access package's expiration date is shorter than PIM's "*Expire eligible assignments after*" date, then the PIM assignment expires when the access package expires.

### Example

| Access package policy assignment expiration | PIM policy max assignment duration | Microsoft Entra ID behavior |
|-------------------------------------|-----------------------------------|-----------------------------|
| 30 days                            | 365 days                          | Entitlement Management sets a 365-day expiration on the PIM assignment when the access policy assignment is created, but removes the PIM assignment after the access policy assignment expires in 30 days. |

## Shorter PIM duration

When the PIM assignment expires before the access package assignment, access is revoked when the PIM assignment expires irrespective of the access package's expiration date.

### Example

| Access package policy assignment expiration | PIM policy max assignment duration | Microsoft Entra ID behavior |
|--------------------------------------------|-----------------------------------|-----------------------------|
| 180 days                                   | 40 days                           | Entitlement Management sets a 40-day expiration on the PIM assignment when the access policy assignment is created. On day 41, although the access package is still assigned, access is revoked. |

## Permanent AP Assignment

If the Access package assignment is permanent, access is revoked based on when the PIM assignment expires.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
|------------------------------------|------------------------------------|-----------------------------|
| None (permanent allowed)           | 40 days                            | Entitlement management sets a 40-day expiration on the PIM assignment when the access policy assignment is created. On day 41, although the access package is still assigned, access is revoked. |

## Permanent PIM Assignment

When the PIM assignment is permanent, it's removed only when the access package assignment expires.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
|------------------------------------|------------------------------------|-----------------------------|
| 60 days                            | None (permanent allowed)           | When entitlement management creates the PIM assignment, it's set to permanent. Access is revoked on day 61 after the access package policy assignment expires. |

## Permanent AP and PIM Assignment

If both the access package and PIM assignments are permanent, the PIM assignment remains as long as the access package assignment.

### Example

| Access package policy assignment expiration | PIM Policy Max Assignment Duration | Microsoft Entra ID behavior |
|------------------------------------|------------------------------------|-----------------------------|
| None (permanent allowed)           | None (permanent allowed)           | In this scenario, when EM creates the PIM assignment, it sets the PIM assignment to permanent. The PIM assignment is only removed if the AP assignment is removed by other ways. |

## Related content

- [Microsoft Entra ID Governance](identity-governance-overview.md)
