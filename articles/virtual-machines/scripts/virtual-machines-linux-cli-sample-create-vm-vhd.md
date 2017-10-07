---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz maszynę Wirtualną z wirtualnego dysku twardego | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną przy użyciu wirtualnego dysku twardego."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="e34e1-103">Utwórz maszynę Wirtualną z wirtualnym dyskiem twardym</span><span class="sxs-lookup"><span data-stu-id="e34e1-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="e34e1-104">W tym przykładzie jest tworzony przy użyciu dysku VHD maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e34e1-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="e34e1-105">Tworzy grupę zasobów, konto magazynu i kontener, a następnie tworzy Maszynę wirtualną przekazując hello wirtualnego dysku twardego toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="e34e1-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="e34e1-106">Zastępuje hello ssh publicznego klucza kluczem publicznym, tak aby było możliwe toohello dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e34e1-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="e34e1-107">Będziesz potrzebować rozruchowy wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="e34e1-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="e34e1-108">Możesz pobrać hello dysku VHD, które zostały użyte z https://azclisamples.blob.core.windows.net/vhds/sample.vhd, lub użyć własnych wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e34e1-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="e34e1-109">Wyszukuje skryptu Hello `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="e34e1-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e34e1-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e34e1-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e34e1-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e34e1-111">Clean up deployment</span></span> 

<span data-ttu-id="e34e1-112">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e34e1-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="e34e1-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e34e1-113">Script explanation</span></span>

<span data-ttu-id="e34e1-114">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="e34e1-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="e34e1-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e34e1-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e34e1-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e34e1-116">Command</span></span> | <span data-ttu-id="e34e1-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e34e1-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e34e1-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="e34e1-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e34e1-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="e34e1-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e34e1-120">Lista kont magazynu az</span><span class="sxs-lookup"><span data-stu-id="e34e1-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="e34e1-121">Listy kont magazynu</span><span class="sxs-lookup"><span data-stu-id="e34e1-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="e34e1-122">Sprawdź — nazwa az konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e34e1-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="e34e1-123">Sprawdza, czy nazwa konta magazynu jest prawidłowa i że jeszcze nie istnieje</span><span class="sxs-lookup"><span data-stu-id="e34e1-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="e34e1-124">Lista kluczy kont magazynu az</span><span class="sxs-lookup"><span data-stu-id="e34e1-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="e34e1-125">Wyświetla listę kluczy w przypadku kont magazynu hello</span><span class="sxs-lookup"><span data-stu-id="e34e1-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="e34e1-126">istnieje az obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="e34e1-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="e34e1-127">Sprawdza, czy istnieje hello obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e34e1-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="e34e1-128">Tworzenie kontenera magazynu az</span><span class="sxs-lookup"><span data-stu-id="e34e1-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="e34e1-129">Tworzy kontener na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="e34e1-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="e34e1-130">Przekazywanie obiektu blob magazynu az</span><span class="sxs-lookup"><span data-stu-id="e34e1-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="e34e1-131">Tworzy obiekt blob w kontenerze hello przy hello przekazywanie wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e34e1-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="e34e1-132">AZ listy maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e34e1-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="e34e1-133">Używane z `--query` Sprawdź, czy nazwa maszyny Wirtualnej hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="e34e1-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="e34e1-134">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="e34e1-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="e34e1-135">Tworzy hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e34e1-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="e34e1-136">AZ wirtualna dostęp zestaw linux użytkownika</span><span class="sxs-lookup"><span data-stu-id="e34e1-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="e34e1-137">Resetuje hello SSH klucza toogive hello bieżącego użytkownika dostępu toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e34e1-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="e34e1-138">AZ vm--adresy ip</span><span class="sxs-lookup"><span data-stu-id="e34e1-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="e34e1-139">Pobiera adres IP hello hello maszynę Wirtualną, która została utworzona.</span><span class="sxs-lookup"><span data-stu-id="e34e1-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e34e1-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e34e1-140">Next steps</span></span>

<span data-ttu-id="e34e1-141">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e34e1-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e34e1-142">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e34e1-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
