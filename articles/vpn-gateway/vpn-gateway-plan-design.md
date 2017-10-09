---
title: "Planowanie i projektowanie pod kątem połączeń między lokalizacjami: Brama sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat bramy sieci VPN planowania i projektowania dla między różnymi lokalizacjami, hybrydowej i połączeń do wirtualnymi"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Planowanie i projektowanie dla usługi VPN Gateway

Planowanie i projektowanie sieci między lokalizacjami i konfiguracje sieci wirtualnej do sieci wirtualnej może być proste i złożone, w zależności od potrzeb sieci. W tym artykule przedstawiono podstawowe zagadnienia dotyczące planowania i projektowania.

## <a name="planning"></a>Planowanie

### <a name="compare"></a>Opcje łączności między lokalizacjami

Jeśli chcesz tooconnect lokalnej bezpiecznie Lokacje sieci wirtualnej tooa, więc ma trzy różne sposoby toodo: lokacja-lokacja, punkt-lokacja i ExpressRoute. Porównaj hello różnych między lokalizacjami połączeń, które są dostępne. wybrana opcja Hello może zależeć od różnych zagadnienia, takie jak:

* Jakiego rodzaju przepływności wymaga rozwiązanie?
* Czy chcesz toocommunicate za pośrednictwem hello publicznej sieci Internet za pośrednictwem bezpiecznej sieci VPN lub za pośrednictwem prywatnego połączenia?
* Masz publicznego toouse dostępny adres IP?
* Czy planujesz toouse urządzenia sieci VPN? Jeśli tak, to czy jest ono zgodne?
* Czy zamierzasz połączyć tylko kilka komputerów, czy też chcesz utworzyć trwałe połączenie dla witryny?
* Jaki typ bramy sieci VPN jest wymagany dla rozwiązania hello ma toocreate?
* Które jednostka SKU bramy należy używać?

### <a name="planningtable"></a>Tabela planowania

Witaj w poniższej tabeli ułatwią podjęcie decyzji hello najlepszej opcji łączności dla rozwiązania.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Przepływ pracy

Witaj następujące przedstawiono listę hello wspólnego przepływu pracy dla łączności chmury:

1. Projekt i plan, który łączności topologii i listy hello adres miejsca do wszystkich sieci mają tooconnect.
2. Tworzenie sieci wirtualnej platformy Azure. 
3. Tworzenie bramy sieci VPN dla hello sieci wirtualnej.
4. Tworzenie i konfigurowanie połączenia lokalnego tooon sieci lub innych sieci wirtualnych (w razie potrzeby).
5. Utwórz i skonfiguruj połączenie punkt-lokacja dla bramy sieci VPN platformy Azure (w razie potrzeby).

## <a name="design"></a>Projekt
### <a name="topologies"></a>Topologie połączenia

