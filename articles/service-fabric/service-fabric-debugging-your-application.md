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
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="c4166-103">Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4166-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4166-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="c4166-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="c4166-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="c4166-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="c4166-106">Debugowanie aplikacji lokalnej sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4166-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="c4166-107">Wdrażanie i debugowanie aplikacji sieci szkieletowej usług Azure w klastrze programowanie komputer lokalny, można oszczędzić czas i pieniądze.</span><span class="sxs-lookup"><span data-stu-id="c4166-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="c4166-108">Visual Studio 2017 lub programu Visual Studio 2015 można wdrożyć klaster lokalny toohello aplikacji hello i automatycznie nawiążą połączenie hello debugera tooall wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="c4166-109">Uruchom lokalnego klastra projektowego, wykonując kroki hello w [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4166-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="c4166-110">Naciśnij klawisz **F5** lub kliknij przycisk **debugowania** > **Rozpocznij debugowanie**.</span><span class="sxs-lookup"><span data-stu-id="c4166-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Rozpocznij debugowanie aplikacji][startdebugging]
3. <span data-ttu-id="c4166-112">Ustaw punkty przerwania w kodzie i kroku przy użyciu aplikacji hello przez kliknięcie polecenia w hello **debugowania** menu.</span><span class="sxs-lookup"><span data-stu-id="c4166-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4166-113">Visual Studio dołącza tooall wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="c4166-114">Gdy jest krokowe kodu, punkty przerwania napotkać uzyskać przez wiele procesów, co powoduje równoczesnych sesji.</span><span class="sxs-lookup"><span data-stu-id="c4166-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="c4166-115">Spróbuj wyłączyć hello punktów przerwania po ich jest trafienie dzięki uzależnione identyfikator wątku hello każdy punkt przerwania lub za pomocą zdarzeń diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c4166-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="c4166-116">Witaj **zdarzeń diagnostycznych** automatycznie zostanie otwarte okno, aby umożliwić przeglądanie zdarzeń diagnostycznych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c4166-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Wyświetl zdarzenia diagnostycznego w czasie rzeczywistym][diagnosticevents]
5. <span data-ttu-id="c4166-118">Można również otworzyć hello **zdarzeń diagnostycznych** okna w Eksploratorze chmury.</span><span class="sxs-lookup"><span data-stu-id="c4166-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="c4166-119">W obszarze **sieci szkieletowej usług**, kliknij prawym przyciskiem myszy dowolny węzeł lub wybrać **śladów przesyłania strumieniowego widoku**.</span><span class="sxs-lookup"><span data-stu-id="c4166-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Otwórz hello okna zdarzeń diagnostycznych][viewdiagnosticevents]
   
    <span data-ttu-id="c4166-121">Jeśli chcesz toofilter śladów tooa określonej usługi lub aplikacji, po prostu włącz śladów przesyłania strumieniowego dla tej określonej usługi lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="c4166-122">zdarzeń diagnostycznych Hello są widoczne w hello są generowane automatycznie **ServiceEventSource.cs** pliku i jest wywoływana przez kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="c4166-123">Witaj **zdarzeń diagnostycznych** okna obsługuje filtrowanie, wstrzymywanie i zapoznanie się zdarzenia w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c4166-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="c4166-124">Filtr Hello jest prosty ciąg wyszukiwania komunikatu o zdarzeniu hello, w tym jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="c4166-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtrowanie, wstrzymać i wznowić lub sprawdzić zdarzenia w czasie rzeczywistym][diagnosticeventsactions]
