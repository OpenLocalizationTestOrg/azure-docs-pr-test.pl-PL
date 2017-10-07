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
# <a name="get-started-with-azure-queue-storage-using-net"></a>Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Omówienie
Usługa Azure Queue Storage umożliwia przesyłanie komunikatów za pomocą chmury między składnikami aplikacji. W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie. Magazyn kolejek zapewnia asynchroniczną obsługę wiadomości do komunikacji między składnikami aplikacji, czy działają w chmurze hello, hello pulpitu, na serwerze lokalnym lub na urządzeniu przenośnym. Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.

### <a name="about-this-tutorial"></a>Informacje o tym samouczku
Ten samouczek pokazuje, jak kod toowrite .NET dla niektórych typowych scenariuszy przy użyciu magazynu kolejek Azure. Omówione scenariusze obejmują tworzenie i usuwanie kolejek oraz dodawanie, odczytywanie i usuwanie komunikatów kolejek.

**Szacowany czas toocomplete:** 45 minut

**Wymagania wstępne:**

* [Program Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteka klienta usługi Azure Storage dla programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Menedżer konfiguracji Azure dla programu .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Konto usługi Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Dodawanie dyrektyw using
Dodaj następujące hello `using` dyrektywy toohello początku hello `Program.cs` pliku:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Przeanalizować parametrów połączenia hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Tworzenie klienta usługi kolejki hello
Witaj **CloudQueueClient** klasa umożliwia możesz tooretrieve kolejek przechowywanych w magazynie kolejek. Klient usługi jednokierunkowej toocreate hello jest następujący:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooQueue pamięci masowej.

## <a name="create-a-queue"></a>Tworzenie kolejki
W tym przykładzie pokazano sposób toocreate kolejki, jeśli jeszcze nie istnieje:

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

## <a name="insert-a-message-into-a-queue"></a>Wstawianie komunikatu do kolejki
tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **CloudQueueMessage**. Następnie wywołaj hello **AddMessage** metody. Klasę **CloudQueueMessage** można utworzyć przy użyciu ciągu (w formacie UTF-8) lub tablicy **bajtów**. Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World":

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

## <a name="peek-at-hello-next-message"></a>Wglądu dalej wiadomości powitania
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessage** metody.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Zmień hello zawartość komunikatu w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello. Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji tooupdate stan hello zadania. powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund. Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta. Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania. Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

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

## <a name="de-queue-hello-next-message"></a>Kolejka do następnej wiadomości powitania
Twój kod usuwa komunikat z kolejki w dwóch etapach. Podczas wywoływania **GetMessage**, Pobierz hello następnej wiadomości w kolejce. Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **DeleteMessage**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Twój kod wywołuje **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Używanie wzorca Async-Await z wspólnymi interfejsami API usługi Queue Storage
Ten przykład przedstawia, jak wzorca Async-Await hello toouse ze wspólnych interfejsów API magazynu kolejek. przykład Witaj wywołuje hello asynchroniczną wersję każdej z hello podanej metody, wskazywany przez hello *Async* sufiks każdej metody. W przypadku metody asynchronicznej hello async-await wzorzec zawiesi lokalne wykonanie do momentu ukończenia wywołania hello. Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello. Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.
Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**. Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu. Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.

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

## <a name="get-hello-queue-length"></a>Pobieranie długości kolejki hello
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. **FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania. Witaj **ApproximateMessageCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.

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

## <a name="delete-a-queue"></a>Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć** metody dla obiekt kolejki hello.

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
    

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* Przejrzyj dokumentację referencyjną usługi kolejki hello szczegółowe informacje o dostępnych interfejsach API:
  * [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Dokumentacja interfejsu API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Dowiedz się, jak kod hello toosimplify pisania toowork z usługą Azure Storage za pomocą hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).
* Wyświetl więcej funkcji toolearn przewodników o dodatkowych opcjach przechowywania danych na platformie Azure.
  * [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore strukturę danych.
  * [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore danych bez struktury.
  * [Połącz tooSQL bazy danych przy użyciu programu .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relacyjnej bazie danych.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
