---
author: rothja
ms.service: billing
ms.topic: include
ms.date: 11/09/2018	
ms.author: jroth
---
| Resource | Default limit | Maximum limit |
| --- | --- | --- |
| Resources per [resource group](../articles/azure-resource-manager/resource-group-overview.md#resource-groups), per resource type |800 |Varies per resource type |
| Deployments per resource group in the deployment history |800 |800 |
| Resources per deployment |800 |800 |
| Management locks per unique scope |20 |20 |
| Number of tags per resource or resource group |15 |15 |
| Tag key length |512 |512 |
| Tag value length |256 |256 |


#### Template limits

| Value | Default limit | Maximum limit |
| --- | --- | --- |
| Parameters |256 |256 |
| Variables |256 |256 |
| Resources, which includes copy count |800 |800 |
| Outputs |64 |64 |
| Template expression |24,576 chars |24,576 chars |
| Resources in exported templates |200 |200 | 
| Template size |1 MB |1 MB |
| Parameter file size |64 KB |64 KB |

You can exceed some template limits by using a nested template. For more information, see [Use linked templates when you deploy Azure resources](../articles/azure-resource-manager/resource-group-linked-templates.md). To reduce the number of parameters, variables, or outputs, you can combine several values into an object. For more information, see [Objects as parameters](../articles/azure-resource-manager/resource-manager-objects-as-parameters.md).

If you reach the limit of 800 deployments per resource group, delete deployments from the history that are no longer needed. You can delete entries from the history with [az group deployment delete](/cli/azure/group/deployment) for the Azure CLI. You also can use [Remove-AzResourceGroupDeployment](/powershell/module/az.resources/remove-azresourcegroupdeployment) in PowerShell. Deleting an entry from the deployment history doesn't affect the deployment resources. 