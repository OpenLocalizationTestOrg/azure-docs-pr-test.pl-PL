---
title: "Analiza aaaUser sesji i zdarzeń w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analiza demograficznych użytkowników aplikacji sieci web."
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Analiza użytkownikami, sesjami i zdarzeń w usłudze Application Insights

Dowiedz się, gdy użytkownicy korzystają z aplikacji sieci web, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają. Analizowanie telemetrii działalności biznesowej i użycia za pomocą [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Rozpoczęcie pracy

Jeśli nie widzisz jeszcze danych w hello użytkowników, sesji lub bloków zdarzenia w portalu usługi Application Insights hello [Dowiedz się, jak tooget pracę z narzędziami użycia hello](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>Narzędzie segmentacji Hello użytkownikami, sesjami i zdarzenia

Trzy użycia hello używać bloków hello tego samego narzędzia tooslice i kości dane telemetryczne z aplikacji sieci web z trzema perspektyw. Filtrowanie i dzielenia danych hello, można ujawnić informacjami na temat hello względną użycie różnych stron i funkcji.

* **Narzędzie Użytkownicy**: używane wiele aplikacji i ich funkcje.  Użytkownicy są liczone przy użyciu anonimowego identyfikatorów przechowywane w plikach cookie przeglądarki. Jedna osoba, za pomocą różnych przeglądarkach lub maszyny będą liczone jako więcej niż jednego użytkownika.
* **Narzędzie sesje**: ile sesji aktywności użytkowników, zostały uwzględnione w pewnych stron i funkcji aplikacji. Sesja jest traktowane po pół godziny czas braku aktywności użytkownika, lub 24 godziny ciągłego użytkowania.
* **Narzędzie zdarzenia**: jak często używane pewnych stron i funkcji aplikacji. Widok strony jest liczony przeglądarką załadowanie strony z aplikacji, pod warunkiem, że [zinstrumentowane on](app-insights-javascript.md). 

    Zdarzenie niestandardowe reprezentuje jedno wystąpienie określonego zdarzenia w aplikacji, często interakcji z użytkownikiem jak kliknij przycisk hello zakończenie niektórych zadań. W aplikacji Wstawianie zbyt kodu[generowanie zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent).

![Użycie narzędzia](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Wykonywanie zapytania dla niektórych użytkowników 

Zapoznaj się z różnych grup użytkowników przez dostosowanie wartości opcji zapytania hello u góry hello hello użytkowników narzędzia: 

* Kto używane: Wybierz niestandardowych zdarzeń i wyświetlenia strony. 
* W trakcie: Wybierz zakres czasu. 
* Przez: Wybierz, jak toobucket hello danych przez pewien czas lub innej właściwości, takie jak przeglądarki lub Miasto. 
* Dzielenie przez: Wybierz właściwość przez danych hello toosplit lub segmentu. 
* Dodaj filtry: Ograniczyć hello zapytania toocertain użytkowników, sesji lub zdarzenia na podstawie ich właściwości, takie jak przeglądarki lub Miasto. 
 
## <a name="saving-and-sharing-reports"></a>Zapisywanie i udostępnianie raportów 
Można zapisać raportów użytkowników, albo prywatnej tooyou tylko w sekcji Moje raporty hello, lub udostępniać inne osoby z toothis dostępu do zasobu usługi Application Insights w hello sekcji udostępnionych raportów.  
 
Podczas zapisywania raportu lub edytowania jego właściwości, wybierz toosave "Bieżący względny zakres czasu", który raport będzie stale odświeżyć dane, wracając niektórych stałej ilości czasu.  
 
Wybierz raport o ustalony zbiór danych toosave "Bieżący bezwzględny zakres czasu". Należy pamiętać, że dane w usłudze Application Insights tylko są przechowywane przez 90 dni, więc jeśli minęło ponad 90 dni od raport z zakresem bezwzględnego czasu został zapisany, hello raportu zostanie wyświetlona pusta. 
 
## <a name="example-instances"></a>Przykład wystąpień

Hello przykład wystąpień sekcja zawiera informacje o kilka poszczególnych użytkowników, sesji lub zdarzeń, które są dopasowane wg hello bieżącego zapytania. Biorąc pod uwagę i eksploracji hello zachowania jednostek w tooaggregates dodanie zapewniają wgląd w sposób osoby faktycznie używają Twojej aplikacji. 
 
## <a name="insights"></a>Insights 

pasek boczny Insights Hello pokazuje dużych klastrach użytkowników, które mają wspólne właściwości. Tych klastrów można ujawnić zaskakująco trendy w sposób użytkownicy korzystają z aplikacji. Na przykład, jeśli 40% wszystkich hello użycia aplikacji pochodzi z osoby za pomocą jednej funkcji.  


## <a name="next-steps"></a>Następne kroki
- Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.
    - [Lejki](usage-funnels.md)
    - [Przechowywanie](app-insights-usage-retention.md)
    - [User Flows (Przepływy użytkowników)](app-insights-usage-flows.md)
    - [Skoroszyty](app-insights-usage-workbooks.md)
    - [Dodaj kontekstu użytkownika](app-insights-usage-send-user-context.md)

