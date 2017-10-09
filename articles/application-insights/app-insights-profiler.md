---
title: "aaaProfiling aplikacji sieci web na platformie Azure za pomocą usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Zidentyfikować hello aktywnej ścieżki w kodzie serwera sieci web za pomocą profilera niskiego poziomu."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Profilowanie aplikacji sieci web platformy Azure na żywo za pomocą usługi Application Insights

*Ta funkcja usługi Application Insights jest GA dla usług aplikacji i w wersji zapoznawczej obliczania.*

Sprawdzić, ile jest czas w każdej metodzie w aplikacji sieci web na żywo przy użyciu hello profilowania narzędzie [Azure Application Insights](app-insights-overview.md). Pokazuje szczegółowe profile bieżących żądań, które zostały obsłużone przez aplikację, a wyróżnia hello "gorących path", który używa hello większość czasu. Powoduje automatyczne wybranie przykłady, które mają czasy odpowiedzi na inny. Hello profiler używa różnych technik toominimize koszty.

Witaj profilera obecnie działa w przypadku platformy ASP.NET sieci web aplikacji działających na usługi aplikacji Azure, w co najmniej hello Basic warstwy cenowej. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Włącz hello profilera

[Zainstaluj usługi Application Insights](app-insights-asp-net.md) w kodzie. Jeśli jest już zainstalowany, upewnij się, że masz hello najnowszej wersji. (toodo, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz pakiety zarządzania pakietami NuGet. Wybierz aktualizacje i wszystkich pakietów aktualizacji). Wdróż ponownie aplikację.

