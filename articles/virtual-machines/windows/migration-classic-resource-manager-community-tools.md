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
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>Społeczność narzędzi toomigrate zasobów IaaS z klasycznym tooAzure Resource Manager
Ten artykuł katalogi hello narzędzia, które tooassist społeczności hello dostarczono migracji zasobów IaaS z modelu wdrażania usługi Azure Resource Manager toohello klasycznego.

> [!NOTE]
> Oficjalnie tych narzędzi nie są obsługiwane przez Microsoft Support. W związku z tym są otwarte powierzając jej ich konserwację w serwisie GitHub i mamy przyjemność tooaccept PRs poprawki lub dodatkowych scenariuszach. tooreport problem, użyj hello przez funkcję GitHub.
> 
> Migrowanie z tych narzędzi spowoduje, że przestój klasyczne maszyny wirtualnej. Jeśli szukasz migracji z obsługiwanych platform, odwiedź 
> 
>   * [Platformy obsługiwane migracji zasobów IaaS ze stosu usługi Resource Manager tooAzure Classic](migration-classic-resource-manager-overview.md)
>   * [Techniczne szczegółowe informacje na temat platformy obsługiwana migracja z klasycznego tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md)
>   * [Migracja zasobów IaaS z klasycznym tooAzure Resource Manager przy użyciu programu Azure PowerShell](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Jest to zestaw narzędzi pomocnika utworzona w ramach migracji przedsiębiorstwa z tooAzure zarządzania usługą Azure Resource Manager. To narzędzie umożliwia tooreplicate infrastruktury do innej subskrypcji, która może służyć do testowania migracji i żelaza ewentualnych problemów przed uruchomieniem hello migracji w ramach subskrypcji w środowisku produkcyjnym.

[Dokumentacja narzędzia toohello łącza](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz jest dodatkowa opcja toomigrate kompletny zestaw zasobów IaaS Menedżera zasobów tooAzure zasobów klasycznych IaaS. Hello migracji może wystąpić w hello sam subskrypcji lub różnych subskrypcji i rodzajów subskrypcji (ex: dostawcy usług Kryptograficznych subskrypcji).

[Dokumentacja narzędzia toohello łącza](https://github.com/Azure/migAz)

## <a name="next-steps"></a>Następne kroki

* [Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

