---
title: "Usługa Azure Premium Storage z programem SQL Server aaaUse | Dokumentacja firmy Microsoft"
description: "W tym artykule używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania oraz zapewnia wskazówki na temat używania usługi Azure Premium Storage z programem SQL Server uruchomiony na maszynach wirtualnych platformy Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Korzystanie z usługi Azure Premium Storage z programem SQL Server na maszynach wirtualnych
## <a name="overview"></a>Omówienie
[Usługa Azure Premium Storage](../../../storage/common/storage-premium-storage.md) jest hello generacji magazynu, który zapewnia małe opóźnienia i wysokiej wydajności we/wy. Najlepsza dla klucza obciążeń intensywnie wykorzystujących we/wy, takich jak program SQL Server na IaaS [maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machines/).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Ten artykuł zawiera wskazówki dotyczące migrowania maszyny wirtualnej z systemem toouse programu SQL Server magazyn w warstwie Premium i planowania. W tym infrastruktury platformy Azure (sieci, magazynu) i kroki maszyny Wirtualnej systemu Windows gościa. przykład Witaj w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) przedstawia migrację tooend zakończenia pełnej kompleksowe jak zwiększona toomove większych maszyn wirtualnych tootake korzystać z lokalnego magazynu SSD przy użyciu programu PowerShell.

Jest ważne toounderstand hello end-to-end proces pomocą usługi Azure Premium Storage z programem SQL Server na maszynach wirtualnych IAAS. Obejmuje to:

* Identyfikacja toouse wymagania wstępne hello magazyn w warstwie Premium.
* Przykłady wdrażanie programu SQL Server na IaaS tooPremium magazynu dla nowych wdrożeń.
* Przykłady Migrowanie istniejących wdrożeń zarówno serwerów autonomicznych, jak i wdrożeń przy użyciu SQL zawsze włączonych grup dostępności.
* Podejścia możliwej migracji.
* Pełne end-to-end przykład Azure, Windows i program SQL Server kroki hello migrację z istniejącej implementacji zawsze włączony.

