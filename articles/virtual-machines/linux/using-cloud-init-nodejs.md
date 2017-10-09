---
title: aaaUsing toocustomize init chmury maszyny Wirtualnej systemu Linux, podczas tworzenia na platformie Azure | Dokumentacja firmy Microsoft
description: Jak toouse toocustomize init chmury a Linux VM podczas tworzenia z hello Azure CLI w wersji 1.0
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
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="78265-103">Użyj toocustomize init chmury maszyny Wirtualnej systemu Linux podczas tworzenia z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="78265-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="78265-104">W tym artykule przedstawiono sposób toomake tooset skryptu init chmury hello hostname zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="78265-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="78265-105">skrypty chmurze init Hello są wywoływane podczas hello tworzenie maszyny Wirtualnej za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78265-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="78265-106">wymaga artykułu Hello:</span><span class="sxs-lookup"><span data-stu-id="78265-106">hello article requires:</span></span>

* <span data-ttu-id="78265-107">konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="78265-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="78265-108">Witaj [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) logowania `azure login`.</span><span class="sxs-lookup"><span data-stu-id="78265-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="78265-109">Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="78265-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="78265-110">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="78265-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="78265-111">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="78265-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="78265-112">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="78265-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="78265-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="78265-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="78265-114">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="78265-114">Quick Commands</span></span>
<span data-ttu-id="78265-115">Utwórz skrypt init.txt chmury, który ustawia hello hostname, wszystkie pakiety aktualizacji i dodaje tooLinux użytkownika sudo.</span><span class="sxs-lookup"><span data-stu-id="78265-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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
<span data-ttu-id="78265-116">Tworzenie maszyn wirtualnych do toolaunch grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="78265-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="78265-117">Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="78265-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="78265-118">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="78265-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="78265-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="78265-119">Introduction</span></span>
<span data-ttu-id="78265-120">Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="78265-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="78265-121">[Init chmury](https://cloudinit.readthedocs.org) jest tooinject standardowy sposób skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux jest uruchamiany dla powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="78265-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="78265-122">Na platformie Azure, istnieją trzy różne sposoby toomake zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.</span><span class="sxs-lookup"><span data-stu-id="78265-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="78265-123">Wstaw skrypty przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="78265-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="78265-124">Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78265-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="78265-125">Szablonu platformy Azure przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="78265-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="78265-126">Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78265-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="78265-127">skrypty tooinject w dowolnym momencie po rozruchu:</span><span class="sxs-lookup"><span data-stu-id="78265-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="78265-128">SSH toorun bezpośrednio poleceń</span><span class="sxs-lookup"><span data-stu-id="78265-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="78265-129">Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively lub szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="78265-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="78265-130">Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.</span><span class="sxs-lookup"><span data-stu-id="78265-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="78265-131">: Rozszerzenia VMAccess wykonuje skrypt główny w hello takie same jak przy użyciu protokołu SSH może.</span><span class="sxs-lookup"><span data-stu-id="78265-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="78265-132">Jednak używanie hello rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="78265-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="78265-133">Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:</span><span class="sxs-lookup"><span data-stu-id="78265-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="78265-134">Alias</span><span class="sxs-lookup"><span data-stu-id="78265-134">Alias</span></span> | <span data-ttu-id="78265-135">Wydawca</span><span class="sxs-lookup"><span data-stu-id="78265-135">Publisher</span></span> | <span data-ttu-id="78265-136">Oferta</span><span class="sxs-lookup"><span data-stu-id="78265-136">Offer</span></span> | <span data-ttu-id="78265-137">SKU</span><span class="sxs-lookup"><span data-stu-id="78265-137">SKU</span></span> | <span data-ttu-id="78265-138">Wersja</span><span class="sxs-lookup"><span data-stu-id="78265-138">Version</span></span> | <span data-ttu-id="78265-139">init chmury</span><span class="sxs-lookup"><span data-stu-id="78265-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="78265-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="78265-140">CentOS</span></span> |<span data-ttu-id="78265-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="78265-141">OpenLogic</span></span> |<span data-ttu-id="78265-142">Centos</span><span class="sxs-lookup"><span data-stu-id="78265-142">Centos</span></span> |<span data-ttu-id="78265-143">7.2</span><span class="sxs-lookup"><span data-stu-id="78265-143">7.2</span></span> |<span data-ttu-id="78265-144">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-144">latest</span></span> |<span data-ttu-id="78265-145">Brak</span><span class="sxs-lookup"><span data-stu-id="78265-145">no</span></span> |
| <span data-ttu-id="78265-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="78265-146">CoreOS</span></span> |<span data-ttu-id="78265-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="78265-147">CoreOS</span></span> |<span data-ttu-id="78265-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="78265-148">CoreOS</span></span> |<span data-ttu-id="78265-149">Stable</span><span class="sxs-lookup"><span data-stu-id="78265-149">Stable</span></span> |<span data-ttu-id="78265-150">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-150">latest</span></span> |<span data-ttu-id="78265-151">Tak</span><span class="sxs-lookup"><span data-stu-id="78265-151">yes</span></span> |
| <span data-ttu-id="78265-152">Debian</span><span class="sxs-lookup"><span data-stu-id="78265-152">Debian</span></span> |<span data-ttu-id="78265-153">credativ</span><span class="sxs-lookup"><span data-stu-id="78265-153">credativ</span></span> |<span data-ttu-id="78265-154">Debian</span><span class="sxs-lookup"><span data-stu-id="78265-154">Debian</span></span> |<span data-ttu-id="78265-155">8</span><span class="sxs-lookup"><span data-stu-id="78265-155">8</span></span> |<span data-ttu-id="78265-156">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-156">latest</span></span> |<span data-ttu-id="78265-157">Brak</span><span class="sxs-lookup"><span data-stu-id="78265-157">no</span></span> |
| <span data-ttu-id="78265-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="78265-158">openSUSE</span></span> |<span data-ttu-id="78265-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="78265-159">SUSE</span></span> |<span data-ttu-id="78265-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="78265-160">openSUSE</span></span> |<span data-ttu-id="78265-161">13.2</span><span class="sxs-lookup"><span data-stu-id="78265-161">13.2</span></span> |<span data-ttu-id="78265-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-162">latest</span></span> |<span data-ttu-id="78265-163">Brak</span><span class="sxs-lookup"><span data-stu-id="78265-163">no</span></span> |
| <span data-ttu-id="78265-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="78265-164">RHEL</span></span> |<span data-ttu-id="78265-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="78265-165">Redhat</span></span> |<span data-ttu-id="78265-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="78265-166">RHEL</span></span> |<span data-ttu-id="78265-167">7.2</span><span class="sxs-lookup"><span data-stu-id="78265-167">7.2</span></span> |<span data-ttu-id="78265-168">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-168">latest</span></span> |<span data-ttu-id="78265-169">Brak</span><span class="sxs-lookup"><span data-stu-id="78265-169">no</span></span> |
| <span data-ttu-id="78265-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="78265-170">UbuntuLTS</span></span> |<span data-ttu-id="78265-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="78265-171">Canonical</span></span> |<span data-ttu-id="78265-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="78265-172">UbuntuServer</span></span> |<span data-ttu-id="78265-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="78265-173">14.04.4-LTS</span></span> |<span data-ttu-id="78265-174">najnowsza</span><span class="sxs-lookup"><span data-stu-id="78265-174">latest</span></span> |<span data-ttu-id="78265-175">Tak</span><span class="sxs-lookup"><span data-stu-id="78265-175">yes</span></span> |

