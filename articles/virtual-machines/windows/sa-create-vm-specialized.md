---
title: aaaCreate maszyny Wirtualnej z dysku specjalne na platformie Azure | Dokumentacja firmy Microsoft
description: "Dołączanie specjalne dysku niezarządzane, w modelu wdrażania usługi Resource Manager hello, aby utworzyć nową maszynę Wirtualną."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Utwórz maszynę Wirtualną z wirtualnego dysku twardego specjalne konta magazynu

Dołączanie dysku niezarządzane specjalne jako dysk systemu operacyjnego hello przy użyciu programu Powershell, aby utworzyć nową maszynę Wirtualną. Specjalne dysku jest kopią wirtualnego dysku twardego z istniejącą maszynę Wirtualną, która przechowuje konta użytkowników hello, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej. 

Dostępne są dwie opcje:
* [Przekazywanie wirtualnego dysku twardego](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Skopiuj hello VHD istniejącej maszyny Wirtualnej Azure](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

```powershell
Install-Module AzureRM.Compute 
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Opcja 1: Przekazanie specjalne dysku VHD

Możesz przekazać powitalne wirtualnego dysku twardego z specjalistyczne maszyny Wirtualnej utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej chmury.

### <a name="prepare-hello-vm"></a>Przygotowanie hello maszyny Wirtualnej
Możesz przekazać specjalne wirtualnego dysku twardego, który został utworzony przy użyciu lokalnej maszyny Wirtualnej lub wirtualnego dysku twardego wyeksportowane z innej chmury. Specjalne wirtualnego dysku twardego przechowuje hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej. Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone. 
  
  * [Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.
  * Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware).
  * Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP. To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania. 


### <a name="get-hello-storage-account"></a>Pobierz hello konta magazynu
Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany. Możesz użyć istniejącego konta magazynu lub Utwórz nową. 

tooshow hello dostępny magazyn kont, wpisz:

```powershell
Get-AzureRmStorageAccount
```

Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [obrazu maszyny Wirtualnej hello przekazywania](#upload-the-vm-vhd-to-your-storage-account) sekcji.

Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:

1. Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello. toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **zachodnie stany USA** regionu, wpisz:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Przekaż konta magazynu tooyour wirtualnego dysku twardego hello
Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello obrazu tooa kontenera na koncie magazynu. W tym przykładzie przekazywania hello pliku **myVHD.vhd** z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie **mojekontomagazynu** w hello **myResourceGroup** grupy zasobów. Plik Hello zostaną umieszczone w hello kontener o nazwie **mojkontener** i będzie hello nową nazwę pliku **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Opcja 2: Kopiowanie hello wirtualnego dysku twardego z istniejącej maszyny Wirtualnej Azure

Możesz skopiować toouse konta wirtualnego dysku twardego tooanother magazynu podczas tworzenia nowego, zduplikowany maszyny Wirtualnej.

### <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, że możesz:

* Informacje o hello **konta magazynu źródłowego i docelowego**. Witaj źródłowej maszyny Wirtualnej należy toohave hello magazynu konto i kontener nazwy. Zazwyczaj nazwa kontenera hello będzie **wirtualne dyski twarde**. Należy również toohave konto magazynu docelowego. Jeśli nie masz jeszcze jeden, można utworzyć przy użyciu portalu albo hello (**więcej usług** > kont magazynu > Dodaj) lub przy użyciu hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet. 
* Zostały pobrane i zainstalowane hello [narzędzia AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Cofnięcie przydziału hello maszyny Wirtualnej
Cofnięcie przydziału hello maszyny Wirtualnej, co zwalnia hello toobe VHD kopiowane. 

* **Portal**: kliknij **maszyn wirtualnych** > **myVM** > Zatrzymaj
* **PowerShell**: Użyj [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello maszyny Wirtualnej o nazwie **myVM** w grupie zasobów **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Witaj **stan** dla hello maszyny Wirtualnej w hello Azure portal zmieni się z **zatrzymane** za**zatrzymane (cofnięciu przydziału)**.

### <a name="get-hello-storage-account-urls"></a>Uzyskiwanie adresów URL konta magazynu hello
Należy adresy URL hello hello kont magazynu źródłowego i docelowego. Witaj adresy URL wyglądać: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Jeśli znasz już nazwę konta i kontener magazynu hello, można po prostu zastąpić hello informacji między toocreate nawiasy hello adres URL. 

Program hello portalu Azure lub adres URL hello tooget programu Azure Powershell:

* **Portal**: kliknij hello  **>**  dla **więcej usług** > **kont magazynu**  >   *Konto magazynu* > **obiekty BLOB** i pliku wirtualnego dysku twardego źródłowego prawdopodobnie znajduje się w hello **wirtualne dyski twarde** kontenera. Kliknij przycisk **właściwości** hello kontenera i skopiować tekst hello etykietą **adres URL**. Będziesz potrzebować adresy URL hello kontenerów zarówno hello źródłowym i docelowym. 
* **PowerShell**: Użyj [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello informacje dotyczące maszyny Wirtualnej o nazwie **myVM** w grupie zasobów hello **myResourceGroup**. W wynikach hello Szukaj w hello **profilu magazynu** sekcji hello **identyfikator Uri dysku Vhd**. Pierwsza część identyfikatora Uri hello Hello jest kontenerem toohello adres URL hello i hello ostatniej części jest hello nazwę wirtualnego dysku twardego systemu operacyjnego hello maszyny Wirtualnej.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Uzyskaj klucze dostępu do magazynu hello
Znajdź hello klucze dostępu dla hello konta magazynu źródłowego i docelowego. Aby uzyskać więcej informacji na temat kluczy dostępu, zobacz [kont magazynu Azure o](../../storage/common/storage-create-storage-account.md).

* **Portal**: kliknij **więcej usług** > **kont magazynu** > *konta magazynu*  >  **Klucze dostępu**. Kopia klucza hello oznaczone jako **klucz1**.
* **PowerShell**: Użyj [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello magazynu klucza dla konta magazynu hello **mojekontomagazynu** w grupie zasobów hello  **myResourceGroup**. Kopia klucza hello etykietą **klucz1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Skopiuj hello wirtualnego dysku twardego
Możesz skopiować pliki między kontami magazynu przy użyciu narzędzia AzCopy. Witaj docelowy kontener Jeśli hello określony kontener nie istnieje, jej zostanie utworzona automatycznie. 

toouse AzCopy, otwórz wiersz polecenia na komputerze lokalnym i przejdź folder toohello, w którym zainstalowano narzędzia AzCopy. Będzie on podobny zbyt*\Microsoft SDKs\Azure\AzCopy C:\Program Files (x86)*. 

toocopy hello wszystkie pliki znajdujące się w kontenerze, użyj hello **/S** przełącznika. Może to być używane toocopy hello wirtualnego dysku twardego systemu operacyjnego i wszystkich dysków danych hello, jeśli są one hello tego samego kontenera. W tym przykładzie pokazano sposób toocopy wszystkie hello pliki w kontenerze hello **mysourcecontainer** na koncie magazynu **mysourcestorageaccount** kontenera toohello **mydestinationcontainer**  w hello **mydestinationstorageaccount** konta magazynu. Zamień na powitania nazw kont magazynu hello i kontenery własne. Zastąp `<sourceStorageAccountKey1>` i `<destinationStorageAccountKey1>` z własnych kluczy.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Jeśli chcesz tylko toocopy konkretnego dysku VHD w kontenerze z wieloma plikami, można również określić nazwę pliku hello za pomocą przełącznika /Pattern hello. W tym przykładzie tylko hello plik o nazwie **myFileName.vhd** zostaną skopiowane.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Po zakończeniu otrzymasz wiadomość, która wygląda:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Rozwiązywanie problemów
* Korzystając z narzędzia AZCopy, jeśli zostanie wyświetlony błąd hello "Serwer nie powiodło się Żądanie hello tooauthenticate", upewnij się, że hello wartość nagłówka autoryzacji hello jest sformatowany poprawnie tym hello podpisu. Jeśli korzystasz z 2 klucza lub klucza pomocniczego magazynu hello, spróbuj użyć hello klucz podstawowy lub 1 magazynu.

## <a name="create-hello-new-vm"></a>Utwórz hello nowej maszyny Wirtualnej 

Należy toocreate sieci i innych toobe zasoby maszyn wirtualnych używanych przez hello nowej maszyny Wirtualnej.

### <a name="create-hello-subnet-and-vnet"></a>Tworzenie hello podsieci i sieci wirtualnej

Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. Utwórz podsieć hello. W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów hello **myResourceGroup**, i ustawia prefiks adresu podsieci hello zbyt**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Utwórz sieć wirtualną hello. W tym przykładzie zestawy hello toobe nazwa sieci wirtualnej **myVnetName**, zbyt hello lokalizacji**zachodnie stany USA**, i hello prefiks adresu sieci wirtualnej hello zbyt**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Tworzenie publicznego adresu IP i karty Sieciowej
tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.

1. Utwórz hello publicznego adresu IP. W tym przykładzie ustawiono zbyt hello nazwa publicznego adresu IP**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Utwórz hello karty sieciowej. W tym przykładzie ustawiono zbyt nazwy kart hello**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP
toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która pozwala dostępu RDP do portu 3389. Ponieważ specjalizowany hello wirtualnego dysku twardego dla hello utworzenia nowej maszyny Wirtualnej z istniejącego maszyny Wirtualnej, po utworzeniu hello maszyny Wirtualnej, należy użyć istniejącego konta z hello źródłowa maszyna wirtualna mająca uprawnienia toolog przy użyciu protokołu RDP.
W tym przykładzie zestawy hello Nazwa grupy NSG zbyt**myNsg** i hello RDP Nazwa reguły zbyt**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Nazwa maszyny Wirtualnej hello zestawu i rozmiaru

W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za "myVM" i hello wirtualna rozmiaru zbyt "Standard_A2".
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Dodaj hello karty Sieciowej
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Skonfiguruj dysk hello systemu operacyjnego

1. Ustaw hello identyfikatora URI dla hello wirtualnego dysku twardego, który został przekazany lub skopiowany. W tym przykładzie hello plik wirtualnego dysku twardego o nazwie **myOsDisk.vhd** jest przechowywana na koncie magazynu o nazwie **Mojekontomagazynu** w kontenerze o nazwie **Mojkontener**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Dodaj dysk hello systemu operacyjnego. Po utworzeniu hello dysk systemu operacyjnego, w tym przykładzie hello termin "osDisk" jest appened toohello wirtualna nazwa toocreate hello nazwa dysku systemu operacyjnego. W tym przykładzie określa również, że tego dysku VHD systemu Windows powinna być dołączone toohello maszyny Wirtualnej jako dysk systemu operacyjnego hello.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Opcjonalnie: Jeśli masz dysków z danymi tego toobe potrzeby dołączony toohello maszyny Wirtualnej, dodać hello dysków z danymi przy użyciu adresów URL hello danych wirtualne dyski twarde i hello odpowiedni numer jednostki logicznej (Lun).

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Korzystając z konta magazynu, adresy URL dysku systemu operacyjnego i danych hello wyglądać mniej więcej tak: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. To w portalu hello można znaleźć przy przeglądanie kontenera magazynu docelowego toohello, klikając hello systemu operacyjnego lub dane wirtualnego dysku twardego, która została skopiowana, a następnie skopiować zawartość hello hello adresu URL.


### <a name="complete-hello-vm"></a>Ukończyć powitalnych maszyny Wirtualnej 

Utwórz hello maszyny Wirtualnej przy użyciu hello konfiguracje, które właśnie utworzyliśmy.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Powinny pojawić się hello nowo utworzona maszyna wirtualna w hello [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą hello następującego środowiska PowerShell polecenia:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Następne kroki
toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego. Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md).

