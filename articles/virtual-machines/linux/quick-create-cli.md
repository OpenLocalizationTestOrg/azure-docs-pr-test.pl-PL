---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych za pomocą interfejsu wiersza polecenia | Microsoft Docs"
description: "Szybka nauka tworzenia maszyn wirtualnych przy użyciu interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="710ea-103">Tworzenie maszyny wirtualnej z systemem Linux za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="710ea-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="710ea-104">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="710ea-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="710ea-105">W tym przewodniku zawarto szczegółowe instrukcje korzystania z interfejsu wiersza polecenia platformy Azure w celu wdrożenia maszyny wirtualnej z systemem Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="710ea-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="710ea-106">Po wdrożeniu serwera zostanie utworzone połączenie SSH i zostanie zainstalowany serwer sieci Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="710ea-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="710ea-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="710ea-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="710ea-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik szybkiego startu będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="710ea-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="710ea-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="710ea-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="710ea-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="710ea-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="710ea-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="710ea-111">Create a resource group</span></span>

<span data-ttu-id="710ea-112">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="710ea-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="710ea-113">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="710ea-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="710ea-114">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *eastus*.</span><span class="sxs-lookup"><span data-stu-id="710ea-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="710ea-115">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="710ea-115">Create virtual machine</span></span>

<span data-ttu-id="710ea-116">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="710ea-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="710ea-117">Następujący przykład umożliwia utworzenie maszyny wirtualnej o nazwie *myVM* i kluczy SSH, jeśli jeszcze nie istnieją w domyślnej lokalizacji kluczy.</span><span class="sxs-lookup"><span data-stu-id="710ea-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="710ea-118">Aby użyć określonego zestawu kluczy, użyj opcji `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="710ea-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="710ea-119">Po utworzeniu maszyny wirtualnej w interfejsie wiersza polecenia platformy Azure zostanie wyświetlona informacja podobna do następującej.</span><span class="sxs-lookup"><span data-stu-id="710ea-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="710ea-120">Zwróć uwagę na element `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="710ea-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="710ea-121">Ten adres jest używany na potrzeby uzyskiwania dostępu do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="710ea-121">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="710ea-122">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="710ea-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="710ea-123">Domyślnie dozwolone są tylko połączenia SSH z maszynami wirtualnymi z systemem Linux wdrożonymi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="710ea-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="710ea-124">Jeśli ta maszyna wirtualna ma być serwerem sieci Web, port 80 należy otworzyć z Internetu.</span><span class="sxs-lookup"><span data-stu-id="710ea-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="710ea-125">Otwórz odpowiedni port za pomocą polecenia [az vm open-port](/cli/azure/vm#open-port).</span><span class="sxs-lookup"><span data-stu-id="710ea-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="710ea-126">Łączenie z maszyną wirtualną za pośrednictwem protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="710ea-126">SSH into your VM</span></span>

<span data-ttu-id="710ea-127">Użyj następującego polecenia, aby utworzyć sesję SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="710ea-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="710ea-128">Pamiętaj o zamianie elementu *<publicIpAddress>* na prawidłowy publiczny adres IP swojej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="710ea-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="710ea-129">W naszym powyższym przykładzie adres IP to *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="710ea-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="710ea-130">Instalowanie serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="710ea-130">Install NGINX</span></span>

<span data-ttu-id="710ea-131">Użyj poniższego skryptu powłoki systemowej w celu zaktualizowania źródeł pakietów i zainstalowania najnowszego pakietu NGINX.</span><span class="sxs-lookup"><span data-stu-id="710ea-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="710ea-132">Wyświetlanie strony powitalnej serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="710ea-132">View the NGINX welcome page</span></span>

<span data-ttu-id="710ea-133">Po zainstalowaniu serwera NGINX i otwarciu portu 80 na maszynie wirtualnej z Internetu możesz użyć wybranej przeglądarki sieci Web, aby wyświetlić domyślną stronę powitalną przeglądarki serwera NGINX.</span><span class="sxs-lookup"><span data-stu-id="710ea-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="710ea-134">Upewnij się, że w celu odwiedzenia strony domyślnej używasz udokumentowanego powyżej *publicznego adresu IP*.</span><span class="sxs-lookup"><span data-stu-id="710ea-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="710ea-136">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="710ea-136">Clean up resources</span></span>

<span data-ttu-id="710ea-137">Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć za pomocą polecenia [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="710ea-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="710ea-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="710ea-138">Next steps</span></span>

<span data-ttu-id="710ea-139">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="710ea-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="710ea-140">Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="710ea-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="710ea-141">Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="710ea-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
