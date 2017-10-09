---
title: aaaUse toocustomize init chmury maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: Jak toouse toocustomize init chmury a Linux VM podczas tworzenia z hello Azure CLI 2.0
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
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="7e2fa-103">Użyj podczas tworzenia chmury init toocustomize Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7e2fa-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="7e2fa-104">W tym artykule przedstawiono sposób toomake tooset skryptu init chmury hello hostname zainstalowanych pakietów aktualizacji i zarządzanie kontami użytkowników z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="7e2fa-105">skrypty chmurze init Hello są wywoływane po utworzeniu maszyny wirtualnej (VM) z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="7e2fa-106">Na pełniejsze omówienie na instalowanie aplikacji, zapisywanie plików konfiguracji i wstrzyknięcie kluczy z usługi Key Vault, zobacz [w tym samouczku](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="7e2fa-107">Można również wykonać te kroki hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="7e2fa-108">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="7e2fa-108">Quick commands</span></span>
<span data-ttu-id="7e2fa-109">Utwórz skrypt init.txt chmury, który ustawia hello hostname, wszystkie pakiety aktualizacji i dodaje tooLinux użytkownika sudo.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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

<span data-ttu-id="7e2fa-110">Tworzenie maszyn wirtualnych do o toolaunch grupy zasobów [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7e2fa-111">Witaj poniższy przykład tworzy hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7e2fa-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7e2fa-112">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu z hello `--custom-data` parametru.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="7e2fa-113">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="7e2fa-113">Detailed walkthrough</span></span>
<span data-ttu-id="7e2fa-114">Podczas uruchamiania nowej maszyny Wirtualnej systemu Linux, w przypadku uzyskiwania standard maszyny Wirtualnej systemu Linux niczego nie dostosowane lub gotowy do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="7e2fa-115">[Init chmury](https://cloudinit.readthedocs.org) jest tooinject standardowy sposób skryptu lub ustawień konfiguracyjnych do tej maszyny Wirtualnej systemu Linux jest uruchamiany dla powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="7e2fa-116">Na platformie Azure, istnieją na kilka różnych sposobów toomake zmiany na Maszynę wirtualną systemu Linux, ponieważ jest on wdrożony lub rozruchu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="7e2fa-117">Wstaw skrypty przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="7e2fa-118">Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="7e2fa-119">Szablonu platformy Azure przy użyciu inicjowania chmury.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="7e2fa-120">Przy użyciu szablonu Azure [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="7e2fa-121">skrypty tooinject w dowolnym momencie po rozruchu:</span><span class="sxs-lookup"><span data-stu-id="7e2fa-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="7e2fa-122">SSH toorun bezpośrednio poleceń</span><span class="sxs-lookup"><span data-stu-id="7e2fa-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="7e2fa-123">Wstaw skrypty przy użyciu hello Azure [rozszerzenia VMAccess](using-vmaccess-extension.md), imperatively lub szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7e2fa-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="7e2fa-124">Narzędzia zarządzania konfiguracją, takie jak Ansible, wartość Zaburzająca, Chef i Puppet.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="7e2fa-125">Rozszerzenia VMAccess wykonuje skrypt główny w hello takie same jak przy użyciu protokołu SSH może.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="7e2fa-126">Jednak używanie hello rozszerzenia maszyny Wirtualnej umożliwia kilka funkcji tej oferty Azure, które mogą być przydatne, w zależności od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="7e2fa-127">Dostępność init chmury na maszynie Wirtualnej Azure szybkie — tworzenie aliasów obrazu:</span><span class="sxs-lookup"><span data-stu-id="7e2fa-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="7e2fa-128">Alias</span><span class="sxs-lookup"><span data-stu-id="7e2fa-128">Alias</span></span> | <span data-ttu-id="7e2fa-129">Wydawca</span><span class="sxs-lookup"><span data-stu-id="7e2fa-129">Publisher</span></span> | <span data-ttu-id="7e2fa-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="7e2fa-130">Offer</span></span> | <span data-ttu-id="7e2fa-131">SKU</span><span class="sxs-lookup"><span data-stu-id="7e2fa-131">SKU</span></span> | <span data-ttu-id="7e2fa-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="7e2fa-132">Version</span></span> | <span data-ttu-id="7e2fa-133">init chmury</span><span class="sxs-lookup"><span data-stu-id="7e2fa-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="7e2fa-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-134">CentOS</span></span> |<span data-ttu-id="7e2fa-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="7e2fa-135">OpenLogic</span></span> |<span data-ttu-id="7e2fa-136">Centos</span><span class="sxs-lookup"><span data-stu-id="7e2fa-136">Centos</span></span> |<span data-ttu-id="7e2fa-137">7.2</span><span class="sxs-lookup"><span data-stu-id="7e2fa-137">7.2</span></span> |<span data-ttu-id="7e2fa-138">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-138">latest</span></span> |<span data-ttu-id="7e2fa-139">Brak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-139">no</span></span> |
| <span data-ttu-id="7e2fa-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-140">CoreOS</span></span> |<span data-ttu-id="7e2fa-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-141">CoreOS</span></span> |<span data-ttu-id="7e2fa-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-142">CoreOS</span></span> |<span data-ttu-id="7e2fa-143">Stable</span><span class="sxs-lookup"><span data-stu-id="7e2fa-143">Stable</span></span> |<span data-ttu-id="7e2fa-144">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-144">latest</span></span> |<span data-ttu-id="7e2fa-145">Tak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-145">yes</span></span> |
| <span data-ttu-id="7e2fa-146">Debian</span><span class="sxs-lookup"><span data-stu-id="7e2fa-146">Debian</span></span> |<span data-ttu-id="7e2fa-147">credativ</span><span class="sxs-lookup"><span data-stu-id="7e2fa-147">credativ</span></span> |<span data-ttu-id="7e2fa-148">Debian</span><span class="sxs-lookup"><span data-stu-id="7e2fa-148">Debian</span></span> |<span data-ttu-id="7e2fa-149">8</span><span class="sxs-lookup"><span data-stu-id="7e2fa-149">8</span></span> |<span data-ttu-id="7e2fa-150">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-150">latest</span></span> |<span data-ttu-id="7e2fa-151">Brak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-151">no</span></span> |
| <span data-ttu-id="7e2fa-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7e2fa-152">openSUSE</span></span> |<span data-ttu-id="7e2fa-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="7e2fa-153">SUSE</span></span> |<span data-ttu-id="7e2fa-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7e2fa-154">openSUSE</span></span> |<span data-ttu-id="7e2fa-155">13.2</span><span class="sxs-lookup"><span data-stu-id="7e2fa-155">13.2</span></span> |<span data-ttu-id="7e2fa-156">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-156">latest</span></span> |<span data-ttu-id="7e2fa-157">Brak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-157">no</span></span> |
| <span data-ttu-id="7e2fa-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="7e2fa-158">RHEL</span></span> |<span data-ttu-id="7e2fa-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="7e2fa-159">Redhat</span></span> |<span data-ttu-id="7e2fa-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="7e2fa-160">RHEL</span></span> |<span data-ttu-id="7e2fa-161">7.2</span><span class="sxs-lookup"><span data-stu-id="7e2fa-161">7.2</span></span> |<span data-ttu-id="7e2fa-162">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-162">latest</span></span> |<span data-ttu-id="7e2fa-163">Brak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-163">no</span></span> |
| <span data-ttu-id="7e2fa-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-164">UbuntuLTS</span></span> |<span data-ttu-id="7e2fa-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="7e2fa-165">Canonical</span></span> |<span data-ttu-id="7e2fa-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7e2fa-166">UbuntuServer</span></span> |<span data-ttu-id="7e2fa-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="7e2fa-167">14.04.4-LTS</span></span> |<span data-ttu-id="7e2fa-168">najnowsza</span><span class="sxs-lookup"><span data-stu-id="7e2fa-168">latest</span></span> |<span data-ttu-id="7e2fa-169">Tak</span><span class="sxs-lookup"><span data-stu-id="7e2fa-169">yes</span></span> |

<span data-ttu-id="7e2fa-170">Możemy pracy z naszych partnerów tooget chmury inicjowania uwzględnione i Praca w obrazach hello udostępniają one tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="7e2fa-171">Dodaj utworzenie init chmury skryptu toohello maszyny Wirtualnej z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7e2fa-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="7e2fa-172">toolaunch skryptu chmury init, podczas tworzenia maszyny Wirtualnej na platformie Azure, określ plik init chmury hello przy użyciu interfejsu wiersza polecenia Azure hello `--custom-data` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="7e2fa-173">Tworzenie maszyn wirtualnych do o toolaunch grupy zasobów [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7e2fa-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7e2fa-174">Witaj poniższy przykład tworzy hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7e2fa-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7e2fa-175">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="7e2fa-176">Utwórz nazwę chmury init skryptu tooset hello hosta maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7e2fa-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="7e2fa-177">Jedną z najważniejszych ustawień żadnej maszyny Wirtualnej systemu Linux i hello najprostszym byłoby hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="7e2fa-178">Firma Microsoft łatwo tę można skonfigurować przy użyciu inicjowania chmury za pomocą tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="7e2fa-179">Przykładowy skrypt init chmury o nazwie `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="7e2fa-180">Podczas hello wstępnego uruchamiania hello maszyny Wirtualnej, ten skrypt init chmury ustawia hello hostname zbyt*myservername*.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="7e2fa-181">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="7e2fa-182">Logowania i sprawdź nazwę hosta hello hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="7e2fa-183">Utwórz skrypt init chmury</span><span class="sxs-lookup"><span data-stu-id="7e2fa-183">Create a cloud-init script</span></span>
<span data-ttu-id="7e2fa-184">Dla bezpieczeństwa ma tooupdate Twojej maszyny Wirtualnej systemu Ubuntu przy pierwszym hello.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="7e2fa-185">Przy użyciu chmury init możemy, z hello Wykonaj skrypt, w zależności od hello dystrybucja systemu Linux, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="7e2fa-186">Przykładowy skrypt init chmury `cloud_config_apt_upgrade.txt` dla hello Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="7e2fa-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="7e2fa-187">Po uruchomieniu systemu Linux, wszystkich pakietów hello zainstalowane są aktualizowane za pośrednictwem **stanie get**.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="7e2fa-188">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="7e2fa-189">Logowania i sprawdź wszystkie pakiety zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="7e2fa-190">Utwórz tooadd skryptu init chmury tooLinux użytkownika</span><span class="sxs-lookup"><span data-stu-id="7e2fa-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="7e2fa-191">Jeden z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest tooadd użytkownika dla siebie lub przy użyciu tooavoid *głównego*.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="7e2fa-192">SSH klucze są najlepsze rozwiązanie dotyczące zabezpieczeń i użyteczność i są dodawane toohello *~/.ssh/authorized_keys* plików za pomocą tego skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="7e2fa-193">Przykładowy skrypt init chmury `cloud_config_add_users.txt` Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="7e2fa-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="7e2fa-194">Po uruchomieniu systemu Linux, wszyscy użytkownicy hello wymienione są utworzone i dodać toohello sudo grupy.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="7e2fa-195">Utwórz Maszynę wirtualną systemu Linux z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) przy użyciu chmury init tooconfigure go podczas rozruchu.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="7e2fa-196">Logowania i weryfikacji hello nowo utworzonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="7e2fa-197">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="7e2fa-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="7e2fa-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e2fa-198">Next steps</span></span>
<span data-ttu-id="7e2fa-199">Init chmurze staje się jeden toomodify standardowy sposób przy rozruchu maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="7e2fa-200">Platforma Azure ma rozszerzenia maszyny Wirtualnej, które pozwalają toomodify Twojego LinuxVM przy rozruchu lub jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="7e2fa-201">Na przykład można użyć hello Azure VMAccessExtension tooreset SSH lub informacje o użytkowniku hello maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="7e2fa-202">Z inicjowaniem chmury będzie potrzebny hasła hello tooreset ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="7e2fa-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="7e2fa-203">Temat funkcji i rozszerzeń maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7e2fa-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="7e2fa-204">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="7e2fa-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
