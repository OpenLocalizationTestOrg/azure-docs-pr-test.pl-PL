---
title: "Jak używać tematów usługi Service Bus za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać tematów usługi Service Bus za pomocą języka PHP na platformie Azure."
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
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="7029b-103">Jak używać tematów usługi Service Bus i subskrypcji za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="7029b-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7029b-104">W tym artykule pokazano, jak używać tematów usługi Service Bus i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="7029b-105">Przykłady są napisane w PHP i użyj [zestaw Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7029b-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="7029b-106">Omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłanie komunikatów do tematu**, **odbieranie komunikatów z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="7029b-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="7029b-107">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="7029b-107">Create a PHP application</span></span>
<span data-ttu-id="7029b-108">Jedynym wymaganiem w przypadku tworzenia aplikacji PHP, który uzyskuje dostęp do usługi obiektów Blob platformy Azure jest odwoływać się do klas w [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7029b-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="7029b-109">Można użyć narzędzia do programowania do tworzenia aplikacji, lub Notatnik.</span><span class="sxs-lookup"><span data-stu-id="7029b-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="7029b-110">Instalację PHP musi mieć również [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="7029b-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="7029b-111">W tym artykule opisano sposób użycia funkcji usługi, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7029b-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="7029b-112">Pobierz klienta usługi Azure bibliotek</span><span class="sxs-lookup"><span data-stu-id="7029b-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="7029b-113">Skonfigurować aplikację do użycia z magistralą usług</span><span class="sxs-lookup"><span data-stu-id="7029b-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="7029b-114">Aby użyć interfejsów API usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="7029b-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="7029b-115">Odwołanie przy użyciu pliku automatycznej ładowarki [require_once] [ require-once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="7029b-116">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="7029b-116">Reference any classes you might use.</span></span>

<span data-ttu-id="7029b-117">Poniższy przykład pokazuje, jak dołączyć plik automatycznej ładowarki i odwołanie **ServiceBusService** klasy.</span><span class="sxs-lookup"><span data-stu-id="7029b-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="7029b-118">W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="7029b-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="7029b-119">Jeśli zainstalowano bibliotek ręcznie lub jako pakiet GRUSZKOWA, należy wskazać **WindowsAzure.php** automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="7029b-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="7029b-120">W poniższych przykładach `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko do klas, które są konieczne na przykład do wykonania.</span><span class="sxs-lookup"><span data-stu-id="7029b-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="7029b-121">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="7029b-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="7029b-122">Można utworzyć klienta usługi Service Bus, musisz najpierw mieć prawidłowe parametry połączenia w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7029b-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="7029b-123">Gdzie `Endpoint` ma zazwyczaj format `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7029b-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="7029b-124">Aby utworzyć dowolnego klienta usługi Azure, należy użyć `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="7029b-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="7029b-125">Możesz:</span><span class="sxs-lookup"><span data-stu-id="7029b-125">You can:</span></span>

* <span data-ttu-id="7029b-126">Parametry połączenia należy przekazać bezpośrednio do niego.</span><span class="sxs-lookup"><span data-stu-id="7029b-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="7029b-127">Użyj **CloudConfigurationManager (CCM)** do sprawdzenia wiele źródeł zewnętrznych ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="7029b-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="7029b-128">Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="7029b-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="7029b-129">Można dodać nowego źródła rozszerzając `ConnectionStringSource` klasy.</span><span class="sxs-lookup"><span data-stu-id="7029b-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="7029b-130">Przykłady przedstawione w tym miejscu ciąg połączenia jest przekazywany bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="7029b-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="7029b-131">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="7029b-131">Create a topic</span></span>
<span data-ttu-id="7029b-132">Mogą wykonywać operacje zarządzania dla tematów usługi Service Bus za pośrednictwem `ServiceBusRestProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="7029b-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="7029b-133">A `ServiceBusRestProxy` obiekt jest tworzony za pomocą `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje tokenu uprawnieniami do zarządzania nim.</span><span class="sxs-lookup"><span data-stu-id="7029b-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="7029b-134">Poniższy przykład przedstawia sposób tworzenia wystąpienia `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createTopic` utworzyć temat o nazwie `mytopic` w `MySBNamespace` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="7029b-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="7029b-135">Można użyć `listTopics` metoda `ServiceBusRestProxy` obiektów, aby sprawdzić, czy temat o określonej nazwie już istnieje w przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="7029b-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="7029b-136">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7029b-136">Create a subscription</span></span>
<span data-ttu-id="7029b-137">Subskrypcje tematu są również tworzone za pomocą `ServiceBusRestProxy->createSubscription` metody.</span><span class="sxs-lookup"><span data-stu-id="7029b-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="7029b-138">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="7029b-139">Tworzenie subskrypcji z filtrem domyślnym (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="7029b-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="7029b-140">Filtr **MatchAll** jest filtrem domyślnym, który jest używany, gdy podczas tworzenia nowej subskrypcji nie został określony żaden filtr.</span><span class="sxs-lookup"><span data-stu-id="7029b-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7029b-141">Gdy **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane do tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="7029b-142">Poniższy przykład tworzy subskrypcję o nazwie "mysubscription" i używa domyślnej **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="7029b-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7029b-143">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="7029b-143">Create subscriptions with filters</span></span>
<span data-ttu-id="7029b-144">Można również ustawiać filtry pozwalające określić, które komunikaty wysyłane do tematu powinny znajdować się w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="7029b-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="7029b-145">Najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="7029b-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="7029b-146">Filtry SQL działają na właściwościach komunikatów, które są publikowane do tematu.</span><span class="sxs-lookup"><span data-stu-id="7029b-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="7029b-147">Aby uzyskać więcej informacji o SqlFilters, zobacz [właściwości SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="7029b-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="7029b-148">Każda reguła w przypadku subskrypcji przetwarza wiadomości przychodzących niezależnie, dodanie ich wiadomości wynik do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="7029b-149">Ponadto każda nowa subskrypcja ma wartość domyślną **reguły** obiektu filtr, który dodaje wszystkie komunikaty z tematu do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="7029b-150">Aby otrzymywać tylko komunikaty zgodny z filtrem, należy usunąć reguły domyślnej.</span><span class="sxs-lookup"><span data-stu-id="7029b-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="7029b-151">Należy usunąć domyślną regułę przy użyciu `ServiceBusRestProxy->deleteRule` metody.</span><span class="sxs-lookup"><span data-stu-id="7029b-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="7029b-152">Poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `MessageNumber` właściwości wyższej niż 3.</span><span class="sxs-lookup"><span data-stu-id="7029b-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="7029b-153">Zobacz [wysyłanie komunikatów do tematu](#send-messages-to-a-topic) informacji o dodawanie właściwości niestandardowych do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7029b-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="7029b-154">Należy pamiętać, że ten kod wymaga użycia dodatkowej przestrzeni nazw: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="7029b-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="7029b-155">Podobnie poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z `SqlFilter` który wybiera tylko komunikaty, które mają `MessageNumber` właściwości mniej niż 3.</span><span class="sxs-lookup"><span data-stu-id="7029b-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="7029b-156">Teraz, gdy wiadomość jest wysyłana do `mytopic` tematu, zawsze jest dostarczany do odbiorców `mysubscription` subskrypcji i selektywnie dostarczany do odbiorców mających subskrypcję `HighMessages` i `LowMessages` subskrypcji (w zależności od zawartości komunikatu).</span><span class="sxs-lookup"><span data-stu-id="7029b-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="7029b-157">Wysyłanie komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="7029b-157">Send messages to a topic</span></span>
<span data-ttu-id="7029b-158">Aby wysłać komunikat do tematu usługi Service Bus, wywołania aplikacji `ServiceBusRestProxy->sendTopicMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="7029b-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="7029b-159">Poniższy kod przedstawia sposób wysłania komunikatu do `mytopic` wcześniej utworzony w temacie `MySBNamespace` przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="7029b-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="7029b-160">Komunikaty wysyłane do tematów usługi Service Bus są wystąpieniami klasy [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="7029b-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="7029b-161">[BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw właściwości standardowych i metody, a także właściwości, które mogą służyć do przechowywania niestandardowych właściwości specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7029b-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="7029b-162">Poniższy przykład przedstawia sposób wysłania 5 wiadomości testowe `mytopic` wcześniej utworzony temat.</span><span class="sxs-lookup"><span data-stu-id="7029b-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="7029b-163">`setProperty` Metoda jest używana do dodawania właściwości niestandardowych (`MessageNumber`) do każdej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7029b-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="7029b-164">Należy pamiętać, że `MessageNumber` wartość właściwości może być różna dla każdej wiadomości (tej wartości można użyć, aby określić, które subskrypcji odbierania, jak pokazano w [Utwórz subskrypcję](#create-a-subscription) sekcji):</span><span class="sxs-lookup"><span data-stu-id="7029b-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="7029b-165">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="7029b-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7029b-166">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="7029b-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7029b-167">Nie ma żadnego limitu liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez temat.</span><span class="sxs-lookup"><span data-stu-id="7029b-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="7029b-168">Ta górny limit na rozmiar tematu jest 5 GB.</span><span class="sxs-lookup"><span data-stu-id="7029b-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="7029b-169">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="7029b-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="7029b-170">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7029b-170">Receive messages from a subscription</span></span>
<span data-ttu-id="7029b-171">Najlepszym sposobem odbierania komunikatów z subskrypcji jest użycie `ServiceBusRestProxy->receiveSubscriptionMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="7029b-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="7029b-172">Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* i *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="7029b-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="7029b-173">Ustawienie domyślne to **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="7029b-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="7029b-174">W przypadku używania trybu [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) odbieranie jest operacją pojedynczego zrzutu. Oznacza to, że kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w subskrypcji, oznacza komunikat jako wykorzystywany i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7029b-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="7029b-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * tryb jest najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="7029b-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="7029b-176">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="7029b-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="7029b-177">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="7029b-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="7029b-178">W domyślnej [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb odbieraniu wiadomości staje się operacją dwuetapowy, co umożliwia obsługę aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7029b-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7029b-179">Gdy usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go w celu uniemożliwienia innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7029b-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="7029b-180">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez przekazanie odebranego komunikatu do `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="7029b-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="7029b-181">Kiedy Usługa Service Bus widzi `deleteMessage` wywołania spowoduje oznaczenie komunikat jako wykorzystany i usunąć go z kolejki.</span><span class="sxs-lookup"><span data-stu-id="7029b-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="7029b-182">Poniższy przykład przedstawia sposób odbierały i przetwarzały komunikat przy użyciu [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (tryb domyślny).</span><span class="sxs-lookup"><span data-stu-id="7029b-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7029b-183">Porady: Obsługa awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="7029b-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="7029b-184">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7029b-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7029b-185">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać `unlockMessage` metody dla odebranego komunikatu (zamiast `deleteMessage` metody).</span><span class="sxs-lookup"><span data-stu-id="7029b-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="7029b-186">Spowoduje to odblokowanie komunikatu w kolejce i udostępnienie go do ponownego odbioru, przez tę samą lub inną odbierającą aplikację usługę Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7029b-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7029b-187">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady wygaśnięcia (na przykład jeśli wystąpiła awaria aplikacji), Usługa Service Bus zostanie automatycznie odblokowanie komunikatu i stał się dostępny do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="7029b-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="7029b-188">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem `deleteMessage` żądania, a następnie komunikat zostanie dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="7029b-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="7029b-189">Jest to często nazywane *co najmniej raz* oznacza to, że przetwarzanie; każdy komunikat jest przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="7029b-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="7029b-190">Jeśli scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę do aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7029b-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="7029b-191">Jest to często osiągane przy użyciu `getMessageId` — metoda, która pozostaje stała między kolejnymi próbami dostarczenia komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7029b-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7029b-192">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7029b-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="7029b-193">Aby usunąć tematu lub subskrypcji, użyj `ServiceBusRestProxy->deleteTopic` lub `ServiceBusRestProxy->deleteSubscripton` metod, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7029b-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="7029b-194">Należy pamiętać, że usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane z tematem.</span><span class="sxs-lookup"><span data-stu-id="7029b-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="7029b-195">Poniższy przykład przedstawia sposób usuwania tematu o nazwie `mytopic` i jego zarejestrowanych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7029b-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="7029b-196">Za pomocą `deleteSubscription` metody, można usunąć subskrypcję niezależnie:</span><span class="sxs-lookup"><span data-stu-id="7029b-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="7029b-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7029b-197">Next steps</span></span>
<span data-ttu-id="7029b-198">Teraz, kiedy znasz już podstawy kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="7029b-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
