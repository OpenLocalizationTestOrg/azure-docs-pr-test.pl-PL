---
title: "kolejkuje toouse aaaHow usługi Service Bus za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kolejki toouse usługi Service Bus na platformie Azure. Przykłady kodu napisane w języku PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a>Jak kolejki usługi Service Bus toouse za pomocą języka PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

W tym przewodniku przedstawiono sposób toouse kolejek usługi Service Bus. Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP](../php-download-sdk.md). Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure Blob hello wymaganiem hello odwołuje się do klas w hello [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie. Można użyć dowolnego toocreate narzędzi rozwoju, aplikacji lub Notatnik.

> [!NOTE]
> Instalację PHP musi mieć również hello [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.
> 
> 

W tym przewodniku użyje funkcji usługi, które mogą być wywoływane w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-hello-azure-client-libraries"></a>Pobierz hello bibliotek klienta platformy Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
kolejki usługi Service Bus hello toouse interfejsów API, hello następujące:

1. Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require_once] instrukcji.
2. Odwoływać się do wszystkich klas, których może używać.

Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki `ServicesBuilder` klasy.

> [!NOTE]
> W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Jeśli zainstalowano bibliotek hello ręcznie lub jako pakiet GRUSZKOWA, musi odwoływać się hello **WindowsAzure.php** automatycznej ładowarki pliku.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

W poniższych przykładach hello, hello `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.

## <a name="set-up-a-service-bus-connection"></a>Skonfiguruj połączenie usługi Service Bus
tooinstantiate klienta usługi Service Bus, musisz najpierw mieć prawidłowe parametry połączenia w następującym formacie:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Gdzie `Endpoint` ma zazwyczaj hello format `[yourNamespace].servicebus.windows.net`.

toocreate dowolnego klienta usługi Azure, należy użyć hello `ServicesBuilder` klasy. Możesz:

* Przekaż połączenia hello ciągu bezpośrednio tooit.
* Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:
  * Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmienne środowiskowe
  * Można dodać nowych źródeł, rozszerzając hello `ConnectionStringSource` — klasa

Przykłady hello opisana w tym temacie ciąg połączenia hello jest przekazywany bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Tworzenie kolejki
Mogą wykonywać operacje zarządzania kolejkami usługi Service Bus za pośrednictwem hello `ServiceBusRestProxy` klasy. A `ServiceBusRestProxy` obiekt jest tworzony za pomocą hello `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje hello tokenu uprawnienia toomanage go.

powitania po przykładzie pokazano, jak tooinstantiate `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createQueue` toocreate kolejki o nazwie `myqueue` w `MySBNamespace` przestrzeni nazw usługi:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Można użyć hello `listQueues` metoda `ServiceBusRestProxy` obiekty toocheck, jeśli kolejka o określonej nazwie już istnieje w przestrzeni nazw.
> 
> 

## <a name="send-messages-tooa-queue"></a>Komunikaty tooa kolejki wysyłania
toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `ServiceBusRestProxy->sendQueueMessage` metody. Witaj następującego kodu pokazuje sposób toosend toohello komunikat `myqueue` kolejki utworzonej wcześniej w `MySBNamespace` przestrzeni nazw usługi.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Komunikaty wysłane za (i odebrane z) kolejek usługi Service Bus są wystąpieniami klasy hello [BrokeredMessage] [ BrokeredMessage] klasy. [BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw standardowych metod i właściwości, które są używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.

Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello. Ta górny limit na rozmiar kolejki wynosi 5 GB.

## <a name="receive-messages-from-a-queue"></a>Odbieranie komunikatów z kolejki

Witaj najlepsze sposób tooreceive wiadomości z kolejki jest toouse `ServiceBusRestProxy->receiveQueueMessage` metody. Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) i [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** jest domyślnym hello.

Korzystając z [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) trybie odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w kolejce, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

W domyślnej hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) tryb odbieraniu wiadomości staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Kiedy Usługa Service Bus odbiera żądanie, znajduje następny toobe wiadomość hello, używane, blokuje go tooprevent innym klientom odbieranie, a następnie zwrócenie go toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania procesu przez przekazanie wiadomość hello Odebrano zbyt`ServiceBusRestProxy->deleteMessage`. Kiedy Usługa Service Bus widzi hello `deleteMessage` wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.

powitania po przykładzie pokazano, jak tooreceive i przetwarza komunikat przy użyciu [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (tryb domyślny hello).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości

Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na wiadomość powitania odebranych (zamiast hello `deleteMessage` metody). Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *co najmniej raz* przetwarzania; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, a następnie dodanie dodatkowych logiki tooapplications toohandle dwukrotnego dostarczania komunikatów jest zalecane. Jest to często osiągane przy użyciu hello `getMessageId` metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.

Aby uzyskać więcej informacji, odwiedź również hello [Centrum deweloperów języka PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


