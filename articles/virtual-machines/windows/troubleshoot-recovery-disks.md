---
title: "Używanie okien, rozwiązywanie problemów z maszyny Wirtualnej przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z maszyny Wirtualnej systemu Windows na platformie Azure, łącząc dysk systemu operacyjnego do odzyskiwania maszyny Wirtualnej przy użyciu programu Azure PowerShell"
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
ms.openlocfilehash: 8b7821b4285e73d461af426bfdfb3fdcc4454517
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="f9303-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Windows, dołączając dysk systemu operacyjnego do odzyskiwania maszyny Wirtualnej przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9303-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="f9303-104">Maszyny wirtualnej systemu Windows (VM) na platformie Azure napotkał błąd podczas rozruchu lub dysk, konieczne może wykonać kroki rozwiązywania problemów na wirtualnym dysku twardym, do samej siebie.</span><span class="sxs-lookup"><span data-stu-id="f9303-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="f9303-105">Typowym przykładem jest aktualizacja aplikacji nie powiodło się, który uniemożliwia było pomyślnie uruchomić maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f9303-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="f9303-106">Ten artykuł zawiera szczegóły dotyczące sposobu używania programu Azure PowerShell do wirtualnego dysku twardego nawiązać połączenia z innej maszyny Wirtualnej systemu Windows, usuń wszelkie błędy, a następnie ponownie utwórz oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="f9303-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="f9303-107">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="f9303-107">Recovery process overview</span></span>
<span data-ttu-id="f9303-108">Proces rozwiązywania problemów jest następujący:</span><span class="sxs-lookup"><span data-stu-id="f9303-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f9303-109">Usuwanie maszyny Wirtualnej, wystąpią problemy, utrzymując wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="f9303-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="f9303-110">Dołączanie i zainstalować wirtualny dysk twardy do innej maszyny Wirtualnej systemu Windows na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="f9303-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f9303-111">Nawiąż połączenie z maszyną wirtualną rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="f9303-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="f9303-112">Edytowanie plików lub uruchamianie narzędzi do rozwiązywania problemów z na oryginalny wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="f9303-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="f9303-113">Odłącz wirtualny dysk twardy od maszyny wirtualnej rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="f9303-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="f9303-114">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="f9303-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="f9303-115">Upewnij się, że masz [najnowsze programu Azure PowerShell](/powershell/azure/overview) zainstalowane i zalogowany do subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="f9303-115">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="f9303-116">W poniższych przykładach zastąpić parametr własne wartości.</span><span class="sxs-lookup"><span data-stu-id="f9303-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="f9303-117">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="f9303-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f9303-118">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="f9303-118">Determine boot issues</span></span>
<span data-ttu-id="f9303-119">Zrzut ekranu maszyny wirtualnej można wyświetlać na platformie Azure, aby ułatwić rozwiązywanie problemów rozruchu.</span><span class="sxs-lookup"><span data-stu-id="f9303-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="f9303-120">Ten zrzut ekranu może ułatwić zidentyfikowanie przyczyny maszyny Wirtualnej nie można uruchomić.</span><span class="sxs-lookup"><span data-stu-id="f9303-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="f9303-121">Poniższy przykład pobiera zrzut ekranu z maszyny Wirtualnej systemu Windows o nazwie `myVM` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="f9303-122">Przejrzyj zrzut ekranu, aby ustalić, dlaczego niepowodzenie maszyny Wirtualnej do rozruchu.</span><span class="sxs-lookup"><span data-stu-id="f9303-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="f9303-123">Należy pamiętać, wszystkie określone komunikaty o błędach lub podać kody błędów.</span><span class="sxs-lookup"><span data-stu-id="f9303-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f9303-124">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="f9303-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="f9303-125">Przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej, należy określić nazwę wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="f9303-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="f9303-126">Poniższy przykład pobiera informacje o Maszynie wirtualnej o nazwie `myVM` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="f9303-127">Wyszukaj `Vhd URI` w `StorageProfile` sekcji z danych wyjściowych poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="f9303-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="f9303-128">Następujące obcięty przykładzie danych wyjściowych `Vhd URI` pod koniec bloku kodu:</span><span class="sxs-lookup"><span data-stu-id="f9303-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

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


