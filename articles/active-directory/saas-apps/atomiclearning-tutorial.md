---
title: 'Tutorial: Azure Active Directory integration with Atomic Learning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Atomic Learning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba

ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with Atomic Learning

In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).

Integrating Atomic Learning with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Atomic Learning
- You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with Atomic Learning, you need the following items:

- An Azure AD subscription
- An Atomic Learning single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Atomic Learning from the gallery
1. Configuring and testing Azure AD single sign-on

## Adding Atomic Learning from the gallery
To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.

**To add Atomic Learning from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

	![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

	![Applications][2]
	
1. To add new application, click **New application** button on the top of dialog.

	![Applications][3]

1. In the search box, type **Atomic Learning**.

	![Creating an Azure AD test user](./media/atomiclearning-tutorial/tutorial_atomiclearning_search.png)

1. In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.

	![Creating an Azure AD test user](./media/atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."

For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.

In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.

**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**

1. In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.

	![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as	**SAML-based Sign-on** to enable single sign-on.
 
	![Configure Single Sign-On](./media/atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

1. On the **Atomic Learning Domain and URLs** section, perform the following steps:

	![Configure Single Sign-On](./media/atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`
	
	> [!NOTE] 
	> This value is not real. Update this value with the actual Sign-On URL. Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value. 
 
1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

	![Configure Single Sign-On](./media/atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

1. Click **Save** button.

	![Configure Single Sign-On](./media/atomiclearning-tutorial/tutorial_general_400.png)

1. To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com). They set this setting to have the SAML SSO connection set properly on both sides.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

	![Creating an Azure AD test user](./media/atomiclearning-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
	
	![Creating an Azure AD test user](./media/atomiclearning-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
	![Creating an Azure AD test user](./media/atomiclearning-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
	![Creating an Azure AD test user](./media/atomiclearning-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

	c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### Creating an Atomic Learning test user

In this section, you create a user called Britta Simon in Atomic Learning. Atomic Learning supports just-in-time provisioning, which is by default enabled. 

There is no action item for you in this section. A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.

### Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.

![Assign User][200] 

**To assign Britta Simon to Atomic Learning, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201] 

1. In the applications list, select **Atomic Learning**.

	![Configure Single Sign-On](./media/atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

1. In the menu on the left, click **Users and groups**.

	![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
	
### Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/atomiclearning-tutorial/tutorial_general_203.png

