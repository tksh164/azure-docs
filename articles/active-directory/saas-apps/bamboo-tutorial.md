---
title: 'Tutorial: Azure Active Directory integration with SAML SSO for Bamboo by resolution GmbH | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAML SSO for Bamboo by resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore

ms.assetid: f00160c7-f4cc-43bf-af18-f04168d3767c
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with SAML SSO for Bamboo by resolution GmbH

In this tutorial, you learn how to integrate SAML SSO for Bamboo by resolution GmbH with Azure Active Directory (Azure AD).

Integrating SAML SSO for Bamboo by resolution GmbH with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to SAML SSO for Bamboo by resolution GmbH.
- You can enable your users to automatically get signed-on to SAML SSO for Bamboo by resolution GmbH (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with SAML SSO for Bamboo by resolution GmbH, you need the following items:

- An Azure AD subscription
- A SAML SSO for Bamboo by resolution GmbH single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding SAML SSO for Bamboo by resolution GmbH from the gallery
1. Configuring and testing Azure AD single sign-on

## Adding SAML SSO for Bamboo by resolution GmbH from the gallery
To configure the integration of SAML SSO for Bamboo by resolution GmbH into Azure AD, you need to add SAML SSO for Bamboo by resolution GmbH from the gallery to your list of managed SaaS apps.

**To add SAML SSO for Bamboo by resolution GmbH from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

	![The Azure Active Directory button][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

	![The Enterprise applications blade][2]
	
1. To add new application, click **New application** button on the top of dialog.

	![The New application button][3]

1. In the search box, type **SAML SSO for Bamboo by resolution GmbH**, select **SAML SSO for Bamboo by resolution GmbH** from result panel then click **Add** button to add the application.

	![SAML SSO for Bamboo by resolution GmbH in the results list](./media/bamboo-tutorial/tutorial_bamboo_addfromgallery.png)

## Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with SAML SSO for Bamboo by resolution GmbH based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Bamboo by resolution GmbH is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Bamboo by resolution GmbH needs to be established.

In SAML SSO for Bamboo by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with SAML SSO for Bamboo by resolution GmbH, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Create a SAML SSO for Bamboo by resolution GmbH test user](#create-a-saml-sso-for-bamboo-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Bamboo by resolution GmbH that is linked to the Azure AD representation of user.
1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Bamboo by resolution GmbH application.

**To configure Azure AD single sign-on with SAML SSO for Bamboo by resolution GmbH, perform the following steps:**

1. In the Azure portal, on the **SAML SSO for Bamboo by resolution GmbH** application integration page, click **Single sign-on**.

	![Configure single sign-on link][4]

1. On the **Single sign-on** dialog, select **Mode** as	**SAML-based Sign-on** to enable single sign-on.
 
	![Single sign-on dialog box](./media/bamboo-tutorial/tutorial_bamboo_samlbase.png)

1. On the **SAML SSO for Bamboo by resolution GmbH Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:

	![SAML SSO for Bamboo by resolution GmbH Domain and URLs single sign-on information](./media/bamboo-tutorial/tutorial_bamboo_url.png)

    a. In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

	b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

1. Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:

	![SAML SSO for Bamboo by resolution GmbH Domain and URLs single sign-on information](./media/bamboo-tutorial/tutorial_bamboo_url1.png)

    In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`
	 
	> [!NOTE] 
	> These values are not real. Update these values with the actual Identifier, Reply URL, and Sign-On URL. Contact [SAML SSO for Bamboo by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bamboo/server/support) to get these values. 

1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

	![The Certificate download link](./media/bamboo-tutorial/tutorial_bamboo_certificate.png) 

1. Click **Save** button.

	![Configure Single Sign-On Save button](./media/bamboo-tutorial/tutorial_general_400.png)

1. Sign-on to your SAML SSO for Bamboo by resolution GmbH company site as administrator.

1. On the right side of the main toolbar, click **Settings** > **Add-ons**.

	![The Settings](./media/bamboo-tutorial/tutorial_bamboo_setings.png)

1. Go to SECURITY section, click on **SAML SingleSignOn** on the Menubar.

	![The Samlsingle](./media/bamboo-tutorial/tutorial_bamboo_samlsingle.png)

1. On the **SAML SIngleSignOn Plugin Configuration page**, click **Add idp**. 

	![The Add idp](./media/bamboo-tutorial/tutorial_bamboo_addidp.png)

1. On the **Choose your SAML Identity Provider** Page, perform the following steps:

	![The identity provider](./media/bamboo-tutorial/tutorial_bamboo_identityprovider.png)

	a. Select **Idp Type** as **AZURE AD**.

	b. In the **Name** textbox, type the name.

	c. In the **Description** textbox, type the description.

	d. Click **Next**.

1. On the **Identity provider configuration** page click **Next**.

	![The identity config](./media/bamboo-tutorial/tutorial_bamboo_identityconfig.png)

1.  On the **Import SAML Idp Metadata** Page, click **Load File** to upload the **METADATA XML** file which you have downloaded from Azure Portal.

	![The idpmetadata](./media/bamboo-tutorial/tutorial_bamboo_idpmetadata.png)

1. Click **Next**.

1. Click **Save settings**.

	![The save](./media/bamboo-tutorial/tutorial_bamboo_save.png)
	
> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/bamboo-tutorial/create_aaduser_01.png)

1. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/bamboo-tutorial/create_aaduser_02.png)

1. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/bamboo-tutorial/create_aaduser_03.png)

1. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/bamboo-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### Create a SAML SSO for Bamboo by resolution GmbH test user

The objective of this section is to create a user called Britta Simon in SAML SSO for Bamboo by resolution GmbH. SAML SSO for Bamboo by resolution GmbH supports just-in-time provisioning and also users can be created manually, contact [SAML SSO for Bamboo by resolution GmbH Client support team](https://marketplace.atlassian.com/plugins/com.resolution.atlasplugins.samlsso-bamboo/server/support) as per your requirement.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Bamboo by resolution GmbH.

![Assign the user role][200] 

**To assign Britta Simon to SAML SSO for Bamboo by resolution GmbH, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201] 

1. In the applications list, select **SAML SSO for Bamboo by resolution GmbH**.

	![The SAML SSO for Bamboo by resolution GmbH link in the Applications list](./media/bamboo-tutorial/tutorial_bamboo_app.png)  

1. In the menu on the left, click **Users and groups**.

	![The "Users and groups" link][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![The Add Assignment pane][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
	
### Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the SAML SSO for Bamboo by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Bamboo by resolution GmbH application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bamboo-tutorial/tutorial_general_01.png
[2]: ./media/bamboo-tutorial/tutorial_general_02.png
[3]: ./media/bamboo-tutorial/tutorial_general_03.png
[4]: ./media/bamboo-tutorial/tutorial_general_04.png

[100]: ./media/bamboo-tutorial/tutorial_general_100.png

[200]: ./media/bamboo-tutorial/tutorial_general_200.png
[201]: ./media/bamboo-tutorial/tutorial_general_201.png
[202]: ./media/bamboo-tutorial/tutorial_general_202.png
[203]: ./media/bamboo-tutorial/tutorial_general_203.png

