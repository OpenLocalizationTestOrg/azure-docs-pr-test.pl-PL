---
title: "Dzienniki aaaCollect bezpośrednio z usługi Azure Service Fabric procesu usługi | Microsoft Azure"
description: "W tym artykule opisano aplikacje będą mogły wysyłać dzienniki bezpośrednio tooa centralnej lokalizacji, takich jak Azure Application Insights lub Elasticsearch, bez polegania na agencie diagnostyki Azure sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="faa76-103">Zbieranie dzienników bezpośrednio z procesu usługi sieć szkieletowa usług Azure</span><span class="sxs-lookup"><span data-stu-id="faa76-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="faa76-104">W trakcie zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="faa76-104">In-process log collection</span></span>
<span data-ttu-id="faa76-105">Zbieranie aplikacji dzienników przy użyciu [rozszerzenia diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) jest dobra opcja w przypadku **sieć szkieletowa usług Azure** usług Jeśli zbiór hello dziennika źródeł i miejsc docelowych jest mały, nie zmieni często, a jest prosta mapowania między hello źródeł i ich miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="faa76-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="faa76-106">Jeśli nie jest to alternatywa usług toohave ich wysłania dzienników przez użytkownika bezpośrednio tooa centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="faa76-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="faa76-107">Ten proces jest nazywany **zbierania dzienników w trakcie** i ma wiele potencjalnych korzyści:</span><span class="sxs-lookup"><span data-stu-id="faa76-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="faa76-108">*Łatwe konfigurowanie i wdrażanie*</span><span class="sxs-lookup"><span data-stu-id="faa76-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="faa76-109">Konfiguracja Hello zbierania danych diagnostycznych jest tylko część hello konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="faa76-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="faa76-110">Należy zachować łatwe tooalways go "zsynchronizowane" z hello pozostałej części aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="faa76-111">Dla każdej aplikacji lub na usługi konfiguracji jest łatwo osiągalny.</span><span class="sxs-lookup"><span data-stu-id="faa76-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="faa76-112">Zbieranie danych dziennika agenta na podstawie zwykle wymaga oddzielnego wdrażania i konfiguracji agenta diagnostyki hello, zadanie bardzo administracyjne i potencjalne źródła błędów.</span><span class="sxs-lookup"><span data-stu-id="faa76-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="faa76-113">Często istnieje tylko jedno wystąpienie agenta hello dozwolonych dla jednej maszyny wirtualnej (węzeł) i konfiguracja agenta hello jest współdzielona przez wszystkie aplikacje i usługi uruchomione w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="faa76-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="faa76-114">*Elastyczność*</span><span class="sxs-lookup"><span data-stu-id="faa76-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="faa76-115">Aplikacja Hello może wysyłać dane hello wszędzie tam, gdzie musi toogo, tak długo, jak istnieje biblioteki klienckiej, która obsługuje system przechowywania danych hello docelowe.</span><span class="sxs-lookup"><span data-stu-id="faa76-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="faa76-116">Można dodać nowych miejsc docelowych pożądane.</span><span class="sxs-lookup"><span data-stu-id="faa76-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="faa76-117">Złożone zasady przechwytywania, filtrowania i agregacja danych może być zaimplementowany.</span><span class="sxs-lookup"><span data-stu-id="faa76-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="faa76-118">Zbieranie danych dziennika agenta na podstawie często jest ograniczona przez hello sink danych, które hello obsługuje agenta.</span><span class="sxs-lookup"><span data-stu-id="faa76-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="faa76-119">Niektóre agenci są rozszerzalne.</span><span class="sxs-lookup"><span data-stu-id="faa76-119">Some agents are extensible.</span></span>

