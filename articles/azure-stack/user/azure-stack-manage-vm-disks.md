---
title: "Zarządzanie dyskami maszyny Wirtualnej w stosie Azure | Dokumentacja firmy Microsoft"
description: "Udostępnić dyski dla maszyn wirtualnych Azure stosu."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 4e5833cf-4790-4146-82d6-737975fb06ba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/14/2017
ms.author: brenduns
ms.reviewer: jiahan
ms.openlocfilehash: 0c36e2eaaf2d266842b2b7de0b0c8dc0ed1e0145
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2017
---
# <a name="virtual-machine-disk-storage-for-azure-stack"></a>Magazyn dyskowy maszyny wirtualnej Azure stosu

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Stos Azure obsługuje korzystanie z [niezarządzanych dysków](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#unmanaged-disks) na maszynie wirtualnej jako dysk systemu operacyjnego (systemu operacyjnego) oraz dysk z danymi. Aby używać dysków niezarządzane, należy utworzyć [konta magazynu](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) , a następnie zapisywania tych dysków jako stronicowe obiekty BLOB w kontenerach w ramach konta magazynu. Dyski te są następnie określane jako dyski maszyny Wirtualnej.

Do zwiększenia wydajności i zmniejszenia kosztów zarządzania systemu Azure stosu, zalecamy, umieść każdy dysk maszyny Wirtualnej w oddzielnych kontenera. Kontener powinno zawierać dysku systemu operacyjnego lub dysku danych, ale nie oba jednocześnie. Jednak nie ma ograniczenia, co uniemożliwia wprowadzanie zarówno do tego samego kontenera.

Jeśli dodasz co najmniej jeden dysk danych do maszyny Wirtualnej, należy zaplanować używanie dodatkowe kontenery jako lokalizację do przechowywania tych dysków. Podobnie jak w przypadku dysków z danymi dysk systemu operacyjnego dla dodatkowych maszyn wirtualnych należy się również w ich własnych osobnych kontenerów.

Kiedy tworzysz wiele maszyn wirtualnych, można ponownie użyć tego samego konta magazynu dla każdej nowej maszyny Wirtualnej. Kontenery tworzone powinna być unikatowa.  

Aby dodać dyski do maszyny Wirtualnej, użyj portalu użytkownika lub środowiska PowerShell.

| Metoda | Opcje
|-|-|
|[Portal użytkowników](#use-the-portal-to-add-additional-disks-to-a-vm)|-Dodaj nowe dyski danych do maszyny Wirtualnej, który został wcześniej zainicjowane. Nowe dyski są tworzone przez stos Azure. </br> </br>-Dodaj istniejący plik VHD jako dysk do maszyny Wirtualnej, który został wcześniej zainicjowane. W tym celu należy najpierw przygotować i przekaż plik VHD do stosu usługi Azure. |
|[PowerShell](#use-powershell-to-add-multiple-unmanaged-disks-to-a-vm) | — Utwórz nową maszynę Wirtualną z dyskiem systemu operacyjnego, a jednocześnie należy dodać co najmniej jeden dysk danych do tej maszyny Wirtualnej. |


## <a name="use-the-portal-to-add-additional-disks-to-a-vm"></a>Dodanie dodatkowych dysków do maszyny Wirtualnej za pomocą portalu
Domyślnie podczas tworzenia maszyny Wirtualnej dla większości elementów portalu marketplace, za pomocą portalu tworzony jest dysk systemu operacyjnego. Dyski utworzone przez usługę Azure są nazywane dysków zarządzanych.

Po udostępnić maszynie Wirtualnej, można użyć portalu można dodać nowy dysk danych lub istniejącego dysku danych do tej maszyny Wirtualnej. Każdy dodatkowy dysk należy umieścić w oddzielnych kontenera. Dyski dodane do maszyny Wirtualnej są nazywane niezarządzane dysków.

### <a name="use-the-portal-to-attach-a-new-data-disk-to-a-vm"></a>Użyj portalu można dołączyć nowego dysku danych do maszyny Wirtualnej

1.  W portalu kliknij **maszyn wirtualnych**.    
    ![Przykład: Pulpit nawigacyjny z maszyny Wirtualnej](media/azure-stack-manage-vm-disks/vm-dashboard.png)

2.  Wybierz maszynę wirtualną, które wcześniej zostały zainicjowane.   
    ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/select-a-vm.png)

3.  Dla maszyny wirtualnej, kliknij przycisk **dysków** > **Dołącz nowy**.       
    ![Przykład: Dołączyć nowego dysku do maszyny wirtualnej](media/azure-stack-manage-vm-disks/Attach-disks.png)    

4.  W **Dołączanie nowego dysku** okienku, kliknij przycisk **lokalizacji**. Domyślna lokalizacja jest ustawiana do tego samego kontenera, w którym jest przechowywana na dysku systemu operacyjnego.      
    ![Przykład: Ustaw lokalizację dysku](media/azure-stack-manage-vm-disks/disk-location.png)

5.  Wybierz **konta magazynu** do użycia. Następnie wybierz pozycję **kontenera** gdzie chcesz umieścić dysk z danymi. Z **kontenery** stronę, można utworzyć nowy kontener Jeśli chcesz. Następnie można zmienić lokalizacji dla nowego dysku do jego własnej kontenera. Korzystając z kontenera osobne dla każdego dysku, możesz dystrybuować umieszczania dysku danych, które może poprawić wydajność. Kliknij przycisk **wybierz** zapisać je.     
    ![Przykład: Select kontenera](media/azure-stack-manage-vm-disks/select-container.png)

6.  W **Dołączanie nowego dysku** pozycję Aktualizuj **nazwa**, **typu**, **rozmiar**, i **buforowanie hosta** ustawienia dysku. Następnie kliknij przycisk **OK** Aby zapisać nową konfigurację dysku dla maszyny Wirtualnej.  
    ![Przykład: Całego dysku załącznika](media/azure-stack-manage-vm-disks/complete-disk-attach.png)  

7.  Po stosu Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.   
    ![Przykład: Wyświetlanie dysku](media/azure-stack-manage-vm-disks/view-data-disk.png)


### <a name="attach-an-existing-data-disk-to-a-vm"></a>Dołączanie istniejącego dysku danych do maszyny Wirtualnej
1.  [Przygotuj plik VHD](https://docs.microsoft.com/azure/virtual-machines/windows/classic/createupload-vhd) do użycia jako dysk z danymi dla maszyny Wirtualnej. Przekazywanie tego pliku VHD na konto magazynu używanej w maszynie Wirtualnej, która ma zostać dołączony plik VHD.

  Planowane jest stosowanie różnych kontenerów do przechowywania pliku VHD niż kontener, który zawiera dysk systemu operacyjnego.   
  ![Przykład: Ładowanie pliku wirtualnego dysku twardego](media/azure-stack-manage-vm-disks/upload-vhd.png)

2.  Po przekazaniu pliku VHD, można przystąpić do Dołącz wirtualny dysk twardy do maszyny Wirtualnej. W menu po lewej stronie kliknij **maszyn wirtualnych**.  
 ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/vm-dashboard.png)

3.  Wybierz maszynę wirtualną z listy.    
  ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/select-a-vm.png)

4.  Na stronie dla maszyny wirtualnej, kliknij przycisk **dysków** > **Attach istniejących**.   
  ![Przykład: Dołączanie istniejącego dysku](media/azure-stack-manage-vm-disks/attach-disks2.png)

5.  W **dołączyć istniejącego dysku** kliknij przycisk **pliku VHD**. **Kont magazynu** zostanie otwarta strona.    
  ![Przykład: Select pliku wirtualnego dysku twardego](media/azure-stack-manage-vm-disks/select-vhd.png)

6.  W obszarze **kont magazynu**, wybierz konto do użycia, a następnie wybierz kontener, który zawiera wcześniej przekazany plik VHD. Wybierz plik VHD, a następnie kliknij przycisk **wybierz** zapisać je.    
  ![Przykład: Select kontenera](media/azure-stack-manage-vm-disks/select-container2.png)

7.  W obszarze **dołączyć istniejącego dysku**, wybrany plik jest wyświetlana w obszarze **pliku VHD**. Aktualizacja **buforowanie hosta** ustawienie dysku, a następnie kliknij przycisk **OK** Aby zapisać nową konfigurację dysku dla maszyny Wirtualnej.    
  ![Przykład: Dołącz plik wirtualnego dysku twardego](media/azure-stack-manage-vm-disks/attach-vhd.png)

8.  Po stosu Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.   
  ![Przykład: Zakończenie dysku dołączyć](media/azure-stack-manage-vm-disks/complete-disk-attach.png)


## <a name="use-powershell-to-add-multiple-unmanaged-disks-to-a-vm"></a>Aby dodać wiele dysków niezarządzanych do maszyny Wirtualnej za pomocą programu PowerShell
Można użyć programu PowerShell do obsługi administracyjnej maszyn wirtualnych i Dodaj nowy dysk danych lub dołączyć w ramach istniejącego wcześniej **VHD** pliku jako dysk z danymi.

**AzureRmVMDataDisk Dodaj** polecenia cmdlet dodaje dysku danych do maszyny wirtualnej. Można dodać dysku danych, podczas tworzenia maszyny wirtualnej lub dysku danych można dodać do istniejącej maszyny wirtualnej. Określ **VhdUri** parametru do dystrybucji dysków do różnych kontenerów.

### <a name="add-data-disks-to-a-new-virtual-machine"></a>Dodaj dyski danych do nowej maszyny wirtualnej
Poniższe przykłady tworzenie maszyny Wirtualnej z dyskami trzy danych za pomocą poleceń programu PowerShell, każdy umieszczone w różnych kontenerów.

Pierwsze polecenie tworzy obiekt maszyny wirtualnej, a następnie przechowuje je w *$VirtualMachine* zmiennej. Polecenie przypisuje nazwę i rozmiar maszyny wirtualnej.
  ```
  $VirtualMachine = New-AzureRmVMConfig -VMName "VirtualMachine" `
                                      -VMSize "Standard_A2"
  ```

Ścieżki danych trzech dysków, aby przypisać trzech kolejnych poleceń *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03* zmiennych. Zdefiniuj nazwę innej ścieżki w adresie URL do dystrybucji dysków do różnych kontenerów.     
  ```
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```

  ```
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```

  ```
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```

Końcowe trzy polecenia Dodaj dyski danych do maszyny wirtualnej przechowywanego w *$VirtualMachine*. Każde polecenie Określa nazwę, lokalizacji i dodatkowe właściwości dysku. Identyfikator URI każdego dysku są przechowywane w *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03*.
  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk1' `
                  -Caching 'ReadOnly' -DiskSizeInGB 10 -Lun 0 `
                  -VhdUri $DataDiskVhdUri01 -CreateOption Empty
  ```

  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk2' `
                 -Caching 'ReadOnly' -DiskSizeInGB 11 -Lun 1 `
                 -VhdUri $DataDiskVhdUri02 -CreateOption Empty
  ```

  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk3' `
                  -Caching 'ReadOnly' -DiskSizeInGB 12 -Lun 2 `
                  -VhdUri $DataDiskVhdUri03 -CreateOption Empty
  ```

Użyj następujących poleceń programu PowerShell, aby dodać Konfiguracja systemu operacyjnego dysku i sieci do maszyny Wirtualnej, a następnie uruchom nową maszynę Wirtualną.
  ```
  #set variables
  $rgName = "myResourceGroup"
  $location = "local"
  #Set OS Disk
  $osDiskUri = "https://contoso.blob.local.azurestack.external/vhds/osDisk.vhd"
  $osDiskName = "osDisk"

  $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $osDiskName -VhdUri $osDiskUri `
      -CreateOption FromImage -Windows

  # Create a subnet configuration
  $subnetName = "mySubNet"
  $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24

  # Create a vnet configuration
  $vnetName = "myVnetName"
  $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
      -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet

  # Create a public IP
  $ipName = "myIP"
  $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
      -AllocationMethod Dynamic

  # Create a network security group cnfiguration
  $nsgName = "myNsg"
  $rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
      -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
      -SourceAddressPrefix Internet -SourcePortRange * `
      -DestinationAddressPrefix * -DestinationPortRange 3389
  $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
      -Name $nsgName -SecurityRules $rdpRule

  # Create a NIC configuration
  $nicName = "myNicName"
  $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
  -Location $location -SubnetId $vnet.Subnets[0].Id -NetworkSecurityGroupId $nsg.Id -PublicIpAddressId $pip.Id

  #Create the new VM
  $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName VirtualMachine | `
      Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
      -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
  New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $VirtualMachine
  ```



### <a name="add-data-disks-to-an-existing-virtual-machine"></a>Dodaj dyski danych do istniejącej maszyny wirtualnej
Poniższe przykłady Dodaj trzy dyski danych do istniejącej maszyny Wirtualnej za pomocą poleceń programu PowerShell.
Pierwsze polecenie pobiera maszyny wirtualnej o nazwie maszyny wirtualnej przy użyciu **Get-AzureRmVM** polecenia cmdlet. Polecenie przechowuje maszynę wirtualną w *$VirtualMachine* zmiennej.
  ```
  $VirtualMachine = Get-AzureRmVM -ResourceGroupName "myResourceGroup" `
                                  -Name "VirtualMachine"
  ```
Trzech kolejnych poleceń przypisać ścieżek dysków z danymi trzy zmienne $DataDiskVhdUri01, $DataDiskVhdUri02 i $DataDiskVhdUri03.  Nazwy innej ścieżki w vhduri wskazują różnych kontenerów do umieszczania dysku.
  ```
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```
  ```
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```
  ```
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```


  Trzech kolejnych polecenia Dodaj dyski danych do maszyny wirtualnej przechowywanego w *$VirtualMachine* zmiennej. Każde polecenie Określa nazwę, lokalizacji i dodatkowe właściwości dysku. Identyfikator URI każdego dysku są przechowywane w *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03*.
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk1" `
                        -VhdUri $DataDiskVhdUri01 -LUN 0 `
                        -Caching ReadOnly -DiskSizeinGB 10 -CreateOption Empty
  ```
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk2" `
                        -VhdUri $DataDiskVhdUri02 -LUN 1 `
                        -Caching ReadOnly -DiskSizeinGB 11 -CreateOption Empty
  ```
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk3" `
                        -VhdUri $DataDiskVhdUri03 -LUN 2 `
                        -Caching ReadOnly -DiskSizeinGB 12 -CreateOption Empty
  ```


  Polecenia końcowego aktualizuje stan maszyny wirtualnej przechowywanego w *$VirtualMachine* w -*ResourceGroupName*.
  ```
  Update-AzureRmVM -ResourceGroupName "myResourceGroup" -VM $VirtualMachine
  ```
<!-- Pending scripts  

## Distribute the data disks of an existing VM
If you have a VM with more than one disk in the same container, the service operator of the Azure Stack deployment might ask you to redistribute the disks into individual containers.

To do so, use the scripts from the following location in GitHub. These scripts can be used to move the data disks to different containers.
-->

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej o maszynach wirtualnych Azure stosu, zobacz [zagadnienia dotyczące maszyn wirtualnych w stosie Azure](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-considerations).
