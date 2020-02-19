﻿---
title: How to generate and transfer HSM-protected keys for Azure Key Vault - Azure Key Vault | Microsoft Docs
description: Use this article to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault. Also known as BYOK or bring your own key.
services: key-vault
author: amitbapat
manager: devtiw
tags: azure-resource-manager

ms.service: key-vault
ms.topic: conceptual
ms.date: 02/17/2020
ms.author: ambapat

---

# Import HSM-protected keys to Key Vault (preview)

> [!NOTE]
> This feature is in preview and only available in **East US 2 EUAP** and **Central US EUAP** regions. 

For added assurance when using Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary. This scenario is often referred to as *bring your own key*, or BYOK. Azure Key Vault uses nCipher nShield family of HSMs (FIPS 140-2 Level 2 validated) to protect your keys.

Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.

> [!NOTE]
> This functionality is not available for Azure China 21Vianet. 
> 
> This import method is only available for [supported HSMs](#supported-hsms). 

For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-overview.md)  For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [What is Azure Key Vault?](key-vault-overview.md).

## Overview

* Generate a key (referred to as Key Exchange Key or KEK) in key vault. This must be an RSA-HSM key with 'import' as the only key operation. Only key vault premium SKU supports RSA-HSM keys.
* Download the public key of KEK as a .pem file
* Transfer KEK public key to your offline workstation connected to  on-premise HSM.
* From your offline workstation, use the BYOK tool provided by your HSM vendor to create a BYOK file. 
* The target key is encrypted with a KEK, which stays encrypted until it is transferred to the Azure Key Vault HSMs. Only the encrypted version of your key leaves the on-premise HSM.
* The KEK that is generated inside the Azure Key Vault HSMs and is not exportable. The HSMs enforce that there can be no clear version of the KEK outside the Key Vault HSMs.
* The KEK must be in the same key vault where the target key is to be imported.
* When the BYOK file is uploaded to Key Vault, Key Vault HSMs use the KEK private key to decrypt the target key material and import it as an HSM key. This operation happens entirely inside Key Vault HSMs and the target key always remains in the HSM protection boundary.

## Prerequisites

See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.

| Requirement | More information |
| --- | --- |
| A subscription to Azure |To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/) |
| A key vault (Premium SKU) to import HSM-protected keys |For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website. |
| An HSM from supported HSMs list along with BYOK tool and instructions provided by your HSM vendor | You must have access to a Hardware Security Module and basic operational knowledge of your HSMs. See [Supported HSMs](#supported-hsms). |
| Azure CLI version 2.1.0 or newer | Please see [Install the Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) for more information.|

## Supported HSMs

|HSM Vendor Name|Supported HSM models|Additional details|
|---|---|---|
|Thales|SafeNet Luna HSM 7 family with firmware version 7.3 or newer| [SafeNet Luna BYOK tool and documentation](https://supportportal.thalesgroup.com/csm?id=kb_article_view&sys_kb_id=3892db6ddb8fc45005c9143b0b961987&sysparm_article=KB0021016)|


> [!NOTE]
> To import HSM-protected keys from nCipher nShield family of HSMs [Use  legacy BYOK procedure](hsm-protected-keys-legacy.md)


## Generate and transfer your key to Azure Key Vault HSM

You will use the following steps to generate and transfer your key to an Azure Key Vault HSM:

* [Step 1: Generate a KEK](#step-1-generate-a-kek)
* [Step 2: Download KEK public key](#step-2-download-kek-public-key)
* [Step 3: Generate and prepare your key for transfer](#step-3-generate-and-prepare-your-key-for-transfer)
* [Step 4: Transfer your key to Azure Key Vault](#step-4-transfer-your-key-to-azure-key-vault)

### Step 1: Generate a KEK

The KEK (Key Exchange Key) is an RSA key generated in Key Vault's HSM. This key is used to encrypt the key to be imported (target key).

KEK must be:
1. an **RSA-HSM** key (2048-bit or 3072-bit or 4096-bit)
2. generated in the same key vault where you intend to import the target key
3. created with allowed key operations set to **import**

Use the [az keyvault key create](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-create) command to create KEK with key operations set to import. Note down the key identifier 'kid' returned from the below command. You'll need it in [Step 3](#step-3-generate-and-prepare-your-key-for-transfer).


```azurecli
az keyvault key create --kty RSA-HSM --size 4096 --name KEKforBYOK --ops import --vault-name ContosoKeyVaultHSM
```

### Step 2: Download KEK public key

Use the [az keyvault key download](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-download) to download the KEK public key into a .pem file. The target key you import is encrypted using the KEK public key.

```azurecli
az keyvault key download --name KEKforBYOK --vault-name ContosoKeyVaultHSM --file KEKforBYOK.publickey.pem
```

Transfer the KEKforBYOK.publickey.pem file to your offline workstation. You will need this file during next step.

### Step 3: Generate and prepare your key for transfer

Please refer to your HSM vendor's documentation to download and install the BYOK tool. Follow instruction from your HSM vendor to generate a target key and then create a Key Transfer Package (a BYOK file). The BYOK tool will use the key identifier from [Step 1](#step-1-generate-a-kek) and KEKforBYOK.publickey.pem file you downloaded in [Step 2](#step-2-download-kek-public-key) to generate an encrypted target key in a BYOK file.

Transfer the BYOK file to your connected workstation.

> [!NOTE] 
> Target key must be an RSA key of size 2048-bit or 3072-bit or 4096-bit. Importing Elliptic Curve keys is not supported at this time.
> <br/><strong>Known issue:</strong> Importing RSA 4K target key from SafeNet Luna HSMs fails. When the issue is resolved this document will be updated.

### Step 4: Transfer your key to Azure Key Vault

For this final step, transfer the Key Transfer Package (a BYOK file) from your disconnected workstation to the Internet-connected workstation and then use the [az keyvault key import](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-import) command to upload the BYOK file the Azure Key Vault HSM, to complete the key import.

```azurecli
az keyvault key import --vault-name ContosoKeyVaultHSM --name ContosoFirstHSMkey --byok-file KeyTransferPackage-ContosoFirstHSMkey.byok
```

If the upload is successful, you see displayed the properties of the key that you just imported.

## Next steps

You can now use this HSM-protected key in your key vault. For more information, see this price and feature [comparison](https://azure.microsoft.com/pricing/details/key-vault/).