## <a name="delete-existing-vm"></a><span data-ttu-id="f9303-129">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="f9303-129">Delete existing VM</span></span>
<span data-ttu-id="f9303-130">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f9303-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f9303-131">Wirtualny dysk twardy jest, gdzie są przechowywane sam system operacyjny, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="f9303-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f9303-132">Samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiaru lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="f9303-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f9303-133">Każdy wirtualny dysk twardy ma dzierżawę przypisana w momencie dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="f9303-134">Dyski danych można dołączać i odłączać nawet wtedy, gdy maszyna wirtualna jest uruchomiona, ale dysku systemu operacyjnego nie można odłączyć, chyba że zasób maszyny wirtualnej zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="f9303-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="f9303-135">Dzierżawy w dalszym ciągu skojarzyć dysk systemu operacyjnego z maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="f9303-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f9303-136">Pierwszy krok w celu odzyskania maszyny Wirtualnej jest usunąć samego zasobu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="f9303-137">Usunięcie maszyny wirtualnej pozostawia wirtualne dyski twarde na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="f9303-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="f9303-138">Po usunięciu maszyny Wirtualnej, możesz dołączyć wirtualnego dysku twardego do innej maszyny Wirtualnej do rozwiązywania oraz usuwania błędów.</span><span class="sxs-lookup"><span data-stu-id="f9303-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="f9303-139">Poniższy przykład powoduje usunięcie maszyny Wirtualnej o nazwie `myVM` z grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="f9303-140">Poczekaj na Maszynie wirtualnej zakończył, usuwanie przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="f9303-141">Dzierżawy na wirtualnym dysku twardym, który kojarzy go z maszyny Wirtualnej musi zostać zwolniony przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="f9303-142">Dołączanie istniejącego wirtualnego dysku twardego do innej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9303-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="f9303-143">Dla następnych kilku krokach możesz użyć innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="f9303-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f9303-144">Istniejącego wirtualnego dysku twardego należy dołączyć do tej maszyny Wirtualnej rozwiązywania problemów, aby przeglądać i edytowania zawartości na dysku.</span><span class="sxs-lookup"><span data-stu-id="f9303-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="f9303-145">Ten proces umożliwia poprawić błędy konfiguracji lub przejrzyj dodatkowe aplikacji lub plików dziennika systemu, np.</span><span class="sxs-lookup"><span data-stu-id="f9303-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f9303-146">Wybierz lub Utwórz inną maszynę Wirtualną do użycia na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="f9303-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="f9303-147">Po dołączeniu istniejącego wirtualnego dysku twardego, podaj adres URL do dysku uzyskanych w poprzednim `Get-AzureRmVM` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9303-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="f9303-148">Poniższy przykład dołącza istniejącego wirtualnego dysku twardego do rozwiązywania problemów z maszyny Wirtualnej o nazwie `myVMRecovery` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="f9303-149">Dodawanie dysku wymaga określenia rozmiaru dysku.</span><span class="sxs-lookup"><span data-stu-id="f9303-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="f9303-150">Jak możemy dołączanie istniejącego dysku, `-DiskSizeInGB` jest określony jako `$null`.</span><span class="sxs-lookup"><span data-stu-id="f9303-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="f9303-151">Ta wartość zapewnia dysk danych jest prawidłowo podłączony i bez konieczności należy określić wartość true, rozmiar dysku danych.</span><span class="sxs-lookup"><span data-stu-id="f9303-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="f9303-152">Zainstalować dysk dołączonych danych</span><span class="sxs-lookup"><span data-stu-id="f9303-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="f9303-153">RDP do rozwiązywania problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f9303-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="f9303-154">Poniższy przykład pobierania pliku połączenia RDP dla maszyny Wirtualnej o nazwie `myVMRecovery` w grupie zasobów o nazwie `myResourceGroup`i pobiera go do `C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="f9303-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="f9303-155">Dysk danych jest automatycznie wykrywane i dołączony.</span><span class="sxs-lookup"><span data-stu-id="f9303-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="f9303-156">Wyświetl listę dołączone woluminy w celu określenia litery dysku w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9303-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="f9303-157">Następujące przykładowe dane wyjściowe zawiera wirtualny dysk twardy podłączony dysk **2**.</span><span class="sxs-lookup"><span data-stu-id="f9303-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="f9303-158">(Można również użyć `Get-Volume` Aby wyświetlić literę dysku):</span><span class="sxs-lookup"><span data-stu-id="f9303-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f9303-159">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="f9303-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f9303-160">Istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f9303-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f9303-161">Po usunięciu problemów wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f9303-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f9303-162">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="f9303-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f9303-163">Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f9303-164">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy dołączanie wirtualnego dysku twardego do rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f9303-165">Z w ramach sesji protokołu RDP, Usuń dysk z danymi na maszyny Wirtualnej odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="f9303-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="f9303-166">Należy numer dysku z poprzedniej `Get-Disk` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f9303-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="f9303-167">Następnie należy użyć `Set-Disk` można ustawić dysku w trybie offline:</span><span class="sxs-lookup"><span data-stu-id="f9303-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="f9303-168">Upewnij się, dysk zostaje ustawione jako w trybie offline przy użyciu `Get-Disk` ponownie.</span><span class="sxs-lookup"><span data-stu-id="f9303-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="f9303-169">Następujące przykładowe dane wyjściowe zawiera teraz dysk jest przełączany do trybu offline:</span><span class="sxs-lookup"><span data-stu-id="f9303-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="f9303-170">Zakończyć sesję RDP.</span><span class="sxs-lookup"><span data-stu-id="f9303-170">Exit your RDP session.</span></span> <span data-ttu-id="f9303-171">W sesji programu Azure PowerShell należy usunąć wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f9303-172">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="f9303-172">Create VM from original hard disk</span></span>
<span data-ttu-id="f9303-173">Aby utworzyć Maszynę wirtualną z oryginalny wirtualny dysk twardy, użyj [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="f9303-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="f9303-174">Rzeczywiste szablonu JSON jest przy użyciu następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="f9303-174">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="f9303-175">https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="f9303-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="f9303-176">Szablon wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu adresu URL wirtualnego dysku twardego starszych polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9303-176">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="f9303-177">Poniższy przykład wdraża szablonu w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-177">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="f9303-178">Odpowiedz monity dla szablonu, takie jak nazwa maszyny Wirtualnej, typ systemu operacyjnego i rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-178">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="f9303-179">`osDiskVhdUri` Jest taka sama jak wcześniej używane podczas dołączanie istniejącego wirtualnego dysku twardego do rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9303-179">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f9303-180">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="f9303-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="f9303-181">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="f9303-181">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f9303-182">Poniższy przykład umożliwia włączenie diagnostycznych rozszerzenia na Maszynie wirtualnej o nazwie `myVMDeployed` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f9303-182">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="f9303-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9303-183">Next steps</span></span>
<span data-ttu-id="f9303-184">Jeśli występują problemy dotyczące nawiązywania połączenia z maszyną Wirtualną, zobacz [połączeniami RDP Rozwiązywanie problemów z maszyną wirtualną Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9303-184">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f9303-185">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9303-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f9303-186">Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9303-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
