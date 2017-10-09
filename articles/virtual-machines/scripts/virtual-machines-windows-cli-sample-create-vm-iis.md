---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — zainstalować usługi IIS | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — Zainstaluj usługę IIS"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="de9b9-103">Szybkie tworzenie maszyny wirtualnej z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de9b9-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="de9b9-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016 i używa hello Azure maszyny wirtualnej niestandardowe rozszerzenie skryptu tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="de9b9-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="de9b9-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do hello domyślna witryna sieci Web IIS na publiczny adres IP hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de9b9-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="de9b9-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="de9b9-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="de9b9-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="de9b9-107">Clean up deployment</span></span> 

<span data-ttu-id="de9b9-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="de9b9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="de9b9-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="de9b9-109">Script explanation</span></span>

<span data-ttu-id="de9b9-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="de9b9-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="de9b9-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="de9b9-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="de9b9-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="de9b9-112">Command</span></span> | <span data-ttu-id="de9b9-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="de9b9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="de9b9-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="de9b9-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="de9b9-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="de9b9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="de9b9-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="de9b9-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="de9b9-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="de9b9-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="de9b9-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="de9b9-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="de9b9-119">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="de9b9-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="de9b9-120">Tworzy sieci zabezpieczeń grupy reguł tooallow ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="de9b9-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="de9b9-121">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="de9b9-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="de9b9-122">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de9b9-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="de9b9-123">Dodaje i uruchamia tooa rozszerzenia maszyny wirtualnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de9b9-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="de9b9-124">W tym przykładzie hello niestandardowe rozszerzenie skryptu jest używany tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="de9b9-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="de9b9-125">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="de9b9-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="de9b9-126">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="de9b9-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de9b9-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de9b9-127">Next steps</span></span>

<span data-ttu-id="de9b9-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de9b9-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="de9b9-129">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de9b9-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
