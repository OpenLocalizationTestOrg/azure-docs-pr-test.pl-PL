---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — utworzyć Maszynę wirtualną systemu Windows Server | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz serwer systemu Windows maszyny Wirtualnej"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="f0a5a-103">Utwórz maszynę wirtualną z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0a5a-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="f0a5a-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="f0a5a-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do maszyny wirtualnej hello za pomocą połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f0a5a-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f0a5a-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f0a5a-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f0a5a-107">Clean up deployment</span></span> 

<span data-ttu-id="f0a5a-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f0a5a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f0a5a-109">Script explanation</span></span>

<span data-ttu-id="f0a5a-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f0a5a-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f0a5a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f0a5a-112">Command</span></span> | <span data-ttu-id="f0a5a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f0a5a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0a5a-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f0a5a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f0a5a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0a5a-116">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="f0a5a-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="f0a5a-117">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="f0a5a-118">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="f0a5a-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="f0a5a-119">Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="f0a5a-120">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="f0a5a-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="f0a5a-121">Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między hello internet i hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="f0a5a-122">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="f0a5a-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="f0a5a-123">Tworzy karty sieci wirtualnej i dołącza go w sieci wirtualnej toohello, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="f0a5a-124">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="f0a5a-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f0a5a-125">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="f0a5a-126">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="f0a5a-127">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="f0a5a-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f0a5a-128">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0a5a-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0a5a-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0a5a-129">Next steps</span></span>

<span data-ttu-id="f0a5a-130">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0a5a-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f0a5a-131">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0a5a-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
