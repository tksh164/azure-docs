---
title: Using API version profiles with Ruby in Azure Stack | Microsoft Docs
description: Learn about using API version profiles with Ruby in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''

ms.assetid: B82E4979-FB78-4522-B9A1-84222D4F854B
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2019
ms.author: sethm
ms.reviewer: sijuman
ms.lastreviewed: 01/09/2019

---

# Use API version profiles with Ruby in Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

## Ruby and API version profiles

The Ruby SDK for the Azure Stack Resource Manager provides tools to help you build and manage your infrastructure. Resource providers in the SDK include compute, virtual networks, and storage with the Ruby language. API profiles in the Ruby SDK enable hybrid cloud development by helping you switch between global Azure resources and resources on Azure Stack.

An API profile is a combination of resource providers and service versions. You can use an API profile to combine different resource types.

- To use the latest versions of all the services, use the **Latest** profile of the Azure SDK rollup gem.
- To use the services compatible with the Azure Stack, use the **V2018_03_01** profile of the Azure SDK rollup gem.
- To use the latest **api-version** of a service, use the **Latest** profile of the specific gem. For example, if you would like to use the latest **api-version** of compute service alone, use the **Latest** profile of the **Compute** gem.
- To use a specific **api-version** for a service, use the specific API versions defined inside the gem.

> [!NOTE]
> You can combine all of the options in the same application.

## Install the Azure Ruby SDK

