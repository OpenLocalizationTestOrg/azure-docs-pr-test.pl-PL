---
title: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z monitorowaniem OMS | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z monitorowaniem OMS"
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
ms.openlocfilehash: 31bfcc532a7d1ea418fb9a15ec882963d1913756
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="07196-103">Monitor maszyny Wirtualnej w usłudze Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="07196-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="07196-104">Ten skrypt tworzy maszynę wirtualną platformy Azure, zainstalowanie agenta programu Operations Management Suite (OMS) i rejestruje system z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="07196-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="07196-105">Po uruchomieniu skryptu, maszyny wirtualne będą widoczne w konsoli OMS.</span><span class="sxs-lookup"><span data-stu-id="07196-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="07196-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="07196-106">Sample script</span></span>

<span data-ttu-id="07196-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "szybkie tworzenie maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="07196-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="07196-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07196-108">Clean up deployment</span></span> 

<span data-ttu-id="07196-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="07196-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="07196-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="07196-110">Script explanation</span></span>

<span data-ttu-id="07196-111">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="07196-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="07196-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="07196-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="07196-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="07196-113">Command</span></span> | <span data-ttu-id="07196-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="07196-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07196-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="07196-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="07196-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="07196-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07196-117">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="07196-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="07196-118">Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="07196-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="07196-119">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="07196-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="07196-120">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="07196-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="07196-121">Jest uruchamiana rozszerzenia maszyny Wirtualnej dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="07196-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="07196-122">W takim przypadku rozszerzenie agenta Operations Management Suite jest używane do instalowania agenta pakietu OMS i rejestrowania maszyn wirtualnych w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="07196-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="07196-123">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="07196-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="07196-124">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="07196-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07196-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07196-125">Next steps</span></span>

<span data-ttu-id="07196-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07196-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="07196-127">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07196-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
