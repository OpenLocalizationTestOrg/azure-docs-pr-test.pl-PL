---
title: "aaaOverview konfiguracji o wysokiej dostępności z bramy sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie opcji konfiguracji o wysokiej dostępności przy użyciu bram Azure VPN Gateway."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności
Ten artykuł zawiera omówienie opcji konfiguracji połączeń obejmujących wiele lokalizacji i połączeń między sieciami wirtualnymi o wysokiej dostępności przy użyciu bram Azure VPN Gateway.

## <a name = "activestandby"></a>O nadmiarowość bramy sieci VPN platformy Azure
Każda brama Azure VPN Gateway składa się z dwóch wystąpień działających w konfiguracji aktywne-w gotowości. Zaplanowanej konserwacji lub nieplanowanych przerw w działaniu wykonywanej toohello aktywnym wystąpieniu wystąpienie rezerwy hello może automatycznie przejąć (failover) i wznowić hello S2S sieci VPN lub połączeń do wirtualnymi. Przełącznik Hello za pośrednictwem spowoduje krótkie przerwy. Dotyczących zaplanowanej obsługi łączności hello powinny zostać przywrócone w ciągu 10 sekund too15. Nieplanowane problemów hello połączenia odzyskiwania będzie większy, o 1 minuta too1 i pół minut w najgorszym przypadku hello. Dla bramy toohello połączeń klienta P2S VPN połączeń P2S hello zostanie rozłączona i hello użytkownicy muszą tooreconnect z komputerów klienckich hello.

