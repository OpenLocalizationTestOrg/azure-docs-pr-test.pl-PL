---
title: aaaAzure Application Insights migawki debugera w przypadku aplikacji .NET | Dokumentacja firmy Microsoft
description: "Debugowanie migawki są zbierane automatycznie, gdy wyjątki zostaną zgłoszone w aplikacjach .NET produkcji"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Debugowanie migawek na wyjątków w aplikacji .NET

Po wystąpieniu wyjątku, można automatycznie zbierać migawki debugowania aplikacji sieci web na żywo. migawki Hello pokazuje stan hello kodu źródłowego i zmiennych w hello obecnie hello wyjątek został zgłoszony. Witaj migawki debugera (wersja zapoznawcza) w [Azure Application Insights](app-insights-overview.md) monitoruje dane telemetryczne wyjątku z aplikacji sieci web. Zbiera migawki na listy wyjątków zgłaszanie top, dzięki czemu masz hello informacje potrzebne toodiagnose problemów w środowisku produkcyjnym. Zawierają hello [pakietu NuGet modułu zbierającego migawki](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) w aplikacji i opcjonalnie skonfigurować parametry kolekcji w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Migawki są wyświetlane na [wyjątki](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights hello.

Można wyświetlić migawki debugowania w stosie wywołań hello portalu toosee hello i sprawdzić zmiennych w każdej ramki stosu wywołań. tooget bardziej wydajne działanie debugowania z kodem źródłowym, otwórz migawki z programu Visual Studio Enterprise 2017 przez [pobieranie hello debugera migawki rozszerzenia dla programu Visual Studio](https://aka.ms/snapshotdebugger).

Kolekcja migawki jest dostępny dla:
* Aplikacje środowiska .NET framework i program ASP.NET systemem .NET Framework 4.5 lub nowszej.
* .NET core 2.0 i ASP.NET Core 2.0 aplikacji uruchomionych w systemie Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Konfigurowanie zbierania migawek dla aplikacji ASP.NET

1. [Włącz usługę Application Insights w aplikacji sieci web](app-insights-asp-net.md), jeśli nie jeszcze go jeszcze gotowe.

2. Zawierają hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji. 

3. Przejrzyj opcje domyślne hello hello pakietu dodane za[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Migawki są zbierane tylko na wyjątki, które zostały zgłoszone tooApplication szczegółowych informacji. W niektórych przypadkach (na przykład starszych wersji platformy .NET hello) może być konieczne, zbyt[Konfigurowanie zbierania wyjątków](app-insights-asp-net-exceptions.md#exceptions) toosee wyjątki z migawkami w portalu hello.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Konfigurowanie zbierania migawek dla aplikacji platformy ASP.NET Core 2.0

1. [Włącz usługę Application Insights w aplikacji sieci web platformy ASP.NET Core](app-insights-asp-net-core.md), jeśli nie jeszcze go jeszcze gotowe.

2. Zawierają hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.

3. Modyfikowanie hello `ConfigureServices` metody w aplikacji `Startup` klasy tooadd hello migawki modułu zbierającego dane telemetryczne procesora. należy dodać kodu Hello zależy od hello wersja przywoływanego hello pakietu Microsoft.ApplicationInsights.ASPNETCore NuGet.

   W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.0 należy dodać:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   W przypadku Microsoft.ApplicationInsights.AspNetCore 2.1.1 należy dodać:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Konfigurowanie zbierania migawek dla innych aplikacji .NET

1. Jeśli aplikacja nie jest już instrumentowane przy użyciu usługi Application Insights, rozpoczęcie pracy przez [włączenie usługi Application Insights i ustawienie hello Instrumentacji klucza](app-insights-windows-desktop.md).

2. Dodaj hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pakietu NuGet w aplikacji.

3. Migawki są zbierane tylko na wyjątki, które zostały zgłoszone tooApplication szczegółowych informacji. Może być konieczne toomodify Twojego tooreport kodu je. Obsługa kodu wyjątków Hello zależy hello struktury aplikacji, ale przykładem jest poniżej:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Udzielanie uprawnień

Właściciele hello subskrypcji platformy Azure można sprawdzić migawki. Inni użytkownicy muszą mieć uprawnienie przez właściciela.

toogrant uprawnienia, przypisz hello `Application Insights Snapshot Debugger` toousers roli, który będzie przeprowadzał inspekcję migawki. Tę rolę można przypisać tooindividual użytkowników lub grup właściciele subskrypcji dla docelowego hello zasobu usługi Application Insights lub grupy zasobów lub subskrypcji.

1. Otwiera blok kontroli dostępu (IAM) hello.
1. Kliknij przycisk Dodaj + hello.
1. Wybierz debuger migawki Insights aplikacji z listy rozwijanej hello ról.
1. Wyszukaj, a następnie wprowadź nazwę hello tooadd użytkownika.
1. Kliknij przycisk Zapisz hello tooadd roli toohello użytkownika hello.


[!IMPORTANT]
    Migawki potencjalnie może zawierać informacje osobiste i innych poufnych w zmiennej i wartości parametrów.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Debugowanie migawek w portalu usługi Application Insights hello

Jeśli migawka jest dostępna dla danego wyjątku lub identyfikator problemu **Otwórz migawki debugowania** na powitania pojawi się przycisk [wyjątek](app-insights-asp-net-exceptions.md) w portalu usługi Application Insights hello.

![Przycisk Otwórz migawki debugowania na wyjątek](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

W widoku debugowania migawki hello Zobacz stosu wywołań i okienku zmiennych. Po wybraniu ramki wywołania hello stosu w okienku Stos wywołań hello, można wyświetlić zmiennych lokalnych i wywołać parametrów dla tej funkcji w okienku zmienne hello.

![Widok debugowania migawka w portalu hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Migawki mogą zawierać poufne informacje, i domyślnie nie są widoczne. migawki tooview musi mieć hello `Application Insights Snapshot Debugger` tooyou przypisanej roli.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Migawki z programu Visual Studio Enterprise 2017 debugowania
1. Kliknij przycisk hello **pobieranie migawki** toodownload przycisk `.diagsession` pliku, który można otworzyć w programie Visual Studio Enterprise 2017 r. 

2. Witaj tooopen `.diagsession` pliku, należy najpierw [Pobierz i zainstaluj rozszerzenie debugera migawki hello for Visual Studio](https://aka.ms/snapshotdebugger).

3. Po otwarciu pliku migawki hello, zostanie wyświetlona strona debugowania minizrzutu hello, w programie Visual Studio. Kliknij przycisk **debugowania kodu zarządzanego** toostart debugowania hello migawki. migawki Hello otwiera toohello wiersz kodu, w którym został zgłoszony wyjątek hello tak, aby umożliwić debugowanie hello bieżący stan procesu hello.

    ![Wyświetl migawkę debugowania w programie Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

migawki pobrany Hello zawiera wszystkie pliki symboli, które zostały odnalezione na serwerze aplikacji sieci web. Te pliki symboli są wymagane tooassociate dane migawki z kodem źródłowym. Dla aplikacji usługi aplikacji upewnij się, że wdrożenie symbol tooenable podczas publikowania aplikacji sieci web.

## <a name="how-snapshots-work"></a>Jak działają migawki

Podczas uruchamiania aplikacji, tworzony jest proces przesyłania oddzielne migawki, który monitoruje aplikację żądań migawki. Po zażądaniu migawki kopii w tle hello uruchomiony proces jest przeprowadzane w około 10 minut too20. proces tle Hello następnie są analizowane i migawki jest tworzony podczas hello główny proces jest kontynuowany toorun i obsługiwać ruch toousers. Witaj migawka jest następnie przekazane tooApplication Insights wraz z odpowiednimi symboli (.pdb) pliki, które są potrzebne tooview hello migawki.

## <a name="current-limitations"></a>Bieżące ograniczenia

### <a name="publish-symbols"></a>Publikuj symbole
Witaj debugera migawki wymaga plików symboli na zmiennych toodecode serwera produkcyjnego hello i tooprovide działanie debugowania w programie Visual Studio. Witaj 15,2 wersji programu Visual Studio 2017 publikuje symboli dla kompilacji wydania domyślnie po jej opublikowaniu tooApp usługi. W poprzednich wersjach, należy tooadd hello następujące profilu publikowania tooyour wiersza `.pubxml` plików symboli są publikowane w trybie wersji:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

W przypadku rozwiązań usługi obliczenia Azure i innych typów zapewnić pliki symboli hello hello tego samego folderu .dll głównej aplikacji hello (zazwyczaj `wwwroot/bin`) lub są dostępne w bieżącej ścieżce hello.

### <a name="optimized-builds"></a>Zoptymalizowane kompilacji
W niektórych przypadkach zmiennych lokalnych nie można wyświetlić w kompilacjach wydania z powodu optymalizacji, które są stosowane podczas procesu kompilacji hello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Te wskazówki ułatwiają rozwiązywanie problemów z hello debugera migawki.

### <a name="verify-hello-instrumentation-key"></a>Sprawdź hello klucza Instrumentacji

Upewnij się, że używasz klucza Instrumentacji poprawne hello w opublikowanej aplikacji. Zazwyczaj usługi Application Insights odczytuje hello klucza Instrumentacji z hello pliku ApplicationInsights.config. Upewnij się, że wartość hello jest sama hello jako klucz Instrumentacji hello hello zasobu usługi Application Insights, które widać w portalu hello.

### <a name="check-hello-uploader-logs"></a>Sprawdź dzienniki przesyłania hello

Po utworzeniu migawki, plik minizrzutu (dmp) jest tworzony na dysku. Proces przesyłania oddzielne przyjmuje ten plik minizrzutu i przekazuje, oraz wszystkie skojarzone pliki PDB tooApplication magazynu debugera migawki szczegółowych informacji. Po pomyślnym przekazaniu minizrzutu hello są usuwane z dysku. pliki dziennika Hello przekazujący minizrzutu hello są przechowywane na dysku. W środowisku usługi aplikacji można znaleźć te dzienniki w `D:\Home\LogFiles\Uploader_*.log`. Użyj hello Kudu zarządzania witryny dla usług aplikacji toofind te pliki dziennika.

1. Otwórz aplikację usługi aplikacji w hello portalu Azure.

2. Wybierz hello **zaawansowane narzędzia** bloku lub Wyszukaj **Kudu**.
3. Kliknij przycisk **Przejdź**.
4. W hello **konsoli debugowania** listy rozwijanej wybierz pozycję **CMD**.
5. Kliknij przycisk **LogFiles**.

Powinny pojawić się co najmniej jeden plik o nazwie, który rozpoczyna się od `Uploader_` i `.log` rozszerzenia. Kliknij przycisk toodownload odpowiednią ikonę hello wszystkie pliki dziennika lub je otworzyć w przeglądarce.
Nazwa pliku Hello zawiera hello nazwy komputera. Jeśli wystąpienie usługi aplikacji znajduje się na więcej niż jednej maszynie, istnieją oddzielnych plików dziennika dla każdego komputera. Gdy moduł przesyłający hello wykryje nowy plik minizrzutu, jest rejestrowany w pliku dziennika hello. Oto przykład pomyślne ukończenie przekazywania:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

W poprzednim przykładzie hello jest klucza Instrumentacji hello `c12a605e73c44346a984e00000000000`. Ta wartość powinna być zgodna hello klucza instrumentacji aplikacji.
Witaj minizrzutu jest skojarzony z migawki o identyfikatorze hello `139e411a23934dc0b9ea08a626db16c5`. Można użyć tego Identyfikatora nowsze hello toolocate skojarzone dane telemetryczne dotyczące wyjątków w aplikacji Analytics szczegółowych informacji.

Moduł przesyłający Hello skanowania pod kątem nowych baz danych PDB o co 15 minut. Oto przykład:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Dla aplikacji, które są _nie_ hostowanych w usłudze App Service, są dzienniki przesyłania hello hello tym samym folderze co minizrzutów hello: `%TEMP%\Dumps\<ikey>` (gdzie `<ikey>` jest klucz Instrumentacji).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Użyj Application Insights wyszukiwania toofind wyjątki z migawkami

Po utworzeniu migawki hello Zgłaszanie wyjątku jest oznaczone przy użyciu identyfikatora migawki. Telemetria wyjątków powitania po Insights tooApplication zgłoszone ten identyfikator migawki jest uwzględniona jako właściwości niestandardowej. Za pomocą bloku wyszukiwania hello w usłudze Application Insights, można znaleźć wszystkie dane telemetryczne z hello `ai.snapshot.id` właściwości niestandardowej.

1. Przeglądaj tooyour zasobu usługi Application Insights w hello portalu Azure.
2. Kliknij przycisk **wyszukiwania**.
3. Typ `ai.snapshot.id` w polu tekstowym wyszukiwania hello i naciśnij klawisz Enter.

![Wyszukaj dane telemetryczne z Identyfikatorem migawki w portalu hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Jeśli to wyszukiwanie nie zwróciło żadnych wyników, migawek nie zostały zgłoszone tooApplication Insights dla aplikacji hello wybrany zakres czasu.

w polu wyszukiwania hello toosearch identyfikator określoną migawkę z dzienników przesyłania hello, wpisz ten identyfikator. Jeśli nie możesz znaleźć dane telemetryczne dla migawki, który został przekazany, wykonaj następujące kroki:

1. Sprawdź, czy przeglądania hello prawo zasobu usługi Application Insights, upewniając hello klucza instrumentacji.

2. Przy użyciu sygnatury czasowej hello z dziennika przekazujący hello, Dostosuj filtru zakresu czasu hello toocover wyszukiwania hello zakresu czasu.

Jeśli nadal nie widać Wystąpił wyjątek o takim identyfikatorze migawki, hello dane telemetryczne dotyczące wyjątków nie został zgłoszony tooApplication szczegółowych informacji. Taka sytuacja może się zdarzyć, jeśli awaria aplikacji po zajęło hello migawki, ale przed zgłosiła ona hello dane telemetryczne dotyczące wyjątków. W takim przypadku sprawdź hello dzienniki usługi aplikacji w obszarze `Diagnose and solve problems` toosee Jeśli wystąpiły nieoczekiwane ponowne uruchomienie lub nieobsługiwane wyjątki.

## <a name="next-steps"></a>Następne kroki

* [Ustaw snappoints w kodzie](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) migawki tooget bez oczekiwania na wyjątek.
* [Diagnozowanie wyjątków w aplikacjach sieci web](app-insights-asp-net-exceptions.md) wyjaśniono, jak toomake więcej widocznych wyjątki tooApplication szczegółowych informacji. 
* [Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie odnajduje anomalii wydajności.
