---
title: "aaaNetwork architektura Omówienie programu środowiska usługi App Service"
description: "Omówienie architektury ofApp topologii sieci środowiska usługi."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Omówienie architektury sieciowej środowisk usługi App Service
## <a name="introduction"></a>Wprowadzenie
Środowiska usługi App Service zawsze są tworzone w obrębie podsieci [sieci wirtualnej] [ virtualnetwork] — aplikacje działające w środowisku usługi aplikacji może komunikować się z prywatnej punkty końcowe znajdujących się na powitania sam wirtualnego Topologia sieci.  Ponieważ klienci mogą zablokować części infrastruktury sieci wirtualnej, jest ważne toounderstand hello rodzaje przepływów komunikacji sieci, które występują w przypadku środowiska usługi aplikacji.

## <a name="general-network-flow"></a>Przepływ sieci ogólne
Jeśli środowisko aplikacji (ASE) używa publiczny wirtualny adres IP (VIP) dla aplikacji, cały ruch przychodzący dociera na tym publicznego adresu VIP.  W tym ruchu HTTP i HTTPS dla aplikacji, a także innych ruch FTP, zdalnego debugowania działania i operacji zarządzania platformy Azure.  Pełną listę hello określonych portów (wymagane i opcjonalne), które są dostępne w publicznych adresów VIP hello artykule hello na [kontrolowanie ruchu przychodzącego] [ controllinginboundtraffic] tooan środowiska usługi aplikacji. 

Środowiska usługi App Service obsługuje również uruchamianie aplikacji, które są powiązane tylko tooa wirtualnych sieci wewnętrzny adres, nazywana także tooas adres ILB (wewnętrzny moduł równoważenia obciążenia).  Na ILB włączone ruchu ASE, HTTP i HTTPS dla aplikacji, a także zdalnego wywoływania debugowania, przychodzą na powitania ILB adres.  W przypadku najbardziej typowych konfiguracji ILB ASE ruch FTP/FTPS pojawią się również na powitania ILB adres.  Jednak operacje zarządzania platformy Azure, nadal będą przepływać tooports 454/455 na powitania publicznego adresu VIP o ILB obsługuje ASE.

Poniższy diagram Hello przedstawiono przegląd hello poszczególnych przepływów ruchu przychodzącego i wychodzącego dla środowiska usługi aplikacji, których aplikacje hello są publiczny wirtualny adres IP powiązane tooa:

![Ogólne przepływów sieci][GeneralNetworkFlows]

Środowiska usługi aplikacji może komunikować się z różnych punktów końcowych klienta prywatnych.  Na przykład aplikacje działające w hello środowiska usługi aplikacji mogą się łączyć serwery toodatabase uruchomionych na maszynach wirtualnych IaaS w hello samej topologii sieci wirtualnej.

> [!IMPORTANT]
> Spojrzenie na diagramie sieciowym hello, hello "inne obliczeniowe zasoby" są wdrażane w innej podsieci z hello środowiska usługi aplikacji. Wdrażanie zasobów w hello tej samej podsieci z hello ASE blokuje połączenia z zasobami toothose ASE (z wyjątkiem określonych ASE wewnątrz routing). Wdrażanie tooa innej podsieci zamiast (w tej samej sieci Wirtualnej hello). Hello środowiska usługi aplikacji będą w stanie tooconnect. Dodatkowa konfiguracja nie jest konieczne.
> 
> 

Środowiska usługi aplikacji również komunikować się z bazą danych Sql i usługi Azure Storage zasoby niezbędne do zarządzania i obsługi środowiska usługi aplikacji.  Niektóre hello Sql i zasobów magazynowania które środowiska usługi aplikacji komunikuje się z znajdują się w hello tego samego regionu hello środowiska usługi aplikacji, podczas gdy inne znajdują się w zdalnym regiony platformy Azure.  W związku z tym toohello wychodzące połączenie internetowe jest zawsze wymagane dla toofunction środowiska usługi aplikacji poprawnie. 

Ponieważ środowisko usługi aplikacji jest wdrażana w podsieci, grup zabezpieczeń sieci może być używane toocontrol podsieci toohello ruchu przychodzącego.  Szczegółowe informacje dotyczące sposobu toocontrol ruchu przychodzącego ruchu tooan środowiska usługi aplikacji, zobacz następujące hello [artykułu][controllinginboundtraffic].

Aby uzyskać więcej informacji na temat tooallow wychodzące połączenie z Internetem między środowiska usługi aplikacji, zobacz hello poniższego artykułu na temat pracy z [Express Route][ExpressRoute].  Hello same podejście opisaną w artykule hello ma zastosowanie w przypadku pracy z połączenie lokacja-lokacja i użycie wymuszonego tunelowania.

## <a name="outbound-network-addresses"></a>Adresy sieciowe ruchu wychodzącego
Adres IP wywołań wychodzących środowiska usługi aplikacji zawsze jest skojarzony z hello wychodzący.  Hello określonego adresu IP jest używana, zależy od tego, czy punkt końcowy hello wywoływana znajduje się w topologii sieci wirtualnej hello, lub na zewnątrz hello topologii sieci wirtualnej.

Jeśli punkt końcowy hello wywoływany jest **poza** hello topologii sieci wirtualnej, a następnie hello wychodzący adres (alias hello wychodzącego translatora adresów Sieciowych) używany jest publiczny VIP hello z hello środowiska usługi aplikacji.  Ten adres znajduje się w interfejsie użytkownika portalu hello na powitania środowiska usługi aplikacji w bloku właściwości.

