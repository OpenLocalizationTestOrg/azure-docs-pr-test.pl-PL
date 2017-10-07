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
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Rozwiązywanie problemów z maszyny Wirtualnej systemu Windows, dołączając tooa odzyskiwanie hello systemu operacyjnego maszyny Wirtualnej przy użyciu programu Azure PowerShell
Jeśli maszyny wirtualnej systemu Windows (VM) na platformie Azure napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów. Typowym przykładem jest aktualizację aplikacji, która uniemożliwia hello maszyna wirtualna stanie tooboot pomyślnie. Ten sposób artykuł szczegóły toouse tooconnect programu Azure PowerShell toofix maszyny Wirtualnej systemu Windows tooanother Twojego wirtualnego dysku twardego wszelkie błędy, następnie utworzyć je ponownie oryginalnej maszyny Wirtualnej.


## <a name="recovery-process-overview"></a>Omówienie procesu odzyskiwania
proces rozwiązywania problemów Hello jest następujący:

1. Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.
2. Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Windows na potrzeby rozwiązywania problemów.
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej. Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.
4. Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.
5. Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.

Upewnij się, że masz [hello najnowsze programu Azure PowerShell](/powershell/azure/overview) zainstalowane i zarejestrowane w ramach subskrypcji tooyour:

```powershell
Login-AzureRMAccount
```

Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.


## <a name="determine-boot-issues"></a>Określenie zagadnień rozruchu
Zrzut ekranu maszyny wirtualnej można wyświetlić na platformie Azure toohelp rozwiązywania problemów z rozruchem. Ten zrzut ekranu może ułatwić zidentyfikowanie przyczyny maszyny Wirtualnej nie powiedzie się tooboot. Witaj poniższy przykład pobiera hello zrzut ekranu z hello maszyny Wirtualnej systemu Windows o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Dlaczego hello maszyny Wirtualnej nie może wykonać tooboot toodetermine zrzut ekranu hello przeglądu. Należy pamiętać, wszystkie określone komunikaty o błędach lub podać kody błędów.


## <a name="view-existing-virtual-hard-disk-details"></a>Szczegóły istniejącego wirtualnego dysku twardego
Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD).

Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Wyszukaj `Vhd URI` w hello `StorageProfile` sekcji z danych wyjściowych hello hello poprzedzających polecenia. Witaj skróconą przykładowe dane wyjściowe wyglądają następująco hello `Vhd URI` końcowej hello hello blok kodu:

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


## <a name="delete-existing-vm"></a>Usuń istniejącą maszynę Wirtualną
Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure. Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje. Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC). Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej. Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta. dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.

pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie. Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu. Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.

powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej. dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej
Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów. Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku. Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np. Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.

Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello adres URL hello uzyskanych w poprzednim hello `Get-AzureRmVM` polecenia. Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Dodawanie dysku wymaga toospecify hello rozmiar dysku hello. Jak możemy dołączyć istniejącego dysku, hello `-DiskSizeInGB` jest określony jako `$null`. Ta wartość zapewnia dysk danych hello jest prawidłowo podłączony, i bez hello muszą toodetermine hello true rozmiar dysku danych.


## <a name="mount-hello-attached-data-disk"></a>Zainstalować dysk dołączonych danych hello

1. Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour RDP. Witaj poniższy przykład pobiera hello pliku połączenia RDP dla maszyny Wirtualnej o nazwie hello `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`i pobiera ją za`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. dysk z danymi Hello jest automatycznie wykryte i dołączony. Wyświetlanie listy hello literę dysku hello toodetermine dołączone woluminy w następujący sposób:

    ```powershell
    Get-Disk
    ```

    następujące przykładowe dane wyjściowe Hello pokazuje hello wirtualny dysk twardy podłączony dysk **2**. (Można również użyć `Get-Volume` literę dysku hello tooview):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Rozwiązywanie problemów na oryginalny wirtualny dysk twardy
Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami. Po ma problemu hello problemów, należy kontynuować hello następujące kroki.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy
Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego hello rozwiązywania problemów z maszyny Wirtualnej. Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.

1. Z wewnątrz sesji protokołu RDP, odinstaluj hello dysku danych na maszyny Wirtualnej odzyskiwania. Numer dysku hello z hello należy poprzedniej `Get-Disk` polecenia cmdlet. Następnie należy użyć `Set-Disk` tooset hello dysk w trybie offline:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Potwierdź dysku hello jest teraz skonfigurowana jako w trybie offline przy użyciu `Get-Disk` ponownie. Witaj przykładowe dane wyjściowe wyglądają następująco zestawu dysku hello jest teraz w trybie offline:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Zakończyć sesję RDP. W sesji programu Azure PowerShell należy usunąć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Tworzenie maszyny Wirtualnej z oryginalny dysk twardy
Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:

- https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON

Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia. Witaj poniższy przykład wdraża hello szablonu toohello grupy zasobów o nazwie `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Witaj odpowiedzi wyświetli monit o hello szablonu, takie jak nazwa maszyny Wirtualnej, typ systemu operacyjnego i rozmiar maszyny Wirtualnej. Witaj `osDiskVhdUri` jest hello takie same jak wcześniej używane podczas podłączania hello istniejącego wirtualnego dysku twardego toohello Rozwiązywanie problemów z maszyny Wirtualnej.


## <a name="re-enable-boot-diagnostics"></a>Włączyć ponownie diagnostykę rozruchu

Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone. Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myVMDeployed` hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [tooan połączenia RDP Rozwiązywanie problemów z maszyny Wirtualnej Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
