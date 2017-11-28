---
title: aaaAzure Szybki Start - CLI tworzenia maszyny Wirtualnej | Dokumentacja firmy Microsoft
description: Dowiesz toocreate maszyn wirtualnych z hello wiersza polecenia platformy Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="49205-103">Utwórz maszynę wirtualną systemu Linux z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="49205-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="49205-104">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="49205-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="49205-105">Szczegóły ten przewodnik przy użyciu hello Azure CLI toodeploy maszyny wirtualnej z systemem Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="49205-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="49205-106">Po wdrożeniu serwera hello połączenia SSH jest tworzony, i NGINX, serwer sieci Web jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="49205-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="49205-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="49205-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49205-108">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="49205-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="49205-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="49205-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49205-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49205-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="49205-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="49205-111">Create a resource group</span></span>

<span data-ttu-id="49205-112">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="49205-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="49205-113">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="49205-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="49205-114">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="49205-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="49205-115">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="49205-115">Create virtual machine</span></span>

<span data-ttu-id="49205-116">Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="49205-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="49205-117">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* i tworzy kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="49205-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="49205-118">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="49205-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="49205-119">Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="49205-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="49205-120">Zwróć uwagę na powitania `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="49205-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="49205-121">Ten adres jest używany tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="49205-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="49205-122">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="49205-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="49205-123">Domyślnie dozwolone są tylko połączenia SSH z maszynami wirtualnymi z systemem Linux wdrożonymi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="49205-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="49205-124">Jeśli ta maszyna wirtualna będzie toobe serwer sieci Web, należy tooopen port 80 hello Internet.</span><span class="sxs-lookup"><span data-stu-id="49205-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="49205-125">Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.</span><span class="sxs-lookup"><span data-stu-id="49205-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="49205-126">Łączenie z maszyną wirtualną za pośrednictwem protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="49205-126">SSH into your VM</span></span>

<span data-ttu-id="49205-127">Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="49205-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="49205-128">Upewnij się, że tooreplace  *<publicIpAddress>*  z hello Popraw publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="49205-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="49205-129">W naszym powyższym przykładzie adres IP to *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="49205-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="49205-130">Instalowanie serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="49205-130">Install NGINX</span></span>

<span data-ttu-id="49205-131">Użyj następujących hello bash źródła pakietów tooupdate skryptu i zainstaluj najnowszy pakiet NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="49205-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="49205-132">Wyświetlanie hello NGINX strony powitalnej</span><span class="sxs-lookup"><span data-stu-id="49205-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="49205-133">NGINX zainstalowane i numer portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet — można użyć przeglądarki sieci web na wybór tooview hello domyślne NGINX strony powitalnej.</span><span class="sxs-lookup"><span data-stu-id="49205-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="49205-134">Należy się hello toouse *publicznego adresu IP* opisane powyżej toovisit hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="49205-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="49205-136">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="49205-136">Clean up resources</span></span>

<span data-ttu-id="49205-137">Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="49205-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="49205-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49205-138">Next steps</span></span>

<span data-ttu-id="49205-139">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="49205-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="49205-140">toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="49205-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="49205-141">Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="49205-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
