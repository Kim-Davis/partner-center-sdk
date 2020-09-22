---
title: Register app details for Partner Center for Microsoft National Cloud
description: Developers must register details about their app with Azure AD through the Azure portal. This helps ensure that only specified apps are able to connect to partner and customer data.
MS-HAID:
- 'pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany'
- 'pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Register app details for Partner Center for Microsoft National Cloud

**Applies to:**

- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Developers must register details about their app with Azure AD through the Azure portal. This helps ensure that only specified apps are able to connect to partner and customer data.

For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell. For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/?view=azureadps-2.0#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.

## Web apps

For web apps, use the following procedures to register your application ID.

### Create or update web app

1. Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app. Sign in to the Azure portal using either a work or school account or a personal Microsoft account.

2. Select **New registration**. For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).

### Configure API access permissions for web app

1. Choose your app. Go to **Settings** of the Web app.

2. In **API Access** section, choose **Required permissions**

3. For Windows Azure Active directory permissions:

    1. Choose **Windows Azure Active Directory permissions**.

    2. In **Applications permissions**, select Read directory data.

    3. Save the permissions.

4. Note the application ID in the **Properties** section of your web app.

### Add a secret key to your app

1. Go to the **Keys** section of your web app.

2. Enter key description and select duration as 1 or 2 years, as you need.

3. Save and copy the secret key value. **This value will not be shown again once you leave this page.**

You should have the following details from the web app configuration:

- Application ID
- Application secret

### Register the Web app in Partner Center

1. Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).

2. Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.

3. In the **Web App** section, choose **Register existing app**.

4. Select the web app you created in Azure portal.

5. Choose **register your app**.

## Native apps

Native apps do not need to be registered to Partner Center. But these apps need to be configured to provide access to Partner Center APIs.

>[!NOTE]
>Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant. This creates the settings on the tenant to enable app permissions.

### Create native app

1. Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app. Sign in to the Azure portal using either a work or school account or a personal Microsoft account.

2. Select **New registration**. For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).

### Configure API access permissions for native app

1. Choose your app. Go to **Settings**.

2. In API Access, choose **Required permissions**.

3. Choose **Windows Azure Active Directory permissions**. In **Delegated permissions**, select these permissions:

    - **Sign in and read user profile**
    - **Read directory data**
    - **Access the directory as the signed-in user**
    - **Read all groups**

4. Save the permissions.

5. Choose **Add** in **Required permissions**.

6. Choose **Select an API**.

    1. In the search box, enter **Microsoft Partner Center** and select it from the results list.

    2. Choose **Select**.

7. Choose **Select permissions**.

    1. Select **Access Partner Center PPE**.
    
    2. Choose **Select**.

8. Choose **Done**.

>[!IMPORTANT]
> Note the application ID in the Properties of your app.

You do not need to register native apps in Partner Center, however the native app must be admin consented . Note the application ID of your native app.
