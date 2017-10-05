---
title: "Rozpoczynanie pracy z magazynem kolejek i Visual Studio połączone usługi (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę przy użyciu magazynu kolejek Azure w projektu usługi w chmurze w programie Visual Studio po połączeniu z kontem magazynu za pomocą programu Visual Studio połączone usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: d0e6e3eab312f169b1d05ba16e2e293e103df1ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="22bd7-103">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (usług w chmurze projekty)</span><span class="sxs-lookup"><span data-stu-id="22bd7-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="22bd7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="22bd7-104">Overview</span></span>
<span data-ttu-id="22bd7-105">W tym artykule opisano, jak rozpocząć pracę przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie usługi w chmurze przy użyciu programu Visual Studio **dodać usług połączonych** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="22bd7-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="22bd7-106">Poniżej opisano sposób tworzenia kolejki w kodzie.</span><span class="sxs-lookup"><span data-stu-id="22bd7-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="22bd7-107">Możemy również opisano sposób wykonywania kolejki podstawowe operacje, takie jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="22bd7-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="22bd7-108">Przykłady są napisane w kodzie języka C# i użyj [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="22bd7-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="22bd7-109">**Dodać usług połączonych** operacji instaluje odpowiednie pakiety NuGet dostęp do magazynu Azure do projektu i dodaje ten ciąg połączenia dla konta magazynu do plików konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="22bd7-110">Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji na temat manipulowanie kolejek w kodzie.</span><span class="sxs-lookup"><span data-stu-id="22bd7-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="22bd7-111">Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22bd7-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="22bd7-112">Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="22bd7-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="22bd7-113">Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="22bd7-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="22bd7-114">Azure Queue Storage to usługa do przechowywania dużej liczby komunikatów, do której można uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="22bd7-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="22bd7-115">Pojedynczy komunikat z kolejki nie może przekraczać 64 KB, a kolejka może zawierać miliony komunikatów — maksymalnie liczbę nieprzekraczającą całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="22bd7-116">Uzyskiwanie dostępu do kolejek w kodzie</span><span class="sxs-lookup"><span data-stu-id="22bd7-116">Access queues in code</span></span>
<span data-ttu-id="22bd7-117">Aby uzyskać dostęp do kolejki w projektach Visual Studio Cloud Services, musisz obejmują następujące elementy do dowolnego pliku źródłowego C#, które uzyskują dostęp do magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="22bd7-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="22bd7-118">Upewnij się, że deklaracje przestrzeni nazw w górnej części pliku C# Uwzględnij je **przy użyciu** instrukcje.</span><span class="sxs-lookup"><span data-stu-id="22bd7-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="22bd7-119">Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="22bd7-120">Użyj następującego kodu można pobrać parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="22bd7-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="22bd7-121">Pobierz **CloudQueueClient** obiektu odwołują się obiekty w koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="22bd7-122">Pobierz **CloudQueue** obiekt do odwoływania się do określonej kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="22bd7-123">**Uwaga:** korzystać ze wszystkich powyższych kodu przed kod w następujących przykładach.</span><span class="sxs-lookup"><span data-stu-id="22bd7-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="22bd7-124">Tworzenie kolejki w kodzie</span><span class="sxs-lookup"><span data-stu-id="22bd7-124">Create a queue in code</span></span>
<span data-ttu-id="22bd7-125">Aby utworzyć kolejkę w kodzie, wystarczy dodać wywołanie **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="22bd7-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="22bd7-126">Dodaj komunikat do kolejki</span><span class="sxs-lookup"><span data-stu-id="22bd7-126">Add a message to a queue</span></span>
<span data-ttu-id="22bd7-127">Aby wstawić komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiekt, a następnie wywołaj **AddMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="22bd7-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="22bd7-128">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="22bd7-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="22bd7-129">Oto przykład, która wstawia komunikat "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="22bd7-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="22bd7-130">Przeczytaj wiadomość w kolejce</span><span class="sxs-lookup"><span data-stu-id="22bd7-130">Read a message in a queue</span></span>
<span data-ttu-id="22bd7-131">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując metodę **PeekMessage**.</span><span class="sxs-lookup"><span data-stu-id="22bd7-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="22bd7-132">Przeczytaj i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="22bd7-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="22bd7-133">Można usunąć kodu (cofnąć kolejka) wiadomości z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="22bd7-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="22bd7-134">Wywołanie **GetMessage** do pobrania następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="22bd7-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="22bd7-135">Komunikat zwrócony z funkcji **GetMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="22bd7-136">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="22bd7-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="22bd7-137">Aby zakończyć usuwanie komunikatu z kolejki, należy wywołać **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="22bd7-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="22bd7-138">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="22bd7-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="22bd7-139">Poniższy kod wywołania **DeleteMessage** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="22bd7-140">Użyj dodatkowych opcji do przetwarzania i usuwanie wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="22bd7-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="22bd7-141">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="22bd7-142">Możesz uzyskać partii wiadomości (do 32).</span><span class="sxs-lookup"><span data-stu-id="22bd7-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="22bd7-143">Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie bardziej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="22bd7-144">Poniższy przykład kodu wykorzystuje metodę **GetMessages**, aby pobrać 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="22bd7-145">Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**.</span><span class="sxs-lookup"><span data-stu-id="22bd7-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="22bd7-146">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="22bd7-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="22bd7-147">Należy zauważyć, że okres 5 minut rozpoczyna się dla wszystkich komunikatów w tym samym czasie, więc po upływie 5 minut od wywołania metody **GetMessages** wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="22bd7-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="22bd7-148">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="22bd7-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="22bd7-149">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="22bd7-149">Get the queue length</span></span>
<span data-ttu-id="22bd7-150">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="22bd7-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="22bd7-151">Metoda **FetchAttributes** prosi usługę kolejki o pobranie atrybutów kolejki, w tym liczby komunikatów.</span><span class="sxs-lookup"><span data-stu-id="22bd7-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="22bd7-152">**ApproximateMethodCount** właściwość zwraca ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="22bd7-153">Użyj wzorca Async-Await z wspólnych interfejsów API kolejki usługi Azure</span><span class="sxs-lookup"><span data-stu-id="22bd7-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="22bd7-154">Ten przykład przedstawia sposób użycia wzorca Async-Await z wspólnych interfejsów API usługi Azure kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="22bd7-155">Przykład wywołuje wersji async każdego z danych metod, można to zaobserwować przez **Async** poprawka po każdej metody.</span><span class="sxs-lookup"><span data-stu-id="22bd7-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="22bd7-156">Gdy jest używana metoda asynchroniczna async-await wzorzec zawiesi lokalne wykonanie do momentu ukończenia wywołania.</span><span class="sxs-lookup"><span data-stu-id="22bd7-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="22bd7-157">Takie zachowanie umożliwia wykonywanie innych zadań, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji bieżącego wątku.</span><span class="sxs-lookup"><span data-stu-id="22bd7-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="22bd7-158">Aby uzyskać szczegółowe informacje o wykorzystaniu wzorca Async-Await w programie .NET, zobacz [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx) (Async i Await [C# i Visual Basic]).</span><span class="sxs-lookup"><span data-stu-id="22bd7-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="22bd7-159">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="22bd7-159">Delete a queue</span></span>
<span data-ttu-id="22bd7-160">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj metodę **Delete** na obiekcie kolejki.</span><span class="sxs-lookup"><span data-stu-id="22bd7-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="22bd7-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22bd7-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

