---
title: aaaDownload dysku VHD systemu Windows z platformy Azure | Dokumentacja firmy Microsoft
description: "Pobierz dysku VHD systemu Windows przy użyciu hello portalu Azure."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="3b0c4-103">Pobierz zestaw Windows wirtualnego dysku twardego z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b0c4-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="3b0c4-104">W tym artykule dowiesz się, jak toodownload [Windows wirtualnego dysku twardego (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pliku z platformy Azure przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="3b0c4-105">Maszynach wirtualnych (VM) platformy Azure używana [dysków](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) jako toostore miejscu systemu operacyjnego, aplikacje i dane.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="3b0c4-106">Wszystkie maszyny wirtualne Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="3b0c4-107">dysk systemu operacyjnego Hello został początkowo utworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są przechowywane na koncie magazynu Azure wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="3b0c4-108">Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="3b0c4-109">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3b0c4-109">Stop hello VM</span></span>

<span data-ttu-id="3b0c4-110">Nie można pobrać wirtualnego dysku twardego z platformy Azure, jeśli jest dołączona tooa uruchamiania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="3b0c4-111">Należy toostop hello wirtualna toodownload dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="3b0c4-112">Jeśli chcesz toouse wirtualnego dysku twardego [obrazu](tutorial-custom-images.md) toocreate innych maszyn wirtualnych o nowe dyski, użyj [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello systemu operacyjnego znajdującego się w pliku hello, a następnie zatrzymać hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="3b0c4-113">Witaj toouse wirtualnego dysku twardego jako dysk nowe wystąpienie klasy istniejącej maszyny Wirtualnej lub dysku danych, należy tylko toostop i deallocate hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="3b0c4-114">toouse hello jako toocreate obrazu wirtualnego dysku twardego innych maszyn wirtualnych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3b0c4-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="3b0c4-115">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b0c4-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="3b0c4-116">[Połącz toohello wirtualna](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b0c4-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="3b0c4-117">Na powitania maszyny Wirtualnej Otwórz okno wiersza polecenia hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="3b0c4-118">Zmień katalog hello zbyt*%windir%\system32\sysprep* i uruchom sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="3b0c4-119">Okno dialogowe narzędzia przygotowywania systemu hello, wybierz **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="3b0c4-120">Wybierz opcje zamykania **zamknięcia**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="3b0c4-121">toouse hello wirtualny dysk twardy jako dysk dla nowego wystąpienia istniejącej maszyny Wirtualnej lub dysku danych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3b0c4-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="3b0c4-122">W menu Centrum hello w hello portalu Azure kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="3b0c4-123">Wybierz hello maszyny Wirtualnej z listy hello.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="3b0c4-124">W bloku hello hello maszyny Wirtualnej, kliknij **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Zatrzymanie maszyny Wirtualnej](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="3b0c4-126">Generowania adresu URL SAS</span><span class="sxs-lookup"><span data-stu-id="3b0c4-126">Generate SAS URL</span></span>

<span data-ttu-id="3b0c4-127">toodownload hello pliku VHD, należy toogenerate [sygnatury dostępu współdzielonego (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="3b0c4-128">Podczas generowania adresu URL hello czas wygaśnięcia jest przypisany toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="3b0c4-129">W menu hello hello bloku hello maszyny Wirtualnej, kliknij polecenie **dysków**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="3b0c4-130">Wybierz dysk systemu operacyjnego hello hello maszyny Wirtualnej, a następnie kliknij przycisk **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="3b0c4-131">Ustawianie czasu wygaśnięcia hello hello adresu URL za*36000*.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="3b0c4-132">Kliknij przycisk **generowania adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-132">Click **Generate URL**.</span></span>

    ![Generowania adresu URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="3b0c4-134">czas wygaśnięcia Hello jest zwiększona z tooprovide domyślne hello wystarczająco dużo czasu toodownload hello dużego pliku wirtualnego dysku twardego systemu operacyjnego Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="3b0c4-135">Można oczekiwać, że plik wirtualnego dysku twardego, który zawiera tootake systemu operacyjnego Windows Server hello kilka toodownload godzin w zależności od połączenia.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="3b0c4-136">Jeśli pobierasz dysku VHD dla dysku danych hello domyślny czas jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="3b0c4-137">Pobierz wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="3b0c4-137">Download VHD</span></span>

1.  <span data-ttu-id="3b0c4-138">W obszarze hello adres URL, który został wygenerowany kliknij plik VHD hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Pobierz wirtualnego dysku twardego](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="3b0c4-140">Może być konieczne tooclick **zapisać** w hello przeglądarki toostart hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="3b0c4-141">Domyślna nazwa pliku VHD hello Hello jest *abcd*.</span><span class="sxs-lookup"><span data-stu-id="3b0c4-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Kliknij przycisk Zapisz w przeglądarce hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="3b0c4-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b0c4-143">Next steps</span></span>

- <span data-ttu-id="3b0c4-144">Dowiedz się, jak za[przekazać tooAzure pliku wirtualnego dysku twardego](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b0c4-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="3b0c4-145">[Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b0c4-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="3b0c4-146">[Zarządzanie dyskami Azure przy użyciu programu PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b0c4-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