![Adres IP ruchu wychodzącego][OutboundIPAddress]

Ten adres także można określić dla ASEs mających tylko publiczne VIP tworząc aplikacji hello środowiska usługi aplikacji, a następnie wykonuje *nslookup* aplikacji hello adresu. Wynikowe adres IP Hello jest zarówno hello publicznego adresu VIP, a także adres NAT ruchu wychodzącego środowiska hello aplikacji usługi.

Jeśli punkt końcowy hello wywoływany jest **wewnątrz** hello topologii sieci wirtualnej, hello wychodzący adres wywoływania aplikacji hello będzie hello wewnętrzny adres IP zasobu obliczeniowego poszczególnych hello uruchamiania aplikacji hello.  Jednak nie ma trwałego mapowanie wewnętrzny tooapps adresów IP w sieci wirtualnej.  Aplikacje można przenosić między zasoby obliczeniowe różnych i zmieniać ukończenia operacji tooscaling hello puli zasobów obliczeniowych dostępnych w środowisku usługi aplikacji.

Jednak ponieważ środowiska usługi aplikacji zawsze znajduje się w podsieci, ma się gwarancji, że hello wewnętrzny adres IP zasobu obliczeniowego uruchomiona aplikacja będzie zawsze leży w obrębie CIDR hello hello podsieci.  W związku z tym szczegółowych list ACL lub grup zabezpieczeń sieci są używane toosecure dostęp do punktów końcowych tooother w sieci wirtualnej hello, hello zakresu podsieci zawierającego toobe potrzeb środowiska usługi aplikacji hello prawa dostępu.

Witaj Poniższy diagram przedstawia tych pojęć więcej szczegółów:

![Adresy sieciowe ruchu wychodzącego][OutboundNetworkAddresses]

W hello powyżej diagramu:

* Ponieważ hello publicznego adresu VIP o hello środowiska usługi aplikacji jest 192.23.1.2, to hello wychodzący adres IP używany w wywołaniach zbyt punkty końcowe "Internet".
* Witaj zakres CIDR hello zawierający podsieci dla środowiska usługi aplikacji hello jest 10.0.1.0/26.  Inne punkty końcowe w ramach hello tej samej infrastrukturze sieci wirtualnej zostanie wyświetlony wywołania z aplikacji jako pochodzący z gdzieś w ramach tego zakresu adresów.

## <a name="calls-between-app-service-environments"></a>Wywołania między środowiska usługi aplikacji
Bardziej złożone scenariusz może mieć miejsce, w przypadku wdrożenia wielu środowiska usługi App Service w hello tej samej sieci wirtualnej i wychodzący wywołań z jednego środowiska usługi aplikacji tooanother środowiska usługi aplikacji.  Tego rodzaju wielu wywołań również będą traktowane jako wywołania "Internet" środowiska usługi aplikacji.

powitania po diagram przedstawia przykład architektury warstwowej z aplikacjami na jeden środowiska usługi aplikacji (np. "Drzwi wejściowe" web apps) wywołanie aplikacji w drugim środowiska usługi aplikacji (np. aplikacje interfejsu API zaplecza wewnętrzne nieprzeznaczonych toobe dostępny z Internetu hello). 

![Wywołania między środowiska usługi aplikacji][CallsBetweenAppServiceEnvironments] 

W hello przykład powyżej hello środowiska usługi aplikacji "ASE jeden" ma adres IP wychodzących 192.23.1.2.  Jeśli aplikacji uruchomionej na tego środowiska usługi aplikacji sprawia, że tooan wywołań wychodzących aplikacji uruchomionych na drugi środowiska usługi aplikacji ("ASE dwóch") znajduje się w hello sam wirtualnych sieci, hello wychodzącego wywołania będą traktowane jako wywołanie "Internet".  W związku z tym ruchu sieciowego hello przychodzące do hello drugi środowiska usługi aplikacji będą wyświetlane jako pochodzący z 192.23.1.2 (tj. nie hello zakres adresów podsieci z hello pierwszy środowiska usługi aplikacji).

Mimo że wywołań między różne środowiska usługi aplikacji są traktowane jako wywołania "Internet", gdy oba środowiska usługi aplikacji znajdują się w hello tego samego regionu Azure hello ruchu w sieci pozostanie na powitania regionalną sieć platformy Azure i nie będzie fizycznie możliwy przepływ za pośrednictwem hello publicznej sieci Internet.  W związku z tym można użyć grupy zabezpieczeń sieci na powitania podsieć hello tooonly zezwala na przychodzące wywołania z drugiego środowiska usługi aplikacji hello pierwszy środowiska usługi aplikacji (których wychodzący adres IP jest 192.23.1.2), w związku z tym zapewnienia bezpiecznej komunikacji między hello Środowiska usługi aplikacji.

## <a name="additional-links-and-information"></a>Linki do dodatkowych i informacji
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Szczegóły ruchu przychodzącego porty używane przez środowiska usługi App Service i przy użyciu toocontrol grup zabezpieczeń sieci dla ruchu przychodzącego ruchu sieciowego jest dostępna [tutaj][controllinginboundtraffic].

Szczegółowe informacje o wykorzystaniu zdefiniowane przez użytkownika tras toogrant wychodzącego Internet access tooApp środowiska usługi jest dostępna w tym [artykułu][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

