---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — wdrażanie hello stosu światła w zestawie skalowania Machin wirtualna Load-Balanced | Dokumentacja firmy Microsoft"
description: "Użyj skryptu niestandardowego rozszerzenia toodeploy hello stosu światła w przypadku obciążenia = skali maszyny wirtualnej ze zrównoważonym ustawiony na platformie Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="ad085-103">Wdrażanie hello stosu światła w zestawie skalowania maszyn wirtualnych z równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="ad085-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="ad085-104">W tym przykładzie tworzy zestaw skali maszyny wirtualnej i stosuje rozszerzenie, które działa na każdej maszynie wirtualnej w zestawie skalowania hello stosu światła hello toodeploy skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ad085-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ad085-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ad085-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="ad085-106">Połączenie</span><span class="sxs-lookup"><span data-stu-id="ad085-106">Connect</span></span>

<span data-ttu-id="ad085-107">Użyj tego toosee kodu sposobu tooyour tooconnect maszyn wirtualnych i na skalę.</span><span class="sxs-lookup"><span data-stu-id="ad085-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ad085-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ad085-108">Clean up deployment</span></span> 

<span data-ttu-id="ad085-109">Uruchom hello następujące grupy zasobów hello tooremove polecenia, zestaw skali hello i maszyn wirtualnych oraz wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="ad085-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ad085-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ad085-110">Script explanation</span></span>

<span data-ttu-id="ad085-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="ad085-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="ad085-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ad085-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ad085-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ad085-113">Command</span></span> | <span data-ttu-id="ad085-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ad085-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad085-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="ad085-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ad085-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="ad085-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ad085-117">Utwórz az vmss</span><span class="sxs-lookup"><span data-stu-id="ad085-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="ad085-118">Tworzy zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ad085-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="ad085-119">Utwórz regułę równoważeniem obciążenia sieciowego az</span><span class="sxs-lookup"><span data-stu-id="ad085-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="ad085-120">Dodaj punkt końcowy równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="ad085-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="ad085-121">Ustaw rozszerzenie vmss az</span><span class="sxs-lookup"><span data-stu-id="ad085-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="ad085-122">Tworzenie rozszerzenia hello, uruchamiany skryptu niestandardowego hello podczas wdrażania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ad085-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="ad085-123">Aktualizacja vmss az-wystąpienia</span><span class="sxs-lookup"><span data-stu-id="ad085-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="ad085-124">Uruchom skrypt niestandardowych hello na hello wystąpień maszyn wirtualnych, które zostały wdrożone przed zastosowaniem hello rozszerzenia zestawu skali toohello.</span><span class="sxs-lookup"><span data-stu-id="ad085-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="ad085-125">AZ vmss skali</span><span class="sxs-lookup"><span data-stu-id="ad085-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="ad085-126">Skalowanie w górę hello skali, dodając więcej wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad085-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="ad085-127">skryptu niestandardowego Hello jest uruchamiane na te, gdy są one wdrażane.</span><span class="sxs-lookup"><span data-stu-id="ad085-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="ad085-128">Lista ip publicznej sieci az</span><span class="sxs-lookup"><span data-stu-id="ad085-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="ad085-129">Uzyskaj adresy IP hello hello maszyny wirtualne utworzone przez hello próbki.</span><span class="sxs-lookup"><span data-stu-id="ad085-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="ad085-130">Pokaż równoważeniem obciążenia sieciowego az</span><span class="sxs-lookup"><span data-stu-id="ad085-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="ad085-131">Pobierz hello frontonu i zaplecza porty używane przez hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ad085-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad085-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad085-132">Next steps</span></span>

<span data-ttu-id="ad085-133">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad085-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ad085-134">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad085-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
