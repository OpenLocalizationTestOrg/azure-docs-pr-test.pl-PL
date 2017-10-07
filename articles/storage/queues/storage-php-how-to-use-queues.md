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
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Jak toouse magazynu kolejek w języku PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure. Przykłady Hello są zapisywane za pomocą klasy z hello zestaw Windows SDK dla programu PHP. Witaj objęte usługą scenariusze obejmują Wstawianie, wgląd, pobieranie i usuwanie komunikatów kolejek, a także tworzenie i usuwanie kolejek.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do magazynu kolejek Azure to hello odwołuje się do klas z hello Azure SDK for PHP z w kodzie. Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.

W tym przewodniku użyje funkcji magazynu kolejek, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-hello-azure-client-libraries"></a>Pobierz bibliotek klienckich hello Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu kolejek
Witaj toouse interfejsów API magazynu kolejek Azure, musisz:

1. Odwołanie hello automatycznej ładowarki pliku przy użyciu hello [require_once] instrukcji.
2. Odwoływać się do wszystkich klas, których można użyć.

Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.

> [!NOTE]
> W tym przykładzie (i inne przykłady w tym artykule) zakłada zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Jeśli zainstalowano bibliotek hello ręcznie, trzeba będzie tooreference hello `WindowsAzure.php` automatycznej ładowarki pliku.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

W poniższych przykładach hello, hello `require_once` instrukcji będą wyświetlane zawsze, ale będzie można odwoływać się tylko klasy hello, które są niezbędne dla tooexecute przykład hello.

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
tooinstantiate klienta magazynu kolejek Azure, musisz najpierw mieć prawidłowe parametry połączenia. Witaj format dla parametrów połączenia usługi kolejki hello ma następującą składnię.

Aby uzyskać dostęp do usługi na żywo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Aby uzyskać dostęp do magazynu emulatora hello:

```php
UseDevelopmentStorage=true
```

toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy. Możesz użyć dowolnej z hello następujące techniki:

* Przekaż połączenia hello ciągu bezpośrednio tooit.
* Użyj **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:
  * Domyślnie, pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.
  * Można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** klasy.

Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Tworzenie kolejki
A **QueueRestProxy** obiekt umożliwia tworzenie kolejki przy użyciu hello **createQueue** metody. Podczas tworzenia kolejki, można ustawić opcje w kolejce hello, ale spowoduje to nie jest wymagane. (hello przykład poniżej przedstawiono, jak metadanych tooset dla kolejki.)

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
> Nie należy polegać na uwzględnianie wielkości liter w metadanych kluczy. Wszystkie klucze są odczytywane z usługi hello pisane małymi literami.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Dodaj tooa kolejki komunikatów
Użyj tooadd kolejkę komunikatów tooa **QueueRestProxy -> polecenie createMessage**. Metoda Hello przyjmuje nazwę kolejki hello, tekst wiadomości powitania i opcje wiadomości, (które są opcjonalne).

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

## <a name="peek-at-hello-next-message"></a>Wglądu dalej wiadomości powitania
Można uzyskać wgląd w komunikat (lub wiadomości) hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie metody **QueueRestProxy -> peekMessages**. Domyślnie program hello **peekMessage** metoda zwraca pojedynczą wiadomość, ale można zmienić tę wartość przy użyciu hello **PeekMessagesOptions -> setNumberOfMessages** metody.

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

## <a name="de-queue-hello-next-message"></a>Kolejka do następnej wiadomości powitania
Twój kod usuwa komunikat z kolejki w dwóch etapach. Najpierw należy wywołać **QueueRestProxy -> listMessages**, co czyni hello komunikat niewidoczne tooany innego kodu, który jest czytania z kolejki hello. Domyślnie ten komunikat pozostanie niewidoczny przez 30 sekund. (Jeśli wiadomość hello nie jest usuwany w tym okresie, stanie się widoczne w kolejce hello ponownie.) z kolejki hello wiadomość hello usuwania toofinish należy wywołać **QueueRestProxy -> deleteMessage**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy tooprocess kończy się niepowodzeniem z kodu, przypisywany komunikat powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu hello sam komunikat i spróbuj ponownie. Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu wiadomość hello.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Zmień hello zawartość komunikatu w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello przez wywołanie metody **QueueRestProxy -> updateMessage**. Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji. powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i ustawia tooextend limitu czasu widoczności hello kolejne 60 sekund. Zapisuje stan pracy, który został skojarzony z wiadomość hello hello i udostępnia innym toocontinue minuty pracy na wiadomość powitania powitania klienta. Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania. Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż  *n*  razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

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

## <a name="additional-options-for-de-queuing-messages"></a>Dodatkowe opcje usuwania komunikatów z kolejek
Istnieją dwa sposoby, który można dostosować pobieranie wiadomości z kolejki. Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić widoczności dłuższy lub krótszy limit czasu, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. Witaj poniższy przykład kodu wykorzystuje hello **getMessages** metody tooget 16 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu **dla** pętli. Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.

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

## <a name="get-queue-length"></a>Pobieranie długości kolejki
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. Witaj **QueueRestProxy -> getQueueMetadata** — metoda zadaje hello kolejki usługi tooreturn metadane dotyczące hello kolejki. Wywoływanie hello **getApproximateMessageCount** metody na powitania zwrócony obiekt zawiera liczbę liczbę wiadomości w kolejce. Liczba Hello jest tylko przybliżonej, ponieważ komunikaty mogą dodane lub usunięte po hello kolejki usługa odpowiada tooyour żądania.

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

## <a name="delete-a-queue"></a>Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania w ramach tego wywołania hello **QueueRestProxy -> deleteQueue** metody.

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

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek Azure hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu:

* Odwiedź hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

