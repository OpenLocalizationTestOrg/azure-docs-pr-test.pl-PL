---
title: "Przekaż obraz niestandardowy Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie i przekazywanie wirtualnego dysku twardego (VHD) na platformie Azure przy użyciu niestandardowego obrazu systemu Linux przy użyciu modelu wdrażania usługi Resource Manager i interfejsu wiersza polecenia platformy Azure w wersji 1.0."
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
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="5c076-103">Przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5c076-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="5c076-104">W tym artykule przedstawiono sposób przekazywania wirtualnego dysku twardego (VHD) na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager i Tworzenie maszyn wirtualnych systemu Linux z tego obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="5c076-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="5c076-105">Ta funkcja pozwala zainstalować i skonfigurować distro Linux do własnych potrzeb, a następnie użyć tego wirtualnego dysku twardego do szybkiego tworzenia maszyn wirtualnych platformy Azure (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="5c076-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5c076-106">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="5c076-106">CLI versions to complete the task</span></span>
<span data-ttu-id="5c076-107">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="5c076-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="5c076-108">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="5c076-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5c076-109">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="5c076-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="5c076-110">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="5c076-110">Quick commands</span></span>
<span data-ttu-id="5c076-111">Jeśli chcesz szybko wykonać zadanie, następujące szczegóły sekcji bazie polecenia do przekazania Maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5c076-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="5c076-112">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#requirements).</span><span class="sxs-lookup"><span data-stu-id="5c076-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="5c076-113">Upewnij się, że masz [1.0 interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="5c076-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5c076-114">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="5c076-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5c076-115">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.</span><span class="sxs-lookup"><span data-stu-id="5c076-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="5c076-116">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="5c076-116">First, create a resource group.</span></span> <span data-ttu-id="5c076-117">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `WestUs` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="5c076-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="5c076-118">Utwórz konto magazynu do przechowywania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5c076-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="5c076-119">Poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="5c076-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="5c076-120">Wyświetl klucze dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5c076-120">List the access keys for your storage account.</span></span> <span data-ttu-id="5c076-121">Zanotuj `key1`:</span><span class="sxs-lookup"><span data-stu-id="5c076-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="5c076-122">Utwórz kontener w ramach konta magazynu przy użyciu klucza magazynu, który został uzyskany.</span><span class="sxs-lookup"><span data-stu-id="5c076-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="5c076-123">Poniższy przykład tworzy kontener o nazwie `myimages` przy użyciu magazynu kluczy wartości `key1`:</span><span class="sxs-lookup"><span data-stu-id="5c076-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="5c076-124">Na koniec należy przekazać dysk VHD do kontenera, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="5c076-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="5c076-125">Określ ścieżkę lokalną na dysk VHD w obszarze `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="5c076-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="5c076-126">Teraz można utworzyć maszyny Wirtualnej z dysku wirtualnego przekazane [przy użyciu szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="5c076-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="5c076-127">Umożliwia także interfejsu wiersza polecenia, określając identyfikator URI do dysku (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="5c076-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="5c076-128">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu dysku wirtualnego wcześniej przekazany:</span><span class="sxs-lookup"><span data-stu-id="5c076-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="5c076-129">Konto magazynu docelowego musi być taka sama jak gdzie przekazany wirtualny dysk.</span><span class="sxs-lookup"><span data-stu-id="5c076-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="5c076-130">Należy również określić lub odpowiedzi, który wyświetla monit o dodatkowe parametry wymagane przez `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="5c076-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="5c076-131">Możesz przeczytać dodatkowe informacje [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="5c076-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="5c076-132">Wymagania</span><span class="sxs-lookup"><span data-stu-id="5c076-132">Requirements</span></span>
<span data-ttu-id="5c076-133">Aby wykonać następujące kroki, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="5c076-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="5c076-134">**Linux zainstalowanego systemu operacyjnego w pliku VHD** -Zainstaluj [dystrybucji zatwierdzone na platformie Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) do dysku wirtualnego w formacie VHD.</span><span class="sxs-lookup"><span data-stu-id="5c076-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="5c076-135">Istnieje wiele narzędzi do tworzenia maszyny Wirtualnej i wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="5c076-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="5c076-136">Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę na w formacie VHD obrazu.</span><span class="sxs-lookup"><span data-stu-id="5c076-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="5c076-137">W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="5c076-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="5c076-138">Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c076-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5c076-139">Nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5c076-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="5c076-140">Podczas tworzenia maszyny Wirtualnej, określ dysk VHD jak format.</span><span class="sxs-lookup"><span data-stu-id="5c076-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="5c076-141">W razie potrzeby możesz przekonwertować dysków VHDX na dysku VHD za pomocą [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c076-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="5c076-142">Ponadto Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, dlatego należy przekonwertować takie dyski wirtualne dyski twarde statycznej przed przekazaniem.</span><span class="sxs-lookup"><span data-stu-id="5c076-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="5c076-143">Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) przekonwertować dyski dynamiczne podczas procesu przekazywania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5c076-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="5c076-144">Maszyny wirtualne utworzone na podstawie niestandardowego obrazu musi znajdować się w tym samym kontem magazynu samego obrazu</span><span class="sxs-lookup"><span data-stu-id="5c076-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="5c076-145">Tworzenie konta magazynu i kontener do przechowywania obu niestandardowego obrazu i utworzone maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="5c076-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="5c076-146">Po utworzeniu wszystkich maszyn wirtualnych, można bezpiecznie usunąć obrazu</span><span class="sxs-lookup"><span data-stu-id="5c076-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="5c076-147">Upewnij się, że masz [1.0 interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="5c076-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5c076-148">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="5c076-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5c076-149">Przykład nazwy parametrów uwzględnione `myResourceGroup`, `mystorageaccount`, i `myimages`.</span><span class="sxs-lookup"><span data-stu-id="5c076-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="5c076-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="5c076-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="5c076-151">Przygotowanie obrazu do załadowania</span><span class="sxs-lookup"><span data-stu-id="5c076-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="5c076-152">Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="5c076-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="5c076-153">Następujące artykuły przedstawiono sposób przygotowania różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="5c076-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="5c076-154">**[Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-155">**[Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5c076-160">**[Inne — niezatwierdzonych dystrybucji](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5c076-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="5c076-161">Zobacz też  **[informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5c076-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5c076-162">[Umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) ma zastosowanie do maszyn wirtualnych z systemem Linux tylko wtedy, gdy jeden z potwierdzony dystrybucji jest używany z szczegóły konfiguracji określone w obsługiwanych wersjach w [systemu Linux na dystrybucje Azure-Endorsed](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c076-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="5c076-163">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5c076-163">Create a resource group</span></span>
<span data-ttu-id="5c076-164">Grupy zasobów logicznie zebranie wszystkich zasobów platformy Azure do obsługi maszyn wirtualnych, takie jak sieci wirtualnych i magazynu.</span><span class="sxs-lookup"><span data-stu-id="5c076-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="5c076-165">Przeczytaj więcej na temat [grupy zasobów platformy Azure, w tym miejscu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c076-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5c076-166">Przed przekazaniem obrazu niestandardowego dysku i Tworzenie maszyn wirtualnych, należy najpierw utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="5c076-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="5c076-167">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="5c076-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5c076-168">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5c076-168">Create a storage account</span></span>
<span data-ttu-id="5c076-169">Maszyny wirtualne są przechowywane jako stronicowe obiekty BLOB w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5c076-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="5c076-170">Przeczytaj więcej na temat [magazynu obiektów blob platformy Azure w tym miejscu](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="5c076-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="5c076-171">Możesz utworzyć konto magazynu obrazu niestandardowego dysku i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5c076-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="5c076-172">Wszystkie maszyny wirtualne utworzone z obrazu niestandardowego dysku muszą być tego samego konta magazynu jako obrazu.</span><span class="sxs-lookup"><span data-stu-id="5c076-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="5c076-173">Poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount` w utworzoną wcześniej grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="5c076-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="5c076-174">Wyświetl klucze konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5c076-174">List storage account keys</span></span>
<span data-ttu-id="5c076-175">Platforma Azure generuje dwa klucze dostępu 512-bitowe dla każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5c076-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="5c076-176">Klawisze dostępu są używane podczas uwierzytelniania na konto magazynu, takich jak do przeprowadzania operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="5c076-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="5c076-177">Przeczytaj więcej na temat [zarządzanie dostępem do magazynu w tym miejscu](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5c076-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="5c076-178">Możesz wyświetlić klawisze dostępu z `azure storage account keys list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c076-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="5c076-179">Wyświetl klucze dostępu dla konta magazynu utworzone:</span><span class="sxs-lookup"><span data-stu-id="5c076-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="5c076-180">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="5c076-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="5c076-181">Zanotuj `key1` jako użyje do interakcji z konta magazynu w następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="5c076-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="5c076-182">Tworzenie kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="5c076-182">Create a storage container</span></span>
<span data-ttu-id="5c076-183">W taki sam sposób jak utworzyć różne katalogów w celu logicznego uporządkowania lokalnego systemu plików możesz utworzyć kontenery w ramach konta magazynu, aby organizować dyski wirtualne i obrazów.</span><span class="sxs-lookup"><span data-stu-id="5c076-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="5c076-184">Konto magazynu może zawierać dowolną liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="5c076-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="5c076-185">Poniższy przykład tworzy kontener o nazwie `myimages`, określania klucza dostępu uzyskanych w poprzednim kroku (`key1`):</span><span class="sxs-lookup"><span data-stu-id="5c076-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="5c076-186">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="5c076-186">Upload VHD</span></span>
<span data-ttu-id="5c076-187">Teraz można faktycznie przekazywanie obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="5c076-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="5c076-188">Jako wszystkich wirtualnych dysków używanych przez maszyny wirtualne, należy przekazać i przechowywania obrazu niestandardowego dysku jako stronicowy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="5c076-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="5c076-189">Określ klucz dostępu do kontenera, który został utworzony w poprzednim kroku, a następnie ścieżkę do obrazu niestandardowego dysku na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="5c076-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="5c076-190">Tworzenie maszyny Wirtualnej z obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="5c076-190">Create VM from custom image</span></span>
<span data-ttu-id="5c076-191">Podczas tworzenia maszyn wirtualnych z obrazu niestandardowego dysku, należy określić identyfikator URI do obrazu dysku.</span><span class="sxs-lookup"><span data-stu-id="5c076-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="5c076-192">Upewnij się, że zgodne konto magazynu docelowego przechowywania obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="5c076-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="5c076-193">Można utworzyć maszyny Wirtualnej przy użyciu szablonu Azure CLI lub JSON Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="5c076-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="5c076-194">Utwórz maszynę Wirtualną przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5c076-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="5c076-195">Należy określić `--image-urn` parametr `azure vm create` polecenie, aby wskazywał obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="5c076-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="5c076-196">Upewnij się, że `--storage-account-name` zgodne z kontem magazynu przechowywania obrazu niestandardowego dysku.</span><span class="sxs-lookup"><span data-stu-id="5c076-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="5c076-197">Nie trzeba używać tego samego kontenera jako obraz niestandardowy dysku do przechowywania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5c076-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="5c076-198">Upewnij się utworzyć wszelkie dodatkowe kontenery w taki sam sposób jak w poprzednich krokach przed przekazaniem dysku niestandardowych obrazów.</span><span class="sxs-lookup"><span data-stu-id="5c076-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="5c076-199">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` z obrazu niestandardowego dysku:</span><span class="sxs-lookup"><span data-stu-id="5c076-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="5c076-200">Należy określić nadal lub odpowiedzi, który wyświetla monit o dodatkowe parametry wymagane przez `azure vm create` polecenia, takich jak sieć wirtualną, publiczny adres IP, nazwę użytkownika i kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="5c076-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="5c076-201">Przeczytaj więcej na temat [dostępne parametry interfejsu wiersza polecenia Menedżera zasobów](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="5c076-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="5c076-202">Utwórz maszynę Wirtualną przy użyciu szablonu JSON</span><span class="sxs-lookup"><span data-stu-id="5c076-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="5c076-203">Szablony usługi Azure Resource Manager są plików JavaScript Object Notation (JSON), które definiują środowiska, które chcesz skompilować.</span><span class="sxs-lookup"><span data-stu-id="5c076-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="5c076-204">Szablony są dzielone w dół dostawców różnych zasobów, takich jak obliczeń lub sieci.</span><span class="sxs-lookup"><span data-stu-id="5c076-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="5c076-205">Możesz użyć istniejących szablonów lub napisać własny.</span><span class="sxs-lookup"><span data-stu-id="5c076-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="5c076-206">Przeczytaj więcej na temat [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c076-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="5c076-207">W ramach `Microsoft.Compute/virtualMachines` dostawcy szablonu, masz `storageProfile` węzła, który zawiera szczegóły konfiguracji dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5c076-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="5c076-208">Są dwa parametry głównym, aby edytować `image` i `vhd` identyfikatorów URI wskaż obrazu niestandardowego dysku i dysk wirtualny nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5c076-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="5c076-209">Poniżej przedstawiono przykład JSON dla przy użyciu obrazu niestandardowego dysku:</span><span class="sxs-lookup"><span data-stu-id="5c076-209">The following shows an example of the JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="5c076-210">Można użyć [tego istniejącego szablonu, aby utworzyć Maszynę wirtualną z obrazu niestandardowego](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) lub przeczytaj o [Tworzenie szablonów usługi Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5c076-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="5c076-211">Po utworzeniu szablonu skonfigurowanego tworzenia maszyn wirtualnych przy użyciu `azure group deployment create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c076-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="5c076-212">Określ identyfikator URI szablonu JSON z `--template-uri` parametru:</span><span class="sxs-lookup"><span data-stu-id="5c076-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="5c076-213">Jeśli masz plik JSON przechowywane lokalnie na komputerze, możesz użyć `--template-file` parametru zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="5c076-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="5c076-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c076-214">Next steps</span></span>
<span data-ttu-id="5c076-215">Po przygotowane i przekazać niestandardowe dysku wirtualnego, można uzyskać więcej informacji [przy użyciu usługi Resource Manager i szablonów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c076-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5c076-216">Warto również [Dodaj dysk danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) do nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5c076-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="5c076-217">Jeśli masz aplikacje działające na które należy uzyskać dostęp do maszyn wirtualnych, należy koniecznie [Otwórz porty i punkty końcowe](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c076-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

