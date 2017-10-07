---
title: aaaMicrosoft Dynamics CRM i Azure Application Insights | Dokumentacja firmy Microsoft
description: "Pobierz dane telemetryczne z programu Microsoft Dynamics CRM Online przy użyciu usługi Application Insights. Pobieranie danych, wizualizacji i eksportowanie Przewodnik instalacji."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Wskazówki: Włączanie dane telemetryczne dla programu Microsoft Dynamics CRM Online przy użyciu usługi Application Insights
W tym artykule opisano sposób danych telemetrycznych tooget [Microsoft Dynamics CRM Online](https://www.dynamics.com/) przy użyciu [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Zostanie omówiony hello Zakończ proces dodawania aplikacji tooyour skryptu usługi Application Insights, przechwytywania danych i wizualizacji danych.

> [!NOTE]
> [Przeglądaj hello przykładowe rozwiązanie](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Dodawanie usługi Application Insights toonew lub istniejącego wystąpienia CRM Online
toomonitor aplikacji, należy dodać aplikację tooyour zestaw SDK usługi Application Insights. Witaj SDK wysyła dane telemetryczne toohello [portalu Application Insights](https://portal.azure.com), której można użyć naszych zaawansowane analizy i narzędzia diagnostyczne lub wyeksportować hello toostorage danych.

### <a name="create-an-application-insights-resource-in-azure"></a>Tworzenie zasobu usługi Application Insights na platformie Azure
1. Pobierz [konta na platformie Microsoft Azure](http://azure.com/pricing). 
2. Zaloguj się na powitania [portalu Azure](https://portal.azure.com) i Dodaj nowy zasób usługi Application Insights. Jest to, gdzie opracowywania i wyświetlania danych.
   
    ![Kliknij pozycję +, usług deweloperskich, usługi Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Wybierz platformy ASP.NET, jako typ aplikacji hello.
3. Otwórz stronę wprowadzenie hello i otworzyć "Monitor i diagnozowanie po stronie klienta".
   
    ![Fragment kodu dotyczący wstawiania na stronie sieci web](./media/app-insights-sample-mscrm/03.png)

**Nie zamykaj strony kodowej hello** podczas hello następnego kroku w innym oknie przeglądarki. Będziesz potrzebować kodu hello wkrótce. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Utwórz zasób sieci web JavaScript w programie Microsoft Dynamics CRM
1. Otwórz wystąpienie CRM Online, a logowanie z uprawnieniami administratora.
2. Otwieranie programu Microsoft Dynamics CRM ustawienia, dostosowania, Dostosuj hello systemu
   
    ![Ustawienia programu Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Ustawienia > dostosowania](./media/app-insights-sample-mscrm/05.png)

    ![Dostosowywanie opcji system hello](./media/app-insights-sample-mscrm/06.png)

1. Utwórz zasób języka JavaScript.
   
    ![Okno dialogowe nowego zasobu sieci Web](./media/app-insights-sample-mscrm/07.png)
   
    Nadaj mu nazwę, wybierz opcję **skryptu (JScript)** i hello Otwórz Edytor tekstów.
   
    ![Witaj Otwórz Edytor tekstu](./media/app-insights-sample-mscrm/08.png)
2. Skopiuj kod hello z usługi Application Insights. Podczas kopiowania upewnij się, że tooignore tagów skryptu. Zapoznaj się poniżej zrzut ekranu:
   
    ![Ustaw klucz Instrumentacji](./media/app-insights-sample-mscrm/09.png)
   
    Kod Hello obejmuje hello Instrumentacji klucza, który identyfikuje z zasobu usługi Application insights.
3. Zapisz i opublikuj.
   
    ![Zapisz i opublikuj](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Formularze dokumentu
1. W programie Microsoft CRM Online Otwórz formularz konta hello
   
    ![Formularz konta](./media/app-insights-sample-mscrm/11.png)
2. Otwórz formularz hello właściwości
   
    ![Właściwości formularza](./media/app-insights-sample-mscrm/12.png)
3. Dodaj hello utworzony zasób sieci web JavaScript
   
    ![Dodawanie menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Dodaj zasób sieci web hello](./media/app-insights-sample-mscrm/14.png)
4. Zapisz i opublikuj swoje dostosowania formularza.

## <a name="metrics-captured"></a>Metryki przechwycić
Po skonfigurowaniu teraz przechwytywania danych telemetrycznych hello formularza. Zawsze, gdy jest on używany, dane zostaną wysłane tooyour zasobu usługi Application Insights.

Poniżej przedstawiono przykłady hello danych, który zostanie wyświetlony.

#### <a name="application-health"></a>Kondycja aplikacji
![Czas ładowania strony przykład](./media/app-insights-sample-mscrm/15.png)

![Przykład strony widoki wykresu](./media/app-insights-sample-mscrm/16.png)

Wyjątki przeglądarki:

![Wykres wyjątków przeglądarki](./media/app-insights-sample-mscrm/17.png)

Kliknij tooget wykresu hello więcej szczegółów:

![Listy wyjątków](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Sposób użycia
![Użytkownikami, sesjami i wyświetleń strony](./media/app-insights-sample-mscrm/19.png)

![Wykresy sesji](./media/app-insights-sample-mscrm/20.png)

![Wersji przeglądarki](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Przeglądarki
![Podział czas ładowania strony](./media/app-insights-sample-mscrm/22.png)

![Liczba sesji według wersji przeglądarki](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Używanie funkcji Geolokalizacji
![Liczba sesji według kraju](./media/app-insights-sample-mscrm/24.png)

![Sesje i użytkowników według kraju](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Żądanie dostępu do strony w widoku
![Podsumowanie widoku strony](./media/app-insights-sample-mscrm/26.png)

![Wyszukaj zdarzenia widoku strony](./media/app-insights-sample-mscrm/27.png)

![Podobne wyświetleń strony](./media/app-insights-sample-mscrm/28.png)

![Właściwości wyświetlania stron](./media/app-insights-sample-mscrm/29.png)

![Strony na sesję](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Przykładowy kod
[Przeglądaj hello przykładowy kod](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Nawet dokładniejszej analizy można zrobić, jeśli użytkownik [wyeksportować hello tooMicrosoft danych usługi Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Przykładowe Microsoft Dynamics CRM rozwiązanie
[Oto hello przykładowe rozwiązanie zaimplementowane w programie Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Dowiedz się więcej
* [Co to jest Application Insights?](app-insights-overview.md)
* [Application Insights dla stron sieci web](app-insights-javascript.md)
* [Więcej przykłady i wskazówki](app-insights-code-samples.md)
