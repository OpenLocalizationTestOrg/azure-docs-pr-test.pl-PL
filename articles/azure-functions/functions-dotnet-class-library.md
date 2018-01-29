---
title: "Azure dokumentacja dla deweloperów funkcje C#"
description: "Zrozumienie sposobu tworzenia usługi Azure Functions przy użyciu języka C#."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 12/12/2017
ms.author: glenga
ms.openlocfilehash: 3de1e9b042a7a356c3c88e604e1e26c256d85657
ms.sourcegitcommit: 828cd4b47fbd7d7d620fbb93a592559256f9d234
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="azure-functions-c-developer-reference"></a>Azure dokumentacja dla deweloperów funkcje C#

<!-- When updating this article, make corresponding changes to any duplicate content in functions-reference-csharp.md -->

Ten artykuł zawiera wprowadzenie do tworzenia usługi Azure Functions przy użyciu języka C# w bibliotekach klas .NET.

Środowisko Azure Functions obsługuje C# i C# skrypt języków programowania. Jeśli szukasz wskazówki [przy użyciu języka C# w portalu Azure](functions-create-function-app-portal.md), zobacz [dokumentacja dla deweloperów (csx) skryptu C#](functions-reference-csharp.md).

W tym artykule przyjęto, że został już przeczytany następujące artykuły:

* [Przewodnik dla deweloperów funkcji platformy Azure](functions-reference.md)
* [Azure Functions narzędzia programu Visual Studio 2017](functions-develop-vs.md)

## <a name="functions-class-library-project"></a>Projektu biblioteki klas funkcji

W programie Visual Studio **usługi Azure Functions** szablonu projektu tworzy C# klasy biblioteki projekt, który zawiera następujące pliki:

