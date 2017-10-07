---
title: "aaaDiagnose lokalnymi łączności za pośrednictwem bramy sieci VPN z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toodiagnose lokalnymi łączności za pośrednictwem bramy sieci VPN z rozwiązywaniem problemów zasobów Azure obserwatora sieciowego."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnozowanie łączność z lokalnymi za pośrednictwem bramy sieci VPN

Brama sieci VPN umożliwia rozwiązanie hybrydowe toocreate adresów hello na potrzeby bezpiecznego połączenia między siecią lokalną a sieci wirtualnej platformy Azure. Zgodnie z wymaganiami są unikatowe, dlatego jest wybór hello lokalnego urządzenia sieci VPN. Azure obecnie obsługuje [kilka urządzeń sieci VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) stale zweryfikowaniu współpracują z hello przez dostawców urządzeń. Sprawdź ustawienia konfiguracji określonego urządzenia hello przed rozpoczęciem konfigurowania lokalnego urządzenia sieci VPN. Podobnie, Brama sieci VPN platformy Azure jest skonfigurowany z zestawem [obsługiwanymi parametrami IPsec](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) służące do nawiązywania połączenia. Obecnie nie istnieje sposób dla Ciebie toospecify lub wybierz określona kombinacja parametrów IPsec z hello bramy sieci VPN platformy Azure. Ustalania udane połączenie między lokalną i platformą Azure hello w lokalnym ustawienia urządzenia sieci VPN musi być zgodny z parametrów protokołu IPsec hello określonej przez bramy sieci VPN platformy Azure. Jeśli hello ustawienia są poprawne, brak utraty połączenia i do tej pory rozwiązywania tych problemów nie prosta i zwykle trwało godziny tooidentify i napraw problem hello.

Z hello Azure obserwatora sieciowego Rozwiązywanie problemów z funkcją, są toodiagnose możliwe problemy z połączeniami i bramy i w ciągu minut mieć wystarczającej ilości informacji toomake problemu hello toorectify świadomej decyzji.

## <a name="scenario"></a>Scenariusz

Połączenie tooconfigure site-to-site platformy Azure i lokalnymi przy użyciu FortiGate hello lokalnej bramy sieci VPN. tooachieve tego scenariusza należy wymagają powitania po zakończeniu instalacji:

