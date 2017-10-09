---
title: "aaaGet pracy z magazynem kolejek i Visual Studio podłączonych usług (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak tooget pracy z magazynem kolejek Azure w projektu usługi w chmurze w programie Visual Studio, po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="15b61-103">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="15b61-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="15b61-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="15b61-104">Overview</span></span>
<span data-ttu-id="15b61-105">W tym artykule opisano sposób uruchamiania przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie usługi w chmurze przy użyciu programu Visual Studio hello tooget **dodać usług połączonych** okna dialogowego .</span><span class="sxs-lookup"><span data-stu-id="15b61-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="15b61-106">Poniżej opisano sposób toocreate kolejki w kodzie.</span><span class="sxs-lookup"><span data-stu-id="15b61-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="15b61-107">Również pokażemy ci jak tooperform basic kolejki operacji, takich jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="15b61-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="15b61-108">Przykłady Hello są zapisywane w kodzie C# i używają hello [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="15b61-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="15b61-109">Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="15b61-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="15b61-110">Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji na temat manipulowanie kolejek w kodzie.</span><span class="sxs-lookup"><span data-stu-id="15b61-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="15b61-111">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="15b61-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="15b61-112">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="15b61-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="15b61-113">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="15b61-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="15b61-114">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="15b61-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="15b61-115">Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="15b61-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="15b61-116">Uzyskiwanie dostępu do kolejek w kodzie</span><span class="sxs-lookup"><span data-stu-id="15b61-116">Access queues in code</span></span>
<span data-ttu-id="15b61-117">kolejki tooaccess w projektach Visual Studio Cloud Services, potrzebne tooinclude hello następujące elementy plik źródłowy tooany C#, który dostęp do magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="15b61-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="15b61-118">Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="15b61-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="15b61-119">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="15b61-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="15b61-120">Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="15b61-121">Pobierz **CloudQueueClient** obiekt tooreference hello kolejki obiektów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="15b61-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="15b61-122">Pobierz **CloudQueue** obiekt tooreference określonej kolejki.</span><span class="sxs-lookup"><span data-stu-id="15b61-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="15b61-123">**Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="15b61-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="15b61-124">Tworzenie kolejki w kodzie</span><span class="sxs-lookup"><span data-stu-id="15b61-124">Create a queue in code</span></span>
<span data-ttu-id="15b61-125">kolejki hello toocreate w kodzie, wystarczy dodać wywołanie za**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="15b61-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="15b61-126">Dodaj tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="15b61-126">Add a message tooa queue</span></span>
<span data-ttu-id="15b61-127">tooinsert komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiektu, a następnie wywołania hello **AddMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="15b61-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="15b61-128">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="15b61-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="15b61-129">Oto przykład, która wstawia wiadomości powitania "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="15b61-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="15b61-130">Przeczytaj wiadomość w kolejce</span><span class="sxs-lookup"><span data-stu-id="15b61-130">Read a message in a queue</span></span>
<span data-ttu-id="15b61-131">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="15b61-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="15b61-132">Przeczytaj i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="15b61-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="15b61-133">Można usunąć kodu (cofnąć kolejka) wiadomości z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="15b61-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="15b61-134">Wywołanie **GetMessage** tooget hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="15b61-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="15b61-135">Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="15b61-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="15b61-136">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="15b61-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="15b61-137">toofinish usuwanie wiadomości powitania z kolejki hello, wywołanie **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="15b61-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="15b61-138">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="15b61-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="15b61-139">Witaj poniższy kod wywołania **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="15b61-140">Użyj dodatkowych opcji tooprocess i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="15b61-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="15b61-141">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="15b61-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="15b61-142">Możesz uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="15b61-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="15b61-143">Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="15b61-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="15b61-144">następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="15b61-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="15b61-145">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="15b61-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="15b61-146">Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="15b61-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="15b61-147">Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="15b61-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="15b61-148">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="15b61-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="15b61-149">Pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="15b61-149">Get hello queue length</span></span>
<span data-ttu-id="15b61-150">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="15b61-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="15b61-151">**FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="15b61-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="15b61-152">Witaj **ApproximateMethodCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="15b61-153">Witaj wzorca Async-Await za pomocą wspólnych interfejsów API kolejki usługi Azure</span><span class="sxs-lookup"><span data-stu-id="15b61-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="15b61-154">Ten przykład przedstawia, jak wzorca Async-Await hello toouse ze wspólnych interfejsów API kolejki usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="15b61-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="15b61-155">przykład Hello wywołuje hello asynchronicznych wersji każdego hello podanej metody, można to zaobserwować przez hello **Async** poprawka po każdej metody.</span><span class="sxs-lookup"><span data-stu-id="15b61-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="15b61-156">Gdy metody asynchronicznej jest używane hello async-await wzorzec zawiesi lokalne wykonanie do momentu ukończenia wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="15b61-157">Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="15b61-158">Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="15b61-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="15b61-159">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="15b61-159">Delete a queue</span></span>
<span data-ttu-id="15b61-160">toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej, wywołanie hello **usunąć** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="15b61-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="15b61-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15b61-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

