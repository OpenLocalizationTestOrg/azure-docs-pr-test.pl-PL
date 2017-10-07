---
title: "Analiza aaaUsage dla aplikacji sieci web za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Dowiedz się, użytkownicy i ich działania z aplikacji sieci web."
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Analiza użycia aplikacji sieci web za pomocą usługi Application Insights

Funkcje aplikacji sieci web są najbardziej popularnych? Czy użytkownicy osiągnąć cele związane z aplikacją? Czy one usunąć w szczególności, i zwracają później?  [Azure Application Insights](app-insights-overview.md) pomaga uzyskać zaawansowane wgląd w jaki sposób użytkownicy korzystają z aplikacji sieci web. Za każdym razem, gdy aktualizacji aplikacji, można ocenić, jak działa dla użytkowników. Z tym wiedzy możesz wprowadzić decyzje dotyczące Twojej dalej programistycznych opartych na danych.

## <a name="send-telemetry-from-your-app"></a>Wysłać dane telemetryczne z aplikacji

najlepsze środowisko Hello są uzyskiwane przez zainstalowanie usługi Application Insights, zarówno w kodzie serwera aplikacji, jak i na stronach sieci web. składniki klienta i serwera aplikacji Hello wysłać dane telemetryczne wstecz toohello portalu Azure do analizy.

1. **Kod serwera:** instalacji hello moduł odpowiednie dla Twojej [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), lub [innych](app-insights-platforms.md) aplikacji.

    * *Nie chcesz tooinstall kod serwera? Po prostu [tworzenie zasobów Azure Application Insights](app-insights-create-new-resource.md).*

