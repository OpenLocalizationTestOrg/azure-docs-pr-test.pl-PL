---
title: "Połączenie sieci wirtualnej platformy Azure tooanother sieci wirtualnej: Portal | Dokumentacja firmy Microsoft"
description: "Utwórz połączenie bramy sieci VPN między sieciami wirtualnymi przy użyciu usługi Resource Manager i hello portalu Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Skonfiguruj połączenie bramy sieci VPN do wirtualnymi przy użyciu hello portalu Azure

W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi. Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji. Podczas łączenia sieci wirtualne z różnych subskrypcji, subskrypcje hello nie ma potrzeby toobe skojarzone z hello tej samej dzierżawy usługi Active Directory. 

Witaj opisanych w tym artykule zastosować toohello modelu wdrażania usługi Resource Manager i użyj hello portalu Azure. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Łączenie różnych modeli wdrażania — witryna Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Łączenie różnych modeli wdrażania — program PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Jeśli Twoje sieci wirtualne są w hello tego samego regionu, może być tooconsider łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).

Komunikację między sieciami wirtualnymi można łączyć z konfiguracjami obejmującymi wiele lokacji. Dzięki temu można ustanowić topologii sieci, łączące łączności między lokalizacjami z połączeniem sieciowym między wirtualnych, jak pokazano w powitania po diagramu:

![Informacje o połączeniach](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "Informacje o połączeniach")

### <a name="why-connect-virtual-networks"></a>Dlaczego łączy się sieci wirtualne?

Warto sieci wirtualnych tooconnect hello z następujących powodów:

* **Niezależna od regionu nadmiarowość i obecność geograficzna**
  
  * Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.
  * Usługi Azure Traffic Manager i Load Balancer pozwalają skonfigurować obciążenie o wysokiej dostępności z nadmiarowością geograficzną w wielu regionach świadczenia usługi Azure. Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.
