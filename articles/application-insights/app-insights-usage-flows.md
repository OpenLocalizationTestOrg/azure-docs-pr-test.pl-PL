---
title: "aaaAnalyze wzorców nawigacji użytkownika z przepływów użytkownika w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przeanalizuj, jak użytkownicy nawigują między stronami hello i funkcje aplikacji sieci web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Analizować wzorce nawigacji użytkownika z przepływów użytkownika w usłudze Application Insights

![Narzędzia przepływu użytkownika Insights aplikacji](./media/app-insights-usage-flows/flows.png)

narzędzia przepływu użytkownika Hello wizualizuje, jak użytkownicy nawigują między stronami hello i funkcje witryny. Ten program jest doskonały dla udzielenie odpowiedzi na pytania, takich jak:
* Jak użytkownicy opuścić stronę w witrynie?
* Co użytkownicy kliknij na stronie w witrynie?
* Gdzie są hello umieszcza czy użytkownicy churn — najbardziej z witryny?
* Czy istnieją miejsca, w którym użytkownicy powtarzania hello tę samą akcję samodzielnego?

narzędzia przepływu użytkownika Hello rozpoczyna się od widoku strony początkowej lub zdarzenie, które określisz. Tego widoku lub zdarzenie niestandardowe przepływy użytkownika pokazuje hello wyświetleń strony i niestandardowych zdarzeń wysłanych przez użytkowników natychmiast później podczas sesji, dwa kroki później, itd. Wiersze z różnymi grubość zawierają ile razy każda ścieżka użytego przez użytkowników. Specjalne węzły "Sesja została zakończona" Pokaż, ilu użytkowników wysyłane nie wyświetleń strony lub niestandardowych zdarzeń po hello poprzedzających węzła, wyróżnianie, gdzie użytkownicy prawdopodobnie pozostałych lokacji.



