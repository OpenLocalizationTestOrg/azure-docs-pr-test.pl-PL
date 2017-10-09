---
title: aaaUpload niestandardowego obrazu systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft
description: "Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego (VHD) z niestandardowego obrazu systemu Linux przy użyciu modelu wdrażania usługi Resource Manager hello i hello Azure CLI w wersji 1.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="3b4c3-103">Przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="3b4c3-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="3b4c3-104">W tym artykule opisano sposób tooupload tooAzure wirtualnego dysku twardego (VHD) przy użyciu hello modelu wdrażania usługi Resource Manager i Tworzenie maszyn wirtualnych systemu Linux z tego obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="3b4c3-105">Ta funkcja pozwala tooinstall i skonfiguruj wymagania tooyour distro systemu Linux, a następnie użyj tego wirtualnego dysku twardego tooquickly Tworzenie maszyn wirtualnych platformy Azure (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3b4c3-106">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="3b4c3-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3b4c3-107">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3b4c3-108">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="3b4c3-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3b4c3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="3b4c3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3b4c3-110">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="3b4c3-110">Quick commands</span></span>
<span data-ttu-id="3b4c3-111">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="3b4c3-112">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#requirements).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="3b4c3-113">Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3b4c3-114">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3b4c3-115">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="3b4c3-116">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-116">First, create a resource group.</span></span> <span data-ttu-id="3b4c3-117">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUs` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="3b4c3-118">Tworzenie dysków wirtualnych toohold konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="3b4c3-119">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="3b4c3-120">Lista hello klucze dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="3b4c3-121">Zanotuj `key1`:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="3b4c3-122">Utwórz kontener w ramach konta magazynu przy użyciu klucza magazynu hello, który został uzyskany.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="3b4c3-123">Witaj poniższy przykład tworzy kontener o nazwie `myimages` przy użyciu wartości klucza magazynu hello z `key1`:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="3b4c3-124">Na koniec przekazać kontener toohello Twojego wirtualnego dysku twardego, utworzony.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="3b4c3-125">Określ hello tooyour ścieżkę lokalną wirtualnego dysku twardego w obszarze `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="3b4c3-126">Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="3b4c3-127">Umożliwia także hello interfejsu wiersza polecenia, określając hello URI tooyour dysku (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="3b4c3-128">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego hello wcześniej przekazany:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="3b4c3-129">Konto magazynu docelowego Hello ma toobe hello sam jako gdzie przekazany wirtualny dysk.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="3b4c3-130">Możesz również muszą toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="3b4c3-131">Więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="3b4c3-132">Wymagania</span><span class="sxs-lookup"><span data-stu-id="3b4c3-132">Requirements</span></span>
<span data-ttu-id="3b4c3-133">Witaj toocomplete następujące kroki, należy:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="3b4c3-134">**Linux zainstalowanego systemu operacyjnego w pliku VHD** -Zainstaluj [dystrybucji zatwierdzone na platformie Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w hello wirtualnego dysku twardego Format.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="3b4c3-135">Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="3b4c3-136">Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="3b4c3-137">W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="3b4c3-138">Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3b4c3-139">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="3b4c3-140">Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="3b4c3-141">W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="3b4c3-142">Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="3b4c3-143">Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="3b4c3-144">Maszyny wirtualne utworzone na podstawie niestandardowego obrazu musi znajdować się w hello samo konto magazynu jako hello samego obrazu</span><span class="sxs-lookup"><span data-stu-id="3b4c3-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="3b4c3-145">Tworzenie toohold konto i kontener magazynu zarówno niestandardowego obrazu i utworzone maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="3b4c3-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="3b4c3-146">Po utworzeniu wszystkich maszyn wirtualnych, można bezpiecznie usunąć obrazu</span><span class="sxs-lookup"><span data-stu-id="3b4c3-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="3b4c3-147">Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3b4c3-148">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3b4c3-149">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="3b4c3-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="3b4c3-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="3b4c3-151">Przygotowanie toobe obraz powitania przekazany</span><span class="sxs-lookup"><span data-stu-id="3b4c3-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="3b4c3-152">Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="3b4c3-153">następujące artykuły Hello przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="3b4c3-154">**[Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-155">**[Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3b4c3-160">**[Inne — niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3b4c3-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="3b4c3-161">Zobacz też hello  **[informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="3b4c3-162">Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) stosuje tooVMs systemem Linux, tylko gdy jeden z hello dystrybucje zatwierdzone na jest używany z hello szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na zatwierdzone na platformie Azure Dystrybucje](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="3b4c3-163">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3b4c3-163">Create a resource group</span></span>
<span data-ttu-id="3b4c3-164">Grupy zasobów logicznie zebranie wszystkich toosupport zasobów Azure hello maszyn wirtualnych, takie jak hello sieci wirtualnych i magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="3b4c3-165">Przeczytaj więcej na temat [grupy zasobów platformy Azure, w tym miejscu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="3b4c3-166">Przed przekazaniem obrazu niestandardowego dysku i Tworzenie maszyn wirtualnych, najpierw toocreate grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="3b4c3-167">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="3b4c3-168">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3b4c3-168">Create a storage account</span></span>
<span data-ttu-id="3b4c3-169">Maszyny wirtualne są przechowywane jako stronicowe obiekty BLOB w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="3b4c3-170">Przeczytaj więcej na temat [magazynu obiektów blob platformy Azure w tym miejscu](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="3b4c3-171">Możesz utworzyć konto magazynu obrazu niestandardowego dysku i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="3b4c3-172">Wszystkie maszyny wirtualne utworzone z dysku niestandardowego obrazu muszą toobe w hello tego samego konta magazynu jako obrazu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="3b4c3-173">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount` w utworzoną wcześniej grupę zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="3b4c3-174">Wyświetl klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3b4c3-174">List storage account keys</span></span>
<span data-ttu-id="3b4c3-175">Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="3b4c3-176">Klawisze dostępu są używane podczas uwierzytelniania toohello konta magazynu, takich jak toocarry operacje zapisu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="3b4c3-177">Przeczytaj więcej na temat [Zarządzanie dostępu tutaj toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="3b4c3-178">Możesz wyświetlić klawisze dostępu z hello `azure storage account keys list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="3b4c3-179">Wyświetl klucze dostępu hello utworzone konto magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="3b4c3-180">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="3b4c3-181">Zanotuj `key1` jak zostanie użyty toointeract z konta magazynu w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="3b4c3-182">Tworzenie kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="3b4c3-182">Create a storage container</span></span>
<span data-ttu-id="3b4c3-183">W hello sam sposób, że toologically różnych katalogach organizowanie lokalnego systemu plików, tworzenie kontenery w ramach tooorganize konta magazynu dysków wirtualnych i obrazów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="3b4c3-184">Konto magazynu może zawierać dowolną liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="3b4c3-185">Witaj poniższy przykład tworzy kontener o nazwie `myimages`, określania klucza dostępu hello uzyskanych w poprzednim kroku hello (`key1`):</span><span class="sxs-lookup"><span data-stu-id="3b4c3-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="3b4c3-186">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="3b4c3-186">Upload VHD</span></span>
<span data-ttu-id="3b4c3-187">Teraz można faktycznie przekazywanie obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="3b4c3-188">Jako wszystkich wirtualnych dysków używanych przez maszyny wirtualne, należy przekazać i przechowywania obrazu niestandardowego dysku jako stronicowy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="3b4c3-189">Określ użytkownika klucza dostępu, kontener hello, utworzony w poprzednim kroku hello, a następnie hello ścieżki toohello dysku niestandardowego obrazu na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="3b4c3-190">Tworzenie maszyny Wirtualnej z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="3b4c3-190">Create VM from custom image</span></span>
<span data-ttu-id="3b4c3-191">Podczas tworzenia maszyn wirtualnych z obrazu niestandardowego dysku, należy określić obraz dysku toohello URI hello.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="3b4c3-192">Upewnij się, że hello zgodne konto magazynu docelowego przechowywania obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="3b4c3-193">Można utworzyć maszyny Wirtualnej przy użyciu szablonu hello Azure CLI lub JSON Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="3b4c3-194">Utwórz maszynę Wirtualną przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b4c3-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="3b4c3-195">Określ hello `--image-urn` parametr hello `azure vm create` polecenia toopoint tooyour dysku niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="3b4c3-196">Upewnij się, że `--storage-account-name` dopasowań hello przechowywania obrazu niestandardowego dysku konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="3b4c3-197">Nie masz toouse hello tego samego kontenera jako hello toostore obrazu niestandardowego dysku maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="3b4c3-198">Upewnij się, że toocreate żadnych dodatkowych kontenerów w hello sam sposób jak hello wcześniejszych krokach przed przekazaniem dysku niestandardowych obrazów.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="3b4c3-199">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z obrazu niestandardowego dysku:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="3b4c3-200">Możesz nadal konieczne toospecify lub wyświetla monit o odpowiedź, hello wszystkie dodatkowe parametry wymagane przez hello `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="3b4c3-201">Dowiedz się więcej o hello [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="3b4c3-202">Utwórz maszynę Wirtualną przy użyciu szablonu JSON</span><span class="sxs-lookup"><span data-stu-id="3b4c3-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="3b4c3-203">Szablony usługi Azure Resource Manager są plików JavaScript Object Notation (JSON), które definiują środowiska hello mają toobuild.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="3b4c3-204">Szablony Hello dzieli się toodifferent dostawców zasobów, takich jak obliczeń lub sieci.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="3b4c3-205">Możesz użyć istniejących szablonów lub napisać własny.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="3b4c3-206">Przeczytaj więcej na temat [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="3b4c3-207">W ramach hello `Microsoft.Compute/virtualMachines` dostawcy szablonu, masz `storageProfile` węzła, który zawiera szczegóły konfiguracji powitania dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="3b4c3-208">Witaj dwie główne parametry tooedit są hello `image` i `vhd` identyfikatorów URI punktu tooyour obrazu niestandardowego dysku i dysk wirtualny nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="3b4c3-209">Witaj poniżej przedstawiono przykład hello JSON dla przy użyciu obrazu niestandardowego dysku:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="3b4c3-210">Można użyć [toocreate tego istniejącego szablonu maszyny Wirtualnej z obrazu niestandardowego](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) lub przeczytaj o [Tworzenie szablonów usługi Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="3b4c3-211">Po utworzeniu szablonu skonfigurowanego tworzenia maszyn wirtualnych przy użyciu hello `azure group deployment create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="3b4c3-212">Określ identyfikator URI szablonu JSON hello z hello `--template-uri` parametru:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="3b4c3-213">Jeśli masz plik JSON przechowywane lokalnie na komputerze, możesz użyć hello `--template-file` parametru zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="3b4c3-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="3b4c3-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b4c3-214">Next steps</span></span>
<span data-ttu-id="3b4c3-215">Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="3b4c3-216">Można również zbyt[Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3b4c3-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="3b4c3-217">Upewnij się, jeśli masz aplikacje działające na maszyn wirtualnych konieczność tooaccess zbyt[Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b4c3-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

