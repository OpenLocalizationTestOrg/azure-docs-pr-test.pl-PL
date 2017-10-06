---
title: "wdrożenie aaaFlighting (testowania wersji beta) w usłudze Azure App Service"
description: "Dowiedz się, jak tooflight nowych funkcji w aplikacji lub w wersji beta testowania aktualizacji w tym samouczku end-to-end. Powoduje przeniesienie razem usługi aplikacji funkcje, takie jak ciągła publikowania, miejsc routingu ruchu i integracji usługi Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service
W tym samouczku przedstawiono sposób toodo *flighting wdrożeń* integrując hello różnych możliwości [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [Azure Application Insights](/services/application-insights/).

*Flighting* jest procesem wdrażania, która weryfikuje nowej funkcji lub zmiany z ograniczoną liczbą rzeczywistą klientów, a główne testowanie w środowisku produkcyjnym. Jest akin toobeta testowania i jest czasem nazywana "transmitowane kontrolowane testu". Wiele dużych przedsiębiorstw witrynę internetową Użyj tej metody, aby uzyskać wczesne sprawdzania poprawności na ich aktualizacji aplikacji, w praktyce ich [elastyczne programowanie](https://en.wikipedia.org/wiki/Agile_software_development). Usługa aplikacji Azure umożliwia toointegrate testów w środowisku produkcyjnym z publikowaniem ciągłej i tego samego scenariusza DevOps hello tooimplement usługi Application Insights. Zalety tego podejścia:

* **Uzyskanie opinii rzeczywistych *przed* są aktualizacje wydane tooproduction** — Witaj tylko element lepszym rozwiązaniem niż uzyskanie opinii zaraz po zwolnieniu jest uzyskanie opinii przed zwolnieniem. Wczesne wymagasz w cyklu życia produktów hello można przetestować aktualizacje o ruchu rzeczywistych użytkowników i zachowania.
* **Ulepszanie [ciągłego test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  — dzięki zintegrowaniu testowanie w produkcji z ciągłej integracji i instrumentacji z usługi Application Insights, sprawdzanie poprawności użytkownika odbywa się wczesne i automatycznie w cykl życia. Pozwala to zmniejszyć inwestycji czas wykonywania testu ręcznego.
* **Optymalizacja przepływ testowej pracy w** -automatyzując testowanie w produkcji z ciągłego monitorowania Instrumentacji potencjalnie wykonasz hello cele różnego rodzaju testów w ramach jednego procesu, taką jak [integracji](https://en.wikipedia.org/wiki/Integration_testing), [regresji](https://en.wikipedia.org/wiki/Regression_testing), [użyteczność](https://en.wikipedia.org/wiki/Usability_testing), dostępności, lokalizacji, [wydajności](https://en.wikipedia.org/wiki/Software_performance_testing), [zabezpieczeń](https://en.wikipedia.org/wiki/Security_testing), i [ akceptacji](https://en.wikipedia.org/wiki/Acceptance_testing).

Flighting wdrożenia nie jest niemal routingu ruchu sieciowego na żywo. W takim wdrożeniu mają wgląd toogain tak szybko jak to możliwe, czy jest nieoczekiwany błąd, spadek wydajności, problemy środowisko użytkownika. Należy pamiętać, że mamy do czynienia z klientami prawdziwe. Tak toodo go do prawej strony, należy się upewnić, że po skonfigurowaniu sieci flighting toogather wdrożenia wszystkich danych hello możesz konieczne w celu toomake podjąć świadomą decyzję dla kolejny krok. W tym samouczku przedstawiono sposób toocollect danych za pomocą usługi Application Insights, ale można użyć usługi New Relic lub inne technologie, które pasujące do danego scenariusza.

## <a name="what-you-will-do"></a>Będzie wykonywać
W tym samouczku przedstawiono sposób toobring hello następujących scenariuszy razem tootest aplikację usługi aplikacji w środowisku produkcyjnym:

* [Kierować ruchem produkcji](app-service-web-test-in-production-get-start.md) tooyour aplikacji w wersji beta
* [Instrumentacja aplikacji](../application-insights/app-insights-web-track-usage.md) tooobtain przydatne metryki
* Stale wdrażanie aplikacji w wersji beta i śledzić metryki aktywnej aplikacji
* Porównaj metryki między aplikacji produkcyjnej hello i toosee aplikacji w wersji beta hello jak zmienia kod tłumaczenia tooresults

## <a name="what-you-will-need"></a>Dane będą potrzebne
* Konto platformy Azure
* A [GitHub](https://github.com/) konta
* Visual Studio 2015 — można pobrać hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Powłoka Git (zainstalowaną z [GitHub dla systemu Windows](https://windows.github.com/)) — dzięki temu możesz toorun zarówno hello Git poleceń programu PowerShell i w hello tej samej sesji
* Najnowsze [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) usługi bits
* Podstawową wiedzę na temat hello następujące czynności:
  * [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania szablonu (zobacz [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Należy toocomplete konto platformy Azure w tym samouczku:
>
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu można zachować konta hello i korzystać z bezpłatnych usług platformy Azure, takich jak aplikacje sieci Web.
> * Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
>
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a name="set-up-your-production-web-app"></a>Konfigurowanie aplikacji sieci web w środowisku produkcyjnym
> [!NOTE]
> skrypt Hello używany w tym samouczku zostaną skonfigurowane automatycznie ciągłego publikowania z repozytorium GitHub. Wymaga to, że Twoje poświadczenia GitHub są już przechowywane na platformie Azure, w przeciwnym razie hello uwzględnione w skryptach, wdrożenie zakończy się niepowodzeniem podczas próby ustawienia kontroli źródła tooconfigure hello aplikacji sieci web.
>
> toostore Twojego GitHub poświadczenia na platformie Azure, tworzenie aplikacji sieci web w hello [Azure Portal](https://portal.azure.com/) i [skonfigurować wdrożenie GitHub](app-service-continuous-deployment.md). Wystarczy toodo raz.
>
>

W typowy scenariusz DevOps masz aplikację, która działa na platformie Azure i mają toomake tooit zmiany poprzez publikowanie ciągłe. W tym scenariuszu zostanie wdrożona tooproduction szablonu, który został opracowany i przetestowany.

1. Tworzenie własnych rozwidlenia hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium. Aby uzyskać informacje dotyczące tworzenia rozwidlenia, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/). Po utworzeniu rozwidlenia, można to sprawdzić w przeglądarce.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Otwórz sesję powłoki Git. Jeśli nie masz jeszcze powłoki Git, zainstaluj [GitHub dla systemu Windows](https://windows.github.com/) teraz.
3. Utwórz lokalne Sklonowanie rozwidlenia, wykonując następujące polecenia hello:

     https://github.com/<your_fork>/ToDoApp.git klonowania git
4. Po utworzeniu sieci lokalnej klonowania, przejdź zbyt*&lt;repository_root >*\ARMTemplates i wykonywania hello deploy.ps1 skryptu unikatowy sufiks, jak pokazano poniżej:

     https://github.com/<your_fork>/todoapp.git — RepoUrl.\deploy.ps1 - ResourceGroupSuffix < your_suffix >
5. Po wyświetleniu monitu wpisz hello Żądana nazwa użytkownika i hasło, aby uzyskać dostęp do bazy danych. Pamiętaj poświadczenia bazy danych, ponieważ będą potrzebne toospecify je ponownie podczas aktualizowania hello grupy zasobów.

   Powinny pojawić się hello inicjowania obsługi administracyjnej postęp różnych zasobów platformy Azure. Po zakończeniu wdrażania, skrypt hello uruchamianie aplikacji hello w przeglądarce hello i zapewniają przyjazne sygnału dźwiękowego.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Ponownie w sesji programu Git powłoki, uruchom polecenie:

     . \swap — nazwa ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Po zakończeniu działania skryptu hello, przejdź wstecz adres frontonu toohello toobrowse (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello aplikacja była uruchomiona w środowisku produkcyjnym.
8. Zaloguj się do hello [Azure Portal](https://portal.azure.com/) i spójrz na to, co jest tworzony.

   Będziesz w stanie toosee dwie aplikacje sieci web w hello tej samej grupie zasobów, z hello `Api` sufiksu w nazwie hello. Jeśli wyświetlany jest widok grupy zasobów hello, pojawi się także hello bazy danych SQL i serwera, hello planu usługi aplikacji i hello przemieszczania miejsc aplikacji sieci web hello. Przeglądanie hello różne zasoby i porównaj je z  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json sposobu ich konfiguracji w szablonie hello.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Zdefiniowano hello aplikacji produkcyjnej.  Teraz załóżmy Załóżmy, że nie możesz odbierać opinię, że użyteczność jest niska dla aplikacji hello. Możesz zdecydować, tooinvestigate. Chcesz zacząć tooinstrument Twojego toogive aplikacji należy opinii.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Zbadaj: Instrumentacja aplikację klienta dla monitorowania metryki
1. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo.sln w programie Visual Studio.
2. Przywróć wszystkie pakiety Nuget, klikając prawym przyciskiem myszy rozwiązanie > **Zarządzaj pakietami NuGet dla rozwiązania** > **przywrócić**.
3. Kliknij prawym przyciskiem myszy **MultiChannelToDo.Web** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów tooToDoApp*&lt;your_suffix >* > **tooProject Dodaj usługę Application Insights**.
4. W portalu Azure hello, otwórz hello bloku hello **MultiChannelToDo.Web** zasobów szczegółowe informacje o aplikacji. Następnie w hello **kondycji aplikacji** część, kliknij przycisk **Dowiedz się, jak strona przeglądarki toocollect ładowanie danych** > skopiować kod.
5. Dodaj hello skopiować kod Instrumentacji JS zbyt*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml tuż przed zamknięciem hello `<heading>` tagu. Musi on zawierać klucza Instrumentacji unikatowy hello zasobu szczegółowe informacje o aplikacji.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Wysyłanie zdarzeń niestandardowych tooApplication wgląd do kliknięcia myszą przez dodanie hello następującego kodu toohello dolnej części treści:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Ta Wstawka kodu JavaScript wysyła tooApplication zdarzenie niestandardowe Insights za każdym razem, gdy użytkownik kliknie w dowolnym miejscu w aplikacji sieci web hello.
7. W powłoce Git należy Zatwierdź i Wypchnij rozwidlenia tooyour zmiany w witrynie GitHub. Następnie poczekaj przeglądarki toorefresh klientów.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Tooproduction zmiany aplikacji hello wdrożone wymiany (MB):

     . \swap — nazwa ToDoApp < your_suffix >
9. Przeglądaj toohello zasobu usługi Application Insights, który został skonfigurowany. Niestandardowe zdarzenia kliknięcia.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Jeśli nie widzisz metryki dla niestandardowych zdarzeń, poczekaj kilka minut i kliknij przycisk **Odśwież**.

Załóżmy, że zostanie wyświetlony wykres, takich jak poniżej:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

I siatki zdarzeń hello poniżej:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Zgodnie z kodu aplikacji ToDoApp tooyour, hello **przycisk** zdarzenia odpowiada przycisk Prześlij toohello i hello **dane wejściowe** zdarzenia odpowiada toohello pola tekstowego. Do tej pory rzeczy sensu. Jednak prawdopodobnie jest dobrym ilość kliknięcia i bardzo kilku kliknięć na powitania wykonania (hello **LI** zdarzeń).

Na podstawie tego, możesz formularza z hipotezę, że niektórych użytkowników występują pomylić część hello interfejsu użytkownika jest aktywne i to, że wyglądzie hello kursora dla zaznaczonego tekstu, gdy znajduje się na powitania elementy listy i ich ikony.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Może to być contrived przykład. Niemniej jednak jest toomake będzie poprawy tooyour aplikacji, a następnie wykonaj flighting opinie użyteczności tooget wdrożenia klientów na żywo.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumentacja dla monitorowania metryki aplikacji serwera
Jest to tangens, ponieważ scenariusz hello przedstawiona w tym samouczku dotyczy tylko powitania klienta aplikacji. Jednak aby informacje były kompletne skonfigurujesz hello aplikacji po stronie serwera.

1. Kliknij prawym przyciskiem myszy **MultiChannelToDo** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów tooToDoApp*&lt;your_suffix >* > **tooProject Dodaj usługę Application Insights**.
2. W powłoce Git należy Zatwierdź i Wypchnij rozwidlenia tooyour zmiany w witrynie GitHub. Następnie poczekaj przeglądarki toorefresh klientów.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Tooproduction zmiany aplikacji hello wdrożone wymiany (MB):

     . \swap — nazwa ToDoApp < your_suffix >

Gotowe.

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Zbadaj: Dodaj tagi specyficzne dla miejsca tooyour klienta aplikacji metryki
W tej sekcji skonfigurujesz hello wdrożenia różnych miejsc toosend telemetrii specyficzne dla miejsca toohello tego samego zasobu usługi Application Insights. W ten sposób można porównać telemetrii danych między ruchu z różnych miejsc (środowisk wdrażania) tooeasily zobaczyć efekt hello zmiany aplikacji. At hello sam czas hello produkcji ruchu można oddzielić od hello rest, dzięki czemu można kontynuować toomonitor aplikacji produkcyjnych zgodnie z potrzebami.

Ponieważ w przypadku zbierania danych na zachowanie klienta będzie [Dodaj telemetrię inicjatora tooyour kod JavaScript](../application-insights/app-insights-api-filtering-sampling.md) w index.cshtml. Jeśli chcesz tootest wydajności po stronie serwera, na przykład, również należy podobnie w kodzie serwera (zobacz [aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk](../application-insights/app-insights-api-custom-events-metrics.md).

1. Najpierw dodaj Witaj kodu bewteen Witaj dwie `//` komentarze poniżej w bloku kodu JavaScript hello dodania toohello `<heading>` tagu wcześniej.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Ten kod inicjatora powoduje hello `appInsights` tooadd obiektu hello właściwość niestandardowa o nazwie `Environment` tooevery część wysyłania danych telemetrycznych.
2. Następnie dodaj tej właściwości niestandardowej jako [gniazdo ustawienie](web-sites-staged-publishing.md#AboutConfiguration) dla aplikacji sieci web na platformie Azure. toodo tego hello uruchom następujące polecenia w sesji programu Git powłoki.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Witaj Web.config w projekcie już definiuje hello `environment` ustawienia aplikacji. To ustawienie, podczas testowania aplikacji hello lokalnie, Twoje metryki zostanie oznaczone z `VS Debugger`. Jednak po naciśnięciu tooAzure Twoje zmiany Azure znajduje i używa hello `environment` aplikacji zamiast tego ustawienia w konfiguracji aplikacji sieci web hello i Twoje metryki zostaną oznaczone tagiem `Production`.
3. Zatwierdź i push rozwidlenia tooyour zmian kodu w witrynie GitHub, a następnie odczekaj dla użytkowników toouse hello nowej aplikacji (należy toorefresh hello przeglądarki). Zajmuje około 15 minut przez hello nowych właściwości tooshow w szczegółowe dane aplikacji `MultiChannelToDo.Web` zasobów.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Teraz przejdź toohello **niestandardowe zdarzenia** ponownie bloku i Filtruj hello metryki na `Environment=Production`. Teraz powinno być możliwe toosee wszystkie hello nowych zdarzeń niestandardowych w środowisku produkcyjnym hello gniazdo z tego filtru.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Kliknij przycisk hello **ulubione** , takich jak przycisk toosave hello bieżącego Eksploratora metryk ustawienia toosomething **niestandardowe zdarzenia: produkcji**. Możesz łatwo przełączać się między tego widoku oraz widoku miejsca wdrożenia później.

   > [!TIP]
   > W celu wykonania analizy jeszcze bardziej skuteczne, należy wziąć pod uwagę [integrowanie zasobu usługi Application Insights z usługi Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Dodaj znaczniki specyficzne dla miejsca tooyour serwera aplikacji metryk
Ponownie aby informacje były kompletne skonfigurujesz hello aplikacji po stronie serwera. W odróżnieniu od powitania klienta aplikacji, która jest instrumentowany w języku JavaScript tagi specyficzne dla miejsca dla aplikacji serwera hello są instrumentowane przy użyciu kodu platformy .NET.

1. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Dodaj blok kodu hello poniżej, bezpośrednio przed hello zamykającego nawiasu klamrowego przestrzeni nazw.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Popraw błędy rozpoznawania nazw hello przez dodanie hello `using` instrukcje poniżej toohello początku pliku hello:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Dodaj kod hello poniżej toohello początku hello `Application_Start()` metody:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Zatwierdź i push rozwidlenia tooyour zmian kodu w witrynie GitHub, a następnie odczekaj dla użytkowników toouse hello nowej aplikacji (należy toorefresh hello przeglądarki). Zajmuje około 15 minut przez hello nowych właściwości tooshow w szczegółowe dane aplikacji `MultiChannelToDo` zasobów.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Aktualizacja: Konfigurowanie gałąź w wersji beta
1. Otwórz  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json i Znajdź hello `appsettings` zasobów (Wyszukaj `"name": "appsettings"`). Istnieją 4 z nich, po jednej dla każdego miejsca.
2. Dla każdego `appsettings` zasobów, Dodaj `"environment": "[parameters('slotName')]"` końcu toohello ustawienie aplikacji hello `properties` tablicy. Nie zapomnij tooend hello poprzedniego wiersza przecinkami.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Dodany hello `environment` ustawienie tooall hello miejsc w szablonie hello aplikacji.
3. W hello tego samego pliku, Znajdź hello `slotconfignames` zasobów (Wyszukaj `"name": "slotconfignames"`). Istnieją 2 z nich, po jednej dla każdej aplikacji.
4. Dla każdego `slotconfignames` zasobów, Dodaj `"environment"` toohello koniec hello `appSettingNames` tablicy. Nie zapomnij tooend hello poprzedniego wiersza przecinkami.

    Po prostu wprowadzone hello `environment` miejsca wdrożenia odpowiednich tooits USB ustawienie aplikacji dla obydwu aplikacji.  
5. W sesji programu Git powłoki hello uruchom następujące polecenia z hello sam sufiks grupy zasobów, używanego wcześniej.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Po wyświetleniu monitu podaj jak poprzednio hello tych samych poświadczeń bazy danych SQL. Następnie, kiedy zadawane grupy zasobów hello tooupdate, typ `Y`, następnie `ENTER`.

    Gdy skrypt hello kończy, wszystkich zasobów w grupie zasobów z oryginalnego hello zostaną zachowane, ale nowe miejsce o nazwie "beta" jest tworzony w nim z hello sam konfiguracji jako miejsca "Tymczasowości" hello, który został utworzony w początku hello.

   > [!NOTE]
   > Ta metoda tworzenia wdrożenia w różnych środowiskach różni się od metody hello w [Agile software development z usługi aplikacji Azure](app-service-agile-software-development.md). W tym miejscu Utwórz środowisk wdrażania z miejsc wdrożenia, w której jako utworzono środowisk wdrażania z grupami zasobów. Zarządzanie środowiskami wdrożenia z grupami zasobów umożliwia toodevelopers off-limits środowiska produkcyjnego hello tookeep, ale nie jest toodo łatwe testowanie w środowisku produkcyjnym, co można zrobić w prosty sposób z miejsc.
   >
   >

W razie potrzeby, można również utworzyć aplikację alfa, uruchamiając

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

W tym samouczku użytkownik będzie tylko nadal używać aplikacji w wersji beta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Aktualizacji: Aktualizacje aplikacji w wersji beta toohello wypychania
Utwórz kopię tooyour aplikacji, które mają tooimprove.

1. Upewnij się, że możesz teraz w gałęzi w wersji beta

        git checkout beta
2. W  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, Znajdź hello `<li>` tagu i Dodaj hello `style="cursor:pointer"` atrybutu, jak pokazano poniżej.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Zatwierdź i Wypchnij tooAzure.
4. Sprawdź, czy zmiana hello teraz jest uwzględniana w gnieździe beta hello przechodząc toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Jeśli nie widzisz hello zmienić jeszcze, Odśwież przeglądarkę tooget hello nowy kod javascript.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Teraz, gdy masz zmiany w gnieździe beta hello jesteś gotowy tooperform flighting wdrożenia.

## <a name="validate-route-traffic-toohello-beta-app"></a>Sprawdź poprawność: Trasy ruchu toohello beta aplikacji
W tej sekcji będzie kierować ruch toohello beta aplikacji. For sake of przejrzystości demonstracyjnych będzie tooroute znaczna część hello użytkownika ruchu tooit. W rzeczywistości hello ilość ruchu sieciowego, które mają być tooroute zależy od konkretnej sytuacji. Na przykład jeśli witryna jest na dużą skalę hello Microsoft.com, następnie należy mniej niż jeden procent całkowitej ruchu w kolejności toogain przydatnych danych.

1. W sesji programu Git powłoki uruchom następujące polecenia tooroute hello połowy miejsca toohello ruchu hello produkcji w wersji beta:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Witaj `ReroutePercentage=50` właściwość określa, że 50% hello produkcji ruch będzie adres URL aplikacji w wersji beta routingiem toohello (określonego przez hello `ActionHostName` właściwości).
2. Teraz przejdź toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% ruchu hello powinno być teraz przekierowanego toohello miejsca w wersji beta.
3. W zasobu usługi Application Insights, filtrować metryki hello przez środowisko = "beta".

   > [!NOTE]
   > Jeśli zapiszesz ten widok filtrowany jako ulubiony innego, można łatwo Przerzuć widoków Eksploratora metryk hello między produkcyjnego i widoków w wersji beta.
   >
   >

Załóżmy, że w usłudze Application Insights zobaczyć coś podobnego toohello następujące czynności:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Nie tylko jest to wskazującą, że istnieje wiele więcej kliknięć na powitania `<li>` tagi, ale prawdopodobnie toobe skoków kliknięć na `<li>` tagów. Następnie stwierdzić, że osoby odkryć hello nowe `<li>` znaczniki są aktywne i są teraz wyczyszczenie wszystkich ich wcześniej wykonać zadania w aplikacji hello.

Na podstawie danych hello flighting wdrożenia, możesz zdecydować, że Twój nowy interfejs użytkownika jest gotowa do produkcji.

## <a name="go-live-move-your-new-code-into-production"></a>Przejdź na żywo: Przenieś nowy kod do środowiska produkcyjnego
Użytkownik jest teraz gotowy toomove Twojego tooproduction aktualizacji. Co to jest doskonałym rozwiązaniem jest teraz wiesz, że aktualizacja została już sprawdzona *przed* zostanie przypisany tooproduction. Dlatego teraz możesz mogą bezpiecznie wdrażać go. Ponieważ utworzono aplikację klienta AngularJS toohello aktualizacji, tylko weryfikowane hello kod po stronie klienta. Gdyby toomake zmiany toohello zaplecza interfejsu API sieci Web aplikacji, można zweryfikować zmiany podobnie i łatwe.

1. W powłoce Git należy usunąć regułę routingu ruchu hello, uruchamiając następujące polecenie hello:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Uruchom polecenia Git hello:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Poczekaj kilka minut, aż hello nowego kodu toohello toobe wdrożone miejsca, a następnie uruchom http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net, który hello nowa aktualizacja jest przygotowaniu miejsca hello tymczasowych gniazda. Pamiętaj, tym hello z rozwidlenia głównej gałęzi jest połączony przemieszczania toohello miejsca w aplikacji.
4. Teraz Zamień hello przemieszczania miejsca w środowisku produkcyjnym

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Podsumowanie
Usługa aplikacji Azure ułatwia tootest toomedium małe firmy swoje aplikacje skierowane do klienta w środowisku produkcyjnym, coś wykonanej tradycyjnie w dużych przedsiębiorstw. Mamy nadzieję, że w tym samouczku przyznał Ci hello wiedzy potrzebne Twój świat DevOps toobring razem usługi aplikacji i usługi Application Insights toomake flighting wdrażania, a także innych scenariuszy testów w środowisku produkcyjnym.

## <a name="more-resources"></a>Więcej zasobów
* [Programowanie zwinne oprogramowania z usługi aplikacji Azure](app-service-agile-software-development.md)
* [Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych](web-sites-staged-publishing.md)
* [Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON modułu sprawdzania poprawności](http://jsonlint.com/)
* [Rozgałęzianie Git — podstawowe rozgałęzianie i scalanie](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Witryna typu Wiki Kudu projektu](https://github.com/projectkudu/kudu/wiki)
