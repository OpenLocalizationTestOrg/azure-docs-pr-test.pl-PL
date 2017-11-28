---
title: "Różne sposoby, aby utworzyć Maszynę wirtualną systemu Linux za pomocą interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Informacje na temat różnych sposobów tworzenia maszyny wirtualnej z systemem Linux na platformie Azure oraz linki do narzędzi i samouczków dotyczących poszczególnych metod."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="03b0b-103">Różne sposoby tworzenia maszyny wirtualnej z systemem Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="03b0b-104">Platforma Azure umożliwia elastyczne tworzenie maszyn wirtualnych z systemem Linux przy użyciu dowolnych narzędzi i przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="03b0b-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="03b0b-105">Ten artykuł zawiera podsumowanie różnych sposobów oraz przykłady tworzenia maszyn wirtualnych z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="03b0b-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="03b0b-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-106">Azure CLI</span></span>
<span data-ttu-id="03b0b-107">Maszyny wirtualne na platformie Azure można tworzyć przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="03b0b-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="03b0b-108">Interfejs wiersza polecenia platformy Azure w wersji 1.0 — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="03b0b-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="03b0b-109">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](../windows/creation-choices.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="03b0b-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="03b0b-110">Interfejs wiersza polecenia platformy Azure w wersji 1.0 jest dostępny na wielu platformach przy użyciu pakietów menedżera npm, pakietów dostępnych dla określonych dystrybucji lub kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="03b0b-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="03b0b-111">Jeśli chcesz, możesz uzyskać więcej informacji na temat [sposobu instalowania i konfigurowania interfejsu wiersza polecenia platformy Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="03b0b-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="03b0b-112">Poniższe samouczki zawierają przykłady dotyczące używania interfejsu wiersza polecenia platformy Azure w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="03b0b-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="03b0b-113">Zapoznaj się z poszczególnymi artykułami, aby uzyskać więcej informacji na temat przedstawionych poleceń Szybki start interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="03b0b-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="03b0b-114">Tworzenie maszyny wirtualnej systemu Linux z poziomu interfejsu wiersza polecenia platformy Azure w celach programistycznych i testowych</span><span class="sxs-lookup"><span data-stu-id="03b0b-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="03b0b-115">Poniższy przykład tworzy CoreOS maszyny Wirtualnej za pomocą klucza publicznego o nazwie *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="03b0b-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="03b0b-116">Tworzenie zabezpieczonej maszyny wirtualnej systemu Linux przy użyciu szablonu Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="03b0b-117">W poniższym przykładzie maszyna wirtualna jest tworzona przy użyciu szablonu przechowywanego w witrynie GitHub:</span><span class="sxs-lookup"><span data-stu-id="03b0b-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="03b0b-118">Tworzenie kompletnego środowiska systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="03b0b-119">Obejmuje tworzenie modułu równoważenia obciążenia i wielu maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="03b0b-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="03b0b-120">Dodawanie dysku do maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="03b0b-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="03b0b-121">W poniższym przykładzie dodano *5* dysku Gb do istniejącej maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="03b0b-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="03b0b-122">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="03b0b-122">Azure portal</span></span>
<span data-ttu-id="03b0b-123">Witryna [Azure Portal](https://portal.azure.com) umożliwia szybkie tworzenie maszyn wirtualnych, ponieważ nie wymaga instalacji żadnych składników w systemie.</span><span class="sxs-lookup"><span data-stu-id="03b0b-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="03b0b-124">Użyj witryny Azure Portal, aby utworzyć maszynę wirtualną:</span><span class="sxs-lookup"><span data-stu-id="03b0b-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="03b0b-125">Tworzenie maszyny wirtualnej z systemem Linux przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="03b0b-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="03b0b-126">Wybór systemu operacyjnego i obrazu</span><span class="sxs-lookup"><span data-stu-id="03b0b-126">Operating system and image choices</span></span>
<span data-ttu-id="03b0b-127">Podczas tworzenia maszyny wirtualnej możesz wybrać obraz w oparciu o system operacyjny, który chcesz uruchomić.</span><span class="sxs-lookup"><span data-stu-id="03b0b-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="03b0b-128">Platforma Azure i jej partnerzy oferują wiele obrazów, z których część zawiera wstępnie zainstalowane aplikacje i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="03b0b-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="03b0b-129">Możesz również przekazać własny obraz (więcej informacji można znaleźć w [poniższej sekcji](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="03b0b-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="03b0b-130">Obrazy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-130">Azure images</span></span>
<span data-ttu-id="03b0b-131">Użyj poleceń `azure vm image` interfejsu wiersza polecenia, aby wyświetlić dostępne obrazy według wydawcy, wersji dystrybucji i kompilacji.</span><span class="sxs-lookup"><span data-stu-id="03b0b-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="03b0b-132">Wyświetl dostępnych wydawców w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03b0b-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="03b0b-133">Wyświetl dostępne produkty (oferty) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03b0b-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="03b0b-134">Wyświetl dostępne jednostki SKU (wersje dystrybucji) dla danej oferty w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03b0b-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="03b0b-135">Wyświetl dostępne obrazy dla danego wydania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03b0b-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="03b0b-136">Polecenia `azure vm quick-create` i `azure vm create` mają aliasy umożliwiające szybki dostęp do najpopularniejszych dystrybucji i ich najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="03b0b-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="03b0b-137">Użycie aliasów jest zwykle łatwiejsze niż określanie wydawcy, oferty, jednostki SKU i wersji za każdym razem podczas tworzenia maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="03b0b-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="03b0b-138">Alias</span><span class="sxs-lookup"><span data-stu-id="03b0b-138">Alias</span></span> | <span data-ttu-id="03b0b-139">Wydawca</span><span class="sxs-lookup"><span data-stu-id="03b0b-139">Publisher</span></span> | <span data-ttu-id="03b0b-140">Oferta</span><span class="sxs-lookup"><span data-stu-id="03b0b-140">Offer</span></span> | <span data-ttu-id="03b0b-141">SKU</span><span class="sxs-lookup"><span data-stu-id="03b0b-141">SKU</span></span> | <span data-ttu-id="03b0b-142">Wersja</span><span class="sxs-lookup"><span data-stu-id="03b0b-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="03b0b-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="03b0b-143">CentOS</span></span> |<span data-ttu-id="03b0b-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="03b0b-144">OpenLogic</span></span> |<span data-ttu-id="03b0b-145">Centos</span><span class="sxs-lookup"><span data-stu-id="03b0b-145">Centos</span></span> |<span data-ttu-id="03b0b-146">7.2</span><span class="sxs-lookup"><span data-stu-id="03b0b-146">7.2</span></span> |<span data-ttu-id="03b0b-147">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-147">latest</span></span> |
| <span data-ttu-id="03b0b-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="03b0b-148">CoreOS</span></span> |<span data-ttu-id="03b0b-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="03b0b-149">CoreOS</span></span> |<span data-ttu-id="03b0b-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="03b0b-150">CoreOS</span></span> |<span data-ttu-id="03b0b-151">Stable</span><span class="sxs-lookup"><span data-stu-id="03b0b-151">Stable</span></span> |<span data-ttu-id="03b0b-152">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-152">latest</span></span> |
| <span data-ttu-id="03b0b-153">Debian</span><span class="sxs-lookup"><span data-stu-id="03b0b-153">Debian</span></span> |<span data-ttu-id="03b0b-154">credativ</span><span class="sxs-lookup"><span data-stu-id="03b0b-154">credativ</span></span> |<span data-ttu-id="03b0b-155">Debian</span><span class="sxs-lookup"><span data-stu-id="03b0b-155">Debian</span></span> |<span data-ttu-id="03b0b-156">8</span><span class="sxs-lookup"><span data-stu-id="03b0b-156">8</span></span> |<span data-ttu-id="03b0b-157">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-157">latest</span></span> |
| <span data-ttu-id="03b0b-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="03b0b-158">openSUSE</span></span> |<span data-ttu-id="03b0b-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="03b0b-159">SUSE</span></span> |<span data-ttu-id="03b0b-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="03b0b-160">openSUSE</span></span> |<span data-ttu-id="03b0b-161">13.2</span><span class="sxs-lookup"><span data-stu-id="03b0b-161">13.2</span></span> |<span data-ttu-id="03b0b-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-162">latest</span></span> |
| <span data-ttu-id="03b0b-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="03b0b-163">RHEL</span></span> |<span data-ttu-id="03b0b-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="03b0b-164">Redhat</span></span> |<span data-ttu-id="03b0b-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="03b0b-165">RHEL</span></span> |<span data-ttu-id="03b0b-166">7.2</span><span class="sxs-lookup"><span data-stu-id="03b0b-166">7.2</span></span> |<span data-ttu-id="03b0b-167">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-167">latest</span></span> |
| <span data-ttu-id="03b0b-168">SLES</span><span class="sxs-lookup"><span data-stu-id="03b0b-168">SLES</span></span> |<span data-ttu-id="03b0b-169">SLES</span><span class="sxs-lookup"><span data-stu-id="03b0b-169">SLES</span></span> |<span data-ttu-id="03b0b-170">SLES</span><span class="sxs-lookup"><span data-stu-id="03b0b-170">SLES</span></span> |<span data-ttu-id="03b0b-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="03b0b-171">12-SP1</span></span> |<span data-ttu-id="03b0b-172">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-172">latest</span></span> |
| <span data-ttu-id="03b0b-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="03b0b-173">UbuntuLTS</span></span> |<span data-ttu-id="03b0b-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="03b0b-174">Canonical</span></span> |<span data-ttu-id="03b0b-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="03b0b-175">UbuntuServer</span></span> |<span data-ttu-id="03b0b-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="03b0b-176">14.04.4-LTS</span></span> |<span data-ttu-id="03b0b-177">najnowsza</span><span class="sxs-lookup"><span data-stu-id="03b0b-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="03b0b-178">Użycie własnego obrazu</span><span class="sxs-lookup"><span data-stu-id="03b0b-178">Use your own image</span></span>
<span data-ttu-id="03b0b-179">Jeśli potrzebujesz specjalnego dostosowania, możesz użyć obrazu opartego na istniejącej maszynie wirtualnej platformy Azure poprzez *przechwycenie* tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="03b0b-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="03b0b-180">Możesz również przekazać obraz utworzony lokalnie.</span><span class="sxs-lookup"><span data-stu-id="03b0b-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="03b0b-181">Aby uzyskać więcej informacji o obsługiwanych dystrybucjach i sposobach wykorzystania własnych obrazów, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="03b0b-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="03b0b-182">Dystrybucje zatwierdzone na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="03b0b-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="03b0b-183">Informacje dotyczące niezatwierdzonych dystrybucji</span><span class="sxs-lookup"><span data-stu-id="03b0b-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="03b0b-184">Przekazywanie i tworzenie maszyny wirtualnej z systemem Linux z niestandardowego obrazu dysku</span><span class="sxs-lookup"><span data-stu-id="03b0b-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="03b0b-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md) (Jak przechwycić maszynę wirtualną systemu Linux jako szablon usługi Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="03b0b-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="03b0b-186">Przykładowe polecenia Szybki start umożliwiające przechwycenie istniejącej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="03b0b-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="03b0b-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03b0b-187">Next steps</span></span>
* <span data-ttu-id="03b0b-188">Utwórz maszynę wirtualną z systemem Linux przy użyciu [portalu](quick-create-portal.md), interfejsu [wiersza polecenia platformy Azure](quick-create-cli.md) lub [szablonu](../windows/cli-deploy-templates.md) usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="03b0b-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="03b0b-189">Po utworzeniu maszyny wirtualnej z systemem Linux [dodaj dysk danych](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="03b0b-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="03b0b-190">Szybkie kroki umożliwiające [zresetowanie hasła lub kluczy SSH i zarządzanie użytkownikami](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="03b0b-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

