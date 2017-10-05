---
title: "Jak używać usługi Azure API Management z sieciami wirtualnymi"
description: "Dowiedz się, jak nawiązanie połączenia z siecią wirtualną w Azure API Management i dostęp do usług sieci web za jego pośrednictwem."
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
ms.openlocfilehash: 268cee739188d81feffc36ac07fcdfa18ff95a4d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-azure-api-management-with-virtual-networks"></a>Jak używać usługi Azure API Management z sieciami wirtualnymi
Sieci wirtualnych platformy Azure (sieci wirtualne) umożliwiają umieszczać zasobów platformy Azure w kontroli dostępu do sieci routeable z systemem innym niż internet. Te sieci następnie mogą być połączone z sieciami lokalnymi przy użyciu różnych technologii sieci VPN. Aby dowiedzieć się więcej o sieciach wirtualnych platformy Azure Uruchom z informacjami w tym miejscu: [omówienie sieci wirtualnych Azure](../virtual-network/virtual-networks-overview.md).

Zarządzanie interfejsami API Azure można wdrożyć w sieci wirtualnej (VNET), więc można uzyskać dostęp do usług zaplecza w sieci. Portalu dla deweloperów i bramy interfejsu API, można skonfigurować jako dostępny z Internetu lub tylko w ramach sieci wirtualnej.

> [!NOTE]
> Zarządzanie interfejsami API Azure obsługuje sieci wirtualnych Menedżera zasobów klasycznych jak Azure.
>
>

## <a name="enable-vpn"></a>Połączenia włączyć sieci Wirtualnej
> [!NOTE]
> Łączność sieci Wirtualnej jest dostępna w **Premium** i **Developer** warstw. Aby przełączyć się między warstwami, otwórz usługi Zarządzanie interfejsami API w portalu Azure, a następnie otwórz **skali i cenach** kartę. W obszarze **warstwa cenowa** sekcji, wybierz warstwę Premium lub deweloperem i kliknij przycisk Zapisz.
>

Aby włączyć łączność w sieci Wirtualnej, należy otworzyć usługi Zarządzanie interfejsami API na platformie Azure, portalu i Otwórz **sieci wirtualnej** strony.

![Zarządzanie interfejsami API menu sieci wirtualnej][api-management-using-vnet-menu]

Wybierz typ żądany dostęp:

* **Zewnętrzne**: portal bramy i deweloperów zarządzanie interfejsami API są dostępne z publicznego Internetu za pomocą zewnętrznej usługi równoważenia obciążenia. Bramy mogą uzyskiwać dostęp do zasobów w sieci wirtualnej.

![Publiczna komunikacja równorzędna][api-management-vnet-public]

* **Wewnętrzny**: portalu bramy i deweloperów interfejsu API zarządzania jest dostępny tylko w obrębie sieci wirtualnej za pomocą wewnętrznego modułu równoważenia obciążenia. Bramy mogą uzyskiwać dostęp do zasobów w sieci wirtualnej.

![Prywatna komunikacja równorzędna][api-management-vnet-private]

Teraz zostanie wyświetlona lista wszystkich regionów, których obsługa została zainicjowana usługi Zarządzanie interfejsami API. Wybierz sieć Wirtualną i podsieć dla każdego regionu. Lista zostanie wypełniona z klasycznym i dostępne w Twojej subskrypcji platformy Azure, które są skonfigurowane w regionie, który jest konfigurowany sieci wirtualnych Menedżera zasobów.

> [!NOTE]
> **Punkt końcowy usługi** na powyższym diagramie obejmuje bramy/serwera Proxy, Portal wydawcy portalu dla deweloperów, GIT i bezpośredniego zarządzania punktu końcowego.
> **Punkt końcowy zarządzania** na powyższym diagramie jest punktem końcowym hostowanych w usłudze, aby zarządzać konfiguracją za pośrednictwem portalu Azure i programu Powershell.
> Należy również zauważyć, że mimo, że na diagramie przedstawiono adresów IP dla swoich różnych punktów końcowych usługi Zarządzanie interfejsami API **tylko** reaguje na jego skonfigurowanych nazwy hostów.

> [!IMPORTANT]
> Podczas wdrażania wystąpienia zarządzanie interfejsami API Azure Resource Manager sieci Wirtualnej, usługa musi być w dedykowanym podsieć, która nie zawiera żadnych innych zasobów, z wyjątkiem wystąpienia usługi Azure API Management. Jeśli próby wdrożenie wystąpienia usługi Azure API Management do podsieci sieci Wirtualnej Resource Manager zawierający inne zasoby, wdrożenie zakończy się niepowodzeniem.
>
>

![Wybierz sieci VPN][api-management-setup-vpn-select]

Kliknij przycisk **zapisać** w górnej części ekranu.