- Follow the official instructions to install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
- Follow the official instructions to install [Ruby](https://www.ruby-lang.org/en/documentation/installation/).
  - While installing, choose **Add Ruby to PATH variable**.
  - Install the development kit during Ruby installation when prompted.
  - Next, install the bundler using the following command:  
    `Gem install bundler`
- If not available, create a subscription and save the subscription ID to be used later. Instructions to create a subscription are [here](../azure-stack-subscribe-plan-provision-vm.md).
- Create a service principal and save its ID and secret. Instructions to create a service principal for Azure Stack are [here](../azure-stack-create-service-principals.md).
- Make sure your service principal has contributor/owner role on your subscription. Instructions on how to assign role to service principal are [here](../azure-stack-create-service-principals.md).

## Install the Rubygem packages

You can install the Azure Rubygem packages directly.

```Ruby  
gem install azure_mgmt_compute
gem install azure_mgmt_storage
gem install azure_mgmt_resources
gem install azure_mgmt_network
Or use them in your Gemfile.
gem 'azure_mgmt_storage'
gem 'azure_mgmt_compute'
gem 'azure_mgmt_resources'
gem 'azure_mgmt_network'
```

The Azure Resource Manager Ruby SDK is in preview and will likely have breaking interface changes in upcoming releases. An increased number in the minor version may indicate breaking changes.

## Use the azure_sdk gem

The gem, **azure_sdk**, is a rollup of all the supported gems in the Ruby SDK. This gem consists of a **Latest** profile, which supports the latest version of all services. It introduces two versioned profile **V2017_03_09** and **V2018_03_01** profiles, which are built for Azure Stack.

You can install the azure_sdk rollup gem with the following command:  

```Ruby  
gem install 'azure_sdk'
```

## Prerequisites

In order to use the Ruby Azure SDK with Azure Stack, you must supply the following values, and then set the values with environment variables. See the instructions after the table for your operating system on setting the environmental variables.

| Value | Environment variables | Description |
| --- | --- | --- |
| Tenant ID | AZURE_TENANT_ID | The value of your Azure Stack [tenant ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-overview). |
| Client ID | AZURE_CLIENT_ID | The service principal application ID saved when service principal was created on the previous section of this document.  |
| Subscription ID | AZURE_SUBSCRIPTION_ID | The [subscription ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview#subscriptions) is how you access offers in Azure Stack. |
| Client Secret | AZURE_CLIENT_SECRET | The service principal application Secret saved when service principal was created. |
| Resource Manager Endpoint | ARM_ENDPOINT | See [The Azure Stack resource manager endpoint](#the-azure-stack-resource-manager-endpoint).  |

### The Azure Stack resource manager endpoint

The Microsoft Azure Resource Manager is a management framework that allows administrators to deploy, manage and monitor Azure resources. Azure Resource Manager can handle these tasks as a group, rather than individually, in a single operation.

You can get the metadata information from the Resource Manager endpoint. The endpoint returns a JSON file with the information required to run your code.

 > [!NOTE]  
 > The **ResourceManagerUrl** in the Azure Stack Development Kit (ASDK) is: `https://management.local.azurestack.external/`
 > The **ResourceManagerUrl** in integrated systems is: `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`  
 > To retrieve the metadata required: `<ResourceManagerUrl>/metadata/endpoints?api-version=1.0`
  
 Sample JSON file:

 ```json
 {
   "galleryEndpoint": "https://portal.local.azurestack.external:30015/",  
   "graphEndpoint": "https://graph.windows.net/",  
   "portal Endpoint": "https://portal.local.azurestack.external/",
   "authentication": {
     "loginEndpoint": "https://login.windows.net/",
     "audiences": ["https://management.<yourtenant>.onmicrosoft.com/3cc5febd-e4b7-4a85-a2ed-1d730e2f5928"]
   }
 }
```

### Set environmental variables

**Microsoft Windows**  
To set the environment variables, in a Windows command prompt, use the following format:  
`set AZURE_TENANT_ID=<YOUR_TENANT_ID>`

**macOS, Linux, and Unix-based systems**
In Unix based systems, you can use the following command:  
`export AZURE_TENANT_ID=<YOUR_TENANT_ID>`

## Existing API profiles

The Azure_sdk rollup gem has the following three profiles:

1. **V2018_03_01**
  Profile built for Azure Stack. Use this profile for utilizing all the latest versions of services available in Azure Stack.
2. **V2017_03_09**  
  Profile built for Azure Stack. Use this profile for services to be most compatible with the Azure Stack.
3. **Latest**  
  Profile consists of latest versions of all services. Use the latest versions of all the services.

For more information about Azure Stack and API profiles, see the [Summary of API profiles](azure-stack-version-profiles.md#summary-of-api-profiles).

## Azure Ruby SDK API profile usage

You can use the following code to instantiate a profile client. This parameter is only required for Azure Stack or other private clouds. Global Azure already has these settings by default.

```Ruby  
active_directory_settings = get_active_directory_settings(ENV['ARM_ENDPOINT'])

provider = MsRestAzure::ApplicationTokenProvider.new(
  ENV['AZURE_TENANT_ID'],
  ENV['AZURE_CLIENT_ID'],
  ENV['AZURE_CLIENT_SECRET'],
  active_directory_settings
)
credentials = MsRest::TokenCredentials.new(provider)
options = {
  credentials: credentials,
  subscription_id: subscription_id,
  active_directory_settings: active_directory_settings,
  base_url: ENV['ARM_ENDPOINT']
}

# Target profile built for Azure Stack
client = Azure::Resources::Profiles::V2018_03_01::Mgmt::Client.new(options)
```

The profile client can be used to access individual resource providers, such as compute, storage, and network:

```Ruby  
# To access the operations associated with Compute
profile_client.compute.virtual_machines.get 'RESOURCE_GROUP_NAME', 'VIRTUAL_MACHINE_NAME'

# Option 1: To access the models associated with Compute
purchase_plan_obj = profile_client.compute.model_classes.purchase_plan.new

# Option 2: To access the models associated with Compute
# Notice Namespace: Azure::Profiles::<Profile Name>::<Service Name>::Mgmt::Models::<Model Name>
purchase_plan_obj = Azure::Profiles::V2018_03_01::Compute::Mgmt::Models::PurchasePlan.new
```

## Define Azure Stack environment setting functions

To authenticate the service principal to the Azure Stack environment, define the endpoints using `get_active_directory_settings()`. This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables:

```Ruby  
# Get Authentication endpoints using Arm Metadata Endpoints
def get_active_directory_settings(armEndpoint)
  settings = MsRestAzure::ActiveDirectoryServiceSettings.new
  response = Net::HTTP.get_response(URI("#{armEndpoint}/metadata/endpoints?api-version=1.0"))
  status_code = response.code
  response_content = response.body
  unless status_code == "200"
    error_model = JSON.load(response_content)
    fail MsRestAzure::AzureOperationError.new("Getting Azure Stack Metadata Endpoints", response, error_model)
  end
  result = JSON.load(response_content)
  settings.authentication_endpoint = result['authentication']['loginEndpoint'] unless result['authentication']['loginEndpoint'].nil?
  settings.token_audience = result['authentication']['audiences'][0] unless result['authentication']['audiences'][0].nil?
  settings
end
```

## Samples using API profiles

You can use the following samples found on GitHub as references for creating solutions with Ruby and Azure Stack API profiles:

- [Manage Azure resources and resource groups with Ruby](https://github.com/Azure-Samples/Hybrid-Resource-Manager-Ruby-Resources-And-Groups)
- [Manage virtual machines using Ruby](https://github.com/Azure-Samples/Hybrid-Compute-Ruby-Manage-VM)
- [Deploy an SSH Enabled VM with a Template in Ruby](https://github.com/Azure-Samples/Hybrid-Resource-Manager-Ruby-Template-Deployment)

### Sample Resource Manager and groups

To run the sample, ensure that you have installed Ruby. If you are using Visual Studio Code, download the Ruby SDK extension as well.

> [!NOTE]  
> You can get the repository for the sample at "[Manage Azure resources and resource groups with Ruby](https://github.com/Azure-Samples/Hybrid-Resource-Manager-Ruby-Resources-And-Groups)".

1. Clone the repository:

   ```bash
   git clone https://github.com/Azure-Samples/Hybrid-Resource-Manager-Ruby-Resources-And-Groups.git
   ```

2. Install the dependencies using bundle:

   ```Bash
   cd Hybrid-Resource-Manager-Ruby-Resources-And-Groups
   bundle install
   ```

3. Create an Azure service principal using PowerShell and retrieve the values needed.

   For instructions on creating a service principal, see [Use Azure PowerShell to create a service principal with a certificate](../azure-stack-create-service-principals.md).

   Values needed are:
   - Tenant ID
   - Client ID
   - Client Secret
   - Subscription ID
   - Resource Manager Endpoint

   Set the following environment variables using the information you retrieved from the Service Principal you created.

   - export AZURE_TENANT_ID={your tenant id}
   - export AZURE_CLIENT_ID={your client id}
   - export AZURE_CLIENT_SECRET={your client secret}
   - export AZURE_SUBSCRIPTION_ID={your subscription id}
   - export ARM_ENDPOINT={your AzureStack Resource manager url}

   > [!NOTE]  
   > On Windows, use set instead of export.

4. Ensure the location variable is set to your Azure Stack location; for example, `LOCAL="local"`.

5. Add the following line of code if you using Azure Stack or other private clouds to target the right active directory endpoints:

   ```Ruby  
   active_directory_settings = get_active_directory_settings(ENV['ARM_ENDPOINT'])
   ```

6. In the options variable, add the Active Directory settings and the base URL to work with Azure Stack:

   ```ruby  
   options = {
   credentials: credentials,
   subscription_id: subscription_id,
   active_directory_settings: active_directory_settings,
   base_url: ENV['ARM_ENDPOINT']
   }
   ```

7. Create a profile client that targets the Azure Stack profile:

   ```ruby  
   client = Azure::Resources::Profiles::V2018_03_01::Mgmt::Client.new(options)
   ```

8. To authenticate the service principal with Azure Stack, the endpoints should be defined using **get_active_directory_settings()**. This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables:

   ```ruby  
   def get_active_directory_settings(armEndpoint)
     settings = MsRestAzure::ActiveDirectoryServiceSettings.new
     response = Net::HTTP.get_response(URI("#{armEndpoint}/metadata/endpoints?api-version=1.0"))
     status_code = response.code
     response_content = response.body
     unless status_code == "200"
       error_model = JSON.load(response_content)
       fail MsRestAzure::AzureOperationError.new("Getting Azure Stack Metadata Endpoints", response, error_model)
     end
     result = JSON.load(response_content)
     settings.authentication_endpoint = result['authentication']['loginEndpoint'] unless result['authentication']['loginEndpoint'].nil?
     settings.token_audience = result['authentication']['audiences'][0] unless result['authentication']['audiences'][0].nil?
     settings
   end
   ```

9. Run the sample.

   ```ruby
   bundle exec ruby example.rb
   ```

## Next steps

- [Install PowerShell for Azure Stack](azure-stack-powershell-install.md)
- [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md)  
