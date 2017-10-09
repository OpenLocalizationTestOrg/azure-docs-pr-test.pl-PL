---
title: "aaaHow toouse Azure Service Bus z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak zestaw SDK zadań Webjob hello toouse Azure Service Bus kolejek i tematów."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="b7f36-103">W jaki sposób toouse usługa Azure Service Bus z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="b7f36-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="b7f36-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b7f36-104">Overview</span></span>
<span data-ttu-id="b7f36-105">Ten przewodnik zawiera C# jak przykłady kodu przedstawiające tootrigger proces po odebraniu wiadomości usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7f36-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="b7f36-106">Przykłady kodu Hello użyj [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="b7f36-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="b7f36-107">Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b7f36-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="b7f36-108">wstawki kodu Hello Pokaż tylko funkcje, nie hello kod, który tworzy hello `JobHost` obiektu jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b7f36-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="b7f36-109">A [pełny przykład kodu usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) znajduje się w repozytorium azure-zadań webjob sdk przykłady hello w witrynie GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="b7f36-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="b7f36-110"><a id="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7f36-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="b7f36-111">toowork usługi Service Bus oferuje tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pakietu dodatkowo toohello inne pakiety zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="b7f36-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="b7f36-112">Masz również parametry połączenia AzureWebJobsServiceBus hello tooset w parametry połączenia magazynu toohello dodanie.</span><span class="sxs-lookup"><span data-stu-id="b7f36-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="b7f36-113">Można to zrobić w hello `connectionStrings` sekcji hello pliku App.config, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b7f36-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="b7f36-114">Aby uzyskać przykładowy projekt, który zawiera ustawienie parametrów połączenia usługi Service Bus hello w pliku App.config hello, zobacz [przykład usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="b7f36-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="b7f36-115">można również ustawić parametry połączenia Hello w hello środowiska uruchomieniowego platformy Azure, które następnie zastępują ustawienia App.config hello, po uruchomieniu hello zadania WebJob na platformie Azure; Aby uzyskać więcej informacji, zobacz [wprowadzenie hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b7f36-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="b7f36-116"><a id="trigger"></a>Jak odebraniu tootrigger funkcja, gdy komunikat kolejki usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="b7f36-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="b7f36-117">wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello `ServiceBusTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="b7f36-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="b7f36-118">Konstruktor atrybutu Hello przyjmuje parametr określający nazwę hello hello toopoll kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7f36-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="b7f36-119">Jak działa ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="b7f36-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="b7f36-120">Hello SDK odbiera komunikat w `PeekLock` tryb i wywołania `Complete` na wiadomość powitania, jeśli funkcja hello zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli funkcja hello nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b7f36-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="b7f36-121">Jeśli funkcja hello uruchomione dłużej niż hello `PeekLock` limit czasu blokady hello jest automatycznie odnawiane.</span><span class="sxs-lookup"><span data-stu-id="b7f36-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="b7f36-122">Usługi Service Bus ma własną obsługi skażone kolejki, która nie może być kontrolowana ani konfigurowane za pomocą hello zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="b7f36-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="b7f36-123">Ciąg komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="b7f36-123">String queue message</span></span>
<span data-ttu-id="b7f36-124">Witaj Poniższy przykładowy kod odczytuje komunikat z kolejki, zawiera ciąg, który zapisuje toohello ciąg hello zestaw SDK zadań Webjob pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7f36-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="b7f36-125">**Uwaga:** w przypadku tworzenia hello kolejki komunikatów w aplikacji, która nie używa hello zestaw SDK zadań Webjob, upewnij się, że tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) zbyt "text/plain".</span><span class="sxs-lookup"><span data-stu-id="b7f36-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="b7f36-126">Komunikat z kolejki POCO</span><span class="sxs-lookup"><span data-stu-id="b7f36-126">POCO queue message</span></span>
<span data-ttu-id="b7f36-127">Hello SDK zostanie automatycznie deserializacji komunikatu w kolejce, który zawiera dane JSON dla POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) typu.</span><span class="sxs-lookup"><span data-stu-id="b7f36-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="b7f36-128">Witaj Poniższy przykładowy kod odczytuje komunikat z kolejki, która zawiera `BlobInformation` obiektu, który ma `BlobName` właściwości:</span><span class="sxs-lookup"><span data-stu-id="b7f36-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="b7f36-129">Aby uzyskać przykłady kodu przedstawiający sposób hello takie same właściwości toouse hello toowork POCO z obiektów blob i tabelach w funkcji, zobacz hello [wersji magazynu kolejek w tym artykule](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="b7f36-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="b7f36-130">Jeśli swój kod, który tworzy komunikat z kolejki hello nie używa hello zestaw SDK zadań Webjob, należy użyć kodu toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b7f36-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="b7f36-131">Typy ServiceBusTrigger współpracuje z</span><span class="sxs-lookup"><span data-stu-id="b7f36-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="b7f36-132">Oprócz `string` i POCO typy, można użyć hello `ServiceBusTrigger` atrybut z tablicy bajtów lub `BrokeredMessage` obiektu.</span><span class="sxs-lookup"><span data-stu-id="b7f36-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="b7f36-133"><a id="create"></a>Jak toocreate usługi Service Bus kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="b7f36-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="b7f36-134">toowrite funkcję, która tworzy nowy komunikat kolejki użyć hello `ServiceBus` atrybutu i podaj hello kolejki nazwa toohello atrybut konstruktora.</span><span class="sxs-lookup"><span data-stu-id="b7f36-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="b7f36-135">Utwórz pojedynczy komunikat z kolejki w funkcji z systemem innym niż async</span><span class="sxs-lookup"><span data-stu-id="b7f36-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="b7f36-136">powitania po przykładowy kod używa toocreate parametru wyjściowego nowej wiadomości w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello komunikat w kolejce hello o nazwie "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="b7f36-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="b7f36-137">Parametr wyjściowy Hello tworzenia pojedynczy komunikat z kolejki mogą być następujące typy hello:</span><span class="sxs-lookup"><span data-stu-id="b7f36-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="b7f36-138">Można serializować typu POCO zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="b7f36-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="b7f36-139">Automatycznie zserializowanym w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b7f36-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="b7f36-140">Parametry typu POCO komunikatu w kolejce jest tworzony, gdy kończy się funkcja hello; Jeśli parametr hello ma wartość null, hello SDK tworzy komunikat z kolejki, który zwróci wartość null, podczas wiadomości powitania jest odbierany i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="b7f36-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="b7f36-141">Dla hello innych typów, jeśli parametr hello ma wartość null komunikatu w kolejce nie zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="b7f36-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="b7f36-142">Tworzenie wielu wiadomości w kolejce lub w funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="b7f36-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="b7f36-143">toocreate wiele komunikatów, należy użyć hello `ServiceBus` atrybutem `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w powitania po przykładowym kodzie:</span><span class="sxs-lookup"><span data-stu-id="b7f36-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="b7f36-144">Każdy komunikat kolejki jest tworzony natychmiast po hello `Add` metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="b7f36-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="b7f36-145"><a id="topics"></a>Jak toowork z tematów usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="b7f36-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="b7f36-146">wywołuje funkcję hello SDK toowrite po odebraniu wiadomości na temat usługi Service Bus, użyj hello `ServiceBusTrigger` atrybut z konstruktora hello, który przyjmuje nazwy tematu i subskrypcji, jak pokazano w powitania po przykładowym kodzie:</span><span class="sxs-lookup"><span data-stu-id="b7f36-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="b7f36-147">toocreate komunikat na temat użycia hello `ServiceBus` atrybutem hello nazwa tematu sam sposobu korzystania z kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7f36-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="b7f36-148">Funkcje dodane w wersji 1.1</span><span class="sxs-lookup"><span data-stu-id="b7f36-148">Features added in release 1.1</span></span>
<span data-ttu-id="b7f36-149">Witaj, następujące funkcje zostały dodane w wersji 1.1:</span><span class="sxs-lookup"><span data-stu-id="b7f36-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="b7f36-150">Zezwalaj na możliwość głębokiego dostosowania przetwarzania za pośrednictwem komunikatu `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="b7f36-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="b7f36-151">`MessagingProvider`Dostosowywanie hello usługi Service Bus obsługuje `MessagingFactory` i `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="b7f36-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="b7f36-152">A `MessageProcessor` strategii wzorzec umożliwia toospecify procesora na kolejki/tematu.</span><span class="sxs-lookup"><span data-stu-id="b7f36-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="b7f36-153">Współbieżność przetwarzania komunikatu jest obsługiwany przez domyślną.</span><span class="sxs-lookup"><span data-stu-id="b7f36-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="b7f36-154">Łatwe dostosowywanie `OnMessageOptions` za pośrednictwem `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="b7f36-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="b7f36-155">Zezwalaj na [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe określone na `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (dla scenariuszy, w którym możesz nie mieć Zarządzanie prawami).</span><span class="sxs-lookup"><span data-stu-id="b7f36-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="b7f36-156">Należy pamiętać, że zadań Webjob Azure tooautomatically nie można udostępnić nieistniejącą kolejek i tematów bez AccessRights zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b7f36-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="b7f36-157"><a id="queues"></a>Tematy pokrewne objętych hello magazynu kolejek jak tooarticle</span><span class="sxs-lookup"><span data-stu-id="b7f36-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="b7f36-158">Aby uzyskać informacje o scenariuszach zestaw SDK zadań Webjob nie dotyczą tooService magistrali, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b7f36-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="b7f36-159">Tematy w tym artykule Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b7f36-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="b7f36-160">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="b7f36-160">Async functions</span></span>
* <span data-ttu-id="b7f36-161">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="b7f36-161">Multiple instances</span></span>
* <span data-ttu-id="b7f36-162">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="b7f36-162">Graceful shutdown</span></span>
* <span data-ttu-id="b7f36-163">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="b7f36-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="b7f36-164">Ustawianie parametrów połączenia SDK hello w kodzie</span><span class="sxs-lookup"><span data-stu-id="b7f36-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="b7f36-165">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="b7f36-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="b7f36-166">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="b7f36-166">Trigger a function manually</span></span>
* <span data-ttu-id="b7f36-167">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="b7f36-167">Write logs</span></span>

## <span data-ttu-id="b7f36-168"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7f36-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="b7f36-169">W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7f36-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="b7f36-170">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="b7f36-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

