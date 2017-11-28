---
title: Jak tagu maszyny wirtualnej systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat znakowanie Azure maszyny wirtualnej systemu Linux utworzone na platformie Azure przy użyciu modelu wdrażania Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="1dcb9-103">Jak tagu maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1dcb9-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="1dcb9-104">W tym artykule opisano różne sposoby tagu maszyny wirtualnej systemu Linux na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="1dcb9-105">Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="1dcb9-106">Azure obecnie obsługuje maksymalnie 15 znaczników dla zasobu i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="1dcb9-107">Tagi mogą dotyczącymi zasobów w czasie tworzenia lub dodać do istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="1dcb9-108">Należy pamiętać, tagi są obsługiwane dla zasobów utworzone za pośrednictwem tylko modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="1dcb9-109">Znakowanie za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1dcb9-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="1dcb9-110">Aby rozpocząć, należy najnowszej [2.0 interfejsu wiersza polecenia platformy Azure (wersja zapoznawcza)](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1dcb9-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1dcb9-111">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1dcb9-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1dcb9-112">Wszystkie właściwości można wyświetlić dla danej maszyny wirtualnej, tym tagów, za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1dcb9-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="1dcb9-113">Aby dodać nowy znacznik maszyny Wirtualnej za pomocą wiersza polecenia platformy Azure, można użyć `azure vm update` polecenia wraz z parametrem tag **— Ustawianie**:</span><span class="sxs-lookup"><span data-stu-id="1dcb9-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="1dcb9-114">Aby usunąć tagów, można użyć **— Usuń** parametru w `azure vm update` polecenia.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="1dcb9-115">Teraz, gdy firma Microsoft zastosowano tagi naszych zasobów Azure CLI i portalu, Spójrzmy na szczegóły użycia, aby zobaczyć tagów w portalu rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="1dcb9-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="1dcb9-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1dcb9-116">Next steps</span></span>
* <span data-ttu-id="1dcb9-117">Aby dowiedzieć się więcej na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [przy użyciu tagów do organizowania zasobów platformy Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="1dcb9-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="1dcb9-118">Aby dowiedzieć się, jak tagów można zarządzać korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="1dcb9-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
