---
title: "Połączenie wirtualnej sieci tooanother sieci wirtualnej: wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono łączenie sieci wirtualnych przy użyciu usługi Azure Resource Manager oraz interfejsu wiersza polecenia platformy Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Konfigurowanie połączenia bramy sieci VPN między sieciami wirtualnymi przy użyciu interfejsu wiersza polecenia platformy Azure

W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi. Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji. Podczas łączenia sieci wirtualne z różnych subskrypcji, subskrypcje hello nie ma potrzeby toobe skojarzone z hello tej samej dzierżawy usługi Active Directory. 

Witaj opisanych w tym artykule mają zastosowanie modelu wdrażania usługi Resource Manager toohello i użyć wiersza polecenia platformy Azure. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Łączenie różnych modeli wdrażania — witryna Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Łączenie różnych modeli wdrażania — program PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Jeśli Twoje sieci wirtualne są w hello tego samego regionu, może być tooconsider łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).

Komunikację między sieciami wirtualnymi można łączyć z konfiguracjami obejmującymi wiele lokacji. Dzięki temu można ustanowić topologii sieci, łączące łączności między lokalizacjami z połączeniem sieciowym między wirtualnych, jak pokazano w powitania po diagramu:

![Informacje o połączeniach](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Dlaczego łączy się sieci wirtualne?

Warto sieci wirtualnych tooconnect hello z następujących powodów:

* **Niezależna od regionu nadmiarowość i obecność geograficzna**

  * Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.
  * Usługi Azure Traffic Manager i Load Balancer pozwalają skonfigurować obciążenie o wysokiej dostępności z nadmiarowością geograficzną w wielu regionach świadczenia usługi Azure. Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.
* **Regionalne aplikacje wielowarstwowe z izolacją lub granicami administracyjnymi**

  * Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wieloma sieciami wirtualnymi, połączonych ze sobą tooisolation lub wymagań administracyjnych.

Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

### <a name="which-set-of-steps-should-i-use"></a>Która instrukcje mają zastosowanie w moim przypadku?

W tym artykule przedstawiono dwa różne zestawy kroków. Jeden zestaw kroków [sieci wirtualnych, które znajdują się w hello tej samej subskrypcji](#samesub)i drugi dla [sieci wirtualnych, które znajdują się w różnych subskrypcji](#difsub).

## <a name="samesub"></a>Połączyć sieci wirtualnych, które znajdują się w hello tej samej subskrypcji

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej). Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Planowanie zakresów adresów IP

Hello następujące kroki utworzymy dwie sieci wirtualne wraz z ich bramy odpowiednich podsieci i konfiguracji. Następnie utworzymy połączenie sieci VPN między Witaj dwie sieci wirtualne. Jest ważne tooplan zakresów adresów IP powitania dla konfiguracji sieci. Niezbędne jest upewnienie się, że zakresy sieci wirtualnej ani sieci lokalnej nie zachodzą na siebie w jakikolwiek sposób. W tych przykładach nie uwzględniamy serwera DNS. Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Używamy hello następujące wartości w przykładach hello:

**Wartości dla sieci TestVNet1:**

* Nazwa sieci wirtualnej: TestVNet1
* Grupa zasobów: TestRG1
* Lokalizacja: Wschodnie stany USA
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Publiczny adres IP: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Wartości dla sieci TestVNet4:**

* Nazwa sieci wirtualnej: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupa zasobów: TestRG4
* Lokalizacja: West US
* GatewayName: VNet4GW
* Publiczny adres IP: VNet4GWIP
* VPNType: RouteBased
* Połączenie: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>Krok 1 — Połącz tooyour subskrypcji

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Krok 2 — Tworzenie i konfigurowanie sieci TestVNet1

1. Utwórz grupę zasobów.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Utwórz TestVNet1 i hello podsieci dla TestVNet1. W tym przykładzie jest tworzona sieć wirtualna TestVNet1 i podsieć o nazwie FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Utwórz przestrzeń adresową dodatkowe hello podsieci wewnętrznej bazy danych. Zwróć uwagę, w tym kroku, możemy określić przestrzeń adresowa hello zarówno utworzony wcześniej czy hello dodatkową przestrzeń adresów czy chcemy tooadd. Jest to spowodowane hello [zaktualizować sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#update) polecenia zastępuje hello poprzednie ustawienia. Upewnij się, że toospecify na wszystkie prefiksy adresów hello, korzystając z tego polecenia.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Utwórz hello podsieci wewnętrznej bazy danych.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Utwórz podsieć bramy hello. Należy zauważyć, że podsieci bramy hello o nazwie "GatewaySubnet". Nazwa jest wymagana. W tym przykładzie podsieć bramy hello używa /27. Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając co najmniej /28 lub /27. Umożliwi to za mało adresów tooaccommodate możliwe dodatkowe konfiguracje, które można w hello przyszłych.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej. Należy zauważyć, że hello AllocationMethod jest dynamiczny. Nie można określić hello adresu IP, które mają toouse. Jest dynamicznie przydzielonego tooyour bramy.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Tworzenie bramy sieci wirtualnej powitania dla TestVNet1. Konfiguracje połączeń między sieciami wirtualnymi wymagają zastosowania wartości RouteBased obiektu VpnType. Po uruchomieniu tego polecenia, używając hello parametr — nie - oczekiwania nie widać żadnych opinie i danych wyjściowych. Witaj — nie - oczekiwania parametr umożliwia toocreate bramy hello w tle hello. Nie oznacza tej bramy VPN hello zakończy tworzenie natychmiast. Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od bramy hello jednostka SKU, którego używasz.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Krok 3 — Tworzenie i konfigurowanie sieci TestVNet4

1. Utwórz grupę zasobów.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Utwórz sieć TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Utwórz dodatkowe podsieci dla sieci TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Utwórz podsieć bramy hello.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Prześlij żądanie dotyczące publicznego adresu IP.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Utwórz bramę sieci wirtualnej TestVNet4 hello.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Krok 4 — Utwórz hello połączenia

Mamy teraz dwie sieci wirtualne z bramami sieci VPN. Witaj następnym krokiem jest toocreate połączenia bramy sieci VPN między hello bram sieci wirtualnej. Jeśli użyto hello przykładach z bram sieci wirtualnej są w różnych grupach zasobów. Gdy bramy znajdują się w różnych grupach zasobów, należy tooidentify i określ hello identyfikatorów zasobów dla każdej bramy podczas nawiązywania połączenia. Jeśli Twoje sieci wirtualne są w hello tej samej grupie zasobów, można użyć hello [drugi zestaw instrukcji](#samerg) wystarczy identyfikatorów zasobów hello toospecify.

### <a name="diffrg"></a>tooconnect sieci wirtualnych, które znajdują się w różnych grupach zasobów

1. Pobierz hello identyfikator VNet1GW zasobów z danych wyjściowych hello hello następujące polecenie:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  W danych wyjściowych hello Znajdź hello "identyfikator:" wiersza. wartości Hello w cudzysłowy hello są potrzebne toocreate hello połączenia w następnej sekcji hello. Skopiuj te wartości tooa edytora tekstów, takiego jak Notatnik, dzięki czemu można łatwo je wklejać podczas tworzenia połączenia.

  Przykładowe dane wyjściowe:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Skopiuj wartości powitania po **"id":** w cudzysłowy hello.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Pobierz hello identyfikator VNet4GW zasobów i skopiuj hello wartości tooa edytora tekstu.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Utwórz połączenie tooTestVNet4 TestVNet1 hello. W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4. Brak klucza współdzielonego, do którego odwołuje się przykłady hello. Możesz użyć własnych wartości dla klucza udostępnionego hello. ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń. Tworzenie połączenia trwa krótko podczas toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Utwórz połączenie tooTestVNet1 TestVNet4 hello. Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1. Upewnij się, że klucze hello udostępnionych pasują do siebie. Trwa kilka minut tooestablish hello połączenia.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Sprawdź połączenia. Zobacz sekcję [Weryfikowanie połączenia](#verify).

### <a name="samerg"></a>tooconnect sieci wirtualnych, które znajdują się w hello same grupy zasobów

1. Utwórz połączenie tooTestVNet4 TestVNet1 hello. W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4. Grupy zasobów hello powiadomienia są hello sam w przykładach hello. Widoczny jest również określany w przykładach hello klucza wspólnego. Możesz użyć własnych wartości dla klucza udostępnionego hello, jednak hello klucz współużytkowany musi być zgodna dla obu połączeń. Tworzenie połączenia trwa krótko podczas toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Utwórz połączenie tooTestVNet1 TestVNet4 hello. Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1. Upewnij się, że klucze hello udostępnionych pasują do siebie. Trwa kilka minut tooestablish hello połączenia.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Sprawdź połączenia. Zobacz sekcję [Weryfikowanie połączenia](#verify).

## <a name="difsub"></a>Łączenie sieci wirtualnych, które należą do różnych subskrypcji

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

W tym scenariuszu nawiązywane jest połączenie między sieciami wirtualnymi TestVNet1 i TestVNet5. Witaj sieci wirtualne znajdują się różnych subskrypcji. Subskrypcje Hello nie są skojarzone z hello toobe tej samej dzierżawy usługi Active Directory. Hello czynności dla tej konfiguracji dodać dodatkowego połączenia do wirtualnymi w kolejności tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Krok 5 — Tworzenie i konfigurowanie sieci TestVNet1

Te instrukcje są nadal kroki hello w powyższej sekcji hello. Należy wykonać [krok 1](#Connect) i [krok 2](#TestVNet1) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN dla TestVNet1. W przypadku tej konfiguracji nie jest wymagane toocreate TestVNet4 z poprzedniej sekcji hello, mimo że, jeśli tworzysz, nie będzie ona konflikt z tych kroków. Po ukończeniu kroków 1 i 2 przejdź do kroku 6 (poniżej).

### <a name="verifyranges"></a>Krok 6 - Sprawdź, czy zakresy adresów IP hello

Podczas tworzenia dodatkowych połączeń, jest ważne tooverify, który hello przestrzeń adresową hello nowej sieci wirtualnej nie zachodzi na inne zakresy sieci wirtualnej lub zakresy bramy sieci lokalnej. W tym ćwiczeniu program hello następujące wartości hello TestVNet5:

**Wartości dla sieci TestVNet5:**

* Nazwa sieci wirtualnej: TestVNet5
* Grupa zasobów: TestRG5
* Lokalizacja: Japan East
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Publiczny adres IP: VNet5GWIP
* VPNType: RouteBased
* Połączenie: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>Krok 7 — Tworzenie i konfigurowanie sieci TestVNet5

Ten krok należy wykonać w kontekście hello hello nową subskrypcję, 5 subskrypcji. Ta część może zostać wykonana przez administratora hello w innej organizacji, który jest właścicielem hello subskrypcji. tooswitch między subskrypcjami "listy kont az — wszystkie" toolist hello subskrypcje dostępne tooyour konta, a następnie użyj "skonfigurowane konto az — subskrypcji <subscriptionID>" tooswitch toohello subskrypcji, które mają toouse.

1. Upewnij się, że możesz są połączone tooSubscription 5, a następnie utwórz grupę zasobów.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Utwórz sieć wirtualną TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Dodaj podsieci.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Dodaj podsieć bramy hello.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Prześlij żądanie dotyczące publicznego adresu IP.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Utwórz bramę TestVNet5 hello

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Krok 8 — Utwórz hello połączenia

Możemy podzielić ten krok do dwóch sesji CLI oznaczona jako **[subskrypcji 1]**, i **[subskrypcji 5]** hello bramy znajdują się w różnych subskrypcji hello. tooswitch między subskrypcjami "listy kont az — wszystkie" toolist hello subskrypcje dostępne tooyour konta, a następnie użyj "skonfigurowane konto az — subskrypcji <subscriptionID>" tooswitch toohello subskrypcji, które mają toouse.

1. **[Subskrypcji 1]**  Logowania i połącz tooSubscription 1. Witaj uruchom następujące polecenie tooget hello nazwy i Identyfikatora hello bramy z danych wyjściowych hello:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Kopiuj dane wyjściowe powitania dla "identyfikator:". Wyślij hello identyfikator i nazwa hello hello sieci wirtualnej bramy (VNet1GW) toohello administratora subskrypcji 5 za pomocą poczty e-mail lub innej metody.

  Przykładowe dane wyjściowe:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Subskrypcji 5]**  Logowania i połącz tooSubscription 5. Witaj uruchom następujące polecenie tooget hello nazwy i Identyfikatora hello bramy z danych wyjściowych hello:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Kopiuj dane wyjściowe powitania dla "identyfikator:". Wyślij hello identyfikator i nazwa hello hello sieci wirtualnej bramy (VNet5GW) toohello administratora subskrypcji 1 za pośrednictwem poczty e-mail lub innej metody.

3. **[Subskrypcji 1]**  w tym kroku, tworzenia połączenia hello z TestVNet1 tooTestVNet5. Możesz użyć własnych wartości dla klucza udostępnionego hello, jednak hello klucz współużytkowany musi być zgodna dla obu połączeń. Tworzenie połączenia może zająć chwilę podczas toocomplete. Upewnij się, że połączenie tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Subskrypcji 5]**  Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet5 tooTestVNet1. Upewnij się, że hello udostępnionych kluczy dopasowania i Połącz z tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Zweryfikuj hello połączenia
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Następne kroki

* Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz hello [dokumentacji maszyn wirtualnych](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
