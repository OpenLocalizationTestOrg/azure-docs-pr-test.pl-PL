---
title: "Jak używać tematów i subskrypcji Azure Service Bus za pomocą języka Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać tematów usługi Service Bus i subskrypcji platformy Azure z poziomu aplikacji Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="41370-103">Sposób użycia usługi Service Bus tematów i subskrypcji za pomocą języka Node.js</span><span class="sxs-lookup"><span data-stu-id="41370-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="41370-104">W tym przewodniku opisano, jak używać tematów usługi Service Bus i subskrypcji z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="41370-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="41370-105">Omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości** do tematu, **odbieranie komunikatów z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="41370-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="41370-106">Aby uzyskać więcej informacji o tematach i subskrypcjach, zobacz sekcję [Następne kroki](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="41370-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="41370-107">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="41370-107">Create a Node.js application</span></span>
<span data-ttu-id="41370-108">Utwórz pustą aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="41370-108">Create a blank Node.js application.</span></span> <span data-ttu-id="41370-109">Instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie aplikacji Node.js do witryny sieci Web Azure], [usługi w chmurze Node.js] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell lub witryny sieci Web za pomocą programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="41370-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="41370-110">Skonfigurować aplikację do użycia z magistralą usług</span><span class="sxs-lookup"><span data-stu-id="41370-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="41370-111">Aby korzystać z usługi Service Bus, Pobierz pakiet Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="41370-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="41370-112">Ten pakiet zawiera zestaw bibliotek, które komunikują się z usługi Service Bus REST.</span><span class="sxs-lookup"><span data-stu-id="41370-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="41370-113">Umożliwia uzyskanie pakietu węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="41370-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="41370-114">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu, w którym utworzono przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41370-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="41370-115">Typ **azure instalacji narzędzia npm** w oknie wiersza polecenia, co powinno spowodować następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="41370-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="41370-116">Możesz ręcznie uruchomić **ls** polecenie, aby sprawdzić, czy **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="41370-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="41370-117">W tym folderze znaleźć **azure** pakiet, który zawiera biblioteki, musisz mieć dostęp tematów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="41370-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="41370-118">Zaimportuj moduł</span><span class="sxs-lookup"><span data-stu-id="41370-118">Import the module</span></span>
<span data-ttu-id="41370-119">Za pomocą Notatnika lub innego edytora tekstu, Dodaj następujący element do góry **server.js** pliku aplikacji:</span><span class="sxs-lookup"><span data-stu-id="41370-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="41370-120">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="41370-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="41370-121">Moduł Azure odczytuje zmiennych środowiskowych `AZURE_SERVICEBUS_NAMESPACE` i `AZURE_SERVICEBUS_ACCESS_KEY` informacje wymagane do nawiązania połączenia usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="41370-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="41370-122">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie podczas wywoływania metody `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="41370-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="41370-123">Na przykład ustawienia zmiennych środowiskowych dla usługi w chmurze platformy Azure, zobacz [Node.js usługi chmury z magazynem][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="41370-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="41370-124">Na przykład ustawienia zmiennych środowiskowych dla witryny sieci Web platformy Azure, zobacz [aplikacji sieci Web Node.js z magazynem][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="41370-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="41370-125">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="41370-125">Create a topic</span></span>
<span data-ttu-id="41370-126">**ServiceBusService** obiektu umożliwia pracę z tematów.</span><span class="sxs-lookup"><span data-stu-id="41370-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="41370-127">Poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="41370-128">Dodaj ją w górnej części **server.js** pliku po instrukcji, aby zaimportować moduł azure:</span><span class="sxs-lookup"><span data-stu-id="41370-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="41370-129">Wywołując `createTopicIfNotExists` na **ServiceBusService** obiektu określonego tematu zostanie zwrócony (jeśli istnieje) lub zostanie utworzony nowy temat o określonej nazwie.</span><span class="sxs-lookup"><span data-stu-id="41370-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="41370-130">Poniższy kod używa `createTopicIfNotExists` można utworzyć lub połączyć się z tematem o nazwie `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="41370-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="41370-131">`createServiceBusService` Metoda obsługuje również dodatkowe opcje, które umożliwiają zastąpienie domyślnych ustawień tematu, takie jak czas wygaśnięcia wiadomości lub temat maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="41370-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="41370-132">Poniższy przykład przedstawia rozmiar maksymalny tematu 5GB z czasem wygaśnięcia wynoszącym 1 minutę:</span><span class="sxs-lookup"><span data-stu-id="41370-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="41370-133">Filtry</span><span class="sxs-lookup"><span data-stu-id="41370-133">Filters</span></span>
<span data-ttu-id="41370-134">Opcjonalne operacjach filtrowania może odnosić się do operacji wykonywanych przy użyciu **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="41370-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="41370-135">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę o sygnaturze są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="41370-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="41370-136">Po wykonaniu przetwarzanie wstępne opcje żądania, wywołuje metodę `next`, przekazywanie wywołania zwrotnego z następującą sygnaturą:</span><span class="sxs-lookup"><span data-stu-id="41370-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="41370-137">W tym wywołania zwrotnego, a po zakończeniu przetwarzania `returnObject` (odpowiedzi z żądania do serwera), wywołania zwrotnego musi wywołać obok, jeśli istnieje kontynuować przetwarzanie inne filtry lub wywołać `finalCallback` w inny sposób, aby zakończyć wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="41370-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="41370-138">Dwa filtry, które implementują logikę ponawiania wchodzą w skład zestawu Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="41370-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="41370-139">Tworzy następujące **ServiceBusService** obiekt, który używa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="41370-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="41370-140">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="41370-140">Create subscriptions</span></span>
<span data-ttu-id="41370-141">Subskrypcje tematu są również tworzone za pomocą **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="41370-142">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych do wirtualnej kolejki subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="41370-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="41370-143">Subskrypcje są trwałe i będzie nadal istnieć do czasu albo lub temat są skojarzone z, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="41370-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="41370-144">Jeśli Twoja aplikacja logiki, aby utworzyć subskrypcję, go należy najpierw sprawdź, czy ta subskrypcja już istnieje przy użyciu `getSubscription` metody.</span><span class="sxs-lookup"><span data-stu-id="41370-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="41370-145">Tworzenie subskrypcji z filtrem domyślnym (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="41370-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="41370-146">Filtr **MatchAll** jest filtrem domyślnym, który jest używany, gdy podczas tworzenia nowej subskrypcji nie został określony żaden filtr.</span><span class="sxs-lookup"><span data-stu-id="41370-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="41370-147">Gdy **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane do tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="41370-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="41370-148">Poniższy przykład tworzy subskrypcję o nazwie "AllMessages" i używa domyślnej **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="41370-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="41370-149">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="41370-149">Create subscriptions with filters</span></span>
<span data-ttu-id="41370-150">Istnieje również możliwość utworzenia filtrów, które zezwalają na zakresu, które komunikaty wysyłane do tematu powinny być widoczne w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="41370-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="41370-151">Najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **SqlFilter**, która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="41370-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="41370-152">Filtry SQL działają na właściwościach komunikatów, które są publikowane do tematu.</span><span class="sxs-lookup"><span data-stu-id="41370-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="41370-153">Aby uzyskać więcej informacji na temat wyrażeń, które mogą być używane z filtrem SQL, przejrzyj [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.</span><span class="sxs-lookup"><span data-stu-id="41370-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="41370-154">Filtry można dodać do subskrypcji przy użyciu `createRule` metody **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="41370-155">Ta metoda umożliwia dodawanie nowych filtrów do istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="41370-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="41370-156">Ponieważ domyślnego filtru jest automatycznie stosowane do wszystkich nowych subskrypcji, należy najpierw usunąć domyślny filtr lub **MatchAll** zastępują inne filtry, można określić.</span><span class="sxs-lookup"><span data-stu-id="41370-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="41370-157">Należy usunąć domyślną regułę przy użyciu `deleteRule` metody **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="41370-158">Poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `messagenumber` właściwości wyższej niż 3:</span><span class="sxs-lookup"><span data-stu-id="41370-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="41370-159">Podobnie poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają `messagenumber` właściwości mniej niż 3:</span><span class="sxs-lookup"><span data-stu-id="41370-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="41370-160">Teraz wysłania komunikatu do `MyTopic`, zawsze zostanie dostarczona do odbiorców `AllMessages` subskrypcję tematu i selektywnie dostarczany do odbiorców mających subskrypcję `HighMessages` i `LowMessages` subskrypcje tematu (w zależności od zawartości komunikatu).</span><span class="sxs-lookup"><span data-stu-id="41370-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="41370-161">Sposób wysyłania komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="41370-161">How to send messages to a topic</span></span>
<span data-ttu-id="41370-162">Aby wysłać komunikat do tematu usługi Service Bus, aplikacja musi używać `sendTopicMessage` metody **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="41370-163">Komunikaty wysyłane do tematów usługi Service Bus są **BrokeredMessage** obiektów.</span><span class="sxs-lookup"><span data-stu-id="41370-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="41370-164">**BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `Label` i `TimeToLive`), słownik, który jest używany do przechowywania niestandardowych właściwości specyficzne dla aplikacji oraz treść danych ciągu.</span><span class="sxs-lookup"><span data-stu-id="41370-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="41370-165">Aplikacja możne ustawić treść komunikatu przez przekazanie wartości ciągu na `sendTopicMessage` i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="41370-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="41370-166">W poniższym przykładzie pokazano sposób wysyłania pięciu testowych komunikatów do `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="41370-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="41370-167">Należy pamiętać, że `messagenumber` wartość właściwości każdego komunikatu różni się w iteracji pętli (umożliwi to określenie subskrypcje, które go otrzymają):</span><span class="sxs-lookup"><span data-stu-id="41370-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="41370-168">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="41370-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="41370-169">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="41370-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="41370-170">Nie ma żadnego limitu liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez temat.</span><span class="sxs-lookup"><span data-stu-id="41370-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="41370-171">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="41370-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="41370-172">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="41370-172">Receive messages from a subscription</span></span>
<span data-ttu-id="41370-173">Komunikaty są odbierane z subskrypcją za pomocą `receiveSubscriptionMessage` metoda **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="41370-174">Domyślnie komunikaty są usuwane z subskrypcji one są w trybie do odczytu; można jednak odczytać (peek) i zablokować wiadomość bez usuwania go z subskrypcji, ustawiając parametr opcjonalny `isPeekLock` do **true**.</span><span class="sxs-lookup"><span data-stu-id="41370-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="41370-175">Domyślne zachowanie odczytywanie i usuwanie wiadomości w ramach operacji receive jest najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="41370-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="41370-176">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="41370-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="41370-177">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="41370-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="41370-178">Jeśli `isPeekLock` ustawiono parametr **true**, odbieranie staje się operacją dwuetapowy, co umożliwia obsługę aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="41370-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="41370-179">Gdy usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go w celu uniemożliwienia innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41370-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="41370-180">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez wywołanie metody **deleteMessage** — metoda i dostarczający komunikat, który ma zostać usunięty jako parametr.</span><span class="sxs-lookup"><span data-stu-id="41370-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="41370-181">**DeleteMessage** metoda będzie oznaczyć komunikat jako wykorzystany i usunąć go z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="41370-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="41370-182">W poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="41370-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="41370-183">Przykład otrzymuje najpierw i usuwa komunikat z subskrypcji "LowMessages" i otrzyma komunikat z subskrypcji "HighMessages" przy użyciu `isPeekLock` ustawioną na true.</span><span class="sxs-lookup"><span data-stu-id="41370-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="41370-184">Następnie usuwa komunikat przy użyciu `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="41370-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="41370-185">Sposób obsługi awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="41370-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="41370-186">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="41370-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="41370-187">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać `unlockMessage` metoda **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="41370-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="41370-188">Spowoduje to odblokowanie komunikatu w subskrypcji i udostępnienie go do ponownego odbioru, przez tę samą lub inną odbierającą aplikację usługę Service Bus.</span><span class="sxs-lookup"><span data-stu-id="41370-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="41370-189">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady wygaśnięcia (na przykład jeśli wystąpiła awaria aplikacji), Usługa Service Bus automatycznie odblokowuje komunikat i udostępnia go do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="41370-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="41370-190">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem `deleteMessage` metoda jest wywoływana, a następnie komunikat zostanie dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="41370-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="41370-191">Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="41370-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="41370-192">Jeśli scenariusz nie toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę do swojej aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="41370-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="41370-193">Jest to często osiągane przy użyciu **MessageId** właściwości wiadomości, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="41370-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="41370-194">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="41370-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="41370-195">Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte przez [portalu Azure] [ Azure portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="41370-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="41370-196">W poniższym przykładzie pokazano sposób usuwania tematu o nazwie `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="41370-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="41370-197">Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane z tematem.</span><span class="sxs-lookup"><span data-stu-id="41370-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="41370-198">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="41370-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="41370-199">Poniższy przykład przedstawia sposób usuwania subskrypcji o nazwie `HighMessages` z `MyTopic` tematu:</span><span class="sxs-lookup"><span data-stu-id="41370-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="41370-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41370-200">Next Steps</span></span>
<span data-ttu-id="41370-201">Teraz, kiedy znasz już podstawy tematów usługi Service Bus, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="41370-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="41370-202">Zobacz [kolejki, tematy i subskrypcje][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="41370-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="41370-203">Dokumentacja interfejsów API dla elementu [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="41370-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="41370-204">Odwiedź stronę [zestawu Azure SDK dla węzła] [ Azure SDK for Node] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="41370-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[tworzenie i wdrażanie aplikacji Node.js do witryny sieci Web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