> [!NOTE]
> Adres VIP wystąpienia interfejsu API zarządzania zmieni zawsze sieci Wirtualnej jest włączone lub wyłączone.  
> Po przeniesieniu z interfejsu API zarządzania spowoduje również zmianę adresu VIP **zewnętrznych** do **wewnętrzne** lub na odwrót
>


> [!IMPORTANT]
> Usuń API Management z sieci Wirtualnej lub zmienić ten, który został wdrożony w uprzednio używanych sieci Wirtualnej mogą pozostać zablokowane przez 4 godziny. W tym okresie nie będzie można usunąć sieci Wirtualnej lub wdrożyć nowy zasób.

## <a name="enable-vnet-powershell"></a>Połączenia Włącz sieć Wirtualną przy użyciu poleceń cmdlet programu PowerShell
Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell

* **Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) można utworzyć usługi Azure API Management w sieci Wirtualnej.

* **Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) Aby przenieść istniejącą usługę Azure API Management w sieci wirtualnej.

## <a name="connect-vnet"></a>Nawiązywanie połączenia z usługą sieci web hostowanych w sieci wirtualnej
Po usługi API Management jest podłączony do sieci Wirtualnej, dostęp do usług zaplecza w nim nie różni się od uzyskiwanie dostępu do usług publicznego. Po prostu wpisz lokalny adres IP lub nazwę hosta (Jeśli serwer DNS jest skonfigurowany dla sieci Wirtualnej) usługi sieci web do **adres URL usługi sieci Web** pole podczas tworzenia nowego interfejsu API lub edytowanie istniejących.

