---
title: "aaaDifferent sposobów toocreate Maszynę wirtualną systemu Linux na platformie Azure | Microsoft Azure"
description: "Dowiedz się toocreate różne sposoby hello maszyny wirtualnej systemu Linux na platformie Azure, w tym tootools łącza i samouczki dotyczące każdej z metod."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="f21e2-103">Różne sposoby toocreate Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f21e2-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="f21e2-104">Masz hello elastyczność w Azure toocreate maszyny wirtualnej systemu Linux (VM) przy użyciu narzędzia i przepływów pracy tooyou samodzielnej.</span><span class="sxs-lookup"><span data-stu-id="f21e2-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="f21e2-105">Ten artykuł zawiera podsumowanie tych różnic oraz przykłady tworzenia maszyn wirtualnych systemu Linux, łącznie z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f21e2-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="f21e2-106">Można również wyświetlić w tym hello opcji tworzenia [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="f21e2-107">Witaj [Azure CLI 2.0](/cli/azure/install-az-cli2) jest dostępny na platformach za pomocą pakietu npm, wprowadzone do distro pakietów lub kontener Docker.</span><span class="sxs-lookup"><span data-stu-id="f21e2-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="f21e2-108">Zainstaluj hello kompilacji najbardziej odpowiednie dla danego środowiska, a następnie zaloguj się za pomocą konta Azure tooan [az logowania](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="f21e2-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="f21e2-109">Utwórz Maszynę wirtualną systemu Linux z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f21e2-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="f21e2-110">Za pomocą polecenia [az group create](/cli/azure/group#create) utwórz grupę zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f21e2-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="f21e2-111">Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) o nazwie *myVM* przy użyciu najnowszych hello *UbuntuLTS* obrazu i generowanie kluczy SSH, jeśli nie już istnieją w *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="f21e2-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="f21e2-112">Tworzenie maszyny wirtualnej z systemem Linux przy użyciu szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f21e2-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="f21e2-113">Witaj poniższym przykładzie użyto [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) toocreate Maszynę wirtualną z szablonu przechowywany w serwisie GitHub:</span><span class="sxs-lookup"><span data-stu-id="f21e2-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="f21e2-114">Tworzenie maszyny wirtualnej z systemem Linux i dostosowywanie jej za pomocą skryptów cloud-init</span><span class="sxs-lookup"><span data-stu-id="f21e2-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="f21e2-115">Tworzenie aplikacji wysokiej dostępności ze zrównoważonym obciążeniem na wielu maszynach wirtualnych z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="f21e2-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="f21e2-116">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f21e2-116">Azure portal</span></span>
<span data-ttu-id="f21e2-117">Witaj [portalu Azure](https://portal.azure.com) pozwala tooquickly tworzenie maszyny Wirtualnej, ponieważ nie ma nic tooinstall w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="f21e2-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="f21e2-118">Użyj hello Azure toocreate portalu hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f21e2-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="f21e2-119">Utwórz Maszynę wirtualną systemu Linux przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f21e2-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="f21e2-120">Wybór systemu operacyjnego i obrazu</span><span class="sxs-lookup"><span data-stu-id="f21e2-120">Operating system and image choices</span></span>
<span data-ttu-id="f21e2-121">Podczas tworzenia maszyny Wirtualnej, należy wybrać obraz oparty na powitania ma toorun systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f21e2-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="f21e2-122">Platforma Azure i jej partnerzy oferują wiele obrazów, z których część zawiera wstępnie zainstalowane aplikacje i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="f21e2-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="f21e2-123">Lub przekazać jeden z własnych obrazów (zobacz [hello następujących sekcji](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="f21e2-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="f21e2-124">Obrazy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f21e2-124">Azure images</span></span>
<span data-ttu-id="f21e2-125">Użyj hello [obrazu maszyny wirtualnej az](/cli/azure/vm/image) polecenia toosee, co jest dostępne, wydawca, wersja distro i kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f21e2-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="f21e2-126">Aby wyświetlić dostępnych wydawców:</span><span class="sxs-lookup"><span data-stu-id="f21e2-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="f21e2-127">Aby wyświetlić dostępne produkty (oferty) dla wybranego wydawcy:</span><span class="sxs-lookup"><span data-stu-id="f21e2-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="f21e2-128">Aby wyświetlić dostępne jednostki SKU (wersje dystrybucji) dla danej oferty:</span><span class="sxs-lookup"><span data-stu-id="f21e2-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="f21e2-129">Aby wyświetlić dostępne obrazy dla danego wydania:</span><span class="sxs-lookup"><span data-stu-id="f21e2-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="f21e2-130">Aby uzyskać więcej przykładów z przeglądaniem i wykorzystywaniem dostępnych obrazów, zobacz [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą interfejsu wiersza polecenia Azure hello](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="f21e2-131">Witaj [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia zawiera aliasy tooquickly dostępu można użyć hello częściej dystrybucjach i ich najnowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="f21e2-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="f21e2-132">Używanie aliasów często jest szybsza niż określenie hello wydawcy, oferty, jednostki SKU i wersji w przypadku tworzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f21e2-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="f21e2-133">Alias</span><span class="sxs-lookup"><span data-stu-id="f21e2-133">Alias</span></span> | <span data-ttu-id="f21e2-134">Wydawca</span><span class="sxs-lookup"><span data-stu-id="f21e2-134">Publisher</span></span> | <span data-ttu-id="f21e2-135">Oferta</span><span class="sxs-lookup"><span data-stu-id="f21e2-135">Offer</span></span> | <span data-ttu-id="f21e2-136">SKU</span><span class="sxs-lookup"><span data-stu-id="f21e2-136">SKU</span></span> | <span data-ttu-id="f21e2-137">Wersja</span><span class="sxs-lookup"><span data-stu-id="f21e2-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f21e2-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="f21e2-138">CentOS</span></span> |<span data-ttu-id="f21e2-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f21e2-139">OpenLogic</span></span> |<span data-ttu-id="f21e2-140">Centos</span><span class="sxs-lookup"><span data-stu-id="f21e2-140">Centos</span></span> |<span data-ttu-id="f21e2-141">7.2</span><span class="sxs-lookup"><span data-stu-id="f21e2-141">7.2</span></span> |<span data-ttu-id="f21e2-142">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-142">latest</span></span> |
| <span data-ttu-id="f21e2-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f21e2-143">CoreOS</span></span> |<span data-ttu-id="f21e2-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f21e2-144">CoreOS</span></span> |<span data-ttu-id="f21e2-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f21e2-145">CoreOS</span></span> |<span data-ttu-id="f21e2-146">Stable</span><span class="sxs-lookup"><span data-stu-id="f21e2-146">Stable</span></span> |<span data-ttu-id="f21e2-147">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-147">latest</span></span> |
| <span data-ttu-id="f21e2-148">Debian</span><span class="sxs-lookup"><span data-stu-id="f21e2-148">Debian</span></span> |<span data-ttu-id="f21e2-149">credativ</span><span class="sxs-lookup"><span data-stu-id="f21e2-149">credativ</span></span> |<span data-ttu-id="f21e2-150">Debian</span><span class="sxs-lookup"><span data-stu-id="f21e2-150">Debian</span></span> |<span data-ttu-id="f21e2-151">8</span><span class="sxs-lookup"><span data-stu-id="f21e2-151">8</span></span> |<span data-ttu-id="f21e2-152">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-152">latest</span></span> |
| <span data-ttu-id="f21e2-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f21e2-153">openSUSE</span></span> |<span data-ttu-id="f21e2-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="f21e2-154">SUSE</span></span> |<span data-ttu-id="f21e2-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f21e2-155">openSUSE</span></span> |<span data-ttu-id="f21e2-156">13.2</span><span class="sxs-lookup"><span data-stu-id="f21e2-156">13.2</span></span> |<span data-ttu-id="f21e2-157">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-157">latest</span></span> |
| <span data-ttu-id="f21e2-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="f21e2-158">RHEL</span></span> |<span data-ttu-id="f21e2-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="f21e2-159">Redhat</span></span> |<span data-ttu-id="f21e2-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="f21e2-160">RHEL</span></span> |<span data-ttu-id="f21e2-161">7.2</span><span class="sxs-lookup"><span data-stu-id="f21e2-161">7.2</span></span> |<span data-ttu-id="f21e2-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-162">latest</span></span> |
| <span data-ttu-id="f21e2-163">SLES</span><span class="sxs-lookup"><span data-stu-id="f21e2-163">SLES</span></span> |<span data-ttu-id="f21e2-164">SLES</span><span class="sxs-lookup"><span data-stu-id="f21e2-164">SLES</span></span> |<span data-ttu-id="f21e2-165">SLES</span><span class="sxs-lookup"><span data-stu-id="f21e2-165">SLES</span></span> |<span data-ttu-id="f21e2-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="f21e2-166">12-SP1</span></span> |<span data-ttu-id="f21e2-167">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-167">latest</span></span> |
| <span data-ttu-id="f21e2-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f21e2-168">UbuntuLTS</span></span> |<span data-ttu-id="f21e2-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="f21e2-169">Canonical</span></span> |<span data-ttu-id="f21e2-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f21e2-170">UbuntuServer</span></span> |<span data-ttu-id="f21e2-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="f21e2-171">14.04.4-LTS</span></span> |<span data-ttu-id="f21e2-172">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f21e2-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="f21e2-173">Użycie własnego obrazu</span><span class="sxs-lookup"><span data-stu-id="f21e2-173">Use your own image</span></span>
<span data-ttu-id="f21e2-174">Jeśli potrzebujesz specjalnego dostosowania, możesz użyć obrazu opartego na istniejącej maszynie wirtualnej platformy Azure poprzez przechwycenie tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f21e2-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="f21e2-175">Możesz również przekazać obraz utworzony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f21e2-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="f21e2-176">Aby uzyskać więcej informacji o obsługiwanych dystrybucjach i toouse własnych obrazów, zobacz temat hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="f21e2-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="f21e2-177">Dystrybucje zatwierdzone na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f21e2-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="f21e2-178">Informacje dotyczące niezatwierdzonych dystrybucji</span><span class="sxs-lookup"><span data-stu-id="f21e2-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="f21e2-179">[Jak toocreate obrazu z istniejącej maszyny Wirtualnej Azure](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="f21e2-180">Szybki start przykład polecenia toocreate obrazu z istniejącej maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="f21e2-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="f21e2-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f21e2-181">Next steps</span></span>
* <span data-ttu-id="f21e2-182">Utwórz Maszynę wirtualną systemu Linux z hello [CLI](quick-create-cli.md), z hello [portal](quick-create-portal.md), lub za pomocą [szablonu usługi Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="f21e2-183">Po utworzeniu maszyny wirtualnej z systemem Linux [dowiedz się więcej o dyskach i magazynie platformy Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="f21e2-184">Szybkie kroki zbyt[zresetowanie hasła lub kluczy SSH i zarządzanie użytkownikami](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f21e2-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
