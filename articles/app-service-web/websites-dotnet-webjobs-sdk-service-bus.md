---
title: "Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs"
description: "Dowiedz się, jak używać tematów i kolejek usługi Azure Service Bus przy użyciu zestawu SDK zadań Webjob."
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="a63bd-103">Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs</span><span class="sxs-lookup"><span data-stu-id="a63bd-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="a63bd-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a63bd-104">Overview</span></span>
<span data-ttu-id="a63bd-105">Ten przewodnik zawiera C# przykłady kodu, których pokazano, jak do wyzwalania procesu po odebraniu wiadomości usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a63bd-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="a63bd-106">Kod przykłady użycia [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="a63bd-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="a63bd-107">Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a63bd-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="a63bd-108">Wstawki kodu Pokaż tylko funkcje, nie tworzy kodu `JobHost` obiektu jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a63bd-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="a63bd-109">A [pełny przykład kodu usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) znajduje się w repozytorium azure-zadań webjob sdk próbek w witrynie GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="a63bd-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="a63bd-110"><a id="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a63bd-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="a63bd-111">Do pracy z usługą Service Bus, musisz zainstalować [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) pakietu NuGet, oprócz innych pakietów zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="a63bd-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="a63bd-112">Należy również ustawić parametry połączenia AzureWebJobsServiceBus oprócz parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="a63bd-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="a63bd-113">Można to zrobić w `connectionStrings` sekcji w pliku App.config, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a63bd-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="a63bd-114">Aby uzyskać przykładowy projekt, który zawiera ustawienie parametrów połączenia magistrali usług w pliku App.config, zobacz [przykład usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="a63bd-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="a63bd-115">Można również ustawić parametry połączenia w środowisko uruchomieniowe platformy Azure, które następnie zastępują ustawienia App.config, po uruchomieniu zadania WebJob na platformie Azure; Aby uzyskać więcej informacji, zobacz [wprowadzenie do zestawu SDK WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a63bd-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="a63bd-116"><a id="trigger"></a>Sposób włączania funkcji po odebraniu komunikatu w kolejce usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="a63bd-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="a63bd-117">Aby napisać funkcję, która wywołuje zestaw SDK zadań Webjob po odebraniu komunikatu w kolejce, użyj `ServiceBusTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a63bd-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="a63bd-118">Konstruktor atrybutu ma parametr, który określa nazwę kolejki do sondowania.</span><span class="sxs-lookup"><span data-stu-id="a63bd-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="a63bd-119">Jak działa ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="a63bd-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="a63bd-120">Zestaw SDK odbiera wiadomości w `PeekLock` tryb i wywołania `Complete` na komunikat, jeśli funkcja zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli funkcja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="a63bd-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="a63bd-121">Jeśli funkcja uruchomione dłużej niż `PeekLock` limit czasu blokady automatycznie zostanie odnowiona.</span><span class="sxs-lookup"><span data-stu-id="a63bd-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="a63bd-122">Usługi Service Bus ma własną obsługi skażone kolejki, która nie może być kontrolowana ani skonfigurowane przez zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="a63bd-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="a63bd-123">Ciąg komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="a63bd-123">String queue message</span></span>
<span data-ttu-id="a63bd-124">Poniższy przykładowy kod odczytuje komunikat z kolejki, który zawiera ciąg i zapisuje ciąg do pulpitu nawigacyjnego, zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="a63bd-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="a63bd-125">**Uwaga:** wiadomości w kolejce w przypadku tworzenia w aplikacji, która nie korzysta z zestawu SDK zadań Webjob, upewnij się ustawić [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) do "text/plain".</span><span class="sxs-lookup"><span data-stu-id="a63bd-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="a63bd-126">Komunikat z kolejki POCO</span><span class="sxs-lookup"><span data-stu-id="a63bd-126">POCO queue message</span></span>
<span data-ttu-id="a63bd-127">Zestaw SDK zostanie automatycznie deserializacji komunikatu w kolejce, który zawiera dane JSON dla POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) typu.</span><span class="sxs-lookup"><span data-stu-id="a63bd-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="a63bd-128">Poniższy przykładowy kod odczytuje komunikat z kolejki, która zawiera `BlobInformation` obiektu, który ma `BlobName` właściwości:</span><span class="sxs-lookup"><span data-stu-id="a63bd-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="a63bd-129">Dla przykładów kodu przedstawiający sposób użycia właściwości POCO do pracy z obiektów blob i tabelach w tej samej funkcji, zobacz [wersji magazynu kolejek w tym artykule](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="a63bd-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="a63bd-130">Jeśli zestaw SDK zadań Webjob nie są używane swój kod, który tworzy komunikat z kolejki, należy użyć kodu podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="a63bd-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="a63bd-131">Typy ServiceBusTrigger współpracuje z</span><span class="sxs-lookup"><span data-stu-id="a63bd-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="a63bd-132">Oprócz `string` i POCO typy, można użyć `ServiceBusTrigger` atrybut z tablicy bajtów lub `BrokeredMessage` obiektu.</span><span class="sxs-lookup"><span data-stu-id="a63bd-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="a63bd-133"><a id="create"></a>Jak utworzyć wiadomości do kolejki usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="a63bd-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="a63bd-134">Aby napisać funkcję, która tworzy nowy Użyj komunikat kolejki `ServiceBus` atrybutu i przekaż nazwę kolejki do konstruktora atrybutów.</span><span class="sxs-lookup"><span data-stu-id="a63bd-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="a63bd-135">Utwórz pojedynczy komunikat z kolejki w funkcji z systemem innym niż async</span><span class="sxs-lookup"><span data-stu-id="a63bd-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="a63bd-136">Poniższy przykładowy kod używa parametru wyjściowego można utworzyć nowej wiadomości w kolejce o nazwie "outputqueue" o tej samej zawartości, co komunikat w kolejce o nazwie "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="a63bd-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="a63bd-137">Parametr wyjściowy do tworzenia pojedynczy komunikat z kolejki może być dowolny z następujących typów:</span><span class="sxs-lookup"><span data-stu-id="a63bd-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="a63bd-138">Można serializować typu POCO zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="a63bd-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="a63bd-139">Automatycznie zserializowanym w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a63bd-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="a63bd-140">Parametry typu POCO komunikatu w kolejce jest tworzony, gdy kończy się funkcja; Jeśli parametr ma wartość null, zestaw SDK tworzy komunikat z kolejki, która zwróci wartość null, gdy komunikat jest odbierany i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="a63bd-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="a63bd-141">Dla innych typów Jeśli parametr ma wartość null komunikatu w kolejce nie zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="a63bd-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="a63bd-142">Tworzenie wielu wiadomości w kolejce lub w funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="a63bd-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="a63bd-143">Aby utworzyć wiele komunikatów, użyj `ServiceBus` atrybutem `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w poniższym przykładzie kodu:</span><span class="sxs-lookup"><span data-stu-id="a63bd-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="a63bd-144">Każdy komunikat kolejki jest tworzony natychmiast po `Add` metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="a63bd-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="a63bd-145"><a id="topics"></a>Jak pracować z tematów usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="a63bd-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="a63bd-146">Aby napisać funkcję, która wywołuje zestawu SDK, gdy wiadomość zostanie odebrana na temat usługi Service Bus, użyj `ServiceBusTrigger` atrybut z konstruktora, który przyjmuje nazwy tematu i subskrypcji, jak pokazano w poniższym przykładzie kodu:</span><span class="sxs-lookup"><span data-stu-id="a63bd-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="a63bd-147">Aby utworzyć komunikat na temat, użyj `ServiceBus` atrybutu o nazwie tematu taki sam sposób korzystasz z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a63bd-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="a63bd-148">Funkcje dodane w wersji 1.1</span><span class="sxs-lookup"><span data-stu-id="a63bd-148">Features added in release 1.1</span></span>
<span data-ttu-id="a63bd-149">Następujące funkcje zostały dodane w wersji 1.1:</span><span class="sxs-lookup"><span data-stu-id="a63bd-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="a63bd-150">Zezwalaj na możliwość głębokiego dostosowania przetwarzania za pośrednictwem komunikatu `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="a63bd-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="a63bd-151">`MessagingProvider`Dostosowywanie usługi Service Bus obsługuje `MessagingFactory` i `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="a63bd-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="a63bd-152">A `MessageProcessor` wzorzec strategii pozwala na określenie procesora na kolejki/tematu.</span><span class="sxs-lookup"><span data-stu-id="a63bd-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="a63bd-153">Współbieżność przetwarzania komunikatu jest obsługiwany przez domyślną.</span><span class="sxs-lookup"><span data-stu-id="a63bd-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="a63bd-154">Łatwe dostosowywanie `OnMessageOptions` za pośrednictwem `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="a63bd-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="a63bd-155">Zezwalaj na [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) podane na `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (dla scenariuszy, w którym możesz nie mieć Zarządzanie prawami).</span><span class="sxs-lookup"><span data-stu-id="a63bd-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="a63bd-156">Należy pamiętać, że zadań Webjob Azure nie można automatycznie udostępnić nieistniejącej kolejki i tematy bez AccessRights zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a63bd-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="a63bd-157"><a id="queues"></a>Tematy pokrewne objętych artykułem porad kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="a63bd-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="a63bd-158">Aby uzyskać informacje o scenariuszach zestaw SDK zadań Webjob nie specyficzne dla usługi Service Bus, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a63bd-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="a63bd-159">Tematy w tym artykule są następujące:</span><span class="sxs-lookup"><span data-stu-id="a63bd-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="a63bd-160">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="a63bd-160">Async functions</span></span>
* <span data-ttu-id="a63bd-161">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="a63bd-161">Multiple instances</span></span>
* <span data-ttu-id="a63bd-162">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="a63bd-162">Graceful shutdown</span></span>
* <span data-ttu-id="a63bd-163">Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji</span><span class="sxs-lookup"><span data-stu-id="a63bd-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="a63bd-164">Ustaw parametry połączenia SDK w kodzie</span><span class="sxs-lookup"><span data-stu-id="a63bd-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="a63bd-165">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="a63bd-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="a63bd-166">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="a63bd-166">Trigger a function manually</span></span>
* <span data-ttu-id="a63bd-167">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="a63bd-167">Write logs</span></span>

## <span data-ttu-id="a63bd-168"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a63bd-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="a63bd-169">Ten przewodnik zawiera podane przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a63bd-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="a63bd-170">Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a63bd-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

