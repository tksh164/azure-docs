---
title: 'Tutorial: Azure Active Directory integration with HR2day by Merces | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HR2day by Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba

ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with HR2day by Merces

In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).

Integrating HR2day by Merces with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to HR2day by Merces.
- You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.
- You can manage your accounts in one central location--the Azure portal.

For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## Prerequisites

To configure Azure AD integration with HR2day by Merces, you need the following items:

- An Azure AD subscription.
- An HR2day by Merces single sign-on enabled subscription.

> [!NOTE]
> We don't recommend using a production environment to test the steps in this tutorial.

To test the steps in this tutorial, follow these recommendations:

- Don't use your production environment unless it's necessary.
- Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.  

## Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. 
The scenario that's outlined here consists of two main building blocks:

1. Adding HR2day by Merces from the gallery.
1. Configuring and testing Azure AD single sign-on.

## Add HR2day by Merces from the gallery
To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.

**To add HR2day by Merces from the gallery, take the following steps:**

1. In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon. 

	![Active Directory][1]

1. Go to **Enterprise applications**. Then go to **All applications**.

	![Applications][2]
	
1. To add a new application, select the **New application** button on the top of the dialog box.

	![Applications][3]

1. In the search box, type **HR2day by Merces**.

	![Creating an Azure AD test user](./media/hr2day-tutorial/tutorial_hr2daybymerces_search.png)

1. In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.

	![Creating an Azure AD test user](./media/hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  Configure and test Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."

For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD. In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.

In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.

To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:

1. Configure Azure AD single sign-on: Enable your users to use this feature.
1. Create an Azure AD test user: Test Azure AD single sign-on with Britta Simon.
1. Create an HR2day by Merces test user: Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.
1. Assign the Azure AD test user: Enable Britta Simon to use Azure AD single sign-on.
1. Test single sign-on: Verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.

**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**

1. In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.

	![Configure single sign-On][4]

1. To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.
 
	![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

1. In the **HR2day by Merces Domain and URLs** section, take the following steps:

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.

	b. In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.

	> [!NOTE] 
	> These values are not real. Update these values with the actual sign-on URL and identifier. Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values. 
 


1. On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

1. This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD. They do this by using federation that's based on the SAML protocol.

    Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token. The following screenshot shows an example of this. 

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2day_00.png)
	
   > [!NOTE]
   >  Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant. You need this value to complete the steps in the next section. 

1. In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image. Then take the following steps.
	
      | Attribute name    |   Attribute value |  
    | ------------------- | -------------------- |    
	| ATTR_LOGINCLAIM | `join([mail],"102938475Z","@"` |
	
	  a. To open the **Add Attribute** dialog, select **Add attribute**.

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_attribute_04.png)

	![Configure single sign-On](./media/hr2day-tutorial/tutorial_attribute_05.png)

	b. In the **Name** box, type **ATTR_LOGINCLAIM**.

	c. From the **Value** list, select **Join()**.

	d. From the **String1** list, select **user.mail**.

	e. For **String2**, type the unique identifier that's provided by your HR2day team.

	f. In the **Separator** box, type **\@**.
	
	g. Select **Ok**.

1. Select the **Save** button.

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_general_400.png)

1. In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window. Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

1. To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl). Attach the downloaded **Certificate(Base64)** file to your email. Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.

    > [!NOTE]
    >Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.

	> [!TIP]
   	>You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab. Then access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).
   > 

### Create an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, take the following steps:**

1. In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.

	![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups**, and then select **All users**.
	
	![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog box, select **Add** on the top of the dialog box.
 
	![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_03.png) 

1. In the **User** dialog box, take the following steps:
 
	![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_04.png) 

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the **email address** of BrittaSimon.

    c. Select **Show Password**, and then write down the password.

    d. Select **Create**.
 
### Create an HR2day by Merces test user

The objective of this section is to create a user called Britta Simon in HR2day by Merces. To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl). 

> [!NOTE]
> If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.

![Assign user][200] 

**To assign Britta Simon to HR2day by Merces, take the following steps:**

1. In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**. Next, select **All applications**.

	![Assign user][201] 

1. In the applications list, select **HR2day by Merces**.

	![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

1. In the menu on the left, select **Users and groups**.

	![Assign user][202] 

1. Select the **Add** button. Then, in the **Add Assignment** dialog box, select **Users and groups**.

	![Assign user][203]

1. In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.

1. Click the **Select** button.

1. In the **Add Assignment** dialog box, select **Assign**.
	
### Test single sign-on

The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.  

When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.

## Additional resources

* [List of tutorials about how to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hr2day-tutorial/tutorial_general_01.png
[2]: ./media/hr2day-tutorial/tutorial_general_02.png
[3]: ./media/hr2day-tutorial/tutorial_general_03.png
[4]: ./media/hr2day-tutorial/tutorial_general_04.png

[100]: ./media/hr2day-tutorial/tutorial_general_100.png

[200]: ./media/hr2day-tutorial/tutorial_general_200.png
[201]: ./media/hr2day-tutorial/tutorial_general_201.png
[202]: ./media/hr2day-tutorial/tutorial_general_202.png
[203]: ./media/hr2day-tutorial/tutorial_general_203.png

