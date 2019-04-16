---
title: 'Tutorial: Azure Active Directory integration with RFPIO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba

ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with RFPIO

In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).

Integrating RFPIO with Azure AD provides you with the following benefits:

- You can control who in Azure AD who has access to RFPIO.
- You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location--the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with RFPIO, you need the following items:

- An Azure AD subscription.
- A RFPIO single sign-on-enabled subscription.

> [!NOTE]
> We don't recommend that you use a production environment to test the steps in this tutorial.

To test the steps in this tutorial, follow these recommendations:

- Do not use your production environment unless it's necessary.
- If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario that's outlined in this tutorial consists of two main building blocks:

1. Adding RFPIO from the gallery.
1. Configuring and testing Azure AD single sign-on.

## Add RFPIO from the gallery
To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.

### To add RFPIO from the gallery

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon. 

	![Active Directory][1]

1. Select **Enterprise applications**, and then select **All applications**.

	![Applications][2]
	
1. To add a new application, select the **New application** button on the top of dialog box.

	![Applications][3]

1. In the search box, type **RFPIO**.

	![Creating an Azure AD test user](./media/rfpio-tutorial/tutorial_rfpio_search.png)

1. In the results panel, select **RFPIO**, and then select the **Add** button to add the application.

	![Creating an Azure AD test user](./media/rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  Configure and test Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.

In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:

1. **Configure Azure AD Single Sign-On**--to enable your users to use this feature.
1. **Create an Azure AD test user**-- to test Azure AD single sign-on with Britta Simon.
1. **Create a RFPIO test user** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.
1. **Assign the Azure AD test user**--to enable Britta Simon to use Azure AD single sign-on.
1. **Test Single Sign-On** --to verify if the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.

**To configure Azure AD single sign-on with RFPIO, perform the following steps:**

1. In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.

	![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as	**SAML-based Sign-on** to enable single sign-on.
 
	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_samlbase.png)

1. On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url.png)

    a. In the **Identifier** textbox, type the URL: `https://www.rfpio.com`

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url1.png)

	b. Check **Show advanced URL settings**.

	c. In the **Relay State** textbox enter a string value. Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value. 

1. Check **Show advanced URL settings**. If you wish to configure the application in **SP** initiated mode:	

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url2.png)

	In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`

1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_certificate.png) 

1. Click **Save** button.

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_general_400.png)

1. In a different web browser window, login to the **RFPIO** website as an administrator.

1. Click on the bottom left corner dropdown.

	![Configure Single Sign-On](./media/rfpio-tutorial/app1.png)

1. Click on the **Organization Settings**. 

	![Configure Single Sign-On](./media/rfpio-tutorial/app2.png)

1. Click on the **FEATURES & INTEGRATION**.

	![Configure Single Sign-On](./media/rfpio-tutorial/app4.png)

1. In the **SAML SSO Configuration** Click **Edit**.

	![Configure Single Sign-On](./media/rfpio-tutorial/app3.png)

1. In this Section perform following actions:

	![Configure Single Sign-On](./media/rfpio-tutorial/app5.png)
	
	a. Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.

	> [!NOTE]
	>To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**. 

	b. Click **Validate**.

	c. After Clicking **Validate**, Flip **SAML(Enabled)** to on.

	d. Click **Submit**.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### Create an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

	![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
	
	![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
	![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
	![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

	c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### Create a RFPIO test user

To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.  
In the case of RFPIO, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your RFPIO company site as an administrator.

1. Click on the bottom left corner dropdown.

	![Configure Single Sign-On](./media/rfpio-tutorial/app1.png)

1. Click on the **Organization Settings**. 

	![Configure Single Sign-On](./media/rfpio-tutorial/app2.png)

1. Click **TEAM MEMBERS**.

	![Configure Single Sign-On](./media/rfpio-tutorial/app6.png)

1. Click on **ADD MEMBERS**.

	![Configure Single Sign-On](./media/rfpio-tutorial/app7.png)

1. In the **Add New Members** section. Perform following actions:

	![Configure Single Sign-On](./media/rfpio-tutorial/app8.png)

	a. Enter **Email address** in the **Enter one email per line** field.

	b. Please select **Role** according your requirements.

	c. Click **ADD MEMBERS**.
		
	> [!NOTE]
    > The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.

![Assign User][200] 

**To assign Britta Simon to RFPIO, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201] 

1. In the applications list, select **RFPIO**.

	![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_app.png) 

1. In the menu on the left, click **Users and groups**.

	![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
	
### Test single sign-on

In this section, you test your Azure AD single sign-on configuration by using the Access Panel.

When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).

## Additional resources

* [List of tutorials about how to integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/rfpio-tutorial/tutorial_general_01.png
[2]: ./media/rfpio-tutorial/tutorial_general_02.png
[3]: ./media/rfpio-tutorial/tutorial_general_03.png
[4]: ./media/rfpio-tutorial/tutorial_general_04.png

[100]: ./media/rfpio-tutorial/tutorial_general_100.png

[200]: ./media/rfpio-tutorial/tutorial_general_200.png
[201]: ./media/rfpio-tutorial/tutorial_general_201.png
[202]: ./media/rfpio-tutorial/tutorial_general_202.png
[203]: ./media/rfpio-tutorial/tutorial_general_203.png

