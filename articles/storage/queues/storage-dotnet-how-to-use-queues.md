---
title: "aaaGet pracy z magazynem kolejek Azure przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Usługa Azure Queues zapewnia niezawodne, asynchroniczne przesyłanie komunikatów między składnikami aplikacji. Chmury tooscale składniki Twojej aplikacji obsługi komunikatów włącza niezależnie."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="421d0-104">Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="421d0-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="421d0-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="421d0-105">Overview</span></span>
<span data-ttu-id="421d0-106">Usługa Azure Queue Storage umożliwia przesyłanie komunikatów za pomocą chmury między składnikami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="421d0-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="421d0-107">W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="421d0-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="421d0-108">Magazyn kolejek zapewnia asynchroniczną obsługę wiadomości do komunikacji między składnikami aplikacji, czy działają w chmurze hello, hello pulpitu, na serwerze lokalnym lub na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="421d0-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="421d0-109">Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="421d0-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="421d0-110">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="421d0-110">About this tutorial</span></span>
<span data-ttu-id="421d0-111">Ten samouczek pokazuje, jak kod toowrite .NET dla niektórych typowych scenariuszy przy użyciu magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="421d0-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="421d0-112">Omówione scenariusze obejmują tworzenie i usuwanie kolejek oraz dodawanie, odczytywanie i usuwanie komunikatów kolejek.</span><span class="sxs-lookup"><span data-stu-id="421d0-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="421d0-113">**Szacowany czas toocomplete:** 45 minut</span><span class="sxs-lookup"><span data-stu-id="421d0-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="421d0-114">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="421d0-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="421d0-115">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="421d0-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="421d0-116">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="421d0-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="421d0-117">Menedżer konfiguracji Azure dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="421d0-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="421d0-118">[Konto usługi Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="421d0-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="421d0-119">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="421d0-119">Add using directives</span></span>
<span data-ttu-id="421d0-120">Dodaj następujące hello `using` dyrektywy toohello początku hello `Program.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="421d0-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="421d0-121">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="421d0-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="421d0-122">Tworzenie klienta usługi kolejki hello</span><span class="sxs-lookup"><span data-stu-id="421d0-122">Create hello Queue service client</span></span>
<span data-ttu-id="421d0-123">Witaj **CloudQueueClient** klasa umożliwia możesz tooretrieve kolejek przechowywanych w magazynie kolejek.</span><span class="sxs-lookup"><span data-stu-id="421d0-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="421d0-124">Klient usługi jednokierunkowej toocreate hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="421d0-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="421d0-125">Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooQueue pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="421d0-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="421d0-126">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="421d0-126">Create a queue</span></span>
<span data-ttu-id="421d0-127">W tym przykładzie pokazano sposób toocreate kolejki, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="421d0-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="421d0-128">Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="421d0-128">Insert a message into a queue</span></span>
<span data-ttu-id="421d0-129">tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="421d0-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="421d0-130">Następnie wywołaj hello **AddMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="421d0-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="421d0-131">Klasę **CloudQueueMessage** można utworzyć przy użyciu ciągu (w formacie UTF-8) lub tablicy **bajtów**.</span><span class="sxs-lookup"><span data-stu-id="421d0-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="421d0-132">Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World":</span><span class="sxs-lookup"><span data-stu-id="421d0-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="421d0-133">Wglądu dalej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="421d0-133">Peek at hello next message</span></span>
<span data-ttu-id="421d0-134">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="421d0-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="421d0-135">Zmień hello zawartość komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="421d0-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="421d0-136">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="421d0-137">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji tooupdate stan hello zadania.</span><span class="sxs-lookup"><span data-stu-id="421d0-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="421d0-138">powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="421d0-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="421d0-139">Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="421d0-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="421d0-140">Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="421d0-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="421d0-141">Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="421d0-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="421d0-142">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="421d0-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="421d0-143">Kolejka do następnej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="421d0-143">De-queue hello next message</span></span>
<span data-ttu-id="421d0-144">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="421d0-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="421d0-145">Podczas wywoływania **GetMessage**, Pobierz hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="421d0-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="421d0-146">Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="421d0-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="421d0-147">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="421d0-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="421d0-148">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="421d0-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="421d0-149">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="421d0-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="421d0-150">Twój kod wywołuje **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="421d0-151">Używanie wzorca Async-Await z wspólnymi interfejsami API usługi Queue Storage</span><span class="sxs-lookup"><span data-stu-id="421d0-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="421d0-152">Ten przykład przedstawia, jak wzorca Async-Await hello toouse ze wspólnych interfejsów API magazynu kolejek.</span><span class="sxs-lookup"><span data-stu-id="421d0-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="421d0-153">przykład Witaj wywołuje hello asynchroniczną wersję każdej z hello podanej metody, wskazywany przez hello *Async* sufiks każdej metody.</span><span class="sxs-lookup"><span data-stu-id="421d0-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="421d0-154">W przypadku metody asynchronicznej hello async-await wzorzec zawiesi lokalne wykonanie do momentu ukończenia wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="421d0-155">Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="421d0-156">Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="421d0-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="421d0-157">Wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="421d0-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="421d0-158">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="421d0-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="421d0-159">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="421d0-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="421d0-160">Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="421d0-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="421d0-161">następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="421d0-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="421d0-162">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="421d0-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="421d0-163">Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="421d0-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="421d0-164">Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="421d0-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="421d0-165">Pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="421d0-165">Get hello queue length</span></span>
<span data-ttu-id="421d0-166">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="421d0-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="421d0-167">**FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="421d0-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="421d0-168">Witaj **ApproximateMessageCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="421d0-169">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="421d0-169">Delete a queue</span></span>
<span data-ttu-id="421d0-170">toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="421d0-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="421d0-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="421d0-171">Next steps</span></span>
<span data-ttu-id="421d0-172">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="421d0-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="421d0-173">Przejrzyj dokumentację referencyjną usługi kolejki hello szczegółowe informacje o dostępnych interfejsach API:</span><span class="sxs-lookup"><span data-stu-id="421d0-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="421d0-174">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="421d0-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="421d0-175">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="421d0-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="421d0-176">Dowiedz się, jak kod hello toosimplify pisania toowork z usługą Azure Storage za pomocą hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="421d0-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="421d0-177">Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="421d0-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="421d0-178">[Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore strukturę danych.</span><span class="sxs-lookup"><span data-stu-id="421d0-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="421d0-179">[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore danych bez struktury.</span><span class="sxs-lookup"><span data-stu-id="421d0-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="421d0-180">[Połącz tooSQL bazy danych przy użyciu programu .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relacyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="421d0-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
