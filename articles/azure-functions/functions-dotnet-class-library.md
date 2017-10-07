---
title: "aaaUsing .NET klasy bibliotek z usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bibliotek klas .NET tooauthor za pomocą usługi Azure Functions"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Używanie bibliotek klas .NET z usługi Azure Functions

Ponadto pliki tooscript, usługi Azure Functions obsługuje publikowania biblioteki klas jako hello implementacji dla jednego lub więcej funkcji. Zalecane jest użycie hello [Azure funkcje programu Visual Studio 2017 narzędzia](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Wymagania wstępne 

Ten artykuł zawiera hello następujące wymagania wstępne:

- [W wersji zapoznawczej programu Visual Studio 2017 15 ustęp 3](https://www.visualstudio.com/vs/preview/). Zainstaluj obciążeń hello **ASP.NET i sieć web development** i **Azure programowanie**.
- [Funkcja Azure Tools dla programu Visual Studio 2017 r](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Projektu biblioteki klas funkcji

W programie Visual Studio Utwórz nowy projekt usługi Azure Functions. Nowy szablon projektu Hello tworzy pliki hello *host.json* i *local.settings.json*. Możesz [Dostosowywanie ustawień środowiska uruchomieniowego usługi Azure Functions w host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

Plik Hello *local.settings.json* przechowuje ustawienia Azure funkcje podstawowe narzędzia, parametry połączenia i ustawień aplikacji. toolearn więcej informacji na temat jego struktury, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Atrybut FunctionName

Atrybut Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) oznacza metodę jako punktu wejścia funkcji. Musi on być używany z wyzwalaczem dokładnie jeden i 0 lub więcej wejściowa i wyjściowa powiązania.

### <a name="conversion-toofunctionjson"></a>Toofunction.json konwersji

Po utworzeniu projektu usługi Azure Functions generuje plik `function.json` w katalogu hello pasujących do nazwy funkcji hello zdefiniowane przez `[FunctionName]`. Określa wyzwalaczy i powiązań i punkty toohello projektu zestawu plików.

Ta konwersja jest wykonywana przez pakiet NuGet hello [Microsoft\.NET\.Sdk\.funkcji](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). Witaj źródło jest dostępne w repozytorium GitHub hello [azure\-funkcje\-vs\-kompilacji\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Wyzwalacze i powiązania

Witaj poniższej tabeli wymieniono hello wyzwalaczy i powiązań, które są dostępne w programie Azure Functions projektu biblioteki klas. Atrybuty w przestrzeni nazw hello `Microsoft.Azure.WebJobs`.

| Powiązanie | Atrybut | Pakiet NuGet |
|------   | ------    | ------        |
| [Wyzwalacz magazynu obiektów blob, dane wejściowe, dane wyjściowe](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Magazynu obiektów blob] |
| [Rozwiązania cosmos DB wejściowa i wyjściowa powiązania](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Wyzwalacz centra zdarzeń i danych wyjściowych](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Plik zewnętrzny dane wejściowe i wyjściowe](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Wyzwalacz protokołu HTTP i elementu webhook](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Aplikacje mobilne dane wejściowe i wyjściowe](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Centra powiadomień w danych wyjściowych](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Kolejki magazynu wyzwalacza i danych wyjściowych](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Dane wyjściowe SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Dane wyjściowe i wyzwalaczy usługi Service Bus](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Tabela magazynu wejściowe i wyjściowe](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Wyzwalacz czasomierza](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Dane wyjściowe usługi Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Wyzwalacz magazynu obiektów blob, wejściowa i wyjściowa powiązania

Wyzwalacz obsługuje funkcje platformy Azure, wejściowa i wyjściowa powiązania dla magazynu obiektów Blob platformy Azure. Aby uzyskać więcej informacji na wyrażenia wiązania i metadanych, zobacz [powiązania magazynu obiektów Blob platformy Azure funkcji](functions-bindings-storage-blob.md).

Wyzwalacz obiektu blob jest zdefiniowana z hello `[BlobTrigger]` atrybutu. Można użyć atrybutu hello `[StorageAccount]` toodefine hello magazynu konta, które jest używane przez całą funkcję lub klasy.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

Obiekt blob danych wejściowych i wyjściowych są definiowane przy użyciu hello `[Blob]` atrybutu wraz z `FileAccess` parametr wskazujący odczytu lub zapisu. Witaj następujący przykład używa wyzwalacz obiektów blob i powiązania wyjściowego obiektu blob.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Rozwiązania cosmos DB wejściowa i wyjściowa powiązania

Azure Functions obsługuje wejściowa i wyjściowa powiązania dla DB rozwiązania Cosmos. toolearn więcej informacji na temat funkcji hello hello DB rozwiązania Cosmos powiązania, zobacz [powiązania bazy danych Azure funkcji rozwiązania Cosmos](functions-bindings-documentdb.md).

tooa toobind DB rozwiązania Cosmos dokumentu, użyj atrybutu hello `[DocumentDB]` w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Poniższy przykład Hello ma wyzwalacz kolejki i interfejs API usługi DocumentDB powiązania wyjściowego:

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Wyzwalacz centra zdarzeń i danych wyjściowych

Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania usługi Event hubs. Aby uzyskać więcej informacji, zobacz [powiązania Centrum zdarzeń funkcji Azure](functions-bindings-event-hubs.md).

Witaj typy `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` i `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` są zdefiniowane w pakiecie NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Witaj poniższym przykładzie użyto wyzwalacz Centrum zdarzeń:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Witaj poniższym przykładzie przedstawiono Centrum zdarzeń danych wyjściowych przy użyciu wartości zwracanych metody hello jako dane wyjściowe hello:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>Plik zewnętrzny dane wejściowe i wyjściowe

Środowisko Azure Functions obsługuje wyzwalacza, dane wejściowe i powiązania danych wyjściowych dla plików zewnętrznych, takich jak dysk Google, Dropbox i OneDrive. toolearn więcej, zobacz [powiązania zewnętrznego pliku funkcji Azure](functions-bindings-external-file.md). Witaj atrybuty `[ExternalFileTrigger]` i `[ExternalFile]` są zdefiniowane w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hello poniższy przykład C# pokazuje zewnętrzny plik wejściowa i wyjściowa powiązania. kopie kodu Hello hello pliku wyjściowego toohello pliku wejściowego.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP i elementy webhook

Użyj hello `HttpTrigger` wyzwalacz toodefine HTTP atrybutu lub elementu webhook. Ten atrybut jest zdefiniowany w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http]. Można dostosować poziom autoryzacji hello, typ elementu webhook trasy i metod. Witaj poniższym przykładzie zdefiniowano wyzwalacz protokołu HTTP przy użyciu uwierzytelniania anonimowego i _genericJson_ typu elementu webhook.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Aplikacje mobilne dane wejściowe i wyjściowe

Azure Functions obsługuje wejściowa i wyjściowa powiązania dla aplikacji mobilnych. toolearn więcej, zobacz [powiązania Azure funkcji Mobile Apps](functions-bindings-mobile-apps.md). Atrybut Hello `[MobileTable]` jest zdefiniowany w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].

Witaj poniższym przykładzie pokazano Mobile Apps powiązania wyjściowego:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Centra powiadomień w danych wyjściowych

Azure Functions obsługuje powiązanie danych wyjściowych dla usługi Notification Hubs. toolearn więcej, zobacz [powiązania wyjściowego Centrum powiadomień Azure funkcji](functions-bindings-notification-hubs.md). Atrybut Hello `[NotificationHub]` jest zdefiniowany w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Kolejki magazynu wyzwalacza i danych wyjściowych

Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązań dla kolejek platformy Azure. Aby uzyskać więcej informacji, zobacz [powiązania magazynu kolejek Azure funkcji](functions-bindings-storage-queue.md).

Witaj poniższy przykład przedstawia sposób toouse hello typ zwracany funkcji z kolejki danych wyjściowych powiązanie, używając hello `[Queue]` atrybutu. toodefine wyzwalacz kolejki użyć hello `[QueueTrigger]` atrybutu.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>Dane wyjściowe SendGrid

Środowisko Azure Functions obsługuje dane wyjściowe SendGrid powiązanie do wysyłania wiadomości e-mail programowo. toolearn więcej, zobacz [powiązania włączenie funkcji Azure](functions-bindings-sendgrid.md).

Atrybut Hello `[SendGrid]` jest zdefiniowany w pakiecie NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Witaj poniżej znajduje się przykład wyzwalacza kolejki usługi Service Bus i użyciu powiązania danych wyjściowych SendGrid `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Dane wyjściowe i wyzwalaczy usługi Service Bus

Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania dla tematów i kolejek usługi Service Bus. Aby uzyskać więcej informacji na temat konfigurowania powiązań, zobacz [powiązania funkcji usługi Azure Service Bus](functions-bindings-service-bus.md).

Witaj atrybuty `[ServiceBusTrigger]` i `[ServiceBus]` są zdefiniowane w pakiecie NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Witaj, poniżej przedstawiono przykładowy wyzwalacza kolejki usługi Service Bus:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Witaj poniżej znajduje się przykład danych wyjściowych usługi Service Bus powiązanie, używając zwracany typ metody hello jako dane wyjściowe hello:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>Tabela magazynu wejściowe i wyjściowe

Azure Functions obsługuje wejściowa i wyjściowa powiązania dla magazynu tabel Azure. toolearn więcej, zobacz [powiązania magazynu tabel Azure funkcji](functions-bindings-storage-table.md).

Witaj poniższym przykładzie jest klasą z dwóch funkcji prezentacja magazynu w tabeli danych wyjściowych i wejściowych powiązania. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>Wyzwalacz czasomierza

Środowisko Azure Functions ma powiązanie wyzwalacza czasomierza umożliwia uruchamianie funkcji kodu na podstawie zdefiniowanego harmonogramu. Zobacz toolearn więcej informacji na temat funkcji hello powiązania hello [zaplanować wykonanie kodu z usługi Azure Functions](functions-bindings-timer.md).

W planie zużycie hello, można określić harmonogramów z [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Jeśli używasz planu usługi App Service umożliwia także ciągu TimeSpan. 

Poniższy przykład Hello definiuje wyzwalacza bazującego na czasomierzu wykonywana co 5 minut:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Dane wyjściowe usługi Twilio

Azure Functions obsługuje usługi Twilio output tooenable powiązania funkcji toosend SMS tekst wiadomości. toolearn więcej, zobacz [powiązania wyjściowego wiadomości SMS wysłać z usługi Azure Functions przy użyciu hello usługi Twilio](functions-bindings-twilio.md). 

Atrybut Hello `[TwilioSms]` jest zdefiniowany w pakiecie hello [Microsoft.Azure.WebJobs.Extensions.Twilio].

Witaj C# przykładzie użyto kolejki usługi Twilio i wyzwalaczy powiązania wyjściowego:

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat używania usługi Azure Functions w języku C# skryptów, zobacz [Azure funkcje C\# skryptu dokumentacja dla deweloperów](functions-reference-csharp.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
