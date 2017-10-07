---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Linux z NGINX | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="9e99c-103">Utwórz maszynę Wirtualną z NGINX</span><span class="sxs-lookup"><span data-stu-id="9e99c-103">Create a VM with NGINX</span></span>

<span data-ttu-id="9e99c-104">Ten skrypt tworzy maszynę wirtualną platformy Azure i używa hello Azure maszyny wirtualnej niestandardowe rozszerzenie skryptu tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="9e99c-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="9e99c-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do pokaz witryny sieci Web na publiczny adres IP hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e99c-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e99c-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9e99c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="9e99c-107">Rozszerzenie niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="9e99c-107">Custom Script Extension</span></span>

<span data-ttu-id="9e99c-108">Witaj niestandardowe rozszerzenie skryptu kopiuje ten skrypt na powitania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e99c-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="9e99c-109">skrypt Hello jest następnie uruchom tooinstall i skonfigurować serwer sieci web NGINX.</span><span class="sxs-lookup"><span data-stu-id="9e99c-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="9e99c-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9e99c-110">Clean up deployment</span></span> 

<span data-ttu-id="9e99c-111">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e99c-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e99c-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9e99c-112">Script explanation</span></span>

<span data-ttu-id="9e99c-113">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9e99c-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9e99c-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="9e99c-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e99c-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9e99c-115">Command</span></span> | <span data-ttu-id="9e99c-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9e99c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e99c-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9e99c-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9e99c-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9e99c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e99c-119">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="9e99c-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9e99c-120">Tworzy hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e99c-120">Creates hello virtual machine.</span></span> <span data-ttu-id="9e99c-121">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9e99c-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9e99c-122">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9e99c-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="9e99c-123">Tworzy sieci zabezpieczeń grupy reguł tooallow ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9e99c-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="9e99c-124">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e99c-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="9e99c-125">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9e99c-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9e99c-126">Dodaje i uruchamia tooa rozszerzenia maszyny wirtualnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e99c-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="9e99c-127">W tym przykładzie hello niestandardowe rozszerzenie skryptu jest używany tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="9e99c-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="9e99c-128">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="9e99c-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9e99c-129">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e99c-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e99c-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e99c-130">Next steps</span></span>

<span data-ttu-id="9e99c-131">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e99c-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9e99c-132">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e99c-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
