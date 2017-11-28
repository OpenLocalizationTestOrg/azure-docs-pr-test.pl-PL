---
title: "Utworzyć Maszynę wirtualną systemu Linux na platformie Azure na podstawie szablonu | Dokumentacja firmy Microsoft"
description: "Sposób użycia 2.0 interfejsu wiersza polecenia Azure, aby utworzyć Maszynę wirtualną systemu Linux na podstawie szablonu usługi Resource Manager"
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
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="041d4-103">Tworzenie maszyny wirtualnej systemu Linux przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="041d4-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="041d4-104">W tym artykule przedstawiono szybki sposób wdrożenia maszyny wirtualnej systemu Linux (VM) do szablonów usługi Azure Resource Manager i 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="041d4-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="041d4-105">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="041d4-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="041d4-106">Przegląd szablonów</span><span class="sxs-lookup"><span data-stu-id="041d4-106">Templates overview</span></span>
<span data-ttu-id="041d4-107">Szablony usługi Azure Resource Manager są plikami JSON, definiujące infrastrukturze i konfiguracji rozwiązania Azure.</span><span class="sxs-lookup"><span data-stu-id="041d4-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="041d4-108">Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="041d4-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="041d4-109">Aby dowiedzieć się więcej o formacie szablonu i sposobu tworzenia, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="041d4-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="041d4-110">Aby wyświetlić składnię JSON dla typów zasobów, zobacz [Define resources in Azure Resource Manager templates](/azure/templates/) (Definiowanie zasobów w szablonach usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="041d4-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="041d4-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="041d4-111">Create resource group</span></span>
<span data-ttu-id="041d4-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="041d4-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="041d4-113">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="041d4-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="041d4-114">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupVM* w *eastus* regionu:</span><span class="sxs-lookup"><span data-stu-id="041d4-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="041d4-115">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="041d4-115">Create virtual machine</span></span>
<span data-ttu-id="041d4-116">Poniższy przykład tworzy Maszynę wirtualną z [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="041d4-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="041d4-117">Podaj wartość własny klucz publiczny SSH, takie jak zawartość *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="041d4-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="041d4-118">Jeśli musisz utworzyć parę kluczy SSH, zobacz [sposobu tworzenia i używania parę kluczy SSH dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="041d4-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="041d4-119">W tym przykładzie wybrano szablon przechowywany w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="041d4-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="041d4-120">Można również pobrać lub utworzyć szablon i określ ścieżkę lokalną o takiej samej `--template-file` parametru.</span><span class="sxs-lookup"><span data-stu-id="041d4-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="041d4-121">Aby SSH do maszyny Wirtualnej, należy uzyskać publiczny adres IP z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="041d4-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="041d4-122">Następnie możesz SSH do maszyny Wirtualnej jako normalne:</span><span class="sxs-lookup"><span data-stu-id="041d4-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="041d4-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="041d4-123">Next steps</span></span>
<span data-ttu-id="041d4-124">W tym przykładzie utworzono podstawowej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="041d4-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="041d4-125">Aby uzyskać więcej szablonów Menedżera zasobów, które obejmują struktur aplikacji lub utworzyć bardziej złożonych środowiskach, przejdź [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="041d4-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>