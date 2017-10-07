---
title: "aaaGet pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Jak tooget uruchamiane przy użyciu magazynu kolejek Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu tooa konto magazynu przy użyciu programu Visual Studio usługami"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie

Azure queue storage umożliwia wysyłanie komunikatów między składnikami aplikacji chmury. W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie. Magazyn kolejek zapewnia asynchroniczną obsługę wiadomości do komunikacji między składnikami aplikacji, czy działają w chmurze hello, hello pulpitu, na serwerze lokalnym lub na urządzeniu przenośnym. Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.

Ten samouczek pokazuje, jak kod toowrite ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu kolejek Azure. Te scenariusze obejmują typowych zadań, takich jak tworzenie kolejki systemu Azure i dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce.

##<a name="prerequisites"></a>Wymagania wstępne

* [Program Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Tworzenie kontrolera MVC 

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i wybierz z menu kontekstowego hello **kontrolera -> Dodaj**.

    ![Dodaj tooan kontrolera aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Na powitania **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Na powitania **Dodaj kontroler** okno dialogowe, nazwy kontrolera hello *QueuesController*i wybierz **Dodaj**.

    ![Kontroler MVC hello nazwy](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Dodaj następujące hello *przy użyciu* toohello dyrektywy `QueuesController.cs` pliku:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Tworzenie kolejki

Witaj poniższe kroki przedstawiają sposób toocreate kolejki:

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku. 

1. Dodaj metodę o nazwie **CreateQueue** zwracającą **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. W ramach hello **CreateQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Pobierz **CloudQueue** obiekt, który reprezentuje nazwę odwołania toohello wymaganej kolejki. Witaj **CloudQueueClient.GetQueueReference** — metoda nie powoduje żądanie magazynu kolejek. czy istnieje kolejka hello, zwracane jest odwołanie Hello. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Wywołaj hello **CloudQueue.CreateIfNotExists** metody toocreate hello kolejki, jeśli jeszcze nie istnieje. Witaj **CloudQueue.CreateIfNotExists** metoda zwraca **true** Jeśli hello kolejka nie istnieje i został utworzony pomyślnie. W przeciwnym razie **false** jest zwracany.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **CreateQueue** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `CreateQueue.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **Utwórz kolejkę** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Tworzenie kolejki](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Jak wspomniano wcześniej, hello **CloudQueue.CreateIfNotExists** metoda zwraca **true** tylko, gdy hello kolejki nie istnieje i zostanie utworzony. W związku z tym po uruchomieniu aplikacji hello podczas hello kolejka istnieje, metoda hello zwraca **false**. Aplikacja hello toorun wielokrotnie, należy usunąć kolejki hello przed ponownym uruchomieniem aplikacji hello. Trwa usuwanie kolejki hello może odbywać się za pośrednictwem hello **CloudQueue.Delete** metody. Możesz także usunąć hello kolejki przy użyciu hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub hello [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Dodaj tooa kolejki komunikatów

Po wprowadzeniu [utworzenie kolejki](#create-a-queue), można dodawać komunikaty toothat kolejki. Ta sekcja przeprowadzi Cię przez procedurę dodawania kolejki komunikatów tooa *kolejki testowej*. 

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku.

1. Dodaj metodę o nazwie **AddMessage** zwracającą **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **AddMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Utwórz hello **CloudQueueMessage** obiekt reprezentujący wiadomość hello ma tooadd toohello kolejki. A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Wywołaj hello **CloudQueue.AddMessage** metody tooadd hello messaged toohello kolejki.

    ```csharp
    queue.AddMessage(message);
    ```

1. Utwórz i ustaw kilku **obiekt ViewBag** właściwości do wyświetlenia w widoku hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **AddMessage** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `AddMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **komunikat Dodaj** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Dodaj komunikat](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Witaj dwie sekcje - [Przeczytaj wiadomość z kolejki bez jego usuwania](#read-a-message-from-a-queue-without-removing-it) i [odczytu i usuwania komunikatu z kolejki](#read-and-remove-a-message-from-a-queue) -ilustrują sposób tooread wiadomości z kolejki.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Przeczytaj wiadomość z kolejki bez jego usuwania

W tej części przedstawiono sposób toopeek wiadomości w kolejce (odczytu hello pierwszą wiadomość bez jego usuwania).  

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku.

1. Dodaj metodę o nazwie **PeekMessage** zwracającą **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **PeekMessage** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Wywołaj hello **CloudQueue.PeekMessage** metody tooread hello pierwszą wiadomość hello kolejki bez jego usuwania z kolejki hello. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Aktualizacja hello **obiekt ViewBag** z dwóch wartości: Nazwa kolejki hello i wiadomości powitania, który został odczytany. Witaj **CloudQueueMessage** obiekt udostępnia dwie właściwości pobierania wartości obiektu hello: **CloudQueueMessage.AsBytes** i **CloudQueueMessage.AsString**. **AsString** (używane w tym przykładzie) zwraca ciąg znaków, podczas gdy **AsBytes** zwraca tablicę bajtów.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **PeekMessage** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `PeekMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

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

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **komunikat Peek** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Wgląd do wiadomości](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Przeczytaj i usunąć wiadomości z kolejki

W tej sekcji omówiono sposób tooread i usuwanie wiadomości z kolejki.   

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku.

1. Dodaj metodę o nazwie **przeczytanyWiadomość** zwracającą **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Wywołaj hello **CloudQueue.GetMessage** metody tooread hello pierwszą wiadomość hello kolejki. Witaj **CloudQueue.GetMessage** metoda pozwala hello innego kodu odczytującego komunikaty, aby żadnego innego kodu można zmodyfikować lub usunąć wiadomości powitania podczas z jego przetworzeniem komunikat niewidoczne dla tooany 30 sekund (domyślnie). toochange hello ilość czasu wiadomość hello jest niewidoczny, zmodyfikuj hello **visibilityTimeout** parametr przekazywany toohello **CloudQueue.GetMessage** metody.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Wywołaj hello **CloudQueueMessage.Delete** metody toodelete hello wiadomości z kolejki hello.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Aktualizacja hello **obiekt ViewBag** z hello usunięte wiadomości i hello nazwę kolejki hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **przeczytanyWiadomość** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `ReadMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

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

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **komunikat odczytu/usuwania** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Komunikat do odczytu i usuwania](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Pobieranie długości kolejki hello

W tej części przedstawiono, jak tooget hello długość kolejki (liczba komunikatów). 

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku.

1. Dodaj metodę o nazwie **GetQueueLength** zwracającą **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **przeczytanyWiadomość** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Wywołaj hello **CloudQueue.FetchAttributes** atrybutów kolejki metody tooretrieve hello (łącznie z jej długość). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Witaj dostępu **CloudQueue.ApproximateMessageCount** długość kolejki właściwości tooget hello.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki, a jego długość.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **GetQueueLength** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `GetQueueLengthMessage.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **pobieranie długości kolejki** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Pobieranie długości kolejki](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Usuwanie kolejki
W tej części przedstawiono sposób toodelete kolejki. 

> [!NOTE]
> 
> W tej sekcji założono zostały wykonane kroki hello [Konfigurowanie środowiska deweloperskiego hello](#set-up-the-development-environment). 

1. Otwórz hello `QueuesController.cs` pliku.

1. Dodaj metodę o nazwie **DeleteQueue** zwracającą **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. W ramach hello **DeleteQueue** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Użyj hello poniższy kod tooget hello połączenia ciągu i przechowywania informacji o koncie magazynu z konfiguracji usługi Azure hello: (zmiana  *&lt;nazwy konta magazynu >* toohello nazwę hello magazynu Azure konto, której masz dostęp.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Pobierz **CloudQueueClient** obiekt reprezentuje klienta usługi kolejki.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Pobierz **CloudQueueContainer** obiekt, który reprezentuje kolejkę toohello odwołania. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Wywołaj hello **CloudQueue.Delete** kolejki hello toodelete metody reprezentowany przez hello **CloudQueue** obiektu.

    ```csharp
    queue.Delete();
    ```

1. Aktualizacja hello **obiekt ViewBag** o nazwie hello hello kolejki, a jego długość.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. W hello **Eksploratora rozwiązań**, rozwiń hello **widoków** folderu, kliknij prawym przyciskiem myszy **kolejek**i wybierz z menu kontekstowego hello **Dodaj -> Widok**.

1. Na powitania **Dodaj widok** okna dialogowego, wprowadź **DeleteQueue** hello nazwy widoku i wybierz **Dodaj**.

1. Otwórz `DeleteQueue.cshtml`i zmodyfikuj go, aby wygląda hello następującego fragmentu kodu:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. W hello **Eksploratora rozwiązań**, rozwiń węzeł hello **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.

1. Po hello ostatniego **Html.ActionLink**, Dodaj następujące hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Uruchamianie aplikacji hello, a następnie wybierz **pobieranie długości kolejki** toosee wyniki podobne toohello po zrzut ekranu:
  
    ![Usuwanie kolejki](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.

  * [Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
