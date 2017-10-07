---
title: "aaaUpgrading Analiza dzienników Azure toonew dziennik wyszukiwania | Dokumentacja firmy Microsoft"
description: "nowy język kwerendy analizy dzienników Hello jest prawie tutaj i mogą uczestniczyć w publicznej wersji zapoznawczej hello.  W tym artykule opisano hello zalet nowego języka hello i w jaki sposób tooconvert obszaru roboczego."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Uaktualnij usługi Analiza dzienników Azure obszaru roboczego toonew dziennik wyszukiwania

> [!NOTE]
> Uaktualnienia toohello nowy język kwerendy analizy dzienników jest obecnie opcjonalne nadanie za czas[zdobycia na powitania nowy język](https://go.microsoft.com/fwlink/?linkid=856078).  

Hello nowy język kwerendy Log Analytics jest w tym miejscu i należy tooupgrade Twojego obszaru roboczego tootake ją wykorzystać.  W tym artykule opisano hello zalet nowego języka hello i w jaki sposób tooconvert obszaru roboczego.  Jeśli nie możesz teraz wybrać tooupgrade, obszaru roboczego będzie kontynuować toooperate podobnie jak zawsze jak, ale zostaną automatycznie przekonwertowane w późniejszym terminie.  Po tej dacie jest ustawiona, zostanie wyświetlony długiego czasu i powiadomień.

Ten artykuł zawiera szczegółowe informacje na powitania nowy język i hello procesu uaktualniania.

## <a name="why-hello-new-language"></a>Dlaczego hello nowy język?
Zdajemy w dowolnym przejścia jest słabe, czy firma Microsoft nie są po prostu zmiana hello język zapytań do zabawy hello go.  Istnieje kilka przyczyn, które ta zmiana zapewni wartość tooour analizy dzienników klientów.

- **Proste, ale.** nowy język Hello jest łatwiejsze toounderstand i podobne tooSQL z konstrukcji więcej takich jak języka naturalnego niż hello starszej wersji języka.
- **Język pełnego przesyłanie potokowe.**  nowy język Hello ma bardziej rozbudowane funkcje potokowanie niż hello starszej wersji języka.  Prawie wszystkie dane wyjściowe może być toocreate polecenia gazociągami tooanother zapytania bardziej złożone niż kiedykolwiek wcześniej.
- **Ekstrakcje pola czas wyszukiwania.**  nowy język Hello obsługuje bardziej zaawansowanych pola obliczeniowego środowiska uruchomieniowego niż hello starszej wersji języka.  Można używać złożonych obliczeń rozszerzonych polach, a następnie użyć pola obliczeniowego hello dodatkowych poleceń, w tym sprzęgania i agregacji.
- **Zaawansowane sprzężenia.**  nowy język Hello zapewnia bardziej zaawansowanych sprzężenia niż język starszych hello tym hello możliwości toojoin tabele według wielu pól, użyj sprzężeń wewnętrznych i zewnętrznych i Dołącz do rozszerzonego pola.
- **Funkcje daty/godziny.**  nowy język Hello ma bardziej zaawansowane funkcje daty/godziny niż hello starszej wersji języka.
- **Inteligentne Analytics.**  nowy język Hello udostępnia zaawansowane algorytmy tooevaluate wzorce w zestawy danych i porównanie różnych zestawów danych.
- **Zaawansowane portal analityka.**  Hello portal analityka zaawansowane oferuje funkcje analizy nie jest dostępna w portalu usługi Analiza dzienników hello tym multiline zapytania, dodatkowe wizualizacje i diagnostyki zaawansowanej edycji.
- **Zgodność z innymi aplikacjami.**  Witaj nowy język i hello zaawansowane Portal analityka są już używane w celu wykonania analizy w usłudze Application Insights.  Implementowania Log Analytics zapewnia spójność między usługami Azure.
- **Lepsza integracja z usługą Power BI.** Zapytania w nowym języku hello może być wyeksportowane tooPower BI Desktop, mogą korzystać z jego możliwości przekształcania danych sformatowanego.
- **Wiele więcej.** Zobacz toohello [język zapytań Analiza dzienników Azure](https://docs.loganalytics.io) szczegółowe informacje i samouczki dotyczące nowego języka hello lokacji.


## <a name="when-can-i-upgrade"></a>Jeśli można uaktualnić?
uaktualnienie Hello zostanie wycofana we wszystkich regionach platformy Azure, może on być dostępny w pewnych regionach przed pozostałymi.  Użytkownik wie, gdy obszar roboczy jest dostępna toobe uaktualnić, gdy zostanie wyświetlony Baner hello purpurowa hello górze obszaru roboczego zaprasza Cię tooupgrade.

![Uaktualnienie w 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>Co się stanie po uaktualnieniu?
Podczas konwertowania obszaru roboczego żadnych zapisanych wyszukiwań, reguły alertów i widoków, które zostały utworzone za pomocą projektanta widoków hello są automatycznie przekonwertowane toohello nowego języka.  Uwzględnione w rozwiązaniach wyszukiwania nie są konwertowane automatycznie, ale one jest zamiast tego przekonwertowane na bieżąco powitania po ponownym otwarciu.  To jest całkowicie niewidoczne tooyou.

## <a name="can-i-go-back-after-i-upgrade"></a>Po uaktualnieniu można przejść?
Podczas uaktualniania, wykonywana jest kopia zapasowa pełną obszaru roboczego, zawierającego migawkę wszystkich zapisanych wyszukiwań, reguły alertów i widoków.  Dzięki temu można toorestore Twojego stary obszar roboczy, jeśli należy później konieczna.

toorestore obszaru roboczego starszej wersji, przejdź zbyt**ustawienia** w obszarze roboczym, a następnie **podsumowanie uaktualnienia**.  Następnie można wybrać opcję hello zbyt**przywracania starszej wersji obszaru roboczego**.  

![Przywróć starsza wersja](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Jak wykonać uaktualnienie hello?
Obszaru roboczego można uaktualnić, gdy zostanie wyświetlony Baner hello purpurowa u góry hello hello portalu.  

1.  Uruchomić proces uaktualniania hello, klikając na transparencie hello purpurowa, informujący o **Dowiedz się więcej i uaktualnić**.<br>![Uaktualnij 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Zapoznaj się z artykułem hello uzyskać dodatkowe informacje dotyczące uaktualniania hello na stronie informacje o uaktualnianiu hello.<br>![Uaktualnij 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Kliknij przycisk **Uaktualnij teraz** toostart hello uaktualnienia.<br>![Uaktualnij 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Pole o powiadomienia w prawym górnym rogu hello Wyświetla stan hello.<br>![Uaktualnij 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  Gotowe.  Przejdź przez toohave strony wyszukiwania dziennika toohello spojrzeć na uaktualnionym obszaru roboczego.<br>![Uaktualnij 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Jeśli wystąpi problem powodujący hello toofail uaktualnienia, możesz przejść toohello [forum dyskusyjne](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) i zgłoś zapytanie lub [Utwórz żądanie obsługi](../azure-supportability/how-to-create-azure-support-request.md) z hello portalu Azure.

## <a name="how-do-i-learn-hello-new-language"></a>Jak dowiedzieć się nowy język hello?
Ponieważ jest on używany przez wiele usług utworzyliśmy [zewnętrznej witryny toohost hello dokumentacji](https://docs.loganalytics.io/) hello nowego języka.  W tym samouczki, przykłady i toohelp pełne odwołanie, które wchodzenie toospeed. Możesz zapoznać się z samouczkiem hello nowy język w [wprowadzenie do zapytań](https://go.microsoft.com/fwlink/?linkid=856078) i uzyskiwać dostęp do hello dokumentację języka u [analizy dzienników zapytania langauge](https://go.microsoft.com/fwlink/?linkid=856079).  

Jeśli umiesz już z hello starszej wersji analizy dzienników języka zapytań jednak, a następnie można użyć konwertera języka hello, dodanego tooyour obszar roboczy w ramach uaktualnienia hello.

Po prostu wpisz kwerendę starszej wersji, a następnie kliknij przycisk **przekonwertować** toosee hello translacji wersji.  Mogą być następnie albo kliknij przycisk hello hello wyszukiwania przycisk toorun lub Kopiuj i Wklej toouse zapytania hello przekonwertować gdzieś, takie jak reguły alertu.

![Konwerter języka](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Następne kroki
- Zapoznaj się z [samouczka na powitania nowy język](https://go.microsoft.com/fwlink/?linkid=856078).
- Zapoznaj się z artykułem [samouczek przy użyciu portalu wyszukiwania dziennika hello](log-analytics-log-search-log-search-portal.md) z hello nowy język kwerendy.
- Pobierz toohello wprowadzenie nowego [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587).
