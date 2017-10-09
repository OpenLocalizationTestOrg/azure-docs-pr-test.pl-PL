---
title: "toouse aaaHow Azure Service Bus tematów i subskrypcji za pomocą języka Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Service Bus tematów i subskrypcji platformy Azure z poziomu aplikacji Node.js."
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="e7a95-103">Jak tooUse usługi Service Bus tematów i subskrypcji za pomocą języka Node.js</span><span class="sxs-lookup"><span data-stu-id="e7a95-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="e7a95-104">W tym przewodniku opisano sposób toouse usługi Service Bus tematów i subskrypcji z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="e7a95-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="e7a95-105">Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości** tematu tooa **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="e7a95-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="e7a95-106">Aby uzyskać więcej informacji o tematach i subskrypcjach, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="e7a95-107">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="e7a95-107">Create a Node.js application</span></span>
<span data-ttu-id="e7a95-108">Utwórz pustą aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="e7a95-108">Create a blank Node.js application.</span></span> <span data-ttu-id="e7a95-109">Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure], [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu systemu Windows Programu PowerShell lub witryny sieci Web za pomocą programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e7a95-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="e7a95-110">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="e7a95-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="e7a95-111">toouse usługi Service Bus, Pobierz hello Node.js Azure pakietu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="e7a95-112">Ten pakiet zawiera zestaw bibliotek, które komunikują się z usługi Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="e7a95-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="e7a95-113">Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="e7a95-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="e7a95-114">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu toohello, w której utworzono aplikację przykładową.</span><span class="sxs-lookup"><span data-stu-id="e7a95-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="e7a95-115">Typ **azure instalacji narzędzia npm** w oknie polecenia hello, co powinno spowodować hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e7a95-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="e7a95-116">Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="e7a95-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="e7a95-117">W tym folderze znaleźć **azure** pakiet, który zawiera biblioteki hello należy tooaccess tematów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e7a95-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="e7a95-118">Moduł hello importu</span><span class="sxs-lookup"><span data-stu-id="e7a95-118">Import hello module</span></span>
<span data-ttu-id="e7a95-119">Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="e7a95-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="e7a95-120">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="e7a95-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="e7a95-121">Hello Azure moduł odczytuje zmiennych środowiskowych hello `AZURE_SERVICEBUS_NAMESPACE` i `AZURE_SERVICEBUS_ACCESS_KEY` informacji wymaganych tooService tooconnect magistrali.</span><span class="sxs-lookup"><span data-stu-id="e7a95-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="e7a95-122">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="e7a95-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="e7a95-123">Na przykład ustawienia zmiennych środowiskowych powitania dla usługi w chmurze platformy Azure, zobacz [Node.js usługi chmury z magazynem][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="e7a95-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="e7a95-124">Na przykład ustawienia hello zmiennych środowiskowych dla witryny sieci Web platformy Azure, zobacz [aplikacji sieci Web Node.js z magazynem][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="e7a95-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="e7a95-125">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="e7a95-125">Create a topic</span></span>
<span data-ttu-id="e7a95-126">Witaj **ServiceBusService** obiektu umożliwia toowork z tematów.</span><span class="sxs-lookup"><span data-stu-id="e7a95-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="e7a95-127">Poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="e7a95-128">Dodaj ją w górnej części hello **server.js** pliku po hello instrukcji tooimport hello azure modułu:</span><span class="sxs-lookup"><span data-stu-id="e7a95-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="e7a95-129">Wywołując `createTopicIfNotExists` na powitania **ServiceBusService** obiekt hello określony temat zostanie zwrócony (jeśli istnieje) lub zostanie utworzony nowy temat o określonej nazwie hello.</span><span class="sxs-lookup"><span data-stu-id="e7a95-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="e7a95-130">Witaj poniższy kod używa `createTopicIfNotExists` toocreate lub łączenie toohello temat o nazwie `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="e7a95-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="e7a95-131">Witaj `createServiceBusService` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślny temat ustawienia, takie jak czas wygaśnięcia wiadomości lub temat maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="e7a95-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="e7a95-132">Witaj poniższy przykład przedstawia hello tematu maksymalny rozmiar too5GB z czasem toolive wynoszącym 1 minutę:</span><span class="sxs-lookup"><span data-stu-id="e7a95-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="e7a95-133">Filtry</span><span class="sxs-lookup"><span data-stu-id="e7a95-133">Filters</span></span>
<span data-ttu-id="e7a95-134">Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="e7a95-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="e7a95-135">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="e7a95-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="e7a95-136">Po wykonaniu przetwarzanie wstępne opcje żądania hello, hello wywołania metody `next`, przekazywanie wywołania zwrotnego z powitania po podpisaniu:</span><span class="sxs-lookup"><span data-stu-id="e7a95-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="e7a95-137">W tym wywołania zwrotnego i po hello przetwarzania `returnObject` (hello odpowiedzi z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub wywołanie `finalCallback` w przeciwnym razie hello tooend wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="e7a95-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="e7a95-138">Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="e7a95-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="e7a95-139">tworzy następujące Hello **ServiceBusService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="e7a95-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="e7a95-140">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7a95-140">Create subscriptions</span></span>
<span data-ttu-id="e7a95-141">Subskrypcje tematu są również tworzone za pomocą hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="e7a95-142">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.</span><span class="sxs-lookup"><span data-stu-id="e7a95-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a95-143">Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello tematu one są skojarzone z, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="e7a95-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="e7a95-144">Jeśli aplikacja zawiera logikę toocreate subskrypcję, jej należy najpierw sprawdź, czy hello subskrypcji już istnieje przy użyciu `getSubscription` metody.</span><span class="sxs-lookup"><span data-stu-id="e7a95-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="e7a95-145">Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="e7a95-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="e7a95-146">Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="e7a95-147">Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="e7a95-148">Witaj poniższy przykład tworzy subskrypcję o nazwie "AllMessages" i używa hello domyślne **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="e7a95-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="e7a95-149">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="e7a95-149">Create subscriptions with filters</span></span>
<span data-ttu-id="e7a95-150">Istnieje również możliwość utworzenia filtrów, które pozwalają tooscope wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="e7a95-151">Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **SqlFilter**, która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="e7a95-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="e7a95-152">Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="e7a95-153">Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.</span><span class="sxs-lookup"><span data-stu-id="e7a95-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="e7a95-154">Filtry można dodać subskrypcji tooa przy użyciu hello `createRule` metody hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="e7a95-155">Ta metoda umożliwia dodawanie nowych filtrów tooan istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a95-156">Ponieważ hello domyślnego filtru jest stosowane automatycznie tooall nowych subskrypcji, należy najpierw usunąć hello domyślnego filtru lub **MatchAll** zastępują inne filtry, można określić.</span><span class="sxs-lookup"><span data-stu-id="e7a95-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="e7a95-157">Można usunąć reguły domyślnej hello przy użyciu hello `deleteRule` metody **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="e7a95-158">Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `messagenumber` właściwości wyższej niż 3:</span><span class="sxs-lookup"><span data-stu-id="e7a95-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="e7a95-159">Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają `messagenumber` właściwości mniejszą lub równą too3:</span><span class="sxs-lookup"><span data-stu-id="e7a95-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="e7a95-160">Kiedy wiadomość jest teraz wysyłane za`MyTopic`, zawsze zostanie dostarczona do odbiorców mających subskrypcję toohello `AllMessages` subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` subskrypcje tematu (w zależności od zawartości wiadomość hello).</span><span class="sxs-lookup"><span data-stu-id="e7a95-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="e7a95-161">Jak toosend wiadomości tooa tematu</span><span class="sxs-lookup"><span data-stu-id="e7a95-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="e7a95-162">toosend tematu usługi Service Bus tooa wiadomości, aplikacja musi używać `sendTopicMessage` metody hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="e7a95-163">Komunikaty wysyłane są tematy magistrali tooService **BrokeredMessage** obiektów.</span><span class="sxs-lookup"><span data-stu-id="e7a95-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="e7a95-164">**BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `Label` i `TimeToLive`), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść danych ciągu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="e7a95-165">Aplikacja możne ustawić treść wiadomości powitania hello przez przekazanie wartości ciągu na powitania `sendTopicMessage` i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="e7a95-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="e7a95-166">Witaj poniższym przykładzie pokazano, jak toosend pięciu testowych komunikatów do `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="e7a95-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="e7a95-167">Należy pamiętać, że hello `messagenumber` wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (umożliwi to określenie subskrypcje, które go otrzymają):</span><span class="sxs-lookup"><span data-stu-id="e7a95-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="e7a95-168">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e7a95-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e7a95-169">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="e7a95-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e7a95-170">Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="e7a95-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="e7a95-171">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="e7a95-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="e7a95-172">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7a95-172">Receive messages from a subscription</span></span>
<span data-ttu-id="e7a95-173">Komunikaty są odbierane z subskrypcją za pomocą `receiveSubscriptionMessage` metody na powitania **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="e7a95-174">Domyślnie są usuwane z subskrypcji hello one są w trybie do odczytu; można jednak odczytać (peek) i zablokować wiadomość hello bez usuwania go z subskrypcji hello przez ustawienie opcjonalny parametr hello `isPeekLock` za**true**.</span><span class="sxs-lookup"><span data-stu-id="e7a95-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="e7a95-175">Witaj domyślne zachowanie odczytywanie i usuwanie wiadomości powitania jako część operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="e7a95-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="e7a95-176">toounderstand, Rozważmy scenariusz, w którym hello problemów konsumenta mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="e7a95-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="e7a95-177">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="e7a95-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="e7a95-178">Jeśli hello `isPeekLock` ustawiona jest zbyt**true**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="e7a95-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e7a95-179">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="e7a95-180">Po hello aplikacja zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje hello drugi etap procesu odbierania przez wywołanie metody **deleteMessage** — metoda i zapewnianie toobe wiadomości usunąć jako parametr.</span><span class="sxs-lookup"><span data-stu-id="e7a95-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="e7a95-181">Witaj **deleteMessage** metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e7a95-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="e7a95-182">Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="e7a95-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="e7a95-183">Witaj przykład otrzymuje najpierw usuwa komunikat z subskrypcji "LowMessages" hello i następnie odbiera wiadomości z przy użyciu subskrypcji "HighMessages" hello `isPeekLock` ustawić tootrue.</span><span class="sxs-lookup"><span data-stu-id="e7a95-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="e7a95-184">Następnie usuwa wiadomość hello przy użyciu `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="e7a95-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e7a95-185">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="e7a95-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="e7a95-186">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e7a95-187">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metoda **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="e7a95-188">Spowoduje to spowodować komunikatu w subskrypcji hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="e7a95-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e7a95-189">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji i jeśli aplikacja hello nie powiedzie się wiadomość hello tooprocess przed hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), następnie usługi Service Bus umożliwia odblokowanie wiadomość hello automatycznie i ułatwia dostępne toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="e7a95-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="e7a95-190">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="e7a95-191">Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="e7a95-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="e7a95-192">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="e7a95-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="e7a95-193">Jest to często osiągane przy użyciu **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="e7a95-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="e7a95-194">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7a95-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="e7a95-195">Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="e7a95-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="e7a95-196">Witaj poniższym przykładzie pokazano sposób nazywania tematu hello toodelete `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="e7a95-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="e7a95-197">Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.</span><span class="sxs-lookup"><span data-stu-id="e7a95-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="e7a95-198">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e7a95-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="e7a95-199">W poniższym przykładzie pokazano, jak toodelete subskrypcję o nazwie `HighMessages` z hello `MyTopic` tematu:</span><span class="sxs-lookup"><span data-stu-id="e7a95-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="e7a95-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7a95-200">Next Steps</span></span>
<span data-ttu-id="e7a95-201">Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="e7a95-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="e7a95-202">Zobacz [kolejki, tematy i subskrypcje][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="e7a95-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="e7a95-203">Dokumentacja interfejsów API dla elementu [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="e7a95-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="e7a95-204">Odwiedź hello [zestawu Azure SDK dla węzła] [ Azure SDK for Node] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="e7a95-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
