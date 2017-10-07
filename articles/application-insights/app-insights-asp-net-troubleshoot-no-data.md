---
title: "aaaTroubleshooting żadne dane — usługi Application Insights dla platformy .NET"
description: "Nie można wyświetlać dane w usłudze Azure Application Insights? Spróbuj w tym miejscu."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Rozwiązywanie problemów z brakiem danych — usługa Application Insights dla platformy .NET
## <a name="some-of-my-telemetry-is-missing"></a>Brakuje części Moje telemetrii
*W usłudze Application Insights I zobaczyć tylko część hello zdarzenia, które są generowane przez Moja aplikacja.*

* Jeśli widzisz spójnie hello sam ułamek, tooadaptive prawdopodobnie z powodu jego [próbkowania](app-insights-sampling.md). tooconfirm, otwórz wyszukiwania (za pomocą bloku omówienie hello) i przyjrzyj się wystąpienia na żądanie lub inne zdarzenia. U dołu hello hello sekcja właściwości kliknij przycisk "..." tooget właściwości pełne szczegóły. Jeśli żądanie Count > 1, a następnie jest używany w operacji pobierania próbek. 
* W przeciwnym razie jest to możliwe, że w przypadku naciśnięcie [limit szybkości danych](app-insights-pricing.md#limits-summary) dla Twojego planu cenowego. Ograniczenia te są stosowane na minutę.

## <a name="no-data-from-my-server"></a>Żadne dane z serwerem
*Moja aplikacja został zainstalowany na serwerze sieci web, a nie widzisz wszystkie dane telemetryczne z niego. Na komputerze deweloperów Ci poszło OK.*

* Prawdopodobnie problem zapory. [Ustaw wyjątki zapory dla usługi Application Insights toosend danych](app-insights-ip-addresses.md).

*I [zainstalowany Monitor stanu](app-insights-monitor-performance-live-website-now.md) mojej aplikacji sieci web serwera toomonitor istniejących. Nie ma żadnych wyników.*

* Zobacz [Rozwiązywanie problemów z Monitora stanu](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Brak opcji "Dodaj usługę Application Insights" w programie Visual Studio
*Gdy I kliknij prawym przyciskiem myszy istniejący projekt w Eksploratorze rozwiązań, nie ma żadnych opcji usługi Application Insights.*

* Nie wszystkie typy .NET projektu są obsługiwane przez narzędzia hello. Projekty sieci Web i WCF są obsługiwane. Dla innych typów projektów, takich jak aplikacje pulpitu lub usługi, nadal możesz [ręcznie dodać projekt tooyour zestaw SDK usługi Application Insights](app-insights-windows-desktop.md).
* Upewnij się, że masz [programu Visual Studio 2013 Update 3 lub nowszym](http://go.microsoft.com/fwlink/?LinkId=397827). Pochodzi on wstępnie zainstalowane z narzędzia Developer Analytics, które zawierają hello zestaw SDK usługi Application Insights.
* Wybierz **narzędzia**, **rozszerzenia i aktualizacje** i sprawdź, czy **Developer Analytics Tools** jest zainstalowany i włączony. Jeśli tak, kliknij przycisk **aktualizacje** toosee, jeśli dostępna jest aktualizacja.
* Otwórz okno dialogowe Nowy projekt hello i wybierz aplikację sieci Web programu ASP.NET. Jeśli widzisz hello usługi Application Insights opcję Brak, a następnie hello narzędzia są zainstalowane. Jeśli nie, spróbuj odinstalować i ponowne zainstalowanie hello Application Insights Tools.

## <a name="q02"></a>Dodawanie usługi Application Insights nie powiodło się
*Przy próbie tooadd usługi Application Insights tooan istniejący projekt I wyświetlony komunikat o błędzie.*

Prawdopodobne przyczyny:

* Komunikacja z portalem usługi Application Insights hello nie powiodła się; lub
* Istnieje problem z Twoim kontem platformy Azure;
* Masz tylko [dostęp do odczytu toohello subskrypcji lub grupy, w którym chcesz toocreate hello nowy zasób](app-insights-resources-roles-access-control.md).

Poprawka:

* Sprawdź podane poświadczenia logowania dla prawej hello konto platformy Azure. 
* W przeglądarce, sprawdź, czy masz dostęp do toohello [portalu Azure](https://portal.azure.com). Otwórz ustawienia i czy ma żadnych ograniczeń.
* [Dodaj usługę Application Insights tooyour istniejący projekt](app-insights-asp-net.md): W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie "Dodaj usługę Application Insights".
* Jeśli nadal nie działa, wykonaj hello [procedury ręcznego](app-insights-windows-services.md) tooadd zasobów w portalu hello, a następnie dodaj hello SDK tooyour projektu. 

## <a name="emptykey"></a>Otrzymuję komunikat o błędzie "klucza Instrumentacji nie może być pusta"
Prawdopodobnie wystąpił problem podczas zostały instalacji usługi Application Insights lub być może adapter rejestrowania.

W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **usługi Application Insights > Konfiguruj usługę Application Insights**. Otrzymasz okna dialogowego, które można zaprasza toosign w tooAzure i Utwórz zasobu usługi Application Insights lub ponownego użycia istniejącej.

## <a name="NuGetBuild"></a>"Pakietów NuGet brakuje" na serwerze kompilacji
*Wszystko, co tworzy OK I czy debugowanie na moim komputerze programowanie, ale pojawia się błąd NuGet na powitania serwera kompilacji.*

Zobacz [przywracania pakietów NuGet](http://docs.nuget.org/Consume/Package-Restore) i [automatyczne przywracanie pakietów](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Brak tooopen polecenia menu usługi Application Insights z programu Visual Studio
*I kliknij prawym przyciskiem myszy mój projekt w Eksploratorze rozwiązań, nie ma żadnych poleceń usługi Application Insights, lub nie widzę polecenia Otwórz usługę Application Insights.*

Prawdopodobne przyczyny:

* Jeśli ręcznie utworzyć zasobu usługi Application Insights hello lub projekt hello jest typu, który nie jest obsługiwany przez narzędzia Application Insights hello.
* narzędzia Developer Analytics Hello są wyłączone w Visual Studio. 
* Visual Studio jest starsza niż 2013 Update 3.

Poprawka:

* Upewnij się, że używanej wersji programu Visual Studio 2013 z aktualizacją 3 lub nowszym.
* Wybierz **narzędzia**, **rozszerzenia i aktualizacje** i sprawdź, czy **Developer Analytics tools** jest zainstalowany i włączony. Jeśli tak, kliknij przycisk **aktualizacje** toosee, jeśli dostępna jest aktualizacja.
* Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań. Jeśli widzisz polecenia hello **usługi Application Insights > Konfiguruj usługę Application Insights**, użyj jej tooconnect zasobu toohello projektu w hello usługa Application Insights.

W przeciwnym razie wartość danego typu projektu bezpośrednio nie jest obsługiwane przez narzędzia Application Insights hello. toosee telemetrii, logowanie toohello [portalu Azure](https://portal.azure.com), wybierz usługę Application Insights na pasku nawigacyjnym po lewej stronie powitania i wybierz aplikację.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>"Odmowa dostępu" Otwieranie usługi Application Insights z programu Visual Studio
*polecenia menu "Otwieranie usługi Application Insights" Hello przejście toohello portalu Azure, ale występuje błąd "odmowa dostępu".*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Witaj logowania firmy Microsoft ostatnio używana w domyślnej przeglądarce nie ma dostępu zbyt[zasobu, który został utworzony podczas dodawania usługi Application Insights toothis aplikacji hello](app-insights-asp-net.md). Istnieją dwie prawdopodobne przyczyny: 

* Masz więcej niż jedno konto Microsoft — może być służbowy i osobiste konto Microsoft? Witaj logowania ostatnio używana w domyślnej przeglądarce był przeznaczony dla innego konta niż Witaj, który ma dostęp do zbyt[dodać projektu usługi Application Insights toohello](app-insights-asp-net.md). 
  
  * Poprawka: Kliknij swoją nazwę na górnego prawego powitalne okno przeglądarki i Wyloguj. Następnie zaloguj się przy użyciu konta hello, który ma dostęp. Następnie na pasku nawigacyjnym po lewej stronie powitania kliknij usługi Application Insights i wybierz aplikację.
* Ktoś dodać usługi Application Insights toohello projektu, a ich nie pamiętasz toogive możesz [grupy zasobów toohello dostępu](app-insights-resources-roles-access-control.md) , w której został utworzony. 
  
  * Poprawka: Jeśli używane konto organizacyjne, mogą dodawać możesz zespołu toohello; lub mogą udzielać dostępu można indywidualnego dostępu toohello grupy zasobów.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>"Zasobów" nie można odnaleźć na otwarcie usługi Application Insights z programu Visual Studio
*polecenia menu "Otwieranie usługi Application Insights" Hello przejście toohello portalu Azure, ale występuje błąd "nie można odnaleźć zasobów".*

Prawdopodobne przyczyny:

* Usunięto zasób usługi Application Insights dla aplikacji Hello; lub
* Hello klucza Instrumentacji został ustawiony lub zmienione w ApplicationInsights.config edytując je bezpośrednio, bez aktualizowania hello pliku projektu. 

Witaj klucza Instrumentacji w formantach ApplicationInsights.config wysyłania danych telemetrycznych hello. Wiersz w pliku projektu hello kontrolki, którego zasobu jest otwarty, korzystając z polecenia hello w programie Visual Studio. 

Poprawka:

* W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz pozycję usługi Application Insights, Konfiguruj usługę Application Insights. W oknie dialogowym hello można wybrać istniejący zasób tooan telemetrii toosend lub Utwórz nową. Lub:
* Otwórz zasobów hello bezpośrednio. Zaloguj się za[hello portalu Azure](https://portal.azure.com)kliknij na pasku nawigacyjnym po lewej stronie powitania usługi Application Insights, a następnie wybierz aplikację.

## <a name="where-do-i-find-my-telemetry"></a>Gdzie znaleźć Moje telemetrii?
*Po podpisaniu w toohello [portalu Microsoft Azure](https://portal.azure.com), i wyświetlane hello Azure główny pulpit nawigacyjny. Dlatego gdzie można znaleźć dane usługi Application Insights?*

* Na pasku nawigacyjnym po lewej stronie powitania kliknij usługi Application Insights, następnie nazwę aplikacji. Jeśli masz żadnych projektów, należy za[dodać lub skonfigurować usługi Application Insights do projektu sieci web](app-insights-asp-net.md).
  
    Brak zobaczysz Niektóre wykresy podsumowania. Możesz kliknąć za ich pośrednictwem toosee więcej szczegółów.
* W programie Visual Studio podczas debugowania kodu aplikacji, kliknij przycisk Application Insights hello.

## <a name="q03"></a>Brak danych serwera (lub żadne dane na wszystkich)
*I Moja aplikacja uruchomiono, a potem hello usługa Application Insights w Microsoft Azure, ale wszystkie hello wykresy są widoczne "Dowiedz się jak toocollect..." lub "Nie skonfigurowano".* Lub, *tylko dane widoku strony i użytkownika, ale żadne dane z serwera.*

* Uruchom aplikację w trybie debugowania w programie Visual Studio (F5). Użyj aplikacji hello tak jako toogenerate niektóre telemetrii. Sprawdź, czy można przejrzeć zdarzenia rejestrowane w oknie danych wyjściowych programu Visual Studio hello. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Otwórz w portalu usługi Application Insights hello [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md). Dane zazwyczaj są wyświetlane tutaj najpierw.
* Kliknij przycisk Odśwież hello. Blok Hello odświeża sam okresowo, ale możesz także zrobić to ręcznie. Interwał odświeżania Hello jest dłużej większych przedziałów czasu.
* Sprawdź, czy klucze Instrumentacji hello pasują do siebie. W głównym bloku aplikacji w portalu usługi Application Insights hello w hello hello **Essentials** listy rozwijanej, obejrzyj **klucza Instrumentacji**. Następnie, w projekcie w programie Visual Studio Otwórz ApplicationInsights.config i Znajdź hello `<instrumentationkey>`. Sprawdź, czy dwa klucze hello są takie same. Jeśli nie:
  
  * W portalu powitania kliknij przycisk Application Insights i poszukaj zasób aplikacji hello kluczem prawo hello; lub
  * W Eksploratorze rozwiązań programu Visual Studio kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz pozycję usługi Application Insights, konfigurowanie. Resetuj hello aplikacji toosend telemetrii toohello prawo zasobów.
  * Jeśli nie możesz znaleźć hello zgodnymi kluczami, sprawdź, czy używane są takie same hello poświadczenia logowania w programie Visual Studio jak toohello portalu.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* W hello [główny pulpit nawigacyjny Microsoft Azure](https://portal.azure.com), przyjrzeć się hello mapy usługi kondycji. W przypadku niektórych alertów oznaczeń, poczekaj, aż one zwrócono tooOK, a następnie zamknij i otwórz ponownie z bloku aplikacji usługi Application Insights.
* Należy także sprawdzić [naszym blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).
* Czy pisania kodu dla hello [po stronie serwera SDK](app-insights-api-custom-events-metrics.md) które może zmieniać hello klucza Instrumentacji w `TelemetryClient` wystąpień lub `TelemetryContext`? Lub czy zapisu [filtru lub próbkowania konfiguracji](app-insights-api-filtering-sampling.md) może on filtrować się zbyt dużo?
* W przypadku modyfikacji ApplicationInsights.config dokładnie sprawdzić konfigurację hello [TelemetryInitializers i TelemetryProcessors](app-insights-api-filtering-sampling.md). Typ o nazwie niepoprawnie lub parametr może spowodować hello SDK toosend żadne dane.

## <a name="q04"></a>Brak danych dotyczących użycia wyświetleń strony, przeglądarek,
*Czas ładowania strony widoku lub hello przeglądarki lub użycie bloków są widoczne dane w czas odpowiedzi serwera i wykresy żądań serwera, ale żadne dane.*

Witaj dane pochodzą z skryptów w hello stron sieci web. 

* Jeśli dodano usługę Application Insights tooan istniejący projekt sieci web [ręcznie masz skrypty hello tooadd](app-insights-javascript.md).
* Upewnij się, że program Internet Explorer lokacji nie są wyświetlane w trybie zgodności.
* Funkcja debugowania w przeglądarce hello (F12 w niektórych przeglądarkach, następnie wybierz sieć) tooverify, które dane są wysyłane za`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Brak danych zależności lub wyjątku
Zobacz [dane telemetryczne zależności](app-insights-asp-net-dependencies.md) i [dane telemetryczne dotyczące wyjątków](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Brak danych wydajności
Dane dotyczące wydajności (procesora CPU, szybkość We/Wy i tak dalej) jest dostępna dla [usług sieci web Java](app-insights-java-collectd.md), [aplikacji klasycznych systemu Windows](app-insights-windows-desktop.md), [sieci web IIS na aplikacje i usługi Jeśli Zainstaluj monitor stanu](app-insights-monitor-performance-live-website-now.md), i [Usług w chmurze azure](app-insights-azure.md). można znaleźć go w obszarze Ustawienia serwerów.

Nie jest dostępna dla witryn sieci Web Azure.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Żadne dane (serwer), ponieważ po opublikowaniu serwera toomy aplikacji hello
* Sprawdź faktycznie skopiować wszystkie hello firmy Microsoft. Biblioteki DLL ApplicationInsights toohello serwera wraz Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* W zaporze, użytkownik może być zbyt[Otwórz Niektóre porty TCP](app-insights-ip-addresses.md#data-access-api).
* Jeśli masz toouse proxy toosend spoza sieci firmowej, należy ustawić [defaultProxy —](https://msdn.microsoft.com/library/aa903360.aspx) w pliku Web.config
* Windows Server 2008: Upewnij się, że zainstalowano hello następujące aktualizacje: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Użycie danych toosee, ale została zatrzymana
* Sprawdź hello [blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).
* Czy osiągnięto limitu przydziału miesięcznego punktów danych? Otwórz hello ustawienia/przydziału i toofind cennik wychodzących. Jeśli tak, możesz uaktualnić swój plan lub zapłacić za dodatkowe pojemności. Zobacz hello [cennik schemat](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Nie jest wyświetlane wszystkie dane hello używam I oczekiwana
Jeśli aplikacja wysyła dużą ilość danych i używasz hello zestaw SDK usługi Application Insights dla platformy ASP.NET w wersji 2.0.0-beta3 lub hello później, [adaptacyjną próbkowania](app-insights-sampling.md) funkcja może działać i wysłać określonego odsetka telemetrii. 

Można ją wyłączyć, ale nie jest to zalecane. Próbkowanie zaprojektowano tak, aby poprawnie powiązane dane telemetryczne są przesyłane w celach diagnostycznych. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Niewłaściwe dane geograficzne w danych telemetrycznych użytkownika
Hello miasta, regionu i kraju wymiary są uzyskiwane z adresów IP, a nie zawsze są dokładne.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Wyjątek „nie można odnaleźć metody” podczas uruchamiania w usługach Azure Cloud Services
Czy to kompilacja dla .NET 4.6? Wersja 4.6 nie jest automatycznie obsługiwana w rolach usług Azure Cloud Services. [Zainstaluj wersję 4.6 w każdej roli](../cloud-services/cloud-services-dotnet-install-dotnet.md) przed uruchomieniem aplikacji.

## <a name="still-not-working"></a>Nadal nie działa...
* [Application Insights forum](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

