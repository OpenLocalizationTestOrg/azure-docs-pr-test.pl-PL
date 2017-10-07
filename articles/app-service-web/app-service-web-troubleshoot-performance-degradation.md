---
title: "aaaSlow wydajność aplikacji sieci web w usłudze App Service | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomaga powolne web app Rozwiązywanie problemów z wydajnością w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "wydajność aplikacji sieci Web, powolne aplikacji app powolne"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Powolne web app Rozwiązywanie problemów z wydajnością w usłudze Azure App Service
W tym artykule pomocy w rozwiązywaniu problemów z wydajnością aplikacji sieci web wolne w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.

## <a name="symptom"></a>Objaw
Podczas przeglądania aplikacji sieci web hello hello strony obciążenia powoli i czasami limitu czasu.

## <a name="cause"></a>Przyczyna
Ten problem jest często spowodowane przez problemy z poziomu aplikacji, takich jak:

* długi czas trwania żądania sieciowe
* zapytania kod lub bazy danych aplikacji jest nieefektywne
* aplikacji przy użyciu pamięci wysokiej/procesora CPU
* awarii z powodu wyjątku tooan aplikacji

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów
Rozwiązywanie problemów, można podzielić na trzy różne zadania, w kolejności sekwencyjnej:

1. [Sprawdź i monitorowanie zachowania aplikacji](#observe)
2. [Zbieranie danych](#collect)
3. [Ograniczenia hello problem](#mitigate)

[Aplikacje sieci Web usługi aplikacji](/services/app-service/web/) zapewnia różne opcje w każdym kroku.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Sprawdź i monitorowanie zachowania aplikacji
#### <a name="track-service-health"></a>Śledź usługę kondycji
Microsoft Azure publicizes każdym razem, gdy istnieje degradacji przerw i wydajności usługi. Kondycja hello hello usługi można śledzić na powitania [portalu Azure](https://portal.azure.com/). Aby uzyskać więcej informacji, zobacz [śledzić kondycja usługi](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorowanie aplikacji sieci web
Ta opcja umożliwia toofind wychodzących, jeśli masz problemy w aplikacji. W bloku aplikacja sieci web, kliknij hello **żądań i błędów** kafelka. Witaj **Metryka** bloku pokazuje wszystkie metryki hello można dodać.

Niektóre hello metryki dla aplikacji sieci web można toomonitor

* Pamięć średni zestaw roboczy
* Średni czas odpowiedzi
* Czas procesora CPU
* Zestaw roboczy pamięci
* Żądania

![Monitorowanie wydajności aplikacji sieci web](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Aby uzyskać więcej informacji, zobacz:

* [Monitorowanie aplikacji sieci Web w usłudze aplikacji Azure](web-sites-monitor.md)
* [Otrzymywanie powiadomień o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Monitoruje stan punktu końcowego sieci web
Jeśli używasz aplikacji sieci web w hello **standardowe** warstwy cenowej, aplikacje sieci Web umożliwia monitorowanie dwa punkty końcowe z trzech lokalizacji geograficznej.

Monitorowania punktów końcowych konfiguruje testów sieci web z rozproszona geograficznie lokalizacje testujące czas reakcji i przestoje adresów URL sieci web. Hello test wykonuje operacji HTTP GET na czas odpowiedzi hello toodetermine adres URL sieci web hello i przestoje w każdej lokalizacji. Każdej skonfigurowanej lokalizacji uruchamia test co pięć minut.

Czas działania jest monitorowana przy użyciu kodów odpowiedzi HTTP, a czas odpowiedzi jest mierzony w milisekundach. Test monitorowania kończy się niepowodzeniem, jeśli hello kod odpowiedzi HTTP jest mniejsza niż too400 lub jeśli odpowiedź hello trwa dłużej niż 30 sekund. Punkt końcowy jest traktowane jako dostępne w przypadku powodzenia testów monitorowania wszystkich hello określonej lokalizacji.

tooset go, zobacz [monitorowanie aplikacji w usłudze Azure App Service](web-sites-monitor.md).

Zobacz też [utrzymywanie Azure Web Sites zapasową oraz monitorowania punktów końcowych — z Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) Film przedstawiający monitorowania punktów końcowych.

#### <a name="application-performance-monitoring-using-extensions"></a>Monitorowanie wydajności aplikacji przy użyciu rozszerzenia
Można również monitorować wydajność aplikacji za pomocą *lokacji rozszerzenia*.

Każdej aplikacji sieci web usługi aplikacji — zapewnia punkt końcowy rozszerzonego zarządzania, która pozwala toouse zaawansowany zestaw narzędzi wdrożony jako rozszerzenia lokacji. Rozszerzenia obejmują: 

- Edytory kodu źródłowego, takich jak [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Narzędzia do zarządzania dla połączonych zasobów, takich jak bazy danych MySQL połączone tooa aplikacji sieci web.

[Azure Application Insights](/services/application-insights/) i [usługi New Relic](/marketplace/partners/newrelic/newrelic/) to dwie hello wydajności monitorowania rozszerzenia lokacji, które są dostępne. toouse usługi New Relic, należy zainstalować agenta w czasie wykonywania. toouse Azure Application Insights, należy odtworzyć kodu za pomocą zestawu SDK, a można też zainstalować rozszerzenia, która zapewnia dostęp do danych tooadditional. Witaj zestaw SDK umożliwia zapisanie kodu toomonitor hello użycia i wydajności aplikacji bardziej szczegółowo.

Zobacz toouse usługi Application Insights [monitorować wydajność w aplikacji sieci web](../application-insights/app-insights-web-monitor-performance.md).

Zobacz toouse New Relic [zarządzanie wydajnością aplikacji Relic nowego na platformie Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Zbieranie danych
Hello środowiska aplikacji sieci Web udostępnia funkcję diagnostyki dla rejestrowanie informacji z serwera sieci web hello i hello aplikacji sieci web. informacje o Hello jest dzielony diagnostyki serwera sieci web i diagnostyki aplikacji.

#### <a name="enable-web-server-diagnostics"></a>Włącz diagnostykę serwera sieci web
Można włączyć lub wyłączyć hello następujące rodzaje dzienników:

* **Szczegółowe rejestrowanie błędów** — szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej). To może zawierać informacje, które mogą pomóc ustalić, dlaczego serwer hello zwrócił kod błędu hello.
* **Nie powiodło się żądanie śledzenia** — szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śledzenia hello IIS składniki używane tooprocess hello żądania i czas hello w poszczególnych składników. Może to być przydatne, jeśli próbujesz wydajność aplikacji sieci web tooimprove lub określić, co powoduje określonego błędu HTTP.
* **Rejestrowanie serwera w sieci Web** — informacje o transakcjach HTTP przy użyciu hello W3C rozszerzony format pliku dziennika. Jest to przydatne podczas określania ogólną metryki aplikacji sieci web, takich jak hello liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.

#### <a name="enable-application-diagnostics"></a>Włącz diagnostykę aplikacji
Istnieje kilka opcji toocollect danych dotyczących wydajności aplikacji z aplikacji sieci Web, profilu aplikacji na żywo w programie Visual Studio lub zmodyfikować toolog kod z aplikacji, dodatkowe informacje i dane śledzenia. Można wybrać opcje hello oparte na dostęp, ile masz aplikację toohello i obserwowanych z hello narzędzi monitorowania.

##### <a name="use-application-insights-profiler"></a>Użyj Application Insights profilera
Można włączyć przechwytywania danych śledzenia wydajności szczegółowe toostart profilera Insights aplikacji hello. Ślady przechwycone się toofive, które dni temu, gdy są potrzebne tooinvestigate problemy wystąpiły w przeszłości hello są dostępne. Tę opcję można tak długo, jak długo mają zasobu usługi Application Insights dostępu toohello aplikacji sieci web w portalu Azure.

Application Insights Profiler zawiera dane statystyczne dotyczące czas odpowiedzi dla każdego wywołania sieci web i śladów, wskazującą, w którym wierszem kodu spowodował hello powolne odpowiedzi. Czasami hello aplikacji usługi app Service działa wolno, ponieważ niektóre kodu nie jest zapisywany w wydajności sposób. Przykładami sekwencyjnych kod, który można uruchomić w rywalizacji blokad równoległych i niepożądane bazy danych. Usunięcie tych wąskich gardeł w kodzie hello zwiększa wydajność aplikacji hello, ale są twardych toodetect bez konfigurowania dzienników i rozbudowane dane śledzenia. ślady Hello zebrane przez Profiler Insights aplikacji pomaga w identyfikacji hello wierszy kodu, który spowalnia aplikacji hello i rozwiązać ten problem w przypadku aplikacji usługi aplikacji.

 Aby uzyskać więcej informacji, zobacz [profilowania aplikacji sieci web platformy Azure na żywo za pomocą usługi Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Użyj profilowanie zdalne
W usłudze Azure App Service aplikacje sieci Web, aplikacje interfejsu API i zadania Webjob może być zdalnie profilowane. Wybierz tą opcję, jeśli masz zasobów aplikacji sieci web toohello dostępu i wiesz, jak tooreproduce hello problem lub jeśli znasz dokładnego hello sytuacji problem z wydajnością hello interwał czasu.

Profilowanie zdalne jest przydatne, jeśli hello Procesora CPU przez proces hello jest wysoka i proces działa wolniej niż oczekiwano lub hello opóźnienie żądania HTTP są większe niż jest to normalne, można zdalnie profilu procesu i uzyskać hello Procesora próbkowania wywołań stosy tooanalyze Witaj działania procesu i kodu gorących ścieżki.

Aby uzyskać więcej informacji, zobacz [profilowanie zdalne pomocy technicznej w usłudze Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Ręcznie skonfigurować dane śledzenia diagnostycznego
Jeśli masz kod źródłowy aplikacji sieci web toohello dostępu do diagnostyki aplikacji umożliwia informacji toocapture generowanych przez aplikację sieci web. Aplikacje ASP.NET mogą używać hello `System.Diagnostics.Trace` diagnostyki aplikacji toohello klasy toolog informacji logowania. Jednak należy toochange hello kodu i wdrożenie aplikacji. Ta metoda jest zalecane, jeśli aplikacja działa w środowisku testowym.

Aby uzyskać szczegółowe informacje na temat tooconfigure aplikacji w celu rejestrowania, zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Za pomocą portalu pomocy technicznej usługi Azure App Service hello
Aplikacje sieci Web udostępnia aplikacji sieci web hello możliwości tootroubleshoot problemów powiązanych tooyour analizując HTTP dzienniki, dzienniki zdarzeń, zrzuty procesu i inne. Można uzyskać dostępu do tych informacji za pomocą portalu pomocy technicznej w **http://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/Support**

Hello portal pomocy technicznej usługi Azure App Service zapewnia trzech osobnych kartach toosupport hello trzy kroki typowego scenariusza rozwiązywania problemów:

1. Sprawdź bieżące zachowanie
2. Analizowanie zbierania informacji diagnostycznych i uruchamiając hello analizatorów wbudowane
3. Ograniczenia

Problem hello jest przeprowadzana od razu, kliknij przycisk **Analizuj** > **diagnostyki** > **diagnozowanie teraz** toocreate sesję diagnostyki, które zbiera dzienniki HTTP, dzienniki Podglądu zdarzeń zrzuty pamięci, dzienniki błędów PHP i raportu procesu PHP.

Po pobraniu danych hello, portalu pomocy technicznej hello uruchamia analizę danych hello i udostępnia raport HTML.

W przypadku, gdy chcesz toodownload hello dane, domyślnie, powinny być przechowywane w folderze D:\home\data\DaaS hello.

Aby uzyskać więcej informacji w portalu pomocy technicznej usługi Azure App Service hello, zobacz [tooSupport nowe aktualizacje lokacji rozszerzenie dla witryny sieci Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Użyj hello Kudu Debug Console
Aplikacje sieci Web jest dostarczany z konsoli debugowania, która służy do debugowania, eksploracji, przekazywania plików, a także pobieranie informacji na temat środowiska punktów końcowych JSON. Ta konsola jest nazywany hello *konsoli Kudu* lub hello *pulpitu nawigacyjnego SCM* dla aplikacji sieci web.

Uzyskać dostęp do tego pulpitu nawigacyjnego, przechodząc łącze toohello **https://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/**.

Program Kudu udostępnia zagadnienia hello należą:

* ustawienia środowiska aplikacji
* strumień dziennika
* diagnostycznych zrzutu
* Konsola, w którym można uruchomić poleceń cmdlet programu Powershell i podstawowe polecenia systemu DOS debugowania.

Inny przydatną cechą Kudu jest, że w przypadku, gdy aplikacja jest zgłaszanie wyjątków pierwszej szansy, można użyć Kudu i zrzuty hello SysInternals narzędzie Procdump toocreate pamięci. Te zrzuty pamięci są migawki procesu hello i często ułatwiają rozwiązywanie problemów z bardziej skomplikowanych problemów z aplikacją sieci web.

Aby uzyskać więcej informacji o funkcjach dostępnych w Kudu, zobacz [narzędzia Azure witryn sieci Web Team Services, musisz wiedzieć o](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Ograniczenia hello problem
#### <a name="scale-hello-web-app"></a>Aplikacja sieci web hello skali
W usłudze Azure App Service Aby zwiększyć wydajność i przepływność, można dostosować hello skali, w którym są uruchomione aplikacji. Skalowanie w górę aplikacji sieci web obejmuje dwie akcje powiązane: zmiana z wyższej warstwy cenowej i konfigurowanie niektórych ustawień po przełączeniu toohello wyższej warstwy cenowej tooa planu usługi aplikacji.

Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md).

Ponadto można wybrać toorun aplikacji na więcej niż jedno wystąpienie. Skalowanie w poziomie nie tylko zapewnia więcej możliwości przetwarzania, ale umożliwia także niektóre ilość odporność na uszkodzenia. Jeśli proces hello przestanie działać w jednym wystąpieniu, hello innych wystąpień nadal tooserve żądań.

Można ustawić hello skalowanie toobe ręczne lub automatyczne.

#### <a name="use-autoheal"></a>Funkcja AutoHeal użycia
Funkcja AutoHeal odtwarzania procesu roboczego hello aplikacji na podstawie ustawień wybranego (np. zmiany konfiguracji, żądania, limity pamięci lub czasu hello wymagane tooexecute żądania). W większości przypadków hello odtworzenia procesu hello jest hello najszybszy sposób toorecover z problem. Chociaż można zawsze uruchomić ponownie hello aplikacji sieci web z bezpośrednio z poziomu portalu Azure hello, funkcja AutoHeal zrobi to automatycznie za użytkownika. Toodo wystarczy dodać niektóre wyzwalacze w hello głównym pliku web.config dla aplikacji sieci web. Te ustawienia będzie działać w hello sam sposób, nawet jeśli w aplikacji nie jest aplikacji .net.

Aby uzyskać więcej informacji, zobacz [automatyczne naprawianie Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Ponowne uruchomienie aplikacji sieci web hello
Ponowne uruchomienie jest często hello najprostszy sposób toorecover jednorazowo występujące problemy. Na powitania [portalu Azure](https://portal.azure.com/), w bloku aplikacja sieci web, masz toostop opcje hello lub uruchom ponownie aplikację.

 ![Uruchom ponownie problemy z wydajnością toosolve aplikacji sieci web](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

Można również zarządzać aplikacji sieci web przy użyciu programu Azure Powershell. Aby uzyskać więcej informacji, zobacz temat [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Azure PowerShell z usługą Azure Resource Manager).
