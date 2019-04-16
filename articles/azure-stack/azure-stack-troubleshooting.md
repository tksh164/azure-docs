---
title: Microsoft Azure Stack troubleshooting | Microsoft Docs
description: Azure Stack troubleshooting.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''

ms.assetid: a20bea32-3705-45e8-9168-f198cfac51af
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2019
ms.author: jeffgilb
ms.reviewer: unknown
ms.lastreviewed: 01/23/2019

---
# Microsoft Azure Stack troubleshooting

This document provides common troubleshooting information for Azure Stack. 

> [!NOTE]
> Because the Azure Stack Technical Development Kit (ASDK) is offered as an evaluation environment, there is no official support from Microsoft Customer Support Services. If you are experiencing an issue, make sure to check the [Azure Stack MSDN Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) for further assistance and information.  

The recommendations for troubleshooting issues that are described in this section are derived from several sources and may or may not resolve your particular issue. Code examples are provided as is and expected results cannot be guaranteed. This section is subject to frequent edits and updates as improvements to the product are implemented.

## Deployment
### General deployment failure
If you experience a failure during installation, you can restart the deployment from the failed step by using the -rerun option of the deployment script.  

### At the end of ASDK deployment, the PowerShell session is still open and doesn’t show any output.
This behavior is probably just the result of the default behavior of a PowerShell command window, when it has been selected. The development kit deployment has succeeded but the script was paused when selecting the window. You can verify setup has completed by looking for the word "select" in the titlebar of the command window.  Press the ESC key to unselect it, and the completion message should be shown after it.

### Deployment fails due to lack of external access
When deployment fails at stages where external access is required, an exception like the following example will be returned:

```
An error occurred while trying to test identity provider endpoints: System.Net.WebException: The operation has timed out.
   at Microsoft.PowerShell.Commands.WebRequestPSCmdlet.GetResponse(WebRequest request)
   at Microsoft.PowerShell.Commands.WebRequestPSCmdlet.ProcessRecord()at, <No file>: line 48 - 8/12/2018 2:40:08 AM
```
If this error occurs, check to be sure all minimum networking requirements have been met by reviewing the [deployment network traffic documentation](deployment-networking.md). A network checker tool is also available for partners as part of the Partner Toolkit.

Deployment failures with the above exception are typically due to problems connecting to resources on the Internet

To verify this is your issue, you can perform the following steps:

1. Open Powershell
2. Enter-PSSession to the WAS01 or any of the ERCs VMs
3. Run the commandlet: Test-NetConnection login.windows.net -port 443

If this command fails, verify the TOR switch and any other network devices are configured to [allow network traffic](azure-stack-network.md).

## Virtual machines
### Default image and gallery item
A Windows Server image and gallery item must be added before deploying VMs in Azure Stack.

### After restarting my Azure Stack host, some VMs may not automatically start.
After rebooting your host, you may notice Azure Stack services are not immediately available.  This is because Azure Stack [infrastructure VMs](../azure-stack/asdk/asdk-architecture.md#virtual-machine-roles) and resource providers take some time to check consistency, but will eventually start automatically.

You may also notice that tenant VMs don't automatically start after a reboot of the Azure Stack development kit host. This is a known issue, and just requires a few manual steps to bring them online:

1.  On the Azure Stack development kit host, start **Failover Cluster Manager** from the Start Menu.
2.  Select the cluster **S-Cluster.azurestack.local**.
3.  Select **Roles**.
4.  Tenant VMs appear in a *saved* state. Once all Infrastructure VMs are running, right-click the tenant VMs and select **Start** to resume the VM.

### I have deleted some virtual machines, but still see the VHD files on disk. Is this behavior expected?
Yes, this is expected behavior. It was designed this way because:

* When you delete a VM, VHDs are not deleted. Disks are separate resources in the resource group.
* When a storage account gets deleted, the deletion is visible immediately through Azure Resource Manager, but the disks it may contain are still kept in storage until garbage collection runs.

If you see "orphan" VHDs, it is important to know if they are part of the folder for a storage account that was deleted. If the storage account was not deleted, it's normal they are still there.

You can read more about configuring the retention threshold and on-demand reclamation in [manage storage accounts](azure-stack-manage-storage-accounts.md).

## Storage
### Storage reclamation
It may take up to 14 hours for reclaimed capacity to show up in the portal. Space reclamation depends on various factors including usage percentage of internal container files in block blob store. Therefore, depending on how much data is deleted, there is no guarantee on the amount of space that could be reclaimed when garbage collector runs.

