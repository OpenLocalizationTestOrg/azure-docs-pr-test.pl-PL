---
title: aaaDebug aplikacji w programie Visual Studio | Dokumentacja firmy Microsoft
description: "Zwiększyć hello niezawodność i wydajność usług przez opracowywania i debugowania je w programie Visual Studio na lokalny klaster projektowy."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Debugowanie aplikacji lokalnej sieci szkieletowej usług
Wdrażanie i debugowanie aplikacji sieci szkieletowej usług Azure w klastrze programowanie komputer lokalny, można oszczędzić czas i pieniądze. Visual Studio 2017 lub programu Visual Studio 2015 można wdrożyć klaster lokalny toohello aplikacji hello i automatycznie nawiążą połączenie hello debugera tooall wystąpień aplikacji.

1. Uruchom lokalnego klastra projektowego, wykonując kroki hello w [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started.md).
2. Naciśnij klawisz **F5** lub kliknij przycisk **debugowania** > **Rozpocznij debugowanie**.
   
    ![Rozpocznij debugowanie aplikacji][startdebugging]
3. Ustaw punkty przerwania w kodzie i kroku przy użyciu aplikacji hello przez kliknięcie polecenia w hello **debugowania** menu.
   
   > [!NOTE]
   > Visual Studio dołącza tooall wystąpień aplikacji. Gdy jest krokowe kodu, punkty przerwania napotkać uzyskać przez wiele procesów, co powoduje równoczesnych sesji. Spróbuj wyłączyć hello punktów przerwania po ich jest trafienie dzięki uzależnione identyfikator wątku hello każdy punkt przerwania lub za pomocą zdarzeń diagnostycznych.
   > 
   > 
4. Witaj **zdarzeń diagnostycznych** automatycznie zostanie otwarte okno, aby umożliwić przeglądanie zdarzeń diagnostycznych w czasie rzeczywistym.
   
    ![Wyświetl zdarzenia diagnostycznego w czasie rzeczywistym][diagnosticevents]
5. Można również otworzyć hello **zdarzeń diagnostycznych** okna w Eksploratorze chmury.  W obszarze **sieci szkieletowej usług**, kliknij prawym przyciskiem myszy dowolny węzeł lub wybrać **śladów przesyłania strumieniowego widoku**.
   
    ![Otwórz hello okna zdarzeń diagnostycznych][viewdiagnosticevents]
   
    Jeśli chcesz toofilter śladów tooa określonej usługi lub aplikacji, po prostu włącz śladów przesyłania strumieniowego dla tej określonej usługi lub aplikacji.
6. zdarzeń diagnostycznych Hello są widoczne w hello są generowane automatycznie **ServiceEventSource.cs** pliku i jest wywoływana przez kod aplikacji.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Witaj **zdarzeń diagnostycznych** okna obsługuje filtrowanie, wstrzymywanie i zapoznanie się zdarzenia w czasie rzeczywistym.  Filtr Hello jest prosty ciąg wyszukiwania komunikatu o zdarzeniu hello, w tym jego zawartość.
   
    ![Filtrowanie, wstrzymać i wznowić lub sprawdzić zdarzenia w czasie rzeczywistym][diagnosticeventsactions]
