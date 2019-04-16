---
title: 'Tutorial: Azure Active Directory integration with Settling music | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Settling music.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore

ms.assetid: 6f86a8a2-4bd0-40cc-b1b4-752fce123328
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2018
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with Settling music

In this tutorial, you learn how to integrate Settling music with Azure Active Directory (Azure AD).

Integrating Settling music with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Settling music.
- You can enable your users to automatically get signed-on to Settling music (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with Settling music, you need the following items:

- An Azure AD subscription
- A Settling music single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Settling music from the gallery
1. Configuring and testing Azure AD single sign-on

## Adding Settling music from the gallery
To configure the integration of Settling music into Azure AD, you need to add Settling music from the gallery to your list of managed SaaS apps.

**To add Settling music from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

	![The Azure Active Directory button][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

	![The Enterprise applications blade][2]
	
1. To add new application, click **New application** button on the top of dialog.

	![The New application button][3]

1. In the search box, type **Settling music**, select **Settling music** from result panel then click **Add** button to add the application.

	![Settling music in the results list](./media/settlingmusic-tutorial/tutorial_settlingmusic_addfromgallery.png)

## Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Settling music based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Settling music is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Settling music needs to be established.

To configure and test Azure AD single sign-on with Settling music, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Create a Settling music test user](#create-a-settling-music-test-user)** - to have a counterpart of Britta Simon in Settling music that is linked to the Azure AD representation of user.
1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Settling music application.

**To configure Azure AD single sign-on with Settling music, perform the following steps:**

1. In the Azure portal, on the **Settling music** application integration page, click **Single sign-on**.

	![Configure single sign-on link][4]

1. On the **Single sign-on** dialog, select **Mode** as	**SAML-based Sign-on** to enable single sign-on.
 
	![Single sign-on dialog box](./media/settlingmusic-tutorial/tutorial_settlingmusic_samlbase.png)

1. On the **Settling music Domain and URLs** section, perform the following steps:

	![Settling music Domain and URLs single sign-on information](./media/settlingmusic-tutorial/tutorial_settlingmusic_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`

	b. In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.rakurakuseisan.jp/<USERACCOUNT>/`

	> [!NOTE] 
	> These values are not real. Update these values with the actual Sign-On URL and Identifier. Contact [Settling music Client support team](https://rakurakuseisan.jp/) to get these values. 
 
1. On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.

	![The Certificate download link](./media/settlingmusic-tutorial/tutorial_settlingmusic_certificate.png) 

1. Click **Save** button.

	![Configure Single Sign-On Save button](./media/settlingmusic-tutorial/tutorial_general_400.png)

1. On the **Settling music Configuration** section, click **Configure Settling music** to open **Configure sign-on** window. Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**

	![Settling music Configuration](./media/settlingmusic-tutorial/tutorial_settlingmusic_configure.png) 

1. In a different web browser window, login to Settling music as a Security Administrator.

1. On top of the page, click **management** tab.

	![Settling music step1](./media/settlingmusic-tutorial/tutorial_settlingmusic_step1.png)

1. Click on  **System setting** tab.

	![Settling music step2](./media/settlingmusic-tutorial/tutorial_settlingmusic_step2.png)

1. Switch to **Security** tab.

	![Settling music step3](./media/settlingmusic-tutorial/tutorial_settlingmusic_step3.png)

1. On the **Single sign-on setting** section, perform the following steps:

	![Settling music step5](./media/settlingmusic-tutorial/tutorial_settlingmusic_step4.png)

	a. Click **To enable**.

	b. In the **Login URL of the ID provider** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.

	c. In the **ID provider logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.

	d. Click **Choose File** to upload the **Certificate (Base64)** which you have downloaded form Azure portal.

	e. Click the **Save** button.

### Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/settlingmusic-tutorial/create_aaduser_01.png)

1. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/settlingmusic-tutorial/create_aaduser_02.png)

1. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/settlingmusic-tutorial/create_aaduser_03.png)

1. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/settlingmusic-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### Create a Settling music test user

In this section, you create a user called Britta Simon in Settling music. Work with [Settling music Client support team](https://rakurakuseisan.jp/) to add the users in the Settling music platform. Users must be created and activated before you use single sign-on.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Settling music.

![Assign the user role][200] 

**To assign Britta Simon to Settling music, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201] 

1. In the applications list, select **Settling music**.

	![The Settling music link in the Applications list](./media/settlingmusic-tutorial/tutorial_settlingmusic_app.png)  

1. In the menu on the left, click **Users and groups**.

	![The "Users and groups" link][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![The Add Assignment pane][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
	
### Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Settling music tile in the Access Panel, you should get automatically signed-on to your Settling music application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/settlingmusic-tutorial/tutorial_general_01.png
[2]: ./media/settlingmusic-tutorial/tutorial_general_02.png
[3]: ./media/settlingmusic-tutorial/tutorial_general_03.png
[4]: ./media/settlingmusic-tutorial/tutorial_general_04.png

[100]: ./media/settlingmusic-tutorial/tutorial_general_100.png

[200]: ./media/settlingmusic-tutorial/tutorial_general_200.png
[201]: ./media/settlingmusic-tutorial/tutorial_general_201.png
[202]: ./media/settlingmusic-tutorial/tutorial_general_202.png
[203]: ./media/settlingmusic-tutorial/tutorial_general_203.png

