---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz hosta Docker | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie hostów Docker"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="306ac-103">Utwórz maszynę Wirtualną z Docker</span><span class="sxs-lookup"><span data-stu-id="306ac-103">Create a VM with Docker</span></span>

<span data-ttu-id="306ac-104">Ten skrypt tworzy maszynę wirtualną z włączoną Docker i rozpoczyna się w kontenerze Docker działającym NGINX.</span><span class="sxs-lookup"><span data-stu-id="306ac-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="306ac-105">Po uruchomieniu skryptu hello, mają dostęp do serwera sieci web NGINX hello przez hello FQDN hello maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="306ac-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="306ac-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="306ac-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="306ac-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="306ac-107">Clean up deployment</span></span> 

<span data-ttu-id="306ac-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="306ac-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="306ac-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="306ac-109">Script explanation</span></span>

<span data-ttu-id="306ac-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="306ac-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="306ac-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="306ac-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="306ac-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="306ac-112">Command</span></span> | <span data-ttu-id="306ac-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="306ac-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="306ac-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="306ac-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="306ac-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="306ac-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="306ac-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="306ac-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="306ac-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="306ac-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="306ac-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="306ac-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="306ac-119">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="306ac-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="306ac-120">Tworzy sieci zabezpieczeń grupy reguł tooallow ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="306ac-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="306ac-121">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="306ac-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="306ac-122">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="306ac-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="306ac-123">Dodaje i uruchamia tooa rozszerzenia maszyny wirtualnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="306ac-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="306ac-124">W tym przykładzie hello rozszerzenia maszyny Wirtualnej platformy Docker jest używane tooconfigure hostów Docker.</span><span class="sxs-lookup"><span data-stu-id="306ac-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="306ac-125">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="306ac-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="306ac-126">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="306ac-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="306ac-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="306ac-127">Next steps</span></span>

<span data-ttu-id="306ac-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="306ac-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="306ac-129">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="306ac-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
