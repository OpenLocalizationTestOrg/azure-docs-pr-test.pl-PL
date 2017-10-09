---
title: "aaaCreate i przekazać tooAzure dysku VHD systemu Linux | Dokumentacja firmy Microsoft"
description: "Tworzenie i przekazywanie Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Linux hello przy użyciu klasycznego modelu wdrożenia hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="d115d-103">Tworzenie i przekazywanie wirtualnego dysku twardego zawierający hello System operacyjny Linux</span><span class="sxs-lookup"><span data-stu-id="d115d-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d115d-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d115d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d115d-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="d115d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d115d-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d115d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d115d-107">Możesz również [Przekaż obraz niestandardowy dysku przy użyciu usługi Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d115d-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d115d-108">W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD), dzięki czemu można używać jako własnego obrazu toocreate maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d115d-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="d115d-109">Dowiedz się, jak tooprepare hello systemu operacyjnego, można użyć toocreate wiele maszyn wirtualnych na podstawie obrazu.</span><span class="sxs-lookup"><span data-stu-id="d115d-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="d115d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d115d-110">Prerequisites</span></span>
<span data-ttu-id="d115d-111">W tym artykule założono, że hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d115d-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="d115d-112">**Linux zainstalowanego systemu operacyjnego w pliku VHD** — zainstalowano [dystrybucji Linux zatwierdzone na platformie Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (lub zobacz [informacje dotyczące niezatwierdzonych dystrybucji](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa dysku wirtualnego w formacie VHD hello.</span><span class="sxs-lookup"><span data-stu-id="d115d-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="d115d-113">Wiele narzędzi istnieje toocreate maszyny Wirtualnej i wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="d115d-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="d115d-114">Instalowanie i konfigurowanie [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) lub [KVM](http://www.linux-kvm.org/page/RunningKVM), zwracając szczególną uwagę toouse wirtualnego dysku twardego jako formatu obrazu.</span><span class="sxs-lookup"><span data-stu-id="d115d-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="d115d-115">W razie potrzeby można [Konwertuj obraz](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) przy użyciu `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="d115d-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="d115d-116">Można także użyć funkcji Hyper-V [w systemie Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) lub [w systemie Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d115d-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d115d-117">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d115d-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="d115d-118">Podczas tworzenia maszyny Wirtualnej, określ dysk VHD formacie hello.</span><span class="sxs-lookup"><span data-stu-id="d115d-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="d115d-119">W razie potrzeby można przekonwertować przy użyciu tooVHD dysków VHDX [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) lub hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d115d-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="d115d-120">Co więcej Azure nie obsługuje przekazywania dynamicznych wirtualnych dysków twardych, w związku z czym należy tooconvert takich toostatic dyski wirtualne dyski twarde przed przesłaniem.</span><span class="sxs-lookup"><span data-stu-id="d115d-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="d115d-121">Można użyć narzędzia, takie jak [Azure dysk VHD narzędzia dla Przejdź](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dysków dynamicznych podczas procesu przekazywania tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="d115d-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="d115d-122">**Interfejs wiersza polecenia platformy Azure** — najnowsza wersja hello instalacji [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="d115d-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="d115d-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="d115d-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="d115d-124">Krok 1: Przygotowanie toobe obraz powitania przekazany</span><span class="sxs-lookup"><span data-stu-id="d115d-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="d115d-125">Azure obsługuje różne dystrybucje systemu Linux (zobacz [dystrybucje zatwierdzone](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="d115d-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="d115d-126">Hello następujące artykuły przedstawiono sposób tooprepare hello różnych dystrybucje systemu Linux, które są obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d115d-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="d115d-127">Po wykonaniu kroków hello powitania po przewodnikach potem wróć tutaj po utworzeniu pliku wirtualnego dysku twardego, który jest gotowy tooupload tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d115d-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="d115d-128">**[Na podstawie centOS dystrybucji](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-129">**[Debian systemu Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d115d-134">**[Inne — niezatwierdzonych dystrybucji](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d115d-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="d115d-135">Witaj umowy SLA platformy Azure stosuje toovirtual maszynami hello używany w hello szczegóły konfiguracji określone w obsługiwanych wersjach systemu operacyjnego Linux tylko wtedy, gdy jeden z hello dystrybucje zatwierdzone [systemu Linux na Azure-Endorsed dystrybucji ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d115d-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d115d-136">Wszystkie dystrybucje systemu Linux w galerii Azure obrazu hello są potwierdzony dystrybucje z hello wymaganej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d115d-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="d115d-137">Zobacz też hello  **[informacje o instalacji systemu Linux](../create-upload-generic.md#general-linux-installation-notes)**  bardziej ogólne porady dotyczące przygotowywania obrazów systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d115d-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="d115d-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="d115d-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="d115d-139">Krok 2: Przygotowanie hello tooAzure połączenia</span><span class="sxs-lookup"><span data-stu-id="d115d-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="d115d-140">Upewnij się, że używasz hello Azure CLI w hello klasycznego modelu wdrażania (`azure config mode asm`), następnie zalogowanie się na koncie tooyour:</span><span class="sxs-lookup"><span data-stu-id="d115d-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="d115d-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="d115d-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="d115d-142">Krok 3: Przekaż hello tooAzure obrazu</span><span class="sxs-lookup"><span data-stu-id="d115d-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="d115d-143">Należy tooupload konta magazynu w pliku wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="d115d-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="d115d-144">Albo można wybrać istniejące konto magazynu lub [Utwórz nową](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d115d-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="d115d-145">Użyj hello Azure CLI tooupload hello obrazu przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d115d-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="d115d-146">W poprzednim przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="d115d-146">In hello previous example:</span></span>

* <span data-ttu-id="d115d-147">**BlobStorageURL** jest adres URL hello hello konta magazynu, Zaplanuj toouse</span><span class="sxs-lookup"><span data-stu-id="d115d-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="d115d-148">**YourImagesFolder** jest hello kontenera w magazynie obiektów blob w miejscu toostore obrazów</span><span class="sxs-lookup"><span data-stu-id="d115d-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="d115d-149">**VHDName** jest hello etykietą, która jest wyświetlana w portalu tooidentify hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="d115d-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="d115d-150">**PathToVHDFile** jest hello Pełna ścieżka i nazwa pliku VHD hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d115d-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="d115d-151">następujące polecenie Hello przedstawia pełny przykład:</span><span class="sxs-lookup"><span data-stu-id="d115d-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="d115d-152">Krok 4: Tworzenie maszyny Wirtualnej z obrazu hello</span><span class="sxs-lookup"><span data-stu-id="d115d-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="d115d-153">Możesz utworzyć maszynę Wirtualną przy użyciu `azure vm create` w hello sam sposób jak regularne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d115d-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="d115d-154">Określ nazwę hello obrazu należy nadać hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="d115d-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="d115d-155">W hello poniższy przykład, używamy hello **myImage** podany w poprzednim kroku hello nazwa obrazu:</span><span class="sxs-lookup"><span data-stu-id="d115d-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="d115d-156">toocreate własnych maszyn wirtualnych, podać własne nazwy użytkownika + hasła, lokalizację, nazwy DNS i nazwa obrazu.</span><span class="sxs-lookup"><span data-stu-id="d115d-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d115d-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d115d-157">Next steps</span></span>
<span data-ttu-id="d115d-158">Aby uzyskać więcej informacji, zobacz [odwołania wiersza polecenia platformy Azure dla hello Azure klasycznego modelu wdrażania](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d115d-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
