---
title: "Typy punktów końcowych Menedżera aaaTraffic | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano różne typy punktów końcowych, które mogą być używane z usługą Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Punkty końcowe usługi Traffic Manager
Microsoft Azure Traffic Manager umożliwia toocontrol, w jaki sposób ruch sieciowy jest dystrybuowane tooapplication wdrożeń uruchomionych w różnych centrach danych. Skonfiguruj każdego wdrożenia aplikacji jako punktu końcowego w usłudze Traffic Manager. Menedżer ruchu odebrania żądania DNS wybiera tooreturn dostępnego punktu końcowego w hello odpowiedzi DNS. Menedżer ruchu Określa wybór hello na hello bieżący stan punktu końcowego i hello metody routingu ruchu. Aby uzyskać więcej informacji, zobacz [sposób działania usługi Traffic Manager](traffic-manager-how-traffic-manager-works.md).

Istnieją trzy typy punktu końcowego obsługiwane przez usługę Traffic Manager:
* **Punkty końcowe systemu Azure** są używane dla usługi hostowanej na platformie Azure.
* **Zewnętrzne punkty końcowe** są używane poza Azure, lokalnie hostowanych usług lub z innym dostawcą hostingu.
* **Zagnieżdżone punkty końcowe** są bardziej elastyczne routingu ruchu schematy toosupport hello potrzeb wdrożenia większych i bardziej skomplikowanych toocreate profilów usługi Traffic Manager toocombine używane.

Żadne ograniczenia nie są w sposób punkty końcowe o różnych typach są połączone w jeden profil Menedżera ruchu. Każdy profil może zawierać żadnych mieszane typy punktu końcowego.

Witaj następujące sekcje opisują każdego typu punktu końcowego szczegółowo.

## <a name="azure-endpoints"></a>Punkty końcowe systemu Azure

Punkty końcowe systemu Azure są używane dla usług opartych na platformie Azure w usłudze Traffic Manager. obsługiwane są następujące typy zasobów platformy Azure Hello:

* Usługi w chmurze "Klasycznym" maszynom wirtualnym IaaS i PaaS.
* Web Apps
* Zasoby publicznego adresu IP (które może być tooVMs podłączonego bezpośrednio lub za pośrednictwem usługi równoważenia obciążenia Azure). Witaj publicznego adresu IP musi mieć nazwę DNS przypisane toobe używane w profilu usługi Traffic Manager.

Zasoby publicznego adresu IP są zasoby usługi Azure Resource Manager. Nie istnieją w hello klasycznego modelu wdrażania. W związku z tym są tylko obsługiwane w ruchu Menedżera środowiska usługi Azure Resource Manager. Witaj inne typy punktów końcowych są obsługiwane za pośrednictwem zarówno Resource Manager i hello klasycznego modelu wdrażania.

