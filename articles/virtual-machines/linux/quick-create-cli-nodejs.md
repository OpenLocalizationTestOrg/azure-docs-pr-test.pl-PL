---
title: "Tworzenie maszyny wirtualnej z systemem Linux przy użyciu interfejsu wiersza polecenia platformy Azure 1.0 | Microsoft Docs"
description: "Tworzenie maszyny wirtualnej z systemem Linux na platformie Azure przy użyciu interfejsu wiersza polecenia platformy Azure 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="cfbfd-103">Tworzenie maszyny wirtualnej z systemem Linux przy użyciu interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cfbfd-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="cfbfd-104">Ten artykuł pokazuje, jak szybko wdrożyć maszynę wirtualną systemu Linux na platformie Azure przy użyciu polecenia `azure vm quick-create` w interfejsie wiersza polecenia (CLI) platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="cfbfd-105">Polecenie `quick-create` umożliwia wdrożenie maszyny wirtualnej wewnątrz podstawowej, bezpiecznej infrastruktury, której można używać do prototypowania lub szybkiego testowania koncepcji.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="cfbfd-106">Aby utworzyć maszynę wirtualną przy użyciu interfejsu wiersza polecenia platformy Azure 2.0, zobacz [Tworzenie maszyny wirtualnej za pomocą interfejsu wiersza polecenia platformy Azure](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cfbfd-107">Szybkie wdrożenie maszyny wirtualnej z systemem Linux jest możliwe również przy użyciu witryny [Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cfbfd-108">Wymaga artykułu [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="cfbfd-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="cfbfd-109">Quick commands</span></span>

<span data-ttu-id="cfbfd-110">Poniższy przykład pokazuje, jak wdrożyć maszynę Wirtualną CoreOS i dołączyć klucz Secure Shell (SSH) (argumenty mogą się różnić).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cfbfd-111">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="cfbfd-111">Detailed walkthrough</span></span>

<span data-ttu-id="cfbfd-112">W następującym przewodniku krok po kroku wdrażana jest maszyna wirtualna z systemem UbuntuLTS. Przy każdym kroku wyjaśnione jest, co dany krok robi.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="cfbfd-113">Aliasy szybkiego tworzenia maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cfbfd-113">VM quick-create aliases</span></span>

<span data-ttu-id="cfbfd-114">Szybkim sposobem wyboru dystrybucji jest użycie aliasów interfejsu wiersza polecenia (CLI) platformy Azure przypisanych najbardziej typowym dystrybucjom systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="cfbfd-115">Poniższa tabela zawiera listę aliasów dystrybucji (stan dla interfejsu wiersza polecenia platformy Azure w wersji 0.10).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="cfbfd-116">Wszystkie wdrożenia, które używają polecenia `quick-create`, są domyślnie maszynami wirtualnymi na dyskach półprzewodnikowych (SSD), zapewniających szybszą aprowizację oraz wyższą wydajność dostępu do dysku.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="cfbfd-117">(Te aliasy stanowią niewielką część dystrybucji dostępnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="cfbfd-118">Więcej obrazów można znaleźć w witrynie Azure Marketplace, [wyszukując obraz w programie PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [w sieci Web](https://azure.microsoft.com/marketplace/virtual-machines/) albo [przesyłając własny obraz niestandardowy](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="cfbfd-119">Alias</span><span class="sxs-lookup"><span data-stu-id="cfbfd-119">Alias</span></span> | <span data-ttu-id="cfbfd-120">Wydawca</span><span class="sxs-lookup"><span data-stu-id="cfbfd-120">Publisher</span></span> | <span data-ttu-id="cfbfd-121">Oferta</span><span class="sxs-lookup"><span data-stu-id="cfbfd-121">Offer</span></span> | <span data-ttu-id="cfbfd-122">SKU</span><span class="sxs-lookup"><span data-stu-id="cfbfd-122">SKU</span></span> | <span data-ttu-id="cfbfd-123">Wersja</span><span class="sxs-lookup"><span data-stu-id="cfbfd-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="cfbfd-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-124">CentOS</span></span> |<span data-ttu-id="cfbfd-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="cfbfd-125">OpenLogic</span></span> |<span data-ttu-id="cfbfd-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-126">CentOS</span></span> |<span data-ttu-id="cfbfd-127">7.2</span><span class="sxs-lookup"><span data-stu-id="cfbfd-127">7.2</span></span> |<span data-ttu-id="cfbfd-128">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-128">latest</span></span> |
| <span data-ttu-id="cfbfd-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-129">CoreOS</span></span> |<span data-ttu-id="cfbfd-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-130">CoreOS</span></span> |<span data-ttu-id="cfbfd-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-131">CoreOS</span></span> |<span data-ttu-id="cfbfd-132">Stable</span><span class="sxs-lookup"><span data-stu-id="cfbfd-132">Stable</span></span> |<span data-ttu-id="cfbfd-133">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-133">latest</span></span> |
| <span data-ttu-id="cfbfd-134">Debian</span><span class="sxs-lookup"><span data-stu-id="cfbfd-134">Debian</span></span> |<span data-ttu-id="cfbfd-135">credativ</span><span class="sxs-lookup"><span data-stu-id="cfbfd-135">credativ</span></span> |<span data-ttu-id="cfbfd-136">Debian</span><span class="sxs-lookup"><span data-stu-id="cfbfd-136">Debian</span></span> |<span data-ttu-id="cfbfd-137">8</span><span class="sxs-lookup"><span data-stu-id="cfbfd-137">8</span></span> |<span data-ttu-id="cfbfd-138">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-138">latest</span></span> |
| <span data-ttu-id="cfbfd-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cfbfd-139">openSUSE</span></span> |<span data-ttu-id="cfbfd-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="cfbfd-140">SUSE</span></span> |<span data-ttu-id="cfbfd-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cfbfd-141">openSUSE</span></span> |<span data-ttu-id="cfbfd-142">13.2</span><span class="sxs-lookup"><span data-stu-id="cfbfd-142">13.2</span></span> |<span data-ttu-id="cfbfd-143">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-143">latest</span></span> |
| <span data-ttu-id="cfbfd-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="cfbfd-144">RHEL</span></span> |<span data-ttu-id="cfbfd-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="cfbfd-145">Red Hat</span></span> |<span data-ttu-id="cfbfd-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="cfbfd-146">RHEL</span></span> |<span data-ttu-id="cfbfd-147">7.2</span><span class="sxs-lookup"><span data-stu-id="cfbfd-147">7.2</span></span> |<span data-ttu-id="cfbfd-148">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-148">latest</span></span> |
| <span data-ttu-id="cfbfd-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-149">UbuntuLTS</span></span> |<span data-ttu-id="cfbfd-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="cfbfd-150">Canonical</span></span> |<span data-ttu-id="cfbfd-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="cfbfd-151">Ubuntu Server</span></span> |<span data-ttu-id="cfbfd-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="cfbfd-152">14.04.4-LTS</span></span> |<span data-ttu-id="cfbfd-153">najnowsza</span><span class="sxs-lookup"><span data-stu-id="cfbfd-153">latest</span></span> |

<span data-ttu-id="cfbfd-154">W poniższych sekcjach użyto aliasu `UbuntuLTS` dla opcji **ImageURN** (`-Q`) w celu wdrożenia w systemie Ubuntu 14.04.4 LTS Server.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="cfbfd-155">W poprzednim przykładzie polecenie `quick-create` wywoływało tylko flagę `-M` w celu identyfikacji klucza publicznego SSH do przesłania po wyłączeniu haseł SSH, więc zostanie wyświetlony monit o wprowadzenie następujących argumentów:</span><span class="sxs-lookup"><span data-stu-id="cfbfd-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="cfbfd-156">nazwę grupy zasobów (dla pierwszej grupy zasobów platformy Azure jest zazwyczaj odpowiedni dowolny ciąg)</span><span class="sxs-lookup"><span data-stu-id="cfbfd-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="cfbfd-157">Nazwa maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cfbfd-157">VM name</span></span>
* <span data-ttu-id="cfbfd-158">lokalizacja (dobre wartości domyślne to `westus` lub `westeurope`)</span><span class="sxs-lookup"><span data-stu-id="cfbfd-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="cfbfd-159">linux (wskazanie platformie Azure pożądanego systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="cfbfd-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="cfbfd-160">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="cfbfd-160">username</span></span>

<span data-ttu-id="cfbfd-161">W poniższym przykładzie określono wszystkie wartości, dzięki czemu żadne dalsze monity nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="cfbfd-162">Plik klucza publicznego w formacie ssh-rsa `~/.ssh/id_rsa.pub` działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="cfbfd-163">Dane wyjściowe powinny wyglądać podobnie do następującego bloku:</span><span class="sxs-lookup"><span data-stu-id="cfbfd-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="cfbfd-164">Logowanie się do nowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cfbfd-164">Log in to the new VM</span></span>
<span data-ttu-id="cfbfd-165">Zaloguj się do maszyny wirtualnej, używając publicznego adresu IP podanego w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="cfbfd-166">Można również użyć podanej w pełni kwalifikowanej nazwy domeny (FQDN):</span><span class="sxs-lookup"><span data-stu-id="cfbfd-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="cfbfd-167">Proces logowania powinien wyglądać podobnie do następującego bloku danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="cfbfd-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="cfbfd-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfbfd-168">Next steps</span></span>
<span data-ttu-id="cfbfd-169">Polecenie `azure vm quick-create` jest szybkim sposobem wdrożenia maszyny wirtualnej, dzięki któremu możesz zalogować się do powłoki bash i rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="cfbfd-170">Jednak użycie polecenia `vm quick-create` nie zapewnia rozbudowanej kontroli ani nie umożliwia tworzenia bardziej złożonego środowiska.</span><span class="sxs-lookup"><span data-stu-id="cfbfd-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="cfbfd-171">Aby wdrożyć maszynę wirtualną z systemem Linux dostosowaną do swojej infrastruktury, możesz skorzystać z dowolnego z poniższych artykułów:</span><span class="sxs-lookup"><span data-stu-id="cfbfd-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="cfbfd-172">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cfbfd-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cfbfd-173">Tworzenie maszyny wirtualnej z systemem Linux zabezpieczonej przez protokół SSH na platformie Azure przy użyciu szablonów</span><span class="sxs-lookup"><span data-stu-id="cfbfd-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="cfbfd-174">Można również [użyć sterownika platformy Azure `docker-machine` z różnymi poleceniami do szybkiego utworzenia maszyny wirtualnej systemu Linux jako hosta docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfbfd-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
