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
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="9e64d-104">Jak toouse magazynu kolejek w języku Java</span><span class="sxs-lookup"><span data-stu-id="9e64d-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="9e64d-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9e64d-105">Overview</span></span>
<span data-ttu-id="9e64d-106">W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="9e64d-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="9e64d-107">Hello przykłady są napisane w języku Java i używają hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="9e64d-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="9e64d-108">Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie** i **usuwanie** kolejek.</span><span class="sxs-lookup"><span data-stu-id="9e64d-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="9e64d-109">Aby uzyskać więcej informacji dotyczących kolejek, zobacz hello [następne kroki](#Next-Steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9e64d-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="9e64d-110">Uwaga: Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="9e64d-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="9e64d-111">Aby uzyskać więcej informacji, zobacz hello [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="9e64d-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="9e64d-112">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="9e64d-112">Create a Java application</span></span>
<span data-ttu-id="9e64d-113">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9e64d-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="9e64d-114">toodo tak, konieczne będzie tooinstall hello Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e64d-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="9e64d-115">Po zostało to zrobione, należy tooverify spełniającym w systemie deweloperskim hello minimalne wymagania i zależności, które są wymienione w hello [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e64d-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="9e64d-116">Jeżeli komputer spełnia te wymagania, należy wykonać hello instrukcje dotyczące pobierania i instalowania hello biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="9e64d-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="9e64d-117">Po wykonaniu tych zadań, będzie możliwe toocreate aplikacji Java, który używa hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9e64d-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="9e64d-118">Konfigurowanie magazynu kolejek tooaccess Twojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="9e64d-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="9e64d-119">Dodaj następujące importu instrukcje toohello górnej części pliku Java hello miejscu kolejki tooaccess interfejsów API usługi Azure storage toouse hello:</span><span class="sxs-lookup"><span data-stu-id="9e64d-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="9e64d-120">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="9e64d-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="9e64d-121">Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9e64d-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9e64d-122">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, przy użyciu hello nazwy konta magazynu i hello podstawowy klucz dostępu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="9e64d-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9e64d-123">Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:</span><span class="sxs-lookup"><span data-stu-id="9e64d-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="9e64d-124">W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi hello, *pliku ServiceConfiguration.cscfg*i jest dostępny z toohello wywołania  **RoleEnvironment.getConfigurationSettings** metody.</span><span class="sxs-lookup"><span data-stu-id="9e64d-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="9e64d-125">Oto przykład pobierania hello parametrów połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi hello:</span><span class="sxs-lookup"><span data-stu-id="9e64d-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="9e64d-126">Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.</span><span class="sxs-lookup"><span data-stu-id="9e64d-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9e64d-127">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="9e64d-127">How to: Create a queue</span></span>
<span data-ttu-id="9e64d-128">A **CloudQueueClient** obiektu pozwala pobierać obiekty odwołań do kolejki.</span><span class="sxs-lookup"><span data-stu-id="9e64d-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="9e64d-129">Witaj poniższy kod tworzy **CloudQueueClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="9e64d-130">(Uwaga: istnieją dodatkowe sposoby toocreate **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w hello [odwołaniazestawuSDKklientamagazynuAzure].)</span><span class="sxs-lookup"><span data-stu-id="9e64d-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="9e64d-131">Użyj hello **CloudQueueClient** tooget kolejki toohello odwołanie ma toouse obiektu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="9e64d-132">Można utworzyć kolejki hello, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="9e64d-132">You can create hello queue if it doesn't exist.</span></span>

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

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="9e64d-133">Porady: Dodawanie tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="9e64d-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="9e64d-134">tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="9e64d-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="9e64d-135">Następnie wywołaj hello **addMessage** metody.</span><span class="sxs-lookup"><span data-stu-id="9e64d-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="9e64d-136">A **CloudQueueMessage** można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="9e64d-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="9e64d-137">Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="9e64d-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="9e64d-138">Porady: Podgląd przy następnej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="9e64d-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="9e64d-139">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello wywołując **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="9e64d-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="9e64d-140">Porady: Zmienianie hello zawartość komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="9e64d-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="9e64d-141">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello.</span><span class="sxs-lookup"><span data-stu-id="9e64d-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="9e64d-142">Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji.</span><span class="sxs-lookup"><span data-stu-id="9e64d-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="9e64d-143">powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="9e64d-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="9e64d-144">Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="9e64d-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="9e64d-145">Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="9e64d-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="9e64d-146">Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="9e64d-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="9e64d-147">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="9e64d-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="9e64d-148">następujące Hello kodu próbki przeszukuje hello kolejki komunikatów, lokalizuje hello pierwszy wiadomości, która odpowiada zawartości hello "Hello, World", a następnie modyfikuje zawartości wiadomości powitania kończy działanie.</span><span class="sxs-lookup"><span data-stu-id="9e64d-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

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

<span data-ttu-id="9e64d-149">Alternatywnie hello Poniższy przykładowy kod aktualizuje tylko pierwszy widoczny wiadomości powitania na powitania kolejki.</span><span class="sxs-lookup"><span data-stu-id="9e64d-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="9e64d-150">Porady: pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="9e64d-150">How to: Get hello queue length</span></span>
<span data-ttu-id="9e64d-151">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="9e64d-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="9e64d-152">Witaj **downloadAttributes** metody zapyta usługi kolejek hello kilka bieżące wartości, w tym liczbę liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="9e64d-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="9e64d-153">Liczba Hello jest przybliżonej tylko w przypadku, ponieważ komunikaty mogą dodane lub usunięte po hello usługi kolejki odpowiada tooyour żądania.</span><span class="sxs-lookup"><span data-stu-id="9e64d-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="9e64d-154">Witaj **getApproximateMessageCount** metoda zwraca ostatnią wartość hello pobierane przez wywołanie hello zbyt**downloadAttributes**, bez wywoływania usługi kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="9e64d-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

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

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="9e64d-155">Porady: usuwania z kolejki dalej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="9e64d-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="9e64d-156">Kod dequeues wiadomości z kolejki w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="9e64d-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="9e64d-157">Podczas wywoływania **retrieveMessage**, Pobierz hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="9e64d-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="9e64d-158">Komunikat zwrócony z **retrieveMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="9e64d-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="9e64d-159">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="9e64d-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="9e64d-160">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="9e64d-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="9e64d-161">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="9e64d-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="9e64d-162">Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="9e64d-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="9e64d-163">Dodatkowe opcje usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="9e64d-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="9e64d-164">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="9e64d-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="9e64d-165">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="9e64d-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="9e64d-166">Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="9e64d-167">Witaj poniższy przykład kodu wykorzystuje hello **retrieveMessages** metody tooget 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="9e64d-168">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="9e64d-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="9e64d-169">Ustawia również hello niewidoczności limitu czasu toofive minut (300 sekund) dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="9e64d-170">Należy pamiętać, że hello pięć minut rozpoczyna się dla wszystkich komunikatów na powitania sam czasu, gdy pięciu minut od wywołania hello zbyt**retrieveMessages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="9e64d-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="9e64d-171">Porady: Lista kolejek hello</span><span class="sxs-lookup"><span data-stu-id="9e64d-171">How to: List hello queues</span></span>
<span data-ttu-id="9e64d-172">Lista kolejek bieżącego hello, wywołanie hello tooobtain **CloudQueueClient.listQueues()** metodę, która będzie zwracać kolekcję **CloudQueue** obiektów.</span><span class="sxs-lookup"><span data-stu-id="9e64d-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9e64d-173">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="9e64d-173">How to: Delete a queue</span></span>
<span data-ttu-id="9e64d-174">toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej hello wywołania **deleteIfExists** metody na powitania **CloudQueue** obiektu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9e64d-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e64d-175">Next steps</span></span>
<span data-ttu-id="9e64d-176">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="9e64d-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="9e64d-177">[Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="9e64d-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="9e64d-178">[Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołaniazestawuSDKklientamagazynuAzure]</span><span class="sxs-lookup"><span data-stu-id="9e64d-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="9e64d-179">[Interfejs API REST usług magazynu Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="9e64d-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="9e64d-180">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="9e64d-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołaniazestawuSDKklientamagazynuAzure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