![Konfiguracja aktywne-w gotowości](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Połączenia o wysokiej dostępności obejmujące wiele lokalizacji
tooprovide większą dostępność sieci między lokalnych połączeń, istnieje kilka opcji:

* Wiele lokalnych urządzeń sieci VPN
* Brama Azure VPN Gateway w konfiguracji aktywne-aktywne
* Połączenie obu tych opcji

### <a name = "activeactiveonprem"></a>Wiele urządzeń lokalnych, sieci VPN
Można użyć wielu urządzeniach sieci VPN z lokalnej sieci tooconnect tooyour Azure bramy sieci VPN, pokazane na powitania po diagramu:

![Wiele lokalnych połączeń sieci VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Ta konfiguracja zapewnia wiele tuneli active z hello tej samej sieci VPN platformy Azure bramy tooyour urządzeniami lokalnymi w hello tej samej lokalizacji. Istnieją pewne wymagania i ograniczenia:

1. Należy toocreate wiele połączeń sieci VPN S2S z tooAzure urządzenia sieci VPN. Podczas łączenia wielu urządzeniach sieci VPN z hello lokalnego tej samej sieci tooAzure, należy toocreate jedną bramę sieci lokalnej dla każdego urządzenia sieci VPN i jedno połączenie z bramy sieci lokalnej toohello bramy sieci VPN platformy Azure.
2. bramy sieci lokalnej Hello odpowiadającego tooyour urządzenia sieci VPN musi mieć unikatowy publicznych adresów IP w hello właściwości "GatewayIpAddress".
3. Ta konfiguracja wymaga użycia protokołu BGP. Każdej bramy sieci lokalnej reprezentujący urządzenia sieci VPN musi mieć unikatowy adres IP elementu równorzędnego protokołu BGP, na określony we właściwości "BgpPeerIpAddress" hello.
4. pole właściwości prefiks adresu Hello w każdej bramy sieci lokalnej musi nie mogą się pokrywać. Należy określić "BgpPeerIpAddress" hello w /32 formacie CIDR hello prefiks adresu pola, na przykład 10.200.200.254/32.
5. Należy użyć protokołu BGP tooadvertise hello prefiksy tego samego elementu hello prefiksy tooyour sieci VPN platformy Azure Brama sieci lokalnej tego samego i hello ruch zostanie przekazany przez te tunele jednocześnie.
6. Każde połączenie jest uwzględniane hello maksymalna liczba tuneli dla bramy sieci VPN platformy Azure, 10 dla podstawowe i standardowe jednostki SKU i 30 dla wysokowydajnej jednostki SKU. 

W tej konfiguracji bramy sieci VPN platformy Azure hello jest nadal w trybie aktywnego gotowości, hello tak samo trybu failover i krótki przerwania zostanie wykonane zgodnie z opisem [powyżej](#activestandby). Ta konfiguracja chroni przed awariami lub przerwami w działaniu sieci lokalnej i urządzeń sieci VPN.

### <a name="active-active-azure-vpn-gateway"></a>Brama Azure VPN Gateway w konfiguracji aktywne-aktywne
Można teraz utworzyć bramę sieci VPN platformy Azure w konfiguracji aktywny aktywny, gdy oba wystąpienia bramy hello maszyn wirtualnych będzie ustanowienie połączenia VPN S2S tuneli tooyour lokalnego urządzenia sieci VPN, jak pokazano powitania po diagramu:

![Konfiguracja aktywne-aktywne](./media/vpn-gateway-highlyavailable/active-active.png)

W tej konfiguracji każde wystąpienie bramy Azure będzie mieć unikatowe publicznego adresu IP, a każdy ustanowią sieci VPN S2S protokołu IPsec/IKE tunelu tooyour lokalnej sieci VPN urządzenia określone w bramie sieci lokalnej i połączenia. Pamiętaj, że oba tuneli VPN jest częścią hello tego samego połączenia. Nadal będzie konieczne tooconfigure tooaccept urządzenia sieci VPN z lokalnymi lub ustanawiania dwie sieci VPN S2S tuneli toothose dwóch sieci VPN platformy Azure bramy publicznych adresów IP.

Ponieważ hello wystąpieniach bramy Azure znajdują się w konfiguracji aktywny / aktywny, hello ruch z Twojej sieci wirtualnej platformy Azure tooyour lokalnej sieci będą kierowane przez tunele obu jednocześnie, nawet w przypadku lokalnego urządzenia sieci VPN mogą preferować jeden tunel za pośrednictwem Witaj innych. Należy pamiętać, chociaż hello takim samym przepływie TCP lub UDP będzie zawsze przechodzenia hello tego samego tunelu lub ścieżka, chyba że konserwacji zdarzenie w jednym z wystąpień hello.

W przypadku wystąpienia bramy tooone zaplanowanej konserwacji lub nieplanowanego zdarzenia hello tunelu IPsec z tego wystąpienia tooyour w lokalnym urządzenia sieci VPN zostanie odłączona. Witaj odpowiednie trasy na urządzeniach sieci VPN powinna być usunięte lub wycofane automatycznie, dzięki czemu będzie można przełączyć hello ruchu za pośrednictwem toohello inne aktywne tunelu IPsec. Na hello Azure po stronie przełącznika hello za pośrednictwem nastąpi automatycznie z wystąpienia active toohello wystąpienia hello, których to dotyczy.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Podwójna nadmiarowość: bramy sieci VPN w konfiguracji aktywne-aktywne dla platformy Azure i sieci lokalnych
Opcja najbardziej niezawodnym Hello jest toocombine hello aktywny aktywny bram w sieci i Azure, jak pokazano na poniższym diagramie hello.

![Podwójna nadmiarowość](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

W tym miejscu utworzyć i skonfigurować hello bramy sieci VPN platformy Azure w konfiguracji aktywny aktywny i Tworzenie bramy sieci lokalnej i dwa połączenia z dwoma lokalnego urządzenia sieci VPN zgodnie z powyższym opisem. wynik Hello jest z łącznością pełnej sieci 4 tuneli protokołu IPsec między sieci wirtualnej platformy Azure i siecią lokalną.

Wszystkich bram i tunele są aktywne z hello Azure po stronie, więc hello ruch zostanie rozmieszczone na wszystkie 4 tuneli równocześnie, mimo że każdy protokół TCP lub UDP przepływu zostanie ponownie wykonaj hello tunelu tej samej lub ścieżki z hello Azure po stronie. Mimo że przez rozłożenie hello ruchu, mogą zobaczyć nieco większa przepustowość za pośrednictwem tuneli protokołu IPsec hello, hello podstawowym celem tej konfiguracji jest wysokiej dostępności. I powodu statystyczne toohello charakter rozpraszania hello, jest trudne tooprovide hello pomiaru ruchu aplikacji w różnych warunków będzie miało wpływ na powitania łącznej przepływności.

Ta topologia wymaga dwóch bram sieci lokalnej i para hello toosupport dwa połączenia lokalnego urządzenia sieci VPN, a Protokół BGP jest wymagana tooallow hello dwa połączenia toohello tej samej sieci lokalnej. Te wymagania są hello takie same jak hello [powyżej](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Połączenia o wysokiej dostępności między sieciami wirtualnymi za pośrednictwem bram Azure VPN Gateway
Witaj tej samej konfiguracji aktywny aktywny można także zastosować tooAzure wirtualnymi do połączenia. Można utworzyć bramy sieci VPN aktywny aktywny dla obu sieci wirtualnej i połączyć je razem tooform hello sam pełny siatki łączności 4 tuneli między Witaj dwie sieci wirtualnych, jak pokazano w hello diagramie poniżej:

![Połączenia między sieciami wirtualnymi](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Dzięki temu, że zawsze są dwa tunele między dwiema sieciami wirtualnego hello wszystkie zdarzenia zaplanowanej konserwacji, zapewniając zwiększyć dostępność. Mimo że hello samej topologii dla łączności między lokalizacjami wymaga dwóch połączeń, topologii sieci wirtualnej do sieci wirtualnej hello przedstawionych powyżej, należy tylko jedno połączenie dla każdej bramy. Ponadto Protokół BGP jest opcjonalne, chyba że routing tranzytowy za pośrednictwem połączenia do wirtualnymi hello jest wymagana.

## <a name="next-steps"></a>Następne kroki
Zobacz [konfigurowania bramy sieci VPN aktywny-aktywny między lokalizacjami i połączeń między wirtualnymi do](vpn-gateway-activeactive-rm-powershell.md) procedury tooconfigure aktywny aktywny między lokalizacjami i połączeń do wirtualnymi.

