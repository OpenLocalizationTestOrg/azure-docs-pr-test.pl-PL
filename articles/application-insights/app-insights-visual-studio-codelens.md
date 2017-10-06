---
title: "aaaApplication telemetrii wgląd w Visual Studio CodeLens | Dokumentacja firmy Microsoft"
description: "Szybki dostęp do żądania usługi Application Insights i wyjątków telemetrii za pomocą funkcji CodeLens w programie Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Telemetria usługi Application Insights i użycie funkcji CodeLens programu Visual Studio
Metody w kodzie hello aplikacji sieci web może być oznaczony za pomocą dane telemetryczne dotyczące wyjątków w czasie wykonywania i czas odpowiedzi na żądanie. Po zainstalowaniu [Azure Application Insights](app-insights-overview.md) w aplikacji hello telemetrii pojawia się w programie Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) — Witaj uwagi na początku każdej funkcji, w którym użyto hello tooseeing przydatne informacje takie jak numer hello funkcji hello miejsca odwołuje się do lub hello ostatniej osoby, która go edytować.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Usługa Application Insights w funkcji CodeLens jest dostępne w programie Visual Studio 2015 Update 3 i później lub z hello najnowszą wersję [Developer Analytics Tools rozszerzenia](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens są dostępne w hello Enterprise i Professional wersji programu Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Gdzie toofind dane usługi Application Insights
Poszukaj telemetrii usługi Application Insights w wskaźniki CodeLens hello hello metod publicznych żądania aplikacji sieci web. Wskaźniki CodeLens są wyświetlane powyżej metody i innych deklaracji w kodzie języka C# i Visual Basic. Jeśli dane usługi Application Insights są dostępne dla metody, zobaczysz wskaźniki dla żądań i wyjątków, takie jak „100 żądań, 1% zakończony niepowodzeniem” lub „Liczba wyjątków: 10”. Kliknij wskaźnik CodeLens, aby uzyskać więcej szczegółów. 

> [!TIP]
> Żądania usługi Application Insights i wskaźniki wyjątku może zająć kilka sekund dodatkowe tooload po innych wskaźników CodeLens są wyświetlane.
> 
> 

## <a name="exceptions-in-codelens"></a>Wyjątki w funkcji CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

wskaźników CodeLens wyjątek Hello pokazuje hello liczbę wyjątków, które wystąpiły w hello ostatnich 24 godzin z hello 15 większości wyjątki często występujących w aplikacji w tym okresie, podczas przetwarzania żądania hello obsługiwane przez metody hello.

toosee więcej szczegółów, kliknij wskaźników CodeLens wyjątki hello:

* Procent Hello zmiana liczby wyjątki od hello najnowszych 24 godziny względne toohello poprzednich 24 godzin
* Wybierz **Przejdź toocode** kod źródłowy toohello toonavigate hello zgłaszanie wyjątków hello — funkcja
* Wybierz **wyszukiwania** tooquery wszystkich wystąpień tego wyjątku, które wystąpiły w hello w ciągu ostatnich 24 godzin
* Wybierz **Trend** tooview wizualizacji trend dla wystąpień tego wyjątku w hello ostatnich 24 godzin
* Wybierz **Wyświetl wszystkie wyjątki w tej aplikacji** tooquery wszystkie wyjątki, które wystąpiły w hello w ciągu ostatnich 24 godzin
* Wybierz **Eksploruj trendy wyjątek** tooview wizualizacji trend wszystkie wyjątki, które wystąpiły w hello ostatnich 24 godzin. 

> [!TIP]
> Jeśli widzisz "wyjątki 0" w funkcji CodeLens, ale wiesz, że powinien istnieć wyjątki, sprawdź toomake się, że wybrano hello prawo zasobu usługi Application Insights w funkcji CodeLens. tooselect inny zasób, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań hello i wybierz polecenie **usługi Application Insights > Wybierz źródło danych Telemetrycznych**. CodeLens jest wyświetlana tylko dla hello 15 większości wyjątki często występujących w aplikacji hello ostatnich 24 godzin, dlatego jeśli wyjątek jest często hello większość 16 lub mniej, zobaczysz "wyjątki 0". Wyjątki od widoki ASP.NET nie może występować na metod kontrolera hello wygenerowanych widoków.
> 
> [!TIP]
> Jeśli widzisz komunikat „Liczba wyjątki"w funkcji CodeLens, należy tooassociate, które konta platformy Azure z programu Visual Studio lub Twoje poświadczenia konta Azure mogło wygasnąć. W obu przypadkach kliknij pozycję „Liczba wyjątki"i wybierz polecenie **Dodaj konto...**  tooenter swoje poświadczenia.
> 
> 

## <a name="requests-in-codelens"></a>Żądania w funkcji CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Witaj żądania CodeLens wskaźnik pokazuje hello liczba HTTP żądania wysyłane przez zostały obsługiwane przez metody w powitania po 24 godzinach, a także hello odsetek te żądania, których nie powiodła się.

toosee więcej szczegółów, kliknij przycisk hello żądań wskaźników CodeLens:

* Witaj zmiany bezwzględnym i procent liczby żądań, nieudanych żądań i odpowiedzi średni czas na powitania poza toohello 24 godzin względem poprzednich 24 godzin
* niezawodność Hello metody hello obliczany jako hello odsetek żądań, które działał prawidłowo w hello ostatnich 24 godzin
* Wybierz **wyszukiwania** dla żądania lub tooquery żądań zakończonych niepowodzeniem hello wszystkie żądania (nieudane), które wystąpiły w hello ostatnich 24 godzin
* Wybierz **Trend** tooview wizualizacji trend dla żądania, nieudane żądania lub odpowiedzi średni razy w hello ostatnich 24 godzin.
* Wybierz nazwę hello hello zasobu usługi Application Insights w hello lewego górnego rogu hello CodeLens Szczegóły widoku toochange zasobu, który jest źródłem hello dane CodeLens.

## <a name="next"></a>Następne kroki
|  |  |
| --- | --- |
| **[Praca z usługą Application Insights w programie Visual Studio](app-insights-visual-studio.md)**<br/>Wyszukiwanie danych telemetrycznych, wyświetlanie danych CodeLens i konfigurowanie usługi Application Insights. Wszystko to w programie Visual Studio. |![Kliknij prawym przyciskiem myszy projekt hello i wybierz usługę Application Insights wyszukiwania](./media/app-insights-visual-studio-codelens/34.png) |
| **[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**<br/>Monitorowanie użycia, dostępności, zależności i wyjątków. Integrowanie śladów ze struktur rejestrowania. Zapisywanie niestandardowych danych telemetrycznych. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Praca z portalu Application Insights hello](app-insights-dashboards.md)**<br/>Pulpity nawigacyjne, zaawansowane narzędzia diagnostyczne i analityczne, alerty, mapa zależności aplikacji na żywo oraz eksportowanie telemetrii. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

