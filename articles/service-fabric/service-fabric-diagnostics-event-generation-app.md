---
title: "aaaAzure monitorowania poziomu aplikacji usługi sieci szkieletowej | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o aplikacji i zdarzenia dotyczące poziomu usług i dzienniki używane toomonitor i diagnozowanie klastrów sieci szkieletowej usług Azure."
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="86fcb-103">Generowanie zdarzeń i dzienników na poziomie aplikacji i usług</span><span class="sxs-lookup"><span data-stu-id="86fcb-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="86fcb-104">Kod Instrumentacji hello zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="86fcb-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="86fcb-105">Instrumentacja hello kod stanowi podstawę hello najbardziej inne aspekty monitorowania usług.</span><span class="sxs-lookup"><span data-stu-id="86fcb-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="86fcb-106">Instrumentacja jest jedynym sposobem hello, które można określić, że dany element jest nieprawidłowy i toodiagnose, co wymaga toobe stałej.</span><span class="sxs-lookup"><span data-stu-id="86fcb-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="86fcb-107">Chociaż jest technicznie możliwe tooconnect usługi produkcji tooa debugera, nie jest typowym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="86fcb-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="86fcb-108">Tak o szczegółowe dane Instrumentacji jest ważna.</span><span class="sxs-lookup"><span data-stu-id="86fcb-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="86fcb-109">Niektóre produkty automatyczną Instrumentację kodu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="86fcb-110">Mimo że te rozwiązania mogą również działać, ręczne Instrumentacja prawie zawsze jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="86fcb-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="86fcb-111">W celu hello musi mieć wystarczającą ilość tooforensically informacji debugowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="86fcb-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="86fcb-112">W tym dokumencie opisano różne podejścia tooinstrumenting kodu, i gdy toochoose jednej metody zamiast innego.</span><span class="sxs-lookup"><span data-stu-id="86fcb-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="86fcb-113">Źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="86fcb-113">EventSource</span></span>
<span data-ttu-id="86fcb-114">Po utworzeniu rozwiązania sieci szkieletowej usług z szablonu w programie Visual Studio, **EventSource**-klasy (**ServiceEventSource** lub **ActorEventSource**) jest generowany.</span><span class="sxs-lookup"><span data-stu-id="86fcb-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="86fcb-115">Utworzyć szablonu, w którym można dodać zdarzeń dla usługi lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="86fcb-116">Witaj **EventSource** nazwa **musi** być unikatowa i powinny zostać zmienione z ciąg szablonu domyślnego hello Moja firma -&lt;rozwiązania&gt; - &lt; Projekt&gt;.</span><span class="sxs-lookup"><span data-stu-id="86fcb-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="86fcb-117">Istnieniem wielu **EventSource** definicje, które używają hello tej samej przyczyny nazwa problem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="86fcb-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="86fcb-118">Każdy zdefiniowane zdarzenie musi mieć unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="86fcb-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="86fcb-119">Jeśli identyfikator nie jest unikatowa, wystąpi błąd czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="86fcb-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="86fcb-120">Niektóre organizacje preassign zakresów wartości dla identyfikatorów tooavoid konfliktów między oddzielne zespoły deweloperów.</span><span class="sxs-lookup"><span data-stu-id="86fcb-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="86fcb-121">Aby uzyskać więcej informacji, zobacz [zaliczko w blogu](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) lub hello [dokumentacji MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="86fcb-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="86fcb-122">W przypadku używania strukturalnych zdarzeń źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="86fcb-122">Using structured EventSource events</span></span>

<span data-ttu-id="86fcb-123">Każdego zdarzenia hello w hello przykłady kodu w tej sekcji są definiowane dla określonych przypadków, na przykład podczas rejestrowania typu usługi.</span><span class="sxs-lookup"><span data-stu-id="86fcb-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="86fcb-124">Podczas definiowania wiadomości w przypadku użycia, danych można spakować z tekstem hello hello błędu i można więcej łatwo wyszukiwać i filtr na podstawie nazwy hello lub wartości hello określonej właściwości.</span><span class="sxs-lookup"><span data-stu-id="86fcb-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="86fcb-125">Struktury wyjście Instrumentacji hello umożliwia łatwiejsze tooconsume, ale wymaga więcej myśl i godziny toodefine nowe zdarzenie dla każdego przypadku użycia.</span><span class="sxs-lookup"><span data-stu-id="86fcb-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="86fcb-126">Definicje zdarzeń mogą być współużytkowane przez hello całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="86fcb-127">Na przykład metoda uruchamiania lub zatrzymywania zdarzeń będzie można używać ponownie w wielu usług w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="86fcb-128">Usługa specyficznego dla domeny, takich jak system zamówień może mieć **CreateOrder** zdarzenie, które ma własną unikatową zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="86fcb-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="86fcb-129">Takie podejście może wygenerować wiele zdarzeń i mogą wymagać koordynacji identyfikatorów zespołów projektu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="86fcb-130">Ogólnie przy użyciu źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="86fcb-130">Using EventSource generically</span></span>

<span data-ttu-id="86fcb-131">Definiowanie określonych zdarzeń mogą być trudne, wiele osób zdefiniować kilka zdarzenia ze wspólnego zestawu parametrów, które zwykle wysyłają informacji o ich jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="86fcb-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="86fcb-132">Większość aspekt hello strukturę zostaną utracone i jest trudniej toosearch i filtrować wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="86fcb-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="86fcb-133">W takie podejście kilka zdarzeń, które zwykle odpowiadają poziomy rejestrowania toohello są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="86fcb-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="86fcb-134">Witaj następującego fragmentu definiuje debugowania i komunikatu o błędzie:</span><span class="sxs-lookup"><span data-stu-id="86fcb-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="86fcb-135">Przy użyciu hybrydowego Instrumentacji strukturalnych i rodzajowy również może działać również.</span><span class="sxs-lookup"><span data-stu-id="86fcb-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="86fcb-136">Strukturalne Instrumentacji jest używana do raportowania błędów i metryki.</span><span class="sxs-lookup"><span data-stu-id="86fcb-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="86fcb-137">Zdarzenia ogólne może służyć do hello szczegółowe rejestrowanie, który jest używane przez inżynierów do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="86fcb-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="86fcb-138">Platformy ASP.NET Core rejestrowania</span><span class="sxs-lookup"><span data-stu-id="86fcb-138">ASP.NET Core logging</span></span>

<span data-ttu-id="86fcb-139">Toocarefully ważne jego Zaplanuj, jak będzie Instrumentacja kodu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="86fcb-140">plan prawym Instrumentacji Hello może pomóc w uniknięciu potencjalnie destabilizing bazy kodu, a następnie konieczności tooreinstrument hello kodu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="86fcb-141">ryzyko tooreduce, można wybrać Biblioteka instrumentacji, takie jak [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), który jest częścią pakietu Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="86fcb-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="86fcb-142">Ma platformy ASP.NET Core [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfejs, który można używać z dostawcy hello wybranych przez użytkownika, przy jednoczesnym zmniejszeniu hello wpływu na istniejący kod.</span><span class="sxs-lookup"><span data-stu-id="86fcb-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="86fcb-143">Użyj kodu hello w ASP.NET Core w systemach Windows i Linux i w hello pełne .NET Framework, więc jest standardowym kodu instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="86fcb-144">Jest to dodatkowe przedstawione poniżej:</span><span class="sxs-lookup"><span data-stu-id="86fcb-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="86fcb-145">Przy użyciu Microsoft.Extensions.Logging w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="86fcb-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="86fcb-146">Dodaj projekt toohello pakietu Microsoft.Extensions.Logging NuGet ma tooinstrument hello.</span><span class="sxs-lookup"><span data-stu-id="86fcb-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="86fcb-147">Ponadto Dodaj wszelkie pakiety dostawcy (pakietu innych firm, zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="86fcb-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="86fcb-148">Aby uzyskać więcej informacji, zobacz [logowanie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="86fcb-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="86fcb-149">Dodaj **przy użyciu** dyrektywy Microsoft.Extensions.Logging tooyour usługi pliku.</span><span class="sxs-lookup"><span data-stu-id="86fcb-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="86fcb-150">Zdefiniuj zmienną prywatny w klasie usługi.</span><span class="sxs-lookup"><span data-stu-id="86fcb-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="86fcb-151">W Konstruktorze hello klasie usługi Dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="86fcb-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="86fcb-152">Uruchom kod w metody instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="86fcb-153">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="86fcb-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="86fcb-154">Przy użyciu innych dostawców logowania</span><span class="sxs-lookup"><span data-stu-id="86fcb-154">Using other logging providers</span></span>

<span data-ttu-id="86fcb-155">Niektóre dostawców Użyj podejście hello opisane w powyższej sekcji hello tym [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), i [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="86fcb-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="86fcb-156">Możesz podłączyć każdego z nich do platformy ASP.NET Core rejestrowania lub można ich używać oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="86fcb-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="86fcb-157">Serilog jest funkcją, która wzbogaca wszystkich wiadomości wysłanych z rejestrator.</span><span class="sxs-lookup"><span data-stu-id="86fcb-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="86fcb-158">Ta funkcja może być przydatna toooutput hello usługi nazwę, typ i informacji o partycji.</span><span class="sxs-lookup"><span data-stu-id="86fcb-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="86fcb-159">toouse tę możliwość hello infrastruktury platformy ASP.NET Core, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="86fcb-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="86fcb-160">Dodaj hello Serilog, Serilog.Extensions.Logging, i Serilog.Sinks.Observable dzaj pakietami nuget toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="86fcb-161">Na przykład dalej hello należy również dodać Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="86fcb-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="86fcb-162">Lepszym rozwiązaniem jest wyświetlany w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="86fcb-163">W Serilog należy utworzyć wystąpienia rejestratora LoggerConfiguration i hello.</span><span class="sxs-lookup"><span data-stu-id="86fcb-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="86fcb-164">Dodaj Konstruktor Serilog.ILogger argument toohello usługi i podaj hello nowo utworzony rejestratora.</span><span class="sxs-lookup"><span data-stu-id="86fcb-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="86fcb-165">W Konstruktorze usługi hello, Dodaj hello następującego kodu, który tworzy hello enrichers właściwości dla hello **ServiceTypeName**, **ServiceName**, **PartitionId**i  **Identyfikator wystąpienia** właściwości hello usługi.</span><span class="sxs-lookup"><span data-stu-id="86fcb-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="86fcb-166">Dodaje również właściwość enricher toohello fabryki rejestrowanie platformy ASP.NET Core, dzięki czemu można używać Microsoft.Extensions.Logging.ILogger w kodzie.</span><span class="sxs-lookup"><span data-stu-id="86fcb-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="86fcb-167">Kod hello dokumentu hello takie same jak przy użyciu platformy ASP.NET Core bez Serilog.</span><span class="sxs-lookup"><span data-stu-id="86fcb-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="86fcb-168">Firma Microsoft zaleca, że nie używasz hello static Log.Logger z hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="86fcb-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="86fcb-169">Sieć szkieletowa usług może obsługiwać wiele wystąpień hello same usługi typu w ramach jednego procesu.</span><span class="sxs-lookup"><span data-stu-id="86fcb-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="86fcb-170">Jeśli używasz hello Log.Logger statycznych, hello ostatniego składnika zapisywania programu enrichers właściwości hello wyświetli wartości dla wszystkich wystąpień, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="86fcb-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="86fcb-171">Jest jednym z powodów dlaczego hello _logger zmienna jest zmienną prywatnego elementu członkowskiego klasy usługi hello.</span><span class="sxs-lookup"><span data-stu-id="86fcb-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="86fcb-172">Ponadto należy hello _logger dostępne toocommon kod, który może być używane w usługach.</span><span class="sxs-lookup"><span data-stu-id="86fcb-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="86fcb-173">Wybieranie dostawcy logowania</span><span class="sxs-lookup"><span data-stu-id="86fcb-173">Choosing a logging provider</span></span>

<span data-ttu-id="86fcb-174">Jeśli aplikacja korzysta z wysokiej wydajności, **EventSource** zazwyczaj jest to dobre rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="86fcb-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="86fcb-175">**Element EventSource** *zazwyczaj* wykorzystuje mniej zasobów i lepszą wydajność niż platformy ASP.NET Core rejestrowania lub dowolnym hello dostępnych rozwiązań innych firm.</span><span class="sxs-lookup"><span data-stu-id="86fcb-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="86fcb-176">To nie jest problemem w przypadku wielu usług, ale jeśli usługa jest ukierunkowane, za pomocą **EventSource** może być lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="86fcb-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="86fcb-177">Jednak tooget tych zalet strukturę rejestrowanie **EventSource** wymaga większych inwestycji zespołu inżynieryjnego.</span><span class="sxs-lookup"><span data-stu-id="86fcb-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="86fcb-178">Jeśli to możliwe, czy szybkie prototyp kilka opcji rejestrowania, a następnie wybierz hello jedną, która najlepiej odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="86fcb-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86fcb-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86fcb-179">Next steps</span></span>

<span data-ttu-id="86fcb-180">Po wybraniu użytkownika tooinstrument dostawcy rejestrowania aplikacji i usług z dzienników i zdarzeń muszą toobe zagregowane, zanim będzie można wysłać tooany analizy platformy.</span><span class="sxs-lookup"><span data-stu-id="86fcb-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="86fcb-181">Przeczytaj informacje o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) i [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter zrozumieniu hello zalecane opcje.</span><span class="sxs-lookup"><span data-stu-id="86fcb-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
