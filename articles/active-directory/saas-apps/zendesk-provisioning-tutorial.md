---
title: 'Tutorial: Configure Zendesk for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Zendesk.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd-msft

ms.assetid: 01d5e4d5-d856-42c4-a504-96fa554baf66
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2019
ms.author: v-ant
ms.collection: M365-identity-device-management
---

# Tutorial: Configure Zendesk for automatic user provisioning

The objective of this tutorial is to demonstrate the steps to be performed in Zendesk and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Zendesk.

> [!NOTE]
> This tutorial describes a connector built on top of the Azure AD User Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).

## Prerequisites

The scenario outlined in this tutorial assumes that you already have the following prerequisites:

* An Azure AD tenant
* A Zendesk tenant with the [Enterprise](https://www.zendesk.com/product/pricing/) plan or better enabled
* A user account in Zendesk with Admin permissions

> [!NOTE]
> The Azure AD provisioning integration relies on the [Zendesk Rest API](https://developer.zendesk.com/rest_api/docs/core/introduction), which is available to Zendesk teams on the Enterprise plan or better.

## Adding Zendesk from the gallery

Before configuring Zendesk for automatic user provisioning with Azure AD, you need to add Zendesk from the Azure AD application gallery to your list of managed SaaS applications.

**To add Zendesk from the Azure AD application gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.

	![The Azure Active Directory button](common/select-azuread.png)

2. Navigate to **Enterprise Applications** and then select the **All Applications** option.

	![The Enterprise applications blade](common/enterprise-applications.png)

3. To add new application, click **New application** button on the top of dialog.

	![The New application button](common/add-new-app.png)

4. In the search box, type **Zendesk**, select **Zendesk** from result panel then click **Add** button to add the application.

	![Zendesk in the results list](common/search-new-app.png)

## Assigning users to Zendesk

Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Zendesk. Once decided, you can assign these users and/or groups to Zendesk by following the instructions here:

* [Assign a user or group to an enterprise app](../manage-apps/assign-user-or-group-access-portal.md)

### Important tips for assigning users to Zendesk

* Zendesk roles are automatically and dynamically populated in the Azure portal UI today. Before assigning Zendesk roles to users, ensure that an initial sync is completed against Zendesk to retrieve the latest roles in your Zendesk tenant.

* It is recommended that a single Azure AD user is assigned to Zendesk to test your initial automatic user provisioning configuration. Additional users and/or groups may be assigned later once the tests are successful.
  
* It is recommended that a single Azure AD user is assigned to Zendesk to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.

* When assigning a user to Zendesk, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configuring automatic user provisioning to Zendesk 

This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Zendesk based on user and/or group assignments in Azure AD.

> [!TIP]
> You may also choose to enable SAML-based single sign-on for Zendesk, following the instructions provided in the [Zendesk single sign-on tutorial](zendesk-tutorial.md). Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.

### To configure automatic user provisioning for Zendesk in Azure AD:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Enterprise Applications**, select **All applications**, then select **Zendesk**.

	![Enterprise applications blade](common/enterprise-applications.png)

2. In the applications list, select **Zendesk**.

	![The Zendesk link in the Applications list](common/all-applications.png)

3. Select the **Provisioning** tab.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk16.png)

4. Set the **Provisioning Mode** to **Automatic**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk1.png)

5. Under the **Admin Credentials** section, input the **Admin Username**, **Secret Token**, and **Domain** of your Zendesk's account. Examples of these values are:

   * In the **Admin Username** field, populate the username of the admin account on your Zendesk tenant. Example: admin@contoso.com.

   * In the **Secret Token** field, populate the secret token as described in Step 6.

   * In the **Domain** field, populate the subdomain of your Zendesk tenant.
     Example: For an account with a tenant URL of `https://my-tenant.zendesk.com`, your subdomain would be **my-tenant**.

6. The **Secret Token** for your Zendesk account is located in **Admin > API > Settings**.
   Ensure that **Token Access** is set to  **Enabled**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk4.png)

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk2.png)

7. Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Zendesk. If the connection fails, ensure your Zendesk account has Admin permissions and try again.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk19.png)

8. In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk9.png)

9. Click **Save**.

10. Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Zendesk**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk10.png)

11. Review the user attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Zendesk for update operations. Select the **Save** button to commit any changes.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk11.png)

12. Under the **Mappings** section, select **Synchronize Azure Active Directory Groups to ZenDesk**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk12.png)

13. Review the group attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Zendesk for update operations. Select the **Save** button to commit any changes.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk13.png)

14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).

15. To enable the Azure AD provisioning service for Zendesk, change the **Provisioning Status** to **On** in the **Settings** section.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk14.png)

16. Define the users and/or groups that you would like to provision to Zendesk by choosing the desired values in **Scope** in the **Settings** section.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk15.png)

17. When you are ready to provision, click **Save**.

	![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk18.png)

This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section. The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running. You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Zendesk.

For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).

## Connector Limitations

* Zendesk supports usage of groups for Users with Agent roles only. For more information, please refer to [Zendesk's documentation](https://support.zendesk.com/hc/en-us/articles/203661966-Creating-managing-and-using-groups).

* When a custom role is assigned to a user and/or group, the Azure AD automatic user provisioning service will also assign the default role **Agent**. Only **Agents** can be assigned a custom role. For more information, refer to this [Zendesk API documentation](https://developer.zendesk.com/rest_api/docs/support/users#json-format-for-agent-or-admin-requests).  

## Additional resources

* [Managing user account provisioning for Enterprise Apps](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## Next steps

* [Learn how to review logs and get reports on provisioning activity](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/zendesk-tutorial/tutorial_general_01.png
[2]: ./media/zendesk-tutorial/tutorial_general_02.png
[3]: ./media/zendesk-tutorial/tutorial_general_03.png
