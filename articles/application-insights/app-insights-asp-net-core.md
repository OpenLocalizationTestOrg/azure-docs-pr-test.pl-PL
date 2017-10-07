---
title: Application Insights dla platformy ASP.NET Core aaaAzure | Dokumentacja firmy Microsoft
description: "Monitorowanie aplikacji sieci web dla dostępności, wydajności i użycia."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Usługa Application Insights dla aplikacji ASP.NET Core
[Usługa Application Insights](app-insights-overview.md) umożliwia monitorowanie aplikacji sieci web, dostępności, wydajności i użycia. Opinii hello Ci o hello wydajność i skuteczność aplikacji w hello wild można wybrać opcje informowane o kierunku hello hello projektu w każdym cyklu programistycznym.

![Przykład](./media/app-insights-asp-net-core/sample.png)

Będziesz potrzebować subskrypcji z [Microsoft Azure](http://azure.com). Zaloguj się przy użyciu konta Microsoft, które możesz mieć dla systemu Windows, usługi XBox Live lub innych usług w chmurze firmy Microsoft. Zespół może mieć tooAzure organizacyjnej subskrypcji: hello właściciela tooadd poprosić tooit przy użyciu konta Microsoft.

## <a name="getting-started"></a>Wprowadzenie

* W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Konfiguruj usługę Application Insights**, lub **Dodaj > usługi Application Insights**. [Dowiedz się więcej](app-insights-asp-net.md).
* Jeśli nie widzisz tych poleceń menu, wykonaj hello [ręcznego pobierania Przewodnik wprowadzający](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Może być konieczne toodo to jeżeli projekt został utworzony przy użyciu wersji programu Visual Studio przed 2017 r.

## <a name="using-application-insights"></a>Korzystanie z usługi Application Insights
Zaloguj się na powitania [portalu Microsoft Azure](https://portal.azure.com), wybierz pozycję **wszystkie zasoby** lub **usługi Application Insights**, a następnie wybierz zasób hello utworzenia toomonitor aplikacji.

W osobnym oknie przeglądarki należy użyć aplikacji przez pewien czas. Zostanie wyświetlone dane znajdujące się na wykresach usługi Application Insights hello. (Może być tooclick odświeżania). Będzie niewielką ilość danych podczas projektujesz, ale te wykresy naprawdę pochodzić aktywności podczas publikowania aplikacji i wielu użytkowników. 

Strona omówienia Hello zawiera wykresy wydajności: czas odpowiedzi serwera, czas ładowania strony i liczby żądań zakończonych niepowodzeniem. Kliknij przycisk toosee dowolnego wykresu, więcej wykresów i danych.

Widoki w portalu hello dzielą się na trzy główne kategorie:

* [Eksploratora metryk](app-insights-metrics-explorer.md) przedstawia wykres i tabelę metryki i liczby, takie jak czas reakcji, awariami lub metryki samodzielnie utworzony z hello [interfejsu API](app-insights-api-custom-events-metrics.md). Filtr segmentu hello dane i przez tooget wartości właściwości lepiej zrozumieć aplikacji i jej użytkowników.
* [Eksplorator wyszukiwania](app-insights-diagnostic-search.md) zawiera listę poszczególnych zdarzeń, takich jak określone żądania, wyjątki, ślady dziennika lub zdarzenia utworzone samodzielnie z hello [interfejsu API](app-insights-api-custom-events-metrics.md). Filtrowanie wyszukiwania w zdarzeniach hello i nawigowanie między problemów tooinvestigate powiązanych zdarzeń.
* [Analiza](app-insights-analytics.md) pozwala uruchamiać zapytania SQL przypominającej za pośrednictwem telemetrii i jest zaawansowanym narzędziem analityczne i diagnostycznych.

## <a name="alerts"></a>Alerty
* Automatycznie Pobierz [aktywne alerty diagnostycznych](app-insights-proactive-diagnostics.md) który informujące o nietypowych zmian awariami i innych metryk.
* Konfigurowanie [testów dostępności](app-insights-monitor-web-app-availability.md) tootest witryny sieci Web stale z lokalizacji na całym świecie i get wiadomości e-mail, gdy tylko jedną testowania kończy się niepowodzeniem.
* Konfigurowanie [metryki alerty](app-insights-monitor-web-app-availability.md) tooknow w przypadku metryk, takich jak czas odpowiedzi lub stawki wyjątek poza akceptowalnych limitów.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Oprogramowanie typu „open source”
[Przeczytaj i współtworzenia toohello kodu](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Następne kroki
* [Dodawanie stron sieci web tooyour telemetrii](app-insights-javascript.md) toomonitor strony użycia i wydajności.
* [Monitor zależności](app-insights-asp-net-dependencies.md) toosee gdy REST, SQL lub innych zasobów zewnętrznych powoduje spowolnienie użytkownik.
* [Za pomocą interfejsu API hello](app-insights-api-custom-events-metrics.md) toosend własne zdarzenia i metryki dla bardziej szczegółowy widok wydajności i użycia aplikacji.
* [Badania dostępności](app-insights-monitor-web-app-availability.md) Sprawdź aplikację stale z wokół hello world. 

