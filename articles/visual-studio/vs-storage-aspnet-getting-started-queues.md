---
title: "Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę po nawiązaniu połączenia z kontem magazynu przy użyciu programu Visual Studio usług połączonych za pomocą magazynu kolejek Azure w projekcie platformy ASP.NET w programie Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="2e8bb-103">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="2e8bb-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2e8bb-104">Overview</span></span>

<span data-ttu-id="2e8bb-105">Azure queue storage umożliwia wysyłanie komunikatów między składnikami aplikacji chmury.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="2e8bb-106">W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="2e8bb-107">Usługa Queue Storage zapewnia asynchroniczne przesyłanie komunikatów na potrzeby komunikacji między składnikami aplikacji niezależnie od tego, czy działają w chmurze, na komputerze, serwerze lokalnym czy urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="2e8bb-108">Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="2e8bb-109">Ten samouczek pokazuje, jak napisać kod ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="2e8bb-110">Te scenariusze obejmują typowych zadań, takich jak tworzenie kolejki systemu Azure i dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="2e8bb-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2e8bb-111">Prerequisites</span></span>

* [<span data-ttu-id="2e8bb-112">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e8bb-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="2e8bb-113">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2e8bb-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="2e8bb-114">Tworzenie kontrolera MVC</span><span class="sxs-lookup"><span data-stu-id="2e8bb-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="2e8bb-115">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i z menu kontekstowego wybierz **kontrolera -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Dodawanie kontrolera do aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="2e8bb-117">Na **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="2e8bb-119">Na **Dodaj kontroler** okna dialogowego, nazwy kontrolera *QueuesController*i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Nazwa kontrolera MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="2e8bb-121">Dodaj następujące *przy użyciu* dyrektywy `QueuesController.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="2e8bb-122">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-122">Create a queue</span></span>

<span data-ttu-id="2e8bb-123">Poniższe kroki pokazano, jak utworzyć kolejkę:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-124">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-125">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="2e8bb-126">Dodaj metodę o nazwie **CreateQueue** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="2e8bb-127">W ramach **CreateQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-128">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="2e8bb-129">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="2e8bb-130">Pobierz **CloudQueue** obiekt, który reprezentuje odwołanie do nazwy wymaganej kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="2e8bb-131">**CloudQueueClient.GetQueueReference** — metoda nie powoduje żądanie magazynu kolejek.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="2e8bb-132">Czy kolejka istnieje, zwracany jest odwołanie.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-133">Wywołanie **CloudQueue.CreateIfNotExists** metody, aby utworzyć kolejkę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="2e8bb-134">**CloudQueue.CreateIfNotExists** metoda zwraca **true** Jeśli kolejka nie istnieje i został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="2e8bb-135">W przeciwnym razie **false** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="2e8bb-136">Aktualizacja **obiekt ViewBag** o nazwie kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="2e8bb-137">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-138">Na **Dodaj widok** okna dialogowego, wprowadź **CreateQueue** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-139">Otwórz `CreateQueue.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="2e8bb-140">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-141">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-142">Uruchom aplikację i wybierz **Utwórz kolejkę** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Tworzenie kolejki](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="2e8bb-144">Jak wspomniano wcześniej, **CloudQueue.CreateIfNotExists** metoda zwraca **true** tylko gdy kolejka nie istnieje i zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="2e8bb-145">W związku z tym po uruchomieniu aplikacji, gdy kolejka istnieje, metoda zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="2e8bb-146">Aby uruchomić aplikację wiele razy, musisz usunąć kolejkę przed ponownym uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="2e8bb-147">Usuwanie kolejki może odbywać się za pośrednictwem **CloudQueue.Delete** metody.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="2e8bb-148">Możesz także usunąć przy użyciu kolejki [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="2e8bb-149">Dodaj komunikat do kolejki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-149">Add a message to a queue</span></span>

<span data-ttu-id="2e8bb-150">Po wprowadzeniu [utworzenie kolejki](#create-a-queue), można dodawać komunikaty do tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="2e8bb-151">Ta sekcja przeprowadzi Cię przez procedurę dodawania wiadomości do kolejki *kolejki testowej*.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-152">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-153">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2e8bb-154">Dodaj metodę o nazwie **AddMessage** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2e8bb-155">W ramach **AddMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-156">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2e8bb-157">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2e8bb-158">Pobierz **CloudQueueContainer** obiekt, który reprezentuje odwołanie do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-159">Utwórz **CloudQueueMessage** obiekt reprezentujący wiadomości, które chcesz dodać do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="2e8bb-160">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="2e8bb-161">Wywołanie **CloudQueue.AddMessage** metody w celu dodania messaged do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="2e8bb-162">Utwórz i ustaw kilku **obiekt ViewBag** właściwości do wyświetlenia w widoku.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="2e8bb-163">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-164">Na **Dodaj widok** okna dialogowego, wprowadź **AddMessage** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-165">Otwórz `AddMessage.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="2e8bb-166">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-167">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-168">Uruchom aplikację i wybierz **komunikat Dodaj** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Dodaj komunikat](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="2e8bb-170">Dwie sekcje - [Przeczytaj wiadomość z kolejki bez jego usuwania](#read-a-message-from-a-queue-without-removing-it) i [odczytu i usuwania komunikatu z kolejki](#read-and-remove-a-message-from-a-queue) -zilustrować odczytywać wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="2e8bb-171">Przeczytaj wiadomość z kolejki bez jego usuwania</span><span class="sxs-lookup"><span data-stu-id="2e8bb-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="2e8bb-172">W tej sekcji przedstawiono sposób wglądu do wiadomości w kolejce (do odczytu do pierwszej wiadomości bez jego usuwania).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-173">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-174">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2e8bb-175">Dodaj metodę o nazwie **PeekMessage** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2e8bb-176">W ramach **PeekMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-177">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2e8bb-178">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2e8bb-179">Pobierz **CloudQueueContainer** obiekt, który reprezentuje odwołanie do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-180">Wywołanie **CloudQueue.PeekMessage** metody do odczytu do pierwszej wiadomości w kolejce bez usuwania go z kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="2e8bb-181">Aktualizacja **obiekt ViewBag** z dwóch wartości: Nazwa kolejki i komunikat, który został odczytany.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="2e8bb-182">**CloudQueueMessage** obiekt udostępnia dwie właściwości pobierania wartości obiektu: **CloudQueueMessage.AsBytes** i **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="2e8bb-183">**AsString** (używane w tym przykładzie) zwraca ciąg znaków, podczas gdy **AsBytes** zwraca tablicę bajtów.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="2e8bb-184">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-185">Na **Dodaj widok** okna dialogowego, wprowadź **PeekMessage** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-186">Otwórz `PeekMessage.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="2e8bb-187">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-188">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-189">Uruchom aplikację i wybierz **komunikat Peek** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Wgląd do wiadomości](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="2e8bb-191">Przeczytaj i usunąć wiadomości z kolejki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="2e8bb-192">W tej sekcji możesz dowiedzieć się, jak na odczytywanie i usuwanie wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-193">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-194">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2e8bb-195">Dodaj metodę o nazwie **przeczytanyWiadomość** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2e8bb-196">W ramach **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-197">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2e8bb-198">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2e8bb-199">Pobierz **CloudQueueContainer** obiekt, który reprezentuje odwołanie do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-200">Wywołanie **CloudQueue.GetMessage** metody do odczytu do pierwszej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="2e8bb-201">**CloudQueue.GetMessage** — metoda sprawia, że komunikat niewidoczne dla 30 sekund (domyślnie) do innego kodu odczytującego komunikaty, aby żadnego innego kodu można zmodyfikować lub usunąć komunikat podczas z jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="2e8bb-202">Aby zmienić czas wiadomość jest niewidoczny, zmodyfikuj **visibilityTimeout** parametr przekazywany do **CloudQueue.GetMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="2e8bb-203">Wywołanie **CloudQueueMessage.Delete** metodę, aby usunąć wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="2e8bb-204">Aktualizacja **obiekt ViewBag** z komunikatu usunięte i nazwy kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="2e8bb-205">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-206">Na **Dodaj widok** okna dialogowego, wprowadź **przeczytanyWiadomość** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-207">Otwórz `ReadMessage.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="2e8bb-208">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-209">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-210">Uruchom aplikację i wybierz **komunikat odczytu/usuwania** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Komunikat do odczytu i usuwania](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="2e8bb-212">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-212">Get the queue length</span></span>

<span data-ttu-id="2e8bb-213">W tej sekcji przedstawiono sposób pobrać długości kolejki (liczba komunikatów).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-214">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-215">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2e8bb-216">Dodaj metodę o nazwie **GetQueueLength** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2e8bb-217">W ramach **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-218">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2e8bb-219">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2e8bb-220">Pobierz **CloudQueueContainer** obiekt, który reprezentuje odwołanie do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-221">Wywołanie **CloudQueue.FetchAttributes** metody można pobrać atrybutów kolejki (w tym jej długość).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="2e8bb-222">Dostęp **CloudQueue.ApproximateMessageCount** właściwości do pobrania długość kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="2e8bb-223">Aktualizacja **obiekt ViewBag** o nazwie kolejka, a jego długość.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="2e8bb-224">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-225">Na **Dodaj widok** okna dialogowego, wprowadź **GetQueueLength** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-226">Otwórz `GetQueueLengthMessage.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="2e8bb-227">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-228">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-229">Uruchom aplikację i wybierz **pobieranie długości kolejki** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Pobieranie długości kolejki](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="2e8bb-231">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-231">Delete a queue</span></span>
<span data-ttu-id="2e8bb-232">W tej części przedstawiono sposób usunąć kolejkę.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2e8bb-233">W tej sekcji założono zostały wykonane kroki [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2e8bb-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2e8bb-234">Otwórz plik `QueuesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2e8bb-235">Dodaj metodę o nazwie **DeleteQueue** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2e8bb-236">W ramach **DeleteQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2e8bb-237">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2e8bb-238">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2e8bb-239">Pobierz **CloudQueueContainer** obiekt, który reprezentuje odwołanie do kolejki.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2e8bb-240">Wywołanie **CloudQueue.Delete** metodę, aby usunąć kolejkę reprezentowany przez **CloudQueue** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="2e8bb-241">Aktualizacja **obiekt ViewBag** o nazwie kolejka, a jego długość.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="2e8bb-242">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2e8bb-243">Na **Dodaj widok** okna dialogowego, wprowadź **DeleteQueue** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="2e8bb-244">Otwórz `DeleteQueue.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="2e8bb-245">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2e8bb-246">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="2e8bb-247">Uruchom aplikację i wybierz **pobieranie długości kolejki** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="2e8bb-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Usuwanie kolejki](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="2e8bb-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e8bb-249">Next steps</span></span>
<span data-ttu-id="2e8bb-250">Wyświetl więcej poradników dotyczących funkcji, aby dowiedzieć się więcej o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8bb-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="2e8bb-251">Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="2e8bb-252">Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2e8bb-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