8. <span data-ttu-id="c4166-126">Debugowanie usług przypomina profilowanie innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="c4166-127">Łatwe debugowanie zwykle ustawi punktów przerwania za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4166-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="c4166-128">Mimo że kolekcje niezawodnej replikowanie w wielu węzłach, nadal implementować interfejs IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="c4166-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="c4166-129">Oznacza to, której można hello widok wyników w programie Visual Studio podczas debugowania toosee co został zapisany w.</span><span class="sxs-lookup"><span data-stu-id="c4166-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="c4166-130">Wystarczy ustawić punkt przerwania w kodzie w dowolnym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c4166-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Rozpocznij debugowanie aplikacji][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="c4166-132">Debugowania zdalnego aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4166-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="c4166-133">Jeśli aplikacji sieci szkieletowej usług są uruchomione w klastrze usługi sieć szkieletowa na platformie Azure, jesteś w stanie tooremotely debugowania je bezpośrednio z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4166-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="c4166-134">Funkcja Hello wymaga [usługi sieć szkieletowa SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) i [zestawu Azure SDK dla programu .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c4166-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="c4166-135">Zdalne debugowanie jest przeznaczona dla scenariusze tworzenia/testowania i nie toobe używane w środowisku produkcyjnym ze względu na wpływ hello na powitania uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="c4166-136">Przejdź tooyour klastra w **Eksplorator chmury**, kliknij prawym przyciskiem myszy i wybierz opcję **włączenia debugowania**</span><span class="sxs-lookup"><span data-stu-id="c4166-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Włącz debugowanie zdalne][enableremotedebugging]
   
    <span data-ttu-id="c4166-138">To spowoduje zaczną działać poza hello proces włączania hello zdalnego debugowania rozszerzenia na węzły klastra, a także wymagane konfiguracje sieci.</span><span class="sxs-lookup"><span data-stu-id="c4166-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="c4166-139">Kliknij prawym przyciskiem myszy węzeł klastra hello w **Eksplorator chmury**i wybierz polecenie **dołączanie debugera**</span><span class="sxs-lookup"><span data-stu-id="c4166-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Dołączanie debugera][attachdebugger]
3. <span data-ttu-id="c4166-141">W hello **dołączyć tooprocess** okno dialogowe, wybierz proces hello toodebug i kliknij **Dołącz**</span><span class="sxs-lookup"><span data-stu-id="c4166-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Wybierz proces][chooseprocess]
   
    <span data-ttu-id="c4166-143">Nazwa Hello procesu hello ma tooattach do, równa się hello nazwa nazwy zestawu projektu usługi.</span><span class="sxs-lookup"><span data-stu-id="c4166-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="c4166-144">Witaj debuger będzie dołączać węzłów tooall uruchomienie procesu hello.</span><span class="sxs-lookup"><span data-stu-id="c4166-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="c4166-145">W przypadku hello gdzie debugowania usługi bezstanowej wszystkie wystąpienia usługi hello we wszystkich węzłach są częścią hello sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="c4166-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="c4166-146">Jeśli debugujesz usługi stanowej, tylko hello repliki podstawowej dowolnej partycji będzie aktywny i w związku z tym zgłoszony przez debuger hello.</span><span class="sxs-lookup"><span data-stu-id="c4166-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="c4166-147">Jeśli replika podstawowa hello przenosi podczas sesji debugowania hello, przetwarzania hello tej repliki nadal będzie częścią hello sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="c4166-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="c4166-148">W kolejności tooonly catch odpowiednich partycji lub wystąpienia danej usługi można użyć podziału tooonly warunkowych punktów przerwania określonej partycji lub wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="c4166-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Warunkowych punktów przerwania][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="c4166-150">Obecnie nie obsługujemy debugowanie klastra sieci szkieletowej usług z wielu wystąpień hello tej samej nazwy pliku wykonywalnego usługi.</span><span class="sxs-lookup"><span data-stu-id="c4166-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="c4166-151">Po zakończeniu debugowania aplikacji, klikając prawym przyciskiem myszy klaster hello w można wyłączyć rozszerzenia debugowania zdalnego hello **Eksplorator chmury** i wybierz polecenie **Wyłącz debugowanie**</span><span class="sxs-lookup"><span data-stu-id="c4166-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Wyłącz debugowanie zdalne][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="c4166-153">Przesyłanie strumieniowe danych śledzenia przy użyciu węzła klastra zdalnego</span><span class="sxs-lookup"><span data-stu-id="c4166-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="c4166-154">Ma również stanie toostream ślady bezpośrednio z klastra zdalnego węzła tooVisual w Studio.</span><span class="sxs-lookup"><span data-stu-id="c4166-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="c4166-155">Ta funkcja umożliwia toostream ETW śledzenia zdarzeń, utworzony na węźle klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c4166-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="c4166-156">Ta funkcja wymaga [usługi sieć szkieletowa SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) i [zestawu Azure SDK dla programu .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c4166-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="c4166-157">Ta funkcja obsługuje tylko klastry działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c4166-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="c4166-158">Przesyłanie strumieniowe danych śledzenia jest przeznaczona dla scenariusze tworzenia/testowania i nie toobe używane w środowisku produkcyjnym ze względu na wpływ hello na powitania uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4166-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="c4166-159">W scenariuszu produkcyjnym polegać na przekazywanie zdarzeń za pomocą diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="c4166-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="c4166-160">Przejdź tooyour klastra w **Eksplorator chmury**, kliknij prawym przyciskiem myszy i wybierz opcję **włączyć śledzenie przesyłania strumieniowego**</span><span class="sxs-lookup"><span data-stu-id="c4166-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Włącz zdalne śladów przesyłania strumieniowego][enablestreamingtraces]
   
    <span data-ttu-id="c4166-162">To spowoduje zaczną działać poza hello proces włączania hello przesyłania strumieniowego rozszerzenia ślady na węzły klastra, a także wymagane konfiguracje sieci.</span><span class="sxs-lookup"><span data-stu-id="c4166-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="c4166-163">Rozwiń hello **węzłów** element **Eksplorator chmury**, kliknij prawym przyciskiem myszy hello węzeł ma śladów toostream z i wybierz polecenie **widoku śladów przesyłania strumieniowego**</span><span class="sxs-lookup"><span data-stu-id="c4166-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Widok zdalnego przesyłania strumieniowego śledzenia][viewremotestreamingtraces]
   
    <span data-ttu-id="c4166-165">Powtórz krok 2 dla węzłów dowolną liczbę można dowolnie śladów toosee z.</span><span class="sxs-lookup"><span data-stu-id="c4166-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="c4166-166">Każdego strumienia węzłów zostaną wyświetlone w oknie dedykowanych.</span><span class="sxs-lookup"><span data-stu-id="c4166-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="c4166-167">Jesteś teraz możliwe toosee hello śladów emitowane przez usługi Service Fabric i usług.</span><span class="sxs-lookup"><span data-stu-id="c4166-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="c4166-168">Jeśli chcesz toofilter hello zdarzenia tooonly Pokaż określonej aplikacji, wystarczy wpisać hello Nazwa aplikacji hello w filtrze hello.</span><span class="sxs-lookup"><span data-stu-id="c4166-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Wyświetlanie przesyłania strumieniowego śledzenia][viewingstreamingtraces]
3. <span data-ttu-id="c4166-170">Po zakończeniu przesyłania strumieniowego śladów z klastra, można wyłączyć zdalnego ślady przesyłania strumieniowego, klikając prawym przyciskiem myszy klaster hello w **Eksplorator chmury** i wybierz polecenie **Wyłącz śledzenie przesyłania strumieniowego**</span><span class="sxs-lookup"><span data-stu-id="c4166-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Wyłącz zdalne śladów przesyłania strumieniowego][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="c4166-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4166-172">Next steps</span></span>
* <span data-ttu-id="c4166-173">[Testowanie usługi sieć szkieletowa usług](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4166-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="c4166-174">[Zarządzaj aplikacjami sieci szkieletowej usług w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="c4166-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
