---
title: "narzędzia aaaCommunity — przenieść zasoby klasyczne tooAzure Resource Manager | Dokumentacja firmy Microsoft"
description: "Ten artykuł narzędzia hello katalogi świadczonej przez toohelp społeczności hello migracji zasobów IaaS z modelu wdrażania usługi Azure Resource Manager toohello klasycznego."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="64b59-103">Społeczność narzędzi toomigrate zasobów IaaS z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="64b59-104">Ten artykuł katalogi hello narzędzia, które tooassist społeczności hello dostarczono migracji zasobów IaaS z modelu wdrażania usługi Azure Resource Manager toohello klasycznego.</span><span class="sxs-lookup"><span data-stu-id="64b59-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="64b59-105">Oficjalnie tych narzędzi nie są obsługiwane przez Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="64b59-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="64b59-106">W związku z tym są otwarte powierzając jej ich konserwację w serwisie GitHub i mamy przyjemność tooaccept PRs poprawki lub dodatkowych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="64b59-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="64b59-107">tooreport problem, użyj hello przez funkcję GitHub.</span><span class="sxs-lookup"><span data-stu-id="64b59-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="64b59-108">Migrowanie z tych narzędzi spowoduje, że przestój klasyczne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64b59-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="64b59-109">Jeśli szukasz migracji z obsługiwanych platform, odwiedź</span><span class="sxs-lookup"><span data-stu-id="64b59-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="64b59-110">Platformy obsługiwane migracji zasobów IaaS ze stosu usługi Resource Manager tooAzure Classic</span><span class="sxs-lookup"><span data-stu-id="64b59-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="64b59-111">Techniczne szczegółowe informacje na temat platformy obsługiwana migracja z klasycznego tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="64b59-112">Migracja zasobów IaaS z klasycznym tooAzure Resource Manager przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="64b59-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="64b59-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="64b59-113">AsmMetadataParser</span></span>
<span data-ttu-id="64b59-114">Jest to zestaw narzędzi pomocnika utworzona w ramach migracji przedsiębiorstwa z tooAzure zarządzania usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64b59-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="64b59-115">To narzędzie umożliwia tooreplicate infrastruktury do innej subskrypcji, która może służyć do testowania migracji i żelaza ewentualnych problemów przed uruchomieniem hello migracji w ramach subskrypcji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="64b59-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="64b59-116">Dokumentacja narzędzia toohello łącza</span><span class="sxs-lookup"><span data-stu-id="64b59-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="64b59-117">migAz</span><span class="sxs-lookup"><span data-stu-id="64b59-117">migAz</span></span>
<span data-ttu-id="64b59-118">migAz jest dodatkowa opcja toomigrate kompletny zestaw zasobów IaaS Menedżera zasobów tooAzure zasobów klasycznych IaaS.</span><span class="sxs-lookup"><span data-stu-id="64b59-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="64b59-119">Hello migracji może wystąpić w hello sam subskrypcji lub różnych subskrypcji i rodzajów subskrypcji (ex: dostawcy usług Kryptograficznych subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="64b59-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="64b59-120">Dokumentacja narzędzia toohello łącza</span><span class="sxs-lookup"><span data-stu-id="64b59-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="64b59-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64b59-121">Next Steps</span></span>

* [<span data-ttu-id="64b59-122">Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="64b59-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-123">Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-124">Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-125">Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-126">Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64b59-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-127">Przegląd najbardziej typowych błędów migracji</span><span class="sxs-lookup"><span data-stu-id="64b59-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="64b59-128">Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="64b59-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

