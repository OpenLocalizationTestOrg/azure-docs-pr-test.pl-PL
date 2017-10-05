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
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a>Jak używać Magazynu kolejek w języku PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu kolejek Azure. Przykłady są zapisywane za pomocą klasy z zestawu Windows SDK dla programu PHP. Objęte usługą scenariusze obejmują, wstawianie, wgląd, pobieranie i usuwanie komunikatów kolejek, a także tworzenie i usuwanie kolejek.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Jedynym wymaganiem służący do tworzenia aplikacji PHP, który uzyskuje dostęp do magazynu kolejek Azure jest odwoływanie się do klasy z zestawu Azure SDK dla programu PHP z w kodzie. Narzędzia do programowania służy do tworzenia aplikacji, łącznie z Notatnika.

W tym przewodniku użyje funkcji magazynu kolejek, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-the-azure-client-libraries"></a>Pobierz bibliotek klienta platformy Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a>Konfigurowanie aplikacji dostęp do kolejki magazynu
Aby korzystanie z interfejsów API magazynu kolejek Azure, musisz:

1. Odwołanie do pliku automatycznej ładowarki przy użyciu [require_once] instrukcji.
2. Odwoływać się do wszystkich klas, których można użyć.

Poniższy przykład pokazuje, jak dołączyć plik automatycznej ładowarki i odwołanie **ServicesBuilder** klasy.

> [!NOTE]
> W tym przykładzie (i inne przykłady w tym artykule) zakłada zainstalowano bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Jeśli zainstalowano bibliotek ręcznie, konieczne będzie odwoływać się `WindowsAzure.php` automatycznej ładowarki pliku.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

W poniższych przykładach `require_once` instrukcji będą wyświetlane zawsze, ale będzie można odwoływać się tylko klasy, które są niezbędne, na przykład do wykonania.

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
Można utworzyć wystąpienia klienta magazynu kolejek Azure, najpierw musi mieć prawidłowe parametry połączenia. Format dla parametrów połączenia usługi kolejki ma następującą składnię.

Aby uzyskać dostęp do usługi na żywo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Aby uzyskać dostęp do emulatora magazynu:

```php
UseDevelopmentStorage=true
```

Aby utworzyć dowolnego klienta usługi Azure, musisz użyć **ServicesBuilder** klasy. Można użyć jednej z następujących metod:

* Parametry połączenia należy przekazać bezpośrednio do niego.
* Użyj **CloudConfigurationManager (CCM)** do sprawdzenia wiele źródeł zewnętrznych ciągu połączenia:
  * Domyślnie, pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.
  * Można dodać nowego źródła rozszerzając **ConnectionStringSource** klasy.

Przykłady przedstawione w tym miejscu parametry połączenia zostaną przekazane bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Tworzenie kolejki
A **QueueRestProxy** obiekt umożliwia tworzenie kolejki przy użyciu **createQueue** metody. Podczas tworzenia kolejki, można ustawić opcje w kolejce, ale spowoduje to nie jest wymagane. (W poniższym przykładzie pokazano, jak ustawić metadanych w kolejce).

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
> Nie należy polegać na uwzględnianie wielkości liter w metadanych kluczy. Wszystkie klucze są odczytywane z usługi pisane małymi literami.
> 
> 

## <a name="add-a-message-to-a-queue"></a>Dodaj komunikat do kolejki
Aby dodać wiadomości do kolejki, użyj **QueueRestProxy -> polecenie createMessage**. Metoda ma nazwę kolejki, tekst komunikatu i opcje wiadomości, (które są opcjonalne).

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

## <a name="peek-at-the-next-message"></a>Podgląd kolejnego komunikatu
Możesz uzyskać wgląd w komunikat (lub wiadomości) z przodu kolejki bez jego usuwania z kolejki, wywołując **QueueRestProxy -> peekMessages**. Domyślnie **peekMessage** metoda zwraca pojedynczą wiadomość, ale można zmienić tę wartość przy użyciu **PeekMessagesOptions -> setNumberOfMessages** metody.

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

## <a name="de-queue-the-next-message"></a>Usunięcie następnego komunikatu z kolejki
Twój kod usuwa komunikat z kolejki w dwóch etapach. Najpierw należy wywołać **QueueRestProxy -> listMessages**, która sprawia, że komunikat niewidoczne dla innego kodu, który jest czytania z kolejki. Domyślnie ten komunikat pozostanie niewidoczny przez 30 sekund. (Jeśli wiadomość nie jest usuwany w tym okresie, stanie się widoczna w kolejce ponownie.) Aby zakończyć usuwanie komunikatu z kolejki, należy wywołać **QueueRestProxy -> deleteMessage**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie może przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie. Twój kod wywołuje **deleteMessage** natychmiast po przetworzeniu komunikatu.

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

## <a name="change-the-contents-of-a-queued-message"></a>Zmiana zawartości komunikatu w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce przez wywołanie metody **QueueRestProxy -> updateMessage**. Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania. Poniższy kod aktualizuje komunikat kolejki o nową zawartość i Ustawia rozszerzenie limitu czasu widoczności kolejne 60 sekund. Zapisuje stan pracy, który został skojarzony z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad wiadomości. Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania. Zazwyczaj stosuje się również liczbę ponownych prób. Jeśli komunikat zostanie ponowiony więcej niż *n* razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

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
Istnieją dwa sposoby, który można dostosować pobieranie wiadomości z kolejki. Po pierwsze można uzyskać komunikaty zbiorczo (do 32). Po drugie można ustawić widoczności dłuższy lub krótszy limit czasu, dzięki czemu kod będzie bardziej lub mniej czasu na pełne przetworzenie każdego komunikatu. Poniższy przykład kodu wykorzystuje **getMessages** metodę, aby pobrać 16 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu **dla** pętli. Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.

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
Możesz uzyskać szacunkową liczbę komunikatów w kolejce. **QueueRestProxy -> getQueueMetadata** metody prosi usługę kolejki do zwracania metadanych dotyczących kolejki. Wywoływanie **getApproximateMessageCount** metody na zwracanym obiekcie zawiera liczbę liczbę wiadomości w kolejce. Wartość licznika jest tylko przybliżoną, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada na żądania.

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
Aby usunąć kolejkę i wszystkie znajdujące się w niej wiadomości, wywołaj **QueueRestProxy -> deleteQueue** metody.

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
Teraz, kiedy znasz już podstawy magazynu kolejek Azure, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu:

* Odwiedź stronę [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).

Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

