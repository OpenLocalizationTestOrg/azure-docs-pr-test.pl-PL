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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="d70c6-103">Konfigurowanie bramy sieci wirtualnej dla usługi ExpressRoute za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d70c6-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d70c6-104">Resource Manager — witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d70c6-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="d70c6-105">Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="d70c6-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="d70c6-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="d70c6-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="d70c6-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d70c6-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="d70c6-108">W tym artykule przedstawiono tooadd kroki hello, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d70c6-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="d70c6-109">Witaj czynności dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu modelu wdrażania usługi Resource Manager hello, który będzie używany w konfiguracji usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d70c6-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="d70c6-110">Aby uzyskać więcej informacji na temat bram sieci wirtualnej i ustawień konfiguracji bramy ExpressRoute, zobacz [temat bram sieci wirtualnej dla usługi ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="d70c6-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="d70c6-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d70c6-111">Before beginning</span></span>
<span data-ttu-id="d70c6-112">Sprawdź, czy zostały zainstalowane hello najnowsze Azure poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d70c6-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d70c6-113">Jeśli nie zainstalowano hello najnowszych poleceń cmdlet, należy toodo tak przed rozpoczęciem powitalne kroków konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d70c6-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="d70c6-114">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d70c6-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d70c6-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d70c6-115">Next steps</span></span>
<span data-ttu-id="d70c6-116">Po utworzeniu bramy sieci wirtualnej hello możesz połączyć tooan Twojej sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="d70c6-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="d70c6-117">Zobacz [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d70c6-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

