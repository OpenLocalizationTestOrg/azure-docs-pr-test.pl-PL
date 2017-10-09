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
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="fb446-103">Zestawy skalowania maszyn wirtualnych platformy Azure i dyski zarządzane</span><span class="sxs-lookup"><span data-stu-id="fb446-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="fb446-104">[Zestawy skalowania maszyn wirtualnych](/azure/virtual-machine-scale-sets/) platformy Azure obsługują maszyny wirtualne z dyskami zarządzanymi.</span><span class="sxs-lookup"><span data-stu-id="fb446-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="fb446-105">Używanie dysków zarządzanych z zestawami skalowania ma między innymi następujące zalety:</span><span class="sxs-lookup"><span data-stu-id="fb446-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="fb446-106">Nie są już potrzebne toopre — tworzenie i zarządzanie nimi dysków systemu operacyjnego hello toostore kont magazynu dla maszyn wirtualnych zestawu skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="fb446-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="fb446-107">Możesz dołączyć zestaw skali toohello dysków danych zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="fb446-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="fb446-108">W przypadku dysków zarządzanych zestaw skalowania może zawierać do 1000 maszyn wirtualnych opartych na obrazach platformy lub do 100 maszyn wirtualnych opartych na obrazach niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="fb446-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="fb446-109">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="fb446-109">Get started</span></span>

<span data-ttu-id="fb446-110">Prosty sposób tooget pracę z dysków zarządzanych zestawów skalowania jest toodeploy jedną z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb446-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="fb446-111">Więcej informacji znajduje się w [tym artykule](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="fb446-112">Inny prosty sposób tooget uruchomiona jest toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy zestawu skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb446-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="fb446-113">Witaj poniższy przykład pokazuje, jak toocreate Ubuntu zestaw z 10 maszyn wirtualnych, każda z dysku 50 GB i 100 GB danych skalowania:</span><span class="sxs-lookup"><span data-stu-id="fb446-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="fb446-114">Alternatywnie można znaleźć hello [repozytorium GitHub szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) dla folderów zawierających `vmss` toosee wstępnie skompilowany przykłady szablonów, które wdrożyć zestawy skalowania.</span><span class="sxs-lookup"><span data-stu-id="fb446-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="fb446-115">tootell szablony, z których korzystają już zarządzanych dysków, można odwoływać się za[tej listy](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb446-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb446-116">Next steps</span></span>

<span data-ttu-id="fb446-117">Aby uzyskać więcej ogólnych informacji o dyskach zarządzanych, zobacz [ten artykuł](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="fb446-118">toosee tooconvert zestawy skali tooprovision szablonu usługi Resource Manager z zarządzanych dysków, zobacz [w tym artykule](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="fb446-119">Witaj szablony Menedżera zasobów toohello modyfikacje mają zastosowanie również toohello interfejsu API REST usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="fb446-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="fb446-120">Zobacz toolearn więcej informacji o użyciu dysków danych zarządzanych zestawów skali [w tym artykule](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="fb446-121">Praca z zestawami dużą skalę toobegin odwoływać się za[w tym artykule](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="fb446-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


