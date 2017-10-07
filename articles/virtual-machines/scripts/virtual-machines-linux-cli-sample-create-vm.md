---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="099e4-103">Utwórz maszynę wirtualną w pełni skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="099e4-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="099e4-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem operacyjnym Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="099e4-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="099e4-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do maszyny wirtualnej hello za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="099e4-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="099e4-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="099e4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="099e4-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="099e4-107">Clean up deployment</span></span> 

<span data-ttu-id="099e4-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="099e4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="099e4-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="099e4-109">Script explanation</span></span>

<span data-ttu-id="099e4-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="099e4-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="099e4-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="099e4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="099e4-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="099e4-112">Command</span></span> | <span data-ttu-id="099e4-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="099e4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="099e4-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="099e4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="099e4-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="099e4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="099e4-116">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="099e4-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="099e4-117">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="099e4-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="099e4-118">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="099e4-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="099e4-119">Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="099e4-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="099e4-120">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="099e4-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="099e4-121">Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między hello internet i hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="099e4-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="099e4-122">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="099e4-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="099e4-123">Tworzy grupy NSG tooallow reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="099e4-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="099e4-124">W tym przykładzie port 22 jest otwarty dla ruchu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="099e4-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="099e4-125">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="099e4-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="099e4-126">Tworzy karty sieci wirtualnej i dołącza go w sieci wirtualnej toohello, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="099e4-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="099e4-127">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="099e4-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="099e4-128">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="099e4-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="099e4-129">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="099e4-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="099e4-130">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="099e4-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="099e4-131">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="099e4-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="099e4-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="099e4-132">Next steps</span></span>

<span data-ttu-id="099e4-133">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="099e4-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="099e4-134">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="099e4-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
