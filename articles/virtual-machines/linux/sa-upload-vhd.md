---
title: aaaUpload niestandardowego dysku Linux Azure CLI 2.0 | Dokumentacja firmy Microsoft
description: "Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego (VHD), przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI 2.0"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="6080d-103">Przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6080d-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="6080d-104">W tym artykule pokazano, jak tooupload tooan wirtualnego dysku twardego (VHD) magazynu Azure konta hello Azure CLI 2.0 i Tworzenie maszyn wirtualnych systemu Linux z tego dysku niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="6080d-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="6080d-105">Można również wykonać te kroki hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6080d-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6080d-106">Ta funkcja pozwala tooinstall i skonfiguruj wymagania tooyour distro systemu Linux, a następnie użyj tego wirtualnego dysku twardego tooquickly Tworzenie maszyn wirtualnych platformy Azure (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="6080d-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="6080d-107">W tym temacie używa konta magazynu dla hello końcowego wirtualne dyski twarde, ale można też wykonać te czynności przy użyciu [dyskach zarządzanych](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="6080d-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="6080d-108">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="6080d-108">Quick commands</span></span>
<span data-ttu-id="6080d-109">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="6080d-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="6080d-110">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#requirements).</span><span class="sxs-lookup"><span data-stu-id="6080d-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="6080d-111">Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6080d-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6080d-112">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="6080d-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6080d-113">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="6080d-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="6080d-114">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6080d-115">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUs` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="6080d-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="6080d-116">Tworzenie dysków wirtualnych z toohold konta magazynu [Tworzenie konta magazynu az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="6080d-117">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="6080d-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="6080d-118">Listę hello klawiszy dostępu dla konta magazynu z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="6080d-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="6080d-119">Zanotuj `key1`:</span><span class="sxs-lookup"><span data-stu-id="6080d-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="6080d-120">Utwórz kontener w ramach konta magazynu przy użyciu klucza magazynu hello uzyskany z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="6080d-121">Witaj poniższy przykład tworzy kontener o nazwie `mydisks` przy użyciu wartości klucza magazynu hello z `key1`:</span><span class="sxs-lookup"><span data-stu-id="6080d-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="6080d-122">Na koniec, przekaż z kontenera toohello VHD zostały utworzone z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="6080d-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="6080d-123">Określ hello tooyour ścieżkę lokalną wirtualnego dysku twardego w obszarze `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="6080d-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="6080d-124">Określ dysk tooyour URI hello (`--image`) z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6080d-125">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:</span><span class="sxs-lookup"><span data-stu-id="6080d-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="6080d-126">Konto magazynu docelowego Hello ma toobe hello sam jako gdzie przekazany wirtualny dysk.</span><span class="sxs-lookup"><span data-stu-id="6080d-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="6080d-127">Możesz również muszą toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello **tworzenia maszyny wirtualnej az** polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="6080d-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="6080d-128">Więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="6080d-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="6080d-129">Wymagania</span><span class="sxs-lookup"><span data-stu-id="6080d-129">Requirements</span></span>
<span data-ttu-id="6080d-130">Witaj toocomplete następujące kroki, należy:</span><span class="sxs-lookup"><span data-stu-id="6080d-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="6080d-131">**Linux zainstalowanego systemu operacyjnego w pliku VHD** -Zainstaluj [dystrybucji zatwierdzone na platformie Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w hello wirtualnego dysku twardego Format.</span><span class="sxs-lookup"><span data-stu-id="6080d-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="6080d-132">Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="6080d-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="6080d-133">Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu.</span><span class="sxs-lookup"><span data-stu-id="6080d-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="6080d-134">W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="6080d-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="6080d-135">Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="6080d-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6080d-136">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6080d-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="6080d-137">Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello.</span><span class="sxs-lookup"><span data-stu-id="6080d-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="6080d-138">W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6080d-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="6080d-139">Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem.</span><span class="sxs-lookup"><span data-stu-id="6080d-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="6080d-140">Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="6080d-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="6080d-141">Maszyny wirtualne utworzone na podstawie niestandardowych dysku musi znajdować się w hello samo konto magazynu jako hello samego dysku</span><span class="sxs-lookup"><span data-stu-id="6080d-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="6080d-142">Tworzenie toohold konto i kontener magazynu zarówno niestandardowego dysku i utworzone maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="6080d-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="6080d-143">Po utworzeniu wszystkich maszyn wirtualnych, można bezpiecznie usunąć dysku</span><span class="sxs-lookup"><span data-stu-id="6080d-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="6080d-144">Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6080d-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6080d-145">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="6080d-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6080d-146">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="6080d-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="6080d-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="6080d-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="6080d-148">Przygotowanie toobe dysku hello przekazany</span><span class="sxs-lookup"><span data-stu-id="6080d-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="6080d-149">Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="6080d-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="6080d-150">następujące artykuły Hello przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="6080d-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="6080d-151">**[Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-152">**[Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="6080d-157">**[Inne — niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="6080d-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="6080d-158">Zobacz też hello  **[informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6080d-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6080d-159">Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) stosuje tooVMs systemem Linux, tylko gdy jeden z hello dystrybucje zatwierdzone na jest używany z hello szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na zatwierdzone na platformie Azure Dystrybucje](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6080d-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="6080d-160">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="6080d-160">Create a resource group</span></span>
<span data-ttu-id="6080d-161">Grupy zasobów logicznie zebranie wszystkich toosupport zasobów Azure hello maszyn wirtualnych, takie jak hello sieci wirtualnych i magazynu.</span><span class="sxs-lookup"><span data-stu-id="6080d-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="6080d-162">Dla grup zasobów więcej informacji, zobacz [omówienie grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6080d-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6080d-163">Przed przekazaniem dysku niestandardowych i Tworzenie maszyn wirtualnych, należy najpierw toocreate grupą zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="6080d-164">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="6080d-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="6080d-165">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6080d-165">Create a storage account</span></span>

<span data-ttu-id="6080d-166">Utwórz konto magazynu dla niestandardowego dysku i maszyn wirtualnych o [Tworzenie konta magazynu az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="6080d-167">Wszystkie maszyny wirtualne z dyskami niezarządzane, tworzonych z Twojej toobe potrzeby niestandardowego dysku w hello tego samego konta magazynu jako tego dysku.</span><span class="sxs-lookup"><span data-stu-id="6080d-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="6080d-168">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount` w utworzoną wcześniej grupę zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="6080d-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="6080d-169">Wyświetl klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6080d-169">List storage account keys</span></span>
<span data-ttu-id="6080d-170">Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6080d-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="6080d-171">Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak toocarry operacje zapisu.</span><span class="sxs-lookup"><span data-stu-id="6080d-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="6080d-172">Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6080d-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="6080d-173">Wyświetl klucze dostępu hello z [listy kluczy konta magazynu az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="6080d-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="6080d-174">Wyświetl klucze dostępu hello utworzone konto magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="6080d-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="6080d-175">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="6080d-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="6080d-176">Zanotuj `key1` jak zostanie użyty toointeract z konta magazynu w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="6080d-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="6080d-177">Tworzenie kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="6080d-177">Create a storage container</span></span>
<span data-ttu-id="6080d-178">W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzyć dyski kontenery tooorganize konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6080d-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="6080d-179">Konto magazynu może zawierać dowolną liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6080d-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="6080d-180">Tworzenie kontenera z [utworzyć kontenera magazynu az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="6080d-181">Witaj poniższy przykład tworzy kontener o nazwie `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="6080d-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="6080d-182">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6080d-182">Upload VHD</span></span>
<span data-ttu-id="6080d-183">Teraz Przekaż dysku niestandardowych z [az magazynu obiektów blob przekazywania](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="6080d-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="6080d-184">Przekazywanie i przechowywać dysku niestandardowych jako stronicowy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="6080d-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="6080d-185">Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello niestandardowego dysku na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="6080d-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="6080d-186">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6080d-186">Create hello VM</span></span>
<span data-ttu-id="6080d-187">toocreate maszyny Wirtualnej z dyskami niezarządzane, określ dysk tooyour URI hello (`--image`) z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6080d-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6080d-188">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:</span><span class="sxs-lookup"><span data-stu-id="6080d-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="6080d-189">Określ hello `--image` parametr o [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) toopoint tooyour niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="6080d-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="6080d-190">Upewnij się, że `--storage-account` dopasowań hello konto magazynu, w którym przechowywane niestandardowe dysku.</span><span class="sxs-lookup"><span data-stu-id="6080d-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="6080d-191">Nie masz toouse hello tego samego kontenera jako hello toostore niestandardowego dysku maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6080d-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="6080d-192">Upewnij się, że toocreate żadnych dodatkowych kontenerów w hello sam sposób jak hello wcześniejszych krokach przed przekazaniem dysku niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="6080d-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="6080d-193">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z dysku niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="6080d-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="6080d-194">Możesz nadal konieczne toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello **tworzenia maszyny wirtualnej az** polecenia takie jak nazwa użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="6080d-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="6080d-195">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6080d-195">Resource Manager template</span></span>
<span data-ttu-id="6080d-196">Szablony usługi Azure Resource Manager są plików JavaScript Object Notation (JSON), które definiują środowiska hello mają toobuild.</span><span class="sxs-lookup"><span data-stu-id="6080d-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="6080d-197">Szablony Hello dzieli się toodifferent dostawców zasobów, takich jak obliczeń lub sieci.</span><span class="sxs-lookup"><span data-stu-id="6080d-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="6080d-198">Możesz użyć istniejących szablonów lub napisać własny.</span><span class="sxs-lookup"><span data-stu-id="6080d-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="6080d-199">Przeczytaj więcej na temat [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6080d-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="6080d-200">W ramach hello `Microsoft.Compute/virtualMachines` dostawcy szablonu, masz `storageProfile` węzła, który zawiera szczegóły konfiguracji powitania dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6080d-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="6080d-201">Witaj dwie główne parametry tooedit są hello `image` i `vhd` identyfikatorów URI punktu tooyour niestandardowego dysku i dysk wirtualny nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6080d-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="6080d-202">Hello poniżej przedstawiono przykład hello JSON dla przy użyciu niestandardowego dysku:</span><span class="sxs-lookup"><span data-stu-id="6080d-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="6080d-203">Można użyć [toocreate tego istniejącego szablonu maszyny Wirtualnej z obrazu niestandardowego](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) lub przeczytaj o [Tworzenie szablonów usługi Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6080d-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="6080d-204">Po utworzeniu szablonu skonfigurowanego użyj [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6080d-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="6080d-205">Określ identyfikator URI szablonu JSON hello z hello `--template-uri` parametru:</span><span class="sxs-lookup"><span data-stu-id="6080d-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="6080d-206">Jeśli masz plik JSON przechowywane lokalnie na komputerze, możesz użyć hello `--template-file` parametru zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="6080d-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="6080d-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6080d-207">Next steps</span></span>
<span data-ttu-id="6080d-208">Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6080d-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6080d-209">Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6080d-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="6080d-210">Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6080d-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

