---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure w ramach szablonu | Dokumentacja firmy Microsoft"
description: "Jak toouse hello Azure CLI 2.0 toocreate Maszynę wirtualną systemu Linux w ramach szablonu usługi Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="7736f-103">Jak toocreate maszyny wirtualnej systemu Linux przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7736f-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="7736f-104">W tym artykule opisano sposób tooquickly wdrażania maszyny wirtualnej systemu Linux (VM) z szablonów usługi Azure Resource Manager i hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7736f-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="7736f-105">Można również wykonać te kroki hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7736f-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="7736f-106">Przegląd szablonów</span><span class="sxs-lookup"><span data-stu-id="7736f-106">Templates overview</span></span>
<span data-ttu-id="7736f-107">Szablony usługi Azure Resource Manager są plikami JSON, definiujące hello infrastrukturze i konfiguracji rozwiązania Azure.</span><span class="sxs-lookup"><span data-stu-id="7736f-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="7736f-108">Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="7736f-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="7736f-109">toolearn więcej informacji na temat formatu hello hello szablonu i konstrukcji, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7736f-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="7736f-110">Witaj tooview składni JSON dla typów zasobów, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="7736f-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="7736f-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="7736f-111">Create resource group</span></span>
<span data-ttu-id="7736f-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="7736f-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="7736f-113">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7736f-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="7736f-114">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupVM* w hello *eastus* regionu:</span><span class="sxs-lookup"><span data-stu-id="7736f-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7736f-115">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7736f-115">Create virtual machine</span></span>
<span data-ttu-id="7736f-116">Witaj poniższy przykład tworzy Maszynę wirtualną z [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="7736f-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="7736f-117">Podaj wartość hello własny klucz publiczny SSH, takie jak zawartość hello *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="7736f-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="7736f-118">Jeśli potrzebujesz toocreate parę kluczy SSH, zobacz [jak toocreate i używanie SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="7736f-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="7736f-119">W tym przykładzie wybrano szablon przechowywany w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7736f-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="7736f-120">Można również pobrać lub utworzyć szablon i określ ścieżkę lokalną hello z hello tego samego `--template-file` parametru.</span><span class="sxs-lookup"><span data-stu-id="7736f-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="7736f-121">tooyour tooSSH maszyny Wirtualnej, Uzyskaj hello publicznego adresu IP z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="7736f-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="7736f-122">Następnie można tooyour SSH maszyny Wirtualnej jako normalne:</span><span class="sxs-lookup"><span data-stu-id="7736f-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="7736f-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7736f-123">Next steps</span></span>
<span data-ttu-id="7736f-124">W tym przykładzie utworzono podstawowej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7736f-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="7736f-125">W przypadku więcej szablonów Menedżera zasobów, które obejmują struktur aplikacji lub utworzyć bardziej złożonych środowiskach, należy wyszukać hello [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="7736f-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
