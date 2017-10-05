---
title: "Techniczne szczegółowe informacje na temat obsługiwanych platform migracji ze środowiska klasycznego do usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule nie techniczne szczegółowe informacje na temat obsługiwanych platform migracji zasobów z klasycznego do usługi Azure Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ee40d32-a5e8-42a2-97d0-3232fd3cbb98
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 4898998fe27c48bab4dee3dbaed5a174e23dc83a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a><span data-ttu-id="515be-103">Rozbudowana technicznie migracja z obsługą platformy od modelu klasycznego do modelu opartego na usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="515be-103">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>
<span data-ttu-id="515be-104">Spójrzmy szczegółowo na temat migracji z systemu Azure klasycznym modelu wdrożenia do modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="515be-104">Let's take a deep-dive on migrating from the Azure classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="515be-105">Przyjrzymy się zasobów na poziomie zasobów i funkcji pomagające zrozumieć, jak platformy Azure wykonuje migrację zasobów między modelami dwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="515be-105">We look at resources at a resource and feature level to help you understand how the Azure platform migrates resources between the two deployment models.</span></span> <span data-ttu-id="515be-106">Aby uzyskać więcej informacji, przeczytaj artykuł powiadomienia usługi: [obsługiwane platformy migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="515be-106">For more information, please read the service announcement article: [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a><span data-ttu-id="515be-107">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="515be-107">Next steps</span></span>

* [<span data-ttu-id="515be-108">Omówienie migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="515be-108">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-109">Planowanie migracji zasobów rozwiązania IaaS z wdrożenia klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="515be-109">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-110">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="515be-110">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-111">Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="515be-111">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-112">Narzędzia społeczności z migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="515be-112">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-113">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="515be-113">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="515be-114">Przejrzyj najczęściej zadawane pytania dotyczące migrowania zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="515be-114">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
