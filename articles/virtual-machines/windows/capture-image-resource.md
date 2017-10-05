---
title: "Tworzenie zarządzanego obrazu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie zarządzanego obrazu maszyny Wirtualnej lub wirtualnego dysku twardego uogólnionego na platformie Azure. Obrazy mogą służyć do tworzenia wiele maszyn wirtualnych, które używają dysków zarządzanych."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure

Można utworzyć zasobu zarządzanego obrazu z ogólnych maszyny Wirtualnej, która jest przechowywana jako dysków zarządzanych lub niezarządzanych dysku na koncie magazynu. Aby utworzyć wiele maszyn wirtualnych można następnie obrazu. 


## <a name="generalize-the-windows-vm-using-sysprep"></a>Maszyny Wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia

Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje komputer do użycia jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).

Upewnij się, że ról serwera uruchomionych na komputerze są obsługiwane przez program Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Jeśli korzystasz z programu Sysprep przed przekazaniem dysk VHD do platformy Azure po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep. 
> 
> 

1. Zaloguj się do maszyny wirtualnej systemu Windows.
2. Otwórz okno Wiersz polecenia jako administrator. Zmień katalog na **%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.
3. W **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że **Generalize** pole wyboru jest zaznaczone.
4. W **opcje zamykania**, wybierz pozycję **zamknięcia**.
5. Kliknij przycisk **OK**.
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Po zakończeniu działania programu Sysprep, zamyka maszyny wirtualnej. Nie uruchamiaj ponownie maszyny Wirtualnej.


## <a name="create-a-managed-image-in-the-portal"></a>Tworzenie zarządzanego obrazu w portalu 

1. Otwórz [portal](https://portal.azure.com).
2. Kliknij znak plus, aby utworzyć nowy zasób.
3. Filtr wyszukiwania, wpisz **obrazu**.
4. Wybierz **obrazu** z wyników.
5. W **obrazu** bloku, kliknij przycisk **Utwórz**.
6. W **nazwa**, wpisz nazwę obrazu.
7. Jeśli masz więcej niż jedną subskrypcję, wybierz właściwy z **subskrypcji** listy rozwijanej.
7. W **grupy zasobów** wybierz opcję **Utwórz nowy** i wpisz nazwę lub wybierz **z istniejących** i wybierz grupę zasobów do użycia z listy rozwijanej.
8. W **lokalizacji**, wybierz lokalizację, w grupie zasobów.
9. W **typ systemu operacyjnego** wybierz typ systemu operacyjnego, systemu Windows lub Linux.
11. W **obiektu blob magazynu**, kliknij przycisk **Przeglądaj** do wyszukania dysku VHD w magazynie Azure.
12. W **typ konta** wybierz Standard_LRS lub Premium_LRS. Standard korzysta stacje dysków twardych, a Premium dysków SSD. Oba rozwiązania używają magazyn lokalnie nadmiarowy.
13. W **buforowania dysku** wybierz odpowiedni dysk opcję buforowania. Dostępne są następujące opcje **Brak**, **tylko do odczytu** i **odczytem/zapisem**.
14. Opcjonalnie: Również dodaniem istniejącego dysku danych do obrazu, klikając **+ Dodaj dysk danych**.  
15. Po zakończeniu wprowadzania wybrane opcje, kliknij przycisk **Utwórz**.
16. Po utworzeniu obrazu, zobaczysz go jako **obrazu** zasobu na liście zasobów w grupie zasobów, wybrana.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Tworzenie zarządzanego obrazu maszyny wirtualnej przy użyciu programu Powershell

Tworzenie obrazu bezpośrednio z maszyny Wirtualnej sprawdza, czy obraz zawiera wszystkie dyski skojarzonych z maszyną Wirtualną, w tym dysku systemu operacyjnego i dysków z danymi.


Przed rozpoczęciem upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell. Uruchom następujące polecenie, aby go zainstalować.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


1. Utwórz niektóre zmienne.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Upewnij się, że cofnięciu przydziału maszyny Wirtualnej.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Ustaw stan maszyny wirtualnej na **Uogólniono**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Przełącz maszynę wirtualną. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Utwórz konfigurację obrazu.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Tworzenie obrazu.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Tworzenie zarządzanego obrazu dysku VHD w programie PowerShell

Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.


1.  Najpierw należy ustawić wspólne parametry:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate maszyny Wirtualnej.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Maszyna wirtualna zostać oznaczone jako uogólniony.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Utworzyć obraz przy użyciu programu uogólniony wirtualny dysk twardy systemu operacyjnego.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Tworzenie zarządzanego obrazu z migawki za pomocą programu Powershell

Można również utworzyć obraz zarządzanego z migawki wirtualnego dysku twardego z ogólnych maszyny Wirtualnej.

    
1. Utwórz niektóre zmienne. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Pobieranie migawki.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Utwórz konfigurację obrazu.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Tworzenie obrazu.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Następne kroki
- Teraz możesz [utworzyć Maszynę wirtualną z uogólniony obraz zarządzanych](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).  

