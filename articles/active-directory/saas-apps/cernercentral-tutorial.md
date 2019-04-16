---
title: 'Tutorial: Azure Active Directory integration with Cerner Central | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cerner Central.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba

ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with Cerner Central

In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).

Integrating Cerner Central with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Cerner Central
- You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with Cerner Central, you need the following items:

- An Azure AD subscription
- An approved Cerner Central System Account

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Cerner Central from the gallery
1. Configuring and testing Azure AD single sign-on

## Adding Cerner Central from the gallery
To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.

**To add Cerner Central from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

	![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

	![Applications][2]

1. To add new application, click **New application** button on top of the dialog.

	![Applications][3]

1. In the search box, type **Cerner Central**.

	![Creating an Azure AD test user](./media/cernercentral-tutorial/tutorial_cernercentral_search.png)

1. In the results panel, select **Cerner Central**, and then click **Add** button to add the application.

	![Creating an Azure AD test user](./media/cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."

For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.

To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.

**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**

1. In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.

	![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.

	![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

1. On the **Cerner Central Domain and URLs** section, perform the following steps:

	![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_url.png)

    a. In the **Identifier** textbox, type the value using the following patterns:

	| |
	|--|
	| `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
	| `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
	
    b. In the **Reply URL** textbox, type a URL using the following patterns:
	
	| |
	|--|
	| `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
	| `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/sso` |

	> [!NOTE]
	> These values are not the real. Update these values with the actual Identifier and Reply URL. Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.

1. On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_metadataurl.png)

1. Click **Save** button.

	![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_general_400.png)

1. To configure single sign-on on **Cerner Central** side, you need to send the **App Federation Metadata Url** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations). They configure the SSO on application side to complete the integration.

### Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

	![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.

	![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add**.

	![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:

	![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of Britta Simon.

	c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.

### Creating a Cerner Central test user

**Cerner Central** application allows authentication from any federated identity provider. If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning. You can find more details [here](cernercentral-provisioning-tutorial.md) on how to configure automatic user provisioning.

### Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.

![Assign User][200]

**To assign Britta Simon to Cerner Central, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

	![Assign User][201]

1. In the applications list, select **Cerner Central**.

	![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_app.png)

1. In the menu on the left, click **Users and groups**.

	![Assign User][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

	![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.

### Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application. For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).

## Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
* [Configure User Provisioning](cernercentral-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/cernercentral-tutorial/tutorial_general_203.png
