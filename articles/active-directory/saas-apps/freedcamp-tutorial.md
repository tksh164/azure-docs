---
title: 'Tutorial: Azure Active Directory integration with Freedcamp | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Freedcamp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess

ms.assetid: bfc73563-017d-458f-b634-162f93e03b74
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 04/29/2019
ms.author: jeedes

ms.collection: M365-identity-device-management

---
# Tutorial: Azure Active Directory integration with Freedcamp

In this tutorial, you learn how to integrate Freedcamp with Azure Active Directory (Azure AD).
Integrating Freedcamp with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Freedcamp.
* You can enable your users to be automatically signed-in to Freedcamp (Single Sign-On) with their Azure AD accounts.
* You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.

## Prerequisites

To configure Azure AD integration with Freedcamp, you need the following items:

* An Azure AD subscription. If you don't have an Azure AD environment, you can get a [free account](https://azure.microsoft.com/free/)
* Freedcamp single sign-on enabled subscription

## Scenario description

In this tutorial, you configure and test Azure AD single sign-on in a test environment.

* Freedcamp supports **SP and IDP** initiated SSO

## Adding Freedcamp from the gallery

To configure the integration of Freedcamp into Azure AD, you need to add Freedcamp from the gallery to your list of managed SaaS apps.

**To add Freedcamp from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click the **Azure Active Directory** icon.

	![The Azure Active Directory button](common/select-azuread.png)

2. Navigate to **Enterprise Applications** and then select the **All Applications** option.

	![The Enterprise applications blade](common/enterprise-applications.png)

3. To add a new application, click **New application** button on the top of the dialog.

	![The New application button](common/add-new-app.png)

4. In the search box, type **Freedcamp**, select **Freedcamp** from result panel, and then click the **Add** button to add the application.

	![Freedcamp in the results list](common/search-new-app.png)

## Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Freedcamp based on a test user called **Britta Simon**.
For single sign-on to work, a link relationship between an Azure AD user and the related user in Freedcamp needs to be established.

To configure and test Azure AD single sign-on with Freedcamp, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Configure Freedcamp Single Sign-On](#configure-freedcamp-single-sign-on)** - to configure the Single Sign-On settings on application side.
3. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
4. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Create Freedcamp test user](#create-freedcamp-test-user)** - to have a counterpart of Britta Simon in Freedcamp that is linked to the Azure AD representation of user.
6. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal.

To configure Azure AD single sign-on with Freedcamp, perform the following steps:

1. In the [Azure portal](https://portal.azure.com/), on the **Freedcamp** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)

2. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)

3. On the **Set up Single Sign-On with SAML** page, click the **Edit** icon to open the **Basic SAML Configuration** dialog.

	![Edit Basic SAML Configuration](common/edit-urls.png)

4. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    ![Freedcamp Domain and URLs single sign-on information](common/idp-intiated.png)

    a. In the **Identifier** text box, type a URL using the following pattern:
    `https://<SUBDOMAIN>.freedcamp.com/sso/<UNIQUEID>`

    b. In the **Reply URL** text box, type a URL using the following pattern:
    `https://<SUBDOMAIN>.freedcamp.com/sso/acs/<UNIQUEID>`

5. Click **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    ![Freedcamp Domain and URLs single sign-on information](common/metadata-upload-additional-signon.png)

    In the **Sign-on URL** text box, type a URL using the following pattern:
    `https://<SUBDOMAIN>.freedcamp.com/login`

	> [!NOTE]
	> These values are not real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Users can also enter the url values with respect to their own customer domain and they may not be necessarily of the pattern `freedcamp.com`, they can enter any customer domain specific value, specific to their application instance. Also you can contact [Freedcamp Client support team](mailto:devops@freedcamp.com) for further information on url patterns.

4. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, click **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

	![The Certificate download link](common/certificatebase64.png)

6. On the **Set up Freedcamp** section, copy the appropriate URL(s) as per your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

	a. Login URL

	b. Azure AD Identifier

	c. Logout URL

### Configure Freedcamp Single Sign-On

1. In a different web browser window, sign in to Freedcamp as a Security Administrator.

2. On the top-right corner of the page, click on **profile** and then navigate to **My Account**.

	![Freedcamp configuration](./media/freedcamp-tutorial/config01.png)

3. From the left side of the menu bar, click on **SSO** and on the **Your SSO connections** page perform the following steps:

	![Freedcamp configuration](./media/freedcamp-tutorial/config02.png)

	a. In the **Title** text box, type the title.

	b. In the **Entity ID** text box, Paste the **Azure AD Identifier** value, which you have copied from the Azure portal.

	c. In the **Login URL** text box, Paste the **Login URL** value, which you have copied from the Azure portal.

	d. Open the Base64 encoded certificate in notepad, copy its content and paste it into the **Certificate** text box.

	e. Click **Submit**.

### Create an Azure AD test user 

The objective of this section is to create a test user in the Azure portal called Britta Simon.

1. In the Azure portal, in the left pane, select **Azure Active Directory**, select **Users**, and then select **All users**.

    ![The "Users and groups" and "All users" links](common/users.png)

2. Select **New user** at the top of the screen.

    ![New user Button](common/new-user.png)

3. In the User properties, perform the following steps.

    ![The User dialog box](common/user-properties.png)

    a. In the **Name** field, enter **BrittaSimon**.
  
    b. In the **User name** field, type `brittasimon@yourcompanydomain.extension`. For example, BrittaSimon@contoso.com

    c. Select **Show password** check box, and then write down the value that's displayed in the Password box.

    d. Click **Create**.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Freedcamp.

1. In the Azure portal, select **Enterprise Applications**, select **All applications**, then select **Freedcamp**.

	![Enterprise applications blade](common/enterprise-applications.png)

2. In the applications list, select **Freedcamp**.

	![The Freedcamp link in the Applications list](common/all-applications.png)

3. In the menu on the left, select **Users and groups**.

    ![The "Users and groups" link](common/users-groups-blade.png)

4. Click the **Add user** button, then select **Users and groups** in the **Add Assignment** dialog.

    ![The Add Assignment pane](common/add-assign-user.png)

5. In the **Users and groups** dialog, select **Britta Simon** in the Users list, then click the **Select** button at the bottom of the screen.

6. If you are expecting any role value in the SAML assertion then in the **Select Role** dialog select the appropriate role for the user from the list, then click the **Select** button at the bottom of the screen.

7. In the **Add Assignment** dialog, click the **Assign** button.

### Create Freedcamp test user

To enable Azure AD users to sign in to Freedcamp, they must be provisioned into Freedcamp. In Freedcamp, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. In a different web browser window, sign in to Freedcamp as a Security Administrator.

2. On the top-toright corner of the page, click on **profile** and then navigate to **Manage System**.

	![Freedcamp configuration](./media/freedcamp-tutorial/config03.png)

3. On the right side of the Manage System page, perform the following steps:

	![Freedcamp configuration](./media/freedcamp-tutorial/config04.png)

	a. Click on **Add or invite Users**.

	b. In the **Email** text box, enter the email of user like `Brittasimon@contoso.com`.

	c. Click **Add User**.

### Test single sign-on 

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Freedcamp tile in the Access Panel, you should be automatically signed in to the Freedcamp for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## Additional Resources

- [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [What is application access and single sign-on with Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [What is conditional access in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

