---
title: "aaaCreate i przekazywanie maszyny Wirtualnej obrazu przy użyciu programu Powershell | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate i przekaż uogólniony obraz systemu Windows Server (VHD) przy użyciu hello klasycznego modelu wdrażania i programu Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="e0962-103">Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego z systemem Windows Server</span><span class="sxs-lookup"><span data-stu-id="e0962-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="e0962-104">W tym artykule opisano, jak tooupload własne uogólniony maszyny Wirtualnej obrazu jako wirtualny dysk twardy (VHD), można użyć toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e0962-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="e0962-105">Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde w systemie Microsoft Azure, zobacz [o dyski i wirtualne dyski twarde dla maszyn wirtualnych](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0962-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0962-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e0962-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e0962-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="e0962-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e0962-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0962-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e0962-109">Możesz również [przekazać](../upload-generalized-managed.md) maszyny wirtualnej z wykorzystaniem hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0962-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0962-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e0962-110">Prerequisites</span></span>
<span data-ttu-id="e0962-111">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="e0962-111">This article assumes you have:</span></span>

* <span data-ttu-id="e0962-112">**Subskrypcja platformy Azure** — Jeśli nie masz, możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e0962-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="e0962-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -masz hello Microsoft Azure PowerShell modułu zainstalowany i skonfigurowany toouse subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0962-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="e0962-114">**A. Plik VHD** — obsługiwane systemu operacyjnego przechowywanego w pliku VHD i maszyny wirtualnej podłączone tooa Windows.</span><span class="sxs-lookup"><span data-stu-id="e0962-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="e0962-115">Określ, czy toosee hello ról serwera uruchomionych na powitania wirtualnego dysku twardego są obsługiwane przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e0962-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="e0962-116">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="e0962-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e0962-117">Hello VHDX format nie jest obsługiwany w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e0962-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="e0962-118">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello [polecenia cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0962-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="e0962-119">Aby uzyskać więcej informacji, zobacz [wpis w blogu](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0962-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="e0962-120">Krok 1: Przygotowywanie hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e0962-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="e0962-121">Przed przekazaniem hello tooAzure wirtualnego dysku twardego, musi on toobe uogólniony przy użyciu narzędzia Sysprep hello.</span><span class="sxs-lookup"><span data-stu-id="e0962-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="e0962-122">— Przygotowanie toobe wirtualnego dysku twardego hello użyty jako obraz.</span><span class="sxs-lookup"><span data-stu-id="e0962-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="e0962-123">Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0962-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="e0962-124">Utwórz kopię zapasową hello maszyny Wirtualnej przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e0962-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="e0962-125">Aby ukończyć powitalnych procedury został zainstalowany z hello maszyny wirtualnej, która hello systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="e0962-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="e0962-126">Zaloguj się toohello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e0962-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="e0962-127">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="e0962-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="e0962-128">Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="e0962-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Otwórz okno wiersza polecenia](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="e0962-130">Witaj **narzędzie przygotowania systemu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e0962-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Uruchom program Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="e0962-132">W hello **narzędzie przygotowania systemu**, wybierz pozycję **wprowadź systemu poza środowisko pola (OOBE)** i upewnij się, że **Generalize** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="e0962-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="e0962-133">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="e0962-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="e0962-134">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0962-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="e0962-135">Krok 2: Tworzenie konta magazynu i kontener</span><span class="sxs-lookup"><span data-stu-id="e0962-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="e0962-136">Należy konto magazynu na platformie Azure, więc plik VHD hello tooupload miejsce.</span><span class="sxs-lookup"><span data-stu-id="e0962-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="e0962-137">W tym kroku przedstawiono sposób toocreate konta lub get hello informacje z istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="e0962-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="e0962-138">Zastąp zmienne hello w &lsaquo; nawiasy &rsaquo; odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="e0962-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="e0962-139">Login</span><span class="sxs-lookup"><span data-stu-id="e0962-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="e0962-140">Ustaw subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0962-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="e0962-141">Utwórz nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e0962-141">Create a new storage account.</span></span> <span data-ttu-id="e0962-142">Nazwa Hello hello konta magazynu powinna być unikatowa, 3 do 24 znaków.</span><span class="sxs-lookup"><span data-stu-id="e0962-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="e0962-143">Nazwa Hello może być dowolną kombinacją liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="e0962-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="e0962-144">Należy również toospecify lokalizacji, takiej jak "Wschód nam"</span><span class="sxs-lookup"><span data-stu-id="e0962-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="e0962-145">Ustaw nowe konto magazynu hello jako domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="e0962-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="e0962-146">Utwórz nowy kontener.</span><span class="sxs-lookup"><span data-stu-id="e0962-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="e0962-147">Krok 3: Przekaż plik VHD hello</span><span class="sxs-lookup"><span data-stu-id="e0962-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="e0962-148">Użyj hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e0962-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="e0962-149">Z okna programu Azure PowerShell hello używany w poprzednim kroku hello, typ hello następujące polecenie i Zastąp zmienne hello w &lsaquo; nawiasy &rsaquo; odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="e0962-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="e0962-150">Krok 4: Dodawanie listy tooyour obrazów hello niestandardowych obrazów</span><span class="sxs-lookup"><span data-stu-id="e0962-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="e0962-151">Użyj hello [AzureVMImage Dodaj](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) polecenia cmdlet tooadd hello obrazu toohello listy obrazów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e0962-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="e0962-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0962-152">Next steps</span></span>
<span data-ttu-id="e0962-153">Możesz teraz [Tworzenie niestandardowych maszyny Wirtualnej](createportal.md) przy użyciu hello można przekazać obrazu.</span><span class="sxs-lookup"><span data-stu-id="e0962-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
