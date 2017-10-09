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
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Rozpoczynanie pracy z magazynem kolejek i Visual Studio połączone usługi (platformy ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uruchamiania przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie platformy ASP.NET Core za pomocą programu Visual Studio hello tooget **dodać usług połączonych** okna dialogowego. Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.

Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. Pojedynczy komunikat z kolejki można się too64 kilobajtów (KB), rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.

tooget uruchomiona, należy najpierw toocreate kolejce platformy Azure na koncie magazynu. Poniżej opisano sposób toocreate kolejki w kodzie. Również pokażemy ci jak tooperform basic kolejki operacji, takich jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce. Przykłady Hello są napisane w języku C\# kodu i użyć hello biblioteki klienta magazynu Azure dla platformy .NET. Aby uzyskać więcej informacji na temat platformy ASP.NET, zobacz [ASP.NET](http://www.asp.net).

**Uwaga:** niektóre hello interfejsów API, które wykonywania wywołań tooAzure magazynu w ASP.NET Core są asynchroniczne. Zobacz [programowanie asynchroniczne z Async i Await](http://msdn.microsoft.com/library/hh191443.aspx) Aby uzyskać więcej informacji. Poniższy kod Hello przyjęto założenie, że są używane metody programowania asynchronicznego.

* Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji o programowo manipulowanie kolejek.
* Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.
* Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.
* Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.

## <a name="access-queues-in-code"></a>Uzyskiwanie dostępu do kolejek w kodzie
kolejki tooaccess w projektach platformy ASP.NET Core, należy tooinclude hello następujących elementów pliku źródłowego tooany C#, który uzyskuje dostęp do magazynu kolejek Azure.

1. Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Pobierz **CloudQueueClient** obiekt tooreference hello kolejki obiektów na koncie magazynu.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Pobierz **CloudQueue** obiekt tooreference określonej kolejki.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.

### <a name="create-a-queue-in-code"></a>Tworzenie kolejki w kodzie
toocreate hello kolejki systemu Azure w kodzie, wystarczy dodać wywołanie za**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Dodaj tooa kolejki komunikatów
tooinsert komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiektu, a następnie wywołania hello **AddMessageAsync** metody.

A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.

Oto przykład, która wstawia wiadomości powitania "Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Przeczytaj wiadomość w kolejce
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessageAsync** metody.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Przeczytaj i usuwanie wiadomości w kolejce
Można usunąć kodu (dequeue) wiadomość z kolejki w dwóch krokach.

1. Wywołanie **GetMessageAsync** tooget hello następnej wiadomości w kolejce. Komunikat zwrócony z **GetMessageAsync** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.
2. toofinish usuwanie wiadomości powitania z kolejki hello, wywołanie **DeleteMessageAsync**.

Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Witaj poniższy kod wywołania **DeleteMessageAsync** natychmiast po przetworzeniu wiadomość hello.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>Wykorzystanie dodatkowych opcji usuwania komunikatów
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.
Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**. Ustawia również minut too5 limitu czasu niewidoczności powitania dla każdego komunikatu. Należy pamiętać, że hello start 5 minut dla wszystkich komunikatów na powitania sam czasu, dlatego po 5 minut po wywołaniu hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte stają się widoczne ponownie.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Pobieranie długości kolejki hello
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. **FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania. Witaj **ApproximateMethodCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Użyj wzorca Async-Await hello z kolejką wspólnych interfejsów API
Ten przykład przedstawia, jak toouse hello wzorca Async-Await z kolejką wspólnych interfejsów API. Hello próbki wywołania hello async wersja każdego hello podanej metody. Można to zaobserwować przez poprawka hello asynchronicznych po każdej metody. W przypadku metody asynchronicznej hello wzorca Async-Await zawiesi lokalne wykonanie do czasu ukończenia wywołania hello. Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello. Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET, zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
## <a name="delete-a-queue"></a>Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć** metody dla obiekt kolejki hello.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Następne kroki
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

