---
title: "aaaGet pracy z magazynem kolejek i Visual Studio podłączonych usług (platformy ASP.NET Core) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu kolejek Azure w projekcie platformy ASP.NET Core w programie Visual Studio"
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
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="79045-103">Rozpoczynanie pracy z magazynem kolejek i Visual Studio połączone usługi (platformy ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="79045-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="79045-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="79045-104">Overview</span></span>
<span data-ttu-id="79045-105">W tym artykule opisano sposób uruchamiania przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio hello tooget **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79045-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="79045-106">Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="79045-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="79045-107">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="79045-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="79045-108">Pojedynczy komunikat z kolejki można się too64 kilobajtów (KB), rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="79045-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="79045-109">tooget uruchomiona, należy najpierw toocreate kolejce platformy Azure na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="79045-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="79045-110">Poniżej opisano sposób toocreate kolejki w kodzie.</span><span class="sxs-lookup"><span data-stu-id="79045-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="79045-111">Również pokażemy ci jak tooperform basic kolejki operacji, takich jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="79045-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="79045-112">Przykłady Hello są napisane w języku C\# kodu i użyć hello biblioteki klienta magazynu Azure dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="79045-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="79045-113">Aby uzyskać więcej informacji na temat platformy ASP.NET, zobacz [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="79045-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="79045-114">**Uwaga:** niektóre hello interfejsów API, które wykonywania wywołań tooAzure magazynu w ASP.NET Core są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="79045-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="79045-115">Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="79045-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="79045-116">Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="79045-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="79045-117">Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji o programowo manipulowanie kolejek.</span><span class="sxs-lookup"><span data-stu-id="79045-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="79045-118">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79045-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="79045-119">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="79045-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="79045-120">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="79045-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="79045-121">Uzyskiwanie dostępu do kolejek w kodzie</span><span class="sxs-lookup"><span data-stu-id="79045-121">Access queues in code</span></span>
<span data-ttu-id="79045-122">kolejki tooaccess w projektach platformy ASP.NET Core, należy tooinclude hello następujących elementów pliku źródłowego tooany C#, który uzyskuje dostęp do magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="79045-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="79045-123">Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="79045-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="79045-124">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="79045-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="79045-125">Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="79045-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="79045-126">Pobierz **CloudQueueClient** obiekt tooreference hello kolejki obiektów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="79045-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="79045-127">Pobierz **CloudQueue** obiekt tooreference określonej kolejki.</span><span class="sxs-lookup"><span data-stu-id="79045-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="79045-128">**Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="79045-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="79045-129">Tworzenie kolejki w kodzie</span><span class="sxs-lookup"><span data-stu-id="79045-129">Create a queue in code</span></span>
<span data-ttu-id="79045-130">toocreate hello kolejki systemu Azure w kodzie, wystarczy dodać wywołanie za**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="79045-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="79045-131">Dodaj tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="79045-131">Add a message tooa queue</span></span>
<span data-ttu-id="79045-132">tooinsert komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiektu, a następnie wywołania hello **AddMessageAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="79045-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="79045-133">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="79045-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="79045-134">Oto przykład, która wstawia wiadomości powitania "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="79045-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="79045-135">Przeczytaj wiadomość w kolejce</span><span class="sxs-lookup"><span data-stu-id="79045-135">Read a message in a queue</span></span>
<span data-ttu-id="79045-136">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessageAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="79045-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="79045-137">Przeczytaj i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="79045-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="79045-138">Można usunąć kodu (dequeue) wiadomość z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="79045-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="79045-139">Wywołanie **GetMessageAsync** tooget hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="79045-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="79045-140">Komunikat zwrócony z **GetMessageAsync** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="79045-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="79045-141">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="79045-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="79045-142">toofinish usuwanie wiadomości powitania z kolejki hello, wywołanie **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="79045-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="79045-143">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="79045-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="79045-144">Witaj poniższy kod wywołania **DeleteMessageAsync** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="79045-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="79045-145">Wykorzystanie dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="79045-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="79045-146">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="79045-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="79045-147">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="79045-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="79045-148">Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="79045-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="79045-149">następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="79045-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="79045-150">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="79045-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="79045-151">Ustawia również minut too5 limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="79045-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="79045-152">Należy pamiętać, że hello start 5 minut dla wszystkich komunikatów na powitania sam czasu, dlatego po 5 minut po wywołaniu hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte stają się widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="79045-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="79045-153">Pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="79045-153">Get hello queue length</span></span>
<span data-ttu-id="79045-154">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="79045-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="79045-155">**FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="79045-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="79045-156">Witaj **ApproximateMethodCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="79045-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="79045-157">Użyj wzorca Async-Await hello z kolejką wspólnych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="79045-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="79045-158">Ten przykład przedstawia, jak toouse hello wzorca Async-Await z kolejką wspólnych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="79045-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="79045-159">Hello próbki wywołania hello async wersja każdego hello podanej metody.</span><span class="sxs-lookup"><span data-stu-id="79045-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="79045-160">Można to zaobserwować przez poprawka hello asynchronicznych po każdej metody.</span><span class="sxs-lookup"><span data-stu-id="79045-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="79045-161">W przypadku metody asynchronicznej hello wzorca Async-Await zawiesi lokalne wykonanie do czasu ukończenia wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="79045-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="79045-162">Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="79045-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="79045-163">Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET, zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="79045-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="79045-164">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="79045-164">Delete a queue</span></span>
<span data-ttu-id="79045-165">toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="79045-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="79045-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79045-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

