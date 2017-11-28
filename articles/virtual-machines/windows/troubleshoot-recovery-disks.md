---
title: "aaaUse a Windows Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak problemy tootroubleshoot maszyny Wirtualnej systemu Windows na platformie Azure, łącząc tooa odzyskiwanie hello systemu operacyjnego maszyny Wirtualnej przy użyciu programu Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="ad119-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Windows, dołączając tooa odzyskiwanie hello systemu operacyjnego maszyny Wirtualnej przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad119-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="ad119-104">Jeśli maszyny wirtualnej systemu Windows (VM) na platformie Azure napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ad119-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="ad119-105">Typowym przykładem jest aktualizację aplikacji, która uniemożliwia hello maszyna wirtualna stanie tooboot pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ad119-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="ad119-106">Ten sposób artykuł szczegóły toouse tooconnect programu Azure PowerShell toofix maszyny Wirtualnej systemu Windows tooanother Twojego wirtualnego dysku twardego wszelkie błędy, następnie utworzyć je ponownie oryginalnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="ad119-107">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="ad119-107">Recovery process overview</span></span>
<span data-ttu-id="ad119-108">proces rozwiązywania problemów Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="ad119-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="ad119-109">Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="ad119-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="ad119-110">Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Windows na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ad119-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="ad119-111">Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="ad119-112">Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="ad119-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="ad119-113">Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="ad119-114">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="ad119-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="ad119-115">Upewnij się, że masz [hello najnowsze programu Azure PowerShell](/powershell/azure/overview) zainstalowane i zarejestrowane w ramach subskrypcji tooyour:</span><span class="sxs-lookup"><span data-stu-id="ad119-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="ad119-116">Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="ad119-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="ad119-117">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="ad119-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="ad119-118">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="ad119-118">Determine boot issues</span></span>
<span data-ttu-id="ad119-119">Zrzut ekranu maszyny wirtualnej można wyświetlić na platformie Azure toohelp rozwiązywania problemów z rozruchem.</span><span class="sxs-lookup"><span data-stu-id="ad119-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="ad119-120">Ten zrzut ekranu może ułatwić zidentyfikowanie przyczyny maszyny Wirtualnej nie powiedzie się tooboot.</span><span class="sxs-lookup"><span data-stu-id="ad119-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="ad119-121">Witaj poniższy przykład pobiera hello zrzut ekranu z hello maszyny Wirtualnej systemu Windows o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="ad119-122">Dlaczego hello maszyny Wirtualnej nie może wykonać tooboot toodetermine zrzut ekranu hello przeglądu.</span><span class="sxs-lookup"><span data-stu-id="ad119-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="ad119-123">Należy pamiętać, wszystkie określone komunikaty o błędach lub podać kody błędów.</span><span class="sxs-lookup"><span data-stu-id="ad119-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="ad119-124">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="ad119-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="ad119-125">Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="ad119-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="ad119-126">Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ad119-127">Wyszukaj `Vhd URI` w hello `StorageProfile` sekcji z danych wyjściowych hello hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad119-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="ad119-128">Witaj skróconą przykładowe dane wyjściowe wyglądają następująco hello `Vhd URI` końcowej hello hello blok kodu:</span><span class="sxs-lookup"><span data-stu-id="ad119-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="ad119-129">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="ad119-129">Delete existing VM</span></span>
<span data-ttu-id="ad119-130">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ad119-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="ad119-131">Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="ad119-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="ad119-132">Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="ad119-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="ad119-133">Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="ad119-134">Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="ad119-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="ad119-135">dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="ad119-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="ad119-136">pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie.</span><span class="sxs-lookup"><span data-stu-id="ad119-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="ad119-137">Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="ad119-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="ad119-138">Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.</span><span class="sxs-lookup"><span data-stu-id="ad119-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="ad119-139">powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="ad119-140">Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="ad119-141">dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="ad119-142">Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ad119-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="ad119-143">Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ad119-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="ad119-144">Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku.</span><span class="sxs-lookup"><span data-stu-id="ad119-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="ad119-145">Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np.</span><span class="sxs-lookup"><span data-stu-id="ad119-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="ad119-146">Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ad119-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="ad119-147">Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello adres URL hello uzyskanych w poprzednim hello `Get-AzureRmVM` polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad119-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="ad119-148">Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="ad119-149">Dodawanie dysku wymaga toospecify hello rozmiar dysku hello.</span><span class="sxs-lookup"><span data-stu-id="ad119-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="ad119-150">Jak możemy dołączyć istniejącego dysku, hello `-DiskSizeInGB` jest określony jako `$null`.</span><span class="sxs-lookup"><span data-stu-id="ad119-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="ad119-151">Ta wartość zapewnia dysk danych hello jest prawidłowo podłączony, i bez hello muszą toodetermine hello true rozmiar dysku danych.</span><span class="sxs-lookup"><span data-stu-id="ad119-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="ad119-152">Zainstalować dysk dołączonych danych hello</span><span class="sxs-lookup"><span data-stu-id="ad119-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="ad119-153">Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour RDP.</span><span class="sxs-lookup"><span data-stu-id="ad119-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="ad119-154">Witaj poniższy przykład pobiera hello pliku połączenia RDP dla maszyny Wirtualnej o nazwie hello `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`i pobiera ją za`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="ad119-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="ad119-155">dysk z danymi Hello jest automatycznie wykryte i dołączony.</span><span class="sxs-lookup"><span data-stu-id="ad119-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="ad119-156">Wyświetlanie listy hello literę dysku hello toodetermine dołączone woluminy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad119-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="ad119-157">następujące przykładowe dane wyjściowe Hello pokazuje hello wirtualny dysk twardy podłączony dysk **2**.</span><span class="sxs-lookup"><span data-stu-id="ad119-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="ad119-158">(Można również użyć `Get-Volume` literę dysku hello tooview):</span><span class="sxs-lookup"><span data-stu-id="ad119-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="ad119-159">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="ad119-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="ad119-160">Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ad119-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="ad119-161">Po ma problemu hello problemów, należy kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="ad119-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="ad119-162">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="ad119-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="ad119-163">Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego hello rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="ad119-164">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="ad119-165">Z wewnątrz sesji protokołu RDP, odinstaluj hello dysku danych na maszyny Wirtualnej odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ad119-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="ad119-166">Numer dysku hello z hello należy poprzedniej `Get-Disk` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ad119-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="ad119-167">Następnie należy użyć `Set-Disk` tooset hello dysk w trybie offline:</span><span class="sxs-lookup"><span data-stu-id="ad119-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="ad119-168">Potwierdź dysku hello jest teraz skonfigurowana jako w trybie offline przy użyciu `Get-Disk` ponownie.</span><span class="sxs-lookup"><span data-stu-id="ad119-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="ad119-169">Witaj przykładowe dane wyjściowe wyglądają następująco zestawu dysku hello jest teraz w trybie offline:</span><span class="sxs-lookup"><span data-stu-id="ad119-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="ad119-170">Zakończyć sesję RDP.</span><span class="sxs-lookup"><span data-stu-id="ad119-170">Exit your RDP session.</span></span> <span data-ttu-id="ad119-171">W sesji programu Azure PowerShell należy usunąć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="ad119-172">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="ad119-172">Create VM from original hard disk</span></span>
<span data-ttu-id="ad119-173">Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="ad119-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="ad119-174">Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:</span><span class="sxs-lookup"><span data-stu-id="ad119-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="ad119-175">https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="ad119-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="ad119-176">Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad119-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="ad119-177">Witaj poniższy przykład wdraża hello szablonu toohello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="ad119-178">Witaj odpowiedzi wyświetli monit o hello szablonu, takie jak nazwa maszyny Wirtualnej, typ systemu operacyjnego i rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="ad119-179">Witaj `osDiskVhdUri` jest hello takie same jak wcześniej używane podczas podłączania hello istniejącego wirtualnego dysku twardego toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad119-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="ad119-180">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="ad119-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="ad119-181">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="ad119-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="ad119-182">Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myVMDeployed` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad119-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="ad119-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad119-183">Next steps</span></span>
<span data-ttu-id="ad119-184">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [tooan połączenia RDP Rozwiązywanie problemów z maszyny Wirtualnej Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad119-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ad119-185">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad119-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ad119-186">Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad119-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
