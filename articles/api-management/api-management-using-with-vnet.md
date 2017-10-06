---
title: aaaHow toouse Azure API Management z sieciami wirtualnymi
description: "Dowiedz się, jak toosetup tooa połączenia wirtualnej sieci w sieci web Azure API Management i dostęp do usług za jego pośrednictwem."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Jak toouse Azure API Management z sieciami wirtualnymi
Sieci wirtualnych platformy Azure (sieci wirtualne) pozwalają tooplace, który żadnego z zasobów platformy Azure w sieci internet nie routeable, przez Ciebie dostęp do. Sieci te można następnie tooyour połączonych sieciach lokalnych przy użyciu różnych technologii sieci VPN. więcej informacji o sieciach wirtualnych platformy Azure zaczynają tutaj informacje hello toolearn: [omówienie sieci wirtualnych Azure](../virtual-network/virtual-networks-overview.md).

Zarządzanie interfejsami API Azure można wdrożyć wewnątrz hello sieć wirtualną (VNET), więc można uzyskać dostęp do usług zaplecza w sieci hello. Witaj portalu dla deweloperów i interfejsu API bramy, może być dostępny z Internetu hello lub tylko w ramach sieci wirtualnej hello toobe skonfigurowany.

> [!NOTE]
> Zarządzanie interfejsami API Azure obsługuje sieci wirtualnych Menedżera zasobów klasycznych jak Azure.
>
>

## <a name="enable-vpn"></a>Połączenia włączyć sieci Wirtualnej
> [!NOTE]
> Łączność sieci Wirtualnej jest dostępna w hello **Premium** i **Developer** warstw. tooswitch między warstwami hello Otwórz usługi Zarządzanie interfejsami API w hello portalu Azure, a następnie otwórz hello **skali i cenach** kartę. W obszarze hello **warstwa cenowa** sekcji, wybierz warstwę Premium lub deweloperem hello i kliknij przycisk Zapisz.
>

Otwórz usługi Zarządzanie interfejsami API w portalu Azure hello tooenable łączność sieci Wirtualnej, a hello **sieci wirtualnej** strony.

![Zarządzanie interfejsami API menu sieci wirtualnej][api-management-using-vnet-menu]

Wybierz typ dostępu do żądanego hello:

* **Zewnętrzne**: hello interfejsu API zarządzania bramy i developer portal są dostępne z hello publicznej sieci internet za pomocą zewnętrznej usługi równoważenia obciążenia. Brama Hello dostęp do zasobów w sieci wirtualnej hello.

![Publiczna komunikacja równorzędna][api-management-vnet-public]

* **Wewnętrzny**: hello interfejsu API zarządzania bramy i developer portal jest dostępny tylko w obrębie hello sieci wirtualnej za pomocą wewnętrznego modułu równoważenia obciążenia. Brama Hello dostęp do zasobów w sieci wirtualnej hello.

![Prywatna komunikacja równorzędna][api-management-vnet-private]

Teraz zostanie wyświetlona lista wszystkich regionów, których obsługa została zainicjowana usługi Zarządzanie interfejsami API. Wybierz sieć Wirtualną i podsieć dla każdego regionu. Lista Hello jest wypełniana zarówno classic i dostępne w Twojej subskrypcji platformy Azure, które są skonfigurowane w regionie hello, który jest konfigurowany sieci wirtualnych Menedżera zasobów.

> [!NOTE]
> **Punkt końcowy usługi** w hello powyżej diagram zawiera bramy/serwera Proxy, Portal wydawcy portalu dla deweloperów, GIT i hello bezpośredniego zarządzania punktu końcowego.
> **Punkt końcowy zarządzania** hello powyżej diagramu jest punkt końcowy hello hostowanych na powitania konfiguracji toomanage usługi za pośrednictwem portalu Azure i programu Powershell.
> Należy również zauważyć, że mimo że hello diagram przedstawia adresów IP dla swoich różnych punktów końcowych usługi Zarządzanie interfejsami API **tylko** reaguje na jego skonfigurowanych nazwy hostów.

> [!IMPORTANT]
> Podczas wdrażania usługi Azure API Management tooa wystąpienia menedżera zasobów w sieci Wirtualnej, usługa hello musi być w dedykowanym podsieć, która nie zawiera żadnych innych zasobów, z wyjątkiem wystąpienia usługi Azure API Management. Jeśli toodeploy podejmowana jest próba tooa wystąpienia usługi Azure API Management podsieci sieci Wirtualnej Resource Manager, która zawiera inne zasoby, hello wdrożenie zakończy się niepowodzeniem.
>
>

![Wybierz sieci VPN][api-management-setup-vpn-select]

Kliknij przycisk **zapisać** u góry hello hello ekranu.

