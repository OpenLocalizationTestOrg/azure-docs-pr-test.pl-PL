---
title: "Jak używać magazynu kolejek w języku Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi kolejek platformy Azure do tworzenia i usuwania kolejki, Wstaw, Pobierz i usunąć wiadomości. Przykłady napisany w języku Java."
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
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="7ab32-104">Jak używać Magazynu kolejek w języku Java</span><span class="sxs-lookup"><span data-stu-id="7ab32-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="7ab32-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7ab32-105">Overview</span></span>
<span data-ttu-id="7ab32-106">W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab32-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="7ab32-107">Przykłady są napisane w języku Java i użyj [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="7ab32-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="7ab32-108">Omówione scenariusze obejmują **wstawianie**, **wgląd**, **pobierania**, i **usuwanie** kolejki komunikatów, a także **tworzenie** i **usuwanie** kolejek.</span><span class="sxs-lookup"><span data-stu-id="7ab32-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="7ab32-109">Aby uzyskać więcej informacji dotyczących kolejek, zobacz [następne kroki](#Next-Steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7ab32-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="7ab32-110">Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="7ab32-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="7ab32-111">Aby uzyskać więcej informacji, zobacz [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="7ab32-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="7ab32-112">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="7ab32-112">Create a Java application</span></span>
<span data-ttu-id="7ab32-113">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab32-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="7ab32-114">Aby to zrobić, należy zainstalować zestaw Java Development Kit (JDK) i utworzyć konta magazynu platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab32-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="7ab32-115">Po zostało to zrobione, należy sprawdzić, czy platformie programistycznej spełnia minimalne wymagania i zależności, które są wymienione w [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7ab32-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="7ab32-116">Jeżeli system spełnia te wymagania, należy wykonać instrukcje dotyczące pobierania i instalowania biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="7ab32-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="7ab32-117">Po wykonaniu tych zadań, można utworzyć aplikacji Java, który używa przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="7ab32-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="7ab32-118">Konfigurowanie aplikacji dostęp do kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="7ab32-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="7ab32-119">Dodaj następujące instrukcje import u góry pliku języka Java, której chcesz używać interfejsów API magazynu Azure można uzyskać dostępu do kolejek:</span><span class="sxs-lookup"><span data-stu-id="7ab32-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="7ab32-120">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="7ab32-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="7ab32-121">Klienta usługi Azure storage używa parametrów połączenia magazynu do przechowywania punktów końcowych i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="7ab32-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="7ab32-122">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu w następującym formacie, przy użyciu nazwy konta magazynu i podstawowy klucz dostępu dla konta magazynu na liście [Azure Portal](https://portal.azure.com) dla *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="7ab32-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="7ab32-123">Ten przykład przedstawia, jak można zadeklarować pola statycznego do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="7ab32-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="7ab32-124">W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi *pliku ServiceConfiguration.cscfg*i jest dostępny w wyniku wywołania **RoleEnvironment.getConfigurationSettings** metody.</span><span class="sxs-lookup"><span data-stu-id="7ab32-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="7ab32-125">Oto przykład pobierania parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi:</span><span class="sxs-lookup"><span data-stu-id="7ab32-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="7ab32-126">Poniższe przykłady założono użycie jednej z tych dwóch metod można pobrać parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="7ab32-127">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="7ab32-127">How to: Create a queue</span></span>
<span data-ttu-id="7ab32-128">A **CloudQueueClient** obiektu pozwala pobierać obiekty odwołań do kolejki.</span><span class="sxs-lookup"><span data-stu-id="7ab32-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="7ab32-129">Poniższy kod tworzy **CloudQueueClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="7ab32-130">(Uwaga: istnieją dodatkowe sposoby tworzenia **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w [odwołania do zestawu SDK klienta magazynu Azure].)</span><span class="sxs-lookup"><span data-stu-id="7ab32-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="7ab32-131">Użyj **CloudQueueClient** obiekt, aby pobrać odwołanie do kolejki, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="7ab32-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="7ab32-132">Można utworzyć kolejkę, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7ab32-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="7ab32-133">Porady: dodawanie wiadomości do kolejki</span><span class="sxs-lookup"><span data-stu-id="7ab32-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="7ab32-134">Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nową klasę **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="7ab32-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="7ab32-135">Następnie wywołaj **addMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="7ab32-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="7ab32-136">A **CloudQueueMessage** można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="7ab32-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="7ab32-137">Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia komunikat "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="7ab32-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="7ab32-138">Porady: Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="7ab32-138">How to: Peek at the next message</span></span>
<span data-ttu-id="7ab32-139">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="7ab32-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="7ab32-140">Porady: zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7ab32-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="7ab32-141">Możesz zmienić zawartość komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7ab32-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="7ab32-142">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania.</span><span class="sxs-lookup"><span data-stu-id="7ab32-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="7ab32-143">Poniższy kod aktualizuje komunikat kolejki o nową zawartość i ustawia rozszerzenie limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="7ab32-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="7ab32-144">Operacja ta zapisuje stan pracy powiązanej z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad komunikatem.</span><span class="sxs-lookup"><span data-stu-id="7ab32-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="7ab32-145">Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="7ab32-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="7ab32-146">Zazwyczaj stosuje się również liczbę ponownych prób. Jeśli komunikat zostanie ponowiony więcej niż *n* razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="7ab32-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="7ab32-147">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="7ab32-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="7ab32-148">Przeszukuje kolejki komunikatów, następujący przykładowy kod znajduje pierwszy komunikat o zgodna "Hello, World" dla zawartości, a następnie modyfikuje zawartości wiadomości i kończy działanie.</span><span class="sxs-lookup"><span data-stu-id="7ab32-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="7ab32-149">Alternatywnie Poniższy przykładowy kod aktualizuje tylko pierwszy widoczny wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7ab32-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="7ab32-150">Porady: pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="7ab32-150">How to: Get the queue length</span></span>
<span data-ttu-id="7ab32-151">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7ab32-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="7ab32-152">**DownloadAttributes** metody prosi usługę kolejki dla kilku bieżące wartości, w tym liczbę liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7ab32-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="7ab32-153">Wartość licznika jest tylko przybliżoną, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada na żądania.</span><span class="sxs-lookup"><span data-stu-id="7ab32-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="7ab32-154">**GetApproximateMessageCount** metoda zwraca ostatnią wartość pobraną przez wywołanie **downloadAttributes**, bez wywoływania usługi kolejki.</span><span class="sxs-lookup"><span data-stu-id="7ab32-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="7ab32-155">Porady: usuwania z kolejki następny komunikat</span><span class="sxs-lookup"><span data-stu-id="7ab32-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="7ab32-156">Kod dequeues wiadomości z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="7ab32-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="7ab32-157">Podczas wywoływania **retrieveMessage**, Pobierz następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7ab32-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="7ab32-158">Komunikat zwrócony z **retrieveMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="7ab32-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="7ab32-159">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="7ab32-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="7ab32-160">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="7ab32-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="7ab32-161">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="7ab32-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="7ab32-162">Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="7ab32-163">Dodatkowe opcje usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="7ab32-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="7ab32-164">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="7ab32-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="7ab32-165">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="7ab32-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="7ab32-166">Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="7ab32-167">Poniższy przykład kodu wykorzystuje **retrieveMessages** metodę, aby pobrać 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="7ab32-168">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="7ab32-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="7ab32-169">Ustawia również limitu czasu niewidoczności na pięć minut (300 sekund) dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="7ab32-170">Należy pamiętać, że pięć minut rozpoczyna się na wszystkie wiadomości w tym samym czasie, więc po pięciu minut od czasu wywołania **retrieveMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="7ab32-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="7ab32-171">Porady: Lista kolejek</span><span class="sxs-lookup"><span data-stu-id="7ab32-171">How to: List the queues</span></span>
<span data-ttu-id="7ab32-172">Aby uzyskać listę bieżącego kolejek, należy wywołać **CloudQueueClient.listQueues()** metodę, która będzie zwracać kolekcję **CloudQueue** obiektów.</span><span class="sxs-lookup"><span data-stu-id="7ab32-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="7ab32-173">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="7ab32-173">How to: Delete a queue</span></span>
<span data-ttu-id="7ab32-174">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj **deleteIfExists** metoda **CloudQueue** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="7ab32-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ab32-175">Next steps</span></span>
<span data-ttu-id="7ab32-176">Teraz, kiedy znasz już podstawy magazynu kolejek, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="7ab32-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="7ab32-177">[Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="7ab32-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="7ab32-178">[Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołania do zestawu SDK klienta magazynu Azure]</span><span class="sxs-lookup"><span data-stu-id="7ab32-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="7ab32-179">[Interfejs API REST usług magazynu Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="7ab32-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="7ab32-180">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="7ab32-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołania do zestawu SDK klienta magazynu Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
