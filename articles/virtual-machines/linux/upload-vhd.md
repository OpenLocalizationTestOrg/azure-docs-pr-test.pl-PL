---
title: aaaUpload lub kopiowanie niestandardowych maszyny Wirtualnej systemu Linux 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Przekazywanie lub skopiowanie dostosowane maszyny wirtualnej przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="898e2-103">Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="898e2-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="898e2-104">W tym artykule opisano sposób tooupload dostosowane wirtualnego dysku twardego (VHD) lub skopiuj istniejącego dysku VHD na platformie Azure i tworzenie nowych maszyn wirtualnych systemu Linux (maszyn wirtualnych) z hello niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="898e2-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="898e2-105">Można zainstalować i skonfigurować wymagania dotyczące systemu Linux distro tooyour i następnie użyć tego wirtualnego dysku twardego tooquickly tworzenia nowej maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="898e2-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="898e2-106">Jeśli chcesz toocreate wiele maszyn wirtualnych z dostosowanych dysku, należy utworzyć obraz z maszyny Wirtualnej lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="898e2-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="898e2-107">Aby uzyskać więcej informacji, zobacz [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu interfejsu wiersza polecenia hello](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="898e2-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="898e2-108">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="898e2-108">You have two options:</span></span>
* [<span data-ttu-id="898e2-109">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="898e2-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="898e2-110">Skopiuj istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="898e2-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="898e2-111">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="898e2-111">Quick commands</span></span>

<span data-ttu-id="898e2-112">Podczas tworzenia nowej maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) z dysku dostosowane lub specjalne możesz **dołączyć** hello dysku (— attach-os-disk) zamiast określania obraz niestandardowy lub witryny marketplace (— obrazu).</span><span class="sxs-lookup"><span data-stu-id="898e2-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="898e2-113">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* za pomocą hello managed dysku o nazwie *myManagedDisk* utworzone na podstawie niestandardowych dysk VHD:</span><span class="sxs-lookup"><span data-stu-id="898e2-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="898e2-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="898e2-114">Requirements</span></span>
<span data-ttu-id="898e2-115">Witaj toocomplete następujące kroki, należy:</span><span class="sxs-lookup"><span data-stu-id="898e2-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="898e2-116">Maszyny wirtualnej systemu Linux, który został przygotowany do użycia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="898e2-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="898e2-117">Witaj [hello przygotowanie wirtualna](#prepare-the-vm) sekcji tego artykułu opisano, jak toofind distro określone informacje na temat instalowania hello agenta systemu Linux platformy Azure (agenta waagent), który jest wymagany dla hello wirtualna toowork poprawnie na platformie Azure i musisz toobe stanie tooconnect tooit przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="898e2-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="898e2-118">plik VHD Hello z istniejącego [dystrybucji Linux zatwierdzone na platformie Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w formacie VHD hello.</span><span class="sxs-lookup"><span data-stu-id="898e2-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="898e2-119">Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="898e2-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="898e2-120">Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu.</span><span class="sxs-lookup"><span data-stu-id="898e2-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="898e2-121">W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu **przekonwertować qemu img**.</span><span class="sxs-lookup"><span data-stu-id="898e2-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="898e2-122">Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="898e2-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="898e2-123">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="898e2-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="898e2-124">Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello.</span><span class="sxs-lookup"><span data-stu-id="898e2-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="898e2-125">W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [przekonwertować qemu img](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="898e2-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="898e2-126">Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem.</span><span class="sxs-lookup"><span data-stu-id="898e2-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="898e2-127">Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="898e2-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="898e2-128">Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="898e2-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="898e2-129">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="898e2-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="898e2-130">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="898e2-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="898e2-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="898e2-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="898e2-132">Przygotowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="898e2-132">Prepare hello VM</span></span>

<span data-ttu-id="898e2-133">Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="898e2-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="898e2-134">następujące artykuły Hello przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="898e2-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="898e2-135">Na podstawie centOS dystrybucji</span><span class="sxs-lookup"><span data-stu-id="898e2-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-136">Debian systemu Linux</span><span class="sxs-lookup"><span data-stu-id="898e2-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="898e2-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="898e2-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="898e2-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="898e2-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="898e2-141">Inne — niezatwierdzonych dystrybucji</span><span class="sxs-lookup"><span data-stu-id="898e2-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="898e2-142">Zobacz też hello [informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="898e2-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="898e2-143">Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) stosuje tooVMs systemem Linux, tylko gdy jeden z hello dystrybucje zatwierdzone na jest używany z hello szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na zatwierdzone na platformie Azure Dystrybucje](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898e2-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="898e2-144">Opcja 1: Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="898e2-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="898e2-145">Możesz przekazać dostosowane wirtualnego dysku twardego uruchomione na komputerze lokalnym lub wyeksportowany z innej chmury.</span><span class="sxs-lookup"><span data-stu-id="898e2-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="898e2-146">toouse hello wirtualnego dysku twardego toocreate nowej maszyny Wirtualnej Azure, należy tooupload hello wirtualnego dysku twardego tooa magazynu kont i Utwórz dysków zarządzanych z hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="898e2-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="898e2-147">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="898e2-147">Create a resource group</span></span>

<span data-ttu-id="898e2-148">Przed przekazaniem dysku niestandardowych i Tworzenie maszyn wirtualnych, należy najpierw toocreate grupą zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="898e2-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="898e2-149">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji: [dysków zarządzanych Azure — omówienie](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="898e2-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="898e2-150">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="898e2-150">Create a storage account</span></span>

<span data-ttu-id="898e2-151">Utwórz konto magazynu dla niestandardowego dysku i maszyn wirtualnych o [Tworzenie konta magazynu az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="898e2-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="898e2-152">Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu* w utworzoną wcześniej grupę zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="898e2-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="898e2-153">Wyświetl klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="898e2-153">List storage account keys</span></span>
<span data-ttu-id="898e2-154">Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="898e2-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="898e2-155">Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak przeprowadzanie operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="898e2-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="898e2-156">Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="898e2-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="898e2-157">Wyświetl klucze dostępu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="898e2-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="898e2-158">Wyświetl klucze dostępu hello utworzone konto magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="898e2-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="898e2-159">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="898e2-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="898e2-160">Zanotuj **klucz1** jako zostanie użyty toointeract z konta magazynu w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="898e2-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="898e2-161">Tworzenie kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="898e2-161">Create a storage container</span></span>
<span data-ttu-id="898e2-162">W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzyć dyski kontenery tooorganize konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="898e2-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="898e2-163">Konto magazynu może zawierać dowolną liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="898e2-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="898e2-164">Tworzenie kontenera z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="898e2-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="898e2-165">Witaj poniższy przykład tworzy kontener o nazwie *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="898e2-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="898e2-166">Przekaż hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="898e2-166">Upload hello VHD</span></span>
<span data-ttu-id="898e2-167">Teraz Przekaż dysku niestandardowych z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="898e2-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="898e2-168">Przekazywanie i przechowywać dysku niestandardowych jako stronicowy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="898e2-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="898e2-169">Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello niestandardowego dysku na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="898e2-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="898e2-170">Witaj przekazywanie wirtualnego dysku twardego może chwilę potrwać.</span><span class="sxs-lookup"><span data-stu-id="898e2-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="898e2-171">Tworzenie dysku zarządzanego</span><span class="sxs-lookup"><span data-stu-id="898e2-171">Create a managed disk</span></span>


<span data-ttu-id="898e2-172">Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego za pomocą [Tworzenie dysku az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="898e2-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="898e2-173">Witaj poniższy przykład tworzy zarządzanych dysk o nazwie *myManagedDisk* z wirtualnego dysku twardego hello przekazać tooyour o nazwie konto magazynu i kontener:</span><span class="sxs-lookup"><span data-stu-id="898e2-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="898e2-174">Opcja 2: Kopiowanie istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="898e2-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="898e2-175">Można również utworzyć hello dostosowane maszyny Wirtualnej w ramach platformy Azure, a następnie dysku systemu operacyjnego hello kopii i dołącz je tooa nowej maszyny Wirtualnej toocreate kolejną kopię.</span><span class="sxs-lookup"><span data-stu-id="898e2-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="898e2-176">Jest to testowania poprawnie, ale jeśli chcesz toouse istniejącej maszyny Wirtualnej platformy Azure jako hello model wiele nowych maszyn wirtualnych, naprawdę należy utworzyć **obrazu** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="898e2-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="898e2-177">Aby uzyskać więcej informacji o tworzeniu obrazu z istniejącej maszyny Wirtualnej Azure, zobacz [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu hello interfejsu wiersza polecenia](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="898e2-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="898e2-178">Utwórz migawkę</span><span class="sxs-lookup"><span data-stu-id="898e2-178">Create a snapshot</span></span>

<span data-ttu-id="898e2-179">W tym przykładzie tworzy migawkę maszyny wirtualnej o nazwie *myVM* w grupie zasobów *myResourceGroup* i tworzy migawkę o nazwie *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="898e2-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="898e2-180">Tworzenie dysków zarządzanych w hello</span><span class="sxs-lookup"><span data-stu-id="898e2-180">Create hello managed disk</span></span>

<span data-ttu-id="898e2-181">Utwórz nowy dysk zarządzanego z hello migawki.</span><span class="sxs-lookup"><span data-stu-id="898e2-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="898e2-182">Pobierz identyfikator hello hello migawki.</span><span class="sxs-lookup"><span data-stu-id="898e2-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="898e2-183">W tym przykładzie hello migawki o nazwie *osDiskSnapshot* i hello *myResourceGroup* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="898e2-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="898e2-184">Utwórz hello dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="898e2-184">Create hello managed disk.</span></span> <span data-ttu-id="898e2-185">W tym przykładzie utworzysz zarządzanych dysk o nazwie *myManagedDisk* z naszych migawki to 128 GB w rozmiarze w magazynu w warstwie standardowa.</span><span class="sxs-lookup"><span data-stu-id="898e2-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="898e2-186">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="898e2-186">Create hello VM</span></span>

<span data-ttu-id="898e2-187">Teraz utworzyć maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i Dołącz (--attach-os-disk) hello zarządzane dysku jako dysku hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="898e2-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="898e2-188">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myNewVM* za pomocą hello managed utworzone na podstawie przekazanego dysk VHD dysku:</span><span class="sxs-lookup"><span data-stu-id="898e2-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="898e2-189">Powinno być możliwe tooSSH do hello maszyny Wirtualnej przy użyciu poświadczeń hello z hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="898e2-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="898e2-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="898e2-190">Next steps</span></span>
<span data-ttu-id="898e2-191">Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="898e2-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="898e2-192">Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="898e2-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="898e2-193">Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="898e2-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

