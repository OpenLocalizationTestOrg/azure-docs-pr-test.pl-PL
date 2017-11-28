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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="547a3-103">Jak toouse usługi Service Bus tematów i subskrypcji za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="547a3-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="547a3-104">W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="547a3-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="547a3-105">Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="547a3-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="547a3-106">Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="547a3-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="547a3-107">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="547a3-107">Create a PHP application</span></span>
<span data-ttu-id="547a3-108">Witaj wymaganie służący do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure Blob hello jest tooreference klas w hello tylko [zestaw Azure SDK for PHP](../php-download-sdk.md) od w kodzie.</span><span class="sxs-lookup"><span data-stu-id="547a3-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="547a3-109">Można użyć dowolnego toocreate narzędzi rozwoju, aplikacji lub Notatnik.</span><span class="sxs-lookup"><span data-stu-id="547a3-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="547a3-110">Instalację PHP musi mieć również hello [rozszerzenie biblioteki OpenSSL](http://php.net/openssl) zainstalowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="547a3-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="547a3-111">W tym artykule opisano, jak toouse usługi funkcji, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="547a3-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="547a3-112">Pobierz hello bibliotek klienta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="547a3-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="547a3-113">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="547a3-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="547a3-114">Witaj toouse interfejsów API usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="547a3-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="547a3-115">Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] [ require-once] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="547a3-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="547a3-116">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="547a3-116">Reference any classes you might use.</span></span>

<span data-ttu-id="547a3-117">Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServiceBusService** klasy.</span><span class="sxs-lookup"><span data-stu-id="547a3-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="547a3-118">W tym przykładzie (i inne przykłady w tym artykule) przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="547a3-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="547a3-119">Jeśli zainstalowano bibliotek hello ręcznie lub jako pakiet GRUSZKOWA, musi odwoływać się hello **WindowsAzure.php** automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="547a3-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="547a3-120">W następujących przykładach hello, hello `require_once` instrukcji są zawsze wyświetlane, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="547a3-121">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="547a3-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="547a3-122">tooinstantiate klienta usługi Service Bus, należy najpierw mają prawidłowe parametry połączenia w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="547a3-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="547a3-123">Gdzie `Endpoint` ma zazwyczaj hello format `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="547a3-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="547a3-124">toocreate dowolnego klienta usługi Azure, należy użyć hello `ServicesBuilder` klasy.</span><span class="sxs-lookup"><span data-stu-id="547a3-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="547a3-125">Możesz:</span><span class="sxs-lookup"><span data-stu-id="547a3-125">You can:</span></span>

* <span data-ttu-id="547a3-126">Przekaż połączenia hello ciągu bezpośrednio tooit.</span><span class="sxs-lookup"><span data-stu-id="547a3-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="547a3-127">Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="547a3-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="547a3-128">Domyślnie pochodzi on z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="547a3-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="547a3-129">Można dodać nowych źródeł, rozszerzając hello `ConnectionStringSource` klasy.</span><span class="sxs-lookup"><span data-stu-id="547a3-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="547a3-130">Przykłady hello opisana w tym temacie ciąg połączenia hello jest przekazywany bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="547a3-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="547a3-131">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="547a3-131">Create a topic</span></span>
<span data-ttu-id="547a3-132">Mogą wykonywać operacje zarządzania dla tematów usługi Service Bus za pośrednictwem hello `ServiceBusRestProxy` klasy.</span><span class="sxs-lookup"><span data-stu-id="547a3-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="547a3-133">A `ServiceBusRestProxy` obiekt jest tworzony za pomocą hello `ServicesBuilder::createServiceBusService` metoda fabryki z ciąg odpowiednie połączenie, który hermetyzuje hello tokenu uprawnienia toomanage go.</span><span class="sxs-lookup"><span data-stu-id="547a3-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="547a3-134">powitania po przykładzie pokazano, jak tooinstantiate `ServiceBusRestProxy` i Wywołaj `ServiceBusRestProxy->createTopic` toocreate temat o nazwie `mytopic` w `MySBNamespace` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="547a3-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="547a3-135">Można użyć hello `listTopics` metoda `ServiceBusRestProxy` obiekty toocheck, jeśli temat o określonej nazwie już istnieje w przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="547a3-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="547a3-136">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="547a3-136">Create a subscription</span></span>
<span data-ttu-id="547a3-137">Subskrypcje tematu są również tworzone za pomocą hello `ServiceBusRestProxy->createSubscription` metody.</span><span class="sxs-lookup"><span data-stu-id="547a3-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="547a3-138">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji toohello hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="547a3-139">Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="547a3-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="547a3-140">Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="547a3-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="547a3-141">Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="547a3-142">Witaj poniższy przykład tworzy subskrypcję o nazwie "mysubscription" i używa hello domyślne **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="547a3-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="547a3-143">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="547a3-143">Create subscriptions with filters</span></span>
<span data-ttu-id="547a3-144">Można również skonfigurować filtry, które pozwalają toospecify wysyłane wiadomości, które tooa tematu powinny pojawić się w ramach subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="547a3-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="547a3-145">Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="547a3-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="547a3-146">Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="547a3-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="547a3-147">Aby uzyskać więcej informacji o SqlFilters, zobacz [właściwości SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="547a3-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="547a3-148">Każda reguła w przypadku subskrypcji przetwarza wiadomości przychodzących niezależnie, dodawanie subskrypcji toohello wiadomości ich wyników.</span><span class="sxs-lookup"><span data-stu-id="547a3-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="547a3-149">Ponadto każda nowa subskrypcja ma wartość domyślną **reguły** obiektu filtr, który dodaje wszystkie komunikaty z subskrypcji toohello tematu hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="547a3-150">tylko komunikaty tooreceive zgodny z filtrem, należy usunąć hello reguły domyślnej.</span><span class="sxs-lookup"><span data-stu-id="547a3-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="547a3-151">Można usunąć reguły domyślnej hello przy użyciu hello `ServiceBusRestProxy->deleteRule` metody.</span><span class="sxs-lookup"><span data-stu-id="547a3-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="547a3-152">Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `MessageNumber` właściwości wyższej niż 3.</span><span class="sxs-lookup"><span data-stu-id="547a3-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="547a3-153">Zobacz [wysyłania wiadomości tooa tematu](#send-messages-to-a-topic) informacji o dodawaniu toomessages właściwości niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="547a3-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="547a3-154">Należy pamiętać, że ten kod wymaga użycia hello dodatkowe przestrzeni nazw: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="547a3-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="547a3-155">Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z `SqlFilter` który wybiera tylko komunikaty, które mają `MessageNumber` właściwości mniejszą lub równą too3.</span><span class="sxs-lookup"><span data-stu-id="547a3-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="547a3-156">Teraz, gdy jest wysyłany komunikat toohello `mytopic` tematu, zawsze jest dostarczany toohello tooreceivers subskrybowane `mysubscription` subskrypcji i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` (subskrypcji w zależności od zawartości wiadomość hello).</span><span class="sxs-lookup"><span data-stu-id="547a3-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="547a3-157">Wysyłanie wiadomości tooa tematu</span><span class="sxs-lookup"><span data-stu-id="547a3-157">Send messages tooa topic</span></span>
<span data-ttu-id="547a3-158">toosend tematu usługi Service Bus tooa wiadomość hello wywołuje aplikacji `ServiceBusRestProxy->sendTopicMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="547a3-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="547a3-159">Witaj następującego kodu pokazuje sposób toosend toohello komunikat `mytopic` wcześniej utworzony w temacie `MySBNamespace` przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="547a3-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="547a3-160">Komunikaty wysyłane są tematy magistrali tooService wystąpień hello [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="547a3-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="547a3-161">[BrokeredMessage] [ BrokeredMessage] obiekty mają zestaw właściwości standardowych i metody, a także właściwości, które mogą być używane toohold niestandardowe właściwości specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="547a3-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="547a3-162">Witaj poniższy przykład przedstawia sposób testu toosend 5 wiadomości toohello `mytopic` wcześniej utworzony temat.</span><span class="sxs-lookup"><span data-stu-id="547a3-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="547a3-163">Witaj `setProperty` metoda jest używana tooadd właściwości niestandardowych (`MessageNumber`) tooeach wiadomości.</span><span class="sxs-lookup"><span data-stu-id="547a3-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="547a3-164">Należy pamiętać, że hello `MessageNumber` wartość właściwości może być różna dla każdej wiadomości (można użyć toodetermine tej wartości, które subskrypcji odbierania, jak pokazano w hello [Utwórz subskrypcję](#create-a-subscription) sekcji):</span><span class="sxs-lookup"><span data-stu-id="547a3-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="547a3-165">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="547a3-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="547a3-166">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="547a3-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="547a3-167">Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="547a3-168">Ta górny limit na rozmiar tematu jest 5 GB.</span><span class="sxs-lookup"><span data-stu-id="547a3-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="547a3-169">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="547a3-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="547a3-170">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="547a3-170">Receive messages from a subscription</span></span>
<span data-ttu-id="547a3-171">wiadomości powitania od tooreceive najlepsze sposób z subskrypcji jest toouse `ServiceBusRestProxy->receiveSubscriptionMessage` metody.</span><span class="sxs-lookup"><span data-stu-id="547a3-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="547a3-172">Mogą być odbierane wiadomości w dwóch różnych trybach: [ *ReceiveAndDelete* i *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="547a3-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="547a3-173">**PeekLock** jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="547a3-174">Korzystając z hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) trybie odbieranie jest operacją pojedynczego zrzutu; oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu w subskrypcji, oznacza hello komunikat jako wykorzystany i zwraca go toohello aplikacja.</span><span class="sxs-lookup"><span data-stu-id="547a3-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="547a3-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="547a3-176">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="547a3-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="547a3-177">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="547a3-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="547a3-178">W domyślnej hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb odbieraniu wiadomości staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="547a3-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="547a3-179">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="547a3-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="547a3-180">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania procesu przez przekazanie wiadomość hello Odebrano zbyt`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="547a3-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="547a3-181">Kiedy Usługa Service Bus widzi hello `deleteMessage` wywołania spowoduje oznaczenie hello komunikat jako wykorzystany i usunąć go z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="547a3-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="547a3-182">powitania po przykładzie pokazano, jak tooreceive i przetwarza komunikat przy użyciu [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (tryb domyślny hello).</span><span class="sxs-lookup"><span data-stu-id="547a3-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="547a3-183">Porady: Obsługa awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="547a3-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="547a3-184">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="547a3-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="547a3-185">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na wiadomość powitania odebranych (zamiast hello `deleteMessage` metody).</span><span class="sxs-lookup"><span data-stu-id="547a3-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="547a3-186">Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="547a3-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="547a3-187">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="547a3-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="547a3-188">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="547a3-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="547a3-189">Jest to często nazywane *co najmniej raz* przetwarzania; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="547a3-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="547a3-190">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tooapplications toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="547a3-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="547a3-191">Jest to często osiągane przy użyciu hello `getMessageId` metody wiadomość hello, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="547a3-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="547a3-192">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="547a3-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="547a3-193">toodelete tematu lub subskrypcji, użyj hello `ServiceBusRestProxy->deleteTopic` lub hello `ServiceBusRestProxy->deleteSubscripton` metod, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="547a3-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="547a3-194">Należy pamiętać, że usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.</span><span class="sxs-lookup"><span data-stu-id="547a3-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="547a3-195">Witaj poniższy przykład przedstawia sposób toodelete temat o nazwie `mytopic` i jego zarejestrowanych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="547a3-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="547a3-196">Za pomocą hello `deleteSubscription` metody, można usunąć subskrypcję niezależnie:</span><span class="sxs-lookup"><span data-stu-id="547a3-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="547a3-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="547a3-197">Next steps</span></span>
<span data-ttu-id="547a3-198">Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejki, tematy i subskrypcje] [ Queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="547a3-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
