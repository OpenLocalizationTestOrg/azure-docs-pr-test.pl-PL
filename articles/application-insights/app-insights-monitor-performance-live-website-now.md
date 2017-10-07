---
title: "aaaMonitor na żywo ASP.NET sieci web aplikacji za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności witryny sieci Web bez jej ponownego wdrażania. Działa z aplikacjami sieci Web platformy ASP.NET hostowanymi lokalnie na maszynach wirtualnych lub platformie Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Instrumentowanie aplikacji sieci Web w czasie wykonywania za pomocą usługi Application Insights


Można Instrumentacja aplikacji sieci web na żywo z usługą Azure Application Insights, bez konieczności toomodify lub ponownego wdrażania kodu. Jeśli Twoje aplikacje są hostowane na lokalnym serwerze IIS, zainstaluj monitor stanu. Jeśli zostaną aplikacji sieci web platformy Azure lub uruchomić w maszynie Wirtualnej platformy Azure, możesz przełączyć się na monitorowanie usługi Application Insights z poziomu Panelu sterowania Azure hello. Istnieją także osobne artykuły na temat instrumentacji [działających aplikacji sieci Web w technologii J2EE](app-insights-java-live.md) i [usług Azure Cloud Services](app-insights-cloudservices.md). Potrzebna jest subskrypcja platformy [Microsoft Azure](http://azure.com).

![przykładowe wykresy](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Dostępne są opcje trzy aplikacji sieci web, tras tooapply usługi Application Insights tooyour .NET:

* **Czas kompilacji:** [hello Dodaj zestaw SDK usługi Application Insights] [ greenbrown] kodu aplikacji sieci web tooyour.
* **Czas wykonywania:** Instrumentacja aplikacji sieci web na serwerze hello zgodnie z opisem poniżej, bez odbudowywania ani ponownego wdrażania hello kodu.
* **Zarówno:** kompilacji hello zestawu SDK do kodu aplikacji sieci web, a także zastosować dla niej hello rozszerzenia środowiska wykonawczego. Pobierz hello najlepszy obie opcje.

Poniżej przedstawiono podsumowanie tego, co można uzyskać, korzystając z danej trasy:

|  | W czasie kompilacji | W czasie wykonywania |
| --- | --- | --- |
| Żądania i wyjątki |Tak |Tak |
| [Bardziej szczegółowe wyjątki](app-insights-asp-net-exceptions.md) | |Tak |
| [Diagnostyka zależności](app-insights-asp-net-dependencies.md) |Na platformie .NET 4.6 +, ale mniej szczegółów |Tak, kompletne szczegóły: kody wyników, tekst polecenia SQL, czasownik HTTP|
| [Liczniki wydajności sytemu](app-insights-performance-counters.md) |Tak |Tak |
| [Interfejs API dla telemetrii niestandardowej][api] |Tak |Nie |
| [Integracja dziennika śledzenia](app-insights-asp-net-trace-logs.md) |Tak |Nie |
| [Widok strony i dane użytkownika](app-insights-javascript.md) |Tak |Nie |
| Kod toorebuild potrzebny |Tak | Nie |


## <a name="monitor-a-live-azure-web-app"></a>Monitorowanie działającej aplikacji sieci Web platformy Azure

Jeśli aplikacja jest uruchomiona jako usługa Azure usługi sieci web, tutaj w sposób tooswitch dotyczące monitorowania:

* Wybierz usługi Application Insights w Panelu sterowania aplikacji hello na platformie Azure.

    ![Konfigurowanie usługi Application Insights dla aplikacji sieci Web platformy Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Po otwarciu strony podsumowania hello usługi Application Insights, kliknij łącze hello na powitania dolnej tooopen hello pełne zasobu usługi Application Insights.

    ![Kliknij go, tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Monitorowanie aplikacji w chmurze i na maszynie wirtualnej](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Włączanie monitorowania po stronie klienta na platformie Azure

Po włączeniu usługi Application Insights na platformie Azure możesz dodać telemetrię widoku strony i użytkownika.

1. Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji
2.  W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość: 
   
    Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Wartość:`true`
3. **Zapisz** hello ustawienia i **ponowne uruchomienie** aplikacji.

zestaw SDK usługi Application Insights JavaScript Hello jest teraz wprowadzić do każdej strony sieci web.

## <a name="monitor-a-live-iis-web-app"></a>Monitorowanie działającej aplikacji sieci Web usług IIS

Jeśli aplikacja jest hostowana na serwerze usług IIS, włącz usługę Application Insights przy użyciu monitora stanu.

1. Zaloguj się na serwerze sieci Web usług IIS, używając poświadczeń administratora.
2. Jeśli Monitor stanu usługi Application Insights nie jest już zainstalowany, Pobierz i uruchom hello [Instalator Monitor stanu](http://go.microsoft.com/fwlink/?LinkId=506648) (lub uruchom [Instalatora platformy sieci Web](https://www.microsoft.com/web/downloads/platform.aspx) i wyszukaj w nim Application Insights stanu Monitor).
3. Monitor stanu, wybierz hello zainstalowanych aplikacji sieci web lub witryny sieci Web, które mają toomonitor. Zaloguj się przy użyciu poświadczeń platformy Azure.

    Konfigurowanie zasobów hello miejscu powoduje hello toosee hello portalu Application Insights. (Zazwyczaj jest najlepszym toocreate nowy zasób. Wybierz istniejący zasób, jeśli masz już [testy sieci Web][availability] lub [monitorowanie klienta][client] dla tej aplikacji). 

    ![Wybór aplikacji i zasobu.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Uruchom ponownie usługi IIS.

    ![Wybierz ponowne uruchomienie u góry hello hello okna dialogowego.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Działanie usługi sieci Web zostanie na krótko przerwane.

## <a name="customize-monitoring-options"></a>Dostosowywanie opcji monitorowania

Włączanie usługi Application Insights dodaje biblioteki dll i ApplicationInsights.config tooyour aplikacji sieci web. Możesz [edycji pliku .config hello](app-insights-configuration-with-applicationinsights-config.md) toochange niektórych opcji hello.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Po ponownym opublikowaniu aplikacji ponownie włącz usługę Application Insights

Aby ponownie opublikować aplikację, należy wziąć pod uwagę [Dodawanie usługi Application Insights toohello kodu w programie Visual Studio][greenbrown]. Można uzyskać bardziej szczegółowe dane telemetryczne i telemetria niestandardowa toowrite hello możliwości.

Jeśli chcesz, aby toore-opublikować bez dodawania usługi Application Insights toohello kodu, należy pamiętać, że proces wdrażania hello może usunąć hello bibliotek DLL i ApplicationInsights.config z hello opublikowane witryny sieci web. Zatem:

1. Jeśli edytowano plik ApplicationInsights.config, utwórz jego kopię przed ponownym opublikowaniem aplikacji.
2. Ponownie opublikuj aplikację.
3. Ponownie włącz monitorowanie za pomocą usługi Application Insights. (Użyj odpowiedniej metody hello: panel sterowania aplikacji sieci web platformy Azure hello lub hello Monitor stanu na hoście usług IIS.)
4. Przywraca wszelkich zmian, które należy wykonać w pliku .config hello.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Rozwiązywanie problemów z konfiguracją środowiska uruchomieniowego usługi Application Insights

### <a name="cant-connect-no-telemetry"></a>Nie można nawiązać połączenia? Brak telemetrii?

* Otwórz [hello niezbędne porty wychodzące](app-insights-ip-addresses.md#outgoing-ports) w toowork Monitor stanu tooallow zapory na serwerze.

* Otwórz monitor stanu i wybierz swoją aplikację w lewym okienku. Sprawdź, czy istnieją jakiekolwiek komunikaty diagnostyczne dla tej aplikacji w sekcji "Konfiguracja powiadomienia" hello:

  ![Otwórz hello wydajności bloku toosee żądania, czas odpowiedzi, zależności i innych danych](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Na serwerze hello Jeśli zostanie wyświetlony komunikat informujący o "niewystarczające uprawnienia", spróbuj następujących hello:
  * W Menedżerze usług IIS wybierz pulę aplikacji, otwórz **Zaawansowane ustawienia**i w obszarze **Model procesu** należy zwrócić uwagę hello tożsamości.
  * W Panelu sterowania Zarządzanie komputerem Dodaj tę grupę Użytkownicy monitora wydajności toohello tożsamości.
* Jeśli na serwerze jest zainstalowany agent MMA/SCOM (Systems Center Operations Manager), niektóre wersje mogą powodować konflikt. Odinstaluj zarówno SCOM i Monitor stanu i ponownie zainstalować najnowsze wersje hello.
* Zobacz [Rozwiązywanie problemów][qna].

## <a name="system-requirements"></a>Wymagania systemu
Serwerowe systemy operacyjne obsługiwane przez monitor stanu usługi Application Insights:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

z najnowszym dodatkiem SP oraz platformą .NET Framework 4.5

Po stronie klienta hello: Windows 7, 8, 8.1, 10, ponownie z programu .NET Framework 4.5

Obsługiwane wersje usług IIS: 7, 7.5, 8, 8.5 (usługi IIS są wymagane)

## <a name="automation-with-powershell"></a>Automatyzacja przy użyciu programu PowerShell
Monitorowanie można uruchomić i zatrzymać przy użyciu programu PowerShell na serwerze usług IIS.

Najpierw zaimportować moduł usługi Application Insights hello:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Dowiedz się, które aplikacje są monitorowane:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Witaj (opcjonalnie) Nazwa aplikacji sieci web.
* Wyświetla hello monitorowania stanu usługi Application Insights dla każdej aplikacji sieci web (lub o nazwie aplikacji hello) na serwerze IIS.
* Zwraca obiekt `ApplicationInsightsApplication` dla każdej aplikacji:

  * `SdkState==EnabledAfterDeployment`: Aplikacja jest monitorowana i było instrumentowane w czasie wykonywania przez narzędzie Monitor stanu hello, lub `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: aplikacja hello nie został zinstrumentowany na potrzeby usługi Application Insights. Nigdy nie było instrumentowane albo monitorowanie czasu wykonywania zostało wyłączone za pomocą narzędzia Monitor stanu hello lub z `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: aplikacja hello było instrumentowane przez dodanie hello SDK toohello źródła kodu. Nie można zaktualizować ani zatrzymać tego zestawu SDK.
  * `SdkVersion`Pokazuje hello wersja używana do monitorowania aplikacji.
  * `LatestAvailableSdkVersion`zawiera obecnie dostępna jest wersja hello hello galerii NuGet. Wersja toothis tooupgrade hello aplikacji, użyj `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`Nazwa Hello aplikacji hello w usługach IIS
* `-InstrumentationKey`Witaj ikey hello miejscu hello toobe wyniki wyświetlane zasobu usługi Application Insights.
* To polecenie cmdlet dotyczy tylko aplikacji, dla których nie przeprowadzono jeszcze instrumentacji (czyli SdkState == NotInstrumented).

    polecenia cmdlet Hello nie wpływa na aplikację, która jest już instrumentowany. Nie ma znaczenia, czy aplikacja hello było instrumentowane w czasie kompilacji przez dodanie hello SDK toohello kodu, ani nie na czas wykonywania przez poprzednie użycie tego polecenia cmdlet.

    Witaj SDK wersja użyta tooinstrument hello aplikacji jest hello wersji, która została ostatnio większości pobrane toothis serwera.

    toodownload hello najnowszą wersję, użyj ApplicationInsightsVersion aktualizacji.
* Zwraca obiekt `ApplicationInsightsApplication` w przypadku powodzenia. W przypadku niepowodzenia logowania toostderr śledzenia.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`Nazwa Hello aplikacji w usługach IIS
* `-All` Zatrzymuje monitorowanie wszystkich aplikacji na tym serwerze usług IIS, dla których `SdkState==EnabledAfterDeployment`
* Zatrzymuje monitorowanie hello określonych aplikacji i usuwa instrumentacji. Działa tylko dla aplikacji, które zostały zinstrumentowane w czasie wykonywania za pomocą hello narzędzia do monitorowania stanu lub Start ApplicationInsightsApplication. (`SdkState==EnabledAfterDeployment`)
* Zwraca obiekt ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: hello nazwę aplikacji sieci web w usługach IIS.
* `-InstrumentationKey` (opcjonalnie). Użycie wysłania tego toochange hello zasobów toowhich hello danych telemetrycznych aplikacji.
* To polecenie cmdlet:
  * Hello uaktualnienia o nazwie toohello wersji aplikacji hello SDK ostatnio pobrana toothis maszyny. (Działa tylko wtedy, gdy `SdkState==EnabledAfterDeployment`)
  * Jeśli podasz klucza Instrumentacji o nazwie aplikacji hello jest ponownie skonfigurowanych toosend telemetrii toohello zasobów z tego klucza. (Działa, jeśli `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Pobiera hello najnowszy zestaw SDK usługi Application Insights toohello serwera.

## <a name="questions"></a>Pytania dotyczące monitora stanu

### <a name="what-is-status-monitor"></a>Co to jest monitor stanu?

Aplikacja klasyczna, która jest instalowana na serwerze sieci Web usług IIS. Ułatwia ona instrumentację i konfigurowanie aplikacji sieci Web. 

### <a name="when-do-i-use-status-monitor"></a>Kiedy należy używać monitora stanu?

* tooinstrument dowolnej sieci web aplikacji, która jest uruchomiona na serwerze IIS — nawet wtedy, gdy jest już uruchomiona.
* dodatkowe dane telemetryczne tooenable dla aplikacji sieci web, które zostały [skompilowanych przy użyciu zestawu SDK usługi Application Insights hello](app-insights-asp-net.md) w czasie kompilacji. 

### <a name="can-i-close-it-after-it-runs"></a>Czy można zamknąć go po uruchomieniu?

Tak. Po ma instrumentowane hello witryn sieci Web, którą wybierzesz możesz go zamknąć.

Nie zbiera on telemetrii samodzielnie. Po prostu konfiguruje hello aplikacji sieci web i ustawia niektóre uprawnienia.

### <a name="what-does-status-monitor-do"></a>Co robi monitor stanu?

Po wybraniu aplikacji sieci web dla tooinstrument Monitor stanu:

* Pobiera i umieszcza hello zestawy usługi Application Insights i pliku .config w aplikacji sieci web hello folder plików binarnych.
* Modyfikuje `web.config` tooadd hello Application Insights HTTP śledzenia modułu.
* Włącza profilowanie wywołania zależności toocollect CLR.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Należy toorun Monitor stanu zawsze, gdy zaktualizuję aplikacji hello?

Nie, jeśli ponowne wdrażanie odbywa się przyrostowo. 

Wybranie opcji "Usuń istniejące pliki" hello w hello proces publikowania, będzie potrzebny toore Uruchom Monitor stanu tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Jakie dane telemetrii są zbierane?

W przypadku aplikacji z instrumentacją tylko w czasie wykonywania za pomocą monitora stanu:

* Żądania HTTP
* Wywołuje toodependencies
* Wyjątki
* Liczniki wydajności

W przypadku aplikacji już instrumentowanych w czasie kompilacji:

 * Liczniki procesu.
 * Wywołania zależności (.NET 4.5); wartości zwracane w wywołaniach zależności (.NET 4.6).
 * Wartości śladu stosu wyjątków.

[Dowiedz się więcej](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Następne kroki

Wyświetlanie telemetrii:

* [Eksploruj metryki](app-insights-metrics-explorer.md) toomonitor wydajności i użycia
* [Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toodiagnose problemów
* [Analiza](app-insights-analytics.md) dla bardziej zaawansowanych zapytań
* [Tworzenie pulpitów nawigacyjnych](app-insights-dashboards.md)

Dodawanie kolejnych funkcji telemetrii:

* [Tworzenie testów sieci web] [ availability] toomake się, że witryna pozostaje na żywo.
* [Dodaj telemetrię usługi sieci web klienta] [ usage] toosee wyjątki od kodu strony sieci web i toolet wstawiania śledzenia wywołań.
* [Dodaj kod, zestaw SDK usługi Application Insights tooyour] [ greenbrown] tak, aby można wstawiać śledzenia i rejestrowania zgłoszeń

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