Używając punkty końcowe systemu Azure Traffic Manager wykrywa maszyn wirtualnych IaaS 'Klasycznym', usługa w chmurze lub aplikacji sieci Web jest zatrzymana i uruchomiona. Ten stan jest widoczny w hello stan punktu końcowego. Zobacz [monitorowania punktów końcowych usługi Traffic Manager](traffic-manager-monitoring.md#endpoint-and-profile-status) szczegółowe informacje. Po zatrzymaniu hello źródłowa usługa Menedżera ruchu nie wykonuje kontroli kondycji punktu końcowego lub punkt końcowy toohello bezpośredniego ruchu. Usługi Traffic Manager rozliczeń zdarzenia występują dla hello zatrzymał wystąpienie. Po uruchomieniu usługi hello rozliczeń wznawia i hello punkt końcowy jest uprawniona tooreceive ruchu. Wykrywanie punktów końcowych tooPublicIpAddress nie ma zastosowania.

## <a name="external-endpoints"></a>Zewnętrzne punkty końcowe

Zewnętrzne punkty końcowe są używane w przypadku usług poza platformą Azure. Na przykład usługi hostowane lokalnie lub za pomocą innego dostawcy. Zewnętrzne punkty końcowe można użyć pojedynczo lub połączyć się z punktami końcowymi Azure w hello tego samego profilu Menedżera ruchu. Łączenie punkty końcowe systemu Azure z zewnętrzne punkty końcowe umożliwia różne scenariusze:

* W jednym modelu aktywny aktywny lub aktywny / pasywny trybu failover, użyj nadmiarowość Azure tooprovide zwiększyć dla istniejącej lokalnej aplikacji.
* tooreduce opóźnienia aplikacji dla użytkowników wokół Witaj świecie rozszerzyć istniejącej lokalnej aplikacji tooadditional lokalizacje geograficzne na platformie Azure. Aby uzyskać więcej informacji, zobacz [Menedżera ruchu "Performance" routingu ruchu](traffic-manager-routing-methods.md#performance).
* Użyj Azure tooprovide zwiększyć pojemność dla istniejącej aplikacji lokalnych, stale lub jako rozwiązanie "serii chmurą" toomeet kolekcji w żądanie.

W niektórych przypadkach jest przydatne toouse zewnętrzne punkty końcowe tooreference Azure usługi (przykłady można znaleźć hello [— często zadawane pytania](traffic-manager-faqs.md#traffic-manager-endpoints)). W takim przypadku kontroli kondycji są rozliczane według hello szybkość punkty końcowe systemu Azure, nie hello zewnętrzne punkty końcowe szybkości. Jednak w przeciwieństwie do punkty końcowe systemu Azure, jeśli zatrzymać lub usunąć hello źródłowa usługa, kondycji Sprawdź rozliczeń kontynuowany do momentu wyłączenia lub usunąć hello punktu końcowego w usłudze Traffic Manager.

## <a name="nested-endpoints"></a>Zagnieżdżone punkty końcowe

Zagnieżdżone punkty końcowe łączyć wielu Traffic Manager profile toocreate elastyczne routingu ruchu schematów i obsługiwać hello potrzeby większych i złożone wdrożenia. Z punktami końcowymi zagnieżdżone profilu 'child' zostanie dodany jako punkt końcowy tooa 'parent' profilu. Oba profile nadrzędnym a podrzędnym hello może zawierać innych punktów końcowych dowolnego typu, łącznie z innych zagnieżdżonych profilów. Aby uzyskać więcej informacji, zobacz [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Web Apps jako punkty końcowe

Dodatkowe zagadnienia do rozważenia podczas konfigurowania aplikacji sieci Web jako punkty końcowe w usłudze Traffic Manager:

1. Tylko aplikacje sieci Web hello SKU "Standardowy" lub wyższym kwalifikują się do użycia z usługą Traffic Manager. Próbuje tooadd aplikacji sieci Web z niższym niepowodzenie jednostki SKU. Zmiana wersji na starszą hello SKU istniejącej aplikacji sieci Web powoduje w Menedżerze ruchu już wysyłania ruchu toothat aplikacji sieci Web.
2. Gdy punkt końcowy otrzymuje żądania HTTP, używa nagłówka "host" hello w toodetermine żądania hello aplikacji sieci Web powinien zażądać hello usługi. Witaj nagłówek hosta zawiera Żądanie hello nazwę używaną tooinitiate hello DNS, na przykład "contosoapp.azurewebsites.net". toouse innej nazwy DNS z aplikacji sieci Web, a nazwa DNS hello musi być zarejestrowana jako nazwa domeny niestandardowej dla hello aplikacji. Dodając punkt końcowy aplikacji sieci Web jako punktu końcowego platformy Azure, nazwa DNS profilu usługi Traffic Manager hello jest automatycznie rejestrowana hello aplikacji. Rejestracja zostanie automatycznie usunięta po usunięciu hello punktu końcowego.
3. Każdy profil Menedżera ruchu może mieć co najwyżej jeden końcowy aplikacji sieci Web w każdym regionie Azure. toowork wokół dla tego ograniczenia można skonfigurować aplikacji sieci Web jako zewnętrznego punktu końcowego. Aby uzyskać więcej informacji, zobacz hello [— często zadawane pytania](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Włączanie i wyłączanie punktów końcowych

Wyłączenie punktu końcowego w usłudze Traffic Manager mogą być przydatne tootemporarily Usuń ruch z punktu końcowego, który jest w trybie konserwacji lub ponownie wdrażany. Gdy punkt końcowy hello jest uruchomiona ponownie, można ją ponownie włączyć.

Punkty końcowe można włączyć i wyłączone za pomocą portalu usługi Traffic Manager hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST, które są obsługiwane zarówno Resource Manager i hello klasycznego modelu wdrażania.

> [!NOTE]
> Wyłączenie punktu końcowego platformy Azure nie ma nic toodo z jego stanem wdrożenia na platformie Azure. Azure usługi (takie jak maszyny Wirtualnej lub aplikacji sieci Web pozostaje uruchomiona i czy może tooreceive ruch nawet po wyłączeniu w usłudze Traffic Manager. Ruch może zostać zlikwidowane bezpośrednio toohello wystąpienie usługi, a nie za pomocą Menedżera ruchu hello profilu nazwy DNS. Aby uzyskać więcej informacji, zobacz [działania Menedżera ruchu](traffic-manager-how-traffic-manager-works.md).

uprawnienia bieżącego Hello ruchu tooreceive każdego punktu końcowego jest zależna od hello następujące czynniki:

* Stan profilu Hello (włączone/wyłączone)
* Stan punktu końcowego Hello (włączone/wyłączone)
* wyniki Hello hello kontroli kondycji dla tego punktu końcowego

Aby uzyskać więcej informacji, zobacz [monitorowania punktów końcowych usługi Traffic Manager](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Ponieważ działanie Menedżera ruchu polega na powitania poziom DNS, jest punkt końcowy tooinfluence istniejących połączeń tooany. Gdy punkt końcowy jest niedostępny, usługi Traffic Manager kieruje nowych połączeń tooanother dostępnego punktu końcowego. Jednak hosta hello hello wyłączone lub złej kondycji punktu końcowego może kontynuacja tooreceive ruchu za pomocą istniejących połączeń kończą się tymi sesjami. Aplikacje należy ograniczyć hello toodrain ruchu tooallow czas trwania sesji z istniejących połączeń.

Jeśli wszystkie punkty końcowe w profilu są wyłączone lub profil hello jest wyłączona, Menedżera ruchu wysyła nowe zapytanie DNS "NXDOMAIN" odpowiedzi tooa.


## <a name="next-steps"></a>Następne kroki

* Dowiedz się [działania Menedżera ruchu](traffic-manager-how-traffic-manager-works.md).
* Dowiedz się więcej o Menedżerze ruchu [punkt końcowy monitorowania i automatycznej pracy awaryjnej](traffic-manager-monitoring.md).
* Dowiedz się więcej o Menedżerze ruchu [metody routingu ruchu](traffic-manager-routing-methods.md).
