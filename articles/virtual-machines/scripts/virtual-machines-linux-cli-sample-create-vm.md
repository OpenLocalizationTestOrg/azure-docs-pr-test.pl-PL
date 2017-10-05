---
title: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="9b6e3-103">Utwórz maszynę wirtualną w pełni skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="9b6e3-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="9b6e3-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem operacyjnym Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="9b6e3-105">Po uruchomieniu skryptu, można uzyskać dostępu do maszyny wirtualnej za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b6e3-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9b6e3-106">Sample script</span></span>

<span data-ttu-id="9b6e3-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "szybkie tworzenie maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="9b6e3-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9b6e3-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9b6e3-108">Clean up deployment</span></span> 

<span data-ttu-id="9b6e3-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9b6e3-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9b6e3-110">Script explanation</span></span>

<span data-ttu-id="9b6e3-111">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9b6e3-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9b6e3-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9b6e3-113">Command</span></span> | <span data-ttu-id="9b6e3-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9b6e3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b6e3-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9b6e3-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9b6e3-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9b6e3-118">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9b6e3-119">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="9b6e3-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="9b6e3-120">Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="9b6e3-121">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="9b6e3-122">Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między internet i maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="9b6e3-123">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="9b6e3-124">Umożliwia utworzenie reguły NSG zezwalająca na ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="9b6e3-125">W tym przykładzie port 22 jest otwarty dla ruchu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="9b6e3-126">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="9b6e3-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="9b6e3-127">Tworzy karty sieci wirtualnej i dołącza go do sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="9b6e3-128">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9b6e3-129">Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9b6e3-130">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9b6e3-131">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="9b6e3-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9b6e3-132">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b6e3-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b6e3-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b6e3-133">Next steps</span></span>

<span data-ttu-id="9b6e3-134">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b6e3-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9b6e3-135">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b6e3-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
