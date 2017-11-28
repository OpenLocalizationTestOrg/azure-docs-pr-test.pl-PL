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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="e3e9c-103">Konfigurowanie bramy sieci wirtualnej dla usługi przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="e3e9c-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3e9c-104">Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3e9c-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="e3e9c-105">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3e9c-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="e3e9c-106">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e3e9c-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="e3e9c-107">Ten artykuł przeprowadzi Cię przez tooadd kroki hello, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3e9c-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="e3e9c-108">Witaj czynności dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu hello **klasycznego modelu wdrażania** i który będzie można użyć w konfiguracji usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e3e9c-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="e3e9c-109">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="e3e9c-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="e3e9c-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e3e9c-110">Before beginning</span></span>
<span data-ttu-id="e3e9c-111">Sprawdź, czy zostały zainstalowane polecenia cmdlet programu Azure PowerShell hello wymagane dla tej konfiguracji (1.0.2 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="e3e9c-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="e3e9c-112">Jeśli nie zainstalowano hello poleceń cmdlet, musisz toodo tak przed rozpoczęciem powitalne kroków konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e3e9c-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="e3e9c-113">Aby uzyskać więcej informacji na temat instalowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e3e9c-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e3e9c-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3e9c-114">Next steps</span></span>
<span data-ttu-id="e3e9c-115">Po utworzeniu bramy sieci wirtualnej hello możesz połączyć tooan Twojej sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="e3e9c-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="e3e9c-116">Zobacz [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="e3e9c-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

