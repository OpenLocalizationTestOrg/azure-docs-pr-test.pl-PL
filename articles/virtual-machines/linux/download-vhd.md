---
title: aaaDownload dysku VHD systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Pobierz dysku VHD systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello i hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="1e572-103">Pobierz dysku VHD systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1e572-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="1e572-104">W tym artykule dowiesz się, jak toodownload [Linux wirtualnego dysku twardego (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello pliku z platformy Azure przy użyciu wiersza polecenia platformy Azure i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e572-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="1e572-105">Maszynach wirtualnych (VM) platformy Azure używana [dysków](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) jako toostore miejscu systemu operacyjnego, aplikacje i dane.</span><span class="sxs-lookup"><span data-stu-id="1e572-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="1e572-106">Wszystkie maszyny wirtualne Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="1e572-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="1e572-107">dysk systemu operacyjnego Hello został początkowo utworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są przechowywane na koncie magazynu Azure wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="1e572-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="1e572-108">Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="1e572-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="1e572-109">Jeśli jeszcze tego nie zrobiono, zainstaluj [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="1e572-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="1e572-110">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1e572-110">Stop hello VM</span></span>

<span data-ttu-id="1e572-111">Nie można pobrać wirtualnego dysku twardego z platformy Azure, jeśli jest dołączona tooa uruchamiania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1e572-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="1e572-112">Należy toostop hello wirtualna toodownload dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="1e572-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="1e572-113">Jeśli chcesz toouse wirtualnego dysku twardego [obrazu](tutorial-custom-images.md) toocreate innych maszyn wirtualnych o nowe dyski, należy toodeprovision i uogólnienia systemu operacyjnego hello zawarte w hello plików i Zatrzymaj hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1e572-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="1e572-114">Witaj toouse wirtualnego dysku twardego jako dysk nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, należy tylko toostop i deallocate hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1e572-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="1e572-115">toouse hello jako toocreate obrazu wirtualnego dysku twardego innych maszyn wirtualnych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1e572-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="1e572-116">Użyj SSH, nazwa konta hello i hello publicznego adresu IP hello wirtualna tooconnect tooit i anulowanie zastrzeżenia go.</span><span class="sxs-lookup"><span data-stu-id="1e572-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="1e572-117">Witaj + użytkownika parametru spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie.</span><span class="sxs-lookup"><span data-stu-id="1e572-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="1e572-118">Jeśli poświadczenia konta w toohello maszyny Wirtualnej są pieczenia, Opuść to + parametr użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e572-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="1e572-119">Witaj poniższy przykład umożliwia usunięcie ostatnie konto użytkownika elastycznie hello:</span><span class="sxs-lookup"><span data-stu-id="1e572-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="1e572-120">Zaloguj się tooyour konto platformy Azure z [logowania az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1e572-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="1e572-121">Zatrzymaj i cofnięcia przydzielenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1e572-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1e572-122">Generalize hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1e572-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="1e572-123">toouse hello wirtualny dysk twardy jako dysk dla nowego wystąpienia istniejącej maszyny Wirtualnej lub dysku danych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1e572-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="1e572-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e572-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="1e572-125">W menu Centrum powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="1e572-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="1e572-126">Wybierz hello maszyny Wirtualnej z listy hello.</span><span class="sxs-lookup"><span data-stu-id="1e572-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="1e572-127">W bloku hello hello maszyny Wirtualnej, kliknij **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="1e572-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Zatrzymanie maszyny Wirtualnej](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="1e572-129">Generowania adresu URL SAS</span><span class="sxs-lookup"><span data-stu-id="1e572-129">Generate SAS URL</span></span>

<span data-ttu-id="1e572-130">toodownload hello pliku VHD, należy toogenerate [sygnatury dostępu współdzielonego (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1e572-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="1e572-131">Podczas generowania adresu URL hello czas wygaśnięcia jest przypisany toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1e572-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="1e572-132">W menu hello hello bloku hello maszyny Wirtualnej, kliknij polecenie **dysków**.</span><span class="sxs-lookup"><span data-stu-id="1e572-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="1e572-133">Wybierz dysk systemu operacyjnego hello hello maszyny Wirtualnej, a następnie kliknij przycisk **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="1e572-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="1e572-134">Kliknij przycisk **generowania adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="1e572-134">Click **Generate URL**.</span></span>

    ![Generowania adresu URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="1e572-136">Pobierz wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="1e572-136">Download VHD</span></span>

1.  <span data-ttu-id="1e572-137">W obszarze hello adres URL, który został wygenerowany kliknij plik VHD hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="1e572-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Pobierz wirtualnego dysku twardego](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="1e572-139">Może być konieczne tooclick **zapisać** w hello przeglądarki toostart hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="1e572-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="1e572-140">Domyślna nazwa pliku VHD hello Hello jest *abcd*.</span><span class="sxs-lookup"><span data-stu-id="1e572-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Kliknij przycisk Zapisz w przeglądarce hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="1e572-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e572-142">Next steps</span></span>

- <span data-ttu-id="1e572-143">Dowiedz się, jak za[przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku z hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e572-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="1e572-144">[Zarządzanie hello Azure dysków Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e572-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

