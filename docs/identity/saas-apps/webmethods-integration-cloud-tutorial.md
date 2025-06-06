---
title: Configure webMethods Integration Suite for Single sign-on with Microsoft Entra ID
description: Learn how to configure single sign-on between Microsoft Entra ID and webMethods Integration Suite.

author: nguhiu
manager: CelesteDG
ms.reviewer: celested
ms.service: entra-id
ms.subservice: saas-apps

ms.topic: how-to
ms.date: 05/20/2025
ms.author: gideonkiratu

# Customer intent: As an IT administrator, I want to learn how to configure single sign-on between Microsoft Entra ID and webMethods Integration Suite so that I can control who has access to webMethods Integration Suite, enable automatic sign-in with Microsoft Entra accounts, and manage my accounts in one central location.
---
# Configure webMethods Integration Suite for Single sign-on with Microsoft Entra ID

In this article,  you learn how to integrate webMethods Integration Suite with Microsoft Entra ID. When you integrate webMethods Integration Suite with Microsoft Entra ID, you can:

* Control in Microsoft Entra ID who has access to webMethods Integration Suite.
* Enable your users to be automatically signed-in to webMethods Integration Suite with their Microsoft Entra accounts.
* Manage your accounts in one central location.

## Prerequisites
The scenario outlined in this article assumes that you already have the following prerequisites:

[!INCLUDE [common-prerequisites.md](~/identity/saas-apps/includes/common-prerequisites.md)]
* webMethods Integration Suite single sign-on (SSO) enabled subscription.

## Scenario description

In this article,  you configure and test Microsoft Entra single sign-on in a test environment.

* webMethods Integration Suite supports **SP** and **IDP** initiated SSO.

* webMethods Integration Suite supports **just-in-time** user provisioning.

## Add webMethods Integration Suite from the gallery

To configure the integration of webMethods Integration Suite into Microsoft Entra ID, you need to add webMethods Integration Suite from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](~/identity/role-based-access-control/permissions-reference.md#cloud-application-administrator).
1. Browse to **Entra ID** > **Enterprise apps** > **New application**.
1. In the **Add from the gallery** section, type **webMethods Integration Suite** in the search box.
1. Select **webMethods Integration Suite** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

 Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/microsoft-365/admin/misc/azure-ad-setup-guides)

<a name='configure-and-test-azure-ad-sso-for-webmethods-integration-suite'></a>

## Configure and test Microsoft Entra SSO for webMethods Integration Suite

Configure and test Microsoft Entra SSO with webMethods Integration Suite using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in webMethods Integration Suite.

To configure and test Microsoft Entra SSO with webMethods Integration Suite, perform the following steps:

1. **[Configure Microsoft Entra SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    1. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
1. **[Configure webMethods Integration Suite SSO](#configure-webmethods-integration-suite-sso)** - to configure the single sign-on settings on application side.
    1. **[Create webMethods Integration Suite test user](#create-webmethods-integration-suite-test-user)** - to have a counterpart of B.Simon in webMethods Integration Suite that's linked to the Microsoft Entra representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

<a name='configure-azure-ad-sso'></a>

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](~/identity/role-based-access-control/permissions-reference.md#cloud-application-administrator).
1. Browse to **Entra ID** > **Enterprise apps** > **webMethods Integration Suite** > **Single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Edit Basic SAML Configuration](common/edit-urls.png)

4. To configure the **webMethods Integration Cloud**, on the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

	| Identifier URL |
	|----------------------------------------------|
	| `<SUBDOMAIN>.webmethodscloud.com`|
	| `<SUBDOMAIN>.webmethodscloud.eu` |
	| `<SUBDOMAIN>.webmethodscloud.de` |
	|

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

	| Reply URL	|
	|----------------------------------------------|
	| `https://<SUBDOMAIN>.webmethodscloud.com/integration/live/saml/ssoResponse`|
	| `https://<SUBDOMAIN>.webmethodscloud.eu/integration/live/saml/ssoResponse`|
	| `https://<SUBDOMAIN>.webmethodscloud.de/integration/live/saml/ssoResponse`|
	|

	c. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    d. In the **Sign-on URL** text box, type a URL using one of the following patterns:

	| Sign-on URL |
	|--------------------------------|
	|`https://<SUBDOMAIN>.webmethodscloud.com/integration/live/saml/ssoRequest`|
	|`https://<SUBDOMAIN>.webmethodscloud.eu/integration/live/saml/ssoRequest`|
	|`https://<SUBDOMAIN>.webmethodscloud.de/integration/live/saml/ssoRequest`|
	|

	> [!NOTE]
	> These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [webMethods Integration Suite Client support team](https://empower.softwareag.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

5. To configure the **webMethods API Cloud**, on the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

	| Identifier URL |
	|----------------------------------------------|
	| `<SUBDOMAIN>.webmethodscloud.com`|
	|`<SUBDOMAIN>.webmethodscloud.eu`|
	| `<SUBDOMAIN>.webmethodscloud.de`|
	|

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

	| Reply URL	|
	|----------------------------------------------|
	| `https://<SUBDOMAIN>.webmethodscloud.com/umc/rest/saml/initsso`|
	| `https://<SUBDOMAIN>.webmethodscloud.eu/umc/rest/saml/initsso`|
	| `https://<SUBDOMAIN>.webmethodscloud.de/umc/rest/saml/initsso`|
	|

	c. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    d. In the **Sign-on URL** text box, type a URL using one of the following patterns:
	
	| Sign-on URL |
	|--------------------------------|
	| `https://api.webmethodscloud.com/umc/rest/saml/initsso/?tenant=<TENANTID>`|
	| `https://api.webmethodscloud.eu/umc/rest/saml/initsso/?tenant=<TENANTID>`|
	| `https://api.webmethodscloud.de/umc/rest/saml/initsso/?tenant=<TENANTID>`|
	|

	> [!NOTE]
	> These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [webMethods Integration Suite Client support team](https://empower.softwareag.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.

6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

	![The Certificate download link](common/metadataxml.png)

7. On the **Set up webMethods Integration Suite** section, copy the appropriate URL(s) as per your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

<a name='create-an-azure-ad-test-user'></a>

[!INCLUDE [create-assign-users-sso.md](~/identity/saas-apps/includes/create-assign-users-sso.md)]

## Configure webMethods Integration Suite SSO

To configure single sign-on on **webMethods Integration Suite** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [webMethods Integration Suite support team](https://empower.softwareag.com/). They set this setting to have the SAML SSO connection set properly on both sides.

### Create webMethods Integration Suite test user

In this section, a user called Britta Simon is created in webMethods Integration Suite. webMethods Integration Suite supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in webMethods Integration Suite, a new one is created after authentication.

## Test SSO 

In this section, you test your Microsoft Entra single sign-on configuration with following options. 

#### SP initiated:

* Select **Test this application**, this option redirects to webMethods Integration Suite Sign on URL where you can initiate the login flow.  

* Go to webMethods Integration Suite Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

* Select **Test this application**, and you should be automatically signed in to the webMethods Integration Suite for which you set up the SSO. 

You can also use Microsoft My Apps to test the application in any mode. When you select the webMethods Integration Suite tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the webMethods Integration Suite for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Related content

Once you configure webMethods Integration Suite you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Defender for Cloud Apps](/cloud-app-security/proxy-deployment-any-app).
