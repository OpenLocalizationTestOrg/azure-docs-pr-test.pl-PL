---
title: "aaaDebug aplikacji za pomocą usługi Azure Application Insights w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Analiza wydajności i diagnostyka aplikacji sieci Web podczas debugowania oraz w środowisku produkcyjnym."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Debugowanie aplikacji przy użyciu usługi Azure Application Insights w programie Visual Studio
W programie Visual Studio (w wersji 2015 i nowszych) można analizować wydajność i diagnozować problemy w aplikacji sieci Web platformy ASP.NET zarówno podczas debugowania, jak i w środowisku produkcyjnym, przy użyciu telemetrii z usługi [Azure Application Insights](app-insights-overview.md).

Jeśli utworzono aplikację sieci web ASP.NET przy użyciu programu Visual Studio 2017 lub później, jest już hello zestaw SDK usługi Application Insights. W przeciwnym razie, jeśli użytkownik jeszcze tego nie zrobiono, [dodać usługi Application Insights tooyour aplikację](app-insights-asp-net.md).

toomonitor aplikacji po jej w środowisku produkcyjnym na żywo, zwykle wyświetlić hello telemetrii usługi Application Insights w hello [portalu Azure](https://portal.azure.com), gdzie można ustawić alertów i zastosować zaawansowanych narzędzi monitorowania. Jednak do debugowania, możesz również wyszukiwania i analizować dane telemetryczne hello w programie Visual Studio. Używając telemetrii tooanalyze programu Visual Studio zarówno z lokacji produkcyjnych i debugowanie działa na komputerze deweloperskim. W drugim przypadku hello można analizować debugowania działa nawet, jeśli jeszcze nie skonfigurowano hello SDK toosend telemetrii toohello portalu Azure. 

## <a name="run"></a> Debugowanie projektu
Uruchom aplikację sieci Web w trybie debugowania lokalnego, naciskając klawisz F5. Otwórz niektóre dane telemetryczne toogenerate różnych stron.

W programie Visual Studio zobacz temat liczbę hello zdarzenia, które zostały zarejestrowane przez moduł usługi Application Insights hello w projekcie.

![W programie Visual Studio przycisk Application Insights hello pokazuje podczas debugowania.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Kliknij ten przycisk toosearch telemetrii. 

## <a name="application-insights-search"></a>Wyszukiwanie usługi Application Insights
Okno wyszukiwania usługi Application Insights Hello zawiera zdarzenia, które zostały zarejestrowane. (Jeśli zalogowano tooAzure podczas konfigurowania usługi Application Insights, możesz wyszukać hello tego samego zdarzenia w portalu Azure hello.)

![Kliknij prawym przyciskiem myszy projekt hello i wybierz usługę Application Insights wyszukiwania](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Po zaznaczeniu lub Anuluj wybór filtrów, kliknij przycisk wyszukiwania hello na końcu hello hello pole wyszukiwania.
>

na wszystkie pola w zdarzeniach hello działa Hello dowolny tekst wyszukiwania. Na przykład wyszukać część hello adres URL strony; lub hello wartość właściwości, takie jak klient Miasto; lub słów w dzienniku śledzenia.

Kliknij przycisk Właściwości szczegółowe toosee żadnych zdarzeń.

Dla żądania tooyour aplikacji sieci web możesz kliknąć za pośrednictwem toohello kodu.

![W obszarze szczegółów żądania kliknij go, toohello kodu](./media/app-insights-visual-studio/31.png)

Elementy pokrewne można również otworzyć toohelp diagnozowanie żądań zakończonych niepowodzeniem lub wyjątki.

![W obszarze szczegółów żądania przewiń w dół toorelated elementów](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Wyświetl wyjątki oraz nieudanych żądań.
Pokaż raporty wyjątek hello wyszukiwania okna. (W niektórych starszych typów aplikacji sieci Web ASP.NET, należy za[monitorowania wyjątków](app-insights-asp-net-exceptions.md) toosee wyjątki, które są obsługiwane przez platformę hello.)

Kliknij przycisk tooget wyjątku, ślad stosu. Jeśli kod aplikacji hello hello jest otwarty w programie Visual Studio, możesz kliknąć za pośrednictwem z hello stosu śledzenia toohello odpowiedni wiersz kodu hello.

![Ślad stosu wyjątków](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Wyświetlanie podsumowań żądania i wyjątków w kodzie hello
W hello obiektyw kodu wiersz powyżej każdej metody obsługi można zobaczyć liczbę żądań hello i wyjątki zarejestrowane przez usługę Application Insights w ciągu ostatnich 24 godzin hello.

![Ślad stosu wyjątków](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Obiektyw kod przedstawia tylko dane usługi Application Insights, jeśli masz [skonfigurowane portalem usługi Application Insights aplikacji toosend telemetrii toohello](app-insights-asp-net.md).
>

[Więcej informacji o usłudze Application Insights w wierszach Code Lens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Trends
Trends to narzędzie do wizualizacji zachowania aplikacji wraz z upływem czasu. 

Wybierz **Eksploruj trendy Telemetrii** z przycisku paska narzędzi Application Insights hello lub okno wyszukiwania usługi Application Insights. Wybierz jeden z pięciu tooget zapytania wspólnej pracy. W zależności od typów telemetrii, zakresów czasu i innych właściwości możesz analizować różne zestawy danych . 

anomalie toofind danych, wybierz jedną z opcji anomalii hello w obszarze rozwijanym "Typ widoku" hello. Opcje filtrowania Hello u dołu okna hello hello był łatwo toohone w na konkretne podzestawy telemetrii.

![Trends](./media/app-insights-visual-studio/51.png)

[Więcej informacji na temat narzędzia Trends](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Monitorowanie lokalne
(Z programu Visual Studio 2015 Update 2) Jeśli nie skonfigurowano portalu Application Insights toohello telemetrii toosend hello SDK (tak, aby klucz nie istnieje Instrumentacji w ApplicationInsights.config) okna diagnostyki hello wyświetla dane telemetryczne z sesji debugowania najnowsza wersja. 

Jest to pożądane, jeśli poprzednia wersji aplikacji została już opublikowana. Nie chcesz telemetrii hello z Twojej debugowania toobe sesji łączyć z telemetrii hello na powitania portalu Application Insights z opublikowanych aplikacji hello.

Jest również przydatne w przypadku niektórych [telemetria niestandardowa](app-insights-api-custom-events-metrics.md) mają toodebug przed wysłaniem danych telemetrycznych toohello portalu.

* *Na początku I w pełni skonfigurowane usługi Application Insights toosend telemetrii toohello portalu. A teraz chcesz I dane telemetryczne hello toosee tylko w programie Visual Studio.*
  
  * W ustawieniach okna wyszukiwania hello jest opcja toosearch lokalnego diagnostyki nawet wtedy, gdy aplikacja wysyła dane telemetryczne toohello portalu.
  * dane telemetryczne toostop wysyłane toohello portalu komentarz linii hello `<instrumentationkey>...` z ApplicationInsights.config. Jeśli wszystko jest gotowe toosend telemetrii toohello portal Usuń komentarz.


## <a name="next-steps"></a>Następne kroki
|  |  |
| --- | --- |
| **[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**<br/>Monitorowanie użycia, dostępności, zależności i wyjątków. Integrowanie śladów ze struktur rejestrowania. Zapisywanie niestandardowych danych telemetrycznych. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Praca z portalu Application Insights hello](app-insights-dashboards.md)**<br/>Wyświetlanie pulpitów nawigacyjnych, zaawansowanych narzędzi diagnostycznych i danych analitycznych, alerty, mapa na żywo zależności aplikacji i danych telemetrycznych wyeksportowane. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

