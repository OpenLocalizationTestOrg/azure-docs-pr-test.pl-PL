---
title: "Połącz tooAzure klasycznych sieci wirtualnych Menedżera zasobów sieci wirtualnych: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate połączenia sieci VPN między klasycznych sieci wirtualnych i sieci wirtualnych Menedżera zasobów przy użyciu bramy sieci VPN i programu PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Łączenie sieci wirtualnych z różnych modeli wdrażania za pomocą programu PowerShell



W tym artykule opisano, jak tooconnect klasycznych sieci wirtualnych tooResource tooallow Menedżera sieci wirtualnych hello zasobów znajdujących się w hello oddzielne wdrażania modeli toocommunicate ze sobą. Hello opisanych w tym artykule przy użyciu programu PowerShell, ale można również utworzyć tę konfigurację za pomocą hello portalu Azure, wybierając hello artykułu z tej listy.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Łączenie klasycznego tooa sieci wirtualnej Menedżera zasobów w sieci wirtualnej jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Można utworzyć połączenia między sieciami wirtualnymi, które są w różnych subskrypcji i w różnych regionach. Można też połączyć sieci wirtualnych, która jeszcze połączenia lokalnego tooon sieci, tak długo, jak jest hello bramy, które zostały skonfigurowane z dynamicznego lub oparte na trasach. Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule. 

Jeśli hello Twojej sieci wirtualnych tego samego regionu, można wziąć pod uwagę tooinstead, łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Przed rozpoczęciem

Witaj poniższe kroki przeprowadzi użytkownika przez proces tooconfigure niezbędne ustawienia hello bramy dynamiczne lub oparte na trasach dla każdej sieci wirtualnej i Utwórz połączenie sieci VPN między bramami hello. Ta konfiguracja nie obsługuje bramy statyczne lub oparte na zasadach.

### <a name="prerequisites"></a>Wymagania wstępne

* Obie sieci wirtualne zostały już utworzone.
* Hello zakresy adresów dla hello sieci wirtualnych nie pokrywają się ze sobą, ani nie nakładają się ze wszystkimi hello zakresów dla innych połączeń, które hello bramy może być połączone.
* Zainstalowano hello najnowszych poleceń cmdlet programu PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji. Upewnij się, że należy zainstalować zarówno hello usługi zarządzania (ko), jak i hello poleceń cmdlet Menedżera zasobów (RM). 

### <a name="exampleref"></a>Przykładowe ustawienia

Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.

**Klasycznych ustawień sieci wirtualnej**

Nazwa sieci wirtualnej = ClassicVNet <br>
Lokalizacja = zachodnie stany USA <br>
Przestrzeniami adresów sieci wirtualnej = 10.0.0.0/24 <br>
Podsieć 1 = 10.0.0.0/27 <br>
GatewaySubnet = 10.0.0.32/29 <br>
Nazwa sieci lokalnej = RMVNetLocal <br>
Elementu GatewayType = DynamicRouting

**Ustawienia Menedżera zasobów w sieci wirtualnej**

Nazwa sieci wirtualnej = RMVNet <br>
Grupa zasobów = RG1 <br>
Przestrzeni adresów IP sieci wirtualnej = 192.168.0.0/16 <br>
Podsieć 1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Lokalizacja = wschodnie stany USA <br>
Nazwa publicznego adresu IP bramy = gwpip <br>
Brama sieci lokalnej = ClassicVNetLocal <br>
Nazwa bramy sieci wirtualnej = RMGateway <br>
Konfiguracja adresów IP bramy = gwipconfig

## <a name="createsmgw"></a>Sekcja 1 — Konfigurowanie hello klasycznej sieci wirtualnej
### <a name="part-1---download-your-network-configuration-file"></a>Część 1 - pobierania pliku konfiguracji sieci
1. Zaloguj się za tooyour konto platformy Azure w konsoli programu PowerShell hello z podwyższonym poziomem uprawnień. Witaj następujące polecenie cmdlet monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu pobraniu ustawienia konta, aby były dostępne tooAzure środowiska PowerShell. Użyj hello toocomplete poleceń cmdlet programu PowerShell SM ta część hello konfiguracji.

  ```powershell
  Add-AzureAccount
  ```
2. Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie hello. Możesz zmienić lokalizację hello hello pliku tooexport tooa różnych lokalizacji, w razie potrzeby.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Witaj Otwórz plik XML został pobrany tooedit go. Na przykład pliku konfiguracji sieci hello Zobacz hello [schemat konfiguracji sieci](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Część 2 - Sprawdź hello podsieci bramy
W hello **VirtualNetworkSites** elementu, Dodaj tooyour podsieci bramy sieci wirtualnej, jeśli nie została jeszcze utworzona. Podczas pracy z pliku konfiguracji sieci hello, hello podsieć bramy musi mieć nazwę "GatewaySubnet" lub Azure nie może rozpoznać i używać go jako podsieć bramy.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Przykład:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Część 3 — Dodawanie hello lokacji sieci lokalnej
Hello lokację sieci lokalnej, które można dodać reprezentuje hello ma tooconnect toowhich RM sieci wirtualnej. Dodaj **LocalNetworkSites** pliku toohello elementu, jeśli jeszcze nie istnieje. W tym momencie w konfiguracji hello hello VPNGatewayAddress może być dowolnym prawidłowego publicznego adresu IP, ponieważ możemy jeszcze nie utworzono bramę hello hello Menedżera zasobów w sieci wirtualnej. Po utworzymy hello bramy możemy zastąpić ten adres IP — symbol zastępczy hello poprawne publiczny adres IP przypisany toohello RM bramy.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Część 4 - hello skojarzenia sieci wirtualnej z lokacją sieci lokalnej hello
W tej sekcji określono hello lokacji sieci lokalnej, które mają tooconnect hello sieci wirtualnej do. W takim przypadku jest hello odwołanie do wcześniej sieci wirtualnej Menedżera zasobów. Upewnij się, że nazwy hello zgodne. Ten krok nie powoduje utworzenia bramy. Określa hello sieci lokalnej hello bramy połączy się.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Część 5 - Zapisz plik hello oraz przekazywania
Zapisz plik hello, a następnie zaimportuj go tooAzure, uruchamiając następujące polecenie hello. Upewnij się, że w przypadku zmiany ścieżki pliku hello jako wymaganych w danym środowisku.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Widoczny będzie podobny wynik pokazujący, że importowanie hello zakończyła się pomyślnie.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Część 6 - Tworzenie hello bramy

Przed uruchomieniem w tym przykładzie należy odwoływać się toohello toosee oczekuje pobranego hello dokładnej nazwy tego Azure pliku konfiguracji sieci. plik konfiguracji sieci Hello zawiera wartości hello klasyczne sieci wirtualne. Czasami nazwy hello klasycznego sieci wirtualne są zmieniane w pliku konfiguracji sieci hello podczas tworzenia klasycznych ustawień sieci wirtualnej w hello portalu Azure powodu toohello różnice w hello modele wdrażania. Na przykład jeśli użyto hello Azure toocreate portalu klasycznego sieć wirtualną o nazwie "Klasycznej sieci wirtualnej" i utworzony w grupie zasobów o nazwie "ClassicRG" hello nazwę, która jest zawarta w pliku konfiguracji sieci hello jest przekonwertowanego too'Group ClassicRG klasycznej sieci wirtualnej ". Podczas określania nazwy hello sieci wirtualnej, która zawiera spacje, użyj hello wartości w cudzysłowie.


Użyj powitania po toocreate przykładzie brama routingu dynamicznego:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Istnieje możliwość sprawdzenia stanu hello hello bramy przy użyciu hello **Get-AzureVNetGateway** polecenia cmdlet.

## <a name="creatermgw"></a>Sekcja 2: Konfigurowanie hello bramy sieci wirtualnej RM
toocreate Brama sieci VPN dla hello RM sieci wirtualnej, postępuj zgodnie z instrukcjami hello. Po pobraniu hello publicznego adresu IP dla bramy wirtualnej klasycznego hello hello kroki, dopóki nie należy uruchamiać. 

1. Zaloguj się za tooyour konto platformy Azure w konsoli programu PowerShell hello. Witaj następujące polecenie cmdlet monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu ustawienia konta są pobierane, tak aby były dostępne tooAzure środowiska PowerShell.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Pobierz listę subskrypcji Azure, jeśli masz więcej niż jedną subskrypcję.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Określ, które mają toouse subskrypcji hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Utwórz bramę sieci lokalnej. W sieci wirtualnej bramy sieci lokalnej hello zwykle oznacza tooyour lokalizacji lokalnej. W takim przypadku bramy sieci lokalnej hello odwołuje się tooyour klasycznej sieci wirtualnej. Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a także określić prefiks przestrzeni adresów hello. Platforma Azure korzysta prefiks adresu IP hello Określ tooidentify tooyour toosend których ruch lokalizacji lokalnej. Jeśli później, należy tutaj informacje hello tooadjust przed utworzeniem bramy sieci można zmodyfikować wartości hello i przykładowe hello Uruchom ponownie.
   
   **-Nazwa** jest nazwą hello ma bramy sieci lokalnej toohello toorefer tooassign.<br>
   **-AddressPrefix** jest hello przestrzeni adresowej dla sieci wirtualnej klasycznego.<br>
   **-GatewayIpAddress** jest hello publiczny adres IP bramy hello klasycznego VNet. Upewnij się, że toochange hello następujące przykładowe tooreflect hello poprawny adres IP.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Żądaj publicznego adresu IP adres toobe toohello przydzielone bramę sieci wirtualnej dla hello Menedżera zasobów w sieci wirtualnej. Nie można określić hello adresu IP, które mają toouse. adres IP Hello jest dynamicznie przydzielane toohello bramy sieci wirtualnej. Nie oznacza to jednak zmiany adresu IP hello. tylko wtedy Hello zmiany adresu IP bramy sieci wirtualnej hello jest po hello bramy jest usunięty i utworzony ponownie. Nie zmienia ono całej zmiany rozmiaru, resetowanie lub innych wewnętrzny konserwacji/uaktualnień, hello bramy.

  W tym kroku będziemy również ustawić zmiennej używanej w kolejnym kroku.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Sprawdź, czy sieci wirtualnej ma podsieci bramy. Jeśli istnieje podsieć bramy, dodaj je. Upewnij się, że nosi nazwę podsieci bramy hello *GatewaySubnet*.
5. Pobieranie podsieci hello używanym na potrzeby hello bramy, uruchamiając następujące polecenie hello. W tym kroku będziemy również ustawić zmiennej toobe, używany w następnym kroku hello.
   
   **-Nazwa** hello nazwa sieci wirtualnej Menedżera zasobów.<br>
   **-ResourceGroupName** jest hello grupa zasobów tego hello sieci wirtualnej jest skojarzony. podsieć bramy Hello musi już istnieć dla tej sieci wirtualnej i musi mieć nazwę *GatewaySubnet* toowork poprawnie.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Tworzenie konfiguracji adresów IP bramy hello. Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP. Użyj następujących hello przykładowe toocreate konfigurację bramy.

  W tym kroku hello **- SubnetId** i **- PublicIpAddressId** parametry muszą być przekazywane właściwość identyfikatora hello hello podsieci i obiekty adresu IP, odpowiednio. Nie można użyć prostego ciągu. Te zmienne są ustawiane w toorequest krok hello publicznego adresu IP i hello krok tooretrieve hello podsieci.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Tworzenie bramy sieci wirtualnej hello Menedżera zasobów, uruchamiając następujące polecenie hello. Witaj `-VpnType` musi być *RouteBased*. Może upłynąć 45 minut lub więcej hello toocreate bramy.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Po utworzeniu bramy sieci VPN hello, skopiuj hello publicznego adresu IP. Można użyć podczas konfigurowania ustawień sieci lokalnej hello klasycznej sieci wirtualnej. Można użyć następującego polecenia cmdlet tooretrieve hello publicznego adresu IP hello. Witaj publiczny adres IP ma na liście hello zwracany jako *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Sekcja 3: Modyfikowanie hello klasycznych ustawień lokalnej lokacji sieci wirtualnej

W tej sekcji możesz pracować z hello klasycznej sieci wirtualnej. Można zastąpić adres IP — symbol zastępczy hello używane podczas określania ustawień lokacji lokalnej hello, które będą używane tooconnect toohello bramy sieci wirtualnej Menedżera zasobów. 

1. Eksportowanie pliku konfiguracji sieci hello.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Za pomocą edytora tekstu, zmodyfikuj wartość powitania dla VPNGatewayAddress. Zamień adres IP — symbol zastępczy hello hello publiczny adres IP bramy usługi Resource Manager hello, a następnie zapisz zmiany hello.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Importuj hello zmodyfikować tooAzure pliku konfiguracji sieci.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Sekcja 4: Tworzenie połączenia między bramami hello
Tworzenie połączenia między bramami hello wymaga środowiska PowerShell. Konieczne może tooadd Twojego konta Azure toouse hello klasycznej wersji hello poleceń cmdlet programu PowerShell. tak, użyj toodo **Add-AzureAccount**.

1. W konsoli programu PowerShell hello należy ustawić klucz udostępniony. Przed uruchomieniem poleceń cmdlet hello, można znaleźć toohello toosee oczekuje pobranego hello dokładnej nazwy tego Azure pliku konfiguracji sieci. Podczas określania nazwy hello sieci wirtualnej, która zawiera spacje, użyj pojedynczy znaki cudzysłowu otaczające wartość hello.<br><br>W poniższym przykładzie **- VNetName** jest nazwą hello hello klasycznej sieci wirtualnej i **- LocalNetworkSiteName** jest nazwą hello określony dla lokacji sieci lokalnej hello. Witaj **- SharedKey** to Generowanie i określ wartość. Przykład Witaj użyliśmy "abc123", ale można wygenerować i korzystać z bardziej złożonych. Witaj ważne, czy element jest daną hello określone w tym miejscu musi być powitalne samą wartość, że zostanie w następnym kroku hello podczas tworzenia połączenia. Witaj zwracany powinien być wyświetlony **stanu: pomyślnie**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Utwórz połączenie sieci VPN hello, uruchamiając następujące polecenia hello:
   
  Ustaw zmienne hello.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Utwórz połączenie hello. Zwróć uwagę, że hello **- ConnectionType** jest IPsec, nie Vnet2Vnet.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Sekcja 5: Sprawdź połączenia

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>tooverify hello połączenia z klasycznym tooyour sieci wirtualnej Menedżera zasobów w sieci wirtualnej

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>tooverify hello połączenia z Twojej sieci wirtualnej Resource Manager tooyour klasycznej sieci wirtualnej

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

