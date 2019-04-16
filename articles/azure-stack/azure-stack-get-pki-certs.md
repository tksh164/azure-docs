---
title: Generate Azure Stack Public Key Infrastructure certificates for Azure Stack integrated systems deployment | Microsoft Docs
description: Describes the Azure Stack PKI certificate deployment process for Azure Stack integrated systems.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila

ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2019
ms.author: mabrigg
ms.reviewer: ppacent
ms.lastreviewed: 01/25/2019
---

# Azure Stack certificates signing request generation

You can use the Azure Stack Readiness Checker tool to create Certificate Signing Requests (CSRs) suitable for an Azure Stack deployment. Certificates should be requested, generated, and validated with enough time to test before deployment. You can get the tool [from the PowerShell Gallery](https://aka.ms/AzsReadinessChecker).

You can use the Azure Stack Readiness Checker tool (AzsReadinessChecker) to request the following certificates:

- **Standard Certificate Requests** according to [Generate PKI Certificates for Azure Stack Deployment](azure-stack-get-pki-certs.md).
- **Platform-as-a-Service**: You can request platform-as-a-service (PaaS) names for certificates as specified in [Azure Stack Public Key Infrastructure certificate requirements - Optional PaaS Certificates](azure-stack-pki-certs.md#optional-paas-certificates).

## Prerequisites

Your system should meet the following prerequisites before generating the CSR(s) for PKI certificates for an Azure Stack deployment:

- Microsoft Azure Stack Readiness Checker
- Certificate attributes:
  - Region name
  - External fully qualified domain name (FQDN)
  - Subject
- Windows 10 or Windows Server 2016

  > [!NOTE]  
  > When you receive your certificates back from your certificate authority the steps in [Prepare Azure Stack PKI certificates](azure-stack-prepare-pki-certs.md) will need to be completed on the same system!

## Generate certificate signing request(s)

Use these steps to prepare and validate the Azure Stack PKI certificates:

1. Install AzsReadinessChecker from a PowerShell prompt (5.1 or above), by running the following cmdlet:

    ```powershell  
        Install-Module Microsoft.AzureStack.ReadinessChecker
    ```

2. Declare the **subject** as an ordered dictionary. For example:

    ```powershell  
    $subjectHash = [ordered]@{"OU"="AzureStack";"O"="Microsoft";"L"="Redmond";"ST"="Washington";"C"="US"}
    ```

    > [!note]  
    > If a common name (CN) is supplied this will be overwritten by the first DNS name of the certificate request.

3. Declare an output directory that already exists. For example:

    ```powershell  
    $outputDirectory = "$ENV:USERPROFILE\Documents\AzureStackCSR"
    ```

4. Declare identity system

    Azure Active Directory

    ```powershell
    $IdentitySystem = "AAD"
    ```

    Active Directory Federation Services

    ```powershell
    $IdentitySystem = "ADFS"
    ```

5. Declare **region name** and an **external FQDN** intended for the Azure Stack deployment.

    ```powershell
    $regionName = 'east'
    $externalFQDN = 'azurestack.contoso.com'
    ```

    > [!note]  
    > `<regionName>.<externalFQDN>` forms the basis on which all external DNS names in Azure Stack are created, in this example, the portal would be `portal.east.azurestack.contoso.com`.  

6. To generate certificate signing requests for each DNS name:

    ```powershell  
    New-AzsCertificateSigningRequest -RegionName $regionName -FQDN $externalFQDN -subject $subjectHash -OutputRequestPath $OutputDirectory -IdentitySystem $IdentitySystem
    ```

    To include PaaS Services, specify the switch ```-IncludePaaS```

7. Alternatively, for Dev/Test environments, to generate a single certificate request with multiple Subject Alternative Names add **-RequestType SingleCSR** parameter and value (**not** recommended for production environments):

    ```powershell  
    New-AzsCertificateSigningRequest -RegionName $regionName -FQDN $externalFQDN -subject $subjectHash -RequestType SingleCSR -OutputRequestPath $OutputDirectory -IdentitySystem $IdentitySystem
    ```

    To include PaaS Services, specify the switch ```-IncludePaaS```

8. Review the output:

    ```powershell  
    New-AzsCertificateSigningRequest v1.1809.1005.1 started.

    CSR generating for following SAN(s): dns=*.east.azurestack.contoso.com&dns=*.blob.east.azurestack.contoso.com&dns=*.queue.east.azurestack.contoso.com&dns=*.table.east.azurestack.cont
    oso.com&dns=*.vault.east.azurestack.contoso.com&dns=*.adminvault.east.azurestack.contoso.com&dns=portal.east.azurestack.contoso.com&dns=adminportal.east.azurestack.contoso.com&dns=ma
    nagement.east.azurestack.contoso.com&dns=adminmanagement.east.azurestack.contoso.com*dn2=*.adminhosting.east.azurestack.contoso.com@dns=*.hosting.east.azurestack.contoso.com
    Present this CSR to your Certificate Authority for Certificate Generation: C:\Users\username\Documents\AzureStackCSR\wildcard_east_azurestack_contoso_com_CertRequest_20180405233530.req
    Certreq.exe output: CertReq: Request Created

    Log location (contains PII): C:\Users\username\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessChecker.log
    New-AzsCertificateSigningRequest Completed
    ```

9. Submit the **.REQ** file generated to your CA (either internal or public).  The output directory of **New-AzsCertificateSigningRequest** contains the CSR(s) necessary to submit to a Certificate Authority.  The directory also contains, for your reference, a child directory containing the INF file(s) used during certificate request generation. Be sure that your CA generates certificates using your generated request that meet the [Azure Stack PKI Requirements](azure-stack-pki-certs.md).

## Next steps

[Prepare Azure Stack PKI certificates](azure-stack-prepare-pki-certs.md)