* <span data-ttu-id="faa76-120">*Uzyskiwanie dostępu do danych aplikacji toointernal i kontekstu*</span><span class="sxs-lookup"><span data-stu-id="faa76-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="faa76-121">Podsystem diagnostycznych Hello uruchomiony proces aplikacji/usługi hello można łatwo rozszerzyć hello śladów z informacje kontekstowe.</span><span class="sxs-lookup"><span data-stu-id="faa76-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="faa76-122">Z kolekcją dziennika agenta na podstawie danych hello należy wysłać tooan agenta za pomocą mechanizmu komunikacji międzyprocesowej takich jak zdarzenia śledzenia systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="faa76-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="faa76-123">Ten mechanizm można skonfigurować dodatkowe ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="faa76-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="faa76-124">Jest możliwe toocombine i korzystać z obu metod kolekcji.</span><span class="sxs-lookup"><span data-stu-id="faa76-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="faa76-125">W rzeczywistości może być hello najlepsze rozwiązanie dla wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="faa76-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="faa76-126">Na podstawie agenta kolekcji to rozwiązanie fizyczne do zbierania dzienników toohello powiązane całego klastra, a poszczególne węzły klastra.</span><span class="sxs-lookup"><span data-stu-id="faa76-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="faa76-127">To znacznie bardziej niezawodny sposób, niż zbierania dzienników w procesie, problemy z uruchamianiem usługi toodiagnose i awarii.</span><span class="sxs-lookup"><span data-stu-id="faa76-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="faa76-128">Ponadto z wielu usług uruchomionych w klastrze usługi sieć szkieletowa, każda usługa swoją własną kolekcję dziennika w trakcie wykonywania powoduje wiele połączeń wychodzących z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="faa76-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="faa76-129">Duża liczba połączeń wychodzących jest opodatkowania zarówno w przypadku hello podsystemu sieci, jak i miejsce docelowe dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="faa76-130">Agent, takich jak [ **diagnostyki Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) można zebrać dane z wielu usług i Wyślij wszystkie dane za pośrednictwem połączenia kilku, poprawy przepływności.</span><span class="sxs-lookup"><span data-stu-id="faa76-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="faa76-131">W tym artykule zostanie przedstawiony sposób tooset w proces logowania przy użyciu kolekcji [ **biblioteki open source EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="faa76-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="faa76-132">Inne biblioteki mogą być używane dla hello sam cel, ale EventFlow ma zaletą hello o został zaprojektowany specjalnie z myślą w trakcie dziennika kolekcji i toosupport usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="faa76-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="faa76-133">Używamy [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) jako miejsce docelowe dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="faa76-134">Innych miejsc docelowych, takich jak [ **usługi Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) lub [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) również są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="faa76-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="faa76-135">Jest po prostu pytanie zainstalowania odpowiedniego pakietu NuGet i skonfigurowania hello docelowy w pliku konfiguracyjnym EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="faa76-136">Aby uzyskać więcej informacji dotyczących miejsc docelowych dziennika innego niż usługi Application Insights, zobacz [dokumentacji EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="faa76-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="faa76-137">Dodawanie projektu usługi Service Fabric tooa EventFlow biblioteki</span><span class="sxs-lookup"><span data-stu-id="faa76-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="faa76-138">Pliki binarne EventFlow są dostępne jako zestaw pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="faa76-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="faa76-139">tooadd EventFlow tooa projektu usługi Service Fabric, kliknij prawym przyciskiem myszy projekt hello w hello Eksploratorze rozwiązań i wybierz polecenie "Manage NuGet packages".</span><span class="sxs-lookup"><span data-stu-id="faa76-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="faa76-140">Przełącz kartę "Przeglądaj" toohello i wyszukaj "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="faa76-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pakiety EventFlow NuGet w interfejs użytkownika Menedżera pakietów NuGet usługi Visual Studio][1]

<span data-ttu-id="faa76-142">Usługa Hello hosting EventFlow powinna zawierać odpowiednie pakiety w zależności od hello źródłowego i docelowego dla dzienników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="faa76-143">Dodaj hello następujące pakiety:</span><span class="sxs-lookup"><span data-stu-id="faa76-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="faa76-144">(toocapture danych z klasy EventSource hello usługi i EventSources standardowe, takie jak *usługi ServiceFabric* i *Microsoft-ServiceFabric-podmiotów*)</span><span class="sxs-lookup"><span data-stu-id="faa76-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="faa76-145">(zamierzamy toosend hello dzienniki tooan Azure Application Insights zasobów)</span><span class="sxs-lookup"><span data-stu-id="faa76-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="faa76-146">(umożliwia inicjowanie potoku EventFlow hello z konfiguracji usługi Service Fabric i raporty problemów z wysyłaniem danych diagnostycznych jako raportów o kondycji sieci szkieletowej usług)</span><span class="sxs-lookup"><span data-stu-id="faa76-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="faa76-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`pakiet wymaga tootarget projektu usługi hello .NET Framework 4.6 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="faa76-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="faa76-148">Upewnij się, że platforma docelowa odpowiednie hello jest ustawiona we właściwościach projektu przed instalacją tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="faa76-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="faa76-149">Po wszystkich hello pakiety są zainstalowane, następnym krokiem hello jest tooconfigure i Włącz EventFlow w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="faa76-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="faa76-150">Konfigurowanie i włączanie zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="faa76-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="faa76-151">Potok EventFlow odpowiedzialny za wysyłanie dzienników hello jest tworzona na podstawie specyfikacji przechowywane w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="faa76-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="faa76-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`Pakiet instaluje plik początkowej konfiguracji EventFlow pod `PackageRoot\Config` folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="faa76-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="faa76-153">Nazwa pliku Hello jest `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="faa76-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="faa76-154">Ten plik konfiguracyjny musi toobe zmodyfikować toocapture danych z usługi domyślne hello `EventSource` klasy i wysyłania usługi Insights tooApplication danych.</span><span class="sxs-lookup"><span data-stu-id="faa76-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="faa76-155">Przyjęto założenie, że czytelnik zna **Azure Application Insights** service i czy masz zasobu usługi Application Insights planowanie toouse toomonitor usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="faa76-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="faa76-156">Aby uzyskać więcej informacji, zobacz [utworzyć zasobu usługi Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="faa76-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="faa76-157">Otwórz hello `eventFlowConfig.json` w edytorze hello i zmieniać jego zawartości, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="faa76-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="faa76-158">Upewnij się, że nazwa ServiceEventSource hello tooreplace i zgodnie z toocomments klucza Instrumentacji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="faa76-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="faa76-159">Nazwa Hello ServiceEventSource usługi jest hello wartość właściwości Name elementu hello hello `EventSourceAttribute` stosowane toohello ServiceEventSource klasy.</span><span class="sxs-lookup"><span data-stu-id="faa76-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="faa76-160">Wszystkie określono w hello `ServiceEventSource.cs` pliku, który jest częścią hello kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="faa76-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="faa76-161">Na przykład na powitania następujący kod fragment hello nazwa hello ServiceEventSource to *Moja firma-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="faa76-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="faa76-162">Należy pamiętać, że `eventFlowConfig.json` plik jest częścią pakietu konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="faa76-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="faa76-163">Plik toothis zmiany mogą być zawarte w pełnej lub Konfiguracja — tylko do uaktualnienia usługi hello, tooService temat sieci szkieletowej uaktualnienia kontroli kondycji i automatycznego wycofania w przypadku niepowodzenia uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="faa76-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="faa76-164">Aby uzyskać więcej informacji, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="faa76-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="faa76-165">Ostatnim krokiem Hello jest tooinstantiate EventFlow potoku w kodzie uruchamiania usługi, znajduje się w `Program.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="faa76-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="faa76-166">Hello następującymi dodatkami związanych z EventFlow przykład są oznaczane komentarze, począwszy od `****`:</span><span class="sxs-lookup"><span data-stu-id="faa76-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="faa76-167">Nazwa Hello przekazywana jako parametr hello hello `CreatePipeline` metody hello `ServiceFabricDiagnosticsPipelineFactory` jest nazwą hello hello *jednostki kondycji* reprezentujący hello EventFlow dziennika kolekcji potoku.</span><span class="sxs-lookup"><span data-stu-id="faa76-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="faa76-168">Ta nazwa jest używana, jeśli EventFlow napotkał błąd i zgłasza za pośrednictwem hello podsystemu kondycji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="faa76-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="faa76-169">Weryfikacja</span><span class="sxs-lookup"><span data-stu-id="faa76-169">Verification</span></span>
<span data-ttu-id="faa76-170">Uruchomić usługę i sprawdź hello debugowania okno dane wyjściowe w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="faa76-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="faa76-171">Po uruchomieniu usługi hello powinny zacząć się wyświetlać dowód, że usługa wysyła rekordy "Telemetrię usługi Application Insights".</span><span class="sxs-lookup"><span data-stu-id="faa76-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="faa76-172">Otwórz przeglądarkę sieci web i przejdź tooyour przejście zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="faa76-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="faa76-173">Otwórz kartę "Wyszukaj" (u góry hello hello domyślne "Overview" bloku).</span><span class="sxs-lookup"><span data-stu-id="faa76-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="faa76-174">Z niewielkim opóźnieniem powinny zacząć się wyświetlać dane śledzenia w portalu usługi Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="faa76-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Portal usługi Application Insights wyświetlanie dzienników aplikacji sieci szkieletowej usług][2]

## <a name="next-steps"></a><span data-ttu-id="faa76-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="faa76-176">Next steps</span></span>
* [<span data-ttu-id="faa76-177">Więcej informacji na temat diagnozowania i monitorowanie usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="faa76-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="faa76-178">Dokumentacja EventFlow</span><span class="sxs-lookup"><span data-stu-id="faa76-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
