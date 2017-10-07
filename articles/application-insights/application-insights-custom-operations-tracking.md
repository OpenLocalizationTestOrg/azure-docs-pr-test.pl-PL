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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Śledzenie działań niestandardowych z zestawu SDK .NET usługi Application Insights

Zestawy Azure SDK Insights aplikacji automatycznie ścieżki HTTP przychodzących żądań i wywołuje toodependent usług, takich jak żądania HTTP i zapytania SQL. Śledzenie i korelacja żądań i zależności zapewniają wgląd w elastyczność i niezawodność hello całej aplikacji we wszystkich mikrousług, które łączą tę aplikację. 

Brak klasy wzorców aplikacji, których nie można używać objęty. Zapewnienia odpowiedniego monitorowania tych wzorców wymaga ręcznego kodu instrumentacji. W tym artykule opisano kilka wzorców, które mogą wymagać ręcznego instrumentacji, takie jak niestandardowe kolejki przetwarzania i uruchamianie długotrwałe zadania w tle.

Ten dokument zawiera wskazówki dotyczące sposobu tootrack działań niestandardowych z hello zestaw SDK usługi Application Insights. Niniejsza dokumentacja jest odpowiednie dla:

- Application Insights dla platformy .NET (znanej także jako podstawowy zestaw SDK) w wersji 2.4 +.
- Application Insights dla usługi sieci web aplikacji (ASP.NET działających) wersji 2.4.
- Application Insights dla platformy ASP.NET Core w wersji 2.1 +.

## <a name="overview"></a>Omówienie
Operacja jest logiczną pracy wykonywane przez aplikację. Ma on nazwę, godzinę rozpoczęcia, czas trwania, wynik oraz kontekst wykonywania, takie jak nazwa użytkownika, właściwości i wyników. Jeśli operacja A została zainicjowana przez operację B, następnie operacji B ustawiono jako element nadrzędny a. Operacja może mieć tylko jeden obiekt nadrzędny, ale może mieć wiele działań podrzędnych. Aby uzyskać więcej informacji o operacjach i dane telemetryczne korelacji, zobacz [korelacji telemetrii usługi Application Insights Azure](application-insights-correlation.md).

