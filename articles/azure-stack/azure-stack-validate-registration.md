---
title: Validate Azure registration for Azure Stack | Microsoft Docs
description: Use the Azure Stack Readiness Checker to validate Azure registration.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''

ms.assetid:
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/23/2019
ms.author: sethm
ms.reviewer: unknown
ms.lastreviewed: 03/23/2019

---

# Validate Azure registration

Use the Azure Stack Readiness Checker tool (**AzsReadinessChecker**) to validate that your Azure subscription is ready to use with Azure Stack. Validate registration before you begin an Azure Stack deployment. The readiness checker validates that:

- The Azure subscription you use is a supported type. Subscriptions must be a Cloud Service Provider (CSP) or Enterprise Agreement (EA).
- The account you use to register your subscription with Azure can sign in to Azure and is a subscription owner.

For more information about Azure Stack registration, see [Register Azure Stack with Azure](azure-stack-registration.md).

## Get the readiness checker tool

Download the latest version of **AzsReadinessChecker** from the [PowerShell Gallery](https://aka.ms/AzsReadinessChecker).  

## Prerequisites

The following prerequisites are required:

**The computer on which the tool runs:**

- Windows 10 or Windows Server 2016, with internet connectivity.
- PowerShell 5.1 or later. To check your version, run the following PowerShell cmdlet and then review the **Major** and **Minor** versions:  

  ```powershell
  $PSVersionTable.PSVersion
  ```

- [PowerShell configured for Azure Stack](azure-stack-powershell-install.md).
- The latest version of [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker).  

**Azure Active Directory environment:**

- Identify the username and password for an account that is an owner for the Azure subscription you will use with Azure Stack.  
- Identify the subscription ID for the Azure subscription you will use.
- Identify the **AzureEnvironment** you will use. Supported values for the environment name parameter are **AzureCloud**, **AzureChinaCloud**, or **AzureUSGovernment**, depending on which Azure subscription you are using.

## Steps to validate Azure registration

1. On a computer that meets the prerequisites, open an elevated PowerShell prompt, and then run the following command to install **AzsReadinessChecker**:

   ```powershell
   Install-Module Microsoft.AzureStack.ReadinessChecker -Force
   ```

2. From the PowerShell prompt, run the following command to set `$registrationCredential` as the account that is the subscription owner. Replace `subscriptionowner@contoso.onmicrosoft.com` with your account and tenant name:

   ```powershell
   $registrationCredential = Get-Credential subscriptionowner@contoso.onmicrosoft.com -Message "Enter Credentials for Subscription Owner"
   ```

   > [!NOTE]
   > As a CSP, when using a Shared Services or IUR subscription, you must provide the credentials of a user from that respective AAD. Usually this will be similar to `subscriptionowner@iurcontoso.onmicrosoft.com`. That user must have the appropriate credentials, as described in the previous step.

3. From the PowerShell prompt, run the following to set `$subscriptionID` as the Azure subscription to use. Replace `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` with your own subscription ID:

   ```powershell
   $subscriptionID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
   ```

4. From the PowerShell prompt, run the following command to start validation of your subscription:

   - Specify the value for `AzureEnvironment` as **AzureCloud**, **AzureGermanCloud**, or **AzureChinaCloud**.  
   - Provide your Azure Active Directory administrator and your Azure Active Directory tenant name.

   ```powershell
   Invoke-AzsRegistrationValidation -RegistrationAccount $registrationCredential -AzureEnvironment AzureCloud -RegistrationSubscriptionID $subscriptionID
   ```

5. After the tool runs, review the output. Confirm the status is correct for both sign-in and the registration requirements. Successful validation output appears similar to the following example:

   ```shell
   Invoke-AzsRegistrationValidation v1.1809.1005.1 started.
   Checking Registration Requirements: OK
   Log location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessChecker.log
   Report location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json
   Invoke-AzsRegistrationValidation Completed
   ```

## Report and log file

Each time validation runs, it logs results to **AzsReadinessChecker.log** and **AzsReadinessCheckerReport.json**. The location of these files displays along with the validation results in PowerShell.

These files can help you share validation status before you deploy Azure Stack or investigate validation problems. Both files persist the results of each subsequent validation check. The report provides your deployment team confirmation of the identity configuration. The log file can help your deployment or support team investigate validation issues.

By default, both files are written to **C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json**.  

- Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.
- Use the **-CleanReport** parameter at the end of the run command to clear information about previous runs of the tool from **AzsReadinessCheckerReport.json**.

For more information, see [Azure Stack validation report](azure-stack-validation-report.md).

## Validation failures

If a validation check fails, details about the failure display in the PowerShell window. The tool also logs information to the **AzsReadinessChecker.log** file.

The following examples provide guidance on common validation failures:

### User must be an owner of the subscription

```shell
Invoke-AzsRegistrationValidation v1.1809.1005.1 started.
Checking Registration Requirements: Fail
Error Details for registration account admin@contoso.onmicrosoft.com:
The user admin@contoso.onmicrosoft.com is role(s) Reader for subscription 3f961d1c-d1fb-40c3-99ba-44524b56df2d. User must be an owner of the subscription to be used for registration.
Additional help URL https://aka.ms/AzsRemediateRegistration

Log location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessChecker.log
Report location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json
Invoke-AzsRegistrationValidation Completed
```

**Cause** - The account is not an administrator of the Azure subscription.

**Resolution** - Use an account that is an administrator of the Azure subscription that will be billed for usage from the Azure Stack deployment.

### Expired or temporary password

```shell
Invoke-AzsRegistrationValidation v1.1809.1005.1 started.
Checking Registration Requirements: Fail
Error Details for registration account admin@contoso.onmicrosoft.com:
Checking Registration failed with: Retrieving TenantId for subscription [subscription ID] using account admin@contoso.onmicrosoft.com failed with AADSTS50055: Force Change Password.
Trace ID: [Trace ID]
Correlation ID: [Correlation ID]
Timestamp: 2018-10-22 11:16:56Z: The remote server returned an error: (401) Unauthorized.

Log location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessChecker.log
Report location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json
Invoke-AzsRegistrationValidation Completed
```

**Cause** - The account cannot sign in, because the password is either expired or is temporary.

**Resolution** - In PowerShell, run the following command and follow the prompts to reset the password.

```powershell
Login-AzureRMAccount
```

Alternatively, sign in to the [Azure portal](https://portal.azure.com) as the account owner, and the user will be forced to change the password.

### Unknown user type  

```shell
Invoke-AzsRegistrationValidation v1.1809.1005.1 started.
Checking Registration Requirements: Fail
Error Details for registration account admin@contoso.onmicrosoft.com:
Checking Registration failed with: Retrieving TenantId for subscription <subscription ID> using <account> failed with unknown_user_type: Unknown User Type

Log location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessChecker.log
Report location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json
Invoke-AzsRegistrationValidation Completed
```

**Cause** - The account cannot sign in to the specified Azure Active Directory environment. In this example, **AzureChinaCloud** is specified as the **AzureEnvironment**.  

**Resolution** - Confirm that the account is valid for the specified Azure environment. In PowerShell, run the following command to verify the account is valid for a specific environment:

```powershell
Login-AzureRmAccount -EnvironmentName AzureChinaCloud
```

## Next Steps

- [Validate Azure identity](azure-stack-validate-identity.md)
- [View the readiness report](azure-stack-validation-report.md)
- [General Azure Stack integration considerations](azure-stack-datacenter-integration.md)
