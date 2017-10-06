---
title: "Analiza przechowywania aaaUser dla aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Ilu użytkowników zwraca tooyour aplikacji?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Analiza przechowywania użytkownika dla aplikacji sieci web za pomocą usługi Application Insights

Funkcja przechowywania Hello [Azure Application Insights](app-insights-overview.md) pomaga analizować ilu użytkowników zwracać tooyour aplikacji i jak często wykonywać określone zadania lub osiągnięcia celów. Na przykład po uruchomieniu gier lokacji można porównywać hello liczby użytkowników, którzy zwracać toohello lokacji po utracie gry o numerze hello którzy powrócić po nadanie pierwszeństwa. Ta wiedza może pomóc w usprawnieniu zarówno użytkowników, jak i jej strategią biznesową.

## <a name="get-started"></a>Rozpoczęcie pracy

Jeśli nie widzisz jeszcze danych w narzędziu przechowywania hello w portalu usługi Application Insights hello [Dowiedz się, jak tooget pracę z narzędziami użycia hello](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>Narzędzie do przechowywania Hello

![Narzędzie utrzymywania](./media/app-insights-usage-retention/retention.png)

1. Hello narzędzi umożliwia użytkownikom toocreate nowe raporty przechowywania, otwórz istniejących raportów przechowywania, Zapisz bieżący raport do przechowywania lub Zapisz jako, Przywróć zmiany toosaved raporty, odświeżania danych w hello raport, udziału za pośrednictwem poczty e-mail lub bezpośredniego łącza i hello dostępu stronę dokumentacji. 
2. Domyślnie przechowywania zawiera wszystkich użytkowników, którzy niczego została następnie wrócił i czy czymkolwiek innym przez okres. Można wybrać inną kombinację zdarzenia toonarrow hello fokus na działania konkretnego użytkownika.
3. Dodaj co najmniej jeden filtr właściwości. Na przykład można skoncentrować się na użytkowników w danym kraju lub regionu. Kliknij przycisk **aktualizacji** po ustawieniu filtrów hello. 
4. Hello ogólną przechowywania wykres przedstawia podsumowanie przechowywania użytkownika między hello w wybranym okresie. 
5. Siatka Hello pokazuje hello liczbę użytkowników, przechowywane zgodnie z konstruktora zapytań toohello w #2. Każdy wiersz reprezentuje kohorty użytkowników, który wykonał wszystkie zdarzenia w czasie hello przedstawionym okresie. Każdej komórki w wierszu hello pokazuje, ile tego kohorty zwróciła co najmniej raz w późniejszym terminie. W przypadku niektórych użytkowników może zwrócić więcej niż jednym okresie. 
6. karty insights Hello Pokaż górny pięć zdarzenia inicjujący i pięciu najwyższego zwracany zdarzenia toogive użytkowników lepiej zrozumieć ich przechowywania raportu. 

![Przesuwania myszy przechowywania](./media/app-insights-usage-retention/hover.png)

Użytkownicy mogą umieść kursor nad komórek na powitania przechowywania narzędzia tooaccess hello analytics przycisku, która oznacza wyjaśniający, jakie komórki hello etykietki narzędzi. przycisk Analytics Hello pobiera narzędzie analityczne toohello użytkowników z użytkownikami toogenerate wstępnie wypełnione zapytania hello komórki. 

## <a name="use-business-events-tootrack-retention"></a>Użyj przechowywania tootrack zdarzenia biznesowe

tooget hello najbardziej przydatne przechowywania analizy, zdarzenia miary, które reprezentują znaczących działalności. 

Na przykład wielu użytkowników może zostać otwarta strona w aplikacji bez gry hello, który jest wyświetlany. Śledzenie tylko hello wyświetleń strony w związku z tym Podaj oszacowanie niedokładne ile osób zwraca tooplay gry powitania po korzystających z wcześniej. tooget jasny obraz przekazujących odtwarzacze aplikacji należy wysłać zdarzenie niestandardowe, gdy użytkownik faktycznie jest odtwarzany.  

Należy dobrze toocode niestandardowych zdarzeń, które reprezentują akcji klucza biznesowych i ich używać do przechowywania analizy. toocapture hello wyniku gier, należy toowrite wiersz kodu toosend tooApplication zdarzenie niestandardowe szczegółowych informacji. Podczas pisania kodu strony sieci web hello lub w środowisku Node.JS, wygląda następująco:

```JavaScript
    appinsights.trackEvent("won game");
```

Lub w kodzie serwera ASP.NET:

```C#
   telemetry.TrackEvent("won game");
```

[Dowiedz się więcej na temat zapisywania zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Następne kroki
- Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.
    - [Użytkownicy, sesje, zdarzenia](app-insights-usage-segmentation.md)
    - [Lejki](usage-funnels.md)
    - [User Flows (Przepływy użytkowników)](app-insights-usage-flows.md)
    - [Skoroszyty](app-insights-usage-workbooks.md)
    - [Dodaj kontekstu użytkownika](app-insights-usage-send-user-context.md)


