---
title: "aaaUsing zarządzane dysków z Azure zestawy skalowania maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, dlaczego i w jaki sposób toouse zarządzane dysków o zestawy skalowania maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Zestawy skalowania maszyn wirtualnych platformy Azure i dyski zarządzane

[Zestawy skalowania maszyn wirtualnych](/azure/virtual-machine-scale-sets/) platformy Azure obsługują maszyny wirtualne z dyskami zarządzanymi. Używanie dysków zarządzanych z zestawami skalowania ma między innymi następujące zalety:

* Nie są już potrzebne toopre — tworzenie i zarządzanie nimi dysków systemu operacyjnego hello toostore kont magazynu dla maszyn wirtualnych zestawu skalowania hello.

* Możesz dołączyć zestaw skali toohello dysków danych zarządzanych.

* W przypadku dysków zarządzanych zestaw skalowania może zawierać do 1000 maszyn wirtualnych opartych na obrazach platformy lub do 100 maszyn wirtualnych opartych na obrazach niestandardowych.

## <a name="get-started"></a>Rozpoczęcie pracy

Prosty sposób tooget pracę z dysków zarządzanych zestawów skalowania jest toodeploy jedną z hello portalu Azure. Więcej informacji znajduje się w [tym artykule](./virtual-machine-scale-sets-portal-create.md). Inny prosty sposób tooget uruchomiona jest toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy zestawu skalowania maszyny wirtualnej. Witaj poniższy przykład pokazuje, jak toocreate Ubuntu zestaw z 10 maszyn wirtualnych, każda z dysku 50 GB i 100 GB danych skalowania:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Alternatywnie można znaleźć hello [repozytorium GitHub szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) dla folderów zawierających `vmss` toosee wstępnie skompilowany przykłady szablonów, które wdrożyć zestawy skalowania. tootell szablony, z których korzystają już zarządzanych dysków, można odwoływać się za[tej listy](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej ogólnych informacji o dyskach zarządzanych, zobacz [ten artykuł](../virtual-machines/windows/managed-disks-overview.md).

toosee tooconvert zestawy skali tooprovision szablonu usługi Resource Manager z zarządzanych dysków, zobacz [w tym artykule](./virtual-machine-scale-sets-convert-template-to-md.md). Witaj szablony Menedżera zasobów toohello modyfikacje mają zastosowanie również toohello interfejsu API REST usługi Azure.

Zobacz toolearn więcej informacji o użyciu dysków danych zarządzanych zestawów skali [w tym artykule](./virtual-machine-scale-sets-attached-disks.md).

Praca z zestawami dużą skalę toobegin odwoływać się za[w tym artykule](./virtual-machine-scale-sets-placement-groups.md).


