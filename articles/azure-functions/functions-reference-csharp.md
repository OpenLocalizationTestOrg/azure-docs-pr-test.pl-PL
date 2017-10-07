---
title: "aaaAzure dokumentacja dla deweloperów funkcje skryptu C# | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toodevelop usługi Azure Functions przy użyciu języka C#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure funkcje skryptu developer odwołanie w C#
> [!div class="op_single_selector"]
> * [Skryptu C#](functions-reference-csharp.md)
> * [Skrypt F #](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

środowisko skryptu C# dla usługi Azure Functions Hello jest oparta na hello Azure WebJobs SDK. Przepływy danych w funkcji języka C# za pomocą argumenty metody. Argument nazwy zostały określone w `function.json`, i jest wstępnie zdefiniowanych nazw do uzyskiwania dostępu do czynności, takie jak hello tokenów funkcja rejestratora i anulowania.

W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).

Aby uzyskać informacje o użyciu języka C# klasy biblioteki, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>Jak działa csx
Witaj `.csx` format umożliwia toowrite mniej "standardowy" i skoncentrować się na temat pisania tylko C# funkcję. Obejmują wszystkie odwołania do zestawów i przestrzeni nazw na początku hello pliku hello w zwykły sposób. Zamiast zawijania wszystkie elementy w przestrzeni nazw i klasy, wystarczy zdefiniować `Run` metody. Jeśli potrzebujesz tooinclude wszystkie klasy, dla wystąpienia toodefine zwykły obiekty stary obiekt CLR (POCO), można dołączyć klasy wewnątrz hello tego samego pliku.   

## <a name="binding-tooarguments"></a>Powiązanie tooarguments
Witaj różnych powiązania są powiązane tooa C# funkcja za pośrednictwem hello `name` właściwości w hello *function.json* konfiguracji. Każdego powiązania ma własną obsługiwanych typów; na przykład wyzwalacza obiektu blob może obsługiwać ciąg, POCO lub CloudBlockBlob. Witaj, obsługiwane typy są udokumentowane w hello odwołania dla każdego powiązania. Obiekt POCO musi mieć określonej metody pobierającej i ustawiającej zdefiniowane dla każdej właściwości.

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a>Dla powiązania danych wyjściowych przy użyciu wartości zwracanej — metoda

Można użyć wartość zwracaną metody dla powiązania danych wyjściowych przy użyciu nazwy hello `$return` w *function.json*:

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a>Trwa zapisywanie wielu wartości danych wyjściowych

Powiązanie output wiele wartości tooan toowrite, użyj hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typów. Te typy są tylko do zapisu kolekcje, które są napisane toohello powiązanie dane wyjściowe po zakończeniu metody hello.

W tym przykładzie zapisuje wiele wiadomości w kolejce za pomocą `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Rejestrowanie
toolog output tooyour dzienniki przesyłania strumieniowego w języku C#, obejmują argumentu typu `TraceWriter`. Zaleca się jej nazwa `log`. Unikaj używania `Console.Write` w funkcji platformy Azure. 

`TraceWriter`jest zdefiniowany w hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Witaj poziom dziennika `TraceWriter` można skonfigurować w [hosta\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Asynchroniczne
toomake funkcję asynchroniczną, użyj hello `async` — słowo kluczowe i przywracać `Task` obiektu.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Token anulowania
Niektóre operacje wymagają łagodne zamykanie. Mimo że zawsze jest najlepsze kodu toowrite, który może obsługiwać awarii w przypadkach, w którym ma toohandle łagodne zamykanie żądania, należy zdefiniować [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typu argumentu.  A `CancellationToken` podano toosignal wyzwoleniu zamknięcie hosta.

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a>Importowanie przestrzenie nazw
Jeśli potrzebujesz tooimport przestrzeni nazw, możesz to zrobić w zwykły sposób, z hello `using` klauzuli.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Witaj następujących przestrzeni nazw są automatycznie importowane i w związku z tym są opcjonalne:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Zewnętrzne zestawy odwołujące
Dla zestawów struktury, dodaj odwołania przy użyciu hello `#r "AssemblyName"` dyrektywy.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Witaj następujące zestawy są automatycznie dodawane hello Azure Functions Środowisko hostingu:

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

Witaj następujące zestawy mogą odwoływać się prostą nazwę (na przykład `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Odwołania do zestawów niestandardowych

tooreference niestandardowego zestawu, możesz użyć dowolnej *udostępnionego* zestawu lub *prywatnej* zestawu:
- Zestawy udostępnione są współużytkowane przez wszystkie funkcje w aplikacji funkcji. tooreference niestandardowego zestawu, Przekaż hello zestawu tooyour funkcji aplikacji, takich jak w `bin` folder w katalogu głównym aplikacji funkcja hello. 
- Zestawy prywatne są częścią kontekstu daną funkcję i obsługuje ładowania bezpośredniego w różnych wersjach. Zestawy prywatne należy przekazać w `bin` folderu w katalogu funkcji hello. Odwołanie przy użyciu nazwy pliku hello, takich jak `#r "MyAssembly.dll"`. 

Dla informacji na temat sposobu tooupload folder funkcja tooyour plików Zobacz hello następujących sekcji, pakiet zarządzania.

### <a name="watched-directories"></a>Monitorowane katalogów

Witaj katalog, który zawiera plik skryptu funkcji hello automatycznie jest monitorowana dla tooassemblies zmiany. toowatch zestawu zmian w innych katalogów, dodaj je toohello `watchDirectories` na liście [hosta\.json].

## <a name="using-nuget-packages"></a>Za pomocą pakietów NuGet
Przekaż toouse pakietów NuGet w języku C# funkcję, *project.json* toohello funkcja folder pliku w systemie plików hello funkcji aplikacji. Oto przykład *project.json* pliku, który dodaje 1.1.0 odwołania tooMicrosoft.ProjectOxford.Face wersji:

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

Witaj .NET Framework 4.6 jest obsługiwana tylko, upewnij się, że Twoje *project.json* Określa plik `net46` w sposób pokazany poniżej.

Po przekazaniu *project.json* plików, hello środowiska uruchomieniowego pobiera pakiety hello i automatycznie dodaje odwołania toohello pakiet zestawów. Nie ma potrzeby tooadd `#r "AssemblyName"` dyrektywy. toouse hello typów zdefiniowanych w pakietach NuGet hello, Dodaj wymagane hello `using` tooyour instrukcje *run.csx* pliku 

W środowisku uruchomieniowym funkcje hello, przywracanie NuGet działa na podstawie porównania ilości `project.json` i `project.lock.json`. Jeśli hello Data i godzina sygnatur plików hello **nie** uruchamia Przywracanie NuGet dopasowania i pliki do pobrania NuGet zaktualizowane pakiety. Jednakże, jeżeli hello Data i godzina sygnatur plików hello **czy** dopasowania, NuGet nie wykonuje operację przywracania. W związku z tym `project.lock.json` nie powinny zostać wdrożone, ponieważ powoduje ona przywracanie pakietu NuGet tooskip. Wdrażanie blokady hello tooavoid plików, dodawanie hello `project.lock.json` toohello `.gitignore` pliku.

toouse niestandardowe źródło danych NuGet, określ hello źródła danych w *Nuget.Config* pliku w katalogu głównym aplikacji funkcji hello. Aby uzyskać więcej informacji, zobacz [NuGet Konfigurowanie zachowania](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Przy użyciu pliku project.json
1. Open — funkcja hello w hello portalu Azure. Hello rejestruje dane wyjściowe kartę Wyświetla hello pakietu instalacji.
2. tooupload pliku project.json, użyj jednej z metod hello opisanych w hello [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate) w temacie odwołania dla deweloperów usługi Azure Functions hello.
3. Po hello *project.json* przekazać pliku, wyświetlone dane wyjściowe podobne hello poniższy przykład w funkcji do przesyłania strumieniowego dzienników:

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>Zmienne środowiskowe
tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `System.Environment.GetEnvironmentVariable`, jak pokazano w hello poniższy przykład kodu:

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
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
```

## <a name="reusing-csx-code"></a>Ponowne wykorzystywanie kodu csx
Można użyć klasy i metody zdefiniowane w innych *csx* pliki w Twojej *run.csx* pliku. toodo używanego, `#load` dyrektywy w Twojej *run.csx* pliku. W hello poniższy przykład, nazwę procedury rejestrowania `MyLogger` są udostępniane w *myLogger.csx* i ładowane do *run.csx* przy użyciu hello `#load` dyrektywy:

Przykład *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Przykład *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Za pomocą udostępnionej *csx* wspólnego wzorca należy toostrongly wpisać argumentów pomiędzy funkcjami przy użyciu obiektu POCO. W hello poniższy przykład uproszczony, wyzwalacza HTTP i kolejki wyzwalacza udziału obiektu POCO o nazwie `Order` toostrongly typu hello kolejność danych:

Przykład *run.csx* wyzwalacza HTTP:

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

Przykład *run.csx* wyzwalacza kolejki:

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

Przykład *order.csx*:

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

Można użyć ścieżki względnej z hello `#load` dyrektywy:

* `#load "mylogger.csx"`ładuje plik znajdujący się w folderze funkcja hello.
* `#load "loadedfiles\mylogger.csx"`ładuje plik znajdujący się w folderze w folderze funkcja hello.
* `#load "..\shared\mylogger.csx"`ładuje plik znajdujący się w folderze na powitania sam poziom jako folder funkcja hello, oznacza to, bezpośrednio pod *wwwroot*.

Witaj `#load` dyrektywy działa tylko w przypadku *csx* plików (C# skrypt), nie z *.cs* plików.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Powiązanie w czasie wykonywania za pośrednictwem powiązania imperatywne

W języku C# i innych języków .NET, można użyć [imperatywnych](https://en.wikipedia.org/wiki/Imperative_programming) wzorca wiązania jako min. toohello [ *deklaratywne* ](https://en.wikipedia.org/wiki/Declarative_programming) powiązania w *function.json*. Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą toobe obliczane w czasie środowiska uruchomieniowego zamiast projektu. Z tego wzorca można powiązać toosupported danych wejściowych i wyjściowych powiązania na bieżąco w kodzie funkcji.

Zdefiniuj staje się niezbędna powiązania w następujący sposób:

- **Nie** obejmują wpis w *function.json* dla żądanego imperatywnych powiązania.
- Przekaż parametr wejściowy [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) lub [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Użyj powitania po C# wzorzec tooperform hello wiązania z danymi.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

gdzie `BindingTypeAttribute` hello .NET atrybutu, który definiuje wiązania i `T` jest hello wejściowych lub wyjściowych typu, który jest obsługiwany przez ten typ powiązania. `T`nie może być `out` typ parametru (takie jak `out JObject`). Na przykład, w tabeli Mobile Apps output powiązanie obsługuje [sześć output typy](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ale można używać tylko [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) dla `T`.

Tworzy Hello następującego przykładowego kodu [powiązania wyjściowego obiektu blob magazynu](functions-bindings-storage-blob.md#using-a-blob-output-binding) z obiektu blob ścieżki, która jest zdefiniowana w czasie wykonywania, następnie zapisuje obiektu blob toohello ciągu.

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definiuje hello [obiektu blob magazynu](functions-bindings-storage-blob.md) wejściowych lub wyjściowych powiązanie, i [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) jest typ powiązania obsługiwanych danych wyjściowych.
Jest dostępna, hello kod pobiera hello domyślnym ustawieniem aplikacji hello parametry połączenia konta magazynu (czyli `AzureWebJobsStorage`). Toouse ustawienie niestandardowych aplikacji można określić, dodając [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) i przekazanie tablicy atrybutu hello do `BindAsync<T>()`. Na przykład:

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

Witaj poniższej tabeli wymieniono hello .NET atrybuty dla każdego powiązania typu hello pakietów i w których są zdefiniowane.

> [!div class="mx-codeBreakAll"]
| Powiązanie | Atrybut | Dodaj odwołanie |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Usługa Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Kolejki magazynu | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Obiektu blob magazynu | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Tabela magazynu | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md)
* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)
* [Azure dokumentacja dla deweloperów funkcje F #](functions-reference-fsharp.md)
* [Dokumentacja dla deweloperów NodeJS funkcji platformy Azure](functions-reference-node.md)
* [Azure funkcje wyzwalaczy i powiązań](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
