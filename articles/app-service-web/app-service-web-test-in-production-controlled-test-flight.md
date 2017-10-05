---
title: "Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service"
description: "Dowiedz się, jak lotu nowych funkcji w aplikacji lub wersji beta testowania aktualizacji w tym samouczku end-to-end. Powoduje przeniesienie razem usługi aplikacji funkcje, takie jak ciągła publikowania, miejsc routingu ruchu i integracji usługi Application Insights."
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
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service
W tym samouczku przedstawiono sposób wykonywania *flighting wdrożeń* dzięki integracji z różnych funkcji programu [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [Azure Application Insights](/services/application-insights/).

*Flighting* jest procesem wdrażania, która weryfikuje nowej funkcji lub zmiany z ograniczoną liczbą rzeczywistą klientów, a główne testowanie w środowisku produkcyjnym. Podobnie testowania w wersji beta i jest czasem nazywana "transmitowane kontrolowane testu". Wiele dużych przedsiębiorstw witrynę internetową Użyj tej metody, aby uzyskać wczesne sprawdzania poprawności na ich aktualizacji aplikacji, w praktyce ich [elastyczne programowanie](https://en.wikipedia.org/wiki/Agile_software_development). Usługa aplikacji Azure umożliwia testowanie w produkcji jest integrowana z ciągłej publikowanie i Application Insights, aby wdrożyć scenariusz dla tego samego DevOps. Zalety tego podejścia:

* **Uzyskaj opinie rzeczywistych *przed* aktualizacje są wydawane w środowisku produkcyjnym** -jedynym elementem lepszym rozwiązaniem niż uzyskanie opinii zaraz po zwolnieniu jest uzyskanie opinii przed zwolnieniem. Wczesne wymagasz w cyklu życia produktu można przetestować aktualizacje o ruchu rzeczywistych użytkowników i zachowania.
* **Ulepszanie [ciągłego test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  — dzięki zintegrowaniu testowanie w produkcji z ciągłej integracji i instrumentacji z usługi Application Insights, sprawdzanie poprawności użytkownika odbywa się wczesne i automatycznie w cykl życia. Pozwala to zmniejszyć inwestycji czas wykonywania testu ręcznego.
* **Optymalizacja przepływ testowej pracy w** -automatyzując testowanie w produkcji z ciągłego monitorowania Instrumentacji potencjalnie wykonasz celów różnego rodzaju testów w ramach jednego procesu, taką jak [integracji](https://en.wikipedia.org/wiki/Integration_testing), [regresji](https://en.wikipedia.org/wiki/Regression_testing), [użyteczność](https://en.wikipedia.org/wiki/Usability_testing), ułatwień dostępu, lokalizacji, [wydajności](https://en.wikipedia.org/wiki/Software_performance_testing), [zabezpieczeń](https://en.wikipedia.org/wiki/Security_testing), i [akceptacji](https://en.wikipedia.org/wiki/Acceptance_testing).

Flighting wdrożenia nie jest niemal routingu ruchu sieciowego na żywo. W takim wdrożeniu chcesz uzyskiwać wgląd w możliwie jak najszybciej czy też być nieoczekiwany błąd, spadek wydajności, problemy środowisko użytkownika. Należy pamiętać, że mamy do czynienia z klientami prawdziwe. Tak aby zrobić to prawo, należy się upewnić czy zdefiniowano flighting wdrożenia można zebrać wszystkie dane potrzebne do podjąć świadomej decyzji dla kolejny krok. Ten samouczek pokazuje, jak zbierać dane z usługi Application Insights, ale możesz użyć usługi New Relic lub inne technologie, które pasujące do danego scenariusza.

## <a name="what-you-will-do"></a>Będzie wykonywać
Z tego samouczka dowiesz się, jak można wyświetlić następujące scenariusze ze sobą, aby przetestować aplikację usługi aplikacji w środowisku produkcyjnym:

* [Kierować ruchem produkcji](app-service-web-test-in-production-get-start.md) do aplikacji w wersji beta
* [Instrumentacja aplikacji](../application-insights/app-insights-web-track-usage.md) uzyskać przydatne metryki
* Stale wdrażanie aplikacji w wersji beta i śledzić metryki aktywnej aplikacji
* Porównywanie metryk między aplikacją produkcyjnych i aplikacji w wersji beta, aby zobaczyć, jak zmiany kodu przełożyć na wyniki

## <a name="what-you-will-need"></a>Dane będą potrzebne
* Konto platformy Azure
* A [GitHub](https://github.com/) konta
* Visual Studio 2015 — można pobrać [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Powłoka Git (zainstalowaną z [GitHub dla systemu Windows](https://windows.github.com/)) — umożliwia to uruchamianie poleceń programu PowerShell i Git w tej samej sesji
* Najnowsze [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) usługi bits
* Podstawową wiedzę na temat następujących czynności:
  * [Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania szablonu (zobacz [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Do ukończenia tego samouczka jest potrzebne konto platformy Azure.
>
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt służy do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu możesz zachować konto i korzystać z bezpłatnych usług platformy Azure, takich jak aplikacje sieci Web.
> * Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
>
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a name="set-up-your-production-web-app"></a>Konfigurowanie aplikacji sieci web w środowisku produkcyjnym
> [!NOTE]
> Skrypt używany w tym samouczku zostaną skonfigurowane automatycznie ciągłego publikowania z repozytorium GitHub. Wymaga to, że Twoje poświadczenia GitHub są już przechowywane na platformie Azure, w przeciwnym razie wdrażanie przy użyciu skryptu zakończy się niepowodzeniem podczas próby skonfigurowania ustawień kontroli źródła dla aplikacji sieci web.
>
> Aby przechowywać swoje poświadczenia usługi GitHub na platformie Azure, tworzenie aplikacji sieci web w [Azure Portal](https://portal.azure.com/) i [skonfigurować wdrożenie GitHub](app-service-continuous-deployment.md). Wystarczy wykonać jeden raz.
>
>

W typowy scenariusz DevOps masz aplikację, która działa na platformie Azure, i chcesz wprowadzić zmiany poprzez publikowanie ciągłe. W tym scenariuszu zostanie wdrożona do środowiska produkcyjnego szablonu, który został opracowany i przetestowany.

1. Tworzenie własnych rozwidlenia [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium. Aby uzyskać informacje dotyczące tworzenia rozwidlenia, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/). Po utworzeniu rozwidlenia, można to sprawdzić w przeglądarce.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Otwórz sesję powłoki Git. Jeśli nie masz jeszcze powłoki Git, zainstaluj [GitHub dla systemu Windows](https://windows.github.com/) teraz.
3. Utwórz lokalne Sklonowanie rozwidlenia, wykonując następujące polecenie:

     https://github.com/<your_fork>/ToDoApp.git klonowania git
4. Po utworzeniu sieci lokalnej klonowania, przejdź do  *&lt;repository_root >*\ARMTemplates i uruchomić deploy.ps1 skrypt z unikatowy sufiks, jak pokazano poniżej:

     https://github.com/<your_fork>/todoapp.git — RepoUrl.\deploy.ps1 - ResourceGroupSuffix < your_suffix >
5. Po wyświetleniu monitu wpisz odpowiednią nazwę użytkownika i hasło dostępu do bazy danych. Pamiętaj poświadczenia bazy danych, ponieważ trzeba je ponownie określić podczas aktualizowania grupy zasobów.

   Postęp inicjowania obsługi administracyjnej z różnymi zasobami Azure powinna zostać wyświetlona. Po zakończeniu wdrażania, skrypt zostanie uruchomić aplikację w przeglądarce i podamy przyjazne sygnału dźwiękowego.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Ponownie w sesji programu Git powłoki, uruchom polecenie:

     . \swap — nazwa ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Po zakończeniu działania skryptu, przejdź wstecz, aby przejść do adresu serwera sieci Web (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) aby zobaczyć aplikacja była uruchomiona w środowisku produkcyjnym.
8. Zaloguj się do [Azure Portal](https://portal.azure.com/) i spójrz na to, co jest tworzony.

   Powinny być widoczne dwie aplikacje sieci web w tej samej grupie zasobów, z `Api` sufiksu w nazwie. Jeśli wyświetlany jest widok grupy zasobów, pojawi się także z bazą danych SQL i serwera, plan usługi aplikacji i tymczasowej miejsc aplikacji sieci web. Przechodzenie przez różne zasoby i porównaj je z  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json aby zobaczyć, jak są konfigurowane w szablonie.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Zdefiniowano aplikacji produkcyjnej.  Teraz załóżmy Załóżmy, że nie możesz odbierać opinię, że użyteczność jest niska dla aplikacji. Zdecydować zbadać. Zamierzasz Instrumentacja aplikacji pozwalają opinii.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Zbadaj: Instrumentacja aplikację klienta dla monitorowania metryki
1. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo.sln w programie Visual Studio.
2. Przywróć wszystkie pakiety Nuget, klikając prawym przyciskiem myszy rozwiązanie > **Zarządzaj pakietami NuGet dla rozwiązania** > **przywrócić**.
3. Kliknij prawym przyciskiem myszy **MultiChannelToDo.Web** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów do ToDoApp*&lt;your_suffix >* > **Dodaj usługę Application Insights do projektu**.
4. W portalu Azure, otwórz blok dla **MultiChannelToDo.Web** zasobów szczegółowe informacje o aplikacji. Następnie w **kondycji aplikacji** część, kliknij przycisk **Dowiedz się, jak zbierać dane ładowania stron przeglądarki** > skopiować kod.
5. Dodaj skopiowany kod Instrumentacji JS do  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml tuż przed zamknięciem `<heading>` tagu. Musi on zawierać klucz Instrumentacji unikatowy zasób szczegółowe informacje o aplikacji.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Wysyłanie zdarzeń niestandardowych do usługi Application Insights dla myszy kliknięć przez dodanie poniższego kodu do dolnej części treści:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Ta Wstawka kodu JavaScript wysyła do usługi Application Insights zdarzenie niestandardowe, za każdym razem, gdy użytkownik kliknie w dowolnym miejscu w aplikacji sieci web.
7. W powłoce Git Zatwierdź i Wypchnij zmiany do rozwidlenia w serwisie GitHub. Następnie odczekaj klientów odświeżyć przeglądarkę.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Zamień zmiany wdrożonej aplikacji w środowisku produkcyjnym:

     . \swap — nazwa ToDoApp < your_suffix >
9. Przejdź do zasobu usługi Application Insights, który został skonfigurowany. Niestandardowe zdarzenia kliknięcia.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Jeśli nie widzisz metryki dla niestandardowych zdarzeń, poczekaj kilka minut i kliknij przycisk **Odśwież**.

Załóżmy, że zostanie wyświetlony wykres, takich jak poniżej:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

I poniżej siatki zdarzeń:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Zgodnie z ToDoApp kod aplikacji **przycisk** zdarzenia odpowiada przycisk przesyłania i **dane wejściowe** zdarzenie odnosi się do pola tekstowego. Do tej pory rzeczy sensu. Jednak prawdopodobnie jest dobrym ilość kliknięcia i bardzo kilku kliknięć na zadaniach do wykonania ( **LI** zdarzeń).

Na podstawie tych formularza należy Twojej hipotezę, że niektórych użytkowników występują pomylić, która część interfejsu użytkownika nie jest aktywne i to, że kursor jest wstawiony do zaznaczonego tekstu, gdy znajduje się na elementy listy i ich ikony.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Może to być contrived przykład. Niemniej jednak użytkownik chce wprowadzić ulepszenia do aplikacji, a następnie wykonaj flighting wdrożenia do dostawać opinie użyteczności klientów na żywo.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumentacja dla monitorowania metryki aplikacji serwera
Jest to tangens, ponieważ scenariusz przedstawiona w tym samouczku dotyczy tylko aplikacji klienckiej. Jednak aby informacje były kompletne skonfigurujesz aplikacji po stronie serwera.

1. Kliknij prawym przyciskiem myszy **MultiChannelToDo** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów do ToDoApp*&lt;your_suffix >* > **Dodaj usługę Application Insights do projektu**.
2. W powłoce Git Zatwierdź i Wypchnij zmiany do rozwidlenia w serwisie GitHub. Następnie odczekaj klientów odświeżyć przeglądarkę.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Zamień zmiany wdrożonej aplikacji w środowisku produkcyjnym:

     . \swap — nazwa ToDoApp < your_suffix >

Gotowe.

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a>Zbadaj: Dodawanie tagów specyficzne dla miejsca do Twojej metryk aplikacji klienta
W tej sekcji skonfigurujesz miejsc wdrożenia różnych, aby wysłać dane telemetryczne specyficzne dla miejsca do tego samego zasobu usługi Application Insights. W ten sposób można łatwo zobaczyć efekt zmian aplikacji można porównać dane telemetryczne między ruchu z różnych miejsc (środowisk wdrażania). W tym samym czasie ruchu produkcyjnym można oddzielić od pozostałych dzięki czemu można kontynuować do monitorowania aplikacji produkcyjnych zgodnie z potrzebami.

Ponieważ w przypadku zbierania danych na zachowanie klienta będzie [dodać inicjatora telemetrii w kodzie JavaScript](../application-insights/app-insights-api-filtering-sampling.md) w index.cshtml. Jeśli chcesz przetestować wydajności po stronie serwera, na przykład, również należy podobnie w kodzie serwera (zobacz [aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk](../application-insights/app-insights-api-custom-events-metrics.md).

1. Najpierw należy dodać kodu bewteen dwa `//` komentarze poniżej w języku JavaScript zablokować ten zostanie dodany do `<heading>` tagu wcześniej.

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

    Powoduje, że ten kod inicjatora `appInsights` obiekt, aby dodać właściwość niestandardowa o nazwie `Environment` na każdą wysyłania danych telemetrycznych.
2. Następnie dodaj tej właściwości niestandardowej jako [gniazdo ustawienie](web-sites-staged-publishing.md#AboutConfiguration) dla aplikacji sieci web na platformie Azure. Aby to zrobić, uruchom następujące polecenia w sesji programu Git powłoki.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Plik Web.config w projekcie już definiuje `environment` ustawienia aplikacji. To ustawienie, gdy należy przetestować aplikację lokalnie, Twoje metryki zostanie oznaczone z `VS Debugger`. Jednak gdy Wypchnij zmiany do platformy Azure, Azure znajduje i używa `environment` aplikacji zamiast tego ustawienia w konfiguracji aplikacji sieci web, a Twoje metryki zostaną oznaczone tagiem `Production`.
3. Zatwierdź i Wypchnij zmiany kodu do rozwidlenia w witrynie GitHub, a następnie odczekaj dla użytkowników, aby używali nowych aplikacji (trzeba odświeżyć przeglądarkę). Trwa około 15 minut nową właściwość wyświetlani w szczegółowe dane aplikacji `MultiChannelToDo.Web` zasobów.

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. Teraz, przejdź do **niestandardowe zdarzenia** ponownie bloku i odfiltrować metryki `Environment=Production`. Teraz można wyświetlić wszystkich nowych zdarzeń niestandardowych w gnieździe produkcyjnym z tego filtru.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Kliknij przycisk **ulubione** przycisk, aby zapisać bieżące ustawienia Eksploratora metryk podobną **zdarzenia niestandardowe: produkcji**. Możesz łatwo przełączać się między tego widoku oraz widoku miejsca wdrożenia później.

   > [!TIP]
   > W celu wykonania analizy jeszcze bardziej skuteczne, należy wziąć pod uwagę [integrowanie zasobu usługi Application Insights z usługi Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a>Dodaj znaczniki specyficzne dla miejsca do Twojej metryki aplikacji serwera
Ponownie aby informacje były kompletne skonfigurujesz aplikacji po stronie serwera. W przeciwieństwie do aplikacji klienckiej, która jest instrumentowany w języku JavaScript tagi miejsca specyficzne dla aplikacji serwera są instrumentowane przy użyciu kodu platformy .NET.

1. Otwórz  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Dodaj blok kodu poniżej, bezpośrednio przed zamykający nawias klamrowy w przestrzeni nazw.

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
2. Popraw błędy rozpoznawania nazw, dodając `using` instrukcje poniżej na początku pliku:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Dodaj poniższy kod do początku `Application_Start()` metody:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Zatwierdź i Wypchnij zmiany kodu do rozwidlenia w witrynie GitHub, a następnie odczekaj dla użytkowników, aby używali nowych aplikacji (trzeba odświeżyć przeglądarkę). Trwa około 15 minut nową właściwość wyświetlani w szczegółowe dane aplikacji `MultiChannelToDo` zasobów.

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Aktualizacja: Konfigurowanie gałąź w wersji beta
1. Otwórz  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json i Znajdź `appsettings` zasobów (Wyszukaj `"name": "appsettings"`). Istnieją 4 z nich, po jednej dla każdego miejsca.
2. Dla każdego `appsettings` zasobów, Dodaj `"environment": "[parameters('slotName')]"` ustawienia aplikacji na końcu `properties` tablicy. Nie zapomnij o zakończenie poprzedniego wiersza przecinkami.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Dodany `environment` ustawienia aplikacji na wszystkich miejsc w szablonie.
3. W tym samym pliku, Znajdź `slotconfignames` zasobów (Wyszukaj `"name": "slotconfignames"`). Istnieją 2 z nich, po jednej dla każdej aplikacji.
4. Dla każdego `slotconfignames` zasobów, Dodaj `"environment"` na końcu `appSettingNames` tablicy. Nie zapomnij o zakończenie poprzedniego wiersza przecinkami.

    Zostały wprowadzone `environment` aplikacji ustawienie USB na jej miejsce wdrożenia odpowiednich dla obydwu aplikacji.  
5. W sesji programu Git powłoki uruchom następujące polecenia z tej samej grupy zasobów sufiks używany przed.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Po wyświetleniu monitu podaj tego samego SQL poświadczenia bazy danych jako przed. Następnie po otrzymaniu monitu, aby zaktualizować grupy zasobów, wpisz `Y`, następnie `ENTER`.

    Po zakończeniu skryptu, wszystkich zasobów w grupie zasobów oryginalnego zostaną zachowane, ale nowe miejsce o nazwie "beta" jest tworzony w nim z taką samą konfigurację jak miejsca "Tymczasowe", który został utworzony na początku.

   > [!NOTE]
   > Ta metoda tworzenia wdrożenia w różnych środowiskach różni się od metody w [Agile software development z usługi aplikacji Azure](app-service-agile-software-development.md). W tym miejscu Utwórz środowisk wdrażania z miejsc wdrożenia, w której jako utworzono środowisk wdrażania z grupami zasobów. Zarządzanie środowisk wdrażania z grupami zasobów pozwala na przechowywanie w środowisku produkcyjnym off-limits dla deweloperów, ale nie jest łatwe testowanie w środowisku produkcyjnym, co można zrobić w prosty sposób z miejsc.
   >
   >

W razie potrzeby, można również utworzyć aplikację alfa, uruchamiając

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

W tym samouczku użytkownik będzie tylko nadal używać aplikacji w wersji beta.

## <a name="update-push-your-updates-to-the-beta-app"></a>Aktualizacja: Wypychanie aktualizacji aplikacji w wersji beta
Powrót do aplikacji, który chcesz zwiększyć.

1. Upewnij się, że możesz teraz w gałęzi w wersji beta

        git checkout beta
2. W  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, Znajdź `<li>` tagu i Dodaj `style="cursor:pointer"` atrybutu, jak pokazano poniżej.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Zatwierdzanie i wypychania do platformy Azure.
4. Sprawdź, czy zmiany jest teraz widoczne w gnieździe w wersji beta przechodząc do http://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Jeśli nie widzisz jeszcze zmiany, Odśwież przeglądarkę, aby uzyskać nowy kod javascript.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Teraz, gdy masz zmiany w gnieździe w wersji beta można przystąpić do wykonania flighting wdrożenia.

## <a name="validate-route-traffic-to-the-beta-app"></a>Sprawdź poprawność: Kierować ruchem do aplikacji w wersji beta
W tej sekcji będzie kierować ruchem do aplikacji w wersji beta. For sake of przejrzystości demonstracyjnych możesz zacząć trasy znaczna część ruchu użytkowników do niego. W rzeczywistości ilość ruchu sieciowego, które chcesz rozesłać zależy od konkretnej sytuacji. Na przykład jeśli witryna jest na dużą skalę Microsoft.com, następnie konieczne może mniej niż jeden procent całkowitej ruchu w celu uzyskania przydatnych danych.

1. W sesji Git powłoki, uruchom następujące polecenia, aby kierować połowy ruchu produkcji do gniazda, w wersji beta:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   `ReroutePercentage=50` Właściwość określa, że 50% ruchu produkcyjnego będą kierowane do adresu URL aplikacji w wersji beta (określonego przez `ActionHostName` właściwości).
2. Teraz przejdź do http://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% ruchu teraz powinno nastąpić przekierowanie do gniazda, w wersji beta.
3. W zasobu usługi Application Insights, filtrować metryki przez środowisko = "beta".

   > [!NOTE]
   > Jeśli zapiszesz ten widok filtrowany jako ulubiony innego, można łatwo Przerzuć widoków Eksploratora metryk między produkcyjnego i widoków w wersji beta.
   >
   >

Załóżmy, że w usłudze Application Insights Zobacz podobny do następującego:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Nie tylko jest to wskazującą, że istnieje wiele więcej kliknięć na `<li>` tagi, ale wydaje się skoków kliknięć na `<li>` tagów. Następnie stwierdzić, że osoby odkryć nowe `<li>` znaczniki są aktywne i są teraz wyczyszczenie wszystkich ich wcześniej wykonać zadania w aplikacji.

Na podstawie danych flighting wdrożenia, możesz zdecydować, że Twój nowy interfejs użytkownika jest gotowa do produkcji.

## <a name="go-live-move-your-new-code-into-production"></a>Przejdź na żywo: Przenieś nowy kod do środowiska produkcyjnego
Teraz możesz przenieść aktualizacji do środowiska produkcyjnego. Co to jest doskonałym rozwiązaniem jest teraz wiesz, że aktualizacja została już sprawdzona *przed* zostanie przypisany do środowiska produkcyjnego. Dlatego teraz możesz mogą bezpiecznie wdrażać go. Ponieważ wprowadzono aktualizacji do aplikacji klienckiej AngularJS, sprawdzić poprawności tylko kod po stronie klienta. Jeśli masz zamiar dokonać zmian w aplikacji interfejsu API sieci Web zaplecza, można zweryfikować zmiany podobnie i łatwe.

1. W powłoce Git należy usunąć regułę routingu ruchu, uruchamiając następujące polecenie:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Uruchom polecenia Git:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Poczekaj kilka minut, aż nowy kod do wdrożenia dla miejsca przemieszczania, a następnie uruchom http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net, aby sprawdzić, czy nowa aktualizacja jest przygotowaniu miejsca, w miejsce wystawiania. Należy pamiętać, że Twoje rozwidlenia głównej gałęzi jest połączony z miejsca przemieszczania aplikacji.
4. Teraz Zamień miejsce wystawiania w środowisku produkcyjnym

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Podsumowanie
Usługa aplikacji Azure ułatwia dla małych — do średnich firm do testowania ich aplikacji dostępnych dla klienta w środowisku produkcyjnym, coś tradycyjnie wykonanej w dużych przedsiębiorstw. Mamy nadzieję, że w tym samouczku przyznał Ci wiedzy potrzebne ze sobą usługi aplikacji i usługi Application Insights flighting wdrażania, a także innych scenariuszy testów w środowisku produkcyjnym w sieci world DevOps.

## <a name="more-resources"></a>Więcej zasobów
* [Programowanie zwinne oprogramowania z usługi aplikacji Azure](app-service-agile-software-development.md)
* [Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych](web-sites-staged-publishing.md)
* [Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint — moduł sprawdzania poprawności JSON](http://jsonlint.com/)
* [Rozgałęzianie Git — podstawowe rozgałęzianie i scalanie](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Witryna typu Wiki Kudu projektu](https://github.com/projectkudu/kudu/wiki)
