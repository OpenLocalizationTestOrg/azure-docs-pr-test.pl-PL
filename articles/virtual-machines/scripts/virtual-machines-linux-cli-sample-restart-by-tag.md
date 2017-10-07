---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — ponowne uruchomienie maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — ponowne uruchomienie maszyn wirtualnych, za pomocą tagu i identyfikator"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="03678-103">Ponowne uruchomienie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="03678-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="03678-104">W tym przykładzie pokazano kilka sposobów tooget niektórych maszyn wirtualnych i uruchomić je ponownie.</span><span class="sxs-lookup"><span data-stu-id="03678-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="03678-105">Witaj najpierw powoduje ponowne uruchomienie wszystkich hello maszyn wirtualnych w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="03678-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="03678-106">Witaj drugi hello pobiera oznakowane maszyn wirtualnych przy użyciu `az resouce list` filtry toohello zasoby, które są maszyny wirtualne i ponowne uruchomienie tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="03678-107">W tym przykładzie działanie powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="03678-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="03678-108">Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows hello Azure CLI](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="03678-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="03678-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="03678-109">Sample script</span></span>

<span data-ttu-id="03678-110">przykład Witaj ma trzy skryptów.</span><span class="sxs-lookup"><span data-stu-id="03678-110">hello sample has three scripts.</span></span>
<span data-ttu-id="03678-111">Witaj pierwszy z nich obsługuje hello maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="03678-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="03678-112">Opcja oczekiwania nie hello jest używany tak hello polecenie zwraca bez oczekiwania na każdym toobe maszyny Wirtualnej, udostępnione.</span><span class="sxs-lookup"><span data-stu-id="03678-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="03678-113">Witaj drugi czeka na powitania toobe maszyn wirtualnych w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="03678-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="03678-114">trzeci skryptu Hello ponowne uruchomienie wszystkich maszyn wirtualnych hello, które zostały udostępnione, a następnie tylko hello oznakowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="03678-115">Zainicjuj obsługę hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="03678-115">Provision hello VMs</span></span>

<span data-ttu-id="03678-116">Ten skrypt tworzy grupę zasobów, a następnie tworzy trzy toorestart maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="03678-117">Dwa z nich są oznaczone.</span><span class="sxs-lookup"><span data-stu-id="03678-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="03678-118">Oczekiwanie</span><span class="sxs-lookup"><span data-stu-id="03678-118">Wait</span></span>

<span data-ttu-id="03678-119">Ten skrypt sprawdza na powitania stanu udostępniania co 20 sekund, dopóki wszystkie trzy maszyny wirtualne są udostępnione lub jeden z nich tooprovision zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="03678-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="03678-120">Uruchom ponownie hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="03678-120">Restart hello VMs</span></span>

<span data-ttu-id="03678-121">Ten skrypt powoduje ponowne uruchomienie wszystkich maszyn wirtualnych hello w hello grupy zasobów, a następnie ponowne uruchomienie po prostu hello oznakowane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="03678-122">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="03678-122">Clean up deployment</span></span> 

<span data-ttu-id="03678-123">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grup zasobów hello tooremove używane, maszyn wirtualnych i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="03678-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="03678-124">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="03678-124">Script explanation</span></span>

<span data-ttu-id="03678-125">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="03678-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="03678-126">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="03678-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="03678-127">Polecenie</span><span class="sxs-lookup"><span data-stu-id="03678-127">Command</span></span> | <span data-ttu-id="03678-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="03678-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="03678-129">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="03678-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="03678-130">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="03678-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="03678-131">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="03678-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="03678-132">Tworzy hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="03678-133">AZ listy maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="03678-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="03678-134">Używane z `--query` hello tooensure maszyny wirtualne są udostępniane przed ponownym uruchomieniem je, a następnie tooget hello identyfikatorów toorestart maszyn wirtualnych hello je.</span><span class="sxs-lookup"><span data-stu-id="03678-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="03678-135">Lista zasobów az</span><span class="sxs-lookup"><span data-stu-id="03678-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="03678-136">Używane z `--query` tooget hello identyfikatorów hello maszyn wirtualnych przy użyciu tagu hello.</span><span class="sxs-lookup"><span data-stu-id="03678-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="03678-137">ponowne uruchomienie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="03678-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="03678-138">Uruchamia ponownie hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="03678-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="03678-139">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="03678-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="03678-140">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="03678-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03678-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03678-141">Next steps</span></span>

<span data-ttu-id="03678-142">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03678-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="03678-143">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03678-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
