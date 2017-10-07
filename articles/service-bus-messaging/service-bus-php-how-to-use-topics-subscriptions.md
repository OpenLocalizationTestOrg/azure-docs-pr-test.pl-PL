---
title: "Tematy usługi Service Bus toouse aaaHow za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse tematów usługi Service Bus za pomocą języka PHP na platformie Azure."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Jak toouse usługi Service Bus tematów i subskrypcji za pomocą języka PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji. Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP](../php-download-sdk.md). Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Witaj wymaganie służący do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure Blob hello jest tooreference klas w hello tylko [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie. Można użyć dowolnego toocreate narzędzi rozwoju, aplikacji lub Notatnik.

> [!NOTE]
> Instalację PHP musi mieć również hello [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.
> 
> 

W tym artykule opisano, jak toouse usługi funkcji, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-hello-azure-client-libraries"></a>Pobierz hello bibliotek klienta platformy Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
Witaj toouse interfejsów API usługi Service Bus:

1. Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require-once] instrukcji.
2. Odwoływać się do wszystkich klas, których może używać.

Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServiceBusService** klasy.

> [!NOTE]
> W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Jeśli zainstalowano bibliotek hello ręcznie lub jako pakiet GRUSZKOWA, musi odwoływać się hello **WindowsAzure.php** automatycznej ładowarki pliku.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

W następujących przykładach hello, hello `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.

## <a name="set-up-a-service-bus-connection"></a>Skonfiguruj połączenie usługi Service Bus
tooinstantiate klienta usługi Service Bus, należy najpierw mają prawidłowe parametry połączenia w następującym formacie:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Gdzie `Endpoint` ma zazwyczaj hello format `https://[yourNamespace].servicebus.windows.net`.

toocreate dowolnego klienta usługi Azure, należy użyć hello `ServicesBuilder` klasy. Możesz:

* Przekaż połączenia hello ciągu bezpośrednio tooit.
* Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:
  * Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.
  * Można dodać nowych źródeł, rozszerzając hello `ConnectionStringSource` klasy.

Przykłady hello opisana w tym temacie ciąg połączenia hello jest przekazywany bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Tworzenie tematu
Mogą wykonywać operacje zarządzania dla tematów usługi Service Bus za pośrednictwem hello `ServiceBusRestProxy` klasy. A `ServiceBusRestProxy` obiekt jest tworzony za pomocą hello `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje hello tokenu uprawnienia toomanage go.

powitania po przykładzie pokazano, jak tooinstantiate `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createTopic` toocreate temat o nazwie `mytopic` w `MySBNamespace` przestrzeni nazw:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> Można użyć hello `listTopics` metoda `ServiceBusRestProxy` obiekty toocheck, jeśli temat o określonej nazwie już istnieje w przestrzeni nazw usługi.
> 
> 

## <a name="create-a-subscription"></a>Tworzenie subskrypcji
Subskrypcje tematu są również tworzone za pomocą hello `ServiceBusRestProxy->createSubscription` metody. Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji toohello hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello
Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji. Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello. Witaj poniższy przykład tworzy subskrypcję o nazwie "mysubscription" i używa hello domyślne **MatchAll** filtru.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a>Tworzenie subskrypcji z filtrami
Można również skonfigurować filtry, które pozwalają toospecify wysyłane wiadomości, które tooa tematu powinny pojawić się w ramach subskrypcji określonego tematu. Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), która implementuje podzbiór standardu SQL92. Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu. Aby uzyskać więcej informacji o SqlFilters, zobacz [właściwości SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Każda reguła w przypadku subskrypcji przetwarza wiadomości przychodzących niezależnie, dodawanie subskrypcji toohello wiadomości ich wyników. Ponadto każda nowa subskrypcja ma wartość domyślną **reguły** obiektu filtr, który dodaje wszystkie komunikaty z subskrypcji toohello tematu hello. tylko komunikaty tooreceive zgodny z filtrem, należy usunąć hello reguły domyślnej. Można usunąć reguły domyślnej hello przy użyciu hello `ServiceBusRestProxy->deleteRule` metody.
> 
> 

Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `MessageNumber` właściwości wyższej niż 3. Zobacz [wysyłania wiadomości tooa tematu](#send-messages-to-a-topic) informacji o dodawaniu toomessages właściwości niestandardowych.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Należy pamiętać, że ten kod wymaga użycia hello dodatkowe przestrzeni nazw: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z `SqlFilter` który wybiera tylko komunikaty, które mają `MessageNumber` właściwości mniejszą lub równą too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Teraz, gdy jest wysyłany komunikat toohello `mytopic` tematu, zawsze jest dostarczany toohello tooreceivers subskrybowane `mysubscription` subskrypcji i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` (subskrypcji w zależności od zawartości wiadomość hello).

## <a name="send-messages-tooa-topic"></a>Wysyłanie wiadomości tooa tematu
toosend tematu usługi Service Bus tooa wiadomość hello wywołuje aplikacji `ServiceBusRestProxy->sendTopicMessage` metody. Witaj następującego kodu pokazuje sposób toosend toohello komunikat `mytopic` wcześniej utworzony w temacie `MySBNamespace` przestrzeni nazw usługi.

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

Komunikaty wysyłane są tematy magistrali tooService wystąpień hello [BrokeredMessage] [ BrokeredMessage] klasy. [BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw właściwości standardowych i metody, a także właściwości, które mogą być używane toohold niestandardowe właściwości specyficzne dla aplikacji. Witaj poniższy przykład przedstawia sposób testu toosend 5 wiadomości toohello `mytopic` wcześniej utworzony temat. Witaj `setProperty` metoda jest używana tooadd właściwości niestandardowych (`MessageNumber`) tooeach wiadomości. Należy pamiętać, że hello `MessageNumber` wartość właściwości może być różna dla każdej wiadomości (można użyć toodetermine tej wartości, które subskrypcji odbierania, jak pokazano w hello [Utwórz subskrypcję](#create-a-subscription) sekcji):

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello. Ta górny limit na rozmiar tematu jest 5 GB. Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
wiadomości powitania od tooreceive najlepsze sposób z subskrypcji jest toouse `ServiceBusRestProxy->receiveSubscriptionMessage` metody. Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* i *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** jest domyślnym hello.

Korzystając z hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) trybie odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w subskrypcji, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacja. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

W domyślnej hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb odbieraniu wiadomości staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania procesu przez przekazanie wiadomość hello Odebrano zbyt`ServiceBusRestProxy->deleteMessage`. Kiedy Usługa Service Bus widzi hello `deleteMessage` wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.

powitania po przykładzie pokazano, jak tooreceive i przetwarza komunikat przy użyciu [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (tryb domyślny hello). 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Porady: Obsługa awarii aplikacji i komunikatów niemożliwych do odczytania
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na wiadomość powitania odebranych (zamiast hello `deleteMessage` metody). Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *co najmniej raz* przetwarzania; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tooapplications toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello `getMessageId` metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.

## <a name="delete-topics-and-subscriptions"></a>Usuwanie tematów i subskrypcji
toodelete tematu lub subskrypcji, użyj hello `ServiceBusRestProxy->deleteTopic` lub hello `ServiceBusRestProxy->deleteSubscripton` metod, odpowiednio. Należy pamiętać, że usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.

Witaj poniższy przykład przedstawia sposób toodelete temat o nazwie `mytopic` i jego zarejestrowanych subskrypcji.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

Za pomocą hello `deleteSubscription` metody, można usunąć subskrypcję niezależnie:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
