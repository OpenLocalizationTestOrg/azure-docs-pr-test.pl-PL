---
title: "operacje niestandardowe aaaTrack z zestawu .NET SDK usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Śledzenie działań niestandardowych z zestawu .NET SDK usługi Azure Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="457df-103">Śledzenie działań niestandardowych z zestawu SDK .NET usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="457df-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="457df-104">Zestawy Azure SDK Insights aplikacji automatycznie ścieżki HTTP przychodzących żądań i wywołuje toodependent usług, takich jak żądania HTTP i zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="457df-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="457df-105">Śledzenie i korelacja żądań i zależności zapewniają wgląd w elastyczność i niezawodność hello całej aplikacji we wszystkich mikrousług, które łączą tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="457df-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="457df-106">Brak klasy wzorców aplikacji, których nie można używać objęty.</span><span class="sxs-lookup"><span data-stu-id="457df-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="457df-107">Zapewnienia odpowiedniego monitorowania tych wzorców wymaga ręcznego kodu instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="457df-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="457df-108">W tym artykule opisano kilka wzorców, które mogą wymagać ręcznego instrumentacji, takie jak niestandardowe kolejki przetwarzania i uruchamianie długotrwałe zadania w tle.</span><span class="sxs-lookup"><span data-stu-id="457df-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="457df-109">Ten dokument zawiera wskazówki dotyczące sposobu tootrack działań niestandardowych z hello zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="457df-110">Niniejsza dokumentacja jest odpowiednie dla:</span><span class="sxs-lookup"><span data-stu-id="457df-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="457df-111">Application Insights dla platformy .NET (znanej także jako podstawowy zestaw SDK) w wersji 2.4 +.</span><span class="sxs-lookup"><span data-stu-id="457df-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="457df-112">Application Insights dla usługi sieci web aplikacji (ASP.NET działających) wersji 2.4.</span><span class="sxs-lookup"><span data-stu-id="457df-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="457df-113">Application Insights dla platformy ASP.NET Core w wersji 2.1 +.</span><span class="sxs-lookup"><span data-stu-id="457df-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="457df-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="457df-114">Overview</span></span>
<span data-ttu-id="457df-115">Operacja jest logiczną pracy wykonywane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="457df-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="457df-116">Ma on nazwę, godzinę rozpoczęcia, czas trwania, wynik oraz kontekst wykonywania, takie jak nazwa użytkownika, właściwości i wyników.</span><span class="sxs-lookup"><span data-stu-id="457df-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="457df-117">Jeśli operacja A została zainicjowana przez operację B, następnie operacji B ustawiono jako element nadrzędny a. Operacja może mieć tylko jeden obiekt nadrzędny, ale może mieć wiele działań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="457df-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="457df-118">Aby uzyskać więcej informacji o operacjach i dane telemetryczne korelacji, zobacz [korelacji telemetrii usługi Application Insights Azure](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="457df-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="457df-119">W hello zestawu SDK .NET usługi Application Insights, operacja hello jest opisany przez klasy abstrakcyjnej hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) i jego elementy podrzędne [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) i [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="457df-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="457df-120">Przychodzące operacji śledzenia</span><span class="sxs-lookup"><span data-stu-id="457df-120">Incoming operations tracking</span></span> 
<span data-ttu-id="457df-121">Witaj sieci web usługi Application Insights SDK automatycznie zbiera żądania HTTP dla aplikacji ASP.NET, które są uruchamiane w potoku usług IIS i wszystkich aplikacji platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="457df-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="457df-122">Są obsługiwane przez społeczność rozwiązań dla innych platform i struktur.</span><span class="sxs-lookup"><span data-stu-id="457df-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="457df-123">Jednak jeśli aplikacja hello nie jest obsługiwany przez standardowy hello lub obsługiwane przez społeczność rozwiązania, możesz mogą dodawać go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="457df-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="457df-124">Innym przykładem wymagającego niestandardowych śledzenia jest hello procesu roboczego, który odbiera elementy z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="457df-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="457df-125">W przypadku niektórych kolejek hello wywołać tooadd komunikat, który toothis kolejki jest śledzony jako zależność.</span><span class="sxs-lookup"><span data-stu-id="457df-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="457df-126">Jednak hello operacji wysokiego poziomu, która opisuje przetwarzania komunikatów nie są automatycznie zbierane.</span><span class="sxs-lookup"><span data-stu-id="457df-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="457df-127">Zobaczmy, jak można śledzić takie operacje.</span><span class="sxs-lookup"><span data-stu-id="457df-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="457df-128">Na wysokim poziomie zadanie hello jest toocreate `RequestTelemetry` i znanych właściwości.</span><span class="sxs-lookup"><span data-stu-id="457df-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="457df-129">Po zakończeniu operacji hello, śledzić hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="457df-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="457df-130">Witaj poniższy przykład pokazuje, to zadanie.</span><span class="sxs-lookup"><span data-stu-id="457df-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="457df-131">Żądania HTTP w aplikacji siebie Owin</span><span class="sxs-lookup"><span data-stu-id="457df-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="457df-132">W tym przykładzie mamy wykonaj hello [protokołu HTTP dla korelacji](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="457df-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="457df-133">Należy oczekiwać tooreceive nagłówków, których opisano.</span><span class="sxs-lookup"><span data-stu-id="457df-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="457df-134">Witaj protokołu HTTP dla korelacji deklaruje element hello `Correlation-Context` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="457df-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="457df-135">Jednak zostanie pominięty tutaj dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="457df-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="457df-136">Instrumentacja kolejki</span><span class="sxs-lookup"><span data-stu-id="457df-136">Queue instrumentation</span></span>
<span data-ttu-id="457df-137">Do komunikacji HTTP utworzyliśmy protokół toopass korelacji szczegóły.</span><span class="sxs-lookup"><span data-stu-id="457df-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="457df-138">Przy użyciu protokołów niektórych kolejek można przekazać dodatkowe metadane wraz z wiadomości powitania i osobom, które można.</span><span class="sxs-lookup"><span data-stu-id="457df-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="457df-139">Kolejki usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="457df-139">Service Bus queue</span></span>
<span data-ttu-id="457df-140">Z hello Azure [kolejki usługi Service Bus](../service-bus-messaging/index.md), można przekazać zbiór właściwości, oraz wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="457df-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="457df-141">Możemy użyć identyfikatora toopass hello korelacji.</span><span class="sxs-lookup"><span data-stu-id="457df-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="457df-142">kolejki usługi Service Bus Hello używa protokołów opartych na protokole TCP.</span><span class="sxs-lookup"><span data-stu-id="457df-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="457df-143">Usługi Application Insights nie może automatycznie śledzić operacje kolejki tak Śledzimy je ręcznie.</span><span class="sxs-lookup"><span data-stu-id="457df-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="457df-144">Witaj usuwania z kolejki operacji jest wypychane stylu interfejsu API i jesteśmy tootrack nie można go.</span><span class="sxs-lookup"><span data-stu-id="457df-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="457df-145">Umieścić w kolejce</span><span class="sxs-lookup"><span data-stu-id="457df-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="457df-146">Proces</span><span class="sxs-lookup"><span data-stu-id="457df-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="457df-147">Kolejki magazynu systemu Azure</span><span class="sxs-lookup"><span data-stu-id="457df-147">Azure Storage queue</span></span>
<span data-ttu-id="457df-148">powitania po przykładzie pokazano, jak tootrack hello [kolejki usługi Azure Storage](../storage/queues/storage-dotnet-how-to-use-queues.md) operacje oraz korelowanie telemetrii między producent hello, powitania klienta i usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="457df-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="457df-149">kolejki magazynu Hello jest interfejs API protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="457df-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="457df-150">Wszystkie wywołania toohello kolejki są śledzone przez hello modułu zbierającego zależności Insights aplikacji dla żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="457df-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="457df-151">Upewnij się, że masz `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` w `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="457df-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="457df-152">Jeśli nie masz, dodaj ją programowo, zgodnie z opisem w [filtrowanie i przetwarzania wstępnego w hello zestaw SDK usługi Azure Application Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="457df-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="457df-153">Jeśli ręcznie skonfigurować usługi Application Insights, upewnij się, Utwórz i zainicjuj `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` podobnie do:</span><span class="sxs-lookup"><span data-stu-id="457df-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="457df-154">Można również identyfikator operacji usługi Application Insights hello toocorrelate z identyfikatorem hello magazynu żądania.</span><span class="sxs-lookup"><span data-stu-id="457df-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="457df-155">Informacje dotyczące sposobu tooset i get magazynu żądania klienta i identyfikator żądania serwera znajdują się w temacie [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługą Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="457df-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="457df-156">Umieścić w kolejce</span><span class="sxs-lookup"><span data-stu-id="457df-156">Enqueue</span></span>
<span data-ttu-id="457df-157">Ponieważ magazyn kolejek obsługuje hello API protokołu HTTP, wszystkie operacje z kolejką hello automatycznie są śledzone przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="457df-158">W wielu przypadkach ta Instrumentacji powinny być wystarczające.</span><span class="sxs-lookup"><span data-stu-id="457df-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="457df-159">Jednak toocorrelate śledzi po stronie klienta hello z producentów danych śledzenia, należy podać niektóre kontekstu korelacji podobnie toohow jak go w hello protokołu HTTP dla korelacji.</span><span class="sxs-lookup"><span data-stu-id="457df-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="457df-160">W tym przykładzie śledzenie hello opcjonalne `Enqueue` operacji.</span><span class="sxs-lookup"><span data-stu-id="457df-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="457df-161">Możesz:</span><span class="sxs-lookup"><span data-stu-id="457df-161">You can:</span></span>

 - <span data-ttu-id="457df-162">**Korelowanie ponownych prób (jeśli istnieją)**: wszystkie mają jeden wspólnej nadrzędnego, który jest hello `Enqueue` operacji.</span><span class="sxs-lookup"><span data-stu-id="457df-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="457df-163">W przeciwnym razie jest śledzony jako elementy podrzędne hello żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="457df-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="457df-164">Jeśli istnieje wiele żądań logicznej toohello kolejki, może być trudne toofind wywołania, które spowodowało ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="457df-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="457df-165">**Skorelowania dzienników magazynu (Jeśli wymagane)**: są one powiązane z telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="457df-166">Witaj `Enqueue` operacji jest hello podrzędnym działania nadrzędnego (na przykład przychodzące żądanie HTTP).</span><span class="sxs-lookup"><span data-stu-id="457df-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="457df-167">Wywołanie zależności Hello HTTP jest podrzędnym hello hello `Enqueue` operacji i hello podwójnym hello żądania przychodzące:</span><span class="sxs-lookup"><span data-stu-id="457df-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="457df-168">raporty aplikacji hello tooreduce ilość danych telemetrycznych lub jeśli nie chcesz tootrack hello `Enqueue` operacji z innych przyczyn, użyj hello `Activity` bezpośrednio interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="457df-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="457df-169">Utwórz (i uruchom) nowy `Activity` zamiast uruchamiania hello operacji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="457df-170">Jak *nie* muszą tooassign żadnych właściwości na nim, oprócz hello nazwy operacji.</span><span class="sxs-lookup"><span data-stu-id="457df-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="457df-171">Serializować `yourActivity.Id` do ładunku wiadomość hello zamiast `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="457df-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="457df-172">Można również użyć `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="457df-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="457df-173">Usuwania z kolejki</span><span class="sxs-lookup"><span data-stu-id="457df-173">Dequeue</span></span>
<span data-ttu-id="457df-174">Podobnie za`Enqueue`, rzeczywista kolejki magazynu toohello żądanie HTTP jest automatycznie śledzony przez usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="457df-175">Jednak hello `Enqueue` operacji prawdopodobnie dzieje się w kontekście nadrzędnego hello, takie jak kontekst żądania przychodzące.</span><span class="sxs-lookup"><span data-stu-id="457df-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="457df-176">Application Insights SDK automatycznie grupowania takie działanie (i jego części HTTP) z żądania nadrzędnego hello i inne dane telemetryczne zgłoszone w hello sam zakresu.</span><span class="sxs-lookup"><span data-stu-id="457df-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="457df-177">Witaj `Dequeue` operacja jest istotne znaczenie.</span><span class="sxs-lookup"><span data-stu-id="457df-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="457df-178">zestaw SDK usługi Application Insights Hello automatyczne śledzenie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="457df-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="457df-179">Jednak go nie może ustalić kontekst korelacji hello dopóki wiadomość hello jest analizowana.</span><span class="sxs-lookup"><span data-stu-id="457df-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="457df-180">Nie jest możliwe toocorrelate hello HTTP tooget hello komunikat z żądaniem o hello reszty hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="457df-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="457df-181">W wielu przypadkach może być przydatne toocorrelate hello HTTP toohello kolejkę żądań również innych śladów.</span><span class="sxs-lookup"><span data-stu-id="457df-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="457df-182">Witaj poniższym przykładzie pokazano, jak toodo go:</span><span class="sxs-lookup"><span data-stu-id="457df-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="457df-183">Proces</span><span class="sxs-lookup"><span data-stu-id="457df-183">Process</span></span>

<span data-ttu-id="457df-184">W hello poniższy przykład, możemy śledzenia przychodzący komunikat w sposób podobnie toohow możemy śledzenia przychodzące HTTP żądania:</span><span class="sxs-lookup"><span data-stu-id="457df-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="457df-185">Podobnie można instrumentowany innych operacji kolejki.</span><span class="sxs-lookup"><span data-stu-id="457df-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="457df-186">Operacja peek powinien instrumentowany w podobny sposób jako operacja kolejki.</span><span class="sxs-lookup"><span data-stu-id="457df-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="457df-187">Instrumentacja kolejki operacji zarządzania nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="457df-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="457df-188">Usługa Application Insights śledzi operacji, takich jak HTTP, i w większości przypadków jest wystarczające.</span><span class="sxs-lookup"><span data-stu-id="457df-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="457df-189">Gdy Instrumentacja usuwania komunikatów, upewnij się, że ustawisz operacji hello identyfikatorów (korelacji).</span><span class="sxs-lookup"><span data-stu-id="457df-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="457df-190">Alternatywnie można użyć hello `Activity` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="457df-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="457df-191">Nie musisz tooset identyfikatorów operacji na elementach telemetrii hello ponieważ usługi Application Insights jest dla Ciebie:</span><span class="sxs-lookup"><span data-stu-id="457df-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="457df-192">Utwórz nową `Activity` po skonfigurowaniu elementu z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="457df-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="457df-193">Użyj `Activity.SetParentId(message.ParentId)` toocorrelate dzienniki konsumentów i producentów.</span><span class="sxs-lookup"><span data-stu-id="457df-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="457df-194">Uruchom hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="457df-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="457df-195">Śledź usuwania z kolejki, przetwarzania i operacji usunięcia przy użyciu `Start/StopOperation` pomocników.</span><span class="sxs-lookup"><span data-stu-id="457df-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="457df-196">To robić z hello sam asynchroniczne sterowania przepływem (kontekstu wykonywania).</span><span class="sxs-lookup"><span data-stu-id="457df-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="457df-197">W ten sposób ich są skorelowane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="457df-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="457df-198">Zatrzymaj hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="457df-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="457df-199">Użyj `Start/StopOperation`, lub zadzwoń `Track` telemetrii ręcznie.</span><span class="sxs-lookup"><span data-stu-id="457df-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="457df-200">Przetwarzanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="457df-200">Batch processing</span></span>
<span data-ttu-id="457df-201">W przypadku niektórych kolejek można usuwania z kolejki wielu komunikatów z jednego żądania.</span><span class="sxs-lookup"><span data-stu-id="457df-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="457df-202">Przetwarzanie takich wiadomości jest prawdopodobnie niezależna i należy toohello różnych operacji logicznej.</span><span class="sxs-lookup"><span data-stu-id="457df-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="457df-203">W takim przypadku nie jest możliwe toocorrelate hello `Dequeue` przetwarzania komunikatów tooparticular operacji.</span><span class="sxs-lookup"><span data-stu-id="457df-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="457df-204">Każdy komunikat powinien zostać przetworzony w przepływ sterowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="457df-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="457df-205">Aby uzyskać więcej informacji, zobacz hello [zależności wychodzące śledzenia](#outgoing-dependencies-tracking) sekcji.</span><span class="sxs-lookup"><span data-stu-id="457df-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="457df-206">Długotrwałe zadania w tle</span><span class="sxs-lookup"><span data-stu-id="457df-206">Long-running background tasks</span></span>
<span data-ttu-id="457df-207">Niektóre aplikacje uruchamiają długotrwałe operacje, które mogą być spowodowane przez żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="457df-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="457df-208">Z perspektywy śledzenie/Instrumentacji hello nie jest inny niż Instrumentacji żądania lub zależności:</span><span class="sxs-lookup"><span data-stu-id="457df-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="457df-209">W tym przykładzie używamy `telemetryClient.StartOperation` toocreate `RequestTelemetry` i wypełnienia hello korelacji kontekstu.</span><span class="sxs-lookup"><span data-stu-id="457df-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="457df-210">Załóżmy, że masz operacji nadrzędnego, który został utworzony przez żądań przychodzących, które hello operacji zaplanowanej.</span><span class="sxs-lookup"><span data-stu-id="457df-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="457df-211">Tak długo, jak `BackgroundTask` jest uruchamiana w hello takim samym przepływie sterowania asynchroniczne jako przychodzącego żądania, jest skorelowany z tym operacja nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="457df-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="457df-212">`BackgroundTask`i wszystkie elementy zagnieżdżone dane telemetryczne są automatycznie skorelowane z żądaniem hello, który spowodował, nawet po zakończeniu hello żądania.</span><span class="sxs-lookup"><span data-stu-id="457df-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="457df-213">Po uruchomieniu zadania hello z wątku tła hello, która nie ma żadnej operacji (`Activity`) skojarzone z nią `BackgroundTask` nie ma żadnych nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="457df-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="457df-214">Jednak go można mieć zagnieżdżonych działań.</span><span class="sxs-lookup"><span data-stu-id="457df-214">However, it can have nested operations.</span></span> <span data-ttu-id="457df-215">Wszystkie elementy dane telemetryczne zgłoszone zadań hello są skorelowane toohello `RequestTelemetry` utworzone w `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="457df-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="457df-216">Wychodzące zależności śledzenia</span><span class="sxs-lookup"><span data-stu-id="457df-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="457df-217">Możliwe jest śledzenie własnych rodzaj zależności lub operacja nie jest obsługiwana przez usługę Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="457df-218">Witaj `Enqueue` metody kolejki usługi Service Bus hello lub hello kolejki magazynu może służyć jako przykłady takich niestandardowych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="457df-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="457df-219">Witaj ogólne podejście do śledzenia niestandardowych zależności jest:</span><span class="sxs-lookup"><span data-stu-id="457df-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="457df-220">Wywołaj hello `TelemetryClient.StartOperation` — metoda (rozszerzenie), które wypełnia hello `DependencyTelemetry` właściwości, które są potrzebne dla korelacji i niektórych innych właściwości (czas rozpoczęcia sygnatury, czas trwania).</span><span class="sxs-lookup"><span data-stu-id="457df-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="457df-221">Ustaw właściwości niestandardowe na powitania `DependencyTelemetry`, takie jak nazwa hello i innych kontekstu potrzebne.</span><span class="sxs-lookup"><span data-stu-id="457df-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="457df-222">Należy zależność wywołań i poczekaj na jej.</span><span class="sxs-lookup"><span data-stu-id="457df-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="457df-223">Zatrzymaj operację hello z `StopOperation` po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="457df-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="457df-224">Obsługa wyjątków.</span><span class="sxs-lookup"><span data-stu-id="457df-224">Handle exceptions.</span></span>

<span data-ttu-id="457df-225">`StopOperation`tylko zatrzymuje operację hello, które zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="457df-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="457df-226">Jeśli bieżącej operacji uruchomione hello niezgodny hello, co ma toostop, `StopOperation` nie działają.</span><span class="sxs-lookup"><span data-stu-id="457df-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="457df-227">Taka sytuacja może się zdarzyć, jeśli wiele operacji uruchamia się równolegle w hello tego samego kontekstu wykonywania:</span><span class="sxs-lookup"><span data-stu-id="457df-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="457df-228">Upewnij się, że wywoływanie zawsze `StartOperation` i uruchom zadanie w jego własnej kontekstu:</span><span class="sxs-lookup"><span data-stu-id="457df-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="457df-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="457df-229">Next steps</span></span>

- <span data-ttu-id="457df-230">Dowiedz się podstawy hello [korelacji telemetrii](application-insights-correlation.md) w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="457df-231">Zobacz hello [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="457df-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="457df-232">Raport niestandardowy [zdarzenia i metryki](app-insights-api-custom-events-metrics.md) tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="457df-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="457df-233">Zapoznaj się z standard [konfiguracji](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) dla zbioru właściwości kontekstu.</span><span class="sxs-lookup"><span data-stu-id="457df-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="457df-234">Sprawdź hello [Podręcznik użytkownika System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee jak możemy skorelowania danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="457df-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