W hello zestawu SDK .NET usługi Application Insights, operacja hello jest opisany przez klasy abstrakcyjnej hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) i jego elementy podrzędne [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) i [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Przychodzące operacji śledzenia 
Witaj sieci web usługi Application Insights SDK automatycznie zbiera żądania HTTP dla aplikacji ASP.NET, które są uruchamiane w potoku usług IIS i wszystkich aplikacji platformy ASP.NET Core. Są obsługiwane przez społeczność rozwiązań dla innych platform i struktur. Jednak jeśli aplikacja hello nie jest obsługiwany przez standardowy hello lub obsługiwane przez społeczność rozwiązania, możesz mogą dodawać go ręcznie.

Innym przykładem wymagającego niestandardowych śledzenia jest hello procesu roboczego, który odbiera elementy z kolejki hello. W przypadku niektórych kolejek hello wywołać tooadd komunikat, który toothis kolejki jest śledzony jako zależność. Jednak hello operacji wysokiego poziomu, która opisuje przetwarzania komunikatów nie są automatycznie zbierane.

Zobaczmy, jak można śledzić takie operacje.

Na wysokim poziomie zadanie hello jest toocreate `RequestTelemetry` i znanych właściwości. Po zakończeniu operacji hello, śledzić hello telemetrii. Witaj poniższy przykład pokazuje, to zadanie.

### <a name="http-request-in-owin-self-hosted-app"></a>Żądania HTTP w aplikacji siebie Owin
W tym przykładzie mamy wykonaj hello [protokołu HTTP dla korelacji](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Należy oczekiwać tooreceive nagłówków, których opisano.

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

Witaj protokołu HTTP dla korelacji deklaruje element hello `Correlation-Context` nagłówka. Jednak zostanie pominięty tutaj dla uproszczenia.

## <a name="queue-instrumentation"></a>Instrumentacja kolejki
Do komunikacji HTTP utworzyliśmy protokół toopass korelacji szczegóły. Przy użyciu protokołów niektórych kolejek można przekazać dodatkowe metadane wraz z wiadomości powitania i osobom, które można.

### <a name="service-bus-queue"></a>Kolejki usługi Service Bus
Z hello Azure [kolejki usługi Service Bus](../service-bus-messaging/index.md), można przekazać zbiór właściwości, oraz wiadomości powitania. Możemy użyć identyfikatora toopass hello korelacji.

kolejki usługi Service Bus Hello używa protokołów opartych na protokole TCP. Usługi Application Insights nie może automatycznie śledzić operacje kolejki tak Śledzimy je ręcznie. Witaj usuwania z kolejki operacji jest wypychane stylu interfejsu API i jesteśmy tootrack nie można go.

#### <a name="enqueue"></a>Umieścić w kolejce

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

#### <a name="process"></a>Proces
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

### <a name="azure-storage-queue"></a>Kolejki magazynu systemu Azure
powitania po przykładzie pokazano, jak tootrack hello [kolejki usługi Azure Storage](../storage/queues/storage-dotnet-how-to-use-queues.md) operacje oraz korelowanie telemetrii między producent hello, powitania klienta i usługi Azure Storage. 

kolejki magazynu Hello jest interfejs API protokołu HTTP. Wszystkie wywołania toohello kolejki są śledzone przez hello modułu zbierającego zależności Insights aplikacji dla żądania HTTP.
Upewnij się, że masz `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` w `applicationInsights.config`. Jeśli nie masz, dodaj ją programowo, zgodnie z opisem w [filtrowanie i przetwarzania wstępnego w hello zestaw SDK usługi Azure Application Insights](app-insights-api-filtering-sampling.md).

Jeśli ręcznie skonfigurować usługi Application Insights, upewnij się, Utwórz i zainicjuj `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` podobnie do:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Można również identyfikator operacji usługi Application Insights hello toocorrelate z identyfikatorem hello magazynu żądania. Informacje dotyczące sposobu tooset i get magazynu żądania klienta i identyfikator żądania serwera znajdują się w temacie [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługą Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Umieścić w kolejce
Ponieważ magazyn kolejek obsługuje hello API protokołu HTTP, wszystkie operacje z kolejką hello automatycznie są śledzone przez usługę Application Insights. W wielu przypadkach ta Instrumentacji powinny być wystarczające. Jednak toocorrelate śledzi po stronie klienta hello z producentów danych śledzenia, należy podać niektóre kontekstu korelacji podobnie toohow jak go w hello protokołu HTTP dla korelacji. 

W tym przykładzie śledzenie hello opcjonalne `Enqueue` operacji. Możesz:

 - **Korelowanie ponownych prób (jeśli istnieją)**: wszystkie mają jeden wspólnej nadrzędnego, który jest hello `Enqueue` operacji. W przeciwnym razie jest śledzony jako elementy podrzędne hello żądania przychodzącego. Jeśli istnieje wiele żądań logicznej toohello kolejki, może być trudne toofind wywołania, które spowodowało ponownych prób.
 - **Skorelowania dzienników magazynu (Jeśli wymagane)**: są one powiązane z telemetrii usługi Application Insights.

Witaj `Enqueue` operacji jest hello podrzędnym działania nadrzędnego (na przykład przychodzące żądanie HTTP). Wywołanie zależności Hello HTTP jest podrzędnym hello hello `Enqueue` operacji i hello podwójnym hello żądania przychodzące:

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

raporty aplikacji hello tooreduce ilość danych telemetrycznych lub jeśli nie chcesz tootrack hello `Enqueue` operacji z innych przyczyn, użyj hello `Activity` bezpośrednio interfejsu API:

- Utwórz (i uruchom) nowy `Activity` zamiast uruchamiania hello operacji usługi Application Insights. Jak *nie* muszą tooassign żadnych właściwości na nim, oprócz hello nazwy operacji.
- Serializować `yourActivity.Id` do ładunku wiadomość hello zamiast `operation.Telemetry.Id`. Można również użyć `Activity.Current.Id`.


#### <a name="dequeue"></a>Usuwania z kolejki
Podobnie za`Enqueue`, rzeczywista kolejki magazynu toohello żądanie HTTP jest automatycznie śledzony przez usługi Application Insights. Jednak hello `Enqueue` operacji prawdopodobnie dzieje się w kontekście nadrzędnego hello, takie jak kontekst żądania przychodzące. Application Insights SDK automatycznie grupowania takie działanie (i jego części HTTP) z żądania nadrzędnego hello i inne dane telemetryczne zgłoszone w hello sam zakresu.

Witaj `Dequeue` operacja jest istotne znaczenie. zestaw SDK usługi Application Insights Hello automatyczne śledzenie żądań HTTP. Jednak go nie może ustalić kontekst korelacji hello dopóki wiadomość hello jest analizowana. Nie jest możliwe toocorrelate hello HTTP tooget hello komunikat z żądaniem o hello reszty hello telemetrii.

W wielu przypadkach może być przydatne toocorrelate hello HTTP toohello kolejkę żądań również innych śladów. Witaj poniższym przykładzie pokazano, jak toodo go:

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

#### <a name="process"></a>Proces

W hello poniższy przykład, możemy śledzenia przychodzący komunikat w sposób podobnie toohow możemy śledzenia przychodzące HTTP żądania:

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

Podobnie można instrumentowany innych operacji kolejki. Operacja peek powinien instrumentowany w podobny sposób jako operacja kolejki. Instrumentacja kolejki operacji zarządzania nie jest konieczne. Usługa Application Insights śledzi operacji, takich jak HTTP, i w większości przypadków jest wystarczające.

Gdy Instrumentacja usuwania komunikatów, upewnij się, że ustawisz operacji hello identyfikatorów (korelacji). Alternatywnie można użyć hello `Activity` interfejsu API. Nie musisz tooset identyfikatorów operacji na elementach telemetrii hello ponieważ usługi Application Insights jest dla Ciebie:

- Utwórz nową `Activity` po skonfigurowaniu elementu z kolejki hello.
- Użyj `Activity.SetParentId(message.ParentId)` toocorrelate dzienniki konsumentów i producentów.
- Uruchom hello `Activity`.
- Śledź usuwania z kolejki, przetwarzania i operacji usunięcia przy użyciu `Start/StopOperation` pomocników. To robić z hello sam asynchroniczne sterowania przepływem (kontekstu wykonywania). W ten sposób ich są skorelowane poprawnie.
- Zatrzymaj hello `Activity`.
- Użyj `Start/StopOperation`, lub zadzwoń `Track` telemetrii ręcznie.

### <a name="batch-processing"></a>Przetwarzanie wsadowe
W przypadku niektórych kolejek można usuwania z kolejki wielu komunikatów z jednego żądania. Przetwarzanie takich wiadomości jest prawdopodobnie niezależna i należy toohello różnych operacji logicznej. W takim przypadku nie jest możliwe toocorrelate hello `Dequeue` przetwarzania komunikatów tooparticular operacji.

Każdy komunikat powinien zostać przetworzony w przepływ sterowania asynchronicznego. Aby uzyskać więcej informacji, zobacz hello [zależności wychodzące śledzenia](#outgoing-dependencies-tracking) sekcji.

## <a name="long-running-background-tasks"></a>Długotrwałe zadania w tle
Niektóre aplikacje uruchamiają długotrwałe operacje, które mogą być spowodowane przez żądania użytkownika. Z perspektywy śledzenie/Instrumentacji hello nie jest inny niż Instrumentacji żądania lub zależności: 

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

W tym przykładzie używamy `telemetryClient.StartOperation` toocreate `RequestTelemetry` i wypełnienia hello korelacji kontekstu. Załóżmy, że masz operacji nadrzędnego, który został utworzony przez żądań przychodzących, które hello operacji zaplanowanej. Tak długo, jak `BackgroundTask` jest uruchamiana w hello takim samym przepływie sterowania asynchroniczne jako przychodzącego żądania, jest skorelowany z tym operacja nadrzędnej. `BackgroundTask`i wszystkie elementy zagnieżdżone dane telemetryczne są automatycznie skorelowane z żądaniem hello, który spowodował, nawet po zakończeniu hello żądania.

Po uruchomieniu zadania hello z wątku tła hello, która nie ma żadnej operacji (`Activity`) skojarzone z nią `BackgroundTask` nie ma żadnych nadrzędnej. Jednak go można mieć zagnieżdżonych działań. Wszystkie elementy dane telemetryczne zgłoszone zadań hello są skorelowane toohello `RequestTelemetry` utworzone w `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Wychodzące zależności śledzenia
Możliwe jest śledzenie własnych rodzaj zależności lub operacja nie jest obsługiwana przez usługę Application Insights.

Witaj `Enqueue` metody kolejki usługi Service Bus hello lub hello kolejki magazynu może służyć jako przykłady takich niestandardowych śledzenia.

Witaj ogólne podejście do śledzenia niestandardowych zależności jest:

- Wywołaj hello `TelemetryClient.StartOperation` — metoda (rozszerzenie), które wypełnia hello `DependencyTelemetry` właściwości, które są potrzebne dla korelacji i niektórych innych właściwości (czas rozpoczęcia sygnatury, czas trwania).
- Ustaw właściwości niestandardowe na powitania `DependencyTelemetry`, takie jak nazwa hello i innych kontekstu potrzebne.
- Należy zależność wywołań i poczekaj na jej.
- Zatrzymaj operację hello z `StopOperation` po zakończeniu.
- Obsługa wyjątków.

`StopOperation`tylko zatrzymuje operację hello, które zostało uruchomione. Jeśli bieżącej operacji uruchomione hello niezgodny hello, co ma toostop, `StopOperation` nie działają. Taka sytuacja może się zdarzyć, jeśli wiele operacji uruchamia się równolegle w hello tego samego kontekstu wykonywania:

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

Upewnij się, że wywoływanie zawsze `StartOperation` i uruchom zadanie w jego własnej kontekstu:
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

## <a name="next-steps"></a>Następne kroki

- Dowiedz się podstawy hello [korelacji telemetrii](application-insights-correlation.md) w usłudze Application Insights.
- Zobacz hello [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- Raport niestandardowy [zdarzenia i metryki](app-insights-api-custom-events-metrics.md) tooApplication szczegółowych informacji.
- Zapoznaj się z standard [konfiguracji](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) dla zbioru właściwości kontekstu.
- Sprawdź hello [Podręcznik użytkownika System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee jak możemy skorelowania danych telemetrycznych.
