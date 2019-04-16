---
title: Create a NetApp account for Access Azure NetApp Files | Microsoft Docs
description: Describes how to access Azure NetApp Files and create a NetApp account so that you can set up a capacity pool and create a volume.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''

ms.assetid:
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/28/2018
ms.author: b-juche
---
# Create a NetApp account
Creating a NetApp account enables you to set up a capacity pool and subsequently create a volume. You use the Azure NetApp Files blade to create a new NetApp account.

## Before you begin
You must have registered your subscription for using the NetApp Resource Provider and the public preview feature.

[Register for Azure NetApp Files](azure-netapp-files-register.md)

## Steps 

1. Sign in to the Azure portal. 
2. Access the Azure NetApp Files blade by using one of the following methods:  
   * Search for **Azure NetApp Files** in the Azure portal search box.  
   * Click **All services** in the navigation, and then filter to Azure NetApp Files.  

   You can "favorite" the Azure NetApp Files blade by clicking the star icon next to it. 

3. Click **+ Add** to create a new NetApp account.  
   The New NetApp account window appears.  

4. Provide the following information for your NetApp account: 
   * **Account name**  
     Specify a unique name for the subscription.
   * **Subscription**  
     Select a subscription from your existing subscriptions.
   * **Resource group**   
     Use an existing Resource Group or create a new one.
   * **Location**  
     Select the region where you want the account and its child resources to be located.  

     ![New NetApp account](../media/azure-netapp-files/azure-netapp-files-new-netapp-account.png)


5. Click **Create**.     
   The NetApp account you created now appears in the Azure NetApp Files blade. 

## Next steps  

[Set up a capacity pool](azure-netapp-files-set-up-capacity-pool.md)

