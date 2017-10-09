---
title: "aaaCreate na zarządzanej maszynie Wirtualnej Azure z wirtualnego dysku twardego uogólnionego lokalnymi | Dokumentacja firmy Microsoft"
description: "Przekaż uogólniony tooAzure wirtualnego dysku twardego i korzystać z niego toocreate nowych maszyn wirtualnych w modelu wdrażania usługi Resource Manager hello."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Przekaż uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure

W tym temacie przedstawiono przy użyciu programu PowerShell tooupload dysku VHD uogólniony tooAzure maszyny Wirtualnej, tworzenie obrazu na podstawie hello wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną z tego obrazu. Możesz przekazać dysku VHD wyeksportowane z narzędzia wirtualizacji lokalnej lub innej chmury. Przy użyciu [dysków zarządzanych](managed-disks-overview.md) dla hello upraszcza zarządzanie wirtualna hello nowej maszyny Wirtualnej i zapewnia większą dostępność, gdy hello maszyna wirtualna jest umieszczona w zestawie dostępności. 

Jeśli chcesz toouse przykładowego skryptu, zobacz [przykładowy skrypt tooupload tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Przed rozpoczęciem

- Przed przekazaniem tooAzure dowolnego wirtualnego dysku twardego, należy wykonać [przygotowanie tooAzure tooupload Windows VHD lub VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Przegląd [planowanie migracji hello dysków tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) przed rozpoczęciem migracji zbyt[dysków zarządzanych](managed-disks-overview.md).
- Upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


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



## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure
Jeśli nie masz jeszcze programu PowerShell w wersji 1.4 lub nowszy zainstalowany, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

1. Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure. Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji. Zastąp  *<subscriptionID>*  o identyfikatorze hello hello Popraw subskrypcji.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Pobierz hello konta magazynu
Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany. Możesz użyć istniejącego konta magazynu lub Utwórz nową. 

Jeśli będziesz używać hello wirtualnego dysku twardego toocreate dysków zarządzanych dla maszyny Wirtualnej, Lokalizacja konta magazynu hello musi być tej samej lokalizacji hello, w którym zostanie utworzony hello maszyny Wirtualnej.

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

    Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **wschodnie stany USA** regionu, wpisz:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Prawidłowe wartości - SkuName to:
   
   * **Standard_LRS** — magazyn lokalnie nadmiarowy. 
   * **Standard_ZRS** -strefy nadmiarowego magazynu.
   * **Standard_GRS** — z magazynu geograficznie nadmiarowego magazynu. 
   * **Standard_RAGRS** -dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu. 
   * **Premium_LRS** — magazyn lokalnie nadmiarowy Premium. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Przekaż konta magazynu tooyour wirtualnego dysku twardego hello

Użyj hello [AzureRmVhd Dodaj](https://msdn.microsoft.com/library/mt603554.aspx) polecenia cmdlet tooupload hello wirtualnego dysku twardego tooa kontenera na koncie magazynu. W tym przykładzie przekazywania hello pliku *myVHD.vhd* z *"dyski twarde C:\Users\Public\Documents\Virtual\"*  tooa konto magazynu o nazwie *mojekontomagazynu*w hello *myResourceGroup* grupy zasobów. Plik Hello zostaną umieszczone w hello kontener o nazwie *mojkontener* i będzie hello nową nazwę pliku *myUploadedVHD.vhd*.

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

W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete

Zapisz hello **docelowy identyfikator URI** toouse ścieżkę później, jeżeli zostanie toocreate dysków zarządzanych lub nowej maszyny Wirtualnej przy użyciu hello przekazywać wirtualnego dysku twardego.

### <a name="other-options-for-uploading-a-vhd"></a>Inne opcje przekazywanie wirtualnego dysku twardego
 
 
Możesz również przekazywać konta magazynu wirtualnego dysku twardego tooyour przy użyciu jednej z następujących hello:

- [Narzędzie AzCopy](http://aka.ms/downloadazcopy)
- [Obiektu Blob magazynu Azure kopiowania interfejsu API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Obiekty BLOB magazynu Azure Explorer przekazywania](https://azurestorageexplorer.codeplex.com/)
- [Dokumentacja interfejsu API REST usługi Import/Eksport magazynu](https://msdn.microsoft.com/library/dn529096.aspx)
-   Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni. Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello czasu z jednostki rozmiaru i transferu danych. 
    Import/Eksport można używać konta standard storage tooa toocopy. Konieczne będzie toocopy z konta magazynu toopremium standard storage przy użyciu narzędzia, takiego jak narzędzie AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Tworzenie zarządzanego obrazu z hello przekazać wirtualnego dysku twardego 

Tworzenie obrazu zarządzanych za pomocą programu uogólniony wirtualny dysk twardy systemu operacyjnego. Zastąp wartości hello odpowiednimi informacjami.


1.  Najpierw należy ustawić hello typowe parametry:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Utwórz obraz powitania przy użyciu Twojej uogólniony wirtualny dysk twardy systemu operacyjnego.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. Utwórz podsieć hello. W tym przykładzie tworzy podsieć o nazwie *mySubnet* z prefiksu adresu hello *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Utwórz sieć wirtualną hello. W tym przykładzie tworzy sieć wirtualną o nazwie *myVnet* z prefiksu adresu hello *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Tworzenie publicznego adresu IP adres i interfejsu sieciowego

tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.

1. Utwórz publiczny adres IP. W tym przykładzie jest tworzony publiczny adres IP o nazwie *myPip*. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Utwórz hello karty sieciowej. W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP

toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389. 

W tym przykładzie tworzy grupy NSG o nazwie *myNsg* zawierający regułę o nazwie *myRdpRule* za pośrednictwem portu 3389 która zezwala na ruch RDP. Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Utwórz zmienną hello sieci wirtualnej

Utwórz zmienną ukończyć powitalnych sieci wirtualnej. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Uzyskać poświadczenia hello hello maszyny Wirtualnej

Witaj następującego polecenia cmdlet zostanie otwarte okno którym wprowadza użytkownika nowe toouse nazwę i hasło jako hello konta administratora lokalnego na zdalny dostęp do hello maszyny Wirtualnej. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Dodaj hello nazwę maszyny Wirtualnej i konfiguracji maszyny Wirtualnej toohello rozmiar.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Obraz maszyny Wirtualnej hello zestawu jako obraz źródłowy dla hello nowej maszyny Wirtualnej

Ustaw obraz źródłowy hello przy użyciu Identyfikatora hello hello zarządzanego obrazu maszyny Wirtualnej.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Ustawienia konfiguracji systemu operacyjnego hello i Dodaj hello karty sieciowej.

Wprowadź typ magazynu hello (PremiumLRS lub StandardLRS) i hello rozmiar dysku systemu operacyjnego hello. W tym przykładzie typ konta hello zbyt*PremiumLRS*, zbyt hello rozmiar dysku*128 GB* i buforowania dysku zbyt*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Utwórz hello maszyny Wirtualnej

Tworzenie nowej maszyny Wirtualnej za pomocą konfiguracji hello przechowywane w hello hello **$vm** zmiennej.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Następne kroki

toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego. Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