* **Regionalne aplikacje wielowarstwowe z izolacją lub granicami administracyjnymi**
  
  * Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wieloma sieciami wirtualnymi, połączonych ze sobą tooisolation lub wymagań administracyjnych.

Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule. Należy pamiętać, że jeśli w Twojej sieci wirtualne znajdują się w różnych subskrypcji, nie można utworzyć połączenia hello w portalu hello. Można użyć programu [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) lub [interfejsu wiersza polecenia](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Przykładowe ustawienia

Jeśli te kroki jako wykonywania, można użyć hello przykładowe wartości ustawień. W celach demonstracyjnych dla poszczególnych sieci wirtualnych używamy wielu przestrzeni adresowych. Konfiguracje połączeń między sieciami wirtualnymi nie wymagają jednak wielu przestrzeni adresowych.

**Wartości dla sieci TestVNet1:**

* Nazwa sieci wirtualnej: TestVNet1
* Przestrzeń adresowa: 10.11.0.0/16
  * Nazwa podsieci: FrontEnd
  * Zakres adresów podsieci: 10.11.0.0/24
* Grupa zasobów: TestRG1
* Lokalizacja: Wschodnie stany USA
* Przestrzeń adresowa: 10.12.0.0/16
  * Nazwa podsieci: BackEnd
  * Zakres adresów podsieci: 10.12.0.0/24
* Nazwa podsieci bramy: GatewaySubnet (spowoduje to automatyczne wypełnianie w portalu hello)
  * Zakres adresów podsieci bramy: 10.11.255.0/27
* Serwer DNS: Witaj adres IP serwera DNS używany przez
* Nazwa bramy sieci wirtualnej: TestVNet1GW
* Typ bramy: VPN
* Typ sieci VPN: oparta na trasach
* Jednostka SKU: Wybierz hello jednostka SKU bramy ma toouse
* Publiczna nazwa adresu IP: TestVNet1GWIP
* Wartości połączenia:
  * Nazwa: TestVNet1toTestVNet4
  * Klucz współużytkowany: hello klucz udostępniony można utworzyć samodzielnie. W tym przykładzie użyjemy wartości abc123. Hello ważną kwestią jest, że podczas tworzenia hello połączenia między sieciami wirtualnymi hello hello wartość musi być zgodna.

**Wartości dla sieci TestVNet4:**

* Nazwa sieci wirtualnej: TestVNet4
* Przestrzeń adresowa: 10.41.0.0/16
  * Nazwa podsieci: FrontEnd
  * Zakres adresów podsieci: 10.41.0.0/24
* Grupa zasobów: TestRG1
* Lokalizacja: West US
* Przestrzeń adresowa: 10.42.0.0/16
  * Nazwa podsieci: BackEnd
  * Zakres adresów podsieci: 10.42.0.0/24
* Nazwa GatewaySubnet: GatewaySubnet (spowoduje to automatyczne wypełnianie w portalu hello)
  * Zakres adresów podsieci GatewaySubnet: 10.41.255.0/27
* Serwer DNS: Witaj adres IP serwera DNS używany przez
* Nazwa bramy sieci wirtualnej: TestVNet4GW
* Typ bramy: VPN
* Typ sieci VPN: oparta na trasach
* Jednostka SKU: Wybierz hello jednostka SKU bramy ma toouse
* Nazwa publicznego adresu IP: TestVNet4GWIP
* Wartości połączenia:
  * Nazwa: TestVNet4toTestVNet1
  * Klucz współużytkowany: hello klucz udostępniony można utworzyć samodzielnie. W tym przykładzie użyjemy wartości abc123. Hello ważną kwestią jest, że podczas tworzenia hello połączenia między sieciami wirtualnymi hello hello wartość musi być zgodna.

## <a name="CreatVNet"></a>1. Tworzenie i konfigurowanie sieci TestVNet1
Jeśli masz już sieć wirtualną, sprawdź, czy ustawienia hello są zgodne z projektu bramy sieci VPN. Należy zwrócić szczególną uwagę tooany podsieci, które nakładają się z innymi sieciami. Obecność nakładających się podsieci spowoduje, że połączenie nie będzie działać prawidłowo. Sieci wirtualnej ma skonfigurowane poprawne ustawienia hello, możesz rozpocząć hello kroki hello [Określ serwer DNS](#dns) sekcji.

### <a name="toocreate-a-virtual-network"></a>toocreate sieci wirtualnej
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Dodawanie dodatkowej przestrzeni adresowej i tworzenie podsieci
Po utworzeniu sieci wirtualnej można dodać do niej dodatkową przestrzeń adresową oraz utworzyć podsieci.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Tworzenie podsieci bramy
Przed połączeniem tooa bramy sieci wirtualnej, należy najpierw podsieci bramy hello toocreate hello toowhich sieć wirtualna ma zostać tooconnect. Jeśli to możliwe jest najlepszym toocreate podsieć bramy przy użyciu blok CIDR /28 lub /27 w kolejności tooprovide adresów IP za mało tooaccommodate dodatkowych przyszłych wymagań konfiguracyjnych.

W przypadku tworzenia tej konfiguracji jako wykonywania, zobacz toothese [przykładowych ustawień](#values) podczas tworzenia podsieci bramy.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate podsieci bramy
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Określanie serwera DNS (opcjonalne)
Serwer DNS nie jest wymagany w przypadku połączenia typu sieć wirtualna-sieć wirtualna. Jednak jeśli chcesz toohave rozpoznawania nazw zasobów, które są wdrożone tooyour sieci wirtualnej, należy określić serwer DNS. To ustawienie umożliwia określenie serwera DNS hello mają toouse do rozpoznawania nazw dla tej sieci wirtualnej. Nie powoduje ono jednak utworzenia serwera DNS.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Tworzenie bramy sieci wirtualnej
W tym kroku utworzysz hello bramy sieci wirtualnej sieci wirtualnej. Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU. W przypadku tworzenia tej konfiguracji jako wykonywania mogą odwoływać się toohello [ustawienia przykład](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate bramy sieci wirtualnej
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. Tworzenie i konfigurowanie sieci TestVNet4
Po skonfigurowaniu TestVNet1 utworzyć TestVNet4 powtarzając hello poprzednie kroki, zastępując wartości hello tych TestVNet4. Nie trzeba toowait do momentu zakończenia hello bramy sieci wirtualnej dla TestVNet1 tworzenie przed skonfigurowaniem TestVNet4. Jeśli używasz własne wartości, upewnij się, że przestrzenie adresowe hello nie pokrywały się ze wszystkimi hello sieci wirtualnych, który ma tooconnect do.

## <a name="TestVNet1Connection"></a>7. Skonfiguruj połączenie hello TestVNet1
Po zakończeniu bram sieci wirtualnej hello TestVNet1 i TestVNet4, można utworzyć sieci wirtualnej połączenia bramy. W tej sekcji utworzysz połączenie z VNet1 tooVNet4. Te kroki działa tylko dla sieci wirtualnych w hello sam subskrypcji. Jeśli w Twojej sieci wirtualne znajdują się w różnych subskrypcji, należy użyć programu PowerShell toomake hello połączenia. Zobacz hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) artykułu.

1. W **wszystkie zasoby**, przejdź toohello bramy sieci wirtualnej sieci wirtualnej. (np. **TestVNet1GW**). Kliknij przycisk **TestVNet1GW** bloku bramy sieci wirtualnej hello tooopen.
   
    ![Blok połączeń](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Blok połączeń")
2. Kliknij przycisk **+ Dodaj** tooopen hello **Dodaj połączenie** bloku.
3. Na powitania **Dodaj połączenie** bloku, w polu Nazwa hello, wpisz nazwę połączenia. (np. **TestVNet1toTestVNet4**).
   
    ![Nazwa połączenia](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Nazwa połączenia")
4. Dla opcji **Typ połączenia** Wybierz **do wirtualnymi** z listy rozwijanej hello.
5. Witaj **pierwsza brama sieci wirtualnej** wartość pola jest wypełniane automatycznie ponieważ tworzenia tego połączenia na podstawie hello określonej sieci wirtualnej bramy.
6. Witaj **druga Brama sieci wirtualnej** pole jest brama sieci wirtualnej hello hello sieci wirtualnej mają toocreate połączenia. Kliknij przycisk **wybierz inną bramę sieci wirtualnej** tooopen hello **bramy sieci wirtualnej wybierz** bloku.
   
    ![Dodawanie połączenia](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Dodawanie połączenia")
7. Bramy sieci wirtualnej hello widoku, które są wymienione w tym bloku. Pamiętaj, że wyświetlane są tylko bramy sieci wirtualnej objęte subskrypcją. Jeśli chcesz, aby brama sieci wirtualnej tooa tooconnect, który nie jest w ramach subskrypcji, użyj hello [artykułu PowerShell](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Kliknij przycisk hello bramy sieci wirtualnej, który ma tooconnect do.
9. W hello **klucz udostępniony** wpisz klucza wspólnego dla połączenia. Klucz można wygenerować lub utworzyć samodzielnie. W przypadku połączenia lokacja lokacja hello klucz użyty będzie można dokładnie hello tym samym urządzeniu lokalnym i połączenie bramy sieci wirtualnej. Witaj koncepcja jest podobna, z wyjątkiem zamiast urządzenia sieci VPN tooa łączącego się łączysz tooanother bramy sieci wirtualnej.
   
    ![Klucz współużytkowany](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Klucz współużytkowany")
10. Kliknij przycisk **OK** na hello dołu hello bloku toosave zmiany.

## <a name="TestVNet4Connection"></a>8. Skonfiguruj połączenie hello TestVNet4
Następnie należy utworzyć połączenie z TestVNet4 tooTestVNet1. Użyj hello sam metodę użytą toocreate hello połączenia z TestVNet1 tooTestVNet4. Upewnij się, że używasz hello sam wspólny klucz.

## <a name="VerifyConnection"></a>9. Weryfikowanie połączenia
Sprawdź połączenie hello. Dla każdej bramy sieci wirtualnej hello następujące:

1. Zlokalizuj bloku hello hello bramy sieci wirtualnej. (np. **TestVNet4GW**). 
2. W bloku bramy sieci wirtualnej hello, kliknij **połączeń** tooview hello połączeń bloku dla bramy sieci wirtualnej hello.

Wyświetl hello połączeń i sprawdź hello status. Po utworzeniu połączenia hello zostanie wyświetlona **zakończyło się pomyślnie** i **połączony** jako hello wartości stanu.

![Powodzenie](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Powodzenie")

Dwukrotne kliknięcie każdego połączenia oddzielnie tooview więcej informacji na temat hello połączenia.

![Podstawy](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Podstawy")

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi
Wyświetl szczegóły hello — często zadawane pytania dodatkowe informacje dotyczące połączeń do wirtualnymi.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Zobacz hello [dokumentacji maszyn wirtualnych](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) Aby uzyskać więcej informacji.
