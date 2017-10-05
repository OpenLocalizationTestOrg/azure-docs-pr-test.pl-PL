---
title: "Dostosowywanie maszyny Wirtualnej systemu Linux podczas tworzenia na platformie Azure za pomocą init chmurze | Dokumentacja firmy Microsoft"
description: "Jak użyć init chmury w celu dostosowania Maszynę wirtualną systemu Linux podczas tworzenia z interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="bf749-103">Użyć init chmury w celu dostosowania Maszynę wirtualną systemu Linux podczas tworzenia z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="bf749-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="bf749-104">W tym artykule przedstawiono sposób wprowadzania skryptu init chmury, ustawiania nazwy hosta, zainstalowano aktualizację pakietów i zarządzanie kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bf749-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="bf749-105">Skrypty chmurze init wywoływane podczas tworzenia maszyny Wirtualnej z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf749-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="bf749-106">Wykonanie czynności opisanych w tym artykule wymaga:</span><span class="sxs-lookup"><span data-stu-id="bf749-106">The article requires:</span></span>

* <span data-ttu-id="bf749-107">konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="bf749-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="bf749-108">dostępu do [interfejsu wiersza polecenia platformy Azure](../../cli-install-nodejs.md) (po zalogowaniu przy użyciu `azure login`).</span><span class="sxs-lookup"><span data-stu-id="bf749-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="bf749-109">Interfejs wiersza polecenia platformy Azure *musi działać w* trybie usługi Azure Resource Manager`azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="bf749-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bf749-110">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="bf749-110">CLI versions to complete the task</span></span>
<span data-ttu-id="bf749-111">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="bf749-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="bf749-112">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="bf749-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bf749-113">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="bf749-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="bf749-114">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="bf749-114">Quick Commands</span></span>
<span data-ttu-id="bf749-115">Utwórz skrypt init.txt chmury, który ustawia nazwę hosta, wszystkie pakiety aktualizacji i dodaje użytkownika sudo do systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bf749-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
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
<span data-ttu-id="bf749-116">Utwórz grupę zasobów do maszyn wirtualnych do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="bf749-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="bf749-117">Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="bf749-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="bf749-118">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="bf749-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="bf749-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="bf749-119">Introduction</span></span>
<span data-ttu-id="bf749-120">Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="bf749-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="bf749-121">[Init chmury](https://cloudinit.readthedocs.org) jest standardowym sposobem wstrzyknąć skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux, jak jest uruchamiany dla po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="bf749-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="bf749-122">Na platformie Azure, aby wprowadzić zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on są trzy różne sposoby wdrażania lub rozruchu.</span><span class="sxs-lookup"><span data-stu-id="bf749-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="bf749-123">Wstaw skrypty przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="bf749-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="bf749-124">Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf749-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="bf749-125">Szablonu platformy Azure przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="bf749-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="bf749-126">Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf749-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bf749-127">Do dodania skryptów w dowolnym momencie po rozruchu:</span><span class="sxs-lookup"><span data-stu-id="bf749-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="bf749-128">SSH do uruchamiania poleceń, bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="bf749-128">SSH to run commands directly</span></span>
* <span data-ttu-id="bf749-129">Wstaw skrypty przy użyciu platformy Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively lub szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bf749-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="bf749-130">Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.</span><span class="sxs-lookup"><span data-stu-id="bf749-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="bf749-131">: Rozszerzenia VMAccess wykonuje skryptu, tak jak w głównym w taki sam sposób, przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="bf749-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="bf749-132">Jednak przy użyciu rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="bf749-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="bf749-133">Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:</span><span class="sxs-lookup"><span data-stu-id="bf749-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="bf749-134">Alias</span><span class="sxs-lookup"><span data-stu-id="bf749-134">Alias</span></span> | <span data-ttu-id="bf749-135">Wydawca</span><span class="sxs-lookup"><span data-stu-id="bf749-135">Publisher</span></span> | <span data-ttu-id="bf749-136">Oferta</span><span class="sxs-lookup"><span data-stu-id="bf749-136">Offer</span></span> | <span data-ttu-id="bf749-137">SKU</span><span class="sxs-lookup"><span data-stu-id="bf749-137">SKU</span></span> | <span data-ttu-id="bf749-138">Wersja</span><span class="sxs-lookup"><span data-stu-id="bf749-138">Version</span></span> | <span data-ttu-id="bf749-139">init chmury</span><span class="sxs-lookup"><span data-stu-id="bf749-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="bf749-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="bf749-140">CentOS</span></span> |<span data-ttu-id="bf749-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="bf749-141">OpenLogic</span></span> |<span data-ttu-id="bf749-142">Centos</span><span class="sxs-lookup"><span data-stu-id="bf749-142">Centos</span></span> |<span data-ttu-id="bf749-143">7.2</span><span class="sxs-lookup"><span data-stu-id="bf749-143">7.2</span></span> |<span data-ttu-id="bf749-144">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-144">latest</span></span> |<span data-ttu-id="bf749-145">Brak</span><span class="sxs-lookup"><span data-stu-id="bf749-145">no</span></span> |
| <span data-ttu-id="bf749-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="bf749-146">CoreOS</span></span> |<span data-ttu-id="bf749-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="bf749-147">CoreOS</span></span> |<span data-ttu-id="bf749-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="bf749-148">CoreOS</span></span> |<span data-ttu-id="bf749-149">Stable</span><span class="sxs-lookup"><span data-stu-id="bf749-149">Stable</span></span> |<span data-ttu-id="bf749-150">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-150">latest</span></span> |<span data-ttu-id="bf749-151">Tak</span><span class="sxs-lookup"><span data-stu-id="bf749-151">yes</span></span> |
| <span data-ttu-id="bf749-152">Debian</span><span class="sxs-lookup"><span data-stu-id="bf749-152">Debian</span></span> |<span data-ttu-id="bf749-153">credativ</span><span class="sxs-lookup"><span data-stu-id="bf749-153">credativ</span></span> |<span data-ttu-id="bf749-154">Debian</span><span class="sxs-lookup"><span data-stu-id="bf749-154">Debian</span></span> |<span data-ttu-id="bf749-155">8</span><span class="sxs-lookup"><span data-stu-id="bf749-155">8</span></span> |<span data-ttu-id="bf749-156">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-156">latest</span></span> |<span data-ttu-id="bf749-157">Brak</span><span class="sxs-lookup"><span data-stu-id="bf749-157">no</span></span> |
| <span data-ttu-id="bf749-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="bf749-158">openSUSE</span></span> |<span data-ttu-id="bf749-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="bf749-159">SUSE</span></span> |<span data-ttu-id="bf749-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="bf749-160">openSUSE</span></span> |<span data-ttu-id="bf749-161">13.2</span><span class="sxs-lookup"><span data-stu-id="bf749-161">13.2</span></span> |<span data-ttu-id="bf749-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-162">latest</span></span> |<span data-ttu-id="bf749-163">Brak</span><span class="sxs-lookup"><span data-stu-id="bf749-163">no</span></span> |
| <span data-ttu-id="bf749-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="bf749-164">RHEL</span></span> |<span data-ttu-id="bf749-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="bf749-165">Redhat</span></span> |<span data-ttu-id="bf749-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="bf749-166">RHEL</span></span> |<span data-ttu-id="bf749-167">7.2</span><span class="sxs-lookup"><span data-stu-id="bf749-167">7.2</span></span> |<span data-ttu-id="bf749-168">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-168">latest</span></span> |<span data-ttu-id="bf749-169">Brak</span><span class="sxs-lookup"><span data-stu-id="bf749-169">no</span></span> |
| <span data-ttu-id="bf749-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="bf749-170">UbuntuLTS</span></span> |<span data-ttu-id="bf749-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="bf749-171">Canonical</span></span> |<span data-ttu-id="bf749-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="bf749-172">UbuntuServer</span></span> |<span data-ttu-id="bf749-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="bf749-173">14.04.4-LTS</span></span> |<span data-ttu-id="bf749-174">najnowsza</span><span class="sxs-lookup"><span data-stu-id="bf749-174">latest</span></span> |<span data-ttu-id="bf749-175">Tak</span><span class="sxs-lookup"><span data-stu-id="bf749-175">yes</span></span> |

<span data-ttu-id="bf749-176">Firma Microsoft współpracuje z partnerami uzyskanie init chmury uwzględnione i Praca w obrazach, zapewniające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bf749-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="bf749-177">Dodawanie skryptu init chmury do tworzenia maszyny Wirtualnej z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bf749-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="bf749-178">Aby uruchomić skrypt init chmury, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury przy użyciu interfejsu wiersza polecenia Azure `--custom-data` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="bf749-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="bf749-179">Utwórz grupę zasobów do maszyn wirtualnych do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="bf749-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="bf749-180">Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init ją skonfigurować podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="bf749-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="bf749-181">Tworzenie skrypt init chmurze hostname maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bf749-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="bf749-182">Jedno z ustawień najprostszym i najważniejszych żadnej maszyny Wirtualnej systemu Linux jest nazwą hosta.</span><span class="sxs-lookup"><span data-stu-id="bf749-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="bf749-183">Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="bf749-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="bf749-184">Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="bf749-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="bf749-185">Podczas wstępnego uruchamiania maszyny Wirtualnej, ten skrypt init chmury ustawia nazwę hosta `myservername`.</span><span class="sxs-lookup"><span data-stu-id="bf749-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="bf749-186">Logowania i sprawdź nazwę hosta nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bf749-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="bf749-187">Tworzenie chmury init skryptu aktualizującego systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bf749-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="bf749-188">Dla bezpieczeństwa ma maszyny Wirtualnej systemu Ubuntu aktualizacji po pierwszym uruchomieniu komputera.</span><span class="sxs-lookup"><span data-stu-id="bf749-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="bf749-189">Przy użyciu chmury init robimy można przy użyciu skryptu wykonaj, w zależności od używanych dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bf749-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="bf749-190">Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="bf749-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="bf749-191">Po uruchomieniu systemu Linux, wszystkie zainstalowane pakiety są aktualizowane za pośrednictwem `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="bf749-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="bf749-192">Logowania i sprawdź wszystkie pakiety zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="bf749-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="bf749-193">Tworzenie skryptu init chmury, aby dodać użytkownika do systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bf749-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="bf749-194">Jedno z pierwszym zadań na nowej maszyny Wirtualnej z systemem Linux jest dodać użytkownika dla siebie lub unikać `root`.</span><span class="sxs-lookup"><span data-stu-id="bf749-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="bf749-195">SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane do `~/.ssh/authorized_keys` plików za pomocą tego skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="bf749-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="bf749-196">Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="bf749-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="bf749-197">Po uruchomieniu systemu Linux, wyświetlani użytkownicy są tworzone i dodawane do grupy sudo.</span><span class="sxs-lookup"><span data-stu-id="bf749-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="bf749-198">Logowania i Sprawdź nowo utworzonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf749-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="bf749-199">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bf749-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="bf749-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf749-200">Next Steps</span></span>
<span data-ttu-id="bf749-201">Init chmurze staje się coraz standardowy sposób zmodyfikować maszyny Wirtualnej systemu Linux na rozruchu.</span><span class="sxs-lookup"><span data-stu-id="bf749-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="bf749-202">Platforma Azure ma rozszerzenia maszyny Wirtualnej, które umożliwiają modyfikowanie użytkownika LinuxVM przy rozruchu lub jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="bf749-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="bf749-203">Na przykład można użyć Azure VMAccessExtension można zresetować informacje o użytkowniku lub SSH uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bf749-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="bf749-204">Z inicjowaniem chmury może być konieczne ponowne uruchomienie w celu zresetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="bf749-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="bf749-205">Temat funkcji i rozszerzeń maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bf749-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="bf749-206">Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux platformy Azure przy użyciu rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="bf749-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

