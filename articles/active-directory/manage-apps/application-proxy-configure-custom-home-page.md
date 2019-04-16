---
title: Set a custom home page for published apps by using Azure AD Application Proxy | Microsoft Docs
description: Covers the basics about Azure AD Application Proxy connectors
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman

ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/08/2017
ms.author: celested
ms.reviewer: harshja
ms.custom: it-pro
ms.collection: M365-identity-device-management
---
# Set a custom home page for published apps by using Azure AD Application Proxy

This article discusses how to configure apps to direct users to a custom home page. When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first. Set a custom home page so that your users go to the right page when they access the apps. Your users will see the custom home page that you set, whether they access the app from the Azure Active Directory Access Panel or the Office 365 app launcher.

When users launch the app, they're directed by default to the root domain URL for the published app. The landing page is typically set as the home page URL. Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app. 

Here's one example of why a company would set a custom home page:
- Inside your corporate network, users go to `https://ExpenseApp/login/login.aspx` to sign in and access your app.
- Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with `https://ExpenseApp` as the internal URL.
- The default external URL is `https://ExpenseApp-contoso.msappproxy.net`, which doesn't take your users to the sign-in page.  
- Set `https://ExpenseApp-contoso.msappproxy.net/login/login.aspx` as the home page URL. 

>[!NOTE]
>When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](../user-help/active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## Before you start

Before you set the home page URL, keep in mind the following requirements:

* Ensure that the path you specify is a subdomain path of the root domain URL.

  If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.

* If you make a change to the published app, the change might reset the value of the home page URL. When you update the app in the future, you should recheck and, if necessary, update the home page URL.

## Change the home page in the Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) as an administrator.
2. Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list. 
3. Select **Properties** from the settings.
4. Update the **Home page URL** field with your new path. 

   ![Provide new home page URL](./media/application-proxy-configure-custom-home-page/homepage.png)

5. Select **Save**

## Change the home page with PowerShell

### Install the Azure AD PowerShell module

Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module. You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint. 

To install the package, follow these steps:

1. Open a standard PowerShell window, and then run the following command:

    ```powershell
     Install-Module -Name AzureAD
    ```

    If you're running the command as a non-admin, use the `-scope currentuser` option.
2. During the installation, select **Y** to install two packages from Nuget.org. Both packages are required. 

### Find the ObjectID of the app

Obtain the ObjectID of the app, and then search for the app by its home page.

1. In the same PowerShell window, import the Azure AD module.

    ```powershell
    Import-Module AzureAD
    ```

2. Sign in to the Azure AD module as the tenant administrator.

    ```powershell
    Connect-AzureAD
    ```

3. Find the app based on its home page URL. You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**. This example uses *sharepoint-iddemo*.

    ```powershell
    Get-AzureADApplication | Where-Object { $_.Homepage -like "sharepoint-iddemo" } | Format-List DisplayName, Homepage, ObjectID
    ```

4. You should get a result that's similar to the one shown here. Copy the ObjectID GUID to use in the next section.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### Update the home page URL

Create the home page URL, and update your application with that value. Continue using the same PowerShell window to run these commands. Or, if you're using a new PowerShell window, sign in to the Azure AD module again using `Connect-AzureAD`. 

1. Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding section.

    ```powershell
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

   Now that you've confirmed the app, you're ready to update the home page, as follows.

2. Create a blank application object to hold the changes that you want to make. This variable holds the values that you want to update. Nothing is created in this step.

    ```powershell
    $appnew = New-Object "Microsoft.Open.AzureAD.Model.Application"
    ```

3. Set the home page URL to the value that you want. The value must be a subdomain path of the published app. For example, if you change the home page URL from `https://sharepoint-iddemo.msappproxy.net/` to `https://sharepoint-iddemo.msappproxy.net/hybrid/`, app users go directly to the custom home page.

    ```powershell
    $homepage = "https://sharepoint-iddemo.msappproxy.net/hybrid/"
    ```

4. Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."

    ```powershell
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```

5. To confirm that the change was successful, restart the app.

    ```powershell
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Any changes that you make to the app might reset the home page URL. If your home page URL resets, repeat the steps in this section to set it back.

## Next steps

- [Enable remote access to SharePoint with Azure AD Application Proxy](application-proxy-integrate-with-sharepoint-server.md)
- [Enable Application Proxy in the Azure portal](application-proxy-add-on-premises-application.md)