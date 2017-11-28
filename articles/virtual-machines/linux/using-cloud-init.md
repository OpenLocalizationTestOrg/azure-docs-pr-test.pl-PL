---
title: "Init chmury umożliwia dostosowywanie Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
description: "Dostosowywanie maszyny Wirtualnej systemu Linux podczas tworzenia 2.0 interfejsu wiersza polecenia platformy Azure przy użyciu init chmury"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="45bb3-103">Umożliwia dostosowanie Maszynę wirtualną systemu Linux podczas tworzenia init chmury</span><span class="sxs-lookup"><span data-stu-id="45bb3-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="45bb3-104">W tym artykule przedstawiono sposób wprowadzania skryptu init chmury ustawienie Nazwa hosta, zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="45bb3-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="45bb3-105">Skrypty chmurze init są wywoływane po utworzeniu maszyny wirtualnej (VM) z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="45bb3-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="45bb3-106">Na pełniejsze omówienie na instalowanie aplikacji, zapisywanie plików konfiguracji i wstrzyknięcie kluczy z usługi Key Vault, zobacz [w tym samouczku](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="45bb3-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="45bb3-107">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="45bb3-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="45bb3-108">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="45bb3-108">Quick commands</span></span>
<span data-ttu-id="45bb3-109">Utwórz skrypt init.txt chmury, który ustawia nazwę hosta, wszystkie pakiety aktualizacji i dodaje użytkownika sudo do systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="45bb3-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

