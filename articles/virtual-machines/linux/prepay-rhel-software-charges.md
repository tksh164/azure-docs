---
title: Buy Red Hat Enterprise Linux plans - Azure Reservations | Microsoft Docs
description: Learn how you can prepay for your Red Hat usage and save money over your pay-as-you-go costs.
services: virtual-machines-linux
documentationcenter: ''
author: yashesvi
manager: yashesvi
editor: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/18/2019
ms.author: yashar
---
# Prepay for Red Hat Enterprise Linux plans from Azure Reservations

Prepay for your Red Hat usage and save money over your pay-as-you-go costs. The discounts only apply to Red Hat meters and not on the virtual machine usage. You can buy reservations for virtual machines separately to save even more.

You can buy Red Hat software plans in the Azure portal. To buy a plan:

- You must be in an Owner role for at least one Enterprise or Pay-As-You-Go subscription.
- For Enterprise subscriptions, **Add Reserved Instances** must be enabled in the [EA portal](https://ea.azure.com). Or, if that setting is disabled, you must be an EA Admin on the subscription.
- For the Cloud Solution Provider (CSP) program, the admin agents or sales agents can buy the Red Hat plans.

## Buy a Red Hat software plan

1. Go to [Reservations](https://portal.azure.com/#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) in Azure portal.
1. Select **Add** and select Red Hat Linux.
1. Fill in the required fields. Any Red Hat Linux VM that matches the attributes of what you buy gets the discount. The actual number of deployments that get the discount depend on the scope and quantity selected.

    | Field      | Description|
    |:------------|:--------------|
    |Name        |The name of this purchase.|
    |Subscription|The subscription used to pay for this plan. The payment method on the subscription is charged the upfront costs for the reservation. The subscription type must be an enterprise agreement (offer numbers: MS-AZR-0017P or MS-AZR-0148P) or Pay-As-You-Go (offer numbers: MS-AZR-0003P or MS-AZR-0023P). For an enterprise subscription, the charges are deducted from the enrollment's monetary commitment balance or charged as overage. For Pay-As-You-Go subscription, the charges are billed to the credit card or invoice payment method on the subscription.|
    |Scope       |The scope can cover one subscription or multiple subscriptions (shared scope). If you select: <ul><li>Single subscription - The plan discount is applied to Red Hat Linux usage in this subscription. </li><li>Shared - The plan discount is applied to Red Hat Linux usage in any subscription within your billing context. For enterprise customers, the shared scope is the enrollment and includes all subscriptions within the enrollment. For Pay-As-You-Go customers, the shared scope is all Pay-As-You-Go subscriptions created by the account administrator.</li></ul>|
    |Plan     |Select the Red Hat Linux plan. For help in identifying what to buy, see Understand how the Red Hat Linux Enterprise software reservation discount is applied.|
    |VM size     |Red Hat Linux pricing depends on the number of vCPUs on the VM. Select the option that represents the number of vCPUs on your Red Hat Linux VMs.|
    |Term        |One year or three years.|
    |Quantity    |The number of VMs that you're buying this Red Hat Linux plan for. The quantity is the number of running Red Hat Linux instances that can get the billing discount.|
1. Select **Purchase**.
1. Select **View this Reservation** to see the status of your purchase.

The reservation discount is automatically applied to any running Red Hat virtual machines that matches the reservation. The discount applies only to the Red Hat meter. The VM compute charges are not covered by this plan.

## Discount applies to different VM sizes

Like Reserved VM Instances, Red Hat Linux plans offer instance size flexibility. This means that your discount applies even when you deploy a VM that's a different size from the Red Hat plan you bought. For more information, see Understand how the Red Hat Linux Enterprise software reservation discount is applied.

## Cancellation and exchanges not allowed

You can't cancel or exchange a Red Hat plan that you bought. Check your usage to make sure you buy the right plan. For help in identifying what to buy, see Understand how the Red Hat Linux Enterprise software reservation discount is applied.

## Next steps

To learn how to manage a reservation, see [Manage Azure reservations](../../billing/billing-manage-reserved-vm-instance.md).

To learn more, see the following articles:

- [What are Azure Reservations?](../../billing/billing-save-compute-costs-reservations.md)
- [Manage Reservations in Azure](../../billing/billing-manage-reserved-vm-instance.md)
- Understand how the Red Hat reservation discount is applied
- [Understand reservation usage for your Pay-As-You-Go subscription](../../billing/billing-understand-reserved-instance-usage.md)
- [Understand reservation usage for your Enterprise enrollment](../../billing/billing-understand-reserved-instance-usage-ea.md)

## Need help? Contact support

If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.