![Dodawanie interfejsu API z sieci VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Typowe problemy z konfiguracją sieci
Poniżej znajduje się lista typowych problemów z błędem konfiguracji, które mogą wystąpić podczas wdrażania usługi Zarządzanie interfejsami API w sieci wirtualnej.

* **Niestandardowe ustawienia serwera DNS**: Usługa interfejsu API zarządzania zależy od wielu usług Azure. Zarządzanie interfejsami API znajduje się w sieci Wirtualnej przy użyciu niestandardowego serwera DNS, musi rozpoznać nazwy hostów tych usług Azure. Wykonaj [to](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) wytyczne dotyczące niestandardowych ustawień DNS. Znajdują się w poniższej tabeli portów i inne wymagania dotyczące sieci dla odwołania.

> [!IMPORTANT]
> Zaleca się, że jeśli używasz niestandardowych serwerów DNS dla sieci Wirtualnej, skonfigurowaniu który **przed** wdrażania usługi API Management do niego. W przeciwnym razie należy zaktualizować usługi Zarządzanie interfejsami API każdej zmianie serwerów DNS (s), uruchamiając [zastosować operacji konfiguracji sieciowej](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Porty wymagane przez interfejs API zarządzania**: ruchu przychodzącego i wychodzącego do podsieci, w której jest wdrażane zarządzanie interfejsami API można kontrolować przy użyciu [sieciowej grupy zabezpieczeń][Network Security Group]. Jeśli którekolwiek z tych portów są niedostępne, interfejsu API zarządzania może nie działać prawidłowo i może stać się niedostępne. Co najmniej jeden z tych portów zablokowane jest posiadanie innego typowe problemy z błędem konfiguracji podczas korzystania z usługi API Management z sieci Wirtualnej.

Gdy wystąpienie usługi API Management znajduje się w sieci Wirtualnej, są używane porty w poniższej tabeli.

| Źródłowego / docelowego porty | Kierunek | Protokół transportu | Przeznaczenie | Źródłowego / docelowego | Typ dostępu |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Przychodzący |TCP |Zarządzanie interfejsami API komunikacji klienta |INTERNET / VIRTUAL_NETWORK |Zewnętrzne |
| * / 3443 |Przychodzący |TCP |Punkt końcowy zarządzania dla portalu Azure i programu Powershell |INTERNET / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |
| * / 80, 443 |Wychodzący |TCP |Zależność od usługi Azure Storage i Azure Service Bus |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 1433 |Wychodzący |TCP |Zależność Azure SQL |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 11000 - 11999 |Wychodzący |TCP |Zależność Azure SQL w wersji 12 |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 14000 - 14999 |Wychodzący |TCP |Zależność Azure SQL w wersji 12 |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / 5671 |Wychodzący |AMQP |Zależność od dziennika zasad Centrum zdarzeń i agenta monitorowania |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| 6381 - 6383 / 6381 - 6383 |Dla ruchu przychodzącego i wychodzącego |UDP |Zależności w pamięci podręcznej Redis |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |-
| * / 445 |Wychodzący |TCP |Zależności w udziale plików platformy Azure dla GIT |VIRTUAL_NETWORK / INTERNET |Zewnętrzne i wewnętrzne |
| * / * | Przychodzący |TCP |Moduł równoważenia obciążenia infrastruktury platformy Azure | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Zewnętrzne i wewnętrzne |

* **Funkcje protokołu SSL**: Aby umożliwić tworzenie łańcucha certyfikatów SSL i sprawdzania poprawności zarządzanie interfejsami API usługi musi mieć łączność sieciową wychodzących ocsp.msocsp.com, mscrl.microsoft.com i crl.microsoft.com. Ta zależność nie jest wymagana, jeśli dowolny certyfikat, które zostaną przesłane do interfejsu API zarządzania zawierają pełny łańcuch do głównego urzędu certyfikacji.

* **Dostęp DNS**: wychodzący dostęp przez port 53 jest wymagana do komunikacji przy użyciu serwerów DNS. Jeśli istnieje niestandardowy serwer DNS na drugim końcu bramy sieci VPN, serwer DNS musi być dostępny w podsieci hostingu API Management.

* **Monitorowanie kondycji i metryki**: połączenie sieciowe ruchu wychodzącego Azure punktów końcowych monitorowania, które rozwiązanie w następujących domen: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Trasy Instalacja ekspresowa**: Typowa konfiguracja klienta jest określenie własnych trasa domyślna (0.0.0.0/0), co zmusza wychodzący ruch internetowy, zamiast niego przepływ lokalnymi. Ten przepływ ruchu niezmiennie dzieli łączność z usługą Azure API Management ruch wychodzący zablokowanych lokalnie, ponieważ NAT czy nierozpoznawalną zbiór adresów, które nie będą działać z różnymi punkty końcowe systemu Azure. Rozwiązanie jest określenie jednego (lub więcej) trasy zdefiniowane przez użytkownika ([Udr][UDRs]) w podsieci, która zawiera Azure API Management. PRZEZ definiuje tras specyficzne dla podsieci, które będą honorowane zamiast trasy domyślnej.
  Jeśli to możliwe zaleca się następującej konfiguracji:
 * Konfiguracji usługi ExpressRoute anonsuje 0.0.0.0/0 i domyślnie życie tuneli wszystkich ruch wychodzący lokalnymi.
 * PRZEZ stosowana do podsieci, zawierający Azure API Management definiuje 0.0.0.0/0 z Internetu Typ następnego przeskoku.
 Łączna tych kroków powoduje, że poziomie podsieci przez ma pierwszeństwo przed ExpressRoute, wymuszone tunelowanie, w związku z tym zapewnienie wychodzący dostęp do Internetu z usługi Azure API Management.

>[!WARNING]  
>Azure API Management nie jest obsługiwany w konfiguracji usługi ExpressRoute który **niepoprawnie cross anonsować tras z publicznej komunikacji równorzędnej ścieżki do ścieżki prywatnej komunikacji równorzędnej**. Konfiguracji usługi ExpressRoute, które mają publicznej komunikacji równorzędnej skonfigurowane, otrzyma anonsów tras firmy Microsoft dla dużych zestawów zakresów adresów IP firmy Microsoft Azure. Jeśli te zakresy adresów są niepoprawnie cross anonsowany w ścieżce prywatnej komunikacji równorzędnej, wynik końcowy są wszystkie pakiety wychodzącego z podsieci wystąpienia usługi Azure API Management niepoprawnie force-tunneled do sieci lokalnej klienta infrastruktura. Ten przepływ sieci dzieli Azure API Management. Rozwiązanie tego problemu jest zatrzymanie tras między reklam z publicznej komunikacji równorzędnej ścieżki do ścieżki prywatnej komunikacji równorzędnej.


## <a name="troubleshooting"></a>Rozwiązywanie problemów
Podczas wprowadzania zmian w sieci, zapoznaj się [NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), aby sprawdzić, czy usługi Zarządzanie interfejsami API utracił dostęp do wszystkich kluczowych zasobów, których ona zależy. Stan powinien być aktualizowany co 15 minut.

## <a name="limitations"></a>Ograniczenia
* W podsieci zawierającej wystąpienia interfejsu API zarządzania nie może zawierać innych typów zasobów platformy Azure.
* Podsieć i usługi API Management musi być w tej samej subskrypcji.
* Nie można przenieść w podsieci zawierającej wystąpienia interfejsu API zarządzania różnych subskrypcji.
* W wewnętrznej sieci wirtualnej, tylko wewnętrzny adres IP będą dostępne z zakresu w [RFC 1918](https://tools.ietf.org/html/rfc1918), nie można podać publicznego adresu IP.
* W przypadku wdrożeń w przypadku interfejsu API zarządzania z wewnętrzne sieci wirtualne skonfigurowane, użytkownicy są odpowiedzialne za zarządzanie własnych równoważenia zgodnie z nich DNS obciążenia.


## <a name="related-content"></a>Związane z zawartością
* [Połączenie wirtualnej sieci do wewnętrznej bazy danych przy użyciu bramy sieci Vpn](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Łączenie z różne modele wdrażania sieci wirtualnej](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Sposób użycia interfejsu API inspektora śledzenia wywołań w usłudze Azure API Management](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect to a web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
