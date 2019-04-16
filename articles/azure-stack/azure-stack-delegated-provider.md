---
title: Delegating offers in Azure Stack | Microsoft Docs
description: Learn how to put other people in charge of creating offers and signing up users for you.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''

ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2019
ms.author: sethm
ms.reviewer: alfredop
ms.lastreviewed: 01/09/2019

---
# Delegate offers in Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

As the Azure Stack operator, you often want to put other people in charge of signing up users and creating subscriptions. For example, if you're a service provider, you might want resellers to sign up customers and manage them on your behalf. Or, if you're part of a central IT group in an enterprise, you might want to delegate user signup to other IT staff.

Delegation makes it easier to reach and manage more users than you can do by yourself, as shown in the following figure:

![Levels of delegation](media/azure-stack-delegated-provider/image1.png)

With delegation, the delegated provider manages an offer (delegated offer) and end customers obtain subscriptions under that offer without involvement from the system administrator.

## Understand delegation roles and steps

### Delegation roles

The following roles are part of delegation:

* The *Azure Stack operator* manages the Azure Stack infrastructure and creates an offer template. The operator delegates others to provide offers to their tenant.

* The delegated Azure Stack operators are users with *Owner* or *Contributor* rights in the subscriptions called *delegated providers*. They can belong to other organizations, such as other Azure Active Directory (Azure AD) tenants.

* *Users* sign up for the offers and use them for managing their workloads, creating VMs, storing data, and so on.

### Delegation steps

There are two basic steps to setting up delegation:

1. **Create a delegated provider subscription**: Subscribe a user to an offer containing only the subscriptions service. Users who subscribe to this offer can then extend the delegated offers to other users by signing them up for those offers.

2. **Delegate an offer to the delegated provider**: This offer enables the delegated provider to create subscriptions or to extend the offer to their users. The delegated provider can now take the offer and offer it to other users.

The following figure shows the steps for setting up delegation:

![Create the delegated provider and enable them to sign up users](media/azure-stack-delegated-provider/image2.png)

#### Delegated provider requirements

To act as a delegated provider, a user establishes a relationship with the main provider by creating a subscription. This subscription identifies the delegated provider as having the right to present the delegated offers on behalf of the main provider.

After this relationship is established, the Azure Stack operator can delegate an offer to the delegated provider. The delegated provider can take the offer, rename it (but not change its substance), and offer it to its customers.

## Delegation walkthrough

The following sections provide a hands-on walkthrough for setting up a delegated provider, delegating an offer, and verifying that users can sign up for the delegated offer.

### Set up roles

To use this walkthrough, you need two Azure AD accounts in addition to your Azure Stack operator account. If you don't have these two accounts, you must create them. The accounts can belong to any Azure AD user and are referred to as the delegated provider and the user.

| **Role** | **Organizational rights** |
| --- | --- |
| Delegated provider |User |
| User |User |

 > [!NOTE]
 > In the case of a CSP-reseller, creating this delegated provider requires these users in the tenant directory (the user AAD). The Azure Stack operator must [first onboard](azure-stack-enable-multitenancy.md) that tenant AAD, and then configure usage and billing by following [these steps](azure-stack-csp-howto-register-tenants.md).

### Identify the delegated provider

1. Sign in to the administrator portal as an Azure Stack operator.

1. To create an offer that enables a user to become a delegated provider:

   a.  [Create a plan](azure-stack-create-plan.md).
       This plan should include only the subscription service. This article uses a plan named **PlanForDelegation** as an example.

   b.  [Create an offer](azure-stack-create-offer.md) based on this plan. This article uses an offer named **OfferToDP** as an example.

   c.  Add the delegated provider as a subscriber to this offer by selecting **Subscriptions**, then **Add**, then **New Tenant Subscription**.

   ![Add the delegated provider as a subscriber](media/azure-stack-delegated-provider/image3.png)

   > [!NOTE]
   > As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and letting the Azure Stack operator manage the sign-up. Delegated providers are usually a small group. You want to control who is admitted to it, so keeping this offer private makes sense in most cases.

### Azure Stack operator creates the delegated offer

The next step is to create the plan and offer that you're going to delegate, and that your users will use. It's a good idea to define this offer exactly as you want users to see it, because the delegated provider cannot change the plans and quotas it includes.

1. As an Azure Stack operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on the plan. This article uses an offer named **DelegatedOffer** as an example.

   > [!NOTE]
   > This offer does not have to be public, but you can make it public. However, in most cases you only want delegated providers to have access to the offer. After you delegate a private offer as described in the following steps, the delegated provider has access to it.

2. Delegate the offer. Go to **DelegatedOffer**. Under **Settings**, select **Delegated Providers**, then select **Add**.

3. Select the subscription for the delegated provider from the drop-down list, and then select **Delegate**.

   ![Add a delegated provider](media/azure-stack-delegated-provider/image4.png)

### Delegated provider customizes the offer

Sign in to the user portal as the delegated provider and then create a new offer by using the delegated offer as a template.

1. Select **+ Create a resource**, then **Tenant Offers + Plans**, then select **Offer**.

    ![Create a new offer](media/azure-stack-delegated-provider/image5.png)

2. Assign a name to the offer. This example uses **ResellerOffer**. Select the delegated offer on which to base it, and then select **Create**.

   ![Assign a name](media/azure-stack-delegated-provider/image6.png)

   >[!IMPORTANT]
   >It's important to understand that delegated providers can only choose offers that are delegated to them. They cannot make changes to those offers. Only an Azure Stack operator can change these offers, for example, changing their plans and quotas. A delegated provider does not construct an offer from base plans and add-on plans.

3. The delegated provider can make these offers public through their own portal URL. To make the offer public, select **Browse**, and then **Offers**. Select the offer, and then select **Change State**.

4. The public delegated offers are now visible only through the delegated portal. To find and change this URL:

    a.  Select **Browse**, then **All services**, and then under the **GENERAL** category, select **Subscriptions**. Select the delegated provider subscription; for example, **DPSubscription**, then **Properties**.

    b.  Copy the portal URL to a separate location, such as Notepad.

    ![Select the Delegated Provider Subscription](media/azure-stack-delegated-provider/dpportaluri.png)  

   You've finished creating a delegated offer as a delegated provider. Sign out as the delegated provider and close the browser window.

### Sign up for the offer

1. In a new browser window, go to the delegated portal URL that you saved in the previous step. Sign in to the portal as a user.

   >[!NOTE]
   >The delegated offers are not visible unless you use the delegated portal.

1. In the dashboard, select **Get a subscription**. You'll see that only the delegated offers that were created by the delegated provider are presented to the user.

   ![View and select offers](media/azure-stack-delegated-provider/image8.png)

The process of delegating an offer is finished. Now a user can sign up for this offer by getting a subscription to it.

## Move subscriptions between delegated providers

If needed, a subscription can be moved between new or existing delegated provider subscriptions that belong to the same directory tenant. This is done by using the PowerShell cmdlet [Move-AzsSubscription](/powershell/module/azs.subscriptions.admin).

This is useful when:

* You onboard a new team member that will take on the delegated provider role and you want to assign to this team member user subscriptions that were previously created in the default provider subscription.
* You have multiple delegated providers subscriptions in the same directory tenant (Azure Active Directory) and need to move user subscriptions between them. This scenario could be a case where a team member moves between teams and their subscription needs to be allocated to the new team.

## Next steps

* [Provision a VM](azure-stack-provision-vm.md)
