---
title: "aaaGet pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu kolejek Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu tooa konto magazynu przy użyciu programu Visual Studio usługami"
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
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="abc83-103">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="abc83-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="abc83-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="abc83-104">Overview</span></span>

<span data-ttu-id="abc83-105">Azure queue storage umożliwia wysyłanie komunikatów między składnikami aplikacji chmury.</span><span class="sxs-lookup"><span data-stu-id="abc83-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="abc83-106">W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="abc83-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="abc83-107">Magazyn kolejek zapewnia asynchroniczną obsługę wiadomości do komunikacji między składnikami aplikacji, czy działają w chmurze hello, hello pulpitu, na serwerze lokalnym lub na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="abc83-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="abc83-108">Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="abc83-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="abc83-109">Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="abc83-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="abc83-110">Te scenariusze obejmują typowych zadań, takich jak tworzenie kolejki systemu Azure i dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="abc83-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="abc83-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="abc83-111">Prerequisites</span></span>

* [<span data-ttu-id="abc83-112">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abc83-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="abc83-113">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="abc83-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="abc83-114">Tworzenie kontrolera MVC</span><span class="sxs-lookup"><span data-stu-id="abc83-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="abc83-115">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="abc83-117">Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="abc83-119">Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *QueuesController*i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="abc83-121">Dodaj następujące hello *przy użyciu* toohello dyrektywy `QueuesController.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="abc83-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="abc83-122">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="abc83-122">Create a queue</span></span>

<span data-ttu-id="abc83-123">Witaj poniższe kroki przedstawiają sposób toocreate kolejki:</span><span class="sxs-lookup"><span data-stu-id="abc83-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="abc83-124">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-125">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="abc83-126">Dodaj metodę o nazwie **CreateQueue** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="abc83-127">W ramach hello **CreateQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-128">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="abc83-129">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="abc83-130">Pobierz **CloudQueue** obiekt, który reprezentuje nazwę odwołania toohello wymaganej kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="abc83-131">Witaj **CloudQueueClient.GetQueueReference** — metoda nie powoduje żądanie magazynu kolejek.</span><span class="sxs-lookup"><span data-stu-id="abc83-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="abc83-132">czy istnieje kolejka hello, zwracane jest odwołanie Hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-133">Wywołaj hello **CloudQueue.CreateIfNotExists** metody toocreate hello kolejki, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="abc83-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="abc83-134">Witaj **CloudQueue.CreateIfNotExists** metoda zwraca **true** Jeśli hello kolejka nie istnieje i został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="abc83-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="abc83-135">W przeciwnym razie **false** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="abc83-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="abc83-136">Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="abc83-137">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-138">Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateQueue** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-139">Otwórz `CreateQueue.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="abc83-140">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-141">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-142">Uruchamianie aplikacji hello, a następnie wybierz **Utwórz kolejkę** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Tworzenie kolejki](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="abc83-144">Jak wspomniano wcześniej, hello **CloudQueue.CreateIfNotExists** metoda zwraca **true** tylko, gdy hello kolejki nie istnieje i zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="abc83-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="abc83-145">W związku z tym po uruchomieniu aplikacji hello podczas hello kolejka istnieje, metoda hello zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="abc83-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="abc83-146">Aplikacja hello toorun wielokrotnie, należy usunąć kolejki hello przed ponownym uruchomieniem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="abc83-147">Trwa usuwanie kolejki hello może odbywać się za pośrednictwem hello **CloudQueue.Delete** metody.</span><span class="sxs-lookup"><span data-stu-id="abc83-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="abc83-148">Możesz także usunąć hello kolejki przy użyciu hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="abc83-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="abc83-149">Dodaj tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="abc83-149">Add a message tooa queue</span></span>

<span data-ttu-id="abc83-150">Po wprowadzeniu [utworzenie kolejki](#create-a-queue), można dodawać komunikaty toothat kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="abc83-151">Ta sekcja przeprowadzi Cię przez procedurę dodawania kolejki komunikatów tooa *kolejki testowej*.</span><span class="sxs-lookup"><span data-stu-id="abc83-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="abc83-152">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-153">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="abc83-154">Dodaj metodę o nazwie **AddMessage** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="abc83-155">W ramach hello **AddMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-156">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="abc83-157">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="abc83-158">Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="abc83-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-159">Utwórz hello **CloudQueueMessage** obiekt reprezentujący wiadomość hello ma tooadd toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="abc83-160">A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="abc83-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="abc83-161">Wywołaj hello **CloudQueue.AddMessage** metody tooadd hello messaged toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="abc83-162">Utwórz i ustaw kilku **obiekt ViewBag** właściwości do wyświetlenia w widoku hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="abc83-163">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-164">Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddMessage** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-165">Otwórz `AddMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="abc83-166">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-167">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-168">Uruchamianie aplikacji hello, a następnie wybierz **komunikat Dodaj** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Dodaj komunikat](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="abc83-170">Witaj dwie sekcje - [Przeczytaj wiadomość z kolejki bez jego usuwania](#read-a-message-from-a-queue-without-removing-it) i [odczytu i usuwania komunikatu z kolejki](#read-and-remove-a-message-from-a-queue) -ilustrują sposób tooread wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="abc83-171">Przeczytaj wiadomość z kolejki bez jego usuwania</span><span class="sxs-lookup"><span data-stu-id="abc83-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="abc83-172">W tej części przedstawiono sposób toopeek wiadomości w kolejce (odczytu hello pierwszą wiadomość bez jego usuwania).</span><span class="sxs-lookup"><span data-stu-id="abc83-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="abc83-173">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-174">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="abc83-175">Dodaj metodę o nazwie **PeekMessage** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="abc83-176">W ramach hello **PeekMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-177">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="abc83-178">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="abc83-179">Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="abc83-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-180">Wywołaj hello **CloudQueue.PeekMessage** metody tooread hello pierwszą wiadomość hello kolejki bez jego usuwania z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="abc83-181">Aktualizacja hello **obiekt ViewBag** z dwóch wartości: Nazwa kolejki hello i wiadomości powitania, który został odczytany.</span><span class="sxs-lookup"><span data-stu-id="abc83-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="abc83-182">Witaj **CloudQueueMessage** obiekt udostępnia dwie właściwości pobierania wartości obiektu hello: **CloudQueueMessage.AsBytes** i **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="abc83-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="abc83-183">**AsString** (używane w tym przykładzie) zwraca ciąg znaków, podczas gdy **AsBytes** zwraca tablicę bajtów.</span><span class="sxs-lookup"><span data-stu-id="abc83-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="abc83-184">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-185">Na powitania **Dodaj widok** okna dialogowego, wprowadź **PeekMessage** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-186">Otwórz `PeekMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="abc83-187">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-188">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-189">Uruchamianie aplikacji hello, a następnie wybierz **komunikat Peek** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Wgląd do wiadomości](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="abc83-191">Przeczytaj i usunąć wiadomości z kolejki</span><span class="sxs-lookup"><span data-stu-id="abc83-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="abc83-192">W tej sekcji omówiono sposób tooread i usuwanie wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="abc83-193">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-194">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="abc83-195">Dodaj metodę o nazwie **przeczytanyWiadomość** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="abc83-196">W ramach hello **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-197">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="abc83-198">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="abc83-199">Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="abc83-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-200">Wywołaj hello **CloudQueue.GetMessage** metody tooread hello pierwszą wiadomość hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="abc83-201">Witaj **CloudQueue.GetMessage** metoda pozwala hello innego kodu odczytującego komunikaty, aby żadnego innego kodu można zmodyfikować lub usunąć wiadomości powitania podczas z jego przetworzeniem komunikat niewidoczne dla tooany 30 sekund (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="abc83-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="abc83-202">toochange hello ilość czasu wiadomość hello jest niewidoczny, zmodyfikuj hello **visibilityTimeout** parametr przekazywany toohello **CloudQueue.GetMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="abc83-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="abc83-203">Wywołaj hello **CloudQueueMessage.Delete** metody toodelete hello wiadomości z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="abc83-204">Aktualizacja hello **obiekt ViewBag** z hello usunięte wiadomości i hello nazwę kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="abc83-205">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-206">Na powitania **Dodaj widok** okna dialogowego, wprowadź **przeczytanyWiadomość** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-207">Otwórz `ReadMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="abc83-208">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-209">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-210">Uruchamianie aplikacji hello, a następnie wybierz **komunikat odczytu/usuwania** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Komunikat do odczytu i usuwania](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="abc83-212">Pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="abc83-212">Get hello queue length</span></span>

<span data-ttu-id="abc83-213">W tej części przedstawiono, jak tooget hello długość kolejki (liczba komunikatów).</span><span class="sxs-lookup"><span data-stu-id="abc83-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="abc83-214">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-215">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="abc83-216">Dodaj metodę o nazwie **GetQueueLength** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="abc83-217">W ramach hello **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-218">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="abc83-219">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="abc83-220">Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="abc83-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-221">Wywołaj hello **CloudQueue.FetchAttributes** atrybutów kolejki metody tooretrieve hello (łącznie z jej długość).</span><span class="sxs-lookup"><span data-stu-id="abc83-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="abc83-222">Witaj dostępu **CloudQueue.ApproximateMessageCount** długość kolejki właściwości tooget hello.</span><span class="sxs-lookup"><span data-stu-id="abc83-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="abc83-223">Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki, a jego długość.</span><span class="sxs-lookup"><span data-stu-id="abc83-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="abc83-224">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-225">Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetQueueLength** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-226">Otwórz `GetQueueLengthMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="abc83-227">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-228">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-229">Uruchamianie aplikacji hello, a następnie wybierz **pobieranie długości kolejki** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Pobieranie długości kolejki](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="abc83-231">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="abc83-231">Delete a queue</span></span>
<span data-ttu-id="abc83-232">W tej części przedstawiono sposób toodelete kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="abc83-233">W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="abc83-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="abc83-234">Otwórz hello `QueuesController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="abc83-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="abc83-235">Dodaj metodę o nazwie **DeleteQueue** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="abc83-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="abc83-236">W ramach hello **DeleteQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="abc83-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="abc83-237">Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)</span><span class="sxs-lookup"><span data-stu-id="abc83-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="abc83-238">Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="abc83-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="abc83-239">Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="abc83-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="abc83-240">Wywołaj hello **CloudQueue.Delete** kolejki hello toodelete metody reprezentowany przez hello **CloudQueue** obiektu.</span><span class="sxs-lookup"><span data-stu-id="abc83-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="abc83-241">Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki, a jego długość.</span><span class="sxs-lookup"><span data-stu-id="abc83-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="abc83-242">W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="abc83-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="abc83-243">Na powitania **Dodaj widok** okna dialogowego, wprowadź **DeleteQueue** hello nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="abc83-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="abc83-244">Otwórz `DeleteQueue.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="abc83-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="abc83-245">W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="abc83-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="abc83-246">Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="abc83-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="abc83-247">Uruchamianie aplikacji hello, a następnie wybierz **pobieranie długości kolejki** toosee wyniki podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="abc83-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Usuwanie kolejki](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="abc83-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abc83-249">Next steps</span></span>
<span data-ttu-id="abc83-250">Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="abc83-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="abc83-251">Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="abc83-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="abc83-252">Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="abc83-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