8. Debugowanie usług przypomina profilowanie innej aplikacji. Łatwe debugowanie zwykle ustawi punktów przerwania za pomocą programu Visual Studio. Mimo że kolekcje niezawodnej replikowanie w wielu węzłach, nadal implementować interfejs IEnumerable. Oznacza to, której można hello widok wyników w programie Visual Studio podczas debugowania toosee co został zapisany w. Wystarczy ustawić punkt przerwania w kodzie w dowolnym miejscu.
   
    ![Rozpocznij debugowanie aplikacji][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Debugowania zdalnego aplikacji sieci szkieletowej usług
Jeśli aplikacji sieci szkieletowej usług są uruchomione w klastrze usługi sieć szkieletowa na platformie Azure, jesteś w stanie tooremotely debugowania je bezpośrednio z programu Visual Studio.

> [!NOTE]
> Funkcja Hello wymaga [usługi sieć szkieletowa SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) i [zestawu Azure SDK dla programu .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Zdalne debugowanie jest przeznaczona dla scenariusze tworzenia/testowania i nie toobe używane w środowisku produkcyjnym ze względu na wpływ hello na powitania uruchamiania aplikacji.
> 
> 

1. Przejdź tooyour klastra w **Eksplorator chmury**, kliknij prawym przyciskiem myszy i wybierz opcję **włączenia debugowania**
   
    ![Włącz debugowanie zdalne][enableremotedebugging]
   
    To spowoduje zaczną działać poza hello proces włączania hello zdalnego debugowania rozszerzenia na węzły klastra, a także wymagane konfiguracje sieci.
2. Kliknij prawym przyciskiem myszy węzeł klastra hello w **Eksplorator chmury**i wybierz polecenie **dołączanie debugera**
   
    ![Dołączanie debugera][attachdebugger]
3. W hello **dołączyć tooprocess** okno dialogowe, wybierz proces hello toodebug i kliknij **Dołącz**
   
    ![Wybierz proces][chooseprocess]
   
    Nazwa Hello procesu hello ma tooattach do, równa się hello nazwa nazwy zestawu projektu usługi.
   
    Witaj debuger będzie dołączać węzłów tooall uruchomienie procesu hello.
   
   * W przypadku hello gdzie debugowania usługi bezstanowej wszystkie wystąpienia usługi hello we wszystkich węzłach są częścią hello sesji debugowania.
   * Jeśli debugujesz usługi stanowej, tylko hello repliki podstawowej dowolnej partycji będzie aktywny i w związku z tym zgłoszony przez debuger hello. Jeśli replika podstawowa hello przenosi podczas sesji debugowania hello, przetwarzania hello tej repliki nadal będzie częścią hello sesji debugowania.
   * W kolejności tooonly catch odpowiednich partycji lub wystąpienia danej usługi można użyć podziału tooonly warunkowych punktów przerwania określonej partycji lub wystąpienia.
     
     ![Warunkowych punktów przerwania][conditionalbreakpoint]
     
     > [!NOTE]
     > Obecnie nie obsługujemy debugowanie klastra sieci szkieletowej usług z wielu wystąpień hello tej samej nazwy pliku wykonywalnego usługi.
     > 
     > 
4. Po zakończeniu debugowania aplikacji, klikając prawym przyciskiem myszy klaster hello w można wyłączyć rozszerzenia debugowania zdalnego hello **Eksplorator chmury** i wybierz polecenie **Wyłącz debugowanie**
   
    ![Wyłącz debugowanie zdalne][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Przesyłanie strumieniowe danych śledzenia przy użyciu węzła klastra zdalnego
Ma również stanie toostream ślady bezpośrednio z klastra zdalnego węzła tooVisual w Studio. Ta funkcja umożliwia toostream ETW śledzenia zdarzeń, utworzony na węźle klastra sieci szkieletowej usług.

> [!NOTE]
> Ta funkcja wymaga [usługi sieć szkieletowa SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) i [zestawu Azure SDK dla programu .NET 2.9](https://azure.microsoft.com/downloads/).
> Ta funkcja obsługuje tylko klastry działające na platformie Azure.
> 
> 

<!-- -->
> [!WARNING]
> Przesyłanie strumieniowe danych śledzenia jest przeznaczona dla scenariusze tworzenia/testowania i nie toobe używane w środowisku produkcyjnym ze względu na wpływ hello na powitania uruchamiania aplikacji.
> W scenariuszu produkcyjnym polegać na przekazywanie zdarzeń za pomocą diagnostyki Azure.
> 
> 

1. Przejdź tooyour klastra w **Eksplorator chmury**, kliknij prawym przyciskiem myszy i wybierz opcję **włączyć śledzenie przesyłania strumieniowego**
   
    ![Włącz zdalne śladów przesyłania strumieniowego][enablestreamingtraces]
   
    To spowoduje zaczną działać poza hello proces włączania hello przesyłania strumieniowego rozszerzenia ślady na węzły klastra, a także wymagane konfiguracje sieci.
2. Rozwiń hello **węzłów** element **Eksplorator chmury**, kliknij prawym przyciskiem myszy hello węzeł ma śladów toostream z i wybierz polecenie **widoku śladów przesyłania strumieniowego**
   
    ![Widok zdalnego przesyłania strumieniowego śledzenia][viewremotestreamingtraces]
   
    Powtórz krok 2 dla węzłów dowolną liczbę można dowolnie śladów toosee z. Każdego strumienia węzłów zostaną wyświetlone w oknie dedykowanych.
   
    Jesteś teraz możliwe toosee hello śladów emitowane przez usługi Service Fabric i usług. Jeśli chcesz toofilter hello zdarzenia tooonly Pokaż określonej aplikacji, wystarczy wpisać hello Nazwa aplikacji hello w filtrze hello.
   
    ![Wyświetlanie przesyłania strumieniowego śledzenia][viewingstreamingtraces]
3. Po zakończeniu przesyłania strumieniowego śladów z klastra, można wyłączyć zdalnego ślady przesyłania strumieniowego, klikając prawym przyciskiem myszy klaster hello w **Eksplorator chmury** i wybierz polecenie **Wyłącz śledzenie przesyłania strumieniowego**
   
    ![Wyłącz zdalne śladów przesyłania strumieniowego][disablestreamingtraces]

## <a name="next-steps"></a>Następne kroki
* [Testowanie usługi sieć szkieletowa usług](service-fabric-testability-overview.md).
* [Zarządzaj aplikacjami sieci szkieletowej usług w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
