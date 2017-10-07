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
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="c2a09-104">Jak kolejki usługi Service Bus toouse za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="c2a09-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="c2a09-105">W tym przewodniku przedstawiono sposób toouse kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c2a09-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="c2a09-106">Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c2a09-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="c2a09-107">Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="c2a09-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="c2a09-108">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="c2a09-108">Create a PHP application</span></span>
<span data-ttu-id="c2a09-109">Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure Blob hello wymaganiem hello odwołuje się do klas w hello [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c2a09-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="c2a09-110">Można użyć dowolnego toocreate narzędzi rozwoju, aplikacji lub Notatnik.</span><span class="sxs-lookup"><span data-stu-id="c2a09-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="c2a09-111">Instalację PHP musi mieć również hello [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="c2a09-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="c2a09-112">W tym przewodniku użyje funkcji usługi, które mogą być wywoływane w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c2a09-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="c2a09-113">Pobierz hello bibliotek klienta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c2a09-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="c2a09-114">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="c2a09-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="c2a09-115">kolejki usługi Service Bus hello toouse interfejsów API, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c2a09-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="c2a09-116">Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require_once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="c2a09-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="c2a09-117">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="c2a09-117">Reference any classes you might use.</span></span>

<span data-ttu-id="c2a09-118">Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="c2a09-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="c2a09-119">W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="c2a09-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="c2a09-120">Jeśli zainstalowano bibliotek hello ręcznie lub jako pakiet GRUSZKOWA, musi odwoływać się hello **WindowsAzure.php** automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="c2a09-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="c2a09-121">W poniższych przykładach hello, hello `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.</span><span class="sxs-lookup"><span data-stu-id="c2a09-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="c2a09-122">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="c2a09-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="c2a09-123">tooinstantiate klienta usługi Service Bus, musisz najpierw mieć prawidłowe parametry połączenia w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="c2a09-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="c2a09-124">Gdzie `Endpoint` ma zazwyczaj hello format `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c2a09-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="c2a09-125">toocreate dowolnego klienta usługi Azure, należy użyć hello `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="c2a09-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="c2a09-126">Możesz:</span><span class="sxs-lookup"><span data-stu-id="c2a09-126">You can:</span></span>

* <span data-ttu-id="c2a09-127">Przekaż połączenia hello ciągu bezpośrednio tooit.</span><span class="sxs-lookup"><span data-stu-id="c2a09-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="c2a09-128">Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="c2a09-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="c2a09-129">Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="c2a09-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="c2a09-130">Można dodać nowych źródeł, rozszerzając hello `ConnectionStringSource` — klasa</span><span class="sxs-lookup"><span data-stu-id="c2a09-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="c2a09-131">Przykłady hello opisana w tym temacie ciąg połączenia hello jest przekazywany bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c2a09-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="c2a09-132">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="c2a09-132">Create a queue</span></span>
<span data-ttu-id="c2a09-133">Mogą wykonywać operacje zarządzania kolejkami usługi Service Bus za pośrednictwem hello `ServiceBusRestProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="c2a09-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="c2a09-134">A `ServiceBusRestProxy` obiekt jest tworzony za pomocą hello `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje hello tokenu uprawnienia toomanage go.</span><span class="sxs-lookup"><span data-stu-id="c2a09-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="c2a09-135">powitania po przykładzie pokazano, jak tooinstantiate `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createQueue` toocreate kolejki o nazwie `myqueue` w `MySBNamespace` przestrzeni nazw usługi:</span><span class="sxs-lookup"><span data-stu-id="c2a09-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="c2a09-136">Można użyć hello `listQueues` metoda `ServiceBusRestProxy` obiekty toocheck, jeśli kolejka o określonej nazwie już istnieje w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c2a09-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="c2a09-137">Komunikaty tooa kolejki wysyłania</span><span class="sxs-lookup"><span data-stu-id="c2a09-137">Send messages tooa queue</span></span>
<span data-ttu-id="c2a09-138">toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `ServiceBusRestProxy->sendQueueMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="c2a09-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="c2a09-139">Witaj następującego kodu pokazuje sposób toosend toohello komunikat `myqueue` kolejki utworzonej wcześniej w `MySBNamespace` przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="c2a09-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="c2a09-140">Komunikaty wysłane za (i odebrane z) kolejek usługi Service Bus są wystąpieniami klasy hello [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="c2a09-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="c2a09-141">[BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw standardowych metod i właściwości, które są używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2a09-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="c2a09-142">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="c2a09-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="c2a09-143">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="c2a09-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="c2a09-144">Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="c2a09-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="c2a09-145">Ta górny limit na rozmiar kolejki wynosi 5 GB.</span><span class="sxs-lookup"><span data-stu-id="c2a09-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="c2a09-146">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="c2a09-146">Receive messages from a queue</span></span>

<span data-ttu-id="c2a09-147">Witaj najlepsze sposób tooreceive wiadomości z kolejki jest toouse `ServiceBusRestProxy->receiveQueueMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="c2a09-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="c2a09-148">Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) i [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="c2a09-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="c2a09-149">**PeekLock** jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="c2a09-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="c2a09-150">Korzystając z [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) trybie odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w kolejce, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2a09-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="c2a09-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello.</span><span class="sxs-lookup"><span data-stu-id="c2a09-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="c2a09-152">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="c2a09-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="c2a09-153">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="c2a09-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="c2a09-154">W domyślnej hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) tryb odbieraniu wiadomości staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c2a09-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="c2a09-155">Kiedy Usługa Service Bus odbiera żądanie, znajduje następny toobe wiadomość hello, używane, blokuje go tooprevent innym klientom odbieranie, a następnie zwrócenie go toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2a09-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="c2a09-156">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania procesu przez przekazanie wiadomość hello Odebrano zbyt`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="c2a09-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="c2a09-157">Kiedy Usługa Service Bus widzi hello `deleteMessage` wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="c2a09-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="c2a09-158">powitania po przykładzie pokazano, jak tooreceive i przetwarza komunikat przy użyciu [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (tryb domyślny hello).</span><span class="sxs-lookup"><span data-stu-id="c2a09-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="c2a09-159">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="c2a09-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="c2a09-160">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="c2a09-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="c2a09-161">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na wiadomość powitania odebranych (zamiast hello `deleteMessage` metody).</span><span class="sxs-lookup"><span data-stu-id="c2a09-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="c2a09-162">Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="c2a09-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="c2a09-163">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="c2a09-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="c2a09-164">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="c2a09-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="c2a09-165">Jest to często nazywane *co najmniej raz* przetwarzania; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="c2a09-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="c2a09-166">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, a następnie dodanie dodatkowych logiki tooapplications toohandle dwukrotnego dostarczania komunikatów jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="c2a09-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="c2a09-167">Jest to często osiągane przy użyciu hello `getMessageId` metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="c2a09-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2a09-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2a09-168">Next steps</span></span>
<span data-ttu-id="c2a09-169">Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c2a09-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="c2a09-170">Aby uzyskać więcej informacji, odwiedź również hello [Centrum deweloperów języka PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c2a09-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


