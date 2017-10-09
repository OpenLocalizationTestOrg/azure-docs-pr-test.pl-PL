---
title: "Dodawanie sieci wirtualnej tooa bramy sieci wirtualnej dla usługi ExpressRoute: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł przeprowadzi Cię przez procedurę dodawania tooan bramy sieci wirtualnej, już utworzona sieć wirtualna Menedżera zasobów dla usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Konfigurowanie bramy sieci wirtualnej dla usługi ExpressRoute za pomocą programu PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager — witryna Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager — program PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic — PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

W tym artykule przedstawiono tooadd kroki hello, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej. Witaj czynności dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu modelu wdrażania usługi Resource Manager hello, który będzie używany w konfiguracji usługi ExpressRoute. Aby uzyskać więcej informacji na temat bram sieci wirtualnej i ustawień konfiguracji bramy ExpressRoute, zobacz [temat bram sieci wirtualnej dla usługi ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Przed rozpoczęciem
Sprawdź, czy zostały zainstalowane hello najnowsze Azure poleceń cmdlet programu PowerShell. Jeśli nie zainstalowano hello najnowszych poleceń cmdlet, należy toodo tak przed rozpoczęciem powitalne kroków konfiguracji. Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu bramy sieci wirtualnej hello możesz połączyć tooan Twojej sieci wirtualnej obwodu usługi expressroute. Zobacz [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-arm.md).

