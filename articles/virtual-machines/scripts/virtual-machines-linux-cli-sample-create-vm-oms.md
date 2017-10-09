---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Linux z monitorowaniem OMS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="c79db-103">Monitor maszyny Wirtualnej w usłudze Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="c79db-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="c79db-104">Ten skrypt tworzy maszynę wirtualną platformy Azure, instaluje hello agenta Operations Management Suite (OMS) i rejestruje hello system z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c79db-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="c79db-105">Po uruchomieniu skryptu hello hello maszyny wirtualnej będzie widoczny w konsoli OMS hello.</span><span class="sxs-lookup"><span data-stu-id="c79db-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c79db-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c79db-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c79db-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c79db-107">Clean up deployment</span></span> 

<span data-ttu-id="c79db-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c79db-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c79db-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c79db-109">Script explanation</span></span>

<span data-ttu-id="c79db-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="c79db-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c79db-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="c79db-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c79db-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c79db-112">Command</span></span> | <span data-ttu-id="c79db-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c79db-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c79db-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="c79db-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c79db-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="c79db-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c79db-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="c79db-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c79db-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="c79db-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c79db-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="c79db-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c79db-119">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c79db-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c79db-120">Jest uruchamiana rozszerzenia maszyny Wirtualnej dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79db-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="c79db-121">W takim przypadku hello rozszerzenia agenta Operations Management Suite jest agent pakietu OMS hello tooinstall używane i zarejestrować hello maszyny Wirtualnej w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c79db-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="c79db-122">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="c79db-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c79db-123">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c79db-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c79db-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c79db-124">Next steps</span></span>

<span data-ttu-id="c79db-125">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c79db-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c79db-126">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c79db-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