Przyjrzeć hello diagramów w hello [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykułu. Artykuł Hello zawiera podstawowe diagramy, hello modele wdrażania dla każdej topologii i narzędzia wdrażania dostępne hello toodeploy można użyć w konfiguracji.

### <a name="designbasics"></a>Podstawowe informacje o projekcie

Hello w następujących sekcjach omówiono w nim podstawowe bramy sieci VPN hello. 

#### <a name="servicelimits"></a>Limity usług sieci

Przewijanie hello tabel tooview [sieci usług limity](../azure-subscription-service-limits.md#networking-limits). limity Hello na liście mogą mieć wpływ na projekt.

#### <a name="subnets"></a>Temat podsieci

Podczas tworzenia połączenia, należy wziąć pod uwagę zakresy podsieci. Nie można umieścić nakładające się zakresy adresów w podsieci. Nakładające się podsieci jest po jednej wirtualnej sieci lub lokalnymi lokalizacji zawiera hello, który zawiera tą samą przestrzenią adresów, która hello z innej lokalizacji. Oznacza to, należy inżynierów Twojej sieci dla Twojego toocarve sieci lokalnej lokalnymi zakresu dla toouse możesz dla Azure IP adresowania miejsca/podsieci. Należy przestrzeń adresów, która nie jest używany w sieci lokalnej lokalne powitania.

Unikanie nakładające się podsieci ważne jest również podczas pracy z połączeniami sieci wirtualnej do sieci wirtualnej. Jeśli nakłada się na podsieci i adres IP istnieje zarówno wysyłania hello, jak i docelowy sieci wirtualnych, połączeń do wirtualnymi zakończyć się niepowodzeniem. Azure nie może przekierować z toohello danych hello innych sieci wirtualnej ponieważ hello adres docelowy jest częścią hello wysyłania sieci wirtualnej.

Bramy sieci VPN wymaga określonej podsieci o nazwie podsieci bramy. Wszystkie podsieci bramy muszą nosić nazwy GatewaySubnet toowork poprawnie. Upewnij się, nie tooname podsieć bramy innej nazwy i nie wdrażać maszyny wirtualne lub podsieci bramy toohello cokolwiek innego. Zobacz [podsieci bramy](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Temat bram sieci lokalnej

Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej. W hello klasycznego modelu wdrażania hello bramy sieci lokalnej jest określony tooas lokalnej lokacji sieciowej. Podczas konfigurowania bramy sieci lokalnej, nadaj mu nazwę, określ hello publiczny adres IP urządzenia sieci VPN lokalne powitania i określ hello prefiksy adresów, które znajdują się w lokalizacji lokalnej hello. Azure analizuje hello prefiksy adresów docelowy dla ruchu sieciowego, sprawdza hello konfiguracji, które zostały określone dla bramy sieci lokalnej hello i odpowiednio kieruje pakiety. W razie potrzeby można zmodyfikować hello prefiksy adresów. Aby uzyskać więcej informacji, zobacz [bramy sieci lokalnej](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Typy bramy — informacje

Bardzo ważne jest wybranie hello typu bramy poprawne dla danej topologii. W przypadku wybrania niewłaściwego typu hello brama nie będzie działać prawidłowo. Typ bramy Hello Określa jak brama hello łączy i jest wymaganego ustawienia konfiguracji dla modelu wdrażania usługi Resource Manager hello.

dostępne są następujące typy bramy Hello:

* Vpn
* ExpressRoute

#### <a name="connectiontype"></a>Typy połączenia — informacje

Każda konfiguracja wymaga określonego typu połączenia. typy połączeń Hello są:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>Typy sieci VPN — informacje

Każdej konfiguracji wymaga określonego typu sieci VPN. Jeśli są łączenie dwóch konfiguracji, takich jak tworzenie połączenia lokacja-lokacja i toohello połączenie punkt-lokacja tej samej sieci wirtualnej, należy użyć typu sieci VPN, który spełnia wymagania zarówno połączenia.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Witaj w poniższych tabelach hello sieci VPN typu ponieważ mapuje on tooeach Konfiguracja połączenia. Upewnij się, że hello typ sieci VPN dla bramy konfiguracji hello dopasowań, które mają toocreate. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Urządzenia sieci VPN w przypadku połączeń lokacja-lokacja

połączenie tooconfigure Site-to-Site, niezależnie od tego modelu wdrażania należy hello następujące elementy:

* Urządzenia sieci VPN, który jest zgodny z bram sieci VPN platformy Azure
* Adres IPv4 publicznych, który nie znajduje się za translatorem adresów Sieciowych

Należy środowisko toohave skonfigurowanie urządzenia sieci VPN lub ktoś, który może skonfigurować hello urządzenia dla Ciebie.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Należy wziąć pod uwagę routingu tunelowania wymuszonego

W przypadku większości konfiguracji można skonfigurować wymuszanie tunelowania. Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji. Jest to wymagane krytycznych dla większości organizacji IT zasad. 

Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure będzie zawsze przechodzenie od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji. Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.

W obu modeli wdrażania i za pomocą różnych narzędzi można skonfigurować połączenie tunelowania wymuszonego. Aby uzyskać więcej informacji, zobacz [Konfiguracja wymuszonego tunelowania](vpn-gateway-forced-tunneling-rm.md).

**Diagram tunelowania wymuszonego**

![Diagram tunelowania wymuszonego Brama sieci VPN](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Następne kroki

Zobacz hello [bramy sieci VPN — często zadawane pytania](vpn-gateway-vpn-faq.md) i [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykuły Aby uzyskać więcej informacji o toohelp możesz z projektu.

Aby uzyskać więcej informacji o ustawieniach bramy, zobacz [o ustawienia bramy sieci VPN](vpn-gateway-about-vpn-gateway-settings.md).