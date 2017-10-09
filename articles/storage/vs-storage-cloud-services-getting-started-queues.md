---
title: "aaaGet pracy z magazynem kolejek i Visual Studio podłączonych usług (usługi w chmurze) | Dokumentacja firmy Microsoft"
description: "Jak tooget pracy z magazynem kolejek Azure w projektu usługi w chmurze w programie Visual Studio, po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
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
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (usług w chmurze projekty)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uruchamiania przy użyciu magazynu kolejek Azure w programie Visual Studio po utworzony lub odwołanie do konta magazynu Azure w projekcie usługi w chmurze przy użyciu programu Visual Studio hello tooget **dodać usług połączonych** okna dialogowego .

Poniżej opisano sposób toocreate kolejki w kodzie. Również pokażemy ci jak tooperform basic kolejki operacji, takich jak dodawanie, modyfikowanie, Odczyt i usuwanie wiadomości w kolejce. Przykłady Hello są zapisywane w kodzie C# i używają hello [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Witaj **dodać usług połączonych** operacji instaluje hello odpowiednie NuGet pakiety tooaccess magazynu Azure w projekcie i dodaje hello parametry połączenia dla hello magazynu konta tooyour pliki konfiguracji projektu.

* Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) uzyskać więcej informacji na temat manipulowanie kolejek w kodzie.
* Zobacz [dokumentacji magazynu](https://azure.microsoft.com/documentation/services/storage/) ogólne informacje na temat usługi Azure Storage.
* Zobacz [dokumentacji usługi w chmurze](https://azure.microsoft.com/documentation/services/cloud-services/) ogólne informacje dotyczące usług w chmurze Azure.
* Zobacz [ASP.NET](http://www.asp.net) Aby uzyskać więcej informacji na temat programowania aplikacji ASP.NET.

Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.

## <a name="access-queues-in-code"></a>Uzyskiwanie dostępu do kolejek w kodzie
kolejki tooaccess w projektach Visual Studio Cloud Services, potrzebne tooinclude hello następujące elementy plik źródłowy tooany C#, który dostęp do magazynu kolejek Azure.

1. Upewnij się, że deklaracje przestrzeni nazw hello u góry pliku hello C# hello Uwzględnij je **przy użyciu** instrukcje.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Pobierz **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu. Witaj Użyj następującego kodu tooget hello parametry połączenia magazynu, a informacje o koncie magazynu z konfiguracji usługi Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Pobierz **CloudQueueClient** obiekt tooreference hello kolejki obiektów na koncie magazynu.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Pobierz **CloudQueue** obiekt tooreference określonej kolejki.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Uwaga:** korzystać ze wszystkich hello powyżej kodu przed kodem hello w hello następujące przykłady.

## <a name="create-a-queue-in-code"></a>Tworzenie kolejki w kodzie
kolejki hello toocreate w kodzie, wystarczy dodać wywołanie za**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Dodaj tooa kolejki komunikatów
tooinsert komunikat do istniejącej kolejki, Utwórz nową **CloudQueueMessage** obiektu, a następnie wywołania hello **AddMessage** metody.

A **CloudQueueMessage** obiektu można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.

Oto przykład, która wstawia wiadomości powitania "Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Przeczytaj wiadomość w kolejce
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **PeekMessage** metody.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Przeczytaj i usuwanie wiadomości w kolejce
Można usunąć kodu (cofnąć kolejka) wiadomości z kolejki w dwóch krokach.

1. Wywołanie **GetMessage** tooget hello następnej wiadomości w kolejce. Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.
2. toofinish usuwanie wiadomości powitania z kolejki hello, wywołanie **DeleteMessage**.

Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Witaj poniższy kod wywołania **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Użyj dodatkowych opcji tooprocess i usuwanie wiadomości w kolejce
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.

* Możesz uzyskać partię komunikatów (w górę too32).
* Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. następujące Hello przykład kodu wykorzystuje **GetMessages** metody tooget 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli **foreach**. Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu. Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**GetMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.

Oto przykład:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Pobieranie długości kolejki hello
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. **FetchAttributes** metody zapyta hello usługę kolejki o pobranie atrybutów kolejki hello, w tym liczbę wiadomości powitania. Witaj **ApproximateMethodCount** właściwość zwraca hello ostatnią wartość pobraną przez **FetchAttributes** bez wywoływania usługi kolejki hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Witaj wzorca Async-Await za pomocą wspólnych interfejsów API kolejki usługi Azure
Ten przykład przedstawia, jak wzorca Async-Await hello toouse ze wspólnych interfejsów API kolejki usługi Azure. przykład Hello wywołuje hello asynchronicznych wersji każdego hello podanej metody, można to zaobserwować przez hello **Async** poprawka po każdej metody. Gdy metody asynchronicznej jest używane hello async-await wzorzec zawiesi lokalne wykonanie do momentu ukończenia wywołania hello. Takie zachowanie umożliwia hello bieżącego wątku toodo inne zadania, co pomaga uniknąć wąskich gardeł zmniejszających wydajność i poprawia ogólną szybkość reakcji aplikacji hello. Aby uzyskać więcej informacji na temat używania hello wzorca Async-Await w programie .NET zobacz [Async i Await (C# i Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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

## <a name="delete-a-queue"></a>Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej, wywołanie hello **usunąć** metody dla obiekt kolejki hello.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

