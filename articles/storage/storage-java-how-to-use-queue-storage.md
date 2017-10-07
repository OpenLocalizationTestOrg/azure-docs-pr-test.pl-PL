---
title: "toouse aaaHow magazynu kolejek w języku Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate usługi kolejek platformy Azure hello toouse i usuwania kolejki oraz insert, Pobierz i usunąć wiadomości. Przykłady napisany w języku Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a>Jak toouse magazynu kolejek w języku Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure. Hello przykłady są napisane w języku Java i używają hello [Azure Storage SDK for Java][Azure Storage SDK for Java]. Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie** i **usuwanie** kolejek. Aby uzyskać więcej informacji dotyczących kolejek, zobacz hello [następne kroki](#Next-Steps) sekcji.

Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android. Aby uzyskać więcej informacji, zobacz hello [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Tworzenie aplikacji Java
W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.

toodo tak, konieczne będzie tooinstall hello Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure. Po zostało to zrobione, należy tooverify spełniającym w systemie deweloperskim hello minimalne wymagania i zależności, które są wymienione w hello [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub. Jeżeli komputer spełnia te wymagania, należy wykonać hello instrukcje dotyczące pobierania i instalowania hello biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium. Po wykonaniu tych zadań, będzie możliwe toocreate aplikacji Java, który używa hello przykłady w tym artykule.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Konfigurowanie magazynu kolejek tooaccess Twojej aplikacji
Dodaj następujące importu instrukcje toohello górnej części pliku Java hello miejscu kolejki tooaccess interfejsów API usługi Azure storage toouse hello:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Konfiguracja parametrów połączenia usługi Azure storage
Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, przy użyciu hello nazwy konta magazynu i hello podstawowy klucz dostępu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości. Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi hello, *pliku ServiceConfiguration.cscfg*i jest dostępny z toohello wywołania  **RoleEnvironment.getConfigurationSettings** metody. Oto przykład pobierania hello parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.

## <a name="how-to-create-a-queue"></a>Porady: Tworzenie kolejki
A **CloudQueueClient** obiektu pozwala pobierać obiekty odwołań do kolejki. Witaj poniższy kod tworzy **CloudQueueClient** obiektu. (Uwaga: istnieją dodatkowe sposoby toocreate **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w hello [odwołaniazestawuSDKklientamagazynuAzure].)

Użyj hello **CloudQueueClient** tooget kolejki toohello odwołanie ma toouse obiektu. Można utworzyć kolejki hello, jeśli nie istnieje.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a>Porady: Dodawanie tooa kolejki komunikatów
tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **CloudQueueMessage**. Następnie wywołaj hello **addMessage** metody. A **CloudQueueMessage** można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów. Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World".

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a>Porady: Podgląd przy następnej wiadomości powitania
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello wywołując **peekMessage**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Porady: Zmienianie hello zawartość komunikatu w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello. Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji. powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund. Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta. Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania. Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

następujące Hello kodu próbki przeszukuje hello kolejki komunikatów, lokalizuje hello pierwszy wiadomości, która odpowiada zawartości hello "Hello, World", a następnie modyfikuje zawartości wiadomości powitania kończy działanie.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Alternatywnie hello Poniższy przykładowy kod aktualizuje tylko pierwszy widoczny wiadomości powitania na powitania kolejki.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a>Porady: pobieranie długości kolejki hello
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. Witaj **downloadAttributes** metody zapyta usługi kolejek hello kilka bieżące wartości, w tym liczbę liczbę wiadomości w kolejce. Liczba Hello jest przybliżonej tylko w przypadku, ponieważ komunikaty mogą dodane lub usunięte po hello usługi kolejki odpowiada tooyour żądania. Witaj **getApproximateMessageCount** metoda zwraca ostatnią wartość hello pobierane przez wywołanie hello zbyt**downloadAttributes**, bez wywoływania usługi kolejki hello.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a>Porady: usuwania z kolejki dalej wiadomości powitania
Kod dequeues wiadomości z kolejki w dwóch krokach. Podczas wywoływania **retrieveMessage**, Pobierz hello następnej wiadomości w kolejce. Komunikat zwrócony z **retrieveMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **deleteMessage**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu wiadomość hello.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a>Dodatkowe opcje usuwania komunikatów
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki. Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.

Witaj poniższy przykład kodu wykorzystuje hello **retrieveMessages** metody tooget 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu **dla** pętli. Ustawia również hello niewidoczności limitu czasu toofive minut (300 sekund) dla każdego komunikatu. Należy pamiętać, że hello pięć minut rozpoczyna się dla wszystkich komunikatów na powitania sam czasu, gdy pięciu minut od wywołania hello zbyt**retrieveMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a>Porady: Lista kolejek hello
Lista kolejek bieżącego hello, wywołanie hello tooobtain **CloudQueueClient.listQueues()** metodę, która będzie zwracać kolekcję **CloudQueue** obiektów.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a>Porady: Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej hello wywołania **deleteIfExists** metody na powitania **CloudQueue** obiektu.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* [Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]
* [Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołaniazestawuSDKklientamagazynuAzure]
* [Interfejs API REST usług magazynu Azure][Azure Storage Services REST API]
* [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołaniazestawuSDKklientamagazynuAzure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
