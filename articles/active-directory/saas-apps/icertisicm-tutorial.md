---
title: 'Tutorial: Azure Active Directory integration with Icertis Contract Management Platform | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Icertis Contract Management Platform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba

ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with Icertis Contract Management Platform

In this tutorial, you learn how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).

Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Icertis Contract Management Platform
- You can enable your users to automatically get signed-on to Icertis Contract Management Platform (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:

- An Azure AD subscription
- An Icertis Contract Management Platform single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Icertis Contract Management Platform from the gallery
1. Configuring and testing Azure AD single sign-on

## Adding Icertis Contract Management Platform from the gallery
To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.

**To add Icertis Contract Management Platform from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

	![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

	![Applications][2]
	
1. To add new application, click **New application** button on the top of dialog.

	![Applications][3]

1. In the search box, type **Icertis Contract Management Platform**.

	![Creating an Azure AD test user](./media/icertisicm-tutorial/tutorial_icertisicm_search.png)

1. In the results panel, select **Icertis Contract Management Platform**, and then click **Add** button to add the application.

	![Creating an Azure AD test user](./media/icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.

In Icertis Contract Management Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Icertis Contract Management Platform, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Icertis Contract Management Platform application.

**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**

1. In the Azure portal, on the **Icertis Contract Management Platform** application integration page, click **Single sign-on**.

	![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as	**SAML-based Sign-on** to enable single sign-on.
 
	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

1. On the **Icertis Contract Management Platform Domain and URLs** section, perform the following steps:

	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_icertisicm_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`

	b. In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`

	> [!NOTE] 
	> These values are not real. Update these values with the actual Sign-On URL and Identifier. Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) to get these values. 

1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

1. Click **Save** button.

	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_general_400.png)

1. On the **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**

	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_icertisicm_configure.png) 

1. To configure single sign-on on **Icertis Contract Management Platform** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

	![Creating an Azure AD test user](./media/icertisicm-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
	
	![Creating an Azure AD test user](./media/icertisicm-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
	![Creating an Azure AD test user](./media/icertisicm-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
	![Creating an Azure AD test user](./media/icertisicm-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

	c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### Creating an Icertis Contract Management Platform test user

In this section, you create a user called Britta Simon in Icertis Contract Management Platform. Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) to add the users in the Icertis Contract Management Platform.

### Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Icertis Contract Management Platform.

![Assign User][200] 

**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201] 

1. In the applications list, select **Icertis Contract Management Platform**.

	![Configure Single Sign-On](./media/icertisicm-tutorial/tutorial_icertisicm_app.png) 

1. In the menu on the left, click **Users and groups**.

	![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
	
### Testing single sign-on

The objective of this section is to test your Azure AD SSO configuration using the Access Panel.

When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.

## Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/icertisicm-tutorial/tutorial_general_203.png

