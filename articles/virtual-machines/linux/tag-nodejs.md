---
title: tootag aaaHow maszyny wirtualnej systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat znakowanie Azure maszyny wirtualnej systemu Linux utworzone na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="5cdd6-103">Jak tootag maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5cdd6-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="5cdd6-104">W tym artykule opisano różne sposoby tootag maszyny wirtualnej systemu Linux na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="5cdd6-105">Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="5cdd6-106">Obecnie Azure obsługuje tagi too15 według zasobu i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="5cdd6-107">Tagi mogą być umieszczane w zasobie na powitania godzina utworzenia lub dodać tooan istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="5cdd6-108">Należy pamiętać, tagi są obsługiwane dla zasobów utworzone za pośrednictwem modelu wdrażania usługi Resource Manager hello tylko.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="5cdd6-109">Znakowanie za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5cdd6-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="5cdd6-110">toobegin, [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../../xplat-cli-azure-resource-manager.md) i upewnij się, że jesteś w trybie Menedżera zasobów (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="5cdd6-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="5cdd6-111">Wszystkie właściwości można wyświetlić dla podanej maszyny wirtualnej, w tym hello tagów, za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5cdd6-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="5cdd6-112">tooadd nowy znacznik maszyny Wirtualnej za pośrednictwem hello wiersza polecenia platformy Azure, można użyć hello `azure vm set` polecenia wraz z parametru tag hello **-t**:</span><span class="sxs-lookup"><span data-stu-id="5cdd6-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="5cdd6-113">tooremove wszystkie tagi, można użyć hello **– T** parametru w hello `azure vm set` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="5cdd6-114">Firma Microsoft zastosowano tagi zasobów tooour wiersza polecenia platformy Azure i hello portalu Spójrzmy na powitania użycia szczegóły toosee hello tagów w portalu rozliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="5cdd6-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="5cdd6-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5cdd6-115">Next steps</span></span>
* <span data-ttu-id="5cdd6-116">toolearn więcej informacji na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [tooorganize przy użyciu tagów zasobów platformy Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="5cdd6-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="5cdd6-117">toosee tagi ułatwia zarządzanie korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="5cdd6-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
