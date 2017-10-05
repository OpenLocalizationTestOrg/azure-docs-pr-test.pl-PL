---
title: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z NGINX | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="89baf-103">Utwórz maszynę Wirtualną z NGINX</span><span class="sxs-lookup"><span data-stu-id="89baf-103">Create a VM with NGINX</span></span>

<span data-ttu-id="89baf-104">Ten skrypt tworzy maszynę wirtualną platformy Azure i stosuje niestandardowe rozszerzenie skryptu maszyny wirtualnej platformy Azure w celu zainstalowania NGINX.</span><span class="sxs-lookup"><span data-stu-id="89baf-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="89baf-105">Po uruchomieniu skryptu, można uzyskać dostępu do pokaz witryny sieci Web na publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89baf-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="89baf-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="89baf-106">Sample script</span></span>

<span data-ttu-id="89baf-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "szybkie tworzenie maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="89baf-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="89baf-108">Rozszerzenie niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="89baf-108">Custom Script Extension</span></span>

<span data-ttu-id="89baf-109">Rozszerzenie skryptu niestandardowego kopiuje tego skryptu na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89baf-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="89baf-110">Następnie uruchomienia skryptu, aby zainstalować i skonfigurować serwer sieci web NGINX.</span><span class="sxs-lookup"><span data-stu-id="89baf-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="89baf-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="89baf-111">Clean up deployment</span></span> 

<span data-ttu-id="89baf-112">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="89baf-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="89baf-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="89baf-113">Script explanation</span></span>

<span data-ttu-id="89baf-114">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="89baf-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="89baf-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="89baf-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="89baf-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="89baf-116">Command</span></span> | <span data-ttu-id="89baf-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="89baf-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="89baf-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="89baf-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="89baf-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="89baf-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="89baf-120">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="89baf-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="89baf-121">Tworzy maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="89baf-121">Creates the virtual machine.</span></span> <span data-ttu-id="89baf-122">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="89baf-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="89baf-123">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89baf-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="89baf-124">Tworzy reguły grupy zabezpieczeń sieci, aby zezwalać na ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="89baf-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="89baf-125">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="89baf-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="89baf-126">zestaw rozszerzeń maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89baf-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="89baf-127">Dodaje i uruchamia rozszerzenie maszyny wirtualnej do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89baf-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="89baf-128">W tym przykładzie niestandardowe rozszerzenie skryptu jest używany do zainstalowania NGINX.</span><span class="sxs-lookup"><span data-stu-id="89baf-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="89baf-129">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="89baf-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="89baf-130">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="89baf-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89baf-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89baf-131">Next steps</span></span>

<span data-ttu-id="89baf-132">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89baf-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="89baf-133">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89baf-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