2. **Kod strony sieci Web:** Otwórz hello [portalu Azure](https://portal.azure.com), otwórz hello zasobu usługi Application Insights dla aplikacji, a następnie **wprowadzenie > Monitorowanie i diagnozowanie po stronie klienta**. 

    ![Skopiuj skrypt hello do head hello głównej strony sieci web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Pobierz dane telemetryczne:** uruchomić projekt w trybie debugowania na kilka minut, a następnie sprawdź wyniki w bloku omówienie hello w usłudze Application Insights.

    Publikowanie z toomonitor aplikacji wydajność aplikacji i dowiedzieć się, co robią użytkownicy z aplikacją.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Uwzględnia Identyfikatora użytkownika i sesji w obrębie telemetrii
Użytkownicy tootrack wraz z upływem czasu, usługa Application Insights wymaga tooidentify sposób ich. Zdarzenia Hello jest narzędzie hello jedynym narzędziem użycia, które nie wymagają Identyfikatora użytkownika lub identyfikator sesji.

Rozpocznij wysyłanie tych identyfikatorów [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Eksploruj demograficznych użycia oraz statystyki
Dowiedz się, gdy użytkownicy korzystają z aplikacji, jakie stron one jest najbardziej zainteresowani, gdzie znajdują się użytkownicy, jakie przeglądarek i systemów operacyjnych korzystają. 

Raporty Hello użytkowników i sesji filtrować dane według stron lub zdarzeń niestandardowych i segmentację je przez właściwości, takie jak lokalizacja, środowiska i strony. Można także dodać własne filtry.

![Użytkownicy](./media/app-insights-usage-overview/users.png)  

Szczegółowe informacje na powitania prawym punktu interesujących wzorców w hello zestawu danych.  

* Witaj **użytkowników** raport liczby hello liczby unikatowych użytkowników, które uzyskują dostęp do stron w ramach Twojej wybranych okresów. (Użytkownicy są liczone przy użyciu plików cookie. Jeśli ktoś uzyskuje dostęp do witryny za pomocą różnych przeglądarkach lub komputerów klienckich, lub czyści ich plików cookie, a następnie będzie można zliczane więcej niż raz.)
* Witaj **sesji** raport zlicza hello sesje użytkowników, które uzyskują dostęp do witryny. Sesja jest okres aktywności przez użytkownika, został przerwany przez okres aktywności ponad pół godziny.

[Więcej informacji na temat narzędzia hello użytkownikami, sesjami i zdarzenia](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Liczba wyświetleń strony

W bloku użycia hello kliknij za pośrednictwem hello wyświetleń strony kafelka tooget podział najpopularniejszych stron:

![W bloku omówienie hello kliknij hello strony widoki wykresu](./media/app-insights-usage-overview/05-games.png)

w powyższym przykładzie Hello jest gry witryny sieci web. Z wykresów hello natychmiast widać:

* Użycie nie zwiększona hello zeszłym tygodniu. Może być powinniśmy pomyśleć o optymalizacji dla aparatów wyszukiwania?
* Tenisa jest najbardziej popularnym strona gier hello. Ta funkcja pozwala skupić się na dodatkowe ulepszenia toothis strony.
* Średnio użytkowników stronie powitania tenisa około trzy razy w tygodniu. (Istnieją sesje około trzy razy więcej niż użytkowników.)
* Większość użytkowników w witrynie hello hello USA pracy tygodniu i w godzinach pracy. Być może należy udostępniamy przycisk "szybkie Ukryj" na stronie sieci web hello.
* Witaj [adnotacje](app-insights-annotations.md) na wykresie hello Pokaż, gdy nowe wersje hello witryny sieci Web zostały wdrożone. Brak hello ostatnie wdrożeń ma zauważalnego wpływu na sposób użycia.

Co zrobić, jeśli chcesz tooinvestigate hello ruchu tooyour lokacji bardziej szczegółowo, takich jak dzielenie według właściwości niestandardowej, wysyłanych w jego dane telemetryczne wyświetleń strony witryny?

1. Otwórz hello **zdarzenia** narzędzia w menu zasobu usługi Application Insights hello. To narzędzie umożliwia analizowanie, ile strony widoków i zdarzeń niestandardowych, które zostały wysłane z aplikacji, w oparciu o różne opcje filtrowania, cohorting i segmentacji.
2. W hello "Kto używane" z listy rozwijanej wybierz "Dowolny widok strony".
3. W polu listy rozwijanej "Podziału przez" hello wybierz właściwości, według których toosplit ze strony wyświetlić dane telemetryczne.

## <a name="retention---how-many-users-come-back"></a>Przechowywania - wróć ilu użytkowników?

Przechowywania pomaga zrozumieć, jak często użytkownicy zwracać toouse aplikacji w oparciu stado użytkowników, którzy wykonać akcję biznesowych w przedziale czasu. 

- Zrozumienie, jakie określone funkcje, że użytkownicy wstecz toocome więcej niż inne 
- Na podstawie danych użytkownika rzeczywistych hipotez formularza 
- Określić, czy przechowywania jest problem w programie 

![Przechowywanie](./media/app-insights-usage-overview/retention.png) 

Formanty przechowywania Hello na górze umożliwiają, możesz toodefine określonych zdarzeń i przechowywania toocalculate zakresu czasu. Witaj wykresu w środku hello daje wizualną reprezentację hello ogólną procent przechowywania hello zakres czasu. Wykres Hello na dole hello reprezentuje indywidualne przechowywania w danym okresie. Taki poziom szczegółowości pozwala toounderstand, jakie użytkownicy wirtualni i co może mieć wpływ na użytkowników zwracająca na bardziej szczegółowy poziom szczegółowości.  

[Więcej informacji na temat narzędzia przechowywania hello](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Zdarzenia niestandardowe biznesowe

tooget przejrzysty co użytkownicy nie z aplikacji sieci web, jest przydatne tooinsert wierszy kodu toolog niestandardowych zdarzeń. Zdarzenia te można śledzić żadnych czynności użytkownika szczegółowe akcje, takie jak kliknięcie określonego przycisków, toomore firma zdarzenia, takie jak dokonywania zakupu lub zastosowanie gier. 

Chociaż w niektórych przypadkach wyświetleń strony może reprezentować przydatne zdarzeń, nie jest PRAWDA ogólnie. Użytkownik może otworzyć stronę produktu bez kupowanie hello produktu. 

Zdarzenia firmy można wykresu postępu użytkowników za pośrednictwem witryny. Można sprawdzić ich preferencje dotyczące różnych opcjach i gdzie one usunąć out lub ma trudności. Z tej wiedzy można podejmowania świadomych decyzji o hello priorytetów w rozwoju listę prac.

Na stronie sieci web hello mogą być rejestrowane zdarzenia:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Lub po stronie serwera na powitania hello aplikacji sieci web:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Zdarzenia toothese wartości właściwości, można dołączyć, aby mogą filtrować lub podziału hello zdarzeń inspekcji w portalu hello. Ponadto standardowy zestaw właściwości jest dołączone tooeach zdarzeń, takich jak identyfikator użytkownika anonimowego, co pozwala tootrace hello sekwencji działań użytkownika.

Dowiedz się więcej o [zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md#trackevent) i [właściwości](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Zdarzenia metod selekcji i projekcji

W narzędziach użytkownikami, sesjami i zdarzenia hello użytkownik może kątami zdarzeń niestandardowych przez użytkownika, nazwę zdarzenia i właściwości.
![Użytkownicy](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Dane telemetryczne hello projekt aplikacji hello

Podczas projektowania każdej funkcji aplikacji, należy wziąć pod uwagę, jak ma toomeasure jego powodzenia z użytkownikami. Zdecyduj, zdarzenia biznesowe muszą toorecord, a kodem hello śledzenia wywołań dla tych zdarzeń w aplikacji z hello start.

## <a name="a--b-testing"></a>A | Testowanie B
Jeśli nie wiesz, który wariant funkcji więcej powiedzie się, zwolnij ich wprowadzania poszczególnych użytkowników toodifferent dostępny. Mierzony sukces hello każdego z nich, a następnie przesuń tooa ujednoliconego wersji.

Dla tej metody można dołączyć właściwości różne wartości tooall hello telemetrii, wysyłany przez poszczególnych wersji aplikacji. Możesz to zrobić przez definiowanie właściwości w hello active TelemetryContext. Te właściwości domyślne są dodawane wysyła tooevery telemetrii wiadomość hello aplikacji — nie tylko z niestandardowych wiadomości, ale hello także standardowe telemetrii.

W portalu usługi Application Insights hello filtrowania i podziału danych w wartości właściwości hello, tak jak toocompare hello różne wersje.

toodo, [Konfigurowanie inicjatora telemetrii](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

W inicjatorze aplikacji sieci web hello takich jak Global.asax.cs:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

Wszystkie nowe TelemetryClients automatycznie dodają hello wartości właściwości, które określisz. Zdarzenia telemetrii poszczególnych można zastąpić wartości domyślne hello.

## <a name="next-steps"></a>Następne kroki
   - [Użytkownicy, sesje, zdarzenia](app-insights-usage-segmentation.md)
   - [Lejki](usage-funnels.md)
   - [Przechowywanie](app-insights-usage-retention.md)
   - [User Flows (Przepływy użytkowników)](app-insights-usage-flows.md)
   - [Skoroszyty](app-insights-usage-workbooks.md)
   - [Dodaj kontekstu użytkownika](app-insights-usage-send-user-context.md)
