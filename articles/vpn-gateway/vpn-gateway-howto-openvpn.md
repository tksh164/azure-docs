---
title: 'How to configure OpenVPN on Azure VPN Gateway: PowerShell| Microsoft Docs'
description: Steps to configure OpenVPN for Azure VPN Gateway
services: vpn-gateway
author: cherylmc

ms.service: vpn-gateway
ms.topic: conceptual
ms.date: 01/16/2019
ms.author: cherylmc

---
# Configure OpenVPN for Azure point-to-site VPN Gateway (Preview)

This article helps you set up **OpenVPN® Protocol** on Azure VPN Gateway. The article assumes that you already have a working point-to-site environment. If you do not, use the instructions in step 1 to create a point-to-site VPN.

> [!IMPORTANT]
> This Public Preview is provided without a service level agreement and should not be used for production workloads. Certain features may not be supported, may have constrained capabilities, or may not be available in all Azure locations. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for details.

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="register"></a>Register this feature

Click the **TryIt** in these steps to register this feature easily using Azure Cloud Shell.

>[!NOTE]
>If you don't register this feature, you will not be able to use it.
>

After clicking **TryIt** to open the Azure Cloud Shell, copy and paste the following commands:

```azurepowershell-interactive
Register-AzProviderFeature -ProviderNamespace Microsoft.Network -FeatureName AllowVnetGatewayOpenVpnProtocol
```
 
```azurepowershell-interactive
Get-AzProviderFeature -ProviderNamespace Microsoft.Network -FeatureName AllowVnetGatewayOpenVpnProtocol
```

Once the feature shows as registered, reregister the subscription to Microsoft.Network namespace.

```azurepowershell-interactive
Register-AzResourceProvider -ProviderNamespace Microsoft.Network
```

## <a name="vnet"></a>1. Create a point-to-site VPN

If you don't already have a functioning point-to-site environment, follow the instruction to create one. See [Create a point-to-site VPN](vpn-gateway-howto-point-to-site-resource-manager-portal.md) to create and configure a point-to-site VPN gateway with native Azure certificate authentication. 

> [!IMPORTANT]
> The Basic SKU is not supported for OpenVPN.

## <a name="enable"></a>2. Enable OpenVPN on the gateway

Enable OpenVPN on your gateway. Make sure that the gateway is already configured for point-to-site (IKEv2 or SSTP) before running the following commands:

```azurepowershell-interactive
$gw = Get-AzVirtualNetworkGateway -ResourceGroupName $rgname -name $name
Set-AzVirtualNetworkGateway -VirtualNetworkGateway $gw -VpnClientProtocol OpenVPN
```

## Next steps

To configure clients for OpenVPN, see [Configure OpenVPN clients](vpn-gateway-howto-openvpn-clients.md).

**"OpenVPN" is a trademark of OpenVPN Inc.**