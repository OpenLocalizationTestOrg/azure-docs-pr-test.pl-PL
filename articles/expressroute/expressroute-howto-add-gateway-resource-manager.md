---
title: "Dodaj bramę sieci wirtualnej do sieci wirtualnej dla usługi ExpressRoute: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono dodawania bramy sieci wirtualnej do już utworzonego sieci wirtualnej Menedżera zasobów dla usługi ExpressRoute."
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
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="13f73-103">Konfigurowanie bramy sieci wirtualnej dla usługi ExpressRoute za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f73-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13f73-104">Resource Manager — witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="13f73-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="13f73-105">Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f73-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="13f73-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f73-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="13f73-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="13f73-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="13f73-108">W tym artykule przedstawiono kroki umożliwiające dodawanie, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13f73-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="13f73-109">Kroki dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu modelu wdrażania usługi Resource Manager, który będzie używany w konfiguracji usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13f73-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="13f73-110">Aby uzyskać więcej informacji na temat bram sieci wirtualnej i ustawień konfiguracji bramy ExpressRoute, zobacz [temat bram sieci wirtualnej dla usługi ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="13f73-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="13f73-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="13f73-111">Before beginning</span></span>
<span data-ttu-id="13f73-112">Sprawdź, czy zostały zainstalowane najnowsze poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13f73-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="13f73-113">Nie zainstalowano najnowszych poleceń cmdlet, należy to zrobić przed rozpoczęciem kroków konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="13f73-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="13f73-114">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13f73-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="13f73-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13f73-115">Next steps</span></span>
<span data-ttu-id="13f73-116">Po utworzeniu bramy sieci wirtualnej sieci wirtualnej można połączyć z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="13f73-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="13f73-117">Zobacz [połączyć sieć wirtualną z obwodem usługi ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="13f73-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

