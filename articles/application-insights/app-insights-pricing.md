---
title: "cennik i danych woluminu aaaManage dla usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zarządzanie woluminami dane telemetryczne i monitorować kosztów w usłudze Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Zarządzanie wolumin ceny i danych w usłudze Application Insights


Cennik [Azure Application Insights] [ start] opiera się na ilość danych na aplikację. Niskie obciążenie podczas tworzenia lub dla małych aplikacji jest bezpłatne, prawdopodobnie toobe, ponieważ dodatek miesięczne 1 GB, danych telemetrycznych.

Każdy zasób usługi Application Insights jest rozliczany jako osobne usługi i wspiera toohello rachunek za tooAzure Twojej subskrypcji.

Istnieją dwa planów cenowych. plan domyślny Hello jest nazywany Basic. Można włączyć dla hello Enterprise planu, który ma codzienne opłat, ale umożliwia pewnych dodatkowych funkcji, takich jak [Eksport ciągły](app-insights-export-telemetry.md).

Jeśli masz pytania dotyczące sposobu działania ceny dla usługi Application Insights, możesz wolnego toopost zapytania w naszym [forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>plany cen Hello

Zobacz hello [cennikiem usługi Application Insights] [ pricing] dla bieżącego cen w walucie.

### <a name="basic-plan"></a>Podstawowy plan

Podstawowy plan Hello jest domyślne powitania po utworzeniu nowego zasobu usługi Application Insights i jest wystarczające dla większości klientów.

* W planie Basic hello, naliczane są opłaty za ilość danych: liczba bajtów odebranych przez usługę Application Insights telemetrii. Ilość danych jest mierzony jako hello rozmiar pakietu danych JSON hello nieskompresowane odebranych przez usługę Application Insights z aplikacji.
Dla [zaimportowane do analizy danych tabelarycznych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), ilość danych hello jest mierzony jako hello rozmiar nieskompresowanych plików wysłane tooApplication szczegółowych informacji.  
* Pierwszy 1 GB dla każdej aplikacji jest bezpłatne, więc tylko eksperymentowanie lub tworzenie, jest mało prawdopodobne toohave toopay.
* [Metryki strumień na żywo](app-insights-live-stream.md) danych nie są one uwzględniane dla celów cennik.
* [Eksport ciągły](app-insights-export-telemetry.md) jest dostępna za GB dodatkowe obciążenie w planie Basic hello.

### <a name="enterprise-plan"></a>Enterprise plan

* W planie Enterprise hello może używać aplikacja hello wszystkich funkcji usługi Application Insights. [Eksport ciągły](app-insights-export-telemetry.md) i 

[Łącznik analizy dziennika](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) w hello Enterprise plan są dostępne bez żadnych dodatkowych opłat.
* Płaci się na węzeł, który wysyła dane telemetryczne dla wszystkich aplikacji w hello Enterprise plan. 
 * A *węzła* jest maszyną serwerze fizycznym lub wirtualnym lub platforma jako usługa wystąpienia roli, który jest hostem aplikacji.
 * Programowanie maszyny, przeglądarki klienta i urządzeń przenośnych nie są liczone jako węzły.
 * Jeśli aplikacja ma kilka składników, które wysyłają dane telemetryczne, takie jak usługi sieci web i zaplecza pracownika, zostały uwzględnione oddzielnie.
 * [Metryki strumień na żywo](app-insights-live-stream.md) danych nie są one uwzględniane dla cennik purposes.* w ramach subskrypcji, są widoczne obciążenia na węzeł nie każdej aplikacji. Jeśli masz pięć węzłów wysyłania danych telemetrycznych dla 12 aplikacji, a następnie hello naliczają opłaty jest pięć węzłów.
* Chociaż opłaty są podane na miesiąc, są pobierane tylko w przypadku dowolnego godzinę, w którym węzeł wysyła dane telemetryczne z aplikacji. Hello co godzinę opłata jest hello cudzysłowach miesięcznych opłat / 744 (liczba godzin w miesiącu dzień 31 hello).
* Dla każdego węzła wykrył (z godzinowe) znajduje się alokację wolumin danych 200 MB na dzień. Alokacja nieużywanych danych nie jest przenoszona z jednego dnia toohello dalej.
 * Jeśli wybierzesz hello opcja cenową przedsiębiorstwa, każda subskrypcja otrzymuje dziennych dodatków danych na podstawie hello liczby węzłów wysyłania danych telemetrycznych toohello zasobów usługi Application Insights w tej subskrypcji. Dlatego jeśli masz 5 węzłów wysyłanie danych cały dzień, trzeba puli dodatku zasobów usługi Application Insights hello tooall 1 GB zastosowane w danej subskrypcji. Nie ma znaczenia, jeśli niektóre węzły są Wysyłanie więcej danych niż inne węzły ponieważ hello uwzględnionych danych jest współużytkowana przez wszystkie węzły. Jeśli w danym dniu, zasobów usługi Application Insights hello otrzymywać więcej danych niż jest uwzględniona w hello dzienne dane alokacji dla tej subskrypcji, hello na GB danych nadwyżkowe opłaty. 
 * Witaj dzienne dane dodatku jest obliczany jako hello liczbę godzin w hello dnia (UTC) czy każdy węzeł wysyła dane telemetryczne podzielona przez 24 godziny 200 MB. Zatem jeśli masz 4 węzły wysyłanie danych telemetrycznych w trakcie 15 hello 24 godzin, w ciągu dnia hello hello danych dla tego dnia będzie ((4 x 15) / 24) x 200 MB = 500 MB. Cenie hello 2.30 USD na GB dla danych nadwyżkowe hello opłata za będzie 1,15 USD węzłów hello wysłania 1 GB danych tego dnia.
 * Należy pamiętać, hello Enterprise plan codzienne dodatku nie jest udostępniana z aplikacjami, dla których wybrano opcję podstawowe hello i nieużywanych dodatku nie jest przenoszona z typowymi. 
* Oto kilka przykładów ustalania liczby unikatowych węzła:
| Scenariusz                               | Łączna liczba węzłów dziennie |
|:---------------------------------------|:----------------:|
| 1 aplikacja używa 3 wystąpienia usługi Azure App Service i 1 serwera wirtualnego | 4 |
| 3 aplikacje na 2 maszyny wirtualne i zasobów usługi Application Insights hello te aplikacje są w hello tej samej subskrypcji i w hello Enterprise plan | 2 | 
| 4 aplikacji, którego zasoby aplikacji szczegółowe informacje znajdują się w hello tej samej subskrypcji. Każda aplikacja działa 2 wystąpienia 16 poza godzinami szczytu i wystąpień 4, 8 godzinach szczytu. | 13.33 | 
| Usługi w chmurze z rolą proces roboczy 1 i 1 roli sieci Web, każdy uruchomiony 2 wystąpienia | 4 | 
| Klastra sieci szkieletowej usług węzła 5 usługą 50 micro-services każdego micro-uruchomionych wystąpień 3 | 5|

* zachowanie zliczania dokładne węzła Hello zależy od tego, na którym jest przy użyciu zestawu SDK usługi Application Insights aplikacji. 
  * Zestaw SDK w wersji 2.2 i i jego nowszych wersjach, hello zarówno usługi Application Insights [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) lub [zestawu SDK sieci Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) będzie zgłaszać każdy host aplikacji jako węzeł, na przykład Witaj nazwę komputera dla serwera fizycznego i hosty maszyn wirtualnych lub hello Nazwa wystąpienia w przypadku hello usługi w chmurze.  Witaj wyjątku jest aplikacji tylko przy użyciu tylko [.NET Core](https://dotnet.github.io/) i hello aplikacji Insights Core SDK, w których wielkość tylko jeden węzeł będą zgłaszane dla wszystkich hostów hello nazwa hosta nie jest dostępna. 
  * We wcześniejszych wersjach hello SDK hello [zestawu SDK sieci Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) będą zachowywać się tak samo, jak hello nowsze wersje zestawu SDK, jednak hello [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) będzie zgłaszać tylko jeden węzeł bez uwzględniania hello hostów rzeczywistej aplikacji. 
  * Należy pamiętać, że jeśli aplikacja używa hello SDK tooset roleInstance tooa niestandardowej wartości, domyślnie tej samej wartości używane toodetermine hello liczba węzłów. 
  * Jeśli używasz nowej wersji zestawu SDK w aplikacji, która jest uruchamiany z urządzeń przenośnych i komputerów klienckich, istnieje możliwość, że hello liczba węzłów może zwracać numer, który jest bardzo duże (od hello dużą liczbę urządzeń przenośnych i komputerów klienckich). 

### <a name="multi-step-web-tests"></a>Wieloetapowe testy sieci Web

Brak dodatkowych opłat dla [testy sieci web wieloetapowych](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Odnosi się tooweb testy, które wykonują sekwencję akcji. 

Jest bezpłatna oddzielne "testów ping" jednej strony. Dane telemetryczne z testów ping i testy wieloetapowych jest pobierana oraz inne dane telemetryczne z aplikacji.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Operations Management Suite subskrypcji uprawnień

Jako [zapowiedziała niedawno](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), klientów, którzy kupili E1 programu Microsoft Operations Management Suite i E2 są możliwe tooget Application Insights przedsiębiorstwa jako dodatkowy składnik bez ponoszenia dodatkowych kosztów. W szczególności każdej jednostki E1 Operations Management Suite i E2 zawiera węzeł too1 uprawnienie hello Enterprise planu usługi Application Insights. Jak wspomniano powyżej, każdy węzeł usługi Application Insights zawiera too200 MB danych pozyskanych dziennie (niezależnie od wprowadzanie danych analizy dzienników), z przechowywaniem danych 90-dniowy bez ponoszenia dodatkowych kosztów. 

> [!NOTE]
> tooensure uzyskanie to uprawnienie, musisz mieć zasobów usługi Application Insights w przedsiębiorstwie hello cenową planu. To uprawnienie dotyczy tylko jako węzły, więc zasobów usługi Application Insights w planie Basic hello nie będzie zrealizować żadnych korzyści. Należy pamiętać, że tych uprawnień nie będą widoczne na powitania szacowane koszty widoczne w funkcji hello + cennik bloku. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Przejrzyj planów cenowych i Szacowanie kosztów

Applicaition Insights ułatwia hello toounderstand łatwo dostępnych planów cenowych i jakie hello koszty są prawdopodobnie być oparte na ostatnie wzorców użycia. Start przez otwarcie hello **funkcje + cennik** bloku w hello zasobu usługi Application Insights w hello portalu Azure:

![Wybierz cennik.](./media/app-insights-pricing/01-pricing.png)

**a.** Przejrzyj woluminu danych na powitania miesiąc. Dotyczy to wszystkich danych hello odebrał i przechowywane (po jednej [próbkowania](app-insights-sampling.md) z serwera i klienta, aplikacji oraz z testów dostępności.

**b.** Wykonywane oddzielne opłat [testy sieci web wieloetapowych](app-insights-monitor-web-app-availability.md#multi-step-web-tests). (Ta nie obejmuje testów dostępności proste, zawarte w hello danych woluminu bezpłatnie).

**c.** Włącz hello Enterprise plan.

**d.** Kliknij go, toodata zarządzania opcje tooview ilość danych hello ostatniego miesiąca, ustawić dzienny limit albo ustaw wprowadzanie próbkowania.

Application Insights opłaty są dodawane tooyour rachunku Azure. Można wyświetlić szczegóły Azure naliczać opłaty na powitania sekcji rozliczeń hello portalu Azure lub w hello [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![W menu po stronie powitania wybierz rozliczeń.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Szybkość danych
Istnieją trzy sposoby, w których hello jest ograniczona woluminu w przypadku wysłania danych:

* **Próbkowanie:** mechanizm ten może służyć skrócić hello danych telemetrycznych wysłanych z klienta i serwera aplikacji, z minimalnym zakłócenia metryki. To jest podstawowym narzędziem hello tootune hello ilość danych. Dowiedz się więcej o [próbkowania funkcji](app-insights-sampling.md). 
* **Dzienny limit:** podczas tworzenia zasobu usługi Application Insights z hello Azure portal to ustawiono too500 GB/dzień. Witaj domyślne podczas tworzenia zasobu usługi Application Insights z programu Visual Studio, to mały (tylko 32,3 MB na dzień), który jest przeznaczony tylko toofaciliate testowania. W takim przypadku zamierza się, że użytkownik hello zgłosi hello codzienne centralnych zasad dostępu przed wdrożeniem aplikacji hello w środowisku produkcyjnym. maksymalny limit Hello jest 500 GB/dzień, chyba, że zażądano maksymalną wyższą dla aplikacji dużego natężenia ruchu sieciowego. Zachować ostrożność podczas ustawiania hello dzienny limit, zgodnie z celem powinno być **nigdy nie toohit hello dzienny limit**, ponieważ spowoduje utratę danych pozostałej hello hello dnia i można toomonitor aplikacji. toochange, on, użyj hello codzienne woluminu zakończenia bloku połączone z hello bloku Zarządzanie woluminami danych (zobacz poniżej). Należy zauważyć, że niektóre typy subskrypcji środki, nie może zostać użyty dla usługi Application Insights. Jeśli subskrypcja hello ma wydatków ograniczyć, hello codziennie zakończenia bloku będzie mieć instrukcje jak tooremove go i Włącz hello codzienne toobe zakończenia wywoływane poza 32,3 MB/dzień.  
* **Ograniczanie:** tego ograniczenia hello danych szybkość too32 k zdarzeń na sekundę, średnio ponad 1 minutę. 


*Co się stanie, jeśli Moja aplikacja przekracza hello szybkości?*

* Witaj ilość danych aplikacji wysyłanych przez jest oceniane co minutę. W przypadku przekroczenia hello na sekundę szybkość uśrednionej za minutę hello, hello serwer odmawia niektórych żądań. Hello SDK buforów danych hello i próbuje tooresend rozkładanie skoków w ciągu kilku minut. Jeśli aplikacja stale wysyła dane w powyżej hello szybkości, niektóre dane zostaną usunięte. (hello ASP.NET, Java i JavaScript SDK spróbuj tooresend w ten sposób; innych zestawów SDK może po prostu Usuń ograniczenie danych). W przypadku ograniczania przepustowości, zostanie wyświetlone powiadomienie ostrzeżenie, że miało to miejsce.

*Jak sprawdzić, jak dużo danych wysyła mojej aplikacji?*

* Otwórz hello **Zarządzanie woluminami danych** bloku toosee hello codziennych danych woluminu wykresu. 
* W Eksploratorze metryk, Dodaj nowy wykres i wybierz **ilość punktów danych** jako jego metryki. Przełącz na grupowanie i Grupuj według **— typ danych**.

## <a name="tooreduce-your-data-rate"></a>tooreduce szybkość danych
Poniżej przedstawiono niektóre czynności, które można wykonać tooreduce woluminu danych:

* Użyj [próbkowania](app-insights-sampling.md). Ta technologia zmniejsza szybkość danych bez pochylanie Twoje metryki i bez zakłócania toonavigate możliwości hello między elementów pokrewnych wyszukiwania. W aplikacjach server działa automatycznie.
* [Ogranicz liczbę hello wywołania Ajax, które mogą być zgłaszane](app-insights-javascript.md#detailed-configuration) w każdy widok strony, albo Przełącz funkcję Raportowanie Ajax.
* Wyłącz niepotrzebne przez moduły kolekcji [ApplicationInsights.config edycji](app-insights-configuration-with-applicationinsights-config.md). Na przykład można zdecydować, że liczniki wydajności lub dane zależności są inessential.
* Podziel klucze Instrumentacji tooseparate telemetrii. 
* Metryki wstępnie agregacji. Jeśli tooTrackMetric wywołania zostało umieszczone w aplikacji, można zmniejszyć ruch przy użyciu hello przeciążenia, które akceptuje obliczenia średniej hello i odchylenie standardowe partii pomiarów. Możesz też użyć [wstępnie agregację pakietu](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Zarządzanie woluminem danych codzienne maksymalną hello

Można używać hello codzienne woluminu zakończenia toolimit hello dane zebrane, ale spełnieniu zakończenia hello spowoduje utratę wszystkich telemetery wysyłanych z aplikacji hello pozostałej hello dnia. Jest **nie zaleca się** toohave Twojej aplikacji toohit hello codzienne zakończenia od możesz są tootrack hello kondycji i wydajności aplikacji po jej zostaje trafiony. 

Zamiast tego należy użyć [próbkowania](app-insights-sampling.md) tootune hello woluminu toohello poziom danych chcesz i użyj hello dzienny limit jedynie w ostateczności"", w przypadku aplikacji, który rozpoczyna się nieoczekiwanie wysyłania znacznie wyższa woluminów telemetery. 

Kliknij toochange hello codzienne centralnych zasad dostępu, w sekcji konfiguracji zasobu Insihgts aplikacji hello **Zarządzanie woluminami danych** następnie **dzienny limit**.

![Dostosowywanie hello dzienne dane telemetryczne woluminu centralnych zasad dostępu](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>Próbkowanie
[Próbkowanie](app-insights-sampling.md) jest metoda zmniejszenie hello szybkość telemetrii jest tooyour aplikacji, podczas zachowaniu toofind możliwości hello zdarzenia związane z podczas wyszukiwania diagnostycznych i nadal z zachowaniem poprawne zdarzenie zlicza. 

Próbkowanie to efektywny sposób tooreduce opłat i pozostać w wykorzystaniu całego przydziału miesięcznego. Hello algorytm próbkowania zachowuje pozycje powiązane dane telemetryczne, tak aby na przykład podczas wyszukiwania, można znaleźć hello powiązana tooa określonego wyjątku. Algorytm Hello zachowuje poprawne liczby, aby zobaczyć hello poprawne wartości w Eksploratorze metrykę dla żądań, wyjątków stawki i inne liczby.

Istnieje kilka metod pobierania próbek.

* [Próbkowanie adaptacyjną](app-insights-sampling.md) jest domyślną hello hello zestaw SDK platformy ASP.NET, który automatycznie dostosowuje toohello ilość danych telemetrycznych, wysyłanej przez aplikację. Działa ona automatycznie w hello zestawu SDK w aplikacji sieci web, dzięki czemu hello telemetrii ruchu w sieci hello jest zmniejszany. 
* *Wprowadzanie próbkowania* stanowi alternatywę działa w momencie hello, gdzie dane telemetryczne z aplikacji wpływa hello usługa Application Insights. Nie ma wpływu na powitania ilość danych telemetrycznych wysłanych z aplikacji, ale zmniejsza woluminu hello przechowywane przez usługę hello. Można go przydziałów hello tooreduce wykorzystane przez dane telemetryczne z przeglądarki i innych zestawów SDK.

wprowadzanie tooset próbkowania, ustawić kontroli hello w bloku cennik hello:

![Hello przydziału i cenach bloku kliknij Kafelek przykłady hello i wybierz polecenie ułamek próbkowania.](./media/app-insights-pricing/04.png)

> [!WARNING]
> blok danych próbkowania Hello reguluje tylko wartości hello wprowadzanie próbkowania. Go nie odzwierciedlają hello częstotliwość próbkowania, która jest stosowana przez hello zestaw SDK usługi Application Insights w aplikacji. Jeśli przychodzące dane telemetryczne hello już uzyskane podczas próbkowania na powitania zestawu SDK, próbkowania wprowadzanie nie została zastosowana.
> 

rzeczywiste hello toodiscover próbkowania szybkość niezależnie od tego, gdzie ma zastosowane, użyj [Analytics query](app-insights-analytics.md) takich jak ta:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

W każdym zachowane rekordu, `itemCount` wskazuje liczbę hello oryginalnego rekordów, które reprezentuje on równy too1 + hello liczbę poprzednich odrzuconych rekordów. 


## <a name="automation"></a>Automatyzacja

Planu skryptu tooset hello cen można pisać przy użyciu zarządzania zasobami Azure. [Dowiedz się, jak](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Podsumowanie limity
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Następne kroki

* [Próbkowanie](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

