---
title: "Rozpoczynanie pracy z magazynem kolejek i Visual Studio połączone usługi (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę przy użyciu magazynu kolejek Azure w projekcie platformy ASP.NET Core w programie Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="b7360-103">Rozpoczynanie pracy z magazynem kolejek i Visual Studio połączone usługi (platformy ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="b7360-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="b7360-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b7360-104">Overview</span></span>
<span data-ttu-id="b7360-105">W tym artykule opisano, jak rozpocząć pracę przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b7360-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="b7360-106">**Dodać usług połączonych** operacji instaluje odpowiednie pakiety NuGet dostęp do magazynu Azure do projektu i dodaje ten ciąg połączenia dla konta magazynu do plików konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="b7360-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="b7360-107">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które są dostępne z dowolnego miejsca na świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b7360-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="b7360-108">Pojedynczy komunikat z kolejki może być maksymalnie 64 kilobajty (KB), rozmiar, a kolejka może zawierać miliony komunikatów — maksymalnie całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b7360-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="b7360-109">Aby rozpocząć pracę, należy najpierw utworzyć kolejce platformy Azure na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="b7360-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="b7360-110">Poniżej opisano sposób tworzenia kolejki w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b7360-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="b7360-111">Możemy również opisano sposób wykonywania kolejki podstawowe operacje, takie jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="b7360-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="b7360-112">Przykłady są napisane w języku C\# kodu i używanie biblioteki klienta magazynu Azure dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="b7360-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="b7360-113">Aby uzyskać więcej informacji na temat platformy ASP.NET, zobacz [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="b7360-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="b7360-114">**Uwaga:** niektórych interfejsów API, które wykonywania wywołań do magazynu Azure w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="b7360-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="b7360-115">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b7360-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="b7360-116">Poniższy kod przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="b7360-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="b7360-117">Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji o programowo manipulowanie kolejek.</span><span class="sxs-lookup"><span data-stu-id="b7360-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="b7360-118">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b7360-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="b7360-119">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="b7360-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="b7360-120">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b7360-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="b7360-121">Uzyskiwanie dostępu do kolejek w kodzie</span><span class="sxs-lookup"><span data-stu-id="b7360-121">Access queues in code</span></span>
<span data-ttu-id="b7360-122">Aby uzyskać dostęp do kolejki w projektach platformy ASP.NET Core, musisz obejmują następujące elementy do dowolnego języka C# plik źródłowy, który uzyskuje dostęp do magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="b7360-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="b7360-123">Upewnij się, że deklaracje przestrzeni nazw w górnej części pliku C# Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="b7360-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="b7360-124">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="b7360-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7360-125">Użyj następującego kodu można pobrać parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="b7360-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="b7360-126">Pobierz **CloudQueueClient** obiektu odwołują się obiekty w koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="b7360-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="b7360-127">Pobierz **CloudQueue** obiekt do odwoływania się do określonej kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7360-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="b7360-128">**Uwaga:** korzystać ze wszystkich powyższych kodu przed kod w następujących przykładach.</span><span class="sxs-lookup"><span data-stu-id="b7360-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="b7360-129">Tworzenie kolejki w kodzie</span><span class="sxs-lookup"><span data-stu-id="b7360-129">Create a queue in code</span></span>
<span data-ttu-id="b7360-130">Aby utworzyć kolejkę Azure w kodzie, wystarczy dodać wywołanie **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="b7360-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="b7360-131">Dodaj komunikat do kolejki</span><span class="sxs-lookup"><span data-stu-id="b7360-131">Add a message to a queue</span></span>
<span data-ttu-id="b7360-132">Aby wstawić komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiekt, a następnie wywołaj **AddMessageAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="b7360-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="b7360-133">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="b7360-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="b7360-134">Oto przykład, która wstawia komunikat "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="b7360-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="b7360-135">Przeczytaj wiadomość w kolejce</span><span class="sxs-lookup"><span data-stu-id="b7360-135">Read a message in a queue</span></span>
<span data-ttu-id="b7360-136">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **PeekMessageAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="b7360-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="b7360-137">Przeczytaj i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="b7360-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="b7360-138">Można usunąć kodu (dequeue) wiadomość z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="b7360-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="b7360-139">Wywołanie **GetMessageAsync** do pobrania następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="b7360-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="b7360-140">Komunikat zwrócony z **GetMessageAsync** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7360-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="b7360-141">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="b7360-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="b7360-142">Aby zakończyć usuwanie komunikatu z kolejki, należy wywołać **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="b7360-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="b7360-143">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="b7360-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="b7360-144">Poniższy kod wywołania **DeleteMessageAsync** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="b7360-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="b7360-145">Wykorzystanie dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="b7360-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="b7360-146">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7360-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="b7360-147">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="b7360-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="b7360-148">Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="b7360-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="b7360-149">Poniższy przykład kodu wykorzystuje metodę **GetMessages**, aby pobrać 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="b7360-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="b7360-150">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="b7360-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="b7360-151">Ustawia również limitu czasu niewidoczności na 5 minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="b7360-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="b7360-152">Należy pamiętać, że 5 minut rozpocząć dla wszystkich wiadomości w tym samym czasie, więc po 5 minut przekazany po wywołaniu **GetMessages**, wszystkie komunikaty, które nie zostały usunięte stają się widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="b7360-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="b7360-153">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="b7360-153">Get the queue length</span></span>
<span data-ttu-id="b7360-154">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="b7360-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="b7360-155">**FetchAttributes** metody prosi usługę kolejki o pobranie atrybutów kolejki, w tym liczby komunikatów.</span><span class="sxs-lookup"><span data-stu-id="b7360-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="b7360-156">**ApproximateMethodCount** właściwość zwraca ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7360-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="b7360-157">Użyj wzorca Async-Await z kolejką wspólnych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="b7360-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="b7360-158">Ten przykład przedstawia sposób użycia wzorca Async-Await z kolejką wspólnych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="b7360-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="b7360-159">Przykład wywołuje wersji async każdego z danej metody.</span><span class="sxs-lookup"><span data-stu-id="b7360-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="b7360-160">Można to zaobserwować przez Async poprawkę po każdej metody.</span><span class="sxs-lookup"><span data-stu-id="b7360-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="b7360-161">Jeśli zostanie użyta metoda asynchroniczna, wzorzec Async-Await zawiesi lokalne wykonanie do czasu ukończenia wywołania.</span><span class="sxs-lookup"><span data-stu-id="b7360-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="b7360-162">Takie zachowanie umożliwia wykonywanie innych zadań, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji bieżącego wątku.</span><span class="sxs-lookup"><span data-stu-id="b7360-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="b7360-163">Aby uzyskać więcej informacji o wykorzystaniu wzorca Async-Await w programie .NET, zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="b7360-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="b7360-164">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="b7360-164">Delete a queue</span></span>
<span data-ttu-id="b7360-165">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj metodę **Delete** na obiekcie kolejki.</span><span class="sxs-lookup"><span data-stu-id="b7360-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="b7360-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7360-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

