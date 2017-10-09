---
title: "aaaCreate maszyny wirtualnej platformy Azure za pomocą sieci przyspieszony | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszynę wirtualną za pomocą przyspieszony sieci."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Utwórz maszynę wirtualną za pomocą przyspieszony sieci

Z tego samouczka, dowiesz się, jak toocreate Azure maszyny wirtualnej (VM) za pomocą przyspieszony sieci. Przyspieszone sieci jest GA dla systemu Windows i w publicznej wersji zapoznawczej dla określonych dystrybucje systemu Linux. Przyspieszone sieci umożliwia tooa wirtualizacji (SR-IOV) we/wy z jednym elementem głównym maszyny Wirtualnej, co znacznie poprawia wydajność sieci. Ta ścieżka wysokiej wydajności pomija hello hosta hello ścieżki danych, zmniejszając czas oczekiwania, zakłócenia i użycie procesora CPU do użycia z najbardziej wymagających obciążeń sieci hello na obsługiwanych typów maszyny Wirtualnej. powitania po obraz pokazuje komunikacji między dwóch maszyn wirtualnych (VM) z włączonymi i wyłączonymi przyspieszonego sieci:

![Porównanie](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Bez przyspieszonego sieci hello hosta i przełącznik wirtualny hello musi przejść przez cały ruch sieciowy i hello maszyny Wirtualnej. Przełącznik wirtualny Hello udostępnia wszystkie egzekwowanie zasad, takie jako grupy zabezpieczeń sieci dostęp listy kontroli, izolacji i innych ruchu toonetwork usług wirtualizacją sieci. więcej informacji na temat przełączników wirtualnych, przeczytaj hello toolearn [wirtualizacji sieci funkcji Hyper-V i przełącznik wirtualny](https://technet.microsoft.com/library/jj945275.aspx) artykułu.

Z przyspieszonego w sieci, ruch sieciowy dociera do lokalizacji hello wirtualna interfejsu sieciowego (NIC) i następnie przekazany toohello maszyny Wirtualnej. Wszystkich zasad sieciowych, które hello przełącznik wirtualny ma zastosowanie bez przyspieszonego sieci są Odciążone i sprzętu. Stosowanie zasad w sprzętu umożliwia hello kart tooforward ruch sieciowy bezpośrednio toohello maszyny Wirtualnej, pomijanie hello hosta i przełącznik wirtualny hello, przy zachowaniu wszystkich zasad hello zastosowaniu hello hosta.

Hello zalet przyspieszonego sieci mają zastosowanie tylko toohello maszynę Wirtualną, która jest włączone. Najlepiej hello jest idealny tooenable tę funkcję na co najmniej dwie maszyny wirtualne podłączone toohello tej samej sieci wirtualnej platformy Azure (VNet). Podczas komunikacji między sieciami wirtualnymi lub łączącego lokalnymi, ta funkcja ma minimalny wpływ toooverall opóźnienia.

> [!WARNING]
> To Linux publicznej wersji zapoznawczej nie może mieć hello sam poziom dostępności i niezawodności, jako funkcje, które są zazwyczaj wydanie z dostępnością. Funkcja Hello nie jest obsługiwane, mogą mieć ograniczone możliwości i mogą nie być dostępne we wszystkich lokalizacjach Azure. Najbardziej aktualne powiadomień hello na dostępność i stan tej funkcji Sprawdź hello Azure Virtual Network aktualizacji strony.

## <a name="benefits"></a>Korzyści
* **Zmniejszyć opóźnienia / wyższy pakietów na sekundę (pps):** hello usunięcie przełącznika wirtualnego z hello ścieżki danych usuwa pakiety poświęcić czas hello w hello hosta dla przetwarzanie zasad i zwiększa hello liczba pakietów, które mogą być przetwarzane wewnątrz hello maszyny Wirtualnej.
* **Zmniejszona zakłócenia:** przełącznik wirtualny przetwarzania zależy od hello ilość zasad, które należy zastosować toobe i obciążenie hello hello procesora CPU, obsługującym hello przetwarzania. Odciążanie sprzętu toohello wymuszania zasad hello usuwa tego zmienności dostarczania pakietów bezpośrednio zmienia toohello maszyny Wirtualnej, usunięcie hello hosta tooVM komunikacji i wszystkich oprogramowania przerwań i kontekstu.
* **Zmniejszyć użycie procesora CPU:** Bypassing hello przełącznika wirtualnego na hoście hello prowadzi tooless użycie procesora CPU do przetwarzania ruchu sieciowego.

## <a name="Limitations"></a>Ograniczenia
Podczas przy użyciu tej możliwości istnieją Hello następujące ograniczenia:

* **Tworzenie interfejsu sieci:** akcelerowanego sieci można włączyć tylko dla nowych kart sieciowych. Nie można włączyć dla istniejącej karty sieciowej.
* **Tworzenie maszyny Wirtualnej:** A kart interfejsu Sieciowego z włączoną obsługą przyspieszonego sieci może jedynie być dołączone tooa maszyny Wirtualnej, gdy hello zostanie utworzona maszyna wirtualna. Witaj karty Sieciowej nie może być dołączone tooan istniejącej maszyny Wirtualnej.
* **Regiony:** maszyn wirtualnych systemu Windows z przyspieszonego w sieci jest oferowanych w regionach najbardziej platformy Azure. Maszyn wirtualnych systemu Linux z przyspieszonego sieci są dostępne w wielu regionach. rozwija regionów Hello ta funkcja jest dostępna w. Zobacz blog Azure aktualizacje dla sieci wirtualnej hello poniżej hello najnowszych informacji.   
* **Obsługiwane systemy operacyjne:** systemu Windows: Microsoft Windows Server 2012 R2 Datacenter i Windows Server 2016. Linux: Ubuntu Server 16.04 LTS i 4.4.0-77 jądra lub nowszą, SLES 12 z dodatkiem SP2, RHEL 7.3 i CentOS 7.3 (opublikowanej przez "Nieautoryzowanego Wave oprogramowanie").
* **Rozmiar maszyny Wirtualnej:** ogólnego przeznaczenia i rozmiary obliczeniowe są zoptymalizowane pod kątem wystąpienia z co najmniej osiem rdzeni. Aby uzyskać więcej informacji, zobacz hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) i [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej. Witaj zbiór rozmiarów maszyn wirtualnych obsługiwanych w wystąpieniu rozwinie w przyszłości hello.
* **Tylko wdrożenia za pośrednictwem usługi Azure Resource Manager (ARM):** przyspieszony sieci nie jest dostępny do wdrożenia za pomocą funkcji ASM/frontonu REDDOG.

Ograniczenia toothese zmiany są ogłaszane za pośrednictwem hello [sieci wirtualnych Azure aktualizuje](https://azure.microsoft.com/updates/accelerated-networking-in-preview) strony.

## <a name="create-a-windows-vm"></a>Tworzenie maszyny wirtualnej z systemem Windows
Możesz użyć hello portalu Azure lub Azure [PowerShell](#windows-powershell) hello toocreate maszyny Wirtualnej.

### <a name="windows-portal"></a>Portal

1. Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
2. W portalu powitania kliknij **+ nowy** > **obliczeniowe** > **systemu Windows Server Datacenter 2016**. 
3. W hello **systemu Windows Server Datacenter 2016** wyświetlonym bloku, pozostaw *Resource Manager* wybranego w obszarze **wybierz model wdrożenia**i kliknij przycisk **Utwórz** .
4. W hello **podstawy** bloku, który pojawia się, wprowadź następujące wartości hello pozostaw hello pozostałe opcje domyślne lub wybierz lub wprowadź własne wartości, a kliknij hello **OK** przycisk:

    |Ustawienie|Wartość|
    |---|---|
    |Nazwa|MyVm|
    |Grupa zasobów|Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź *MyResourceGroup*|
    |Lokalizacja|Zachodnie stany USA 2|

    Jeśli nowy tooAzure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (które są także określony regionów tooas).
5. W hello **wybierz rozmiar** bloku, zostanie wyświetlone, wprowadź *8* w hello **minimalna liczba rdzeni** polu, a następnie kliknij przycisk **Wyświetl wszystkie**.
6. Kliknij przycisk **DS4_V2 standardowe**, lub dowolny obsługiwany maszyny Wirtualnej, kliknij przycisk hello **wybierz** przycisku.
7. W hello **ustawienia** bloku, zostanie wyświetlone, pozostaw wszystkie ustawienia jako — jest, z wyjątkiem kliknij **włączone** w obszarze **przyspieszony sieci**, następnie kliknij przycisk hello **OK** przycisku. **Uwaga:** , jeśli w poprzednich krokach wybrane wartości dla rozmiaru maszyny Wirtualnej, system operacyjny lub lokalizacji, które nie są wymienione w hello [ograniczenia](#Limitations) sekcji tego artykułu **sieci akcelerowanego**nie jest widoczny.
8. W hello **Podsumowanie** bloku, który jest wyświetlany, kliknij przycisk hello **OK** przycisku. Azure rozpoczyna tworzenie hello maszyny Wirtualnej. Tworzenie maszyny Wirtualnej trwa kilka minut.
9. tooinstall hello przyspieszony sterowników sieciowych systemu Windows, pełną hello etapami hello [Konfigurowanie systemu Windows](#configure-windows) sekcji tego artykułu.

### <a name="windows-powershell"></a>Środowiska PowerShell
1. Zainstaluj najnowszą wersję hello Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell odczytu hello [Omówienie programu Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.
2. Uruchom sesję programu PowerShell, klikając przycisk Start systemu Windows hello, wpisując **środowiska powershell**, klikając **PowerShell** hello wyników wyszukiwania.
3. W oknie programu PowerShell, wprowadź hello `login-azurermaccount` toosign polecenia przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
4. W przeglądarce skopiuj hello następującego skryptu:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. W oknie programu PowerShell kliknij prawym przyciskiem myszy skrypt hello toopaste i uruchomienia jej wykonanie. Zostanie wyświetlony monit o nazwę użytkownika i hasło. Użyj toolog te poświadczenia w toohello maszyny Wirtualnej, łącząc tooit w hello następnego kroku. Jeśli hello skrypt zakończy się niepowodzeniem, a wartości w skrypcie hello zostały zmienione przed jego wykonaniem, potwierdzić wartości hello używane dla rozmiaru maszyny Wirtualnej, system operacyjny i lokalizacja znajduje się w hello [ograniczenia](#Limitations) sekcji tego artykułu.
6. tooinstall hello przyspieszony sterowników sieciowych systemu Windows, pełną hello etapami hello [Konfigurowanie systemu Windows](#configure-windows) sekcji tego artykułu.

### <a name="configure-windows"></a>Konfigurowanie systemu Windows
Po utworzeniu hello maszyny Wirtualnej na platformie Azure, należy zainstalować sterownik sieciowy przyspieszonego powitania dla systemu Windows. Przed wykonaniem hello następujące kroki, należy utworzyć Maszynę wirtualną systemu Windows z przyspieszonego w sieci przy użyciu albo hello [portal](#windows-portal) lub [PowerShell](#windows-powershell) kroków w tym artykule. 

1. Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *MyVm*. Gdy **MyVm** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **MyVm** bloku, który jest wyświetlany, kliknij przycisk hello **Connect** przycisku na powitania lewym górnym rogu bloku hello. **Uwaga:** Jeśli **tworzenie** jest widoczna w obszarze hello **Connect** przycisku Azure nie została jeszcze ukończona tworzenie hello maszyny Wirtualnej. Kliknij przycisk **Connect** tylko wtedy, gdy nie są już wyświetlane **tworzenie** w obszarze hello **Connect** przycisku.
4. Zezwalaj na powitania toodownload Twojego przeglądarki **MyVm.rdp** pliku.  Po pobraniu, kliknij przycisk tooopen pliku hello go. 
5. Kliknij przycisk hello **Connect** przycisku na powitania **Podłączanie pulpitu zdalnego** wyświetlonym, powiadamianie o tym, że hello nie można zidentyfikować wydawcy tego połączenia zdalnego hello.
6. W hello **zabezpieczenia systemu Windows** okno zostanie wyświetlone, kliknij przycisk **więcej opcji**, następnie kliknij przycisk **korzystała z innego konta**. Wprowadź hello nazwy użytkownika i hasła podanego w kroku 4, a następnie kliknij przycisk hello **OK** przycisku.
7. Kliknij przycisk hello **tak** przycisk pojawi się powiadomienie, że nie można zweryfikować tożsamości komputera zdalnego hello hello okno Podłączanie pulpitu zdalnego hello.
8. Kliknij prawym przyciskiem myszy przycisk Start systemu Windows hello, a następnie kliknij przycisk **Menedżera urządzeń**. Rozwiń węzeł hello **karty sieciowe** węzła. Upewnij się, że hello **Mellanox ConnectX 3 wirtualnej funkcja Ethernet karty** pojawia się, jak pokazano na poniższej ilustracji hello:
   
    ![Menedżer urządzeń](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Przyspieszone sieci jest teraz włączony dla maszyny Wirtualnej.

## <a name="create-a-linux-vm"></a>Tworzenie maszyny wirtualnej z systemem Linux
Możesz użyć hello portalu Azure lub Azure [PowerShell](#linux-powershell) toocreate Ubuntu lub SLES maszyny Wirtualnej. RHEL i maszyny wirtualnej CentOS istnieje inny przepływ pracy.  Zobacz poniższe instrukcje hello.

### <a name="linux-portal"></a>Portal
1. Rejestr hello przyspieszony sieci dla systemu Linux w wersji zapoznawczej, wykonując kroki 1 – 5 hello [utworzyć Maszynę wirtualną systemu Linux - PowerShell](#linux-powershell) sekcji tego artykułu.  Możesz zarejestrować się w wersji zapoznawczej hello w portalu hello.
2. Zakończenie kroki 1 – 8 hello w [utworzyć Maszynę wirtualną systemu Windows — portal](#windows-portal) sekcji tego artykułu. W kroku 2 kliknij **Ubuntu Server 16.04 LTS** zamiast **systemu Windows Server Datacenter 2016**. W tym samouczku wybierz toouse hasła, a nie kluczem SSH, chociaż wdrożeń produkcyjnych, możesz użyć dowolnej. Jeśli **przyspieszony sieci** nie pojawia się po wykonaniu kroku 7 hello [utworzyć Maszynę wirtualną systemu Windows — portal](#windows-portal) sekcji tego artykułu, prawdopodobnie jednego hello z następujących powodów:
    - Możesz nie zostały jeszcze zarejestrowane hello podglądu. Upewnij się, że stan użytkownika rejestracji to **zarejestrowanej**, zgodnie z objaśnieniem w kroku 4 hello [utworzyć Maszynę wirtualną systemu Linux - Powershell](#linux-powershell) sekcji tego artykułu. **Uwaga:** Jeśli udział w hello akcelerowanego sieci dla maszyn wirtualnych systemu Windows w wersji zapoznawczej (jego nie dłużej toouse niezbędne tooregister przyspieszony sieci dla maszyn wirtualnych systemu Windows), możesz nie są automatycznie zarejestrowane dla hello akcelerowanego sieci dla Podgląd maszyn wirtualnych systemu Linux. Należy zarejestrować dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux Podgląd tooparticipate w nim.
    - Nie wybrano rozmiar maszyny Wirtualnej, system operacyjny lub lokalizacji na liście hello [ograniczenia](#limitations) sekcji tego artykułu.
3. tooinstall hello przyspieszony sterownik sieciowy dla systemu Linux, pełną hello etapami hello [skonfigurować Linux](#configure-linux) sekcji tego artykułu.

### <a name="linux-powershell"></a>Środowiska PowerShell

>[!WARNING]
>Jeśli Tworzenie maszyn wirtualnych systemu Linux z przyspieszonego sieci w ramach subskrypcji, a następnie spróbuj toocreate maszyny Wirtualnej systemu Windows z przyspieszonego sieci w programie hello tej samej subskrypcji, hello tworzenia maszyny Wirtualnej systemu Windows może zakończyć się niepowodzeniem. Tej wersji zapoznawczej zaleca się testowanie systemu Linux i maszyn wirtualnych systemu Windows z przyspieszonego sieci w oddzielnych subskrypcji.
>

1. Zainstaluj najnowszą wersję hello Azure PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell odczytu hello [Omówienie programu Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.
2. Uruchom sesję programu PowerShell, klikając przycisk Start systemu Windows hello, wpisując **środowiska powershell**, klikając **PowerShell** hello wyników wyszukiwania.
3. W oknie programu PowerShell, wprowadź hello `login-azurermaccount` toosign polecenia przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Rejestr hello przyspieszony sieci platformy Azure w wersji zapoznawczej, wykonując następujące kroki hello:
    - Wyślij wiadomość e-mail zbyt[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) identyfikator subskrypcji platformy Azure i zamierzonego użycia. Poczekaj, aż wiadomość e-mail z potwierdzeniem od firmy Microsoft dotyczące włączania subskrypcji.
    - Wprowadź następujące tooconfirm polecenia, które są zarejestrowane dla podglądu hello hello:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Nie wykonuj kroku 5 do **zarejestrowanej** pojawia się w hello dane wyjściowe po wprowadzeniu hello poprzednie polecenie. Dane wyjściowe musi wyglądać hello następujących danych wyjściowych, aby kontynuować:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Jeśli udział w hello akcelerowanego sieci dla maszyn wirtualnych systemu Windows w wersji zapoznawczej (jego nie dłużej toouse niezbędne tooregister przyspieszony sieci dla maszyn wirtualnych systemu Windows), możesz nie są automatycznie zarejestrowane dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux w wersji zapoznawczej. Należy zarejestrować dla hello akcelerowanego sieci dla maszyn wirtualnych systemu Linux Podgląd tooparticipate w nim.
      >
5. W przeglądarce skopiuj hello następującego skryptu, zastępując Ubuntu lub SLES zgodnie z potrzebami.  Ponownie Redhat i CentOS ma inny przepływ pracy przedstawione poniżej:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. W oknie programu PowerShell kliknij prawym przyciskiem myszy skrypt hello toopaste i uruchomienia jej wykonanie. Zostanie wyświetlony monit o nazwę użytkownika i hasło. Użyj toolog te poświadczenia w toohello maszyny Wirtualnej, łącząc tooit w hello następnego kroku. Jeśli skrypt hello zakończy się niepowodzeniem, upewnij się, że:
    - Zarejestrowanych dla podglądu hello, zgodnie z objaśnieniem w kroku 4
    - Jeśli zmieniono rozmiar, typ systemu operacyjnego lub wartości lokalizacji w skrypcie hello maszyny Wirtualnej przed wykonaniem go, że wartości hello są wymienione w hello [ograniczenia](#Limitations) sekcji tego artykułu.
7. tooinstall hello przyspieszony sterownik sieciowy dla systemu Linux, pełną hello etapami hello [skonfigurować Linux](#configure-linux) sekcji tego artykułu.

### <a name="configure-linux"></a>Konfigurowanie systemu Linux

Po utworzeniu hello maszyny Wirtualnej na platformie Azure, należy zainstalować sterownik sieciowy przyspieszonego powitania dla systemu Linux. Przed wykonaniem hello następujące kroki, należy utworzyć Maszynę wirtualną systemu Linux z przyspieszonego w sieci przy użyciu albo hello [portal](#linux-portal) lub [PowerShell](#linux-powershell) kroków w tym artykule. 

1. Za pomocą przeglądarki internetowej, otwórz hello Azure [portal](https://portal.azure.com) i zaloguj się przy użyciu platformy Azure [konta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
2. U góry hello hello portalu prawym toohello hello *wyszukiwania zasobów* pasek, kliknij przycisk hello **> _** toostart ikona powłoki Bash chmury (wersja zapoznawcza). przedstawia informacje o Hello Bash chmury powłoki pojawi się okienko dole hello hello portalu po kilku sekundach  **username@Azure:~ $** wiersza. Chociaż możesz toohello SSH maszyny Wirtualnej z Twojego komputera zamiast hello chmury powłoki hello instrukcje w tym samouczku założono, że używasz hello chmury powłoki.
3. U góry hello hello portalu, w polu hello zawierający tekst hello *wyszukiwania zasobów*, typ *MyVm*. Gdy **MyVm** pojawia się w wynikach wyszukiwania hello, kliknij ją.
4. W hello **MyVm** bloku, który jest wyświetlany, kliknij przycisk hello **Connect** przycisku na powitania lewym górnym rogu bloku hello. **Uwaga:** Jeśli **tworzenie** jest widoczna w obszarze hello **Connect** przycisku Azure nie została jeszcze ukończona tworzenie hello maszyny Wirtualnej. Kliknij przycisk **Connect** tylko wtedy, gdy nie są już wyświetlane **tworzenie** w obszarze hello **Connect** przycisku.
5. Azure zostanie otwarte okno informujący tooenter hello `ssh adminuser@<ipaddress>`. Wprowadź polecenie w hello chmury powłoki (lub kopiowania go z hello pola, które znajdowały się w kroku 4 i wklej go w powłoce chmury toohello), naciśnij klawisz Enter.
6. Wprowadź **tak** pytanie toohello pytania, możesz Jeśli toocontinue połączenie, naciśnij klawisz Enter.
7. Wprowadź hasło hello, wprowadzona podczas tworzenia hello maszyny Wirtualnej. Po pomyślnym zalogowaniu toohello maszyny Wirtualnej, zostanie wyświetlony adminuser@MyVm:~ $ wiersza. Zalogowano Cię teraz toohello maszyny Wirtualnej za pośrednictwem sesję powłoki hello chmury. **Uwaga:** limit czasu sesji powłoki w chmurze po 10 minutach braku aktywności.

W tym momencie instrukcje hello różnić w zależności od dystrybucji hello, którego używasz. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. W wierszu hello wprowadź `uname -r` i Potwierdź hello wersji:

    * Ubuntu jest "4.4.0-77-generic," lub nowszej
    * SLES jest "4.4.59-92.20-default" lub nowszej

2. Utworzyć rentowność między hello standardowe vNIC sieci i vNIC sieci hello przyspieszony uruchomionych poleceń hello, które należy wykonać. Ruch sieciowy używa hello wyższej wykonywania przyspieszonego sieci wirtualnej karty sieciowej, podczas gdy rentowność hello zapewnia ruchu sieciowego nie zostało przerwane przez niektóre zmiany konfiguracji.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Po uruchamianie skryptu hello hello maszyna wirtualna zostanie ponownie uruchomiona po wstrzymać 60 sekund.
4. Raz powitalne maszyna wirtualna zostanie ponownie uruchomiony, ponownie połącz tooit wykonując kroki 5-7.
5. Uruchom hello `ifconfig` polecenie i Potwierdź, że została znaleziona bond0 i interfejs hello jest wyświetlany jako zapasowe. 
 
 >[!NOTE]
      >Aplikacje przy użyciu przyspieszonego sieci muszą komunikować się za pośrednictwem hello *bond0* interfejs nie *eth0*.  Nazwa interfejsu Hello może się zmienić przed przyspieszonego sieci osiągnie ogólnej dostępności.

#### <a name="rhelcentos"></a>RHEL/CentOS

W celu utworzenia Red Hat Enterprise Linux lub wirtualna 7.3 CentOS wymagane pewne dodatkowe kroki tooload hello najnowszej wersji sterowników wymaganych dla funkcji SR-IOV i hello sterownik funkcji wirtualnej funkcji (Wirtualnej) dla karty sieciowej hello. Hello pierwszą fazę instrukcje hello przygotowuje obraz, który może być używane toomake maszyn wirtualnych, które sterowniki hello wstępnie załadowane.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Pierwszej fazy: przygotowanie Red Hat Enterprise Linux lub CentOS 7.3 obrazu podstawowego. 

1.  Udostępnianie nie - funkcji SR-IOV CentOS 7.3 Maszynę wirtualną na platformie Azure

2.  Instalowania usług LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Pobierz pliki konfiguracji
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Anulowanie zastrzeżenia tej maszyny Wirtualnej

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Z portalu Azure Zatrzymaj tę maszynę Wirtualną; Przejdź przez tooVM "dyskami", przechwytywania hello OSDisk identyfikator URI dysku VHD. Ten identyfikator URI zawiera nazwę dysku VHD hello obrazu podstawowego i jego konta magazynu. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Dwie fazy: obsługi administracyjnej nowych maszyn wirtualnych na platformie Azure

1.  Obsługi administracyjnej nowych maszyn wirtualnych na podstawie AzureRMVMConfig nowy przy użyciu hello obraz podstawowy dysk VHD przechwycone na etapie, za pomocą AcceleratedNetworking włączona na karcie vNIC hello:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Po rozruchu maszyn wirtualnych, urządzenia funkcji Wirtualnej hello przez "lspci" i Sprawdź wpis Mellanox hello. Na przykład możemy powinien zostać wyświetlony ten element w danych wyjściowych lspci hello:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Uruchom skrypt przez hello przez:

    ```bash
    sudo bondvf.sh
    ```

4.  Ponowny rozruch hello nowych maszyn wirtualnych:

    ```bash
    sudo reboot
    ```

Hello wirtualna powinien się rozpoczynać od bond0 skonfigurowany i hello ścieżki przyspieszony sieci włączone.  Uruchom `ifconfig` tooconfirm.