* [Host.JSON](functions-host-json.md) -przechowuje ustawienia konfiguracji, które mają wpływ na wszystkie funkcje w projekcie uruchomionej lokalnie lub na platformie Azure.
* [Local.Settings.JSON](functions-run-local.md#local-settings-file) -przechowuje ustawienia aplikacji i parametry połączenia, które są używane podczas uruchamiania lokalnego.

### <a name="functionname-and-trigger-attributes"></a>Atrybuty FunctionName i wyzwalacza

W bibliotece klas, funkcja jest metodą statyczną z `FunctionName` i atrybut wyzwalacza, jak pokazano w poniższym przykładzie:

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

`FunctionName` Atrybut oznacza metodę jako punktu wejścia funkcji. Nazwa musi być unikatowa wewnątrz projektu.

Atrybut wyzwalacza Określa typ wyzwalacza i wiąże parametr metody danych wejściowych. Funkcja przykład jest wyzwalany przez komunikatu w kolejce, a komunikat z kolejki jest przekazywany do metody w `myQueueItem` parametru.

### <a name="additional-binding-attributes"></a>Atrybuty dodatkowe powiązania

Dodatkowe dane wejściowe i wyjściowe, powiązanie atrybuty mogą być używane. Poniższy przykład modyfikuje mieszanego przez dodanie wiązania kolejki danych wyjściowych. Funkcja zapisuje komunikat danych wejściowych w kolejce do nowego komunikatu w kolejce w innej kolejki.

```csharp
public static class SimpleExampleWithOutput
{
    [FunctionName("CopyQueueMessage")]
    public static void Run(
        [QueueTrigger("myqueue-items-source")] string myQueueItem, 
        [Queue("myqueue-items-destination")] out string myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"CopyQueueMessage function processed: {myQueueItem}");
        myQueueItemCopy = myQueueItem;
    }
}
```

### <a name="conversion-to-functionjson"></a>Konwersja do function.json

Proces kompilacji tworzy *function.json* pliku w folderze funkcji w folderze kompilacji. Ten plik nie jest przeznaczona do można edytować bezpośrednio. Nie można zmienić konfiguracji powiązania lub wyłączenie tej funkcji, edytując ten plik. 

Ten plik ma na celu zawierają informacje, które kontroler skalowania dla [skalowanie decyzji w planie zużycie](functions-scale.md#how-the-consumption-plan-works). Z tego powodu plik zawiera tylko informacje wyzwalacza, nie wejściowych lub wyjściowych powiązania.

Wygenerowany *function.json* plik zawiera `configurationSource` właściwość, która powoduje środowiska uruchomieniowego .NET atrybutów na potrzeby wiązania, a nie *function.json* konfiguracji. Oto przykład:

```json
{
  "generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
  "configurationSource": "attributes",
  "bindings": [
    {
      "type": "queueTrigger",
      "queueName": "%input-queue-name%",
      "name": "myQueueItem"
    }
  ],
  "disabled": false,
  "scriptFile": "..\\bin\\FunctionApp1.dll",
  "entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```

*Function.json* generowania plików jest wykonywane przez pakiet NuGet [Microsoft\.NET\.Sdk\.funkcji](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). Kod źródłowy jest dostępny w repozytorium GitHub [azure\-funkcje\-vs\-kompilacji\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="supported-types-for-bindings"></a>Obsługiwane typy dla powiązania

Każdego powiązania ma własną obsługiwanych typów; na przykład atrybut wyzwalacza obiektu blob można stosować na parametr typu string, a parametr POCO `CloudBlockBlob` parametr lub dowolną inne obsługiwane typy. [Artykule powiązanie dla obiekt blob powiązania](functions-bindings-storage-blob.md#trigger---usage) Wyświetla wszystkie obsługiwane typy parametrów. Aby uzyskać więcej informacji, zobacz [wyzwalaczy i powiązań](functions-triggers-bindings.md) i [docs odwołania wiązania dla każdego typu powiązania](functions-triggers-bindings.md#next-steps).

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="binding-to-method-return-value"></a>Powiązanie z wartości zwracanej — metoda

Wartość zwracaną metody można użyć dla powiązania danych wyjściowych, jak pokazano w poniższym przykładzie:

```csharp
public static class ReturnValueOutputBinding
{
    [FunctionName("CopyQueueMessageUsingReturnValue")]
    [return: Queue("myqueue-items-destination")]
    public static string Run(
        [QueueTrigger("myqueue-items-source-2")] string myQueueItem,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        return myQueueItem;
    }
}
```

## <a name="writing-multiple-output-values"></a>Trwa zapisywanie wielu wartości danych wyjściowych

Aby napisać wiele wartości do powiązania danych wyjściowych, użyj [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typów. Te typy są kolekcji tylko do zapisu, które są zapisywane w powiązaniu danych wyjściowych, po zakończeniu metody.

W tym przykładzie zapisuje wiele wiadomości w kolejce do tej samej kolejki przy użyciu `ICollector`:

```csharp
public static class ICollectorExample
{
    [FunctionName("CopyQueueMessageICollector")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-3")] string myQueueItem,
        [Queue("myqueue-items-destination")] ICollector<string> myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 1: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 2: {myQueueItem}");
    }
}
```

## <a name="logging"></a>Rejestrowanie

Aby rejestrować dane wyjściowe do dzienników przesyłania strumieniowego w języku C#, obejmują argumentu typu `TraceWriter`. Zaleca się jej nazwa `log`. Unikaj używania `Console.Write` w funkcji platformy Azure. 

`TraceWriter`jest zdefiniowany w [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Poziom dziennika `TraceWriter` można skonfigurować w [host.json](functions-host-json.md).

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

> [!NOTE]
> Informacji o nowszej struktury rejestrowania, który można użyć zamiast `TraceWriter`, zobacz [zapisu dzienniki w języku C# funkcje](functions-monitoring.md#write-logs-in-c-functions) w **Monitor usługi Azure Functions** artykułu.

## <a name="async"></a>Asynchroniczne

Aby funkcja asynchronicznego, użyj `async` — słowo kluczowe i przywracać `Task` obiektu.

```csharp
public static class AsyncExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token,
        TraceWriter log)
    {
        log.Info($"BlobCopy function processed.");
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="cancellation-tokens"></a>Anulowanie tokenów

Niektóre operacje wymagają łagodne zamykanie. Mimo że zawsze jest najlepiej napisać kod, który może obsługiwać awarii, w przypadkach, w którym mają być obsługiwane żądania zamknięcia, zdefiniuj [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typu argumentu.  A `CancellationToken` podano sygnalizują wyzwoleniu zamknięcie hosta.

```csharp
public static class CancellationTokenExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="environment-variables"></a>Zmienne środowiskowe

Aby uzyskać wartość zmiennej środowiskowej lub wartość ustawienia aplikacji, należy użyć `System.Environment.GetEnvironmentVariable`, jak pokazano w poniższym przykładzie:

```csharp
public static class EnvironmentVariablesExample
{
    [FunctionName("GetEnvironmentVariables")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
    {
        log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
        log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
        log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
    }

    public static string GetEnvironmentVariable(string name)
    {
        return name + ": " +
            System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
    }
}
```

## <a name="binding-at-runtime"></a>Powiązanie w czasie wykonywania

W języku C# i innych języków .NET, można użyć [imperatywnych](https://en.wikipedia.org/wiki/Imperative_programming) powiązanie wzorzec, w przeciwieństwie do [ *deklaratywne* ](https://en.wikipedia.org/wiki/Declarative_programming) powiązania w atrybutach. Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą ma zostać obliczony w czasie środowiska uruchomieniowego zamiast projektu. Z tego wzorca można powiązać z obsługiwanych danych wejściowych i wyjściowych powiązania na bieżąco w kodzie funkcji.

Zdefiniuj staje się niezbędna powiązania w następujący sposób:

- **Nie** dołączyć atrybut podpisu funkcji dla żądanego imperatywnych powiązania.
- Przekaż parametr wejściowy [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) lub [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Aby wykonać wiązania danych, użyj następującego wzorca C#.

  ```cs
  using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
  {
      ...
  }
  ```

  `BindingTypeAttribute`atrybut .NET, który definiuje Twoje powiązanie jest i `T` jest typem danych wejściowych lub wyjściowych, który jest obsługiwany przez ten typ powiązania. `T`nie może być `out` typ parametru (takie jak `out JObject`). Na przykład, w tabeli Mobile Apps output powiązanie obsługuje [sześć output typy](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ale można używać tylko [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)z powiązaniem nadrzędnych.

### <a name="single-attribute-example"></a>Przykład pojedynczy atrybut

Poniższy przykładowy kod tworzy [powiązania wyjściowego obiektu blob magazynu](functions-bindings-storage-blob.md#output) z obiektu blob ścieżki, która jest zdefiniowana w czasie wykonywania, następnie zapisuje ciąg obiektu blob.

```cs
public static class IBinderExample
{
    [FunctionName("CreateBlobUsingBinder")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-4")] string myQueueItem,
        IBinder binder,
        TraceWriter log)
    {
        log.Info($"CreateBlobUsingBinder function processed: {myQueueItem}");
        using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
                    $"samples-output/{myQueueItem}", FileAccess.Write)))
        {
            writer.Write("Hello World!");
        };
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definiuje [obiektu blob magazynu](functions-bindings-storage-blob.md) wejściowych lub wyjściowych powiązanie, i [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) jest typ powiązania obsługiwanych danych wyjściowych.

### <a name="multiple-attribute-example"></a>Wiele przykład atrybutu

Powyższy przykład pobiera ustawienia aplikacji dla aplikacji funkcja parametrów połączenia w głównym konta magazynu (czyli `AzureWebJobsStorage`). Można określić ustawienie niestandardowych aplikacji, aby użyć konta magazynu przez dodanie [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) i przekazanie tablicy atrybut do `BindAsync<T>()`. Użyj `Binder` parametru nie `IBinder`.  Na przykład:

```cs
public static class IBinderExampleMultipleAttributes
{
    [FunctionName("CreateBlobInDifferentStorageAccount")]
    public async static Task RunAsync(
            [QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
            Binder binder,
            TraceWriter log)
    {
        log.Info($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
        var attributes = new Attribute[]
        {
        new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
        new StorageAccountAttribute("MyStorageAccount")
        };
        using (var writer = await binder.BindAsync<TextWriter>(attributes))
        {
            await writer.WriteAsync("Hello World!!");
        }
    }
}
```

## <a name="triggers-and-bindings"></a>Wyzwalacze i powiązania 

W poniższej tabeli wymieniono powiązania atrybutów, które są dostępne w programie Azure Functions projektu biblioteki klas i wyzwalaczy. Atrybuty w przestrzeni nazw `Microsoft.Azure.WebJobs`.

| Wyzwalacz | Dane wejściowe | Dane wyjściowe|
|------   | ------    | ------  |
| [BlobTrigger](functions-bindings-storage-blob.md#trigger---attributes)| [Blob](functions-bindings-storage-blob.md#input---attributes)| [Blob](functions-bindings-storage-blob.md#output---attributes)|
| [CosmosDBTrigger](functions-bindings-cosmosdb.md#trigger---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#input---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#output---attributes) |
| [EventHubTrigger](functions-bindings-event-hubs.md#trigger---attributes)|| [EventHub](functions-bindings-event-hubs.md#output---attributes) |
| [HTTPTrigger](functions-bindings-http-webhook.md#trigger---attributes)|||
| [QueueTrigger](functions-bindings-storage-queue.md#trigger---attributes)|| [Queue](functions-bindings-storage-queue.md#output---attributes) |
| [ServiceBusTrigger](functions-bindings-service-bus.md#trigger---attributes)|| [ServiceBus](functions-bindings-service-bus.md#output---attributes) |
| [TimerTrigger](functions-bindings-timer.md#attributes) | ||
| |[ApiHubFile](functions-bindings-external-file.md)| [ApiHubFile](functions-bindings-external-file.md)|
| |[MobileTable](functions-bindings-mobile-apps.md#input---attributes)| [MobileTable](functions-bindings-mobile-apps.md#output---attributes) | 
| |[Tabela](functions-bindings-storage-table.md#input---attributes)| [Tabela](functions-bindings-storage-table.md#output---attributes)  | 
| ||[NotificationHub](functions-bindings-notification-hubs.md#attributes) |
| ||[SendGrid](functions-bindings-sendgrid.md#attributes) |
| ||[Twilio](functions-bindings-twilio.md#attributes)| 

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Dowiedz się więcej o wyzwalaczy i powiązań](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [Więcej informacji na temat najlepszych rozwiązań dla usługi Azure Functions](functions-best-practices.md)
