---
title: "aaaCreate zarządzanego obrazu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie zarządzanego obrazu maszyny Wirtualnej lub wirtualnego dysku twardego uogólnionego na platformie Azure. Obrazy mogą być używane toocreate wiele maszyn wirtualnych, które używają dysków zarządzanych."
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
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure

Można utworzyć zasobu zarządzanego obrazu z ogólnych maszyny Wirtualnej, która jest przechowywana jako dysków zarządzanych lub niezarządzanych dysku na koncie magazynu. Witaj może obrazu, a następnie można toocreate używanych wiele maszyn wirtualnych. 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize hello maszyny Wirtualnej systemu Windows za pomocą programu Sysprep

Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).

Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Jeśli korzystasz z programu Sysprep przed przekazaniem tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep. 
> 
> 

1. Zaloguj się toohello maszyny wirtualnej systemu Windows.
2. Otwórz okno wiersza polecenia hello jako administrator. Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.
3. W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.
4. W **opcje zamykania**, wybierz pozycję **zamknięcia**.
5. Kliknij przycisk **OK**.
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej. Nie uruchamiaj ponownie hello maszyny Wirtualnej.


## <a name="create-a-managed-image-in-hello-portal"></a>Tworzenie zarządzanego obrazu w portalu hello 

1. Otwórz hello [portal](https://portal.azure.com).
2. Kliknij przycisk hello toocreate znak plus nowy zasób.
3. Witaj filtr wyszukiwania, wpisz **obrazu**.
4. Wybierz **obrazu** z hello wyników.
5. W hello **obrazu** bloku, kliknij przycisk **Utwórz**.
6. W **nazwa**, wpisz nazwę hello obrazu.
7. Jeśli masz więcej niż jedną subskrypcję, wybierz hello właściwy z hello **subskrypcji** listy rozwijanej.
7. W **grupy zasobów** wybierz opcję **Utwórz nowy** i wpisz nazwę lub wybierz **z istniejących** i wybierz z listy rozwijanej hello toouse grupy zasobów.
8. W **lokalizacji**, wybierz lokalizację hello grupy zasobów.
9. W **typ systemu operacyjnego** hello typ systemu operacyjnego, systemu Windows lub Linux.
11. W **obiektu blob magazynu**, kliknij przycisk **Przeglądaj** toolook dla hello dysku VHD w magazynie Azure.
12. W **typ konta** wybierz Standard_LRS lub Premium_LRS. Standard korzysta stacje dysków twardych, a Premium dysków SSD. Oba rozwiązania używają magazyn lokalnie nadmiarowy.
13. W **buforowania dysku** wybierz hello odpowiedniego dysku opcję buforowania. Opcje Hello są **Brak**, **tylko do odczytu** i **odczytem/zapisem**.
14. Opcjonalnie: Można również dodać istniejący obraz toohello dysku danych, klikając **+ Dodaj dysk danych**.  
15. Po zakończeniu wprowadzania wybrane opcje, kliknij przycisk **Utwórz**.
16. Po utworzeniu obrazu hello, zobaczysz go jako **obrazu** zasobu w hello listy zasobów w grupie zasobów hello została wybrana opcja.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Tworzenie zarządzanego obrazu maszyny wirtualnej przy użyciu programu Powershell

Tworzenie obrazu bezpośrednio z maszyn wirtualnych zapewnia obrazu hello powitalne obejmuje wszystkie dyski hello skojarzone hello maszyny Wirtualnej, w tym hello dysku systemu operacyjnego i dysków z danymi.


Przed rozpoczęciem upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

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
2. Upewnij się, że powitalne cofnięciu przydziału maszyny Wirtualnej.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Ustaw stan hello hello maszyny wirtualnej za**Uogólniono**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Pobierz hello maszyny wirtualnej. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Utwórz konfigurację obraz powitania.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Utwórz obraz powitania.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Tworzenie zarządzanego obrazu dysku VHD w programie PowerShell

Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego.


1.  Najpierw należy ustawić hello typowe parametry:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Witaj Step\deallocate maszyny Wirtualnej.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Oznacz hello maszyny Wirtualnej, ponieważ uogólniony.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Utwórz obraz powitania przy użyciu Twojej uogólniony wirtualny dysk twardy systemu operacyjnego.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Tworzenie zarządzanego obrazu z migawki za pomocą programu Powershell

Można również utworzyć obraz zarządzanego z migawki hello wirtualnego dysku twardego z ogólnych maszyny Wirtualnej.

    
1. Utwórz niektóre zmienne. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Pobierz hello migawki.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Utwórz konfigurację obraz powitania.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Utwórz obraz powitania.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Następne kroki
- Teraz możesz [utworzyć Maszynę wirtualną z obrazu zarządzanych hello uogólniony](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

