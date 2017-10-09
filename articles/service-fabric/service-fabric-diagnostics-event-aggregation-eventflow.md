---
title: "Usługi sieci szkieletowej zdarzeń agregacji z EventFlow aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat agregowania i zbierania zdarzeń przy użyciu EventFlow monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="7be23-103">Agregacja zdarzeń i kolekcji przy użyciu EventFlow</span><span class="sxs-lookup"><span data-stu-id="7be23-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="7be23-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) może kierować zdarzenia z tooone węzła lub więcej monitorowania miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="7be23-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="7be23-105">Ponieważ jest uwzględniona jako pakietu NuGet w projekcie usługi, EventFlow kod i konfiguracja są przesyłane z usługą hello, eliminując problem z konfiguracją każdego węzła hello wymienione wcześniej o diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="7be23-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="7be23-106">EventFlow jest uruchamiany w ramach procesu usługi i łączy się bezpośrednio toohello skonfigurowany w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7be23-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="7be23-107">Ze względu na powitania bezpośrednie połączenie EventFlow działa platformy Azure, kontenera i lokalnego wdrożenia usługi.</span><span class="sxs-lookup"><span data-stu-id="7be23-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="7be23-108">Należy zachować ostrożność, jeśli uruchomisz EventFlow w scenariuszach wysokiej gęstości, takich jak w kontenerze, ponieważ każdy potoku EventFlow sprawia, że połączenie zewnętrzne.</span><span class="sxs-lookup"><span data-stu-id="7be23-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="7be23-109">Tak Jeśli host kilka procesów, możesz uzyskać kilka połączeń wychodzących!</span><span class="sxs-lookup"><span data-stu-id="7be23-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="7be23-110">Nie jest to tyle problemem w przypadku aplikacji usługi Service Fabric, ponieważ wszystkie repliki `ServiceType` Uruchom w hello tego samego procesu, i ogranicza hello liczby połączeń wychodzących.</span><span class="sxs-lookup"><span data-stu-id="7be23-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="7be23-111">EventFlow oferuje również filtrowanie zdarzeń, tak aby były wysyłane tylko zdarzenia hello zgodne hello określony filtr.</span><span class="sxs-lookup"><span data-stu-id="7be23-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="7be23-112">Konfigurowanie EventFlow</span><span class="sxs-lookup"><span data-stu-id="7be23-112">Setting up EventFlow</span></span>

