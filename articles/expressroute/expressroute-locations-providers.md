---
title: 'Locations and connectivity providers: Azure ExpressRoute | Microsoft Docs'
description: This article provides a detailed overview of locations where services are offered and how to connect to Azure regions. Sorted by location.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''

ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2019
ms.author: pareshmu
---
# ExpressRoute partners and peering locations

> [!div class="op_single_selector"]
> * [Locations By Provider](expressroute-locations.md)
> * [Providers By Location](expressroute-locations-providers.md)


The tables in this article provide information on ExpressRoute connectivity providers, ExpressRoute geographical coverage, Microsoft cloud services supported over ExpressRoute, and ExpressRoute System Integrators (SIs).

## <a name="partners"></a>ExpressRoute connectivity providers
ExpressRoute is supported across all Azure regions and locations. The following map provides a list of Azure regions and ExpressRoute locations. ExpressRoute locations refer to those where Microsoft peers with several service providers.

![Location map][0]

You will have access to Azure services across all regions within a geopolitical region if you connected to at least one ExpressRoute location within the geopolitical region. 

### Azure regions to ExpressRoute locations within a geopolitical region
The following table provides a map of Azure regions to ExpressRoute locations within a geopolitical region.

| **Geopolitical region** | **Zone** | **Azure regions** | **ExpressRoute locations** |
| --- | --- | --- | --- |
| **Australia Government** | 1 | Australia Central, Australia Central 2 |Canberra, Canberra2 |
| **Europe** | 1 |France Central, France South, North Europe, West Europe, UK West, UK South |Amsterdam, Amsterdam2, Dublin, London, London2, Marseille, Newport(Wales), Paris, Zurich |
| **North America** | 1 |East US, West US, East US 2, West US 2, Central US, South Central US, North Central US, West Central US, Canada Central, Canada East |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, New York, San Antonio, Seattle, Silicon Valley, Washington DC, Washington DC2, Montreal, Quebec City, Toronto |
| **Asia** | 2 |East Asia, Southeast Asia |Hong Kong, Kuala Lumpur, Singapore, Singapore2, Taipei |
| **Australia** | 2 |Australia Southeast, Australia East |Melbourne, Perth, Sydney | 
| **India** | 2 |India West, India Central, India South |Chennai, Chennai2, Mumbai, Mumbai2 |
| **Japan** | 2 |Japan West, Japan East |Osaka, Tokyo |
| **South Korea** | 2 |Korea Central, Korea South |Busan, Seoul|
| **UAE** | 2 | UAE Central, UAE North | Dubai |
| **South Africa** | 3 |South Africa West, South Africa North |Cape Town, Johannesburg |
| **South America** | 3 |Brazil South |Sao Paulo |

### Regions and geopolitical boundaries for national clouds
The table below provides information on regions and geopolitical boundaries for national clouds.

| **Geopolitical region** | **Azure regions** | **ExpressRoute locations** |
| --- | --- | --- |
| **US Government cloud** |US Gov Arizona, US Gov Iowa, US Gov Texas, US Gov Virginia, US DoD Central, US DoD East  |Chicago, Dallas, New York, Phoenix, San Antonio, Seattle, Silicon Valley, Washington DC |
| **China East** |China East, China East2 |Shanghai, Shanghai2 |
| **China North** |China North, China North2 |Beijing, Beijing2 |
| **Germany** |Germany Central, Germany East |Berlin, Frankfurt |

Connectivity across geopolitical regions is not supported on the standard ExpressRoute SKU. You will need to enable the ExpressRoute premium add-on to support global connectivity. Connectivity to national cloud environments is not supported. You can work with your connectivity provider if such a need arises.

## <a name="locations"></a>Connectivity provider locations

