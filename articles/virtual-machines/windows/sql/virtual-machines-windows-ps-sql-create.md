---
title: aaaCreate maszyny wirtualnej programu SQL Server w programie Azure PowerShell (Resource Manager) | Dokumentacja firmy Microsoft
description: "Zawiera kroki i skryptów programu PowerShell do tworzenia maszyny Wirtualnej platformy Azure z obrazów Galeria maszyny wirtualnej programu SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu programu Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak hello toocreate jednej maszyny wirtualnej platformy Azure przy użyciu **usługi Azure Resource Manager** modelu wdrażania przy użyciu poleceń cmdlet programu Azure PowerShell. W tym samouczku utworzymy jednej maszyny wirtualnej za pomocą pojedynczego dysku z obrazu w hello galerii SQL. Zostanie utworzony nowy dostawców dla hello magazynu, sieci i zasoby obliczeniowe, które będą używane przez maszynę wirtualną hello. Jeśli masz istniejące dostawców dla każdego z tych zasobów, można użyć tych dostawców.

Należy hello klasycznej wersji w tym temacie, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu usługi Azure PowerShell klasycznego](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku potrzebne są:

* Konto platformy Azure i subskrypcji przed jego uruchomieniem. Jeśli nie masz, zaloguj się do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* [Program Azure PowerShell)](/powershell/azure/overview), minimalna wersja 1.4.0 lub nowszy (w tym samouczku napisane przy użyciu wersji 1.5.0).
  * tooretrieve Twojej wersji, typ **flagą Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Skonfiguruj subskrypcję
Otwórz program Windows PowerShell i ustanowienia tooyour dostępu do konta platformy Azure, uruchamiając następujące polecenie cmdlet hello. Zostaną wyświetlone z logowaniem tooenter ekranu swoje poświadczenia. Użyj hello sam adres e-mail i hasło, użyj toosign w toohello portalu Azure.

    Add-AzureRmAccount

Po pomyślnym zalogowaniu zobaczysz niektóre informacje na ekranie, zawierającą SubscriptionId hello, z którym użytkownik zalogowany. Jest to hello subskrypcji, w którym zostaną utworzone zasoby hello w tym samouczku, chyba że zostanie zmienione tooa innej subskrypcji. Jeśli masz wiele SubscriptionIds, uruchom następujące polecenie cmdlet tooreturn hello listę wszystkich SubscriptionIds Twojego:

    Get-AzureRmSubscription

Uruchom następujące polecenie cmdlet z Twojej żądany identyfikator subskrypcji hello tooanother toochange SubscriptionID.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Zdefiniuj zmienne obrazu
toosimplify użyteczność i zrozumienia ukończyć powitalnych skryptu z tego samouczka Rozpoczniemy, definiując liczba zmiennych. Zmień wartości parametrów hello, ale należy wziąć pod nazewnictwa długości pokrewne tooname ograniczenia i znaków specjalnych podczas modyfikowania hello wartości.

