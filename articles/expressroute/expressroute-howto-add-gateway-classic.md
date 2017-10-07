---
title: "Konfigurowanie bramy sieci wirtualnej dla usługi przy użyciu programu PowerShell: klasycznym: Azure | Dokumentacja firmy Microsoft"
description: "Konfigurowanie bramy sieci wirtualnej dla wdrożenia klasycznego modelu sieci wirtualnej przy użyciu programu PowerShell dla konfiguracji usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Konfigurowanie bramy sieci wirtualnej dla usługi przy użyciu programu PowerShell (klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager — program PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic — PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Ten artykuł przeprowadzi Cię przez tooadd kroki hello, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej. Witaj czynności dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu hello **klasycznego modelu wdrażania** i który będzie można użyć w konfiguracji usługi ExpressRoute. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Przed rozpoczęciem
Sprawdź, czy zostały zainstalowane polecenia cmdlet programu Azure PowerShell hello wymagane dla tej konfiguracji (1.0.2 lub nowszej). Jeśli nie zainstalowano hello poleceń cmdlet, musisz toodo tak przed rozpoczęciem powitalne kroków konfiguracji. Aby uzyskać więcej informacji na temat instalowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu bramy sieci wirtualnej hello możesz połączyć tooan Twojej sieci wirtualnej obwodu usługi expressroute. Zobacz [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-classic.md).

