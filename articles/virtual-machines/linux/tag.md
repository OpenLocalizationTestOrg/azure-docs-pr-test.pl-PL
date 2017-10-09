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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="42414-103">Jak tootag maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="42414-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="42414-104">W tym artykule opisano różne sposoby tootag maszyny wirtualnej systemu Linux na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="42414-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="42414-105">Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="42414-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="42414-106">Obecnie Azure obsługuje tagi too15 według zasobu i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="42414-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="42414-107">Tagi mogą być umieszczane w zasobie na powitania godzina utworzenia lub dodać tooan istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="42414-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="42414-108">Należy pamiętać, tagi są obsługiwane dla zasobów utworzone za pośrednictwem modelu wdrażania usługi Resource Manager hello tylko.</span><span class="sxs-lookup"><span data-stu-id="42414-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="42414-109">Znakowanie za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="42414-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="42414-110">toobegin, potrzebujesz hello najnowszych [2.0 interfejsu wiersza polecenia platformy Azure (wersja zapoznawcza)](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="42414-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="42414-111">Można również wykonać te kroki hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42414-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="42414-112">Wszystkie właściwości można wyświetlić dla podanej maszyny wirtualnej, w tym hello tagów, za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="42414-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="42414-113">tooadd nowy znacznik maszyny Wirtualnej za pośrednictwem hello wiersza polecenia platformy Azure, można użyć hello `azure vm update` polecenia wraz z parametru tag hello **— Ustawianie**:</span><span class="sxs-lookup"><span data-stu-id="42414-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="42414-114">tagi tooremove, można użyć hello **— Usuń** parametru w hello `azure vm update` polecenia.</span><span class="sxs-lookup"><span data-stu-id="42414-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="42414-115">Firma Microsoft zastosowano tagi zasobów tooour wiersza polecenia platformy Azure i hello portalu Spójrzmy na powitania użycia szczegóły toosee hello tagów w portalu rozliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="42414-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="42414-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42414-116">Next steps</span></span>
* <span data-ttu-id="42414-117">toolearn więcej informacji na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [tooorganize przy użyciu tagów zasobów platformy Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="42414-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="42414-118">toosee tagi ułatwia zarządzanie korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="42414-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
