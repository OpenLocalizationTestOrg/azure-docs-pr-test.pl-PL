---
title: "Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu programu .NET | Microsoft Docs"
description: "Usługa Azure Queues zapewnia niezawodne, asynchroniczne przesyłanie komunikatów między składnikami aplikacji. Przesyłanie komunikatów za pomocą chmury umożliwia składnikom aplikacji niezależne skalowanie."
services: storage
documentationcenter: .net
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: tamram
ms.openlocfilehash: 00c737205c8970bf3cd3036b8bfa653c962949d0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Omówienie
Usługa Azure Queue Storage umożliwia przesyłanie komunikatów za pomocą chmury między składnikami aplikacji. W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie. Usługa Queue Storage zapewnia asynchroniczne przesyłanie komunikatów na potrzeby komunikacji między składnikami aplikacji niezależnie od tego, czy działają w chmurze, na komputerze, serwerze lokalnym czy urządzeniu przenośnym. Usługa Queue Storage obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.

### <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku pokazano, jak napisać kod .NET dla niektórych typowych scenariuszy przy użyciu usługi Azure Queue Storage. Omówione scenariusze obejmują tworzenie i usuwanie kolejek oraz dodawanie, odczytywanie i usuwanie komunikatów kolejek.

**Szacowany czas trwania:** 45 minut

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
Dodaj następujące dyrektywy `using` na początku pliku `Program.cs`:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a>Analizowanie parametrów połączenia
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a>Tworzenie klienta usługi kolejki
Klasa **CloudQueueClient** umożliwia pobieranie kolejek przechowywanych w usłudze Queue Storage. Oto jeden ze sposobów tworzenia klienta usługi:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Teraz możesz przystąpić do pisania kodu, który będzie odczytywać dane z usługi Queue Storage i zapisywać je w nim.

## <a name="create-a-queue"></a>Tworzenie kolejki
W tym przykładzie pokazano, jak utworzyć kolejkę, jeśli jeszcze nie istnieje:

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

## <a name="insert-a-message-into-a-queue"></a>Wstawianie komunikatu do kolejki
Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nową klasę **CloudQueueMessage**. Następnie wywołaj metodę **AddMessage**. Klasę **CloudQueueMessage** można utworzyć przy użyciu ciągu (w formacie UTF-8) lub tablicy **bajtów**. Oto kod, który tworzy kolejkę (jeśli kolejka nie istnieje) i wstawia komunikat „Hello, World”:

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

## <a name="peek-at-the-next-message"></a>Podgląd kolejnego komunikatu
Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując metodę **PeekMessage**.

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

## <a name="change-the-contents-of-a-queued-message"></a>Zmiana zawartości komunikatu w kolejce
Możesz zmienić zawartość komunikatu w kolejce. Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania. Poniższy kod aktualizuje komunikat kolejki o nową zawartość i ustawia rozszerzenie limitu czasu widoczności o kolejne 60 sekund. Operacja ta zapisuje stan pracy powiązanej z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad komunikatem. Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania. Zazwyczaj stosuje się również liczbę ponownych prób. Jeśli komunikat zostanie ponowiony więcej niż *n* razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

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

## <a name="de-queue-the-next-message"></a>Usunięcie następnego komunikatu z kolejki
Twój kod usuwa komunikat z kolejki w dwóch etapach. Jeśli wywołasz funkcję **GetMessage**, uzyskasz następny komunikat w kolejce. Komunikat zwrócony z funkcji **GetMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund. Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać funkcję **DeleteMessage**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę. Twój kod wywołuje funkcję **DeleteMessage** natychmiast po przetworzeniu komunikatu.

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Używanie wzorca Async-Await z wspólnymi interfejsami API usługi Queue Storage
Ten przykład przedstawia sposób użycia wzorca Async-Await z wykorzystaniem wspólnych interfejsów API usługi Queue Storage. Przykład wywołuje asynchroniczną wersję każdej z danych metod, co jest wskazane przez sufiks *Async* każdej metody. Jeśli zostanie użyta metoda asynchroniczna, wzorzec Async-Await zawiesi lokalne wykonanie do momentu ukończenia wywołania. Takie zachowanie umożliwia wykonywanie innych zadań przez bieżący wątek, co pomaga unikać wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji. Aby uzyskać szczegółowe informacje o wykorzystaniu wzorca Async-Await w programie .NET, zobacz [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx) (Async i Await [C# i Visual Basic]).

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.
Po pierwsze można uzyskać komunikaty zbiorczo (do 32). Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu. Poniższy przykład kodu wykorzystuje metodę **GetMessages**, aby pobrać 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**. Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu. Należy zauważyć, że okres 5 minut rozpoczyna się dla wszystkich komunikatów w tym samym czasie, więc po upływie 5 minut od wywołania metody **GetMessages** wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.

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

## <a name="get-the-queue-length"></a>Pobieranie długości kolejki
Możesz uzyskać szacunkową liczbę komunikatów w kolejce. Metoda **FetchAttributes** prosi usługę kolejki o pobranie atrybutów kolejki, w tym liczby komunikatów. Właściwość **ApproximateMessageCount** zwraca ostatnią wartość pobraną przez metodę **FetchAttributes** bez wywoływania usługi kolejki.

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

## <a name="delete-a-queue"></a>Usuwanie kolejki
Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj metodę **Delete** na obiekcie kolejki.

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
    

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy usługi Queue Storage, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.

* Przejrzyj dokumentację referencyjną usługi kolejki, aby uzyskać szczegółowe informacje o dostępnych interfejsach API:
  * [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Dokumentacja interfejsu API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Dowiedz się, jak uprościć zapisywany kod, aby pracować z usługą Azure Storage za pomocą zestawu [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).
* Wyświetl więcej poradników dotyczących funkcji, aby dowiedzieć się więcej o dodatkowych opcjach przechowywania danych na platformie Azure.
  * Zapoznaj się z tematem [Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md), aby przechowywać dane strukturalne.
  * Zapoznaj się z tematem [Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md), aby przechowywać dane bez struktury.
  * [Połącz się z usługą SQL Database przy użyciu platformy .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md), aby zapisać dane relacyjne.

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