1. Brama sieci wirtualnej - hello bramy sieci VPN w systemie Azure
1. Bramy sieci lokalnej - hello [lokalnej bramy sieci VPN (FortiGate)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) reprezentacja w chmurze Azure
1. Połączenie lokacja lokacja (zasady na podstawie) - [połączenie między hello bramy sieci VPN i hello lokalnego routera](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Konfigurowanie FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Szczegółowe wskazówki krok po kroku dotyczące konfigurowania konfiguracji lokacja-lokacja można znaleźć, odwiedzając: [tworzenie sieci wirtualnej za pomocą połączenia lokacja-lokacja za pomocą portalu Azure hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Jeden z kroków konfiguracji krytyczne hello konfiguruje parametry Komunikacja IPsec hello, wszelkie błędnej konfiguracji prowadzi tooloss łączności między hello siecią lokalną a platformą Azure. Obecnie bramy sieci VPN platformy Azure są hello toosupport skonfigurowane następujące parametry IPsec dotyczących fazy 1. Należy zwrócić uwagę, jak wspomniano wcześniej, nie można modyfikować tych ustawień.  Jak widać w poniższej tabeli hello hello algorytmów szyfrowania obsługiwane przez bramę sieci VPN platformy Azure są AES256, AES128 i algorytmu 3DES.

### <a name="ike-phase-1-setup"></a>Instalator faza 1 IKE

| **Właściwość** | **PolicyBased** | **Brama RouteBased i Standard lub VPN wysokiej wydajności** |
| --- | --- | --- |
| Wersja IKE |IKEv1 |IKEv2 |
| Grupa Diffie’ego-Hellmana |Grupa 2 (1024 bity) |Grupa 2 (1024 bity) |
| Metoda uwierzytelniania |Klucz wstępny |Klucz wstępny |
| Algorytmy szyfrowania |AES256 AES128 3DES |AES256 3DES |
| Algorytm skrótu |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Okres istnienia (czas) skojarzenia zabezpieczeń (Security Association — SA) fazy 1 |28 800 sekund |10 800 sekund |

Jako użytkownik, będzie wymagany tooconfigure Twojego FortiGate Przykładowa konfiguracja można znaleźć w [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Nieświadomie skonfigurowany toouse Twojego FortiGate SHA-512 jako hello algorytmem wyznaczania wartości skrótu. Ten algorytm nie jest obsługiwany algorytm dla połączeń opartych na zasadach, pracy połączenia sieci VPN.

Te problemy są tootroubleshoot twardym i są często nieintuicyjnych głównych przyczyn. W takim przypadku można otworzyć Pomoc tooget biletu pomocy technicznej dotyczące rozwiązywania problemu hello. Ale z obserwatora sieciowego Azure Rozwiązywanie problemów z interfejsu API, można zidentyfikować te problemy samodzielnie.

## <a name="troubleshooting-using-azure-network-watcher"></a>Rozwiązywanie problemów przy użyciu usługi Azure obserwatora sieciowego

toodiagnose połączenia, połączenie tooAzure środowiska PowerShell i zainicjować hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet. Można znaleźć hello uzyskać szczegółowe informacje na temat używania tego polecenia cmdlet w [połączenia - środowiska PowerShell i rozwiązywanie problemów z Brama sieci wirtualnej](network-watcher-troubleshoot-manage-powershell.md). To polecenie cmdlet może trwać toofew toocomplete minut.

Po zakończeniu działania polecenia cmdlet hello można przechodzić toohello lokalizacji magazynu określony w poleceniu cmdlet hello tooget szczegółowe informacje na o problemie hello i dzienniki. Azure obserwatora sieciowego tworzy folderu zip, który zawiera następujące pliki dziennika hello:

![1][1]

Otwórz hello pliku o nazwie IKEErrors.txt i wyświetla następujące hello o błędzie, informujący, wystąpił problem z lokalnym IKE ustawienia konfiguracji.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Można uzyskać szczegółowe informacje z hello Scrubbed wfpdiag.txt o błędzie hello, ponieważ w takim przypadku informacje o że `ERROR_IPSEC_IKE_POLICY_MATCH` tego tooconnection realizacji nie działa prawidłowo.

Inny powszechnym błędem konfiguracji jest hello Określanie niepoprawne kluczy współużytkowanych. W razie hello poprzedzających przykład podał różnych kluczy współużytkowanych, hello IKEErrors.txt pokazuje hello następujący błąd: `Error: Authentication failed. Check shared key`.

Azure obserwatora sieciowego Rozwiązywanie problemów z funkcją pozwala toodiagnose oraz rozwiązywanie problemów z bramy sieci VPN i połączeń z hello łatwość prostego polecenia cmdlet programu PowerShell. Obecnie firma Microsoft obsługuje diagnostykę hello następujące warunki i działają na dodanie więcej warunku.

### <a name="gateway"></a>Brama

| Typ błędu | Przyczyna | Log|
|---|---|---|
| NoFault | Gdy błąd nie została wykryta. |Tak|
| GatewayNotFound | Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie. |Nie|
| PlannedMaintenance |  Wystąpienie bramy jest w trakcie konserwacji.  |Nie|
| UserDrivenUpdate | Gdy aktualizacja użytkownika jest w toku. Może to być operacji zmiany rozmiaru. | Nie |
| VipUnResponsive | Nie można osiągnąć hello głównej wystąpienie hello bramy. Dzieje się tak, gdy hello badania kondycji nie powiodło się. | Nie |
| PlatformInActive | Istnieje problem z platformą hello. | Nie|
| ServiceNotRunning | Usługa podstawowej Hello nie jest uruchomiona. | Nie|
| NoConnectionsFoundForGateway | Połączenia nie istnieje w bramie hello. Jest to tylko ostrzeżenie.| Nie|
| ConnectionsNotConnected | Brak połączenia hello są połączone. Jest to tylko ostrzeżenie.| Tak|
| GatewayCPUUsageExceeded | Bieżące użycie bramy Hello użycia procesora CPU jest > 95%. | Tak |

### <a name="connection"></a>Połączenie

| Typ błędu | Przyczyna | Log|
|---|---|---|
| NoFault | Gdy błąd nie została wykryta. |Tak|
| GatewayNotFound | Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie. |Nie|
| PlannedMaintenance | Wystąpienie bramy jest w trakcie konserwacji.  |Nie|
| UserDrivenUpdate | Gdy aktualizacja użytkownika jest w toku. Może to być operacji zmiany rozmiaru.  | Nie |
| VipUnResponsive | Nie można osiągnąć hello głównej wystąpienie hello bramy. Zdarza się, gdy hello badania kondycji nie powiodło się. | Nie |
| ConnectionEntityNotFound | Brak konfiguracji połączenia. | Nie |
| ConnectionIsMarkedDisconnected | Witaj połączenia jest oznaczony jako "odłączony". |Nie|
| ConnectionNotConfiguredOnGateway | Witaj podległej usłudze nie ma powitalne skonfigurowane połączenie. | Tak |
| ConnectionMarkedStandy | źródłowa usługa Hello jest oznaczona jako stan wstrzymania.| Tak|
| Authentication | Niezgodność klucz wstępny. | Tak|
| PeerReachability | Brama równorzędnej Hello jest nieosiągalny. | Tak|
| IkePolicyMismatch | Brama równorzędnej Hello ma zasady IKE, które nie są obsługiwane przez platformę Azure. | Tak|
| Błąd WfpParse | Wystąpił błąd podczas analizowania dziennika platformy filtrowania systemu Windows hello. |Tak|

## <a name="next-steps"></a>Następne kroki

Dowiedz się toocheck połączenie bramy sieci VPN z programu PowerShell i automatyzacja Azure po przejściu na stronę [bramy sieci VPN monitora obserwatora sieciowego Azure rozwiązywania problemów](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