Aby uzyskać więcej informacji o tła w programie SQL Server w maszynach wirtualnych platformy Azure, zobacz [programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Autor:** Sol Danielowi **recenzenci techniczni:** Śledź Vargas Artur Luis, Sanjay Mishra, Pravin Mital, blogu Thomasa Juergen, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Wymagania wstępne dotyczące magazyn w warstwie Premium
Istnieje kilka wymagań wstępnych dotyczących używania magazyn w warstwie Premium.

### <a name="machine-size"></a>Rozmiar maszyny
Dla magazynu Premium należy toouse DS serii maszyn wirtualnych (VM). Jeśli nie używasz maszyny serii DS w usługi w chmurze przed, należy usunąć hello istniejącej maszyny Wirtualnej, zachowanie hello dołączonych dysków i następnie utwórz nową usługę w chmurze przed ponownym utworzeniem hello maszyny Wirtualnej jako DS * rozmiaru roli. Aby uzyskać więcej informacji na temat rozmiarów maszyny wirtualnej, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Usługi w chmurze
Po utworzeniu nowej usługi w chmurze tylko można DS * maszyn wirtualnych z magazyn w warstwie Premium. Jeśli używasz programu SQL Server zawsze na platformie Azure, hello zawsze na odbiornika będzie odnosić się toohello Azure wewnętrznego lub zewnętrznego adresu IP usługi równoważenia obciążenia adres skojarzony z usługą w chmurze. Ten artykuł skupia się na temat toomigrate przy zachowaniu dostępności w tym scenariuszu.

> [!NOTE]
> Serii DS * musi być hello pierwsza maszyna wirtualna, który jest wdrożony toohello nową usługę w chmurze.
>
>

### <a name="regional-vnets"></a>Regionalnych sieci wirtualnych
Dla maszyn wirtualnych DS * należy skonfigurować hello sieci wirtualnych (VNET) hosting sieci regionalnych toobe maszyn wirtualnych. To "rozszerzenie" hello sieci Wirtualnej jest tooallow hello większych maszyn wirtualnych toobe udostępnione w innych klastrach i umożliwić komunikację między nimi. W hello następującego zrzutu ekranu hello wyróżnioną lokalizację pokazuje regionalnych sieci wirtualnych, hello pierwszego wyniku pokazuje "wąskie" sieci Wirtualnej.

![RegionalVNET][1]

Zostanie podniesiony Microsoft obsługi biletów toomigrate tooa regionalnej sieci Wirtualnej, Microsoft będzie zmiany, a następnie toocomplete hello migracji tooregional sieci wirtualnych, zmień właściwość hello AffinityGroup w konfiguracji sieci hello. Najpierw wyeksportować hello konfigurację sieci w programie PowerShell, a następnie zastąp hello **AffinityGroup** właściwości w hello **VirtualNetworkSite** element z **lokalizacji** Właściwość. Określ `Location = XXXX` gdzie `XXXX` jest region platformy Azure. Następnie można zaimportować hello nowej konfiguracji.

Na przykład biorąc pod uwagę powitania po konfigurację sieci Wirtualnej:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove tego tooa regionalnej sieci Wirtualnej w Europa Zachodnia, zmienić toohello konfiguracji powitania po:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Konta magazynu
Konieczne będzie toocreate nowe konto magazynu, który jest skonfigurowany dla usługi Premium Storage. Należy zauważyć, że użycie hello magazyn w warstwie Premium jest hello konta magazynu, nie dla poszczególnych dysków VHD, jednak podczas korzystania z maszyny Wirtualnej serii DS * możesz dołączyć pliki VHD z konta Premium i standardowa magazynu. Może to rozważyć, jeśli nie chcesz, aby tooplace hello wirtualnego dysku twardego systemu operacyjnego na toohello konta Premium Storage.

następujące Hello **AzureStorageAccountPowerShell nowy** z hello "Premium_LRS" **typu** tworzy konto magazynu Premium:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Ustawienia pamięci podręcznej wirtualne dyski twarde
Witaj podstawowa różnica między tworzenie dysków, które są częścią konta Premium Storage jest ustawienie hello dyskowej pamięci podręcznej. Dla danych programu SQL Server woluminu dyski go zaleca się użycie "**buforowania odczytu**". W przypadku woluminów dziennika transakcji hello dysku pamięci podręcznej ustawienie zbyt "**Brak**". To jest inna niż hello zalecenia dotyczące kont magazynu w warstwie standardowa.

Po dołączeniu hello wirtualne dyski twarde nie można zmienić ustawienia pamięci podręcznej hello. Czy należy toodetach i ponownie dołączyć hello wirtualnego dysku twardego z ustawieniem zaktualizowano pamięci podręcznej.

### <a name="windows-storage-spaces"></a>Miejsca do magazynowania systemu Windows
Można użyć [miejsca do magazynowania systemu Windows](https://technet.microsoft.com/library/hh831739.aspx) tak samo jak z poprzedniego magazynu w warstwie standardowa, umożliwi toomigrate maszynę Wirtualną, która jest już przy użyciu funkcji miejsca do magazynowania. przykład Witaj w [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (krok 9 i do przodu) pokazuje hello tooextract kodu programu Powershell i zaimportuj maszynę Wirtualną za pomocą wielu dołączonych dysków VHD.

Pule magazynu były używane z przepływności tooenhance konta magazynu Azure standardowe i zmniejszenia opóźnień. Wartość można znaleźć w testowanie pod kątem nowych wdrożeń pul magazynu z atrybutem magazyn w warstwie Premium, ale co zwiększa stopnia złożoności z instalacji magazynu.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Jak toofind które dyski wirtualne Azure mapowania pul toostorage
Ponieważ istnieją różne pamięci podręcznej ustawienie zalecenia dotyczące dołączonych dysków VHD, można zdecydować toocopy hello wirtualne dyski twarde tooa konta Premium Storage. Jednak gdy użytkownik przyłącz je ponownie toohello nowej serii DS maszyny Wirtualnej, może być konieczne ustawienia pamięci podręcznej hello tooalter. Jest prostsze powitalne tooapply magazyn w warstwie Premium zalecanych ustawień pamięci podręcznej, jeśli masz oddzielnych dysków VHD dla hello danych SQL plików i dziennika plików (zamiast pojedynczego wirtualnego dysku twardego, który zawiera zarówno).

> [!NOTE]
> Jeśli masz pliki danych i dziennika programu SQL Server na powitania na powitania wzorce dostępu we/wy dla obciążeń bazy danych zależy od tego samego woluminu, hello buforowanie wybranej opcji. Tylko testowania wykaże buforowania, która opcja jest najlepsza w przypadku tego scenariusza.
>
>

Miejsca do magazynowania systemu Windows, które składają się z wielu dysków VHD, konieczne będzie toolook w przypadku korzystania z oryginalnego tooidentify skrypty, które wirtualne dyski twarde dołączonych są jednak w określonej puli, więc można zdefiniować ustawienia pamięci podręcznej hello odpowiednio dla każdego dysku.

Jeśli nie masz oryginalnego tooshow dostępne skryptu można, które wirtualne dyski twarde mapy toohello puli magazynu, można użyć hello następujące kroki toodetermine hello magazynowania dysku puli mapowania.

Dla każdego dysku Użyj hello następujące kroki:

1. Pobranie listy dysków dołączonych tooVM z hello **Get-AzureVM** polecenia:

    Get-AzureVM - ServiceName <servicename> — nazwa <vmname> | Get-AzureDataDisk
2. Uwaga hello Diskname i jednostki LUN.

    ![DisknameAndLUN][2]
3. Pulpit zdalny na powitania maszyny Wirtualnej. Następnie przejdź zbyt**Zarządzanie komputerem** | **Menedżera urządzeń** | **dysków**. Przyjrzyj się hello właściwości każdego hello "Microsoft dysków wirtualnych"

    ![VirtualDiskProperties][3]
4. w tym miejscu numer LUN Hello jest numer LUN toohello odwołania podane podczas podłączania hello toohello wirtualnego dysku twardego maszyny Wirtualnej.
5. Dla hello "Microsoft Virtual Disk" Przejdź toohello **szczegóły** na karcie następnie hello **właściwości** listy znajduje się zbyt**klucz sterownika**. W hello **wartość**, hello Uwaga **przesunięcia**, który jest 0002 w hello następującego zrzutu ekranu. Witaj 0002 oznacza hello Dysk_fizyczny_2 hello odwołań do puli magazynu.

    ![VirtualDiskPropertyDetails][4]
6. Dla każdej puli magazynów zrzutu limit hello skojarzone dyski:

    Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Teraz można używać tego tooassociate informacji dołączonych dysków tooPhysical wirtualnych dysków twardych w pule magazynu.

Zmapowaniu wirtualne dyski twarde tooPhysical dysków w pule magazynu można następnie odłączyć i skopiuj je za pośrednictwem tooa konta Premium Storage, a następnie dołącz je z poprawne ustawienie pamięci podręcznej w hello. Zobacz przykład Witaj w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), kroki od 8 do 12. Te kroki pokazują, jak tooextract plik wirtualnego dysku twardego maszyny Wirtualnej, dołączyć dysku konfiguracji tooa CSV kopiowanie hello wirtualne dyski twarde, zmiany ustawień pamięci podręcznej konfiguracji dysku hello i na koniec ponownie wdrożyć hello wirtualna serii DS maszyny Wirtualnej z hello wszystkie dołączone dyski.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Maszyna wirtualna magazynu przepustowość i przepływność magazynu wirtualnego dysku twardego
Witaj wydajność magazynu zależy hello rozmiar maszyny Wirtualnej DS * określone i hello rozmiary dysku VHD. maszyny wirtualne Hello mają różne przydziały hello liczba wirtualnych dysków twardych, które można dołączać i hello maksymalnej przepustowości, obsługują one (MB/s). Hello przepustowości określonych liczb, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Zwiększona IOPS są osiągane o dużym rozmiarze dysku. Należy rozważyć to Zastanawiając się ścieżki migracji. Aby uzyskać szczegółowe informacje [można znaleźć tabeli hello IOPS i typów dysków](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Na koniec należy rozważyć, czy maszyny wirtualne mają inny dysk maksymalnej przepustowości, które wspierają dla wszystkich dysków dołączonych. Wysokie obciążenie może nasycenia hello dysku maksymalna przepustowość dostępną dla tego rozmiaru roli maszyny Wirtualnej. Na przykład Standard_DS14 będzie obsługuje konto too512MB/s; w związku z tym z trzech dysków P30 można nasycenia przepustowości dysku hello hello maszyny Wirtualnej. Jednak w tym przykładzie limit przepływności hello może zostać przekroczona w zależności od różnych hello odczytu i zapisu z systemem IOs.

## <a name="new-deployments"></a>Nowych wdrożeń
Witaj w dwóch następnych sekcjach pokazują, jak można wdrożyć maszyn wirtualnych programu SQL Server tooPremium magazynu. Jak wspomniano wcześniej, niekoniecznie niepotrzebne dysk systemu operacyjnego hello tooplace na magazyn w warstwie Premium. Możesz wybrać toodo to jeśli zostanie są mają zostać tooplace żadnych intensywnych obciążeń we/wy na powitania wirtualnego dysku twardego systemu operacyjnego.

Witaj w pierwszym przykładzie pokazano, przy użyciu istniejących obrazów w galerii Azure. Witaj drugi przykład przedstawia sposób toouse niestandardowych maszyny Wirtualnej obrazu, który ma w istniejącego konta magazynu w warstwie standardowa.

> [!NOTE]
> Tych przykładów założono, że utworzono już regionalnej sieci Wirtualnej.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Utwórz nową maszynę Wirtualną z magazynu Premium z galerii
w poniższym przykładzie Hello pokazuje, jak tooplace hello wirtualnego dysku twardego systemu operacyjnego na magazyn w warstwie premium i Dołącz wirtualne dyski twarde Premium magazynu. Można jednak również umieścić hello dysk systemu operacyjnego w ramach konta Standard Storage, a następnie dołącz wirtualne dyski twarde, które znajdują się na koncie magazynu Premium. Przedstawiono oba scenariusze.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Krok 1: Tworzenie konta magazynu w warstwie Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Krok 2: Tworzenie nowej usługi w chmurze
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Krok 3: Reserve VIP usługi chmury (opcjonalnie)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Krok 4: Tworzenie kontenera maszyny Wirtualnej
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Krok 5: Wprowadzenie do wirtualnego dysku twardego systemu operacyjnego na Standard lub Premium Storage
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Krok 6: Tworzenie maszyny Wirtualnej
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Utwórz nowy toouse maszyny Wirtualnej — wersja Premium magazynu z niestandardowego obrazu
W tym scenariuszu pokazano, gdzie masz istniejących dostosowanych obrazów, które znajdują się na koncie magazynu w warstwie standardowa. Jak wspomniano, jeśli chcesz hello tooplace wirtualnego dysku twardego systemu operacyjnego na magazyn w warstwie Premium należy toocopy hello obrazu, który istnieje w hello konta Standard Storage i przenieść je tooa magazyn w warstwie Premium, zanim będzie można go używać. Jeśli masz obrazu lokalnej, możesz także użyć tej metody toocopy który bezpośrednio toohello konta Premium Storage.

#### <a name="step-1-create-storage-account"></a>Krok 1: Tworzenie konta magazynu
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Krok 2 Tworzenie usługi w chmurze
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Krok 3: Użyj istniejącego obrazu
Można użyć istniejącego obrazu. Można też [zająć obraz istniejącej maszyny](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Uwaga hello maszyny, które utworzeniem obrazu nie ma toobe DS * maszyny. Po utworzeniu obrazu hello hello po Pokaż kroki jak toocopy on toohello konta Premium Storage z hello **Start AzureStorageBlobCopy** polecenia programu PowerShell.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Krok 4: Kopię Blob między kontami magazynu
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Krok 5: Regularne sprawdzanie stanu kopiowania:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Krok 6: Dodawanie tooAzure repozytorium obrazu dysku w subskrypcji
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Może się okazać, nawet jeśli raporty o stanie hello jako Powodzenie, można nadal uzyskanie błąd dzierżawy dysku. W takim przypadku poczekaj około 10 minut.
>
>

#### <a name="step-7--build-hello-vm"></a>Krok 7: Tworzenie hello maszyny Wirtualnej
W tym miejscu tworzysz hello maszyny Wirtualnej z obrazu i dołączanie dwóch dysków VHD magazynu Premium:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Istniejące wdrożenia, które nie należy używać zawsze włączonych grup dostępności
> [!NOTE]
> Istniejące wdrożenia, najpierw Zobacz hello [wymagania wstępne](#prerequisites-for-premium-storage) tego tematu.
>
>

Istnieją różne zagadnienia dotyczące wdrożenia programu SQL Server, których nie należy używać zawsze włączonych grup dostępności i tych, które wykonują. Jeśli nie jest używana zawsze włączone i mieć istniejących autonomicznego serwera SQL, możesz uaktualnić tooPremium magazynu przy użyciu nowego konta magazyn i usługa w chmurze. Należy wziąć pod uwagę hello następujące opcje:

* **Tworzenie nowej maszyny Wirtualnej serwera SQL**. Można utworzyć nowego programu SQL Server maszynę Wirtualną, która używa konta Premium Storage, zgodnie z opisem w nowych wdrożeń. Następnie kopia zapasowa i przywracanie baz danych konfiguracji i użytkownika programu SQL Server. Witaj, aplikacja musi mieć toobe zaktualizowane tooreference hello nowego programu SQL Server, gdy dostęp jest uzyskiwany wewnętrznie i zewnętrznie. Będzie potrzebny toocopy wszystkie obiekty "poza db" tak, jakby wcześniej zadania migracji serwera SQL (SxS) obok siebie. Obejmuje to obiekty, takie jak nazwy logowania, certyfikaty i połączone serwery.
* **Migrowanie istniejących maszyn wirtualnych serwera SQL**. Będzie to wymagało przełączania w tryb offline hello maszyny Wirtualnej programu SQL Server, a następnie przenoszenia go tooa nową usługę w chmurze, która obejmuje kopiowanie wszystkich jego toohello wirtualne dyski twarde dołączonych konta Premium Storage. Gdy hello maszyny Wirtualnej do trybu online, aplikacja hello będzie odwoływać hello nazwa hosta serwera jako przed. Należy pamiętać, że rozmiar hello hello istniejącego dysku będzie miało wpływ na powitania charakterystyki wydajności. Na przykład dysk 400 GB pobiera zaokrąglona tooa P20. Jeśli znasz nie wymagają tego wydajności dysku, można odtworzyć hello maszyny Wirtualnej jako wirtualna serii DS i Dołącz wirtualne dyski twarde specyfikacji wydajności rozmiar hello, które są wymagane na magazynu Premium. Następnie można odłączyć i ponownie dołączyć hello pliki bazy danych SQL.

> [!NOTE]
> Podczas kopiowania dysków VHD hello należy pamiętać o rozmiarze hello, w zależności od wielkości hello oznacza typ dysku magazynu Premium dzielą się na, określa specyfikacji wydajności dysku. Azure zaokrągli się toohello najbliższej dysku rozmiar, jeśli dysk GB, 400, to zostanie zaokrąglona tooa P20. W zależności od istniejącego we/wy wymagań z hello wirtualnego dysku twardego systemu operacyjnego nie trzeba toomigrate tego tooa konta Premium Storage.
>
>

Jeśli program SQL Server jest dostępny zewnętrznie, VIP usługi chmury hello zostanie zmieniona. Będą także mieć tooupdate punktów końcowych, listy ACL i DNS ustawienia.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Istniejące wdrożenia, które używają zawsze włączone grupy dostępności
> [!NOTE]
> Istniejące wdrożenia, najpierw Zobacz hello [wymagania wstępne](#prerequisites-for-premium-storage) tego tematu.
>
>

Początkowo w tej sekcji przedstawiono, jak zawsze na współdziała z sieci platformy Azure. Firma Microsoft będzie następnie rozbić migracje w scenariuszach tootwo: migracje, w którym mogą następować Przestój i migracje, w którym należy osiągnąć minimalnym czasem przestojów.

Lokalnego programu SQL Server zawsze włączonych grup dostępności Użyj odbiornika lokalnych, które rejestruje wirtualnego nazwę DNS oraz adres IP, który jest współużytkowana przez jeden lub więcej serwerów SQL. Jeżeli klienci łączą się routingu hello odbiornik IP toohello podstawowego serwera SQL. Jest to serwer hello, będący właścicielem hello zawsze na IP zasobu w tym czasie.

![DeploymentsUseAlways na][6]

W systemie Microsoft Azure może mieć tooa adres przypisany tylko jeden IP karty Sieciowej na powitania maszyny Wirtualnej, dlatego w kolejności tooachieve hello samą warstwę abstrakcji jako lokalną, hello adres IP, który jest przypisywany toohello wewnętrzne/zewnętrzne moduły równoważenia obciążenia (ILB/ELB) korzysta z platformy Azure. Witaj IP zasobu, który jest udostępniana między serwerami hello ustawiono toohello tego samego adresu IP jako hello ILB/ELB. Ta jest publikowana w hello DNS, a ruch klientów jest przekazywana hello ILB/ELB toohello podstawowego serwera SQL repliki. Witaj ILB/ELB wie, która programu SQL Server jest podstawowego, ponieważ używa sond tooprobe hello zawsze na IP zasobu. W poprzednim przykładzie hello go sondy w każdym węźle, który ma punkt końcowy odwołuje się hello ELB/ILB, zależności odpowiada jest hello podstawowego serwera SQL.

> [!NOTE]
> Witaj ILB i ELB mają przypisaną tooa określonej usługi w chmurze Azure, w związku z tym wszelkie migracja do chmury na platformie Azure najprawdopodobniej oznacza że powitalne zmieni IP usługi równoważenia obciążenia.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migrowanie zawsze na wdrożenia, które umożliwiają Przestój
Istnieją dwa strategii toomigrate zawsze na wdrożenia, które umożliwiają przestój:

1. **Dodaj więcej tooan replikach pomocniczych istniejących zawsze na klaster**
2. **Migrowanie tooa nowy zawsze na klaster**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Dodaj więcej tooan replikach pomocniczych istniejący zawsze na klaster
Jedną ze strategii jest tooadd więcej toohello pomocnicze bazy danych zawsze włączonej grupy dostępności. Należy tooadd na nową usługę w chmurze i zaktualizować odbiornika hello hello nowych IP usługi równoważenia obciążenia.

##### <a name="points-of-downtime"></a>Punkty przestój:
* Sprawdzanie poprawności klastra.
* Test trybu failover zawsze na nowe pomocnicze bazy danych.

Jeśli używane są pule magazynu systemu Windows w ramach hello maszyny Wirtualnej dla wyższej przepustowości we/wy, następnie te zostaną przełączone do trybu offline podczas pełnej weryfikacji klastra. test weryfikacji Hello jest wymagana podczas dodawania węzłów toohello klastra. czas trwania testu hello toorun Hello może być inna, więc należy przetestować to w Twojej tooget środowiska testowego reprezentatywny Przybliżona godzina, o ile to może potrwać.

Należy udostępnić czasu, gdzie można wykonywać ręcznego przełączania trybu failover i chaos testowania na powitania nowo dodany węzłów tooensure zawsze o wysokiej dostępności funkcji, zgodnie z oczekiwaniami.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Należy zatrzymać wszystkie wystąpienia programu SQL Server, której pule magazynów hello są używane przed hello weryfikacji uruchamia.
>
> ##### <a name="high-level-steps"></a>Ogólne kroki
>

1. Utwórz dwóch nowych serwerów SQL w nową usługę w chmurze z dołączonym magazynem Premium.
2. Skopiuj przez pełne kopie zapasowe i przywracanie z **NORECOVERY**.
3. Skopiuj za pośrednictwem "poza użytkownik bazy danych" obiekty zależne, takie jak nazwy logowania itp.
4. Utworzenie nowego wewnętrznego obciążenia równoważenia (ILB) lub Użyj zewnętrznego modułu równoważenia obciążenia (ELB), a następnie skonfigurować końcowych równoważenia obciążenia w obu węzłach nowego.

   > [!NOTE]
   > Sprawdź, czy przed kontynuowaniem na wszystkich węzłach jest hello prawidłowej konfiguracji punktu końcowego
   >
   >
5. Zatrzymaj toohello dostępu użytkownika/aplikacji SQL Server (Jeśli używane są pule magazynu).
6. Zatrzymaj usługi aparatu programu SQL Server na wszystkich węzłach (Jeśli używane są pule magazynu).
7. Dodaj nowe węzły toocluster i pełna weryfikacja została uruchomiona.
8. Po sprawdzania poprawności zakończy się pomyślnie, należy uruchomić wszystkie usługi serwera SQL.
9. Dzienniki transakcji i przywracania kopii zapasowych baz danych użytkowników.
10. Dodaj nowe węzły do hello zawsze włączonej grupy dostępności i umieścić replikacji do **synchroniczne**.
11. Dodaj adres IP hello zasób Adres hello nowe chmury usługi ILB/ELB za pomocą programu PowerShell dla zawsze włączone oparte na przykład Witaj obejmujący wiele lokacji w hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). Usługa klastrowania systemu Windows hello zbioru **możliwych właścicieli** z hello **adres IP** zasobów toohello nowe węzły stary. W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Tooone pracy awaryjnej hello nowe węzły.
13. Należy hello nowe węzły automatycznej pracy awaryjnej partnerów i testy trybu failover.
14. Usuń węzły oryginalnego z grupy dostępności.

##### <a name="advantages"></a>Zalety
* Nowe serwery SQL mogą być testowane (SQL Server i aplikacji), zanim zostaną one dodane tooAlways na.
* Można zmienić rozmiar maszyny Wirtualnej hello i dostosowywać hello tooyour dokładne wymagania dotyczące magazynu w. Jednakże może być korzystne tookeep wszystkich ścieżek plików SQL hello hello takie same.
* Można kontrolować uruchomienia hello transferu toohello kopii zapasowych bazy danych hello replikach pomocniczych. Ta różni się od przy użyciu usługi Azure **Start AzureStorageBlobCopy** toocopy polecenia wirtualne dyski twarde, ponieważ jest to kopia asynchronicznego.

##### <a name="disadvantages"></a>Wady
* Gdy używane są pule magazynu systemu Windows, brak przestoju klastra podczas hello pełnej weryfikacji klastra dla hello nowe dodatkowe węzły.
* W zależności od hello wersja programu SQL Server oraz hello istniejących liczby replik pomocniczych, możesz nie być możliwe tooadd więcej replikach pomocniczych bez usuwania istniejących replik pomocniczych.
* Może być długi czas transferu danych SQL podczas konfigurowania hello pomocnicze bazy danych.
* Brak dodatkowych kosztów podczas migracji, gdy zostały uruchomione równolegle nowej maszyny.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Migrowanie tooa nowy zawsze na klaster
Kolejną strategią jest toocreate całkowicie nowe zawsze na klastrze z całkiem nowe węzły w nową usługę w chmurze, a następnie toouse klientom Witaj przekierowania go.

##### <a name="points-of-downtime"></a>Punkty przestoju
Brak przestoju podczas przenoszenia aplikacji i użytkowników toohello nowe zawsze na odbiornika. Przestój Hello zależy od:

* Witaj czas toodatabases kopie zapasowe dziennika transakcji końcowej toorestore na nowych serwerach.
* Hello czas tooupdate klienta aplikacji toouse nowe zawsze na odbiornika.

##### <a name="advantages"></a>Zalety
* Można przetestować środowiska produkcyjnego rzeczywiste hello, SQL Server, a zmiany kompilacji systemu operacyjnego.
* Masz hello opcja toocustomize hello magazynu i toopotentially zmniejszyć rozmiar maszyny wirtualnej. Może to spowodować zmniejszenie kosztów.
* W trakcie tego procesu można aktualizacji kompilacji programu SQL Server lub wersji. Możesz również uaktualnić hello systemu operacyjnego.
* powitalne poprzedniego zawsze na klastra może działać jako cel stałe wycofywania.

##### <a name="disadvantages"></a>Wady
* Należy nazwę DNS hello toochange hello odbiornika, jeśli chcesz, aby obie zawsze na klastry z systemem jednocześnie. Spowoduje to dodanie administracji obciążenie podczas migracji hello jako ciągi aplikacji klienta musi odzwierciedlać nową nazwę odbiornika hello.
* Musisz zaimplementować mechanizm synchronizacji między dwa tookeep środowisk hello, zamknij je jako jako możliwych toominimize hello wykonana końcowa synchronizacja wymagania przed migracją.
* Zostanie dodany koszt podczas migracji ma hello nowego środowiska uruchamiania.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migrowanie zawsze na wdrożeń minimalizująca przestoje
Minimalizująca przestoje istnieją dwa strategii migracji wdrożeń zawsze włączone:

1. **Korzystanie z istniejących pomocniczy: pojedynczej lokacji**
2. **Korzystanie z istniejących dodatkowej Replica(s): obejmujący wiele lokacji**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Korzystanie z istniejących pomocniczy: pojedynczej lokacji
Jedną ze strategii minimalizująca przestoje jest tootake istniejącej chmurze dodatkowej i usunąć go z hello bieżącej usługi w chmurze. Następnie skopiuj hello wirtualne dyski twarde toohello nowe konto magazynu Premium i Utwórz hello maszyny Wirtualnej w hello nową usługę w chmurze. Następnie zaktualizuj odbiornika hello w klaster i pracy awaryjnej.

##### <a name="points-of-downtime"></a>Punkty przestoju
* Brak przestoju podczas aktualizowania hello ostatni węzeł z punktem końcowym hello o zrównoważonym obciążeniu.
* Ponowne połączenie z klienta może być opóźnione w zależności od konfiguracji klienta/serwera DNS.
* Jeśli wybierzesz tootake hello zawsze na klastrze grupy w trybie offline tooswap się adresy IP hello jest dodatkowy Przestój. Można tego uniknąć przy użyciu zależności lub i możliwych właścicieli hello dodany adres IP. W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Witaj toopartake dodanego węzła w jako zawsze na partnerski trybu Failover, należy należy tooadd punktu końcowego platformy Azure z toohello odwołania, ustaw równoważenia obciążenia. Po uruchomieniu hello **AzureEndpoint Dodaj** polecenia toodo tego bieżącego tooremain połączenia, Otwórz, ale nowych połączeń toohello odbiornika nie będzie możliwe toobe do czasu hello modułu równoważenia obciążenia został zaktualizowany. Podczas testowania to widziany toolast 90-120seconds, to powinno zostać przetestowana.
>
>

##### <a name="advantages"></a>Zalety
* Bez dodatkowych kosztów ponoszonych podczas migracji.
* Jeden do jednego migracji.
* Złożoności.
* Pozwala na zwiększenie IOPS przez jednostki SKU magazynu Premium. Jeśli strona 3rd hello dyski są odłączone od hello maszyny Wirtualnej i skopiowany toohello nową usługę w chmurze, narzędzie może być rozmiaru wirtualnego dysku twardego hello tooincrease używane, co zapewnia wyższej przepustowości. Aby zwiększyć rozmiar wirtualnego dysku twardego, zobacz [dyskusjach prowadzonych na forum](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Wady
* Podczas migracji jest do tymczasowej utraty wysokiej dostępności i odzyskiwania po awarii.
* Jak jest to migracji 1:1, konieczne będzie toouse minimalny rozmiar maszyny Wirtualnej, która będzie obsługiwać numer wirtualne dyski twarde, więc może nie być możliwe toodownsize maszyn wirtualnych.
* W tym scenariuszu użyje hello Azure **Start AzureStorageBlobCopy** polecenia, które jest asynchroniczne. Na zakończenie kopiowania nie ma żadnych umowy SLA. czas Hello kopii hello różni się podczas zależy to od oczekiwania w kolejce, również będą zależą hello ilość danych tootransfer. czas kopiowania Hello zwiększa hello transfer jest zazwyczaj tooanother centrum danych Azure, który obsługuje magazyn w warstwie Premium w innym regionie. Jeśli masz tylko węzły 2, należy wziąć pod uwagę możliwe środki zaradcze w przypadku kopiowania hello trwa dłużej niż w trakcie testów. Może to być powitania po pomysłów.
  * Dodać tymczasowego 3 węzła programu SQL Server dla wysokiej dostępności, przed migracją hello uzgodnionych przestojów.
  * Uruchom migrację hello poza Azure zaplanowanej konserwacji.
  * Upewnij się, że zostały prawidłowo skonfigurowane z kworum klastra.  

##### <a name="high-level-steps"></a>Ogólne kroki
Ten dokument nie wykazują jest przykład tooend pełną zakończenia jednak hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) zawiera szczegółowe informacje, które można wykorzystać tooperform, to.

![MinimalDowntime][8]

* Zbieranie konfiguracji dysku i Usuń węzeł hello (nie należy usuwać dołączonych dysków VHD).
* Utwórz konto magazynu Premium i skopiuj wirtualne dyski twarde z hello konta magazynu w warstwie standardowa
* Utwórz nową usługę w chmurze i wdrożenie hello SQL2 maszyny Wirtualnej w tej usłudze w chmurze. Utwórz hello maszyny Wirtualnej przy użyciu hello skopiowane oryginalny wirtualny dysk twardy systemu operacyjnego i dołączanie hello skopiowane wirtualne dyski twarde.
* Skonfiguruj ILB / ELB i dodać punkty końcowe.
* Aktualizacja odbiornika przez:
  * Biorąc hello zawsze w grupie w trybie offline i aktualizowania hello zawsze na odbiornik o nowe ILB / adresu ELB IP.
  * Lub dodawanie zasobu adresu IP hello z nowego chmury usługi ILB/ELB za pomocą programu PowerShell do klastra systemu Windows. Następnie zestaw hello możliwych właścicieli hello adresu IP zasobu toohello migracji węzła, SQL2 i Ustaw jako zależności lub w hello nazwy sieciowej. W sekcji hello "Dodawanie zasobu adresu IP w tej samej podsieci" hello [dodatku](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Sprawdź klientów toohello propagowania/konfiguracji DNS.
* Migrowanie maszyny Wirtualnej SQL1 i kroków 2 – 4.
* Jeśli przy użyciu kroków 5ii, Dodaj SQL1 możliwych właścicieli dla hello dodawania zasobu adresu IP
* Testy trybu failover.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Korzystanie z istniejących dodatkowej replica(s): obejmujący wiele lokacji
Jeśli niektóre węzły w więcej niż jednego centrum danych Azure (DC) lub w przypadku środowiska hybrydowego, można użyć konfiguracji zawsze włączone, w tym przestoju toominimize środowiska.

Metoda Hello jest toochange hello zawsze włączony synchronizacja tooSynchronous lokalne powitania lub dodatkowej Azure kontrolera domeny, a następnie trybu failover za pośrednictwem toothat programu SQL Server. Następnie skopiuj hello wirtualne dyski twarde tooa konta Premium Storage i Wdróż ponownie hello maszyny do nowej usługi w chmurze. Zaktualizuj hello odbiornika, a następnie wykonaj powrót po awarii.

##### <a name="points-of-downtime"></a>Punkty przestoju
Przestój Hello składa się z hello czasu toofailover toohello zamiast kontrolera domeny i z powrotem. Zależy także od konfiguracji klienta/serwera DNS i ponowne połączenie z klienta mogą być opóźnione.
Należy wziąć pod uwagę hello poniższy przykład hybrydowego zawsze w konfiguracji:

![MultiSite1][9]

##### <a name="advantages"></a>Zalety
* Można korzystać z istniejącej infrastruktury.
* Najpierw mieć hello opcji uaktualniania toopre hello magazynu Azure na hello DR Azure kontrolera domeny.
* można tak skonfigurować Hello magazynu DR Azure kontrolera domeny.
* Brak co najmniej dwóch przechodzenia w tryb failover podczas migracji, wyłączając testowy tryb failover.
* Nie należy toomove danych programu SQL Server z kopii zapasowej i przywracania.

##### <a name="disadvantages"></a>Wady
* W zależności od tooSQL dostępu klienta serwera może występować większe opóźnienia, gdy serwer SQL jest uruchomiony w aplikacji alternatywnych toohello kontrolera domeny.
* Hello czasu kopiowania wirtualnych dysków twardych tooPremium przechowywania może trwać długo. Może to mieć wpływ na na decyzję dotyczącą tego, czy tookeep hello węzła w hello grupy dostępności. Należy wziąć pod uwagę to po dziennika pracy intensywnych obciążeń uruchomionych podczas migracji hello jest wymagane, ponieważ węzeł podstawowy hello będzie mieć tookeep hello Niezreplikowane transakcje w jego dzienniku transakcji. W związku z tym to można powiększać znacznie.
* W tym scenariuszu użyje hello Azure **Start AzureStorageBlobCopy** polecenia, które jest asynchroniczne. Na zakończenie nie ma żadnych umowy dotyczącej poziomu usług. Witaj czasu kopii hello różni się podczas zależy to od oczekiwania w kolejce, również będzie zależeć hello ilość tootransfer danych. W związku z tym istnieje tylko jeden węzeł 2 centrum danych, należy podjąć kroki zaradcze w przypadku kopiowania hello trwa dłużej niż w trakcie testów. Może to być powitania po pomysłów.
  * Dodaj węzeł tymczasowy SQL 2 dla HA przed migracją hello uzgodnionych przestojów.
  * Uruchom migrację hello poza Azure zaplanowanej konserwacji.
  * Upewnij się, że zostały prawidłowo skonfigurowane z kworum klastra.

W tym scenariuszu założono, że udokumentowanych instalacji i wiedzieć odwzorowania hello magazynu w kolejności toomake zmiany ustawień pamięci podręcznej dysku optymalne.

##### <a name="high-level-steps"></a>Ogólne kroki
![Multisite2][10]

* Upewnij się, hello lokalnymi / alternatywny hello Azure kontrolera domeny głównej serwera SQL i dołączyć je hello innych automatycznej pracy awaryjnej partnera (AFP).
* Zbierz informacje o konfiguracji dysków z SQL2 i Usuń węzeł hello (nie należy usuwać dołączonych dysków VHD).
* Utwórz konto magazynu Premium i skopiuj wirtualne dyski twarde z hello konta Standard Storage.
* Utwórz nową usługę w chmurze a hello SQL2 maszyny Wirtualnej z jej dołączone dyski magazynu dodatków.
* Skonfiguruj ILB / ELB i dodać punkty końcowe.
* Aktualizacja hello zawsze na odbiornik o nowe ILB / ELB IP adres i testowania trybu failover.
* Sprawdź konfigurację DNS hello.
* Zmień hello AFP tooSQL2 migracji SQL1 i przejść przez kroki od 2 do 5.
* Testy trybu failover.
* Przełącz hello AFP tooSQL1 Wstecz i SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Dodatek: Migrowanie tooPremium wdrożenia w wielu lokacjach zawsze na klaster Magazyn
Witaj pozostałej części tego tematu zawiera szczegółowy przykład konwersji obejmujący wiele lokacji zawsze na tooPremium magazynu klastra. Ponadto konwertuje hello odbiornika z za pomocą zewnętrznego obciążenia (ELB) usługi równoważenia tooan wewnętrznego modułu równoważenia obciążenia (ILB).

### <a name="environment"></a>Środowisko
* Windows 2k 12 / SQL 2k 12
* Pliki 1 DB na SP
* 2 x pule magazynu w każdym węźle

![Appendix1][11]

### <a name="vm"></a>MASZYNY WIRTUALNEJ:
W tym przykładzie zamierzamy toodemonstrate przenoszenie z tooILB ELB. ELB nie była dostępna przed ILB, więc ten pokazuje, jak toothis tooswitch podczas hello migracji.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>Kroki przed: TooSubscription połączyć
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Krok 1: Utwórz nowe konto magazynu i usługa w chmurze
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Krok 2: Zwiększ hello dozwolonych błędów na zasoby<Optional>
W niektórych zasobów, które należą tooyour zawsze włączonej grupy dostępności, istnieją ograniczenia na liczbę błędów, które mogą wystąpić w okresie, w którym usługa klastrowania hello podejmie grupy zasobów hello toorestart. Zaleca się, że możesz zwiększyć to o ile Instruktaż tej procedury, ponieważ w przeciwnym razie ręcznie trybu failover i wyzwalacza przechodzenia w tryb failover przez zamknięcie maszyny można uzyskać limit toothis Zamknij.

Będzie go można toodouble rozsądne hello awarii dodatku, toodo to w Menedżerze klastra trybu Failover, przejdź toohello właściwości hello zawsze włączone grupy zasobów:

![Appendix3][13]

Zmień hello too6 maksymalna liczba awarii.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Krok 3: Dodawanie adresu IP zasobu dla grupy klastra<Optional>
Jeśli masz tylko jeden adres IP dla hello Grupa klastra i jest wyrównany toohello chmury podsieci, należy pamiętać, jeśli przypadkowo w tryb offline wszystkich węzłów klastra w chmurze hello czy sieci, a następnie hello IP klastra zasobu i nazwa sieciowa klastra nie będzie możliwe toocome online. W hello zdarzenia o tym, które uniemożliwi aktualizuje tooother zasobów klastra.

#### <a name="step-4-dns-configuration"></a>Krok 4: Konfiguracja DNS
tooimplement przejścia zależy od tego, jak DNS są wykorzystywane i zaktualizować.
Zawsze włączone jest zainstalowany, tworzy grupy zasobów klastra z systemem Windows, otwórz Menedżera klastra trybu Failover, będzie mógł przeglądać czy co najmniej trzy zasoby będą dostępne, Witaj dwie hello dokument odwołuje się tooare:

* Wirtualnej nazwy sieciowej (VNN) — jest to hello DNS nazwy tego klienta połączenia toowhen pożądane tooSQL tooconnect serwerach za pośrednictwem zawsze włączone.
* Zasób adres IP — jest hello adresów IP skojarzonych z hello VNN, może mieć więcej niż jeden, i w wielu lokacjach konfiguracji będzie mieć adres IP według podsieci/lokacji.

Podczas łączenia tooSQL serwera i sterownik SQL Server Client hello będzie pobrać rekordy DNS hello skojarzone z odbiornika hello i spróbuj tooconnect tooeach zawsze na skojarzony adres IP, poniżej omówiono niektóre czynników, które wpływają na to.

Hello liczba równoczesnych rekordy DNS, które są skojarzone z nazwą odbiornika hello zależy nie tylko hello liczba adresów IP skojarzonych, ale hello "RegisterAllIpProviders'setting w klastrze trybu Failover dla hello zawsze ON VNN zasobów.

Podczas wdrażania zawsze na platformie Azure istnieją inne czynności toocreate hello odbiornika i adresy IP, są toomanually skonfigurować too1 "RegisterAllIpProviders" hello, to jest wdrożenie zawsze na lokalnej różnych tooan gdzie too1 jest już ustawiona.

Jeśli "RegisterAllIpProviders" ma wartość 0, a następnie zostanie wyświetlony tylko jeden rekord DNS w systemie DNS skojarzone z hello odbiornika:

![Appendix4][14]

Jeśli 'RegisterAllIpProviders' to 1:

![Appendix5][15]

Poniższy kod Hello będzie zrzutu limit hello VNN ustawienia i ustaw ją automatycznie, należy Uwaga dla hello zmienić efekt tootake należy tootake hello VNN w trybie offline i włącz je ponownie w trybie online, biorąc to pod hello odbiornika w trybie offline powoduje klienta łączności przerw w działaniu.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

W kolejnych kroków migracji konieczne będzie tooupdate hello zawsze na odbiornik o aktualizacja adresu IP, który będzie odwoływać się do modułu równoważenia obciążenia, te obejmują usunięcie zasobu adresu IP i dodawania. Po aktualizacji IP hello należy tooensure hello nowy adres IP został zaktualizowany w strefie DNS i klientom Witaj aktualizowania ich lokalnej pamięci podręcznej DNS.

Jeśli klienci znajdują się w segmencie inną sieć i referencyjne z innego serwera DNS, należy tooconsider, co się stanie o Transfer strefy DNS podczas migracji hello jako hello aplikacji ponownego połączenia czas będzie ograniczone przez co najmniej hello czas transferu strefy żadnych nowych adresów IP dla odbiornika hello. Podlegają ograniczenia czasu, w tym miejscu, należy omówienia i przetestować wymuszania przyrostowy transfer strefy z zespołów systemu Windows, i również umieścić hello DNS tooa rekordów hosta zmniejszyć czasu tooLive (TTL), z więc klientom Witaj aktualizację. Aby uzyskać więcej informacji, zobacz [przyrostowych transferów stref](https://technet.microsoft.com/library/cc958973.aspx) i [Start DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Witaj domyślny czas TTL rekord DNS, który jest skojarzony z hello odbiornika zawsze na platformie Azure to 1200 sekund. Możesz tooreduce to jeśli podczas aktualizacji klientom Witaj tooensure migracji adresu ich DNS hello zaktualizowane protokołu IP dla odbiornika hello podlegają ograniczenia czasu. Możesz wyświetlić i zmodyfikować konfigurację hello przez zrzucanie limit konfiguracji hello hello VNN:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Należy pamiętać, hello niższe hello "HostRecordTTL" wyższy stopień ruch DNS zostanie przeprowadzona.

##### <a name="client-application-settings"></a>Ustawienia aplikacji klienta
Jeśli Twoje aplikacja obsługuje klienta SQL hello .net 4.5 SQLClient, możesz użyć "MULTISUBNETFAILOVER = TRUE" — słowo kluczowe, jest to zalecane toobe stosowane zgodnie z umożliwia szybsze połączenia tooSQL zawsze włączonej grupy dostępności podczas pracy awaryjnej. Wylicza wszystkie adresy IP skojarzone z hello zawsze na odbiornika równolegle i wykonuje skuteczniejsze szybkość ponów próbę połączenia TCP w trybie failover.

Aby uzyskać więcej informacji na temat ustawień hello powyżej, zobacz [MultiSubnetFailover — słowo kluczowe i skojarzonych z funkcji](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Zobacz też [SqlClient obsługę wysokiej dostępności, odzyskiwania po awarii](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Krok 5: Ustawienia kworum klastra
Jak ma toobe pobieranie co najmniej jeden serwer SQL nie działa w czasie, należy zmodyfikować konfigurację kworum klastra hello, jeśli za pomocą monitora udziału plików (FSW) z węzłami 2, należy ustawić Większość węzłów tooallow kworum hello i korzystać z dynamicznych głosowania, a to tooallow dla stałą tooremain jednego węzła.

    Set-ClusterQuorum -NodeMajority  

Aby uzyskać więcej informacji dotyczących zarządzania oraz konfigurowania kworum klastra hello, zobacz [Konfigurowanie i zarządzanie kworum w klastrze pracy awaryjnej systemu Windows Server 2012 hello](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Krok 6: Wyodrębnianie istniejące punkty końcowe i listy kontroli dostępu
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Zapisz te tooa plik tekstowy.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Krok 7: Zmień partnerskich trybu Failover i tryby replikacji
Jeśli masz więcej niż 2 serwery SQL, możesz zmienić hello pracy awaryjnej, innym pomocniczej w innego kontrolera domeny lub too'Synchronous lokalnymi i nadać mu automatycznego partnera pracy awaryjnej (AFP), jest więc zachowują HA podczas wprowadzania zmian. Można to zrobić przy użyciu języka TSQL z jednak modyfikować SSMS:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Krok 8: Usuń dodatkowej maszyny Wirtualnej z usługi w chmurze
Należy się przygotować toomigrate chmury węzła pomocniczego, jeśli jest to obecnie podstawowego, powinien zainicjowaniu ręcznego przełączania trybu failover.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Krok 9: Zmień ustawienia w pliku CSV pamięci podręcznej dysku i Zapisz
Woluminy danych te należy ustawić tooREADONLY.

W przypadku woluminów TLOG te należy ustawić tooNONE.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Krok 10: Kopiowanie dysków VHD
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Można sprawdzić stan kopiowania hello hello wirtualne dyski twarde toohello konta Premium Storage:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Poczekaj, aż wszystkie one są rejestrowane jako Powodzenie.

Aby uzyskać informacje dotyczące poszczególnych obiektów blob:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Krok 11: Dysk systemu operacyjnego rejestru
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Krok 12: Zaimportuj dodatkowej do nowej usługi w chmurze
Kod Hello poniżej również używa hello dodać opcję tutaj można zaimportować maszynę hello i korzystać z hello retainable adresu VIP.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Krok 13: Tworzenie ILB na nowe usługi chmury, Dodaj obciążenia zrównoważonym punktów końcowych i listy kontroli dostępu
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Krok 14: Zawsze aktualizacji
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Teraz Usuń hello starego usługi w chmurze adresu IP.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Krok 15: Sprawdzanie aktualizacji DNS
Teraz należy sprawdzić serwery DNS w sieci klienta programu SQL Server i upewnij się, że klaster został dodany hello rekord hosta dodatkowe hello dodany adres IP. Jeśli te serwery DNS nie zostały zaktualizowane, należy wziąć pod uwagę wymuszania transferu strefy DNS i upewnij się, że hello klienci w podsieci są możliwe tooresolve tooboth zawsze na adresy IP, jest więc nie trzeba toowait automatyczne replikacja DNS.

#### <a name="step-16-reconfigure-always-on"></a>Krok 16: Skonfiguruj ponownie zawsze na
W tym momencie poczekać hello dodatkowej tego węzła, który był migrowanych toofully ponownego zsynchronizowania jej z węzła lokalne powitania przełącznika toosynchronous węzła replikacji i stał się hello AFP.  

#### <a name="step-17-migrate-second-node"></a>Kroku 17: Drugi węzeł migracji
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Krok 18: Zmień ustawienia w pliku CSV pamięci podręcznej dysku i Zapisz
Woluminy danych te należy ustawić tooREADONLY.

W przypadku woluminów TLOG te należy ustawić tooNONE.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Krok 19: Utwórz nowe konto magazynu niezależnie od przypadku węzła pomocniczego
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Krok 20: Kopiowanie dysków VHD
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Można sprawdzić stan kopiowania hello wirtualnego dysku twardego dla wszystkich dysków VHD: ForEach ($disk w $diskobjects) {$lun = $disk. Jednostka LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Etykieta_dysku $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Poczekaj, aż wszystkie one są rejestrowane jako Powodzenie.

Aby uzyskać informacje dotyczące poszczególnych obiektów blob:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Krok 21: Dysk rejestru systemu operacyjnego
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Krok 22: Dodawanie obciążenia zrównoważonym punktów końcowych i listy kontroli dostępu
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Krok 23: Test trybu failover
Należy umożliwiają teraz węzła migrowanych hello synchronizacji z lokalnymi hello zawsze na węźle, umieść go w tryb replikacji toosynchronous i poczekaj, aż został zsynchronizowany. Następnie w tryb failover z lokalnego toohello pierwszego węzła migracji, która jest hello AFP. Po którym pracuje, zmień hello ostatnio migracji AFP toohello węzła.

Należy testy trybu failover pomiędzy wszystkimi węzłami i uruchamiania, ale oczekiwano testy chaos tooensure przechodzenia w tryb failover działa jako i w odpowiednim manor.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Krok 24: Odłożyć ustawienia kworum klastra / czas wygaśnięcia DNS / Pntrs pracy awaryjnej / ustawienia synchronizacji
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Dodawanie zasobu adresu IP na tej samej podsieci
Jeśli masz tylko 2 serwery SQL i chcesz toomigrate ich tooa nowe usługi chmury, ale mają tookeep hello ich w tej samej podsieci, można uniknąć, biorąc hello odbiornika zawsze w trybie offline toodelete hello oryginalnego adresu IP i dodać hello nowego adresu IP. W przypadku migracji hello maszyn wirtualnych tooanother podsieci, nie należy toodo to sposób będzie sieć dodatkowe klastra, która będzie odwoływać się do tej podsieci.

Po ma włączane hello migracji pomocniczy, a także dodać hello nowego adresu IP zasobu hello nową usługę w chmurze przed trybu failover hello istniejącą główną, należy wykonać następujące czynności, w ramach hello Menedżera klastra trybu Failover:

tooadd adres IP, zobacz hello [dodatku](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), krok 14.

1. Hello bieżącego adresu IP zasobu, można zmienić w too'Existing możliwych właścicieli hello podstawowego serwera SQL ", w przykładzie hello poniżej"dansqlams4":

    ![Appendix13][23]
2. Hello nowego adresu IP zasobu, można zmienić w too'Migrated możliwych właścicieli hello pomocniczym programu SQL Server ", w przykładzie hello poniżej"dansqlams5":

    ![Appendix14][24]
3. Gdy ta opcja jest ustawiona można trybu failover i w przypadku migrowania hello ostatniego węzła hello możliwych właścicieli można edytować, że węzeł zostanie dodany jako możliwego właściciela:

    ![Appendix15][25]

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Magazyn w warstwie Premium systemu Azure](../../../storage/common/storage-premium-storage.md)
* [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
