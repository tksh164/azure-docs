---
title: PowerShell modules for Machine Learning Studio
titleSuffix: Azure Machine Learning Studio
description: Use PowerShell to create and manage Azure Machine Learning Studio workspaces, experiments, web services, and more. 
services: machine-learning
ms.service: machine-learning
ms.subservice: studio
ms.topic: conceptual

author: xiaoharper
ms.author: amlstudiodocs
ms.date: 01/25/2019
---
# PowerShell modules for Azure Machine Learning Studio

Using PowerShell modules, you can programmatically manage your Studio resources and assets such as workspaces, datasets, and web services.

You can interact with Studio resources using three Powershell modules:

* [Azure PowerShell Az](#az-rm) released in 2018, includes all functionality of AzureRM, although with different cmdlet names
* [AzureRM](#az-rm) released in 2016
* [Azure Machine Learning PowerShell classic](#classic) released in 2016

Although these modules have some similarities, each is designed for particular scenarios. This article describes the differences between the PowerShell modules, and helps you decide which ones to choose.

## <a name="choosing-modules"></a> Choosing modules

Choosing between the available PowerShell modules depends on the type of resources you are managing.

Check the [support table](#support-table) below to see which resources are supported by each module. Since PowerShell classic can be installed in parallel with either Az or AzureRM, you can install two modules and cover all resource types (classic with Az or classic with AzureRM)

However, it is not recommended to have Az and AzureRM installed at the same time. To decide between Az and AzureRM, Microsoft recommends Az for all future deployments. Use AzureRm only if there are special circumstances in your environment that require it.

To learn more about the differences between Az and AzureRM, as well as our provided migration path, see our [introduction to the Azure PowerShell Az.](https://docs.microsoft.com/powershell/azure/new-azureps-module-az)

## <a name="az-rm"></a> Azure PowerShell Az and AzureRM

Az and AzureRM both manage solutions deployed using the **Azure Resource Manager** deployment model. These resources include Studio workspaces and Studio New web services. To manage resources deployed using the classic deployment model, you should use the PowerShell classic module. If you would like to learn more about the deployment models, see the [Azure Resource Manager vs. classic deployment](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) article.

Az is now the intended PowerShell module for interacting with Azure and includes all the previous functionality of AzureRM. AzureRM will continue to receive bug fixes, but it will receive no new cmdlets or features. While there is an upgrade path from AzureRM, if you encounter problems with Az when working with Studio, report the problem and fall back to using AzureRM.

To get started with Az, follow the [installation instructions for Azure Az](https://docs.microsoft.com/powershell/azure/install-az-ps).

## <a name="classic"></a> PowerShell classic

The Studio [PowerShell classic module](https://aka.ms/amlps) allows you to manage resources deployed using the **classic deployment model**. These resources include Studio user assets, classic web services, and classic web service endpoints.

However, Microsoft recommends that you use the Resource Manager deployment model for all new resources to simplify the deployment and management of resources. If you would like to learn more about the deployment models, see the [Azure Resource Manager vs. classic deployment](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) article.

To get started with PowerShell classic, download the [release package](https://github.com/hning86/azuremlps/releases) from GitHub and follow the [instructions for installation](https://github.com/hning86/azuremlps/blob/master/README.md). The instructions explain how to unblock the downloaded/unzipped DLL and then import it into your PowerShell environment.

## <a name="support-table"></a> PowerShell support table

 **Studio workspaces** | **Az** |  **AzureRM** | **PowerShell classic** |
| --- | --- | --- | --- |
| Create/Delete workspaces | [Resource Manager templates](https://docs.microsoft.com/azure/machine-learning/studio/deploy-with-resource-manager-template) | [Resource Manager templates](https://docs.microsoft.com/azure/machine-learning/studio/deploy-with-resource-manager-template) |  |
| Manage workspace users |  |  | [Add-AmlWorkspaceUsers](https://github.com/hning86/azuremlps#add-amlworkspaceusers)|
| Manage commitment plans | [New-AzMlCommitmentPlan](https://docs.microsoft.com/powershell/module/az.machinelearning/new-azmlcommitmentplan) | [New-AzureRmMlCommitmentPlan](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/new-azurermmlcommitmentplan) |
|||
| **Web services** | **Az** | **AzureRM** | **PowerShell classic** |
| Manage web services | [New-AzMlWebService](https://docs.microsoft.com/powershell/module/az.machinelearning/new-azmlwebservice) <br> (New web services) | [New-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/new-azurermmlwebservice) <br> (New web services) |[New-AmlWebService](https://github.com/hning86/azuremlps#manage-classic-web-service) <br> (classic web services) |
| Manage endpoints/keys |  [Get-AzMlWebServiceKeys](https://docs.microsoft.com/powershell/module/az.machinelearning/get-azmlwebservicekeys) <br> (New web services) | [Get-AzureRmMlWebServiceKeys](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/get-azurermmlwebservicekeys) <br> (New web services) | [Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#manage-classic-web-servcie-endpoint) <br> (classic web services) |
|||
| **User assets** | **Az** | **AzureRM** | **PowerShell classic** |
| Manage datasets/trained models |  |  | [Get-AmlDataset](https://github.com/hning86/azuremlps#manage-user-assets-dataset-trained-model-transform) |
| Manage experiments |  |  | [Start-AmlExperiment](https://github.com/hning86/azuremlps#manage-experiment) |
| Manage custom modules |  |  | [New-AmlCustomModule](https://github.com/hning86/azuremlps#manage-custom-module) |


## Next steps
Follow these links for full documentation for the PowerShell modules:
* [AzureRM](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/#machine_learning)
* [PowerShell classic](https://aka.ms/amlps)
* [Azure PowerShell Az](https://docs.microsoft.com/powershell/module/az.machinelearning/#machine_learning)
