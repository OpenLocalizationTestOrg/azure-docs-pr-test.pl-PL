---
title: Pobierz dysku VHD systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Pobierz dysku VHD systemu Linux przy użyciu wiersza polecenia platformy Azure i portalu Azure."
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="c48f4-103">Pobierz dysku VHD systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c48f4-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="c48f4-104">W tym artykule opisano sposób pobierania [Linux wirtualnego dysku twardego (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pliku z platformy Azure przy użyciu wiersza polecenia platformy Azure i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c48f4-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="c48f4-105">Maszynach wirtualnych (VM) platformy Azure używana [dysków](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) jako miejsce do przechowywania systemu operacyjnego, aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="c48f4-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="c48f4-106">Wszystkie maszyny wirtualne Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="c48f4-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="c48f4-107">Dysk systemu operacyjnego został początkowo utworzony z obrazu, a zarówno dysku systemu operacyjnego i obrazu są przechowywane na koncie magazynu Azure wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="c48f4-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="c48f4-108">Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="c48f4-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="c48f4-109">Jeśli jeszcze tego nie zrobiono, zainstaluj [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c48f4-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="c48f4-110">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c48f4-110">Stop the VM</span></span>

<span data-ttu-id="c48f4-111">Nie można pobrać wirtualnego dysku twardego z platformy Azure, jeśli jest podłączony do uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c48f4-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="c48f4-112">Należy zatrzymać maszynę Wirtualną do pobrania dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="c48f4-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="c48f4-113">Jeśli chcesz użyć wirtualnego dysku twardego [obrazu](tutorial-custom-images.md) Aby utworzyć pozostałe maszyny wirtualne o nowe dyski, należy anulowanie zastrzeżenia i uogólnienia systemu operacyjnego znajdującego się w pliku i Zatrzymaj maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c48f4-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="c48f4-114">Do użycia jako dysk wirtualny dysk twardy nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, wystarczy zatrzymać i cofnięcia przydzielenia Maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c48f4-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="c48f4-115">Aby użyć wirtualnego dysku twardego jako obraz do tworzenia innych maszyn wirtualnych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c48f4-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="c48f4-116">Aby podłączyć się do niego i anulowanie zastrzeżenia go, należy użyć SSH, nazwę konta i publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c48f4-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="c48f4-117">+ Parametr użytkownika spowoduje również usunięcie ostatniego elastycznie konta.</span><span class="sxs-lookup"><span data-stu-id="c48f4-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="c48f4-118">Jeśli poświadczenia konta w celu maszyny Wirtualnej są pieczenia, Opuść to + parametr użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c48f4-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="c48f4-119">Poniższy przykład umożliwia usunięcie ostatniego elastycznie konta:</span><span class="sxs-lookup"><span data-stu-id="c48f4-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="c48f4-120">Zaloguj się do konta platformy Azure z [logowania az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c48f4-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="c48f4-121">Zatrzymaj i cofnięcia przydzielenia Maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c48f4-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="c48f4-122">Generalize maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c48f4-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="c48f4-123">Do użycia jako dysk wirtualny dysk twardy nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c48f4-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="c48f4-124">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c48f4-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="c48f4-125">W menu Centrum kliknij pozycję **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="c48f4-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="c48f4-126">Wybierz maszynę Wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="c48f4-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="c48f4-127">W bloku maszyny Wirtualnej, kliknij przycisk **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="c48f4-127">On the blade for the VM, click **Stop**.</span></span>

    ![Zatrzymanie maszyny Wirtualnej](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="c48f4-129">Generowania adresu URL SAS</span><span class="sxs-lookup"><span data-stu-id="c48f4-129">Generate SAS URL</span></span>

<span data-ttu-id="c48f4-130">Aby pobrać plik wirtualnego dysku twardego, należy wygenerować [sygnatury dostępu współdzielonego (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c48f4-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="c48f4-131">Podczas generowania adresu URL czas wygaśnięcia jest przypisana do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c48f4-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="c48f4-132">W menu bloku dla maszyny Wirtualnej, kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="c48f4-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="c48f4-133">Wybierz dysk systemu operacyjnego dla maszyny Wirtualnej, a następnie kliknij przycisk **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="c48f4-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="c48f4-134">Kliknij przycisk **generowania adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="c48f4-134">Click **Generate URL**.</span></span>

    ![Generowania adresu URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="c48f4-136">Pobierz wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="c48f4-136">Download VHD</span></span>

1.  <span data-ttu-id="c48f4-137">Pod adresem URL, który został wygenerowany kliknij przycisk Pobierz plik VHD.</span><span class="sxs-lookup"><span data-stu-id="c48f4-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Pobierz wirtualnego dysku twardego](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="c48f4-139">Może zajść potrzeba kliknięcia przycisku **zapisać** w przeglądarce, aby rozpocząć pobieranie.</span><span class="sxs-lookup"><span data-stu-id="c48f4-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="c48f4-140">Domyślna nazwa pliku VHD jest *abcd*.</span><span class="sxs-lookup"><span data-stu-id="c48f4-140">The default name for the VHD file is *abcd*.</span></span>

    ![Kliknij przycisk Zapisz w przeglądarce](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="c48f4-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c48f4-142">Next steps</span></span>

- <span data-ttu-id="c48f4-143">Dowiedz się, jak [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie niestandardowych dysku 2.0 interfejsu wiersza polecenia Azure](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c48f4-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="c48f4-144">[Zarządzanie dyskami Azure, Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c48f4-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