*Przy użyciu platformy ASP.NET Core? [Sprawdź tutaj](#aspnetcore).*

W [https://portal.azure.com](https://portal.azure.com), otwórz hello zasobu usługi Application Insights dla aplikacji sieci web. Otwórz **wydajności** i kliknij przycisk **włączyć profilera Insights aplikacji...** .

![Witaj, kliknij polecenie Włącz transparent profilera][enable-profiler-banner]

Alternatywnie możesz zawsze kliknąć **Konfiguruj** tooview stan, włączanie lub wyłączanie hello profilera.

![W bloku wydajności hello kliknij przycisk Konfiguruj][performance-blade]

Aplikacje sieci Web, które są skonfigurowane przy użyciu usługi Application Insights są wyświetlane w bloku Konfigurowanie. Postępuj zgodnie z instrukcjami tooinstall hello profilera agenta w razie potrzeby. Jeśli żadnej aplikacji sieci web jest skonfigurowana jeszcze z usługą Application Insights, kliknij przycisk *Dodaj aplikacje połączone*.

Użyj hello *włączyć profilera* lub *wyłączanie profilera* przyciski w toocontrol bloku Konfigurowanie hello hello profilera na wszystkie aplikacje sieci web połączonej.



![Skonfiguruj bloku][linked app services]

toostop lub ponownego uruchomienia profilera powitania dla poszczególnych wystąpień usługi aplikacji, znajdziesz ją **w hello zasobów usługi aplikacji**w **zadania Web Job**. toodelete jej wygląd w obszarze **rozszerzenia**.

![Wyłącz program profilujący do zadania sieci web][disable-profiler-webjob]

Zaleca się, że masz hello profilera włączone na wszystkich sieci web aplikacji toodiscover wszelkie problemy z wydajnością dotyczące tak szybko, jak to możliwe.

Użycie aplikacji sieci web tooyour WebDeploy toodeploy zmiany, upewnij się, czy wykluczyć hello **App_Data** folderu przed usunięciem podczas wdrażania. W przeciwnym razie hello rozszerzenia profilera pliki zostaną usunięte podczas wdrażania obok tooAzure aplikacji sieci web hello.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Przy użyciu profilera z maszynami wirtualnymi Azure i zasobów obliczeniowych (wersja zapoznawcza)

Gdy użytkownik [Włącz usługi Application Insights dla usługi Azure aplikacji w czasie wykonywania](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler jest automatycznie dostępny. (Jeśli jeszcze włączone usługi Application Insights dla zasobu hello, potrzebna wersja lates toohello tooupdate za pośrednictwem hello **Konfiguruj** kreatora.)

Brak [wersję zapoznawczą hello profilera dla rozwiązań usługi obliczenia Azure zasobów](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Limity

przechowywanie danych domyślne Hello jest 5 dni. Maksymalna pozyskanych dziennie 10 GB.

Jest bezpłatna dla hello usługi profilera. Aplikacja sieci web musi być obsługiwana przez co najmniej hello podstawowe warstwy usług aplikacji.

## <a name="viewing-profiler-data"></a>Wyświetlanie danych profilera

Otwórz hello wydajności bloku i przewiń w dół listy operacji toohello.




![Blok Insights wydajności aplikacji przykłady kolumny][performance-blade-examples]

Witaj kolumny w tabeli hello są:

* **Liczba** — Witaj liczba tych żądań w zakresie czasu hello hello bloku.
* **Mediana** -hello typowe czasie aplikacji toorespond tooa żądania. Połowa wszystkich odpowiedzi zostały szybciej niż to.
* **95. percentyl** 95% odpowiedzi zostały szybciej niż to. Jeśli tego rysunku jest bardzo różnią się od medianę hello, może to być tymczasowy problem z aplikacją. (Lub może być wyjaśnione przy użyciu funkcji projektu, takie jak buforowanie.)
* **Przykłady** — ikona wskazuje, że profiler hello zostały przechwycone dane śledzenia stosu dla tej operacji.

Kliknij przycisk hello przykłady ikona tooopen hello śledzenia explorer. Pokazuje Eksploratora Hello przechwycone ma kilka przykłady, które hello profilera, sklasyfikowane przez czas odpowiedzi.

Wybierz tooshow przykładowy podział poziomie kodu czas spędzony wykonywania hello żądania.

![Eksplorator śledzenia usługi Application Insights][trace-explorer]

**Pokaż ścieżkę aktywną** otwiera hello największych węzeł liścia lub co najmniej coś zamknąć. W większości przypadków ten węzeł będzie sąsiadujących ze sobą tooa wąskie gardło.



* **Etykieta**: hello nazwę funkcji hello lub zdarzeń. drzewo Hello zawiera zarówno kod i zdarzenia (takie jak zdarzenia SQL i http). zdarzenia najwyższego Hello reprezentuje ogólną hello czas trwania żądania.
* **Upłynął**: hello odstęp czasu między rozpoczęciem hello hello i na końcu hello.
* **Gdy**: Pokazuje, kiedy hello funkcji lub zdarzenia został uruchomiony w ramach funkcji tooother relacji.

## <a name="how-tooread-performance-data"></a>Jak tooread danych wydajności

Profilera usługi firmy Microsoft używa kombinacji próbkowania — metoda i instrumentacji tooanalyze hello wydajność aplikacji.
Gdy szczegółowe kolekcji jest w toku, przykłady profilera usługi hello wskaźnik instrukcji każdego Procesora hello maszyny w każdym milisekund.
Każda próbka przechwytuje hello stosu wywołań zakończenie wątku hello aktualnie wykonywane, podając szczegółowe i przydatne informacje o tym, co, że wątek wykonywanych zarówno na poziomie wysoki i niski poziom abstrakcji. Usługi profiler zbiera również inne zdarzenia, takie jak zdarzenia przełączania kontekstu, zdarzenia TPL i korelacji działania tootrack zdarzenia puli wątków i przyczynowości.

stos wywołań Hello pokazywane w widoku osi czasu hello jest wynikiem hello hello powyżej próbkowania i instrumentacji. Ponieważ każdy przykład przechwytuje hello stosu wywołań zakończenie wątku hello, zawiera kod z hello .NET framework, a także innych platform, do którego odwołuje.

### <a id="jitnewobj"></a>Obiekt alokacji (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`są funkcje pomocnicze wewnątrz przydziela pamięć z sterty zarządzanej .NET framework. `clr!JIT\_New`wywoływane, gdy obiekt jest przydzielony. `clr!JIT\_Newarr1`wywoływane, gdy przydzielone jest Tablica obiektów. Te dwie funkcje są zazwyczaj bardzo szybko i powinno zająć względnie krótkim czasie. Jeśli widzisz `clr!JIT\_New` lub `clr!JIT\_Newarr1` trwać dość czasu na osi czasu, to wskazanie, że hello kodu mogą być Alokacja wiele obiektów i zużywa dużo pamięci.

### <a id="theprestub"></a>Podczas ładowania kodu (`clr!ThePreStub`)
`clr!ThePreStub`jest to funkcja pomocnika wewnątrz .NET framework, który przygotowuje tooexecute kodu hello powitania po raz pierwszy. Zwykle obejmuje to między innymi, kompilacja JIT (tylko w czasie). W przypadku każdego C# metody `clr!ThePreStub` powinna być wywoływana co najwyżej raz podczas hello istnienia procesu.

Jeśli widzisz `clr!ThePreStub` zajmuje dużo czasu dla żądania, oznacza to żądanie jest hello pierwszej wykonuje metody, a czas hello .NET framework środowisko uruchomieniowe tooload, czy metoda jest znacząca. Należy wziąć pod uwagę rozgrzewania procesu, który wykonuje część kodu hello przed użytkowników do niego dostęp, lub rozważ użycie polecenia NGen z zestawów.

### <a id="lockcontention"></a>Blokowanie rywalizacji (`clr!JITutil\_MonContention` lub `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`lub `clr!JITutil\_MonEnterWorker` wskazać hello bieżący wątek oczekuje na toobe blokady, wydane. To zwykle zostaną wyświetlone podczas wykonywania C# instrukcji "lock", wywołania metody Monitor.Enter lub wywołania metody z atrybutem MethodImplOptions.Synchronized. Rywalizacji blokad zazwyczaj ma miejsce, gdy wątek A uzyskuje blokadę i wątku B próbuje hello tooacquire sam zablokować przed zwolnieniem wątku A.

### <a id="ngencold"></a>Podczas ładowania kodu (`[COLD]`)
Jeśli nazwa metody hello zawiera `[COLD]`, takich jak `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, oznacza to środowisko uruchomieniowe tego hello platformy .NET framework jest wykonywany kod, który nie jest zoptymalizowana przez <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">Optymalizacja sterowana profilem</a> dla powitania po raz pierwszy. Dla każdej metody go powinny być widoczne co najwyżej jeden raz w okresie istnienia hello hello procesu.

Ładowania kodu zajmuje dużo czasu na żądanie, wskazuje, to żądanie jest hello pierwszy tooexecute jeden hello zoptymalizowanego część hello metody. Należy wziąć pod uwagę ciepłych proces wykonujący część hello kodu, zanim do niego dostęp przez użytkowników.

### <a id="httpclientsend"></a>Wysyłanie żądania HTTP
Metody, takie jak `HttpClient.Send` wskazuje kod hello oczekuje na toocomplete żądania HTTP.

### <a id="sqlcommand"></a>Operacja bazy danych
Metoda, takich jak SqlCommand.Execute wskazuje, że kod hello oczekuje na toocomplete operacji bazy danych.

### <a id="await"></a>Oczekiwanie (`AWAIT\_TIME`)
`AWAIT\_TIME`Wskazuje, że kod hello oczekuje na inną toocomplete zadań. Zwykle dzieje się z C# "await" instrukcji. Gdy nie istniał hello kodu C# "await", hello wątku cofa i zwraca kontroli toohello z puli wątków oraz jest nie wątku, który jest zablokowana i czeka na toofinish "await" hello. Jednak logicznie hello wątku, że została hello await "zablokowaniu" Oczekiwanie na powitania toocomplete operacji. `AWAIT\_TIME` Wskazuje hello zablokowane czasu oczekiwania na powitania toocomplete zadań.

### <a id="block"></a>Czas blokowania
`BLOCKED_TIME`Wskazuje, że kod hello oczekuje na inną toobe zasobów dostępnych, takich jak oczekiwania na obiekt synchronizacji, oczekiwania wątku toobe dostępne lub Oczekiwanie toofinish żądania.

### <a id="cpu"></a>Czas procesora CPU
Witaj procesora CPU jest zajęty wykonywaniem instrukcji hello.

### <a id="disk"></a>Czas dysku
Aplikacja Hello wykonuje operacje dysku.

### <a id="network"></a>Czas sieci
Aplikacja Hello jest przeprowadzanie operacji sieciowych.

### <a id="when"></a>Gdy kolumny
Jest to wizualizację jak hello przykłady włącznie zbierane dla węzła w zależności od wraz z upływem czasu. 32 przedziałów czasu jest podzielony zakres łączny Hello hello żądania i hello włącznie przykłady dla tego węzła jest zebranych w tych zasobników 32. Każdy zasobnika następnie jest reprezentowany jako pasek, którego wysokość reprezentuje skalowaną wartość. Dla węzłów oznaczone `CPU_TIME` lub `BLOCKED_TIME`, lub w przypadku relacji oczywiste korzystanie z zasobów (procesora, dysku, wątek), hello paska reprezentuje korzystanie z jednego z tych zasobów hello okres czasu tego zasobnika. Dla tych metryk możesz uzyskać większa niż 100% przez korzystanie z wielu zasobów. Na przykład jeśli średnio Użyj dwa procesory przedziałach, możesz uzyskać 200%.


## <a id="troubleshooting"></a>Rozwiązywanie problemów

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Jak sprawdzić, czy działa profilera usługi Application Insights?

Hello profiler jest uruchamiany jako zadanie web ciągły w aplikacji sieci Web. Można otwierać hello zasobów aplikacji sieci Web w https://portal.azure.com i sprawdzić stan "ApplicationInsightsProfiler" w bloku zadania Webjob hello. Jeśli nie jest uruchomiony, otwórz **dzienniki** toofind się więcej.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Dlaczego nie można odnaleźć przykładami stosu, mimo że hello profiler działa?

Oto kilka rzeczy, które można sprawdzić.

1. Upewnij się, że sieci Web planu usługi aplikacji jest warstwy podstawowa lub nowszym.
2. Upewnij się, aplikacja sieci Web ma Application Insights SDK 2.2 Beta i powyżej włączyć.
3. Upewnij się, że aplikacja sieci Web ma ustawienie APPINSIGHTS_INSTRUMENTATIONKEY hello z hello tego samego klucza Instrumentacji używane przez zestaw SDK usługi Application Insights.
4. Upewnij się, że aplikacja sieci Web jest uruchomiona na platformie .net Framework 4.6.
5. Jeśli jest to aplikacja platformy ASP.NET Core, Sprawdź również, czy [hello wymagane zależności](#aspnetcore).

Po rozpoczęciu profilera hello jest okres rozgrzewania krótkich po hello profiler zbiera aktywnie kilka śledzenia wydajności. Po wykonaniu tej profilera hello zbieranie śladów wydajności przez dwie minuty w co godzinę.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Został przy użyciu profilera usługi Azure. Jakie happened tooit?  

Po włączeniu Application Insights profilera agenta profilera usługi Azure jest wyłączona.

### <a id="double-counting"></a>Zliczanie w równoległych wątków o podwójnej precyzji

W niektórych przypadkach hello Metryka całkowity czas w podglądzie stosu hello jest większa niż rzeczywisty czas trwania hello hello żądania.

Może się to zdarzyć, gdy istnieją dwa lub więcej wątków skojarzony z żądaniem, równoległe. czas całkowita liczba wątków Hello następnie jest większa niż czas, który upłynął hello. W wielu przypadkach jeden wątek może być oczekiwanie na hello innych toocomplete. to Hello toodetect prób podglądu i Pomiń Zaczekaj postrzegać hello, ale errs po stronie powitania przedstawiający zbyt dużo zamiast pominięcie, co może być ważnych informacji.  

Po wyświetleniu równoległych wątków w dane śledzenia, należy toodetermine, który wątków oczekujących, dzięki czemu można określić ścieżkę krytyczną hello hello żądania. W większości przypadków szybko po prostu oczekuje przechodzi w stan oczekiwania na wątek hello hello inne wątki. Skoncentrować się na inne hello i Ignoruj czas hello w hello wątków oczekujących.

### <a id="issue-loading-trace-in-viewer"></a>Nie danych profilowania

1. Jeśli próbujesz danych hello tooview jest starsza niż kilka tygodni, spróbuj ograniczyć czas filtru i spróbuj ponownie.

2. Sprawdź, czy serwery proxy lub zapora nie zablokowane toohttps://gateway.azureserviceprofiler.net dostępu.

3. Sprawdź, że hello usługi Application Insights jest klucza instrumentacji, używanym w aplikacji hello takie same jak hello zasobu usługi Application Insights, które włączono profilowanie z. klucz Hello zazwyczaj znajduje się w ApplicationInsights.config, ale można także znaleźć w pliku web.config lub app.config.

### <a name="error-report-in-hello-profiling-viewer"></a>Raport o błędach w hello profilowania podglądu

Plik biletu pomocy technicznej z hello portalu. Podaj identyfikator korelacji hello z komunikat o błędzie hello.

## <a name="manual-installation"></a>Instalacja ręczna

Po skonfigurowaniu profilera hello hello następujące aktualizacje zostały wprowadzone ustawienia aplikacji sieci Web toohello. Można wykonać je samodzielnie ręcznie, jeśli dane środowisko wymaga na przykład, jeśli aplikacja działa w środowisku usługi aplikacji Azure (ASE):

1. W bloku kontroli aplikacji sieci web hello Otwórz okno Ustawienia.
2. Ustaw ".Net Framework w wersji" toov4.6.
3. Ustaw tooOn "Zawsze włączone".
4. Dodaj ustawienie aplikacji "__APPINSIGHTS_INSTRUMENTATIONKEY__" i toohello wartość hello zestawu tego samego klucza Instrumentacji używane przez hello zestawu SDK.
5. Otwieranie zaawansowanych narzędzi.
6. Kliknij przycisk "Przejdź do" z witryny sieci Web Kudu tooopen hello.
7. Wybierz "Lokacji rozszerzenia" hello Kudu witryny sieci Web.
8. Zainstaluj "__usługi Application Insights__" z galerii.
9. Uruchom ponownie hello aplikacji sieci web.

## <a id="aspnetcore"></a>Obsługa platformy ASP.NET Core

Aplikacja platformy ASP.NET Core musi tooinstall 2.1.0-beta6 pakietu Microsoft.ApplicationInsights.AspNetCore Nuget lub wyższej toowork z hello profilera. Nie obsługujemy hello niższych wersjach po 2017-6/27.

## <a name="next-steps"></a>Następne kroki

* [Praca z usługi Application Insights w programie Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