### <a name="location-and-resource-group"></a>Lokalizacji i grupy zasobów
Użyj dwóch zmiennych toodefine hello danych regionu i hello grupy zasobów w której zostanie utworzona hello inne zasoby dotyczące hello maszyny wirtualnej.

Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Magazyn właściwości
Użyj hello następujące zmienne toodefine hello konta i hello typ magazynu używanych przez maszynę wirtualną hello toobe magazynu.

Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych. Należy pamiętać, że w tym przykładzie używamy [magazyn w warstwie Premium](../../../storage/common/storage-premium-storage.md), który jest zalecane w przypadku obciążeń produkcyjnych. Aby uzyskać więcej informacji na ten wskazówki i inne zalecenia, zobacz [wydajności najlepsze rozwiązania dotyczące programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Właściwości sieci
Użyj powitania po interfejsu sieciowego hello toodefine zmienne, Metoda alokacji TCP/IP hello, hello wirtualnej nazwy sieciowej, Nazwa podsieci wirtualnej hello, hello zakres adresów IP dla sieci wirtualnej hello, hello zakres adresów IP podsieci hello i hello używanej przez sieć hello w maszynie wirtualnej hello toobe etykieta nazwy domeny publicznej.

Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Właściwości maszyny wirtualnej
Użyj następującego nazwę maszyny wirtualnej hello toodefine zmienne, nazwę komputera hello hello rozmiar maszyny wirtualnej i hello nazwa dysku systemu operacyjnego dla maszyny wirtualnej hello hello.

Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Właściwości obrazu
Użyj hello następujące zmienne toodefine hello obrazu toouse hello maszyny wirtualnej. W tym przykładzie obraz programu SQL Server 2016 Enterprise hello jest używany.

Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Należy pamiętać, że można uzyskać pełną listę ofert obrazu programu SQL Server za pomocą polecenia Get-AzureRmVMImageOffer hello:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

Aby zobaczyć hello dostępne oferty, za pomocą polecenia Get-AzureRmVMImageSku hello jednostki SKU. Witaj następujące polecenie zawiera wszystkie jednostki SKU, które są dostępne dla hello **SQL2014SP1 WS2012R2** oferty.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Z modelu wdrażania usługi Resource Manager hello pierwszy obiekt hello, tworzona jest hello grupy zasobów. Używamy hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate polecenia cmdlet, grupy zasobów platformy Azure i jej zasobach z zasobem hello grupy nazwy i lokalizacji zdefiniowane przez hello zmiennych, które zostały wcześniej zainicjowane.

Wykonaj następujące polecenie cmdlet toocreate hello nowej grupy zasobów.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
maszyny wirtualnej Hello wymaga zasobów magazynu hello dysku systemu operacyjnego oraz hello danych programu SQL Server i plików dziennika. Dla uproszczenia utworzymy jednego dysku dla obu. Możesz dołączyć dodatkowe dyski później za pomocą hello [dysku Azure Dodaj](/powershell/module/azure/add-azuredisk) polecenia cmdlet w kolejności tooplace danych programu SQL Server i pliki dziennika w dedykowanych dysków. Używamy hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate polecenia cmdlet magazynu w warstwie standardowa konta w nowej grupy zasobów oraz nazwy konta magazynu hello, nazwa jednostki Sku magazynu i lokalizacja zdefiniowane przy użyciu zmiennych hello wcześniej zainicjowana.

Wykonaj następujące polecenie cmdlet toocreate hello nowego konta magazynu.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Maszyna wirtualna Hello wymaga liczba zasobów sieciowych do obsługi łączności sieciowej.

* Każda maszyna wirtualna wymaga sieci wirtualnej.
* Sieć wirtualna musi mieć co najmniej jedną podsieć zdefiniowane.
* Interfejs sieciowy musi być zdefiniowany publiczny lub prywatny adres IP.

### <a name="create-a-virtual-network-subnet-configuration"></a>Tworzenie konfiguracji podsieci sieci wirtualnej
Firma Microsoft będzie Rozpocznij od utworzenia konfiguracji podsieci dla naszych sieci wirtualnej. W naszym samouczku utworzymy podsieci domyślnej przy użyciu hello [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) polecenia cmdlet. Utworzymy naszych konfiguracji podsieci sieci wirtualnej z hello nazwy i adresu prefiks podsieci zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.

> [!NOTE]
> Można zdefiniować dodatkowe właściwości konfiguracji podsieci sieci wirtualnej hello za pomocą tego polecenia cmdlet, ale która wykracza poza zakres tego samouczka hello.
>
>

Wykonaj następujące polecenia cmdlet toocreate hello konfiguracji podsieci wirtualnej.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Następnie utworzymy naszych sieci wirtualnej przy użyciu hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) polecenia cmdlet. W tej nowej grupy zasobów o nazwie hello, lokalizacji i prefiksu adresu zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane i konfiguracji podsieci hello zdefiniowaną w poprzednim kroku hello utworzymy naszych sieci wirtualnej.