> [!NOTE]
> Zasób usługi Application Insights musi zawierać wyświetleń strony lub zdarzeń niestandardowych toouse hello przepływu użytkownika narzędzia. [Dowiedz się, jak tooset Twojego stronę toocollect aplikacji automatycznie widoków z hello zestaw SDK usługi Application Insights JavaScript](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Rozpocznij, wybierając pozycję Wyświetl stronę początkową lub zdarzenie niestandardowe

![Wybierz zdarzenie początkowej dla przepływu użytkownika](./media/app-insights-usage-flows/flows-initial-event.png)

tooget uruchomiona udzielenie odpowiedzi na pytania z narzędziem użytkownika przepływów hello wybierz widoku strony początkowej lub niestandardowe zdarzenie tooserve jako punkt początkowy dla wizualizacji hello hello:
1. Kliknij łącze hello w hello "co zrobić użytkownicy po...?" tytuł, lub kliknij przycisk Edytuj hello. 
2. Wybierz widok strony lub niestandardowe zdarzenie z listy rozwijanej "Event początkowego" hello.
3. Kliknij przycisk "Utwórz wykresu".

kolumny "Krok 1" Hello wizualizacji hello pokazuje, co użytkownicy czy najczęściej zaraz po początkowej zdarzeń hello, uporządkowanych góry do dołu z tooleast najczęściej. Hello "Krok 2" i pokazać kolejnych kolumn, co użytkownicy, czy tworzenie obrazu wszystkich użytkowników sposoby hello przejście do witryny.

Domyślnie hello przepływu użytkownika narzędzia losowo próbek hello tylko ostatnich 24 godzinach wyświetleń strony i niestandardowe zdarzenie z witryny. Można zwiększyć zakres czasu hello i zmienić saldo hello wydajności i dokładność losowych próbek w menu Edycja hello.

Jeśli hello strony widoków i zdarzeń niestandardowych nie są istotne tooyou, kliknij przycisk "X" hello na powitania węzły mają toohide. Po wybraniu hello węzły mają toohide, kliknij przycisk "Utwórz wykresu" hello poniżej hello wizualizacji. toosee wszystkie węzły hello zostały ukryte, kliknij przycisk Edytuj hello następnie znaleźć w sekcji "Wykluczone zdarzenia" hello.

Jeśli wyświetleń strony lub niestandardowych zdarzeń brakuje który spodziewana toosee wizualizacji hello:
* Sprawdź sekcję "Wykluczone zdarzenia" hello, w menu Edycja hello.
* Formant hello "Poziom szczegółowości" hello edycji menu tooinclude rzadziej zdarzeń w hello wizualizacji.
* Jeśli widok strony hello lub niestandardowe zdarzenie oczekiwane jest rzadko przez użytkowników, spróbuj wysłać zwiększa zakres czasu hello wizualizacji hello w menu Edycja hello.
* Upewnij się, że widok strony hello lub niestandardowe zdarzenie oczekiwane skonfigurowano toobe zebrane przez hello zestaw SDK usługi Application Insights w kodzie źródłowym hello witryny. [Dowiedz się więcej o zbieraniu niestandardowego zdarzenia.](app-insights-api-custom-events-metrics.md)

Jeśli chcesz toosee więcej czynności w wizualizacji hello, użyj hello "Liczba kroków" suwak w hello menu Edycja.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Po odwiedzeniu strony lub funkcji, użytkownicy gdzie i co użytkownik klika polecenie?

![Użyj toounderstand przepływu użytkownika, gdy użytkownik kliknie](./media/app-insights-usage-flows/flows-one-step.png)

Początkowa zdarzenie w przypadku widoku strony, hello pierwsza kolumna ("krok 1") wizualizacji hello to toounderstand szybkie, co użytkownicy czy natychmiast po odwiedzania strony hello. Spróbuj otworzyć witryny w następnej toohello okno wizualizacji przepływu użytkownika. Porównaj interakcji użytkowników z listy toohello strony hello zdarzeń w kolumnie "Krok 1" hello Twoje oczekiwania. Często elementu interfejsu użytkownika na stronie hello, który wydaje się nieważny tooyour zespołu można między hello najczęściej używanych na stronie powitania. Można go doskonały punkt początkowy projektowania ulepszenia tooyour lokacji.

Początkowej zdarzenie w przypadku niestandardowych zdarzeń, hello pierwsza kolumna zawiera użytkowników czy tylko po wykonaniu tej akcji. Podobnie jak w przypadku wyświetleń strony, należy wziąć pod uwagę Jeśli hello obserwowanych zachowania użytkowników zgodny oczekiwań i celów Twojego zespołu. Jeśli wybrane zdarzenie początkowej "Added elementu tooShopping koszyka", na przykład, Szukaj toosee Jeśli "Przejdź tooCheckout" i "Ukończone zakupu" są wyświetlane w krótkim czasie hello wizualizacji. Jeśli zachowania użytkownika znacznie różni się od Twoich oczekiwań, użyj toounderstand wizualizacji hello jak użytkownicy są pobierania "spowodowane" bieżący projekt witryny sieci.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Gdzie są hello umieszcza czy użytkownicy churn — najbardziej z witryny?

Obserwowanie "Sesja została zakończona" węzły wyświetlane wysokiej w górę w kolumnie wizualizacji hello, szczególnie w strumieniu. Oznacza to, w przypadku wielu użytkowników, prawdopodobnie churned z witryny po następujące hello powyższa ścieżka stron i interakcje interfejsu użytkownika. Czasami przenoszenie oczekiwano — po zakończeniu zakupu w witrynie handlu elektronicznego, na przykład -, ale zazwyczaj zmian jest znak problemy związane z projektem, niska wydajność lub inne problemy z witryny można zwiększyć.

Należy pamiętać, że "sesja została zakończona" węzły są oparte tylko na dane telemetryczne zebrane przez ten zasób usługi Application Insights. Jeśli usługi Application Insights nie odbiera dane telemetryczne dla niektórych interakcji użytkownika, użytkownicy nadal może mieć interakcji z witryny w sposób, po hello przepływu użytkownika narzędzia mówi hello sesja została zakończona.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Czy istnieją miejsca, w którym użytkownicy powtarzania hello tę samą akcję samodzielnego?

Poszukaj widok strony lub niestandardowe zdarzenie powtarzające się w kolejnych krokach wizualizacji hello przez wielu użytkowników. Zwykle oznacza to, że użytkownicy wykonują powtarzających się czynności w witrynie. Jeśli znajdziesz powtarzania pomyśleć o zmianę hello projekt witryny lub dodanie nowych funkcji tooreduce powtarzania. Jeśli znajdziesz użytkowników wykonywania powtarzających się czynności w każdym wierszu elementu tabeli, na przykład dodać funkcje edycji zbiorczej.

## <a name="common-questions"></a>Często zadawane pytania

### <a name="why-do-steps-appear-disconnected"></a>Dlaczego kroki są wyświetlane bez połączenia?

![Użytkownik przepływów mających odłączonego kroki](./media/app-insights-usage-flows/flows-disconnected.png)

Odłączeniu czynności (kolumn) w wizualizacji przepływu użytkownika, oznacza to, że żaden ścieżek hello wykonywaną przez użytkowników między krokami hello nie był wystarczająco często toobe pokazano. tooshow mniej częste zdarzenia na powitania wizualizacji kroki hello wyświetlane połączenie, suwak hello "Poziom szczegółowości" w menu Edycja hello.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Hello początkowej zdarzeń reprezentują hello pierwszego czasu hello zdarzenia pojawi się w sesji lub dowolnym momencie, w jakiej występuje w sesji?

Zdarzenie początkowej Hello na powitania wizualizacji reprezentuje tylko hello po raz pierwszy użytkownik wysłany tego widoku strony lub niestandardowe zdarzenie podczas sesji. Jeśli użytkownicy mogą wysyłać zdarzenia początkowej hello wiele razy w sesji, a następnie kolumny "Krok 1" hello wyświetlane są tylko zachowanie użytkowników po hello *pierwszy* wystąpienie zdarzenia początkowej, nie wszystkie wystąpienia.

## <a name="next-steps"></a>Następne kroki

* [Przegląd wykorzystania](app-insights-usage-overview.md)
* [Użytkownikami, sesjami i zdarzenia](app-insights-usage-segmentation.md)
* [Przechowywanie](app-insights-usage-retention.md)
* [Dodawanie zdarzeń niestandardowych tooyour aplikacji](app-insights-api-custom-events-metrics.md)