The following table shows connectivity locations and the service providers for each location. If you want to view service providers and the locations for which they can provide service, see [Locations by service provider](expressroute-locations.md#locations). 


### Production Azure
| **Location** | **Peering Location Owner** | **Service Providers** |
| --- | --- | --- |
| **Amsterdam** | Equinix | Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, euNetworks, GÉANT, InterCloud, Interxion, KPN, IX Reach, Level 3 Communications, Megaport, NTT Communications, Orange, Tata Communications, TeleCity Group, Telefonica, Telenor, Telia Carrier, Verizon, Zayo |
| **Amsterdam2** | Interxion | DE-CIX, Interxion |
| **Atlanta** | Equinix | Equinix, Megaport |
| **Busan** |LG CNS | LG CNS |
| **Canberra** | CDC | CDC |
| **Canberra2** | CDC | CDC |
| **Cape Town** | Teraco | Internet Solutions - Cloud Connect, Liquid Telecom, Teraco |
| **Chennai** | Tata Communications | Global CloudXchange (GCX), SIFY, Tata Communications |
| **Chennai2** | Airtel | Airtel |
| **Chicago** | Equinix | Aryaka Networks, AT&T NetBond, Cologix, Comcast, Coresite, Equinix, InterCloud, Internet2, Level 3 Communications, Megaport, PacketFabric, PCCW Global Limited, Sprint, Telia Carrier, Verizon, Zayo |
| **Dallas** | Equinix | Aryaka Networks, AT&T NetBond, Cologix, Equinix, Internet2, Level 3 Communications, Megaport, Neutrona Networks, Telmex Uninet, Telia Carrier, Verizon, Zayo|
| **Denver** | CoreSite | CoreSite, Megaport, Zayo |
| **Dubai** | Etisalat UAE | Etisalat UAE |
| **Dublin** | Equinix | Colt, eir, Equinix, Interxion, Megaport |
| **Hong Kong** | Equinix | Aryaka Networks, British Telecom, China Telecom Global, Equinix, Megaport, NTT Communications, Orange, PCCW Global Limited, Tata Communications, Verizon |
| **Johannesburg** | Teraco | Internet Solutions - Cloud Connect, Liquid Telecom, Teraco |
| **Kuala Lumpur** | TIME dotCom | TIME dotCom |
| **Las Vegas** | Switch | CenturyLink Cloud Connect, Megaport |
| **London** | Equinix | AT&T NetBond, British Telecom, Colt, Equinix, InterCloud, Internet Solutions - Cloud Connect, Interxion, Jisc, Level 3 Communications, Megaport, MTN, NTT Communications, Orange, PCCW Global Limited, Tata Communications, Telehouse - KDDI, Telenor, Telia Carrier, Verizon, Vodafone, Zayo |
| **London2** | Telehouse | IX Reach, Equinix |
| **Los Angeles** | CoreSite | CoreSite, Equinix, Megaport, Neutrona Networks, NTT, Zayo |
| **Marseille** |Interxion | Interxion |
| **Melbourne** | NextDC | AARNet, Equinix, Megaport, NEXTDC, Optus, Telstra Corporation |
| **Miami** | Equinix | C3ntro+, Equinix, Megaport, Neutrona Networks |
| **Montreal** | Cologix | Bell Canada, Cologix, Telus, Zayo |
| **Mumbai** | Tata Communications | Global CloudXchange (GCX), Sify, Tata Communications, Vodafone Idea |
| **Mumbai2** | Airtel | Airtel, Sify, Vodafone Idea |
| **New York** | Equinix | CenturyLink Cloud Connect, Coresite, Equinix, InterCloud, Megaport, Zayo |
| **Newport(Wales)** | Next Generation Data | British Telecom, Level 3 Communications, Next Generation Data |
| **Osaka** | Equinix | Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT SmartConnect, Softbank |
| **Paris** | Interxion | Colt, Equinix, Intercloud, Interxion, Orange, Zayo |
| **Perth** | NextDC | Megaport, NextDC |
| **Quebec City** | 4Degrees | Bell Canada, Megaport |
| **San Antonio** | CyrusOne | CenturyLink Cloud Connect, Megaport |
| **Sao Paulo** | Equinix | Aryaka Networks, Ascenty Data Centers, British Telecom, Equinix, Level 3 Communications, Neutrona Networks, Orange, Tata Communications, Telefonica, UOLDIVEO |
| **Seattle** | Equinix | Aryaka Networks, Equinix, Level 3 Communications, Megaport, Zayo |
| **Seoul** | KINX | KINX, LG CNS, Sejong Telecom |
| **Silicon Valley** | Equinix | Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink Cloud Connect, Comcast, Coresite, Equinix, InterCloud, IX Reach, PacketFabric, Level 3 Communications, Megaport, Orange, Sprint, Tata Communications, Verizon, Zayo |
| **Singapore** | Equinix | Aryaka Networks, AT&T NetBond, British Telecom, Epsilon Global Communications, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, SingTel, Tata Communications, Telstra Corporation, Verizon, Vodafone |
| **Singapore2** | Global Switch | Colt, Epsilon Global Communications, Megaport, SingTel |
| **Sydney** | Equinix | AARNet, AT&T NetBond, British Telecom, Equinix, Kordia, Megaport, NEXTDC, NTT Communications, Optus, Orange, Telstra Corporation, Verizon |
| **Taipei** | Chief Telecom | Chief Telecom |
| **Tokyo** | Equinix | Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink Cloud Connect, Colt, Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT EAST, Orange, Softbank, Verizon |
| **Toronto** | Cologix | AT&T NetBond, Bell Canada, CenturyLink Cloud Connect, Cologix, Equinix, Megaport, Telus, Zayo |
| **Washington DC** | Equinix | Aryaka Networks, AT&T NetBond, British Telecom, Cologix, Comcast, Coresite, Equinix, Internet2, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, PacketFabric, Sprint, Tata Communications, Telia Carrier, Verizon, Zayo |
| **Washington DC2** | Coresite | Coresite | 
| **Zurich** | Interxion | Interxion |

 **+** denotes coming soon

### National cloud environments

### US Government cloud
| **Location** | **Service Providers** |
| --- | --- |
| **Chicago** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |
| **Dallas** |Equinix, Megaport, Verizon |
| **New York** |Equinix, CenturyLink Cloud Connect, Verizon |
| **Phoenix** | AT&T NetBond, CenturyLink Cloud Connect |
| **San Antonio** | Megaport |
| **Silicon Valley** | Equinix, Level 3 Communications, Verizon |
| **Seattle** | Equinix, Megaport |
| **Washington DC** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |

### China
| **Location** | **Service Providers** |
| --- | --- |
| **Beijing** |China Telecom |
| **Beijing2** | GDS |
| **Shanghai** |China Telecom |
| **Shanghai2** | GDS |

To learn more, see [ExpressRoute in China](http://www.windowsazure.cn/home/features/expressroute/)

### Germany
| **Location** | **Service Providers** |
| --- | --- |
| **Berlin** |e-shelter, Megaport+, T-Systems |
| **Frankfurt** |Colt, Equinix, Interxion |

## <a name="c1partners"></a>Connectivity Through Exchange Providers
If your connectivity provider is not listed in previous sections, you can still create a connection.

* Check with your connectivity provider to see if they are connected to any of the exchanges in the table above. You can check the following links to gather more information about services offered by exchange providers. Several connectivity providers are already connected to Ethernet exchanges.
  * [Cologix](https://www.cologix.com/)
  * [CoreSite](https://www.coresite.com/)
  * [Equinix Cloud Exchange](https://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [InterXion](https://www.interxion.com/)
  * [NextDC](https://www.nextdc.com/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [PacketFabric](https://www.packetfabric.com/packetcor/microsoft-azure/)
  
* Have your connectivity provider extend your network to the peering location of choice.
  * Ensure that your connectivity provider extends your connectivity in a highly available manner so that there are no single points of failure.
* Order an ExpressRoute circuit with the exchange as your connectivity provider to connect to Microsoft.
  * Follow steps in [Create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) to set up connectivity.

## <a name="c1partners"></a>Connectivity Through Additional Service Providers
| **Location** | **Exchange** | **Connectivity Providers** |
| --- | --- | --- |
| **Amsterdam** | Equinix, Telecity | BICS, CloudXpress, Eurofiber, Fastweb S.p.A, Gulf Bridge International, MainOne, Nianet, Post, Proximus, TDC Erhverv, Telecom Italia Sparkle, Telia |
| **Cape Town** | Teraco | MTN |
| **Chicago** | Equinix | Lightower, Windstream |
| **Dallas** | Equinix, Megaport | Axtel, C3ntro Telecom, Cox Business, Data Foundry, Transtelco |
| **Frankfurt** | Telecity | BICS, Cinia, Nianet, QSC AG |
| **Hamburg** | Equinix | Cinia |
| **Hong Kong** | Equinix | Chief, Macroview Telecom |
| **Johannesburg** | Teraco | MTN |
| **London** | BICS, Equinix, euNetworks, Telecity | Bezeq International Ltd., CoreAzure, Epsilon Telecommunications Limited, Exponential E, HSO, NexGen Networks, Proximus, Tamares Telecom, Zain |
| **Los Angeles** | Equinix |Transtelco |
| **Madrid** | Level3 | Zertia |
| **Montreal** | Cologix, Equinix | Airgate Technologies, Inc. Cogeco Peer 1, Rogers, Zirro |
| **New York** |Equinix, Megaport | Altice Business, Lightower, Webair |
| **Paris** | Equinix | Proximus |
| **Quebec City** | Megaport | Fibrenoire |
| **Sao Paula** | Equinix | Venha Pra Nuvem |
| **Seattle** |Equinix | Alaska Communications |
| **Silicon Valley** |Equinix | Cox Business, Windstream |
| **Singapore** |Equinix |1CLOUDSTAR, BICS, Epsilon Telecommunications Limited, LGA Telecom, United Information Highway (UIH) |
| **Slough** | Equinix | HSO|
| **Sydney** | Megaport | Macquarie Telecom Group|
| **Tokyo** | Equinix | ARTERIA Networks Corporation, BroadBand Tower, Inc. |
| **Toronto** | Equinix | Airgate Technologies, Inc. Cogeco Peer 1, IVedha Inc, Rogers, Thinktel, Zirro|
| **Washington DC** |Equinix | Altice Business, BICS, Cox Business, Gtt Communications Inc, Epsilon Telecommunications Limited, Lightower, Masergy, Windstream |

## ExpressRoute system integrators
Enabling private connectivity to fit your needs can be challenging, based on the scale of your network. You can work with any of the system integrators listed in the following table to assist you with onboarding to ExpressRoute.

| **Continent** | **System integrators** |
| --- | --- |
| **Asia** |Avanade Inc., OneAs1a |
| **Australia** | Ensyst, IT Consultancy, MOQdigital, Vigilant.IT |
| **Europe** |Avanade Inc., Altogee, Bright Skies GmbH, Inframon, MSG Services, New Signature, Nelite, Orange Networks, sol-tec |
| **North America** |Avanade Inc., Equinix Professional Services, FlexManage, Lightstream, Perficient, Presidio |
| **South America** |Avanade Inc., Venha Pra Nuvem |
## Next steps
* For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).
* Ensure that all prerequisites are met. See [ExpressRoute prerequisites](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Location map"
