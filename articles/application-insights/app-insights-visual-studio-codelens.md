---
title: "Telemetria usługi Application Insights i użycie funkcji CodeLens programu Visual Studio | Microsoft Docs"
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
ms.author: mbullwin
ms.openlocfilehash: 418c391f896ac60f509b963f0aff70ad699fc43b
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Telemetria usługi Application Insights i użycie funkcji CodeLens programu Visual Studio
Metody w kodzie aplikacji sieci Web mogą być adnotowane przy użyciu telemetrii dotyczącej wyjątków czasu wykonywania i czasu odpowiedzi na żądanie. W przypadku instalowania usługi [Azure Application Insights](app-insights-overview.md) w aplikacji dane telemetryczne pojawią się w funkcji [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) programu Visual Studio — w uwagach na górze każdej funkcji, w których są wyświetlane użyteczne informacje, takie jak liczba miejsc, w których odwoływano się do funkcji i nazwisko ostatniej osoby, która ją edytowała.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Usługa Application Insights z funkcją CodeLens jest dostępna w programie Visual Studio 2015 Update 3 i nowszych lub w najnowszej wersji [rozszerzenia programu Developer Analytics Tools](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). Funkcja CodeLens jest dostępna w wersjach Professional i Enterprise programu Visual Studio.
> 
> 

## <a name="where-to-find-application-insights-data"></a>Znajdywanie danych usługi Application Insights
Poszukaj danych telemetrycznych usługi Application Insights we wskaźnikach CodeLens dla metod publicznych żądań aplikacji sieci Web. Wskaźniki CodeLens są wyświetlane powyżej metody i innych deklaracji w kodzie języka C# i Visual Basic. Jeśli dane usługi Application Insights są dostępne dla metody, zobaczysz wskaźniki dla żądań i wyjątków, takie jak „100 żądań, 1% zakończony niepowodzeniem” lub „Liczba wyjątków: 10”. Kliknij wskaźnik CodeLens, aby uzyskać więcej szczegółów. 

> [!TIP]
> Ładowanie wskaźników żądań i wyjątków usługi Application Insights może potrwać kilka dodatkowych sekund dłużej niż wyświetlenie innych wskaźników CodeLens.
> 
> 

## <a name="exceptions-in-codelens"></a>Wyjątki w funkcji CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

Wskaźnik CodeLens wyjątku pokazuje liczbę wyjątków, które wystąpiły w ciągu ostatnich 24 godzin w 15 najczęściej występujących wyjątkach w aplikacji w tym okresie podczas przetwarzania żądania obsłużonego przez metodę.

Aby uzyskać szczegółowe informacje, kliknij wskaźnik CodeLens wyjątków:

* Wartość procentowa zmiany w liczbie wyjątków z ostatnich 24 godzin względem poprzednich 24 godzin
* Wybierz polecenie **Przejdź do kodu**, aby przejść do kodu źródłowego dla funkcji wywołującej wyjątek
* Wybierz polecenie **Wyszukaj**, aby wykonać zapytania do wszystkich wystąpień tego wyjątku, które wystąpiły w ciągu ostatnich 24 godzin
* Wybierz polecenie **Trend**, aby wyświetlić wizualizację trendu dla wystąpień tego wyjątku w ciągu ostatnich 24 godzin
* Wybierz polecenie **Wyświetl wszystkie wyjątki w tej aplikacji**, aby wykonać zapytania do wszystkich wyjątków, które wystąpiły w ciągu ostatnich 24 godzin
* Wybierz polecenie **Eksploruj trendy wyjątków**, aby wyświetlić wizualizację trendu dla wszystkich wyjątków, które wystąpiły w ciągu ostatnich 24 godzin. 

> [!TIP]
> Jeśli widzisz komunikat „Liczba wyjątków: 0” w funkcji CodeLens, ale wiesz, że powinny pojawić się wyjątki, upewnij się, że wybrano właściwy zasób usługi Application Insights w funkcji CodeLens. Aby wybrać inny zasób, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz polecenie **Application Insights > Wybierz źródło telemetrii**. Funkcja CodeLens jest wyświetlana tylko dla 15 najczęściej występujących wyjątków w aplikacji w ciągu ostatnich 24 godzin, dlatego jeśli wyjątek znajduje się na miejscu 16 lub dalszym, zobaczysz informację „Liczba wyjątków: 0”. Wyjątki od widoków platformy ASP.NET mogą nie pojawić się w metodach kontrolera, które wygenerowały te widoki.
> 
> [!TIP]
> Jeśli widzisz komunikat „Liczba wyjątków: ?” w funkcji CodeLens, należy skojarzyć konto platformy Azure z programem Visual Studio lub może się okazać, że poświadczenie Twojego konta platformy Azure wygasło. W obu przypadkach kliknij pozycję „Liczba wyjątków: ?” i wybierz polecenie **Dodaj konto...**, aby wprowadzić poświadczenia.
> 
> 

## <a name="requests-in-codelens"></a>Żądania w funkcji CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Wskaźnik CodeLens żądania pokazuje liczbę żądań HTTP, które zostały obsłużone przez metodę w ciągu ostatnich 24 godzin oraz wartość procentową żądań, które nie powiodły się.

Aby uzyskać szczegółowe informacje, kliknij wskaźnik CodeLens żądań:

* Wartość bezwzględna i procentowa zmian w liczbie żądań, żądań zakończonych niepowodzeniem lub średnim czasie odpowiedzi z ostatnich 24 godzin względem poprzednich 24 godzin
* Niezawodność metody, obliczana jako procent żądań, które nie zakończyły się niepowodzeniem w ciągu ostatnich 24 godzin
* Wybierz polecenie **Wyszukaj** dla żądań lub żądań zakończonych niepowodzeniem, aby wykonać zapytania do wszystkich żądań (zakończonych niepowodzeniem), które wystąpiły w ciągu ostatnich 24 godzin
* Wybierz polecenie **Trend**, aby wyświetlić wizualizację trendu dla żądań, żądań zakończonych niepowodzeniem lub średniego czasu odpowiedzi w ciągu ostatnich 24 godzin.
* Wybierz nazwę zasobu usługi Application Insights w lewym górnym rogu widoku szczegółów funkcji CodeLens, aby zmienić zasób, który jest źródłem danych tej funkcji.

## <a name="next"></a>Następne kroki
|  |  |
| --- | --- |
| **[Praca z usługą Application Insights w programie Visual Studio](app-insights-visual-studio.md)**<br/>Wyszukiwanie danych telemetrycznych, wyświetlanie danych CodeLens i konfigurowanie usługi Application Insights. Wszystko to w programie Visual Studio. |![Kliknij prawym przyciskiem myszy projekt i wybierz kolejno opcje Application Insights, Wyszukiwanie](./media/app-insights-visual-studio-codelens/34.png) |
| **[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**<br/>Monitorowanie użycia, dostępności, zależności i wyjątków. Integrowanie śladów ze struktur rejestrowania. Zapisywanie niestandardowych danych telemetrycznych. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Praca z portalem usługi Application Insights](app-insights-dashboards.md)**<br/>Pulpity nawigacyjne, zaawansowane narzędzia diagnostyczne i analityczne, alerty, mapa zależności aplikacji na żywo oraz eksportowanie telemetrii. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

