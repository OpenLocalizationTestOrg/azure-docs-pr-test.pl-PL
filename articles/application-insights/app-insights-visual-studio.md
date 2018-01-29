---
title: "Debugowanie aplikacji z usługą Azure Application Insights w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Analiza wydajności i diagnostyka aplikacji sieci Web podczas debugowania oraz w środowisku produkcyjnym."
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: mbullwin
ms.openlocfilehash: 656c62e7227eef967696715f0882114631249c6c
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Debugowanie aplikacji przy użyciu usługi Azure Application Insights w programie Visual Studio
W programie Visual Studio (w wersji 2015 i nowszych) można analizować wydajność i diagnozować problemy w aplikacji sieci Web platformy ASP.NET zarówno podczas debugowania, jak i w środowisku produkcyjnym, przy użyciu telemetrii z usługi [Azure Application Insights](app-insights-overview.md).

Jeśli aplikację sieci Web platformy ASP.NET utworzono przy użyciu programu Visual Studio 2017 lub nowszego, zawiera już ona zestaw SDK usługi Application Insights. W przeciwnym razie, jeśli jeszcze tego nie zrobiono, należy [dodać usługę Application Insights do aplikacji](app-insights-asp-net.md).

Monitorowanie aplikacji w środowisku produkcyjnym zwykle polega na przeglądaniu danych telemetrycznych z usługi Application Insights w witrynie [Azure Portal](https://portal.azure.com), w której można ustawiać alerty i stosować zaawansowane narzędzia do monitorowania. Jednak na potrzeby debugowania można również wyszukiwać i analizować dane telemetryczne w programie Visual Studio. Visual Studio umożliwia analizowanie danych telemetrycznych zarówno z lokacji produkcyjnych i debugowanie działa na komputerze deweloperskim. W tym ostatnim przypadku można analizować przebiegi debugowania, nawet jeśli nie skonfigurowano jeszcze zestawu SDK na potrzeby wysyłania danych telemetrycznych do witryny Azure Portal. 

## <a name="run"></a> Debugowanie projektu
Uruchom aplikację sieci Web w trybie debugowania lokalnego, naciskając klawisz F5. Otwórz różne strony w celu wygenerowania telemetrii.

W programie Visual Studio zobacz temat liczbę zdarzeń, które zostały zarejestrowane przez moduł usługi Application Insights w projekcie.

![Przycisk usługi Application Insights jest widoczny w programie Visual Studio podczas debugowania.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Kliknij ten przycisk, aby wyszukać dane telemetryczne. 

## <a name="application-insights-search"></a>Wyszukiwanie usługi Application Insights
Okno wyszukiwania usługi Application Insights pokazuje zarejestrowane zdarzenia. (Jeśli użytkownik zarejestrowany w usłudze Azure podczas konfigurowania usługi Application Insights, można wyszukiwać tego samego zdarzenia w portalu Azure.)

![Kliknij prawym przyciskiem myszy projekt i wybierz kolejno opcje Application Insights, Wyszukiwanie](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Po wybraniu lub anulowaniu wyboru filtrów kliknij przycisk wyszukiwania na końcu tekstowego pola wyszukiwania.
>

Wyszukiwanie dowolnego tekstu działa we wszystkich polach zdarzeń. Można wyszukać na przykład część adresu URL strony, wartość właściwości (taką jak miasto klienta) lub określone słowa w dzienniku śledzenia.

Kliknij dowolne zdarzenie, aby wyświetlić jego szczegółowe właściwości.

W celu wyświetlenia żądań wysyłanych do aplikacji sieci Web można kliknąć w obrębie kodu.

![W obszarze Szczegóły żądania kliknij w obrębie kodu](./media/app-insights-visual-studio/31.png)

Można również otworzyć elementy pokrewne, aby łatwiej diagnozować niepowodzenia żądań lub wyjątki.

![W obszarze Szczegóły żądania przewiń w dół do elementów pokrewnych](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Wyświetl wyjątki oraz nieudanych żądań.
Raporty dotyczące wyjątków są wyświetlane w oknie wyszukiwania. W niektórych starszych typach aplikacji sieci Web platformy ASP.NET trzeba [skonfigurować monitorowanie wyjątków](app-insights-asp-net-exceptions.md), aby zobaczyć wyjątki, które są obsługiwane przez architekturę.

Kliknij wyjątek, aby uzyskać ślad stosu. Jeśli kod aplikacji jest otwarty w programie Visual Studio, można przejść przez ślad stosu do odpowiedniego wiersza kodu.

![Ślad stosu wyjątków](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a>Wyświetlanie podsumowań żądania i wyjątków w kodzie
W wierszu kodu obiektyw powyżej każdej metody obsługi można zobaczyć liczbę żądań i wyjątki zarejestrowane przez usługę Application Insights w ciągu ostatnich 24 godzin.

![Ślad stosu wyjątków](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Dane usługi Application Insights są wyświetlane w wierszach Code Lens tylko wtedy, gdy [skonfigurowano aplikację na potrzeby wysyłania danych telemetrycznych do portalu usługi Application Insights](app-insights-asp-net.md).
>

[Więcej informacji o usłudze Application Insights w wierszach Code Lens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Trends
Trends to narzędzie do wizualizacji zachowania aplikacji wraz z upływem czasu. 

Na przycisku paska narzędzi Application Insights lub w oknie Application Insights Search wybierz pozycję **Eksploruj trendy telemetryczne**. Wybierz jedno z pięciu typowych zapytań, aby rozpocząć. W zależności od typów telemetrii, zakresów czasu i innych właściwości możesz analizować różne zestawy danych . 

Aby znaleźć anomalie w danych, wybierz jedną z opcji anomalii w menu rozwijanym „Typ widoku”. Opcje filtrowania u dołu okna ułatwiają sprecyzowanie konkretnych podzestawów w telemetrii.

![Trends](./media/app-insights-visual-studio/51.png)

[Więcej informacji na temat narzędzia Trends](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Monitorowanie lokalne
(Z programu Visual Studio 2015 Update 2) Jeśli nie skonfigurowano zestaw SDK, aby wysłać dane telemetryczne do portalu usługi Application Insights (tak, aby klucz nie istnieje Instrumentacji w ApplicationInsights.config) oknie diagnostyki wyświetla dane telemetryczne z sesji debugowania najnowsza wersja. 

Jest to pożądane, jeśli poprzednia wersji aplikacji została już opublikowana. Lepiej, aby telemetria z sesji debugowania nie była mieszana z telemetrią z opublikowanej aplikacji w portalu Application Insights.

Jest to również przydatne, jeśli masz trochę [niestandardowej telemetrii](app-insights-api-custom-events-metrics.md), którą chcesz debugować przed wysłaniem telemetrii do portalu.

* *Na początku usługa Application Insights została skonfigurowana do wysyłania telemetrii do portalu, ale teraz chcę widzieć telemetrię tylko w programie Visual Studio.*
  
  * W ustawieniach okna wyszukiwania istnieje możliwość wyszukiwania lokalnych danych diagnostycznych, nawet jeśli aplikacja wysyła telemetrię do portalu.
  * Aby zatrzymać przesyłanie telemetrii do portalu, zakomentuj wiersz `<instrumentationkey>...` w pliku ApplicationInsights.config. Gdy wszystko będzie gotowe, odkomentuj wiersz, aby wznowić wysyłanie telemetrii do portalu.


## <a name="next-steps"></a>Następne kroki
|  |  |
| --- | --- |
| **[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**<br/>Monitorowanie użycia, dostępności, zależności i wyjątków. Integrowanie śladów ze struktur rejestrowania. Zapisywanie niestandardowych danych telemetrycznych. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Praca z portalem usługi Application Insights](app-insights-dashboards.md)**<br/>Wyświetlanie pulpitów nawigacyjnych, zaawansowanych narzędzi diagnostycznych i danych analitycznych, alerty, mapa na żywo zależności aplikacji i danych telemetrycznych wyeksportowane. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

