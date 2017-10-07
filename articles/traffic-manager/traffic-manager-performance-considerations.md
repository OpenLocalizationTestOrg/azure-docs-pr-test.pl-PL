---
title: "zagadnienia dotyczące aaaPerformance dla usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "Zrozumienie wydajności w usłudze Traffic Manager i w jaki sposób tootest wydajność witryny sieci Web, korzystając z Menedżera ruchu"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Zagadnienia dotyczące wydajności dla usługi Traffic Manager

Ta strona opisano zagadnienia dotyczące wydajności przy użyciu usługi Traffic Manager. Należy wziąć pod uwagę hello następujących scenariuszy:

Masz wystąpień witryny sieci Web w hello WestUS i EastAsia regionów. Jeden z wystąpień hello kończy się niepowodzeniem hello sprawdzenie kondycji do badania Menedżera ruchu hello. Ruch aplikacji jest bezpośrednie toohello region dobrej kondycji. Oczekiwano tej pracy awaryjnej, ale wydajność może być problem związany z opóźnienia hello ruchu hello teraz podróży tooa oddalonych regionu.

## <a name="performance-considerations-for-traffic-manager"></a>Zagadnienia dotyczące wydajności dla usługi Traffic Manager

Witaj tylko wpływ na wydajność mające przez Menedżera ruchu w witrynie sieci Web jest hello początkowej wyszukiwania DNS. Żądanie DNS dla nazwy hello profilu Menedżera ruchu jest obsługiwany przez hello DNS firmy Microsoft głównego serwera tej strefy trafficmanager.net hello hostów. Menedżer ruchu wypełnia i regularnie aktualizuje, serwerów głównych DNS firmy Microsoft hello na podstawie zasad Menedżera ruchu hello i hello sondowania wyników. Dzięki temu nawet podczas hello początkowej wyszukiwania DNS nie ma zapytań DNS są wysyłane tooTraffic Manager.

Menedżer ruchu składa się z kilku składników: nazwa DNS, serwery, usługi interfejsu API warstwy magazynu hello i punkt końcowy usługi monitorowania. W przypadku niepowodzenia składnika usługi Traffic Manager brak nie wpływa na powitania nazwy DNS skojarzone z profilem Menedżera ruchu. rejestruje Hello na serwerach DNS firmy Microsoft hello pozostają niezmienione. Jednak nie nawiązały monitorowania punktów końcowych i aktualizacji DNS. W związku z tym usługi Traffic Manager nie jest możliwe tooupdate DNS toopoint tooyour trybu failover lokacją systemowi lokacji głównej.

Rozpoznawanie nazwy DNS jest szybkie i wyniki są buforowane. szybkość Hello hello początkowej wyszukiwania DNS, zależy od hello używanych przez klienta hello serwery DNS do rozpoznawania nazw. Zazwyczaj klienta można ukończyć wyszukiwania DNS w ms ~ 50. wyniki wyszukiwania hello Hello są buforowane na czas trwania hello hello DNS Time-to-live (TTL). Witaj, domyślny czas wygaśnięcia Traffic Manager to 300 sekund.

Ruch nie przepływać przez Menedżera ruchu. Po zakończeniu wyszukiwania DNS hello powitania klienta ma adres IP wystąpienia witryny sieci web. powitania klienta połączenie bezpośrednio adres toothat i nie zostały spełnione przez Menedżera ruchu. nie ma wpływu na wydajność systemu DNS hello Hello zasad Menedżera ruchu, który można wybrać. Jednak wydajności routingu metody może niekorzystnie wpłynąć na środowisko aplikacji hello. Na przykład jeśli zasady przekierowuje ruch z wystąpienia tooan Ameryki Północnej hostowanej w Azji, hello opóźnienia sieci dla tych sesji może być problem z wydajnością.

## <a name="measuring-traffic-manager-performance"></a>Pomiaru wydajności usługi Traffic Manager

Istnieje kilka witryn sieci Web można używać toounderstand hello wydajności i zachowanie profilu usługi Traffic Manager. Wiele z tych witryn jest bezpłatne, ale mogą mieć ograniczenia. Niektóre witryny oferują rozszerzonego monitorowania i raportowania za opłatą.

narzędzia Hello w tych witrynach zmierzyć opóźnienia DNS i wyświetlania hello rozpoznać adresów IP dla lokalizacji klienta wokół hello world. Większość tych narzędzi nie buforują hello wyniki DNS. W związku z tym narzędzia hello pokazują hello pełne wyszukiwanie DNS zawsze, gdy test jest uruchamiany. Podczas testowania z własnego klienta tylko działanie hello pełne DNS wyszukiwania raz w okresie TTL hello.

## <a name="sample-tools-toomeasure-dns-performance"></a>Przykładowe narzędzia toomeasure DNS wydajności

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS oferuje wiele narzędzi wydajności. Narzędzie do porównywania DNS Hello można sprawdzić, jak długo trwa tooresolve nazwę DNS i jak który porównuje dostawcy usługi DNS tooother.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Jest jednym z narzędzi najprostszym hello WebSitePulse. Wprowadź czas rozpoznawania nazw DNS dla adresu URL toosee, hello, pierwszy bajt ostatniego bajtu i innych danych statystycznych wydajności. Można wybrać trzy testu różnych lokalizacjach. W tym przykładzie widać, że wykonanie pierwszej hello wskazuje, że wyszukiwania DNS ma 0.204 s.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Ponieważ powitalne wyniki są buforowane, drugi test powitania dla hello tego samego wyszukiwania DNS hello punktu końcowego Menedżera ruchu przyjmuje 0,002 s.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [Monitor aplikacji syntetycznych urzędu certyfikacji](https://asm.ca.com/en/checkit.php)

    Wcześniej znana jako narzędzie Watchmouse wyboru witryny sieci Web hello, ta lokacja pokazują czas równocześnie w wielu regionach geograficznych hello rozpoznawania nazw DNS. Wprowadź czas rozpoznawania nazw DNS dla adresu URL toosee, hello, czas połączenia i szybkość z wielu lokalizacji geograficznych. Użyj tego toosee testu usługi hostowanej, która jest zwracana dla różnych lokalizacji wokół hello world.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    To narzędzie umożliwia statystyki dla każdego elementu strony sieci web. Witaj kartę analiza strony zawiera hello procent czasu poświęconego na wyszukiwania DNS.

* [Co to jest Mój DNS?](http://www.whatsmydns.net/)

    Ta lokacja nie wyszukiwania DNS z 20 różnych lokalizacji i wyświetla wyniki hello na mapie.

* [Szczegółowej interfejs sieci Web](http://www.digwebinterface.com)

    Ta lokacja zawiera bardziej szczegółowe informacje dotyczące systemu DNS, w tym rekordów CNAME i. Upewnij się, sprawdź w obszarze Opcje hello "koloruj dane wyjściowe" i "Statystykę" i wybierz "All" w obszarze Nameservers.

## <a name="next-steps"></a>Następne kroki

[O metodach routingu ruchu Menedżera ruchu](traffic-manager-routing-methods.md)

[Testowanie ustawień Menedżera ruchu](traffic-manager-testing-settings.md)

[Operacje w usłudze Traffic Manager (dokumentacja interfejsu API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Polecenia cmdlet systemu Azure Traffic Manager](http://go.microsoft.com/fwlink/p/?LinkId=400769)