<span data-ttu-id="45bb3-110">Utwórz grupę zasobów do uruchamiania maszyn wirtualnych do o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="45bb3-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="45bb3-111">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="45bb3-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="45bb3-112">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu z `--custom-data` parametru.</span><span class="sxs-lookup"><span data-stu-id="45bb3-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="45bb3-113">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="45bb3-113">Detailed walkthrough</span></span>
<span data-ttu-id="45bb3-114">Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="45bb3-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="45bb3-115">[Init chmury](https://cloudinit.readthedocs.org) jest standardowym sposobem wstrzyknąć skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux, jak jest uruchamiany dla po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="45bb3-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="45bb3-116">Na platformie Azure, są na kilka różnych sposobów, aby wprowadzić zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="45bb3-117">Wstaw skrypty przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="45bb3-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="45bb3-118">Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="45bb3-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="45bb3-119">Szablonu platformy Azure przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="45bb3-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="45bb3-120">Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="45bb3-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="45bb3-121">Do dodania skryptów w dowolnym momencie po rozruchu:</span><span class="sxs-lookup"><span data-stu-id="45bb3-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="45bb3-122">SSH do uruchamiania poleceń, bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="45bb3-122">SSH to run commands directly</span></span>
* <span data-ttu-id="45bb3-123">Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md), imperatively lub szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="45bb3-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="45bb3-124">Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.</span><span class="sxs-lookup"><span data-stu-id="45bb3-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="45bb3-125">Rozszerzenia VMAccess wykonuje skryptu, tak jak w głównym w taki sam sposób, przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="45bb3-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="45bb3-126">Jednak przy użyciu rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="45bb3-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="45bb3-127">Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:</span><span class="sxs-lookup"><span data-stu-id="45bb3-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="45bb3-128">Alias</span><span class="sxs-lookup"><span data-stu-id="45bb3-128">Alias</span></span> | <span data-ttu-id="45bb3-129">Wydawca</span><span class="sxs-lookup"><span data-stu-id="45bb3-129">Publisher</span></span> | <span data-ttu-id="45bb3-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="45bb3-130">Offer</span></span> | <span data-ttu-id="45bb3-131">SKU</span><span class="sxs-lookup"><span data-stu-id="45bb3-131">SKU</span></span> | <span data-ttu-id="45bb3-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="45bb3-132">Version</span></span> | <span data-ttu-id="45bb3-133">init chmury</span><span class="sxs-lookup"><span data-stu-id="45bb3-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="45bb3-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="45bb3-134">CentOS</span></span> |<span data-ttu-id="45bb3-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="45bb3-135">OpenLogic</span></span> |<span data-ttu-id="45bb3-136">Centos</span><span class="sxs-lookup"><span data-stu-id="45bb3-136">Centos</span></span> |<span data-ttu-id="45bb3-137">7.2</span><span class="sxs-lookup"><span data-stu-id="45bb3-137">7.2</span></span> |<span data-ttu-id="45bb3-138">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-138">latest</span></span> |<span data-ttu-id="45bb3-139">Brak</span><span class="sxs-lookup"><span data-stu-id="45bb3-139">no</span></span> |
| <span data-ttu-id="45bb3-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="45bb3-140">CoreOS</span></span> |<span data-ttu-id="45bb3-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="45bb3-141">CoreOS</span></span> |<span data-ttu-id="45bb3-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="45bb3-142">CoreOS</span></span> |<span data-ttu-id="45bb3-143">Stable</span><span class="sxs-lookup"><span data-stu-id="45bb3-143">Stable</span></span> |<span data-ttu-id="45bb3-144">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-144">latest</span></span> |<span data-ttu-id="45bb3-145">Tak</span><span class="sxs-lookup"><span data-stu-id="45bb3-145">yes</span></span> |
| <span data-ttu-id="45bb3-146">Debian</span><span class="sxs-lookup"><span data-stu-id="45bb3-146">Debian</span></span> |<span data-ttu-id="45bb3-147">credativ</span><span class="sxs-lookup"><span data-stu-id="45bb3-147">credativ</span></span> |<span data-ttu-id="45bb3-148">Debian</span><span class="sxs-lookup"><span data-stu-id="45bb3-148">Debian</span></span> |<span data-ttu-id="45bb3-149">8</span><span class="sxs-lookup"><span data-stu-id="45bb3-149">8</span></span> |<span data-ttu-id="45bb3-150">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-150">latest</span></span> |<span data-ttu-id="45bb3-151">Brak</span><span class="sxs-lookup"><span data-stu-id="45bb3-151">no</span></span> |
| <span data-ttu-id="45bb3-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="45bb3-152">openSUSE</span></span> |<span data-ttu-id="45bb3-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="45bb3-153">SUSE</span></span> |<span data-ttu-id="45bb3-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="45bb3-154">openSUSE</span></span> |<span data-ttu-id="45bb3-155">13.2</span><span class="sxs-lookup"><span data-stu-id="45bb3-155">13.2</span></span> |<span data-ttu-id="45bb3-156">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-156">latest</span></span> |<span data-ttu-id="45bb3-157">Brak</span><span class="sxs-lookup"><span data-stu-id="45bb3-157">no</span></span> |
| <span data-ttu-id="45bb3-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="45bb3-158">RHEL</span></span> |<span data-ttu-id="45bb3-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="45bb3-159">Redhat</span></span> |<span data-ttu-id="45bb3-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="45bb3-160">RHEL</span></span> |<span data-ttu-id="45bb3-161">7.2</span><span class="sxs-lookup"><span data-stu-id="45bb3-161">7.2</span></span> |<span data-ttu-id="45bb3-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-162">latest</span></span> |<span data-ttu-id="45bb3-163">Brak</span><span class="sxs-lookup"><span data-stu-id="45bb3-163">no</span></span> |
| <span data-ttu-id="45bb3-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="45bb3-164">UbuntuLTS</span></span> |<span data-ttu-id="45bb3-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="45bb3-165">Canonical</span></span> |<span data-ttu-id="45bb3-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="45bb3-166">UbuntuServer</span></span> |<span data-ttu-id="45bb3-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="45bb3-167">14.04.4-LTS</span></span> |<span data-ttu-id="45bb3-168">najnowsza</span><span class="sxs-lookup"><span data-stu-id="45bb3-168">latest</span></span> |<span data-ttu-id="45bb3-169">Tak</span><span class="sxs-lookup"><span data-stu-id="45bb3-169">yes</span></span> |

