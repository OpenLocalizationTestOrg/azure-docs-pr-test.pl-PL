---
title: "aaaCreate maszyny Wirtualnej systemu Linux przy użyciu szablonu platformy Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Utwórz Maszynę wirtualną systemu Linux na platformie Azure przy użyciu hello Azure CLI 1.0 i szablonu usługi Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="fe883-103">Jak toocreate a maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe883-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="fe883-104">W tym artykule opisano sposób tooquickly wdrażania maszyny wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 i szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe883-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="fe883-105">wymaga artykułu Hello:</span><span class="sxs-lookup"><span data-stu-id="fe883-105">hello article requires:</span></span>

* <span data-ttu-id="fe883-106">konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="fe883-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="fe883-107">Witaj [Azure CLI 1.0](../../cli-install-nodejs.md) logowania `azure login`.</span><span class="sxs-lookup"><span data-stu-id="fe883-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="fe883-108">Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="fe883-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="fe883-109">Można szybko wdrożyć szablon maszyny Wirtualnej systemu Linux przy użyciu hello [portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe883-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fe883-110">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fe883-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="fe883-111">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="fe883-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="fe883-112">[Azure CLI 1.0](#quick-command-summary) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="fe883-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fe883-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="fe883-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="fe883-114">Szybkie polecenia — podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fe883-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="fe883-115">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="fe883-115">Detailed Walkthrough</span></span>
<span data-ttu-id="fe883-116">Szablony umożliwiają toocreate maszyn wirtualnych na platformie Azure przy użyciu ustawień, które mają toocustomize podczas uruchomienia hello, ustawienia, takie jak nazwy użytkowników i nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="fe883-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="fe883-117">W tym artykule szablon platformy Azure został użyty do utworzenia maszyny wirtualnej z systemem Ubuntu oraz grupy zabezpieczeń sieci z otwartym portem 22 dla usługi SSH.</span><span class="sxs-lookup"><span data-stu-id="fe883-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="fe883-118">Szablony programu Azure Resource Manager są plikami JSON, za pomocą których można wykonywać proste, jednorazowe zadania, takie jak uruchamianie maszyny wirtualnej z systemem Ubuntu przedstawione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="fe883-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="fe883-119">Szablony usługi Azure może być również używane tooconstruct złożonych konfiguracji platformy Azure całego środowisk, takich jak testowych, programistycznych lub produkcyjnych stosu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe883-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="fe883-120">Utwórz hello maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fe883-120">Create hello Linux VM</span></span>
<span data-ttu-id="fe883-121">Witaj po kodu przykładzie pokazano sposób toocall `azure group create` toocreate zasób grupy i wdrażanie zabezpieczone SSH maszyny Wirtualnej systemu Linux hello przy użyciu tego samego czasu [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fe883-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="fe883-122">Należy pamiętać, że w tym przykładzie należy toouse nazw, które są unikatowe tooyour środowiska.</span><span class="sxs-lookup"><span data-stu-id="fe883-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="fe883-123">W tym przykładzie użyto *myResourceGroup* jako hello Nazwa grupy zasobów, a *myVM* jako hello nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe883-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="fe883-124">dane wyjściowe Hello powinna wyglądać powitania po bloku danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="fe883-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="fe883-125">Ten przykład wdrożyć Maszynę wirtualną przy użyciu hello `--template-uri` parametru.</span><span class="sxs-lookup"><span data-stu-id="fe883-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="fe883-126">Można również pobrać lub utworzyć szablon lokalnie i Przekaż szablon hello przy użyciu hello `--template-file` parametr ścieżki pliku szablonu toohello jako argument.</span><span class="sxs-lookup"><span data-stu-id="fe883-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="fe883-127">Witaj wiersza polecenia platformy Azure monituje o parametry hello wymagane przez szablon hello.</span><span class="sxs-lookup"><span data-stu-id="fe883-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe883-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe883-128">Next steps</span></span>
<span data-ttu-id="fe883-129">Wyszukiwanie hello [galerię szablonów](https://azure.microsoft.com/documentation/templates/) toodiscover jakie toodeploy struktur aplikacji dalej.</span><span class="sxs-lookup"><span data-stu-id="fe883-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

