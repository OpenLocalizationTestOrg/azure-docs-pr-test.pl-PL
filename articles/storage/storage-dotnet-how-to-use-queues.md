---
title: "Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu programu .NET | Microsoft Docs"
description: "Usługa Azure Queues zapewnia niezawodne, asynchroniczne przesyłanie komunikatów między składnikami aplikacji. Przesyłanie komunikatów za pomocą chmury umożliwia składnikom aplikacji niezależne skalowanie."
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
ms.openlocfilehash: 7f88aa9c50e669d1be7248346c7b1176bce61249
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="1ada0-104">Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1ada0-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="1ada0-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1ada0-105">Overview</span></span>
<span data-ttu-id="1ada0-106">Usługa Azure Queue Storage umożliwia przesyłanie komunikatów za pomocą chmury między składnikami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ada0-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="1ada0-107">W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="1ada0-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="1ada0-108">Usługa Queue Storage zapewnia asynchroniczne przesyłanie komunikatów na potrzeby komunikacji między składnikami aplikacji niezależnie od tego, czy działają w chmurze, na komputerze, serwerze lokalnym czy urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="1ada0-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="1ada0-109">Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1ada0-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="1ada0-110">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="1ada0-110">About this tutorial</span></span>
<span data-ttu-id="1ada0-111">W tym samouczku pokazano, jak napisać kod .NET dla niektórych typowych scenariuszy przy użyciu usługi Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="1ada0-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="1ada0-112">Omówione scenariusze obejmują tworzenie i usuwanie kolejek oraz dodawanie, odczytywanie i usuwanie komunikatów kolejek.</span><span class="sxs-lookup"><span data-stu-id="1ada0-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="1ada0-113">**Szacowany czas trwania:** 45 minut</span><span class="sxs-lookup"><span data-stu-id="1ada0-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="1ada0-114">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="1ada0-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="1ada0-115">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ada0-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="1ada0-116">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="1ada0-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="1ada0-117">Menedżer konfiguracji Azure dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="1ada0-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="1ada0-118">[Konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="1ada0-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="1ada0-119">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="1ada0-119">Add using directives</span></span>
<span data-ttu-id="1ada0-120">Dodaj następujące dyrektywy `using` na początku pliku `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="1ada0-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="1ada0-121">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="1ada0-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="1ada0-122">Tworzenie klienta usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-122">Create the Queue service client</span></span>
<span data-ttu-id="1ada0-123">Klasa **CloudQueueClient** umożliwia pobieranie kolejek przechowywanych w usłudze Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="1ada0-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="1ada0-124">Oto jeden ze sposobów tworzenia klienta usługi:</span><span class="sxs-lookup"><span data-stu-id="1ada0-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="1ada0-125">Teraz możesz przystąpić do pisania kodu, który będzie odczytywać dane z usługi Queue Storage i zapisywać je w nim.</span><span class="sxs-lookup"><span data-stu-id="1ada0-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="1ada0-126">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-126">Create a queue</span></span>
<span data-ttu-id="1ada0-127">W tym przykładzie pokazano, jak utworzyć kolejkę, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="1ada0-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="1ada0-128">Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-128">Insert a message into a queue</span></span>
<span data-ttu-id="1ada0-129">Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nową klasę **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="1ada0-130">Następnie wywołaj metodę **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="1ada0-131">Klasę **CloudQueueMessage** można utworzyć przy użyciu ciągu (w formacie UTF-8) lub tablicy **bajtów**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="1ada0-132">Oto kod, który tworzy kolejkę (jeśli kolejka nie istnieje) i wstawia komunikat „Hello, World”:</span><span class="sxs-lookup"><span data-stu-id="1ada0-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="1ada0-133">Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="1ada0-133">Peek at the next message</span></span>
<span data-ttu-id="1ada0-134">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując metodę **PeekMessage**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="1ada0-135">Zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="1ada0-135">Change the contents of a queued message</span></span>
<span data-ttu-id="1ada0-136">Możesz zmienić zawartość komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1ada0-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="1ada0-137">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania.</span><span class="sxs-lookup"><span data-stu-id="1ada0-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="1ada0-138">Poniższy kod aktualizuje komunikat kolejki o nową zawartość i ustawia rozszerzenie limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="1ada0-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="1ada0-139">Operacja ta zapisuje stan pracy powiązanej z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad komunikatem.</span><span class="sxs-lookup"><span data-stu-id="1ada0-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="1ada0-140">Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ada0-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="1ada0-141">Zazwyczaj stosuje się również liczbę ponownych prób. Jeśli komunikat zostanie ponowiony więcej niż *n* razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="1ada0-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="1ada0-142">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="1ada0-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="1ada0-143">Usunięcie następnego komunikatu z kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-143">De-queue the next message</span></span>
<span data-ttu-id="1ada0-144">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="1ada0-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="1ada0-145">Jeśli wywołasz funkcję **GetMessage**, uzyskasz następny komunikat w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1ada0-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="1ada0-146">Komunikat zwrócony z funkcji **GetMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="1ada0-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="1ada0-147">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="1ada0-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="1ada0-148">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać funkcję **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="1ada0-149">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="1ada0-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="1ada0-150">Twój kod wywołuje funkcję **DeleteMessage** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1ada0-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="1ada0-151">Używanie wzorca Async-Await z wspólnymi interfejsami API usługi Queue Storage</span><span class="sxs-lookup"><span data-stu-id="1ada0-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="1ada0-152">Ten przykład przedstawia sposób użycia wzorca Async-Await z wykorzystaniem wspólnych interfejsów API usługi Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="1ada0-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="1ada0-153">Przykład wywołuje asynchroniczną wersję każdej z danych metod, co jest wskazane przez sufiks *Async* każdej metody.</span><span class="sxs-lookup"><span data-stu-id="1ada0-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="1ada0-154">Jeśli zostanie użyta metoda asynchroniczna, wzorzec Async-Await zawiesi lokalne wykonanie do momentu ukończenia wywołania.</span><span class="sxs-lookup"><span data-stu-id="1ada0-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="1ada0-155">Takie zachowanie umożliwia wykonywanie innych zadań przez bieżący wątek, co pomaga unikać wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ada0-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="1ada0-156">Aby uzyskać szczegółowe informacje o wykorzystaniu wzorca Async-Await w programie .NET, zobacz [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx) (Async i Await [C# i Visual Basic]).</span><span class="sxs-lookup"><span data-stu-id="1ada0-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="1ada0-157">Wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="1ada0-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="1ada0-158">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="1ada0-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="1ada0-159">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="1ada0-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="1ada0-160">Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1ada0-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="1ada0-161">Poniższy przykład kodu wykorzystuje metodę **GetMessages**, aby pobrać 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="1ada0-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="1ada0-162">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="1ada0-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="1ada0-163">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1ada0-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="1ada0-164">Należy zauważyć, że okres 5 minut rozpoczyna się dla wszystkich komunikatów w tym samym czasie, więc po upływie 5 minut od wywołania metody **GetMessages** wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="1ada0-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="1ada0-165">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-165">Get the queue length</span></span>
<span data-ttu-id="1ada0-166">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1ada0-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="1ada0-167">Metoda **FetchAttributes** prosi usługę kolejki o pobranie atrybutów kolejki, w tym liczby komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1ada0-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="1ada0-168">Właściwość **ApproximateMessageCount** zwraca ostatnią wartość pobraną przez metodę **FetchAttributes** bez wywoływania usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="1ada0-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="1ada0-169">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="1ada0-169">Delete a queue</span></span>
<span data-ttu-id="1ada0-170">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj metodę **Delete** na obiekcie kolejki.</span><span class="sxs-lookup"><span data-stu-id="1ada0-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="1ada0-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ada0-171">Next steps</span></span>
<span data-ttu-id="1ada0-172">Teraz, kiedy znasz już podstawy usługi Queue Storage, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="1ada0-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="1ada0-173">Przejrzyj dokumentację referencyjną usługi kolejki, aby uzyskać szczegółowe informacje o dostępnych interfejsach API:</span><span class="sxs-lookup"><span data-stu-id="1ada0-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="1ada0-174">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="1ada0-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="1ada0-175">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="1ada0-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="1ada0-176">Dowiedz się, jak uprościć zapisywany kod, aby pracować z usługą Azure Storage za pomocą zestawu [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1ada0-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="1ada0-177">Wyświetl więcej poradników dotyczących funkcji, aby dowiedzieć się więcej o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1ada0-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="1ada0-178">Zapoznaj się z tematem [Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md), aby przechowywać dane strukturalne.</span><span class="sxs-lookup"><span data-stu-id="1ada0-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="1ada0-179">Zapoznaj się z tematem [Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md), aby przechowywać dane bez struktury.</span><span class="sxs-lookup"><span data-stu-id="1ada0-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="1ada0-180">[Połącz się z usługą SQL Database przy użyciu platformy .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md), aby zapisać dane relacyjne.</span><span class="sxs-lookup"><span data-stu-id="1ada0-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