<span data-ttu-id="7be23-113">Pliki binarne EventFlow są dostępne jako zestaw pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="7be23-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="7be23-114">tooadd EventFlow tooa projektu usługi Service Fabric, kliknij prawym przyciskiem myszy projekt hello w hello Eksploratorze rozwiązań i wybierz polecenie "Manage NuGet packages".</span><span class="sxs-lookup"><span data-stu-id="7be23-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="7be23-115">Przełącz kartę "Przeglądaj" toohello i wyszukaj "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="7be23-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pakiety EventFlow NuGet w interfejs użytkownika Menedżera pakietów NuGet usługi Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="7be23-117">Zostanie wyświetlona lista pakietów różnych wyświetlani, etykietą "Danych wejściowych" i "Generuje".</span><span class="sxs-lookup"><span data-stu-id="7be23-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="7be23-118">EventFlow obsługuje różne analizatory i rejestrowania różnych dostawców.</span><span class="sxs-lookup"><span data-stu-id="7be23-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="7be23-119">Usługa Hello hosting EventFlow powinna zawierać odpowiednie pakiety w zależności od hello źródłowego i docelowego dla dzienników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7be23-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="7be23-120">Ponadto toohello core ServiceFabric pakietu, należy również co najmniej jeden przychodzących i wychodzących, skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="7be23-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="7be23-121">W przypadku exmaple można dodać następujące pakiety toosent EventSource zdarzenia tooApplication Insights hello:</span><span class="sxs-lookup"><span data-stu-id="7be23-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="7be23-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture danych z klasy EventSource hello usługi i EventSources standardowe, takie jak *usługi ServiceFabric* i *Microsoft-ServiceFabric-podmiotów*)</span><span class="sxs-lookup"><span data-stu-id="7be23-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="7be23-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(zamierzamy toosend hello dzienniki tooan Azure Application Insights zasobów)</span><span class="sxs-lookup"><span data-stu-id="7be23-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="7be23-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(umożliwia inicjowanie potoku EventFlow hello z konfiguracji usługi Service Fabric i raporty problemów z wysyłaniem danych diagnostycznych jako raportów o kondycji sieci szkieletowej usług)</span><span class="sxs-lookup"><span data-stu-id="7be23-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="7be23-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`pakiet wymaga tootarget projektu usługi hello .NET Framework 4.6 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="7be23-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="7be23-126">Upewnij się, że platforma docelowa odpowiednie hello jest ustawiona we właściwościach projektu przed instalacją tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="7be23-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="7be23-127">Po wszystkich hello pakiety są zainstalowane, następnym krokiem hello jest tooconfigure i Włącz EventFlow w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="7be23-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="7be23-128">Konfigurowanie i włączanie zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="7be23-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="7be23-129">potok EventFlow Hello jest odpowiedzialny za wysyłanie dzienników hello jest tworzona na podstawie specyfikacji przechowywane w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7be23-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="7be23-130">Witaj `Microsoft.Diagnostics.EventFlow.ServiceFabric` pakiet instaluje plik początkowej konfiguracji EventFlow pod `PackageRoot\Config` folder rozwiązania o nazwie `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="7be23-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="7be23-131">Ten plik konfiguracyjny musi toobe zmodyfikować toocapture danych z usługi domyślne hello `EventSource` klasy i wszystkie inne dane wejściowe tooconfigure, a następnie Wyślij dane toohello odpowiednie miejsce.</span><span class="sxs-lookup"><span data-stu-id="7be23-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="7be23-132">Poniżej przedstawiono przykładowe *eventFlowConfig.json* oparte na powitania pakietów NuGet wymienionych powyżej:</span><span class="sxs-lookup"><span data-stu-id="7be23-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="7be23-133">Nazwa Hello ServiceEventSource usługi jest hello wartość właściwości Name elementu hello hello `EventSourceAttribute` stosowane toohello ServiceEventSource klasy.</span><span class="sxs-lookup"><span data-stu-id="7be23-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="7be23-134">Wszystkie określono w hello `ServiceEventSource.cs` pliku, który jest częścią hello kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="7be23-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="7be23-135">Na przykład na powitania następujący kod fragment hello nazwa hello ServiceEventSource to *Moja firma-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="7be23-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="7be23-136">Należy pamiętać, że `eventFlowConfig.json` plik jest częścią pakietu konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="7be23-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="7be23-137">Plik toothis zmiany mogą być zawarte w pełnej lub Konfiguracja — tylko do uaktualnienia usługi hello, tooService temat sieci szkieletowej uaktualnienia kontroli kondycji i automatycznego wycofania w przypadku niepowodzenia uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="7be23-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="7be23-138">Aby uzyskać więcej informacji, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="7be23-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="7be23-139">Witaj *filtry* sekcji konfiguracji hello umożliwia toofurther dostosować informacje hello toogo będzie hello EventFlow potoku toohello danych wyjściowych w, dzięki czemu toodrop uwzględnienia niektórych informacji lub zmienić hello Struktura hello danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7be23-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="7be23-140">Aby uzyskać więcej informacji dotyczących filtrowania, zobacz [filtry EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="7be23-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="7be23-141">Ostatnim krokiem Hello jest tooinstantiate EventFlow potoku w kodzie uruchamiania usługi, znajduje się w `Program.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="7be23-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="7be23-142">Nazwa Hello przekazywana jako parametr hello hello `CreatePipeline` metody hello `ServiceFabricDiagnosticsPipelineFactory` jest nazwą hello hello *jednostki kondycji* reprezentujący hello EventFlow dziennika kolekcji potoku.</span><span class="sxs-lookup"><span data-stu-id="7be23-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="7be23-143">Ta nazwa jest używana, jeśli EventFlow napotkał błąd i zgłasza za pośrednictwem hello podsystemu kondycji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7be23-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="7be23-144">Przy użyciu ustawień sieci szkieletowej usług oraz eventFlowConfig tooin parametry aplikacji</span><span class="sxs-lookup"><span data-stu-id="7be23-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="7be23-145">Obsługuje EventFlow przy użyciu ustawień sieci szkieletowej usług oraz ustawienia EventFlow tooconfigure parametry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7be23-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="7be23-146">Może się odwoływać parametrów ustawień sieci szkieletowej tooService przy użyciu tej składni specjalne wartości:</span><span class="sxs-lookup"><span data-stu-id="7be23-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="7be23-147">`<section-name>`to nazwa hello hello sekcji konfiguracji sieci szkieletowej usług, i `<setting-name>` jest ustawienie konfiguracji hello podawania wartości hello, które będzie używane tooconfigure ustawienie EventFlow.</span><span class="sxs-lookup"><span data-stu-id="7be23-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="7be23-148">więcej informacji na temat tooread toodo, przejdź zbyt[obsługę ustawień sieci szkieletowej usług i aplikacji parametry](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="7be23-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="7be23-149">Weryfikacja</span><span class="sxs-lookup"><span data-stu-id="7be23-149">Verification</span></span>

<span data-ttu-id="7be23-150">Uruchomić usługę i sprawdź hello debugowania okno dane wyjściowe w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7be23-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="7be23-151">Po uruchomieniu usługi hello powinny zacząć się wyświetlać się, że dowód, który wysyła usługi rejestruje dane wyjściowe toohello, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="7be23-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="7be23-152">Przejdź tooyour zdarzenie analizy i wizualizacji platformy i upewnij się, że dzienniki rozpoczęły tooshow up (może to potrwać kilka minut).</span><span class="sxs-lookup"><span data-stu-id="7be23-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7be23-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7be23-153">Next steps</span></span>

* [<span data-ttu-id="7be23-154">Analiza zdarzeń i wizualizacji z usługą Application Insights</span><span class="sxs-lookup"><span data-stu-id="7be23-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="7be23-155">Analiza zdarzeń i wizualizacji z OMS</span><span class="sxs-lookup"><span data-stu-id="7be23-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="7be23-156">Dokumentacja EventFlow</span><span class="sxs-lookup"><span data-stu-id="7be23-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)