<span data-ttu-id="78265-176">Firma Microsoft jest praca z naszych partnerów tooget chmury inicjowania uwzględnione pracy w obrazach hello udostępniają one tooAzure.</span><span class="sxs-lookup"><span data-stu-id="78265-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="78265-177">Dodawanie utworzenie init chmury skryptu toohello maszyny Wirtualnej z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="78265-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="78265-178">toolaunch skryptu chmury init, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury hello przy użyciu interfejsu wiersza polecenia Azure hello `--custom-data` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="78265-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="78265-179">Tworzenie maszyn wirtualnych do toolaunch grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="78265-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="78265-180">Utwórz Maszynę wirtualną systemu Linux przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="78265-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="78265-181">Tworzenie chmury init skryptu tooset hello nazwa hosta maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="78265-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="78265-182">Jedną z najważniejszych ustawień żadnej maszyny Wirtualnej systemu Linux i hello najprostszym byłoby hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="78265-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="78265-183">Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="78265-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="78265-184">Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="78265-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="78265-185">Podczas hello wstępnego uruchamiania hello maszyny Wirtualnej, ten skrypt init chmury ustawia hello hostname zbyt`myservername`.</span><span class="sxs-lookup"><span data-stu-id="78265-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

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

<span data-ttu-id="78265-186">Logowania i sprawdź nazwę hosta hello hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="78265-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="78265-187">Tworzenie chmury init tooupdate skryptu systemu Linux</span><span class="sxs-lookup"><span data-stu-id="78265-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="78265-188">Dla bezpieczeństwa ma tooupdate Twojej maszyny Wirtualnej systemu Ubuntu przy pierwszym hello.</span><span class="sxs-lookup"><span data-stu-id="78265-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="78265-189">Przy użyciu chmury init możemy, z hello Wykonaj skrypt, w zależności od hello dystrybucja systemu Linux, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="78265-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="78265-190">Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` dla hello Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="78265-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="78265-191">Po uruchomieniu systemu Linux, wszystkich pakietów hello zainstalowane są aktualizowane za pośrednictwem `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="78265-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="78265-192">Logowania i sprawdź wszystkie pakiety zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="78265-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="78265-193">Tworzenie tooadd skryptu init chmury tooLinux użytkownika</span><span class="sxs-lookup"><span data-stu-id="78265-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="78265-194">Jeden z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest tooadd użytkownika dla siebie lub przy użyciu tooavoid `root`.</span><span class="sxs-lookup"><span data-stu-id="78265-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="78265-195">SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane toohello `~/.ssh/authorized_keys` plików za pomocą tego skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="78265-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="78265-196">Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="78265-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="78265-197">Po uruchomieniu systemu Linux, wszyscy użytkownicy hello wymienione są utworzone i dodać toohello sudo grupy.</span><span class="sxs-lookup"><span data-stu-id="78265-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

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

<span data-ttu-id="78265-198">Logowania i weryfikacji hello nowo utworzonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="78265-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="78265-199">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="78265-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="78265-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78265-200">Next Steps</span></span>
<span data-ttu-id="78265-201">Init chmurze staje się jeden toomodify standardowy sposób przy rozruchu maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="78265-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="78265-202">Platforma Azure ma rozszerzenia maszyny Wirtualnej, które pozwalają toomodify Twojego LinuxVM przy rozruchu lub jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="78265-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="78265-203">Na przykład można użyć hello Azure VMAccessExtension tooreset SSH lub informacje o użytkowniku hello maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="78265-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="78265-204">Z inicjowaniem chmury będzie potrzebny hasła hello tooreset ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="78265-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="78265-205">Temat funkcji i rozszerzeń maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="78265-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="78265-206">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="78265-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

