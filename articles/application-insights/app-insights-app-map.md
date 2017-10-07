---
title: "Mapa w usłudze Azure Application Insights aaaApplication | Dokumentacja firmy Microsoft"
description: "Wizualną prezentację hello zależności między składnikami aplikacji etykietą kluczowych wskaźników wydajności i alerty."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mapowanie aplikacji w usłudze Application Insights
W [Azure Application Insights](app-insights-overview.md), mapa aplikacji jest układu wizualnego relacji zależności hello składników aplikacji. Każdy składnik pokazuje wskaźników KPI takich jak toohelp obciążenia, błędów, wydajności i alerty, odnajdywanie dowolny składnik przyczyną problemu z wydajnością lub błędu. Kliknij go, z dowolnym toomore składnika szczegółowe diagnostycznych, takich jak zdarzenia usługi Application Insights. Jeśli aplikacja korzysta z usług Azure, możesz również kliknąć za pośrednictwem diagnostics tooAzure, takie jak zalecenia doradcy bazy danych SQL.

Podobnie jak inne wykresy można przypiąć toohello mapy aplikacji pulpitu nawigacyjnego platformy Azure, gdzie jest pełną funkcjonalność. 

## <a name="open-hello-application-map"></a>Mapowanie aplikacji hello otwarte
Mapa hello Otwórz za pomocą bloku omówienie hello aplikacji:

![Otwórz aplikację mapy](./media/app-insights-app-map/01.png)

![Mapa aplikacji](./media/app-insights-app-map/02.png)

Mapa Hello pokazuje:

* Testy dostępności
* Składnik po stronie klienta (monitorowane w ramach hello JavaScript SDK)
* Składnik po stronie serwera
* Zależności hello składniki klienta i serwera

Można zwijać i rozwijać grupy łącze zależności:

![Zwiń](./media/app-insights-app-map/03.png)

Jeśli masz wiele zależności jednego typu (SQL, HTTP itp.) są zgrupowane. 

![zależności grupowanych](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Dodatkowych problemów
Każdy węzeł ma odpowiednie wskaźniki, jak hello ładowania, wydajności i niepowodzenie szybkości dla tego składnika. 

Ikonami ostrzeżenia zaznacz możliwych problemów. Pomarańczowe ostrzeżenie oznacza, że błędy występują w żądaniach, wyświetleń strony lub wywołania zależności. Czerwony oznacza współczynnik awaryjności powyżej 5%. Jeśli chcesz tooadjust tych progów, Otwórz opcje.

![ikony błędu](./media/app-insights-app-map/04.png)

Aktywne alerty również Pokaż zapasową: 

![aktywne alerty](./media/app-insights-app-map/05.png)

Jeśli używasz usług SQL Azure jest ikonę, która pokazuje, kiedy są zalecenia, w jaki sposób można poprawić wydajność. 

![zalecenie Azure](./media/app-insights-app-map/06.png)

Kliknij żadnych tooget ikona więcej szczegółów:

![zalecenie Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Kliknij diagnostyczne za pośrednictwem
Każdego z węzłów hello na mapie hello oferuje docelowe kliknij za pomocą diagnostyki. Opcje Hello będą się różnić w zależności od typu hello hello węzła.

![Opcje serwera](./media/app-insights-app-map/09.png)

Dla składników, które są hostowane na platformie Azure opcje hello obejmują toothem łączy bezpośrednich.

## <a name="filters-and-time-range"></a>Filtry i zakres czasu
Domyślnie mapy hello znajduje się podsumowanie wszystkich danych hello dostępna dla wybranego zakresu czasu hello. Ale filtru nazwy tylko w określonych operacji tooinclude lub zależności.

* Nazwa operacji: dotyczy zarówno wyświetleń strony i typy żądania po stronie serwera. Po wybraniu tej opcji hello Mapa pokazuje hello wskaźnika KPI w węźle serwera/klienta hello tylko w operacjach hello wybrane. Pokazuje zależności hello wywoływana w kontekście hello tych określonych działań.
* Nazwa podstawowa zależności: dotyczy to również hello AJAX przeglądarki zależności i zależności po stronie serwera. Jeśli raport dane telemetryczne zależności niestandardowych z hello TrackDependency API pojawią się również w tym miejscu. Możesz wybrać tooshow zależności hello na mapie hello. Obecnie to pole wyboru nie filtruje hello żądania po stronie serwera lub hello wyświetleń strony po stronie klienta.

![Ustaw filtry](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Zapisz filtry
w przypadku zastosowania filtrów hello toosave, hello numeru pin filtrowane widoku na [pulpitu nawigacyjnego](app-insights-dashboards.md).

![Toodashboard numeru PIN](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Okienko błędu
Po kliknięciu węzła w mapie hello okienko błędu jest wyświetlany na prawej stronie powitania podsumowania błędów dla tego węzła. Awarie są najpierw pogrupowane według Identyfikatora operacji i pogrupowane według identyfikatora problemu.

![Okienko błędu](./media/app-insights-app-map/error-pane.png)

Kliknięcie awarii przyjmuje toohello ostatniego wystąpienia tego błędu.

## <a name="resource-health"></a>Kondycja zasobów
W przypadku niektórych typów zasobów kondycja zasobu jest wyświetlany u góry okienka błąd hello hello. Na przykład kliknięcie węzła SQL spowoduje wyświetlenie hello kondycji bazy danych i alerty, które mają być uruchamiane.

![Kondycja zasobów](./media/app-insights-app-map/resource-health.png)

Możesz kliknąć hello zasobu Nazwa tooview standardowe omówienie metryki dla tego zasobu.

## <a name="end-to-end-system-app-maps"></a>System end-to-end aplikacji mapy

*Wymaga zestawu SDK w wersji 2.3 lub nowszej*

Jeśli aplikacja ma kilka części — na przykład usługi zaplecza dodatkowo możesz toohello aplikacji sieci web — mogą być prezentowane z ich wszystkich na mapie jednej zintegrowanej aplikacji.

![Ustaw filtry](./media/app-insights-app-map/multi-component-app-map.png)

Mapa aplikacji Hello znajduje węzły serwera, wykonując wszystkie wywołania zależności HTTP między serwerami z hello zainstalowany zestaw SDK usługi Application Insights. Każdy zasób usługi Application Insights zakłada, że toocontain jeden serwer.

### <a name="multi-role-app-map-preview"></a>Mapa aplikacji usługi roli (wersja zapoznawcza)

Funkcja mapy usługi roli aplikacji Hello w wersji zapoznawczej pozwala mapy aplikacji hello toouse z wieloma serwerami wysyłania danych toohello tego samego zasobu usługi Application Insights / klucz instrumentacji. Serwery w mapie hello są podzielone przez właściwość cloud_RoleName hello elementów telemetrii. Ustaw *Mapa aplikacji usługi roli* za*na* z hello tooenable bloku podglądy tej konfiguracji.

Ta metoda może być wskazane w aplikacji micro-services lub w innych sytuacjach, w którym mają być toocorrelate zdarzenia na wielu serwerach w ramach pojedynczego zasobu usługi Application Insights.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Opinia
Prześlij opinię za pośrednictwem portalu opinie hello.

![Obraz MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Następne kroki

* [Witryna Azure Portal](https://portal.azure.com)
