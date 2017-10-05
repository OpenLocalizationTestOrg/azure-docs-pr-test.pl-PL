---
title: "Jak używać magazynu kolejek w języku PHP | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie korzystania z usługi magazyn kolejek platformy Azure do tworzenia i usuwania kolejki, wstawianie, Pobierz i usunąć wiadomości. Przykłady są zapisywane w kodzie PHP."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="eab44-104">Jak używać Magazynu kolejek w języku PHP</span><span class="sxs-lookup"><span data-stu-id="eab44-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="eab44-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="eab44-105">Overview</span></span>
<span data-ttu-id="eab44-106">W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="eab44-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="eab44-107">Przykłady są zapisywane za pomocą klasy z zestawu Windows SDK dla programu PHP.</span><span class="sxs-lookup"><span data-stu-id="eab44-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="eab44-108">Objęte usługą scenariusze obejmują, wstawianie, wgląd, pobieranie i usuwanie komunikatów kolejek, a także tworzenie i usuwanie kolejek.</span><span class="sxs-lookup"><span data-stu-id="eab44-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="eab44-109">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="eab44-109">Create a PHP application</span></span>
<span data-ttu-id="eab44-110">Jedynym wymaganiem służący do tworzenia aplikacji PHP, który uzyskuje dostęp do magazynu kolejek Azure jest odwoływanie się do klasy z zestawu Azure SDK dla programu PHP z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="eab44-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="eab44-111">Narzędzia do programowania służy do tworzenia aplikacji, łącznie z Notatnika.</span><span class="sxs-lookup"><span data-stu-id="eab44-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="eab44-112">W tym przewodniku użyje funkcji magazynu kolejek, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="eab44-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="eab44-113">Pobierz bibliotek klienta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eab44-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="eab44-114">Konfigurowanie aplikacji dostęp do kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="eab44-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="eab44-115">Aby korzystanie z interfejsów API magazynu kolejek Azure, musisz:</span><span class="sxs-lookup"><span data-stu-id="eab44-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="eab44-116">Odwołanie do pliku automatycznej ładowarki przy użyciu [require_once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="eab44-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="eab44-117">Odwoływać się do wszystkich klas, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="eab44-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="eab44-118">Poniższy przykład pokazuje, jak dołączyć plik automatycznej ładowarki i odwołanie **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="eab44-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="eab44-119">W tym przykładzie (i inne przykłady w tym artykule) zakłada zainstalowano bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="eab44-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="eab44-120">Jeśli zainstalowano bibliotek ręcznie, konieczne będzie odwoływać się `WindowsAzure.php` automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="eab44-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="eab44-121">W poniższych przykładach `require_once` instrukcji będą wyświetlane zawsze, ale będzie można odwoływać się tylko klasy, które są niezbędne, na przykład do wykonania.</span><span class="sxs-lookup"><span data-stu-id="eab44-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="eab44-122">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="eab44-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="eab44-123">Można utworzyć wystąpienia klienta magazynu kolejek Azure, najpierw musi mieć prawidłowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="eab44-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="eab44-124">Format dla parametrów połączenia usługi kolejki ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="eab44-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="eab44-125">Aby uzyskać dostęp do usługi na żywo:</span><span class="sxs-lookup"><span data-stu-id="eab44-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="eab44-126">Aby uzyskać dostęp do emulatora magazynu:</span><span class="sxs-lookup"><span data-stu-id="eab44-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="eab44-127">Aby utworzyć dowolnego klienta usługi Azure, musisz użyć **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="eab44-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="eab44-128">Można użyć jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="eab44-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="eab44-129">Parametry połączenia należy przekazać bezpośrednio do niego.</span><span class="sxs-lookup"><span data-stu-id="eab44-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="eab44-130">Użyj **CloudConfigurationManager (CCM)** do sprawdzenia wiele źródeł zewnętrznych ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="eab44-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="eab44-131">Domyślnie, pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="eab44-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="eab44-132">Można dodać nowego źródła rozszerzając **ConnectionStringSource** klasy.</span><span class="sxs-lookup"><span data-stu-id="eab44-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="eab44-133">Przykłady przedstawione w tym miejscu parametry połączenia zostaną przekazane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="eab44-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="eab44-134">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="eab44-134">Create a queue</span></span>
<span data-ttu-id="eab44-135">A **QueueRestProxy** obiekt umożliwia tworzenie kolejki przy użyciu **createQueue** metody.</span><span class="sxs-lookup"><span data-stu-id="eab44-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="eab44-136">Podczas tworzenia kolejki, można ustawić opcje w kolejce, ale spowoduje to nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="eab44-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="eab44-137">(W poniższym przykładzie pokazano, jak ustawić metadanych w kolejce).</span><span class="sxs-lookup"><span data-stu-id="eab44-137">(The example below shows how to set metadata on a queue.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="eab44-138">Nie należy polegać na uwzględnianie wielkości liter w metadanych kluczy.</span><span class="sxs-lookup"><span data-stu-id="eab44-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="eab44-139">Wszystkie klucze są odczytywane z usługi pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="eab44-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="eab44-140">Dodaj komunikat do kolejki</span><span class="sxs-lookup"><span data-stu-id="eab44-140">Add a message to a queue</span></span>
<span data-ttu-id="eab44-141">Aby dodać wiadomości do kolejki, użyj **QueueRestProxy -> polecenie createMessage**.</span><span class="sxs-lookup"><span data-stu-id="eab44-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="eab44-142">Metoda ma nazwę kolejki, tekst komunikatu i opcje wiadomości, (które są opcjonalne).</span><span class="sxs-lookup"><span data-stu-id="eab44-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="eab44-143">Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="eab44-143">Peek at the next message</span></span>
<span data-ttu-id="eab44-144">Możesz uzyskać wgląd w komunikat (lub wiadomości) z przodu kolejki bez jego usuwania z kolejki, wywołując **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="eab44-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="eab44-145">Domyślnie **peekMessage** metoda zwraca pojedynczą wiadomość, ale można zmienić tę wartość przy użyciu **PeekMessagesOptions -> setNumberOfMessages** metody.</span><span class="sxs-lookup"><span data-stu-id="eab44-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="eab44-146">Usunięcie następnego komunikatu z kolejki</span><span class="sxs-lookup"><span data-stu-id="eab44-146">De-queue the next message</span></span>
<span data-ttu-id="eab44-147">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="eab44-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="eab44-148">Najpierw należy wywołać **QueueRestProxy -> listMessages**, która sprawia, że komunikat niewidoczne dla innego kodu, który jest czytania z kolejki.</span><span class="sxs-lookup"><span data-stu-id="eab44-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="eab44-149">Domyślnie ten komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="eab44-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="eab44-150">(Jeśli wiadomość nie jest usuwany w tym okresie, stanie się widoczna w kolejce ponownie.) Aby zakończyć usuwanie komunikatu z kolejki, należy wywołać **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="eab44-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="eab44-151">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie może przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="eab44-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="eab44-152">Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="eab44-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="eab44-153">Zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="eab44-153">Change the contents of a queued message</span></span>
<span data-ttu-id="eab44-154">Można zmienić zawartość komunikatu w miejscu w kolejce przez wywołanie metody **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="eab44-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="eab44-155">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania.</span><span class="sxs-lookup"><span data-stu-id="eab44-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="eab44-156">Poniższy kod aktualizuje komunikat kolejki o nową zawartość i Ustawia rozszerzenie limitu czasu widoczności kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="eab44-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="eab44-157">Zapisuje stan pracy, który został skojarzony z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad wiadomości.</span><span class="sxs-lookup"><span data-stu-id="eab44-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="eab44-158">Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="eab44-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="eab44-159">Zazwyczaj stosuje się również liczbę ponownych prób. Jeśli komunikat zostanie ponowiony więcej niż *n* razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="eab44-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="eab44-160">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="eab44-160">This protects against a message that triggers an application error each time it is processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="eab44-161">Dodatkowe opcje usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="eab44-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="eab44-162">Istnieją dwa sposoby, który można dostosować pobieranie wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="eab44-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="eab44-163">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="eab44-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="eab44-164">Po drugie można ustawić widoczności dłuższy lub krótszy limit czasu, dzięki czemu kod będzie bardziej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="eab44-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="eab44-165">Poniższy przykład kodu wykorzystuje **getMessages** metodę, aby pobrać 16 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="eab44-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="eab44-166">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="eab44-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="eab44-167">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="eab44-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a><span data-ttu-id="eab44-168">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="eab44-168">Get queue length</span></span>
<span data-ttu-id="eab44-169">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="eab44-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="eab44-170">**QueueRestProxy -> getQueueMetadata** metody prosi usługę kolejki do zwracania metadanych dotyczących kolejki.</span><span class="sxs-lookup"><span data-stu-id="eab44-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="eab44-171">Wywoływanie **getApproximateMessageCount** metody na zwracanym obiekcie zawiera liczbę liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="eab44-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="eab44-172">Wartość licznika jest tylko przybliżoną, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada na żądania.</span><span class="sxs-lookup"><span data-stu-id="eab44-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a><span data-ttu-id="eab44-173">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="eab44-173">Delete a queue</span></span>
<span data-ttu-id="eab44-174">Aby usunąć kolejkę i wszystkie znajdujące się w niej wiadomości, wywołaj **QueueRestProxy -> deleteQueue** metody.</span><span class="sxs-lookup"><span data-stu-id="eab44-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="eab44-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eab44-175">Next steps</span></span>
<span data-ttu-id="eab44-176">Teraz, kiedy znasz już podstawy magazynu kolejek Azure, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu:</span><span class="sxs-lookup"><span data-stu-id="eab44-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="eab44-177">Odwiedź stronę [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="eab44-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="eab44-178">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="eab44-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
<span data-ttu-id="eab44-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span><span class="sxs-lookup"><span data-stu-id="eab44-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span></span>
[Azure Portal]: https://portal.azure.com