Wykonaj następujące polecenia cmdlet toocreate hello sieci wirtualnej.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Utwórz hello publicznego adresu IP
Teraz, gdy mamy naszych sieci wirtualnej zdefiniowane potrzebujemy tooconfigure adresu IP dla maszyny wirtualnej toohello łączności. W tym samouczku utworzymy publiczny adres IP za pomocą dynamicznego adresu IP, adresy toosupport łączności z Internetem. Używamy hello [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress) polecenia cmdlet toocreate hello publicznego adresu IP w prevously utworzoną grupę zasobów hello oraz hello nazwy, lokalizacji, Metoda alokacji i etykieta nazwy domeny DNS zdefiniowane przy użyciu hello zmienne, które zostały wcześniej zainicjowane.

> [!NOTE]
> Można zdefiniować dodatkowe właściwości hello publicznego adresu IP za pomocą tego polecenia cmdlet, ale która wykracza poza zakres hello tego samouczka początkowej. Można również utworzyć za pomocą statycznego adresu prywatny adres lub adres, ale jest to poza zakresem hello tego samouczka.
>
>

Wykonaj następujące polecenie cmdlet toocreate hello publicznego adresu IP.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Utwórz hello interfejsu sieciowego
Teraz możemy toocreate gotowy interfejs sieciowy hello, używanego przez naszych maszyny wirtualnej. Używamy hello [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate polecenia cmdlet naszych interfejsu sieciowego w grupie zasobów hello utworzonego wcześniej i o nazwie hello, lokalizacji, podsieci i publicznego adresu IP wcześniej zdefiniowany.

Wykonaj następujące polecenia cmdlet toocreate hello interfejsu sieciowego.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Konfigurowanie obiektu maszyny Wirtualnej
Teraz, gdy mamy magazynu i zasobów sieciowych zdefiniowanych możemy gotowe toodefine zasoby obliczeniowe dla maszyny wirtualnej hello. W naszym samouczku firma Microsoft będzie określić różne właściwości systemu operacyjnego i hello rozmiar maszyny wirtualnej, określ hello interfejsu sieciowego, który wcześniej utworzony, zdefiniuj magazynu obiektów blob, a następnie określ hello dysku systemu operacyjnego.

### <a name="create-hello-vm-object"></a>Utwórz hello obiektu maszyny Wirtualnej
Firma Microsoft zostanie uruchomiony, określając hello rozmiar maszyny wirtualnej. W tym samouczku będziemy określania DS13. Używamy hello [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate polecenia cmdlet obiektu można skonfigurować maszyny wirtualnej o nazwie hello i rozmiar zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.

Wykonaj następujące polecenia cmdlet toocreate hello maszyny wirtualnej obiekt hello.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Utwórz poświadczenia obiektu toohold hello nazwę i hasło dla hello poświadczenia administratora lokalnego
Zanim firma Microsoft można ustawić właściwości systemu operacyjnego hello hello maszyny wirtualnej, potrzebujemy toosupply hello poświadczenia dla konta administratora lokalnego hello jako bezpieczny ciąg. tooaccomplish, użyjemy hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.

Wykonaj następujące polecenie cmdlet hello i w hello okno żądanie poświadczeń programu Windows PowerShell, wpisz hello toouse nazwę i hasło dla konta administratora lokalnego hello w maszynie wirtualnej Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Ustaw właściwości systemu operacyjnego hello hello maszyny wirtualnej
Teraz możemy gotowe tooset hello właściwości maszyny wirtualnej w system operacyjny. Używamy hello [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) polecenia cmdlet tooset hello typu systemu operacyjnego Windows, wymagają hello [agenta maszyny wirtualnej](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe zainstalowane, określ to polecenie cmdlet hello umożliwia automatyczne Zaktualizuj i ustawić hello nazwę maszyny wirtualnej, hello nazwy komputera i poświadczeń hello przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.

Wykonanie hello następujące polecenia cmdlet tooset hello systemu operacyjnego właściwości maszyny wirtualnej.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Dodaj maszynę wirtualną toohello hello sieciowych — Interfejs
Następnie dodamy hello interfejsu sieciowego, że utworzono wcześniej toohello maszyny wirtualnej. Używamy hello [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) polecenia cmdlet tooadd hello interfejsu sieciowego przy użyciu zmiennej hello interfejsu sieci, wcześniej zdefiniowany.

Wykonanie hello następującego polecenia cmdlet tooset hello sieciowej dla maszyny wirtualnej.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Ustaw lokalizację magazynu obiektów blob hello hello toobe dysku używane przez maszynę wirtualną hello
Następnie możemy ustawi lokalizację magazynu obiektów blob hello hello toobe dysku używane przez maszynę wirtualną hello za pomocą zmiennych hello, wcześniej zdefiniowane.

Wykonanie powitania od lokalizacji magazynu obiektów blob hello tooset polecenia cmdlet.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Ustaw właściwości dysku dla maszyny wirtualnej hello hello systemu operacyjnego
Następnie możemy ustawi systemu operacyjnego hello właściwości dysku dla maszyny wirtualnej hello. Używamy hello [AzureRmVMOSDisk zestaw](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify polecenia cmdlet, który system operacyjny dla maszyny wirtualnej hello hello będą pobierane z obrazu tooset buforowanie tylko tooread (ponieważ program SQL Server jest instalowany na powitania tego samego dysku) i definiowanie Nazwa maszyny wirtualnej Hello i dysku systemu operacyjnego hello zdefiniowane przy użyciu zmiennych hello zdefiniowanego wcześniej.

Wykonanie hello następującego polecenia cmdlet tooset hello właściwości dysku systemu operacyjnego dla maszyny wirtualnej.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Określ obraz platformy hello hello maszyny wirtualnej
Nasze ostatnim krokiem konfiguracji jest obrazu platformy hello toospecify naszych maszyny wirtualnej. W naszym samouczku używamy hello najnowsze obrazu programu SQL Server 2016 CTP. Używamy hello [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse polecenia cmdlet tego obrazu zgodnie z definicją w zmiennych hello, wcześniej zdefiniowane.

Wykonanie hello następującego polecenia cmdlet toospecify hello platformy obrazu dla maszyny wirtualnej.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Utwórz hello maszyny Wirtualnej SQL
Zakończono hello czynności konfiguracyjne, użytkownik jest maszyny wirtualnej hello toocreate gotowe. Używamy hello [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) polecenia cmdlet toocreate hello maszyny wirtualnej za pomocą zmiennych hello zdefiniowaniu.

Wykonaj następujące polecenia cmdlet toocreate hello maszyny wirtualnej.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

Maszyna wirtualna Hello jest tworzona. Powiadomienie, że dla diagnostyki rozruchu utworzeniu konta magazynu w warstwie standardowa ponieważ hello określono konto magazynu dla maszyny wirtualnej hello dysku to konto magazynu premium.

Możesz teraz przeglądać tej maszyny w hello Azure Portal toosee [publicznego adresu IP i nazwy FQDN](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Przykładowy skrypt
Witaj poniższy skrypt zawiera hello wykonania skryptu programu PowerShell na potrzeby tego samouczka. Przyjęto założenie, że masz już toouse subskrypcji platformy Azure hello Instalatora z hello **Add-AzureRmAccount** i **Select-AzureRmSubscription** poleceń.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Następne kroki
Po utworzeniu maszyny wirtualnej hello jesteś maszyny wirtualnej toohello tooconnect gotowe za pomocą protokołu RDP i ustawienia łączności. Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).

