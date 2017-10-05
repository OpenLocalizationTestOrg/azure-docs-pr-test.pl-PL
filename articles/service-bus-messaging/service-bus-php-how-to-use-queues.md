---
title: "Jak używać kolejek usługi Service Bus za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać kolejek usługi Service Bus na platformie Azure. Przykłady kodu napisane w języku PHP."
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
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="87019-104">Jak używać kolejek usługi Service Bus za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="87019-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="87019-105">Ten przewodnik przedstawia, jak używać kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="87019-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="87019-106">Przykłady są napisane w PHP i użyj [zestaw Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="87019-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="87019-107">Omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="87019-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="87019-108">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="87019-108">Create a PHP application</span></span>
<span data-ttu-id="87019-109">Jedynym wymaganiem dla tworzenia aplikacji PHP, który uzyskuje dostęp do usługi obiektów Blob platformy Azure jest odwołanie do klasy w [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie.</span><span class="sxs-lookup"><span data-stu-id="87019-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="87019-110">Można użyć narzędzia do programowania do tworzenia aplikacji, lub Notatnik.</span><span class="sxs-lookup"><span data-stu-id="87019-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="87019-111">Instalację PHP musi mieć również [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="87019-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="87019-112">W tym przewodniku użyje funkcji usługi, które mogą być wywoływane w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="87019-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="87019-113">Pobierz klienta usługi Azure bibliotek</span><span class="sxs-lookup"><span data-stu-id="87019-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="87019-114">Skonfigurować aplikację do użycia z magistralą usług</span><span class="sxs-lookup"><span data-stu-id="87019-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="87019-115">Aby korzystać z kolejki usługi Service Bus interfejsów API, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87019-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="87019-116">Odwołanie przy użyciu pliku automatycznej ładowarki [require_once] [ require_once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="87019-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="87019-117">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="87019-117">Reference any classes you might use.</span></span>

<span data-ttu-id="87019-118">Poniższy przykład pokazuje, jak dołączyć plik automatycznej ładowarki i odwołanie `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="87019-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="87019-119">W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="87019-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="87019-120">Jeśli zainstalowano bibliotek ręcznie lub jako pakiet GRUSZKOWA, należy wskazać **WindowsAzure.php** automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="87019-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="87019-121">W poniższych przykładach `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko do klas, które są konieczne na przykład do wykonania.</span><span class="sxs-lookup"><span data-stu-id="87019-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="87019-122">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="87019-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="87019-123">Można utworzyć klienta usługi Service Bus, najpierw musi mieć prawidłowe parametry połączenia w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="87019-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="87019-124">Gdzie `Endpoint` ma zazwyczaj format `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="87019-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="87019-125">Aby utworzyć dowolnego klienta usługi Azure, należy użyć `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="87019-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="87019-126">Możesz:</span><span class="sxs-lookup"><span data-stu-id="87019-126">You can:</span></span>

* <span data-ttu-id="87019-127">Parametry połączenia należy przekazać bezpośrednio do niego.</span><span class="sxs-lookup"><span data-stu-id="87019-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="87019-128">Użyj **CloudConfigurationManager (CCM)** do sprawdzenia wiele źródeł zewnętrznych ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="87019-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="87019-129">Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="87019-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="87019-130">Można dodać nowego źródła rozszerzając `ConnectionStringSource` — klasa</span><span class="sxs-lookup"><span data-stu-id="87019-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="87019-131">Przykłady przedstawione w tym miejscu ciąg połączenia jest przekazywany bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="87019-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="87019-132">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="87019-132">Create a queue</span></span>
<span data-ttu-id="87019-133">Mogą wykonywać operacje zarządzania kolejkami usługi Service Bus za pośrednictwem `ServiceBusRestProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="87019-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="87019-134">A `ServiceBusRestProxy` obiekt jest tworzony za pomocą `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje tokenu uprawnieniami do zarządzania nim.</span><span class="sxs-lookup"><span data-stu-id="87019-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="87019-135">Poniższy przykład przedstawia sposób tworzenia wystąpienia `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createQueue` utworzyć kolejkę o nazwie `myqueue` w `MySBNamespace` przestrzeni nazw usługi:</span><span class="sxs-lookup"><span data-stu-id="87019-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="87019-136">Można użyć `listQueues` metoda `ServiceBusRestProxy` obiektów, aby sprawdzić, czy kolejka o określonej nazwie już istnieje w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="87019-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="87019-137">Wysyłanie komunikatów do kolejki</span><span class="sxs-lookup"><span data-stu-id="87019-137">Send messages to a queue</span></span>
<span data-ttu-id="87019-138">Aby wysłać wiadomość do kolejki usługi Service Bus, wywołania aplikacji `ServiceBusRestProxy->sendQueueMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="87019-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="87019-139">Poniższy kod przedstawia sposób wysłania komunikatu do `myqueue` kolejki utworzonej wcześniej w `MySBNamespace` przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="87019-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="87019-140">Komunikaty wysłane do (i odebrane z) usługi Service Bus kolejki są wystąpieniami klasy [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="87019-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="87019-141">[BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw standardowych metod i właściwości, które są używane do przechowywania niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87019-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="87019-142">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="87019-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="87019-143">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="87019-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="87019-144">Nie ma żadnego limitu liczby komunikatów w kolejce, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez kolejkę.</span><span class="sxs-lookup"><span data-stu-id="87019-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="87019-145">Ta górny limit na rozmiar kolejki wynosi 5 GB.</span><span class="sxs-lookup"><span data-stu-id="87019-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="87019-146">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="87019-146">Receive messages from a queue</span></span>

<span data-ttu-id="87019-147">Najlepszym sposobem na odbieranie komunikatów z kolejki jest użycie `ServiceBusRestProxy->receiveQueueMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="87019-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="87019-148">Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) i [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="87019-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="87019-149">Ustawienie domyślne to **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="87019-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="87019-150">Korzystając z [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) trybie odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w kolejce, oznacza komunikat jako wykorzystany i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87019-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="87019-151">Tryb [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) jest najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="87019-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="87019-152">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="87019-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="87019-153">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="87019-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="87019-154">W domyślnej [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) tryb odbieraniu wiadomości staje się operacją dwuetapowy, co umożliwia obsługę aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="87019-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="87019-155">Kiedy Usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go, aby uniemożliwić innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87019-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="87019-156">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez przekazanie odebranego komunikatu do `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="87019-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="87019-157">Kiedy Usługa Service Bus widzi `deleteMessage` wywołania spowoduje oznaczenie komunikat jako wykorzystany i usunąć go z kolejki.</span><span class="sxs-lookup"><span data-stu-id="87019-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="87019-158">Poniższy przykład przedstawia sposób odbierały i przetwarzały komunikat przy użyciu [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (tryb domyślny).</span><span class="sxs-lookup"><span data-stu-id="87019-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="87019-159">Sposób obsługi awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="87019-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="87019-160">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="87019-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="87019-161">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać `unlockMessage` metody dla odebranego komunikatu (zamiast `deleteMessage` metody).</span><span class="sxs-lookup"><span data-stu-id="87019-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="87019-162">Spowoduje to odblokowanie komunikatu w kolejce i udostępnienie go do ponownego odbioru, przez tę samą lub inną odbierającą aplikację usługę Service Bus.</span><span class="sxs-lookup"><span data-stu-id="87019-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="87019-163">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady wygaśnięcia (na przykład jeśli wystąpiła awaria aplikacji), Usługa Service Bus zostanie automatycznie odblokowanie komunikatu i stał się dostępny do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="87019-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="87019-164">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem `deleteMessage` żądania, a następnie komunikat zostanie dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="87019-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="87019-165">Jest to często nazywane *co najmniej raz* oznacza to, że przetwarzanie; każdy komunikat jest przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="87019-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="87019-166">Jeśli scenariusz nie Toleruje dwukrotnego przetwarzania, zaleca się następnie dodać dodatkową logikę do aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="87019-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="87019-167">Jest to często osiągane przy użyciu `getMessageId` — metoda, która pozostaje stała między kolejnymi próbami dostarczenia komunikatu.</span><span class="sxs-lookup"><span data-stu-id="87019-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87019-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87019-168">Next steps</span></span>
<span data-ttu-id="87019-169">Teraz, kiedy znasz już podstawy kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="87019-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="87019-170">Aby uzyskać więcej informacji, odwiedź również [Centrum deweloperów języka PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="87019-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