<span data-ttu-id="45bb3-170">Pracujemy nad z naszych partnerów uzyskanie init chmury uwzględnione i Praca w obrazach, zapewniające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="45bb3-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="45bb3-171">Skrypt init chmury do tworzenia maszyny Wirtualnej z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="45bb3-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="45bb3-172">Aby uruchomić skrypt init chmury, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury przy użyciu interfejsu wiersza polecenia Azure `--custom-data` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="45bb3-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="45bb3-173">Utwórz grupę zasobów do uruchamiania maszyn wirtualnych do o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="45bb3-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="45bb3-174">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="45bb3-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="45bb3-175">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="45bb3-176">Utwórz skrypt init chmurze hostname maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="45bb3-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="45bb3-177">Jedno z ustawień najprostszym i najważniejszych żadnej maszyny Wirtualnej systemu Linux jest nazwą hosta.</span><span class="sxs-lookup"><span data-stu-id="45bb3-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="45bb3-178">Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="45bb3-179">Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="45bb3-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="45bb3-180">Podczas wstępnego uruchamiania maszyny Wirtualnej, ten skrypt init chmury ustawia nazwę hosta *myservername*.</span><span class="sxs-lookup"><span data-stu-id="45bb3-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="45bb3-181">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="45bb3-182">Logowania i sprawdź nazwę hosta nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="45bb3-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="45bb3-183">Utwórz skrypt init chmury</span><span class="sxs-lookup"><span data-stu-id="45bb3-183">Create a cloud-init script</span></span>
<span data-ttu-id="45bb3-184">Dla bezpieczeństwa ma maszyny Wirtualnej systemu Ubuntu aktualizacji po pierwszym uruchomieniu komputera.</span><span class="sxs-lookup"><span data-stu-id="45bb3-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="45bb3-185">Przy użyciu chmury init robimy można przy użyciu skryptu wykonaj, w zależności od używanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="45bb3-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="45bb3-186">Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="45bb3-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="45bb3-187">Po uruchomieniu systemu Linux, wszystkie zainstalowane pakiety są aktualizowane za pośrednictwem **stanie get**.</span><span class="sxs-lookup"><span data-stu-id="45bb3-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="45bb3-188">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="45bb3-189">Logowania i sprawdź wszystkie pakiety zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="45bb3-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="45bb3-190">Utwórz skrypt init chmury, aby dodać użytkownika do systemu Linux</span><span class="sxs-lookup"><span data-stu-id="45bb3-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="45bb3-191">Jedno z pierwszym zadań na nowej maszyny Wirtualnej z systemem Linux jest dodać użytkownika dla siebie lub unikać *głównego*.</span><span class="sxs-lookup"><span data-stu-id="45bb3-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="45bb3-192">SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane do *~/.ssh/authorized_keys* plików za pomocą tego skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="45bb3-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="45bb3-193">Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="45bb3-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="45bb3-194">Po uruchomieniu systemu Linux, wyświetlani użytkownicy są tworzone i dodawane do grupy sudo.</span><span class="sxs-lookup"><span data-stu-id="45bb3-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="45bb3-195">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="45bb3-196">Logowania i Sprawdź nowo utworzonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="45bb3-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="45bb3-197">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="45bb3-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="45bb3-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="45bb3-198">Next steps</span></span>
<span data-ttu-id="45bb3-199">Init chmurze staje się coraz standardowy sposób zmodyfikować maszyny Wirtualnej systemu Linux na rozruchu.</span><span class="sxs-lookup"><span data-stu-id="45bb3-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="45bb3-200">Platforma Azure ma rozszerzenia maszyny Wirtualnej, które umożliwiają modyfikowanie użytkownika LinuxVM przy rozruchu lub jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="45bb3-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="45bb3-201">Na przykład można użyć Azure VMAccessExtension można zresetować informacje o użytkowniku lub SSH uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="45bb3-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="45bb3-202">Z inicjowaniem chmury może być konieczne ponowne uruchomienie w celu zresetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="45bb3-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="45bb3-203">Temat funkcji i rozszerzeń maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="45bb3-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="45bb3-204">Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux platformy Azure przy użyciu rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="45bb3-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)