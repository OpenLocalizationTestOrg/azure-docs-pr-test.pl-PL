---
title: "toouse aaaHow magazynu kolejek w języku PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Azure kolejki magazynu usługi toocreate i usuwania kolejki oraz insert, Pobierz i usunąć wiadomości. Przykłady są zapisywane w kodzie PHP."
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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="a007e-104">Jak toouse magazynu kolejek w języku PHP</span><span class="sxs-lookup"><span data-stu-id="a007e-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="a007e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a007e-105">Overview</span></span>
<span data-ttu-id="a007e-106">W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="a007e-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="a007e-107">Przykłady Hello są zapisywane za pomocą klasy z hello zestaw Windows SDK dla programu PHP.</span><span class="sxs-lookup"><span data-stu-id="a007e-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="a007e-108">Witaj objęte usługą scenariusze obejmują Wstawianie, wgląd, pobieranie i usuwanie komunikatów kolejek, a także tworzenie i usuwanie kolejek.</span><span class="sxs-lookup"><span data-stu-id="a007e-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="a007e-109">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="a007e-109">Create a PHP application</span></span>
<span data-ttu-id="a007e-110">Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do magazynu kolejek Azure to hello odwołuje się do klas z hello Azure SDK for PHP z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="a007e-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="a007e-111">Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.</span><span class="sxs-lookup"><span data-stu-id="a007e-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="a007e-112">W tym przewodniku użyje funkcji magazynu kolejek, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a007e-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="a007e-113">Pobierz bibliotek klienckich hello Azure</span><span class="sxs-lookup"><span data-stu-id="a007e-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="a007e-114">Konfigurowanie sieci tooaccess aplikacji magazynu kolejek</span><span class="sxs-lookup"><span data-stu-id="a007e-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="a007e-115">Witaj toouse interfejsów API magazynu kolejek Azure, musisz:</span><span class="sxs-lookup"><span data-stu-id="a007e-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="a007e-116">Odwołanie hello automatycznej ładowarki pliku przy użyciu hello [require_once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="a007e-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="a007e-117">Odwoływać się do wszystkich klas, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="a007e-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="a007e-118">Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="a007e-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="a007e-119">W tym przykładzie (i inne przykłady w tym artykule) zakłada zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="a007e-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="a007e-120">Jeśli zainstalowano bibliotek hello ręcznie, trzeba będzie tooreference hello `WindowsAzure.php` automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="a007e-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="a007e-121">W poniższych przykładach hello, hello `require_once` instrukcji będą wyświetlane zawsze, ale będzie można odwoływać się tylko klasy hello, które są niezbędne dla tooexecute przykład hello.</span><span class="sxs-lookup"><span data-stu-id="a007e-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="a007e-122">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="a007e-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="a007e-123">tooinstantiate klienta magazynu kolejek Azure, musisz najpierw mieć prawidłowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="a007e-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="a007e-124">Witaj format dla parametrów połączenia usługi kolejki hello ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="a007e-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="a007e-125">Aby uzyskać dostęp do usługi na żywo:</span><span class="sxs-lookup"><span data-stu-id="a007e-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="a007e-126">Aby uzyskać dostęp do magazynu emulatora hello:</span><span class="sxs-lookup"><span data-stu-id="a007e-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="a007e-127">toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="a007e-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="a007e-128">Możesz użyć dowolnej z hello następujące techniki:</span><span class="sxs-lookup"><span data-stu-id="a007e-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="a007e-129">Przekaż połączenia hello ciągu bezpośrednio tooit.</span><span class="sxs-lookup"><span data-stu-id="a007e-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="a007e-130">Użyj **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="a007e-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="a007e-131">Domyślnie, pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="a007e-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="a007e-132">Można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** klasy.</span><span class="sxs-lookup"><span data-stu-id="a007e-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="a007e-133">Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="a007e-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="a007e-134">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="a007e-134">Create a queue</span></span>
<span data-ttu-id="a007e-135">A **QueueRestProxy** obiekt umożliwia tworzenie kolejki przy użyciu hello **createQueue** metody.</span><span class="sxs-lookup"><span data-stu-id="a007e-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="a007e-136">Podczas tworzenia kolejki, można ustawić opcje w kolejce hello, ale spowoduje to nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="a007e-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="a007e-137">(hello przykład poniżej przedstawiono, jak metadanych tooset dla kolejki.)</span><span class="sxs-lookup"><span data-stu-id="a007e-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="a007e-138">Nie należy polegać na uwzględnianie wielkości liter w metadanych kluczy.</span><span class="sxs-lookup"><span data-stu-id="a007e-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="a007e-139">Wszystkie klucze są odczytywane z usługi hello pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="a007e-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="a007e-140">Dodaj tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="a007e-140">Add a message tooa queue</span></span>
<span data-ttu-id="a007e-141">Użyj tooadd kolejkę komunikatów tooa **QueueRestProxy -> polecenie createMessage**.</span><span class="sxs-lookup"><span data-stu-id="a007e-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="a007e-142">Metoda Hello przyjmuje nazwę kolejki hello, tekst wiadomości powitania i opcje wiadomości, (które są opcjonalne).</span><span class="sxs-lookup"><span data-stu-id="a007e-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="a007e-143">Wglądu dalej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="a007e-143">Peek at hello next message</span></span>
<span data-ttu-id="a007e-144">Można uzyskać wgląd w komunikat (lub wiadomości) hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie metody **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="a007e-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="a007e-145">Domyślnie program hello **peekMessage** metoda zwraca pojedynczą wiadomość, ale można zmienić tę wartość przy użyciu hello **PeekMessagesOptions -> setNumberOfMessages** metody.</span><span class="sxs-lookup"><span data-stu-id="a007e-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="a007e-146">Kolejka do następnej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="a007e-146">De-queue hello next message</span></span>
<span data-ttu-id="a007e-147">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="a007e-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="a007e-148">Najpierw należy wywołać **QueueRestProxy -> listMessages**, co czyni hello komunikat niewidoczne tooany innego kodu, który jest czytania z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="a007e-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="a007e-149">Domyślnie ten komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="a007e-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="a007e-150">(Jeśli wiadomość hello nie jest usuwany w tym okresie, stanie się widoczne w kolejce hello ponownie.) z kolejki hello wiadomość hello usuwania toofinish należy wywołać **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="a007e-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="a007e-151">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy tooprocess kończy się niepowodzeniem z kodu, przypisywany komunikat powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu hello sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="a007e-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="a007e-152">Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="a007e-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="a007e-153">Zmień hello zawartość komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="a007e-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="a007e-154">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello przez wywołanie metody **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="a007e-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="a007e-155">Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji.</span><span class="sxs-lookup"><span data-stu-id="a007e-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="a007e-156">powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i ustawia tooextend limitu czasu widoczności hello kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="a007e-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="a007e-157">Zapisuje stan pracy, który został skojarzony z wiadomość hello hello i udostępnia innym toocontinue minuty pracy na wiadomość powitania powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a007e-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="a007e-158">Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="a007e-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="a007e-159">Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="a007e-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="a007e-160">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="a007e-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="a007e-161">Dodatkowe opcje usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="a007e-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="a007e-162">Istnieją dwa sposoby, który można dostosować pobieranie wiadomości z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a007e-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="a007e-163">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="a007e-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="a007e-164">Po drugie można ustawić widoczności dłuższy lub krótszy limit czasu, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a007e-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="a007e-165">Witaj poniższy przykład kodu wykorzystuje hello **getMessages** metody tooget 16 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a007e-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="a007e-166">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="a007e-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="a007e-167">Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a007e-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="a007e-168">Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="a007e-168">Get queue length</span></span>
<span data-ttu-id="a007e-169">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a007e-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="a007e-170">Witaj **QueueRestProxy -> getQueueMetadata** — metoda zadaje hello kolejki usługi tooreturn metadane dotyczące hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="a007e-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="a007e-171">Wywoływanie hello **getApproximateMessageCount** metody na powitania zwrócony obiekt zawiera liczbę liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a007e-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="a007e-172">Liczba Hello jest tylko przybliżonej, ponieważ komunikaty mogą dodane lub usunięte po hello kolejki usługa odpowiada tooyour żądania.</span><span class="sxs-lookup"><span data-stu-id="a007e-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="a007e-173">Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="a007e-173">Delete a queue</span></span>
<span data-ttu-id="a007e-174">toodelete kolejkę i wszystkie wiadomości powitania w ramach tego wywołania hello **QueueRestProxy -> deleteQueue** metody.</span><span class="sxs-lookup"><span data-stu-id="a007e-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a007e-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a007e-175">Next steps</span></span>
<span data-ttu-id="a007e-176">Teraz, kiedy znasz już podstawy magazynu kolejek Azure hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu:</span><span class="sxs-lookup"><span data-stu-id="a007e-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="a007e-177">Odwiedź hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="a007e-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="a007e-178">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a007e-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