> [!NOTE]
> Hello adres VIP wystąpienia interfejsu API zarządzania hello zmieni zawsze sieci Wirtualnej jest włączone lub wyłączone.  
> Po przeniesieniu z interfejsu API zarządzania spowoduje również zmianę Hello adres VIP **zewnętrznych** za**wewnętrzne** lub na odwrót
>


> [!IMPORTANT]
> Usunięcie interfejsu API zarządzania z sieci Wirtualnej lub zmienić hello nie została wdrożona w jednym, hello wcześniej używanych sieci Wirtualnej może pozostać zablokowane dla too4 godzin. W tym okresie go nie zostanie hello możliwe toodelete sieci Wirtualnej ani Wdrażanie nowego tooit zasobów.

## <a name="enable-vnet-powershell"></a>Połączenia Włącz sieć Wirtualną przy użyciu poleceń cmdlet programu PowerShell
Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell hello

* **Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate usługi Zarządzanie interfejsami API Azure w sieci Wirtualnej.

* **Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove istniejącej usługi Zarządzanie interfejsami API Azure w sieci wirtualnej.

## <a name="connect-vnet"></a>Połączyć tooa usługi sieci web hostowanych w sieci wirtualnej
Uzyskiwanie dostępu do usług zaplecza w nim nie różni się niż dostęp do usług publicznych się usługi API Management po toohello połączonych sieci Wirtualnej. Po prostu wpisz hello lokalny adres IP lub hello nazwę hosta (Jeśli serwer DNS jest skonfigurowany do hello sieci Wirtualnej) usługi sieci web do hello **adres URL usługi sieci Web** pole podczas tworzenia nowego interfejsu API lub edytowanie istniejących.

