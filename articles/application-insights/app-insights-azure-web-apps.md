---
title: "aaaMonitor wydajność aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności aplikacji dla aplikacji sieci Web platformy Azure. Udostępnianie wykresów czasu ładowania i odpowiedzi oraz informacji o zależnościach oraz ustawianie alertów dotyczących wydajności."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Monitorowanie wydajności aplikacji sieci Web platformy Azure
W hello [Azure Portal](https://portal.azure.com) można skonfigurować monitorowanie wydajności aplikacji dla programu [aplikacje sieci web Azure](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) instruments telemetrii toosend aplikacji o jego toohello działania usługi Application Insights, gdzie są przechowywane i przeanalizowane. Istnieje, można użyć narzędzia wyszukiwania i wykresy metryki toohelp diagnozowanie problemów, zwiększenia wydajności i użycia do oceny.

## <a name="run-time-or-build-time"></a>W czasie wykonywania lub czasie kompilacji
Można skonfigurować monitorowanie przez instrumentacji aplikacji hello na dwa sposoby:

* **Czas wykonywania** — możesz wybrać rozszerzenie monitorowania wydajności, gdy aplikacja sieci Web już działa. Go nie jest konieczne toorebuild lub zainstaluj ponownie aplikację. Uzyskujesz standardowy zestaw pakietów, które monitorują czasy odpowiedzi, współczynniki sukcesu, wyjątki, zależności itd. 
* **Czas kompilacji** — możesz zainstalować pakiet w aplikacji podczas programowania. Ta opcja jest bardziej wszechstronna. W przypadku dodawania toohello same pakiety standardowe, można napisać kod toocustomize hello telemetrii lub toosend własnych danych telemetrycznych. Możesz zalogować się konkretne działania lub zdarzenia rekordu zgodnie z semantyki toohello domeny aplikacji. 

## <a name="run-time-instrumentation-with-application-insights"></a>Instrumentacja w czasie wykonywania za pomocą usługi Application Insights
Jeśli już masz uruchomioną aplikację sieci Web na platformie Azure, otrzymujesz pewne informacje monitorowania: żądania i współczynniki błędów. Dodaj więcej, takich jak czas reakcji, monitorowania toodependencies wywołania inteligentne wykrywanie i hello zaawansowanych język zapytań usługi Analiza dzienników tooget usługi Application Insights. 

1. **Wybierz usługi Application Insights** w Panelu sterowania Azure powitania dla aplikacji sieci web.
   
    ![W obszarze Monitorowanie wybierz pozycję Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Wybierz toocreate nowy zasób, chyba że — konfiguracja zasobu usługi Application Insights dla tej aplikacji jest już w innej trasy.
2. **Zastosuj instrumentację aplikacji sieci Web** po zainstalowaniu usługi Application Insights. 
   
    ![Instrumentacja aplikacji sieci Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Włącz monitorowanie po stronie klienta** dla telemetrii widoku strony i użytkownika.

   * Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji
   * W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość: 
   
    Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Wartość:`true`
   * **Zapisz** hello ustawienia i **ponowne uruchomienie** aplikacji.
3. **Monitoruj aplikację**.  [Dane hello Expore](#explore-the-data).

Później można utworzyć aplikacji hello za pomocą usługi Application Insights, jeśli chcesz.

*Jak usunąć usługi Application Insights, lub przełączyć zasób tooanother toosending?*

* Na platformie Azure, otwórz hello bloku kontroli aplikacja sieci web, a w obszarze Narzędzia deweloperskie, otwórz **rozszerzenia**. Usuń hello rozszerzenia usługi Application Insights. Następnie w obszarze monitorowania, wybierz usługę Application Insights i Utwórz lub wybierz hello żądanego zasobu.

## <a name="build-hello-app-with-application-insights"></a>Tworzenie aplikacji hello za pomocą usługi Application Insights
Usługa Application Insights może zapewnić bardziej szczegółową telemetrię dzięki instalacji zestawu SDK w Twojej aplikacji. W szczególności możesz gromadzić dzienniki śledzenia, [zapisywać niestandardową telemetrię](app-insights-api-custom-events-metrics.md) i uzyskiwać bardziej szczegółowe raporty o wyjątkach.

1. **W programie Visual Studio** (2013 Update 2 lub nowszym) skonfiguruj usługę Application Insights dla projektu.

    Kliknij prawym przyciskiem myszy projekt sieci web hello, a następnie wybierz **Dodaj > usługi Application Insights** lub **Konfiguruj usługę Application Insights**.
   
    ![Kliknij prawym przyciskiem myszy projekt sieci web hello i wybierz polecenie Dodaj i Konfiguruj usługę Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    Jeśli użytkownik jest proszony toosign w, należy użyć hello poświadczeń dla konta platformy Azure.
   
    Operacja Hello zawiera dwa efekty:
   
   1. Tworzy zasób usługi Application Insights na platformie Azure, gdzie telemetria jest przechowywana, analizowana i wyświetlana.
   2. Dodaje hello NuGet usługi Application Insights tooyour kod pakietu (jeśli go nie ma już) i skonfiguruje je toosend telemetrii toohello zasobów platformy Azure.
2. **Testowanie telemetrii hello** w uruchomionej aplikacji hello w komputerze deweloperskim (F5).
3. **Publikowanie aplikacji hello** tooAzure hello — w zwykły sposób. 

*Jak zmienić toosending tooa innego zasobu usługi Application Insights?*

* W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello, wybierz **Konfiguruj usługę Application Insights** i wybierz zasób hello ma. Pobierz toocreate opcji hello nowy zasób. Ponownie skompiluj i wdróż.

## <a name="explore-hello-data"></a>Eksplorowanie danych hello
1. W bloku usługi Application Insights hello Twojej aplikacji sieci web w Panelu sterowania, zobacz Live metryki przedstawiającego żądań i błędów w ciągu sekundy lub dwóch ich wystąpienia. Jest to bardzo przydatny widok w przypadku ponownego publikowania aplikacji — natychmiast zobaczysz wszelkie problemy.
2. Kliknij toohello pełne zasobu usługi Application Insights.

    ![Kliknij elementy](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Możesz tam przejść również bezpośrednio z nawigacji zasobów platformy Azure.

1. Kliknij za pomocą dowolnego tooget wykresu więcej szczegółów:
   
    ![W bloku Omówienie usługi Application Insights hello kliknij wykres](./media/app-insights-azure-web-apps/07-dependency.png)
   
    Możesz [dostosować bloki metryk](app-insights-metrics-explorer.md).
2. Kliknij go, dalsze toosee pojedynczych zdarzeń i ich właściwości:
   
    ![Kliknij przycisk tooopen typu zdarzenia wyszukiwania filtrowane wg typu](./media/app-insights-azure-web-apps/08-requests.png)
   
    Zwróć uwagę, Witaj "..." tooopen łącze wszystkich właściwości.
   
    Możesz [dostosować wyszukiwania](app-insights-diagnostic-search.md).

Bardziej zaawansowane wyszukiwanie za pośrednictwem telemetrii, użyj hello [języka zapytań usługi Analiza dzienników](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Dalsze funkcje telemetrii

* [Dane ładowania strony sieci Web](app-insights-javascript.md)
* [Telemetria niestandardowa](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki
* [Uruchom w aktywnej aplikacji hello profilera](app-insights-profiler.md).
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) — monitorowanie usługi Azure Functions za pomocą usługi Application Insights
* [Włącz diagnostykę Azure](app-insights-azure-diagnostics.md) tooApplication toobe wysyłane szczegółowe informacje.
* [Monitorowanie usługi kondycji metryk](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
* [Odbieraj powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.
* Użyj [usługi Application Insights dla aplikacji JavaScript i stron sieci web](app-insights-javascript.md) tooget klienta telemetrii hello przeglądarek, które strony sieci web.
* [Konfigurowanie testów sieci web dostępności](app-insights-monitor-web-app-availability.md) toobe alert, jeśli witryna jest wyłączony.

