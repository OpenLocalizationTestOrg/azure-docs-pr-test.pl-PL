---
title: "Używanie bibliotek klas .NET z usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia biblioteki klas .NET do użycia w środowisku Azure Functions"
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
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="ac114-104">Używanie bibliotek klas .NET z usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ac114-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="ac114-105">Oprócz plików skryptów usługi Azure Functions obsługuje publikowania biblioteki klas jako implementacja jedną lub więcej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ac114-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="ac114-106">Firma Microsoft zaleca użycie [Azure funkcje programu Visual Studio 2017 narzędzia](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="ac114-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac114-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac114-107">Prerequisites</span></span> 

<span data-ttu-id="ac114-108">Ten artykuł zawiera następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="ac114-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="ac114-109">[W wersji zapoznawczej programu Visual Studio 2017 15 ustęp 3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="ac114-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="ac114-110">Zainstaluj obciążeń **ASP.NET i sieć web development** i **Azure programowanie**.</span><span class="sxs-lookup"><span data-stu-id="ac114-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="ac114-111">Funkcja Azure Tools dla programu Visual Studio 2017 r</span><span class="sxs-lookup"><span data-stu-id="ac114-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="ac114-112">Projektu biblioteki klas funkcji</span><span class="sxs-lookup"><span data-stu-id="ac114-112">Functions class library project</span></span>

<span data-ttu-id="ac114-113">W programie Visual Studio Utwórz nowy projekt usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ac114-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="ac114-114">Tworzy nowy szablon projektu pliki *host.json* i *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="ac114-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="ac114-115">Możesz [Dostosowywanie ustawień środowiska uruchomieniowego usługi Azure Functions w host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="ac114-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="ac114-116">Plik *local.settings.json* przechowuje ustawienia Azure funkcje podstawowe narzędzia, parametry połączenia i ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ac114-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="ac114-117">Aby dowiedzieć się więcej na temat jego struktury, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="ac114-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="ac114-118">Atrybut FunctionName</span><span class="sxs-lookup"><span data-stu-id="ac114-118">FunctionName attribute</span></span>

<span data-ttu-id="ac114-119">Atrybut [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) oznacza metodę jako punktu wejścia funkcji.</span><span class="sxs-lookup"><span data-stu-id="ac114-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="ac114-120">Musi on być używany z wyzwalaczem dokładnie jeden i 0 lub więcej wejściowa i wyjściowa powiązania.</span><span class="sxs-lookup"><span data-stu-id="ac114-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="ac114-121">Konwersja do function.json</span><span class="sxs-lookup"><span data-stu-id="ac114-121">Conversion to function.json</span></span>

<span data-ttu-id="ac114-122">Po utworzeniu projektu usługi Azure Functions generuje plik `function.json` w katalogu zgodnego z nazwą funkcji zdefiniowanych przez `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="ac114-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="ac114-123">Określa wyzwalaczy i powiązań i wskazuje na plik zestawu projektu.</span><span class="sxs-lookup"><span data-stu-id="ac114-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="ac114-124">Ta konwersja jest wykonywana przez pakiet NuGet [Microsoft\.NET\.Sdk\.funkcji](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="ac114-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="ac114-125">Źródło jest dostępne w repozytorium GitHub [azure\-funkcje\-vs\-kompilacji\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="ac114-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="ac114-126">Wyzwalacze i powiązania</span><span class="sxs-lookup"><span data-stu-id="ac114-126">Triggers and bindings</span></span>

<span data-ttu-id="ac114-127">W poniższej tabeli wymieniono wyzwalaczy i powiązań, które są dostępne w programie Azure Functions projektu biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="ac114-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="ac114-128">Atrybuty w przestrzeni nazw `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="ac114-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="ac114-129">Powiązanie</span><span class="sxs-lookup"><span data-stu-id="ac114-129">Binding</span></span> | <span data-ttu-id="ac114-130">Atrybut</span><span class="sxs-lookup"><span data-stu-id="ac114-130">Attribute</span></span> | <span data-ttu-id="ac114-131">Pakiet NuGet</span><span class="sxs-lookup"><span data-stu-id="ac114-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="ac114-132">Wyzwalacz magazynu obiektów blob, dane wejściowe, dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="ac114-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ac114-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ac114-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="ac114-135">[Magazynu obiektów blob]</span><span class="sxs-lookup"><span data-stu-id="ac114-135">[Blob storage]</span></span> |
| [<span data-ttu-id="ac114-136">Rozwiązania cosmos DB wejściowa i wyjściowa powiązania</span><span class="sxs-lookup"><span data-stu-id="ac114-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="ac114-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="ac114-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="ac114-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="ac114-139">Wyzwalacz centra zdarzeń i danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="ac114-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="ac114-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ac114-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="ac114-142">Plik zewnętrzny dane wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="ac114-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="ac114-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="ac114-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="ac114-145">Wyzwalacz protokołu HTTP i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="ac114-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="ac114-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="ac114-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="ac114-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="ac114-148">Aplikacje mobilne dane wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="ac114-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="ac114-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="ac114-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="ac114-151">Centra powiadomień w danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="ac114-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="ac114-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="ac114-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="ac114-154">Kolejki magazynu wyzwalacza i danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="ac114-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ac114-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ac114-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ac114-157">Dane wyjściowe SendGrid</span><span class="sxs-lookup"><span data-stu-id="ac114-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="ac114-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-158">[SendGridAttribute]</span></span> | <span data-ttu-id="ac114-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="ac114-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="ac114-160">Dane wyjściowe i wyzwalaczy usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="ac114-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="ac114-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="ac114-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ac114-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="ac114-163">Tabela magazynu wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="ac114-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ac114-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ac114-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ac114-166">Wyzwalacz czasomierza</span><span class="sxs-lookup"><span data-stu-id="ac114-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="ac114-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="ac114-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="ac114-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="ac114-169">Dane wyjściowe usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="ac114-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="ac114-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="ac114-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="ac114-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="ac114-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="ac114-172">Wyzwalacz magazynu obiektów blob, wejściowa i wyjściowa powiązania</span><span class="sxs-lookup"><span data-stu-id="ac114-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="ac114-173">Wyzwalacz obsługuje funkcje platformy Azure, wejściowa i wyjściowa powiązania dla magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac114-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ac114-174">Aby uzyskać więcej informacji na wyrażenia wiązania i metadanych, zobacz [powiązania magazynu obiektów Blob platformy Azure funkcji](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="ac114-175">Wyzwalacz obiektu blob jest zdefiniowana z `[BlobTrigger]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ac114-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="ac114-176">Można użyć atrybutu `[StorageAccount]` do definiowania konto magazynu jest używana przez całą funkcję lub klasy.</span><span class="sxs-lookup"><span data-stu-id="ac114-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="ac114-177">Obiekt blob danych wejściowych i wyjściowych są definiowane przy użyciu `[Blob]` atrybutu wraz z `FileAccess` parametr wskazujący odczytu lub zapisu.</span><span class="sxs-lookup"><span data-stu-id="ac114-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="ac114-178">W poniższym przykładzie użyto obiektu blob powiązania wyjściowego wyzwalacza i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ac114-178">The following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="ac114-179">Rozwiązania cosmos DB wejściowa i wyjściowa powiązania</span><span class="sxs-lookup"><span data-stu-id="ac114-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="ac114-180">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ac114-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="ac114-181">Aby dowiedzieć się więcej na temat funkcji, powiązania DB rozwiązania Cosmos, zobacz [powiązania bazy danych Azure funkcji rozwiązania Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="ac114-182">Aby powiązać dokumentu rozwiązania Cosmos bazy danych, użyj atrybutu `[DocumentDB]` w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="ac114-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="ac114-183">W poniższym przykładzie przedstawiono wyzwalacz kolejki i interfejs API usługi DocumentDB powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="ac114-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="ac114-184">Wyzwalacz centra zdarzeń i danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="ac114-185">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania usługi Event hubs.</span><span class="sxs-lookup"><span data-stu-id="ac114-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="ac114-186">Aby uzyskać więcej informacji, zobacz [powiązania Centrum zdarzeń funkcji Azure](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="ac114-187">Typy `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` i `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` są zdefiniowane w pakiecie NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ac114-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ac114-188">W poniższym przykładzie użyto wyzwalacz Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="ac114-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="ac114-189">W poniższym przykładzie przedstawiono Centrum zdarzeń danych wyjściowych za pomocą zwracana wartość metody jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ac114-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="ac114-190">Plik zewnętrzny dane wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-190">External file input and output</span></span>

<span data-ttu-id="ac114-191">Środowisko Azure Functions obsługuje wyzwalacza, dane wejściowe i powiązania danych wyjściowych dla plików zewnętrznych, takich jak dysk Google, Dropbox i OneDrive.</span><span class="sxs-lookup"><span data-stu-id="ac114-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="ac114-192">Aby dowiedzieć się więcej, zobacz [powiązania zewnętrznego pliku funkcji Azure](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="ac114-193">Atrybuty `[ExternalFileTrigger]` i `[ExternalFile]` są zdefiniowane w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="ac114-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="ac114-194">W poniższym przykładzie C# pokazano zewnętrzny plik wejściowa i wyjściowa powiązania.</span><span class="sxs-lookup"><span data-stu-id="ac114-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="ac114-195">Kod kopiuje plik wejściowy do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="ac114-195">The code copies the input file to the output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="ac114-196">HTTP i elementy webhook</span><span class="sxs-lookup"><span data-stu-id="ac114-196">HTTP and webhooks</span></span>

<span data-ttu-id="ac114-197">Użyj `HttpTrigger` atrybut do definiowania wyzwalacza HTTP lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="ac114-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="ac114-198">Ten atrybut jest zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="ac114-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="ac114-199">Można dostosować poziom autoryzacji, typ elementu webhook, trasy i metod.</span><span class="sxs-lookup"><span data-stu-id="ac114-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="ac114-200">W poniższym przykładzie zdefiniowano wyzwalacz protokołu HTTP przy użyciu uwierzytelniania anonimowego i _genericJson_ typu elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="ac114-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="ac114-201">Aplikacje mobilne dane wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-201">Mobile Apps input and output</span></span>

<span data-ttu-id="ac114-202">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="ac114-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="ac114-203">Aby dowiedzieć się więcej, zobacz [powiązania Azure funkcji Mobile Apps](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="ac114-204">Atrybut `[MobileTable]` jest zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="ac114-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="ac114-205">W poniższym przykładzie pokazano Mobile Apps powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="ac114-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="ac114-206">Centra powiadomień w danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-206">Notification Hubs output</span></span>

<span data-ttu-id="ac114-207">Azure Functions obsługuje powiązanie danych wyjściowych dla usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ac114-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="ac114-208">Aby dowiedzieć się więcej, zobacz [powiązania wyjściowego Centrum powiadomień Azure funkcji](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="ac114-209">Atrybut `[NotificationHub]` jest zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="ac114-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="ac114-210">Kolejki magazynu wyzwalacza i danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="ac114-210">Queue storage trigger and output</span></span>

<span data-ttu-id="ac114-211">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązań dla kolejek platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac114-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="ac114-212">Aby uzyskać więcej informacji, zobacz [powiązania magazynu kolejek Azure funkcji](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="ac114-213">Poniższy przykład przedstawia użycie zwracanego typu funkcji z kolejki danych wyjściowych powiązanie, używając `[Queue]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ac114-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="ac114-214">Aby zdefiniować wyzwalacz kolejki, należy użyć `[QueueTrigger]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ac114-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="ac114-215">Dane wyjściowe SendGrid</span><span class="sxs-lookup"><span data-stu-id="ac114-215">SendGrid output</span></span>

<span data-ttu-id="ac114-216">Środowisko Azure Functions obsługuje dane wyjściowe SendGrid powiązanie do wysyłania wiadomości e-mail programowo.</span><span class="sxs-lookup"><span data-stu-id="ac114-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="ac114-217">Aby dowiedzieć się więcej, zobacz [powiązania włączenie funkcji Azure](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="ac114-218">Atrybut `[SendGrid]` jest zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="ac114-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="ac114-219">Poniżej przedstawiono przykład wyzwalacza kolejki usługi Service Bus i użyciu powiązania danych wyjściowych SendGrid `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="ac114-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="ac114-220">Dane wyjściowe i wyzwalaczy usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="ac114-220">Service Bus trigger and output</span></span>

<span data-ttu-id="ac114-221">Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania dla tematów i kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ac114-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="ac114-222">Aby uzyskać więcej informacji na temat konfigurowania powiązań, zobacz [powiązania funkcji usługi Azure Service Bus](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="ac114-223">Atrybuty `[ServiceBusTrigger]` i `[ServiceBus]` są zdefiniowane w pakiecie NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ac114-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ac114-224">Poniżej przedstawiono przykład wyzwalacz kolejki usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="ac114-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="ac114-225">Poniżej przedstawiono przykład danych wyjściowych usługi Service Bus powiązanie, używając zwracany typ metody jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ac114-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="ac114-226">Tabela magazynu wejściowe i wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ac114-226">Table storage input and output</span></span>

<span data-ttu-id="ac114-227">Azure Functions obsługuje wejściowa i wyjściowa powiązania dla magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="ac114-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="ac114-228">Aby dowiedzieć się więcej, zobacz [powiązania magazynu tabel Azure funkcji](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="ac114-229">Poniższy przykład jest klasa z dwóch funkcji prezentacja magazynu w tabeli danych wyjściowych i wejściowych powiązania.</span><span class="sxs-lookup"><span data-stu-id="ac114-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="ac114-230">Wyzwalacz czasomierza</span><span class="sxs-lookup"><span data-stu-id="ac114-230">Timer trigger</span></span>

<span data-ttu-id="ac114-231">Środowisko Azure Functions ma powiązanie wyzwalacza czasomierza umożliwia uruchamianie funkcji kodu na podstawie zdefiniowanego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="ac114-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="ac114-232">Aby dowiedzieć się więcej na temat funkcji, powiązania, zobacz [zaplanować wykonanie kodu z usługi Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="ac114-233">W planie zużycie można określić harmonogramów z [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="ac114-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="ac114-234">Jeśli używasz planu usługi App Service umożliwia także ciągu TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="ac114-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="ac114-235">W poniższym przykładzie zdefiniowano wyzwalacz czasomierza wykonywana co 5 minut:</span><span class="sxs-lookup"><span data-stu-id="ac114-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="ac114-236">Dane wyjściowe usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="ac114-236">Twilio output</span></span>

<span data-ttu-id="ac114-237">Azure Functions obsługuje usługi Twilio output powiązania, aby umożliwić funkcji do wysyłania wiadomości SMS programu SMS.</span><span class="sxs-lookup"><span data-stu-id="ac114-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="ac114-238">Aby dowiedzieć się więcej, zobacz [powiązania wyjściowego wiadomości SMS wysłać z usługi Azure Functions przy użyciu usługi Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="ac114-239">Atrybut `[TwilioSms]` jest zdefiniowany w pakiecie [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="ac114-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="ac114-240">W poniższym przykładzie C# korzysta z kolejką usługi Twilio i wyzwalaczy powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="ac114-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="ac114-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac114-241">Next steps</span></span>

<span data-ttu-id="ac114-242">Aby uzyskać więcej informacji na temat używania usługi Azure Functions w języku C# skryptów, zobacz [Azure funkcje C\# skryptu dokumentacja dla deweloperów](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ac114-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="ac114-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="ac114-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="ac114-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="ac114-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="ac114-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="ac114-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="ac114-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="ac114-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="ac114-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="ac114-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="ac114-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="ac114-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ac114-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="ac114-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="ac114-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="ac114-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="ac114-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="ac114-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="ac114-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="ac114-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="ac114-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="ac114-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="ac114-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="ac114-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="ac114-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="ac114-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="ac114-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="ac114-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="ac114-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="ac114-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ac114-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