![Dodawanie interfejsu API z sieci VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Typowe problemy z konfiguracją sieci
Poniżej znajduje się lista typowych problemów z błędem konfiguracji, które mogą wystąpić podczas wdrażania usługi Zarządzanie interfejsami API w sieci wirtualnej.

* **Niestandardowe ustawienia serwera DNS**: hello usługi Zarządzanie interfejsami API zależy od wielu usług Azure. Zarządzanie interfejsami API znajduje się w sieci Wirtualnej przy użyciu niestandardowego serwera DNS, konieczne jest nazwy hostów hello tooresolve tych usług Azure. Wykonaj [to](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) wytyczne dotyczące niestandardowych ustawień DNS. Znajdują się w poniższej tabeli porty hello i inne wymagania dotyczące sieci dla odwołania.

> [!IMPORTANT]
> Zaleca się, korzystając z serwerów DNS niestandardowe dla hello sieci Wirtualnej, jest skonfigurowanie który **przed** wdrażania usługi API Management do niego. W przeciwnym razie należy zbyt aktualizacji usługi Zarządzanie interfejsami API hello każdej zmianie hello serwerów DNS (s), uruchamiając hello [zastosować operacji konfiguracji sieciowej](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Porty wymagane przez interfejs API zarządzania**: ruchu przychodzącego i wychodzącego do podsieci hello, w której jest wdrażane zarządzanie interfejsami API można kontrolować przy użyciu [sieciowej grupy zabezpieczeń][Network Security Group]. Jeśli którekolwiek z tych portów są niedostępne, interfejsu API zarządzania może nie działać prawidłowo i może stać się niedostępne. Co najmniej jeden z tych portów zablokowane jest posiadanie innego typowe problemy z błędem konfiguracji podczas korzystania z usługi API Management z sieci Wirtualnej.

Gdy wystąpienie usługi API Management znajduje się w sieci Wirtualnej, są używane porty hello hello w poniższej tabeli.

| Źródłowego / docelowego porty | Kierunek | Protokół transportu | Przeznaczenie | Źródłowego / docelowego | Typ dostępu |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Przychodzący |TCP |TooAPI komunikacji klienta zarządzania |INTERNET / VIRTUAL_NETWORK |Zewnętrzne |
| * / 3443 |Przychodzący |TCP |Punkt końcowy zarządzania dla portalu Azure i programu Powershell |INTERNET / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |
| * / 80, 443 |Wychodzący |TCP |Zależność od usługi Azure Storage i Azure Service Bus |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 1433 |Wychodzący |TCP |Zależność Azure SQL |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 11000 - 11999 |Wychodzący |TCP |Zależność Azure SQL w wersji 12 |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 14000 - 14999 |Wychodzący |TCP |Zależność Azure SQL w wersji 12 |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 5671 |Wychodzący |AMQP |Zależności dla zasad Centrum tooEvent dziennika i agent monitorowania |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| 6381 - 6383 / 6381 - 6383 |Dla ruchu przychodzącego i wychodzącego |UDP |Zależności w pamięci podręcznej Redis |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |-
| * / 445 |Wychodzący |TCP |Zależności w udziale plików platformy Azure dla GIT |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / * | Przychodzący |TCP |Moduł równoważenia obciążenia infrastruktury platformy Azure | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |

* **Funkcje protokołu SSL**: certyfikat SSL tooenable łańcucha budynku i sprawdzania poprawności hello zarządzanie interfejsami API usługi musi tooocsp.msocsp.com połączenia wychodzącego, mscrl.microsoft.com i crl.microsoft.com. Ta zależność nie jest wymagana, jeśli żadnych certyfikatów, możesz przekazać tooAPI zarządzania zawierają hello pełnego łańcucha toohello urzędu certyfikacji głównego.

* **Dostęp DNS**: wychodzący dostęp przez port 53 jest wymagana do komunikacji przy użyciu serwerów DNS. Jeśli istnieje niestandardowy serwer DNS na hello drugiej bramy sieci VPN, hello serwer DNS musi być dostępny podsieci hello hostingu API Management.

* **Monitorowanie kondycji i metryki**: wychodzącego łączności tooAzure monitorowania punktów końcowych, które rozwiązanie w obszarze hello następujące domeny: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Trasy Instalacja ekspresowa**: Typowa konfiguracja klienta jest toodefine własnych trasa domyślna (0.0.0.0/0), co zmusza wychodzącego Internet ruchu tooinstead przepływu lokalnymi. Tego przepływu ruchu niezmiennie dzieli łączność z usługą Azure API Management, ponieważ ruch wychodzący hello jest zablokowane lokalnie lub NAT d tooan nierozpoznawalną zbiór adresów, które nie będą działać z różnymi punkty końcowe systemu Azure. Witaj rozwiązanie jest toodefine jednej (lub więcej) trasy zdefiniowane przez użytkownika ([Udr][UDRs]) na powitania podsieci, która zawiera hello Azure API Management. PRZEZ definiuje tras specyficzne dla podsieci, które będą honorowane zamiast hello trasy domyślnej.
  Jeśli to możliwe zaleca się hello toouse następującej konfiguracji:
 * konfiguracji usługi ExpressRoute Hello anonsuje 0.0.0.0/0 i domyślnie życie tuneli wszystkich ruch wychodzący lokalnymi.
 * podsieci toohello przez zastosowane Hello zawierającej hello Azure API Management definiuje 0.0.0.0/0 z Internetu Typ następnego przeskoku.
 Witaj połączony wpływ tych kroków jest hello na poziomie podsieci przez ma pierwszeństwo przed hello ExpressRoute wymuszone tunelowanie, w związku z tym zapewnienie wychodzący dostęp do Internetu z hello Azure API Management.

>[!WARNING]  
>Azure API Management nie jest obsługiwany w konfiguracji usługi ExpressRoute który **niepoprawnie cross anonsowanie trasy z hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka**. Konfiguracji usługi ExpressRoute, które mają publicznej komunikacji równorzędnej skonfigurowane, otrzyma anonsów tras firmy Microsoft dla dużych zestawów zakresów adresów IP firmy Microsoft Azure. Jeśli te zakresy adresów są niepoprawnie cross anonsowany w ścieżki prywatnej komunikacji równorzędnej hello, wynik końcowy hello są wszystkich pakietów sieciowych wychodzące z wystąpienia usługi Azure API Management hello podsieci sieci lokalnej klienta niepoprawnie tunneled życie tooa infrastruktura. Ten przepływ sieci dzieli Azure API Management. problem toothis rozwiązania Hello jest toostop tras między reklamy hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka.


## <a name="troubleshooting"></a>Rozwiązywanie problemów
Podczas wprowadzania zmian tooyour sieci, zapoznaj się zbyt[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate Jeśli hello usługi Zarządzanie interfejsami API utracił tooany dostępu z hello kluczowych zasobów, których ona zależy. Stan łączności Hello powinny być aktualizowane co 15 minut.

## <a name="limitations"></a>Ograniczenia
* W podsieci zawierającej wystąpienia interfejsu API zarządzania nie może zawierać innych typów zasobów platformy Azure.
* Witaj podsieci i hello zarządzanie interfejsami API usługi musi być w hello tej samej subskrypcji.
* Nie można przenieść w podsieci zawierającej wystąpienia interfejsu API zarządzania różnych subskrypcji.
* W wewnętrznej sieci wirtualnej, wewnętrzny adres IP będą dostępne tylko zakres hello już wspomniano w [RFC 1918](https://tools.ietf.org/html/rfc1918), nie można podać publicznego adresu IP.
* W przypadku wdrożeń w przypadku interfejsu API zarządzania z wewnętrzne sieci wirtualne skonfigurowane, użytkownicy są odpowiedzialne za zarządzanie własnych równoważenia zgodnie z nich hello DNS obciążenia.


## <a name="related-content"></a>Związane z zawartością
* [Łączenie toobackend sieci wirtualnej przy użyciu bramy sieci Vpn](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Łączenie z różne modele wdrażania sieci wirtualnej](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Jak wywołuje hello toouse tootrace inspektora interfejsu API w usłudze Azure API Management](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
