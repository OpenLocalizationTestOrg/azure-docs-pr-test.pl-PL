---
title: "kolejkuje toouse aaaHow usługi Service Bus w środowisku Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kolejki toouse usługi Service Bus na platformie Azure z poziomu aplikacji Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="14078-103">Jak kolejki usługi Service Bus toouse za pomocą języka Node.js</span><span class="sxs-lookup"><span data-stu-id="14078-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="14078-104">W tym artykule opisano, jak kolejki usługi Service Bus toouse za pomocą języka Node.js.</span><span class="sxs-lookup"><span data-stu-id="14078-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="14078-105">Witaj przykłady są napisane w języku JavaScript i użyj hello modułu Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="14078-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="14078-106">Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="14078-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="14078-107">Aby uzyskać więcej informacji dotyczących kolejek, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="14078-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="14078-108">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="14078-108">Create a Node.js application</span></span>
<span data-ttu-id="14078-109">Utwórz pustą aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="14078-109">Create a blank Node.js application.</span></span> <span data-ttu-id="14078-110">Aby uzyskać instrukcje dotyczące toocreate aplikacji Node.js, zobacz [tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure][Create and deploy a Node.js application tooan Azure Website], lub [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14078-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="14078-111">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="14078-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="14078-112">toouse usługi Azure Service Bus, pobranie i użycie hello Node.js Azure pakietu.</span><span class="sxs-lookup"><span data-stu-id="14078-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="14078-113">Ten pakiet zawiera zestaw bibliotek, które komunikują się z usługi Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="14078-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="14078-114">Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="14078-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="14078-115">Użyj hello **środowiska Windows PowerShell dla środowiska Node.js** toohello toonavigate okno polecenia **c:\\węzła\\sbqueues\\WebRole1** folder, w którym został utworzony z Przykładowa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="14078-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="14078-116">Typ **azure instalacji narzędzia npm** w oknie polecenia hello, co powinno spowodować dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="14078-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="14078-117">Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **node_modules** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="14078-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="14078-118">W tym hello Znajdź folder **azure** pakiet, który zawiera biblioteki hello należy tooaccess kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14078-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="14078-119">Moduł hello importu</span><span class="sxs-lookup"><span data-stu-id="14078-119">Import hello module</span></span>
<span data-ttu-id="14078-120">Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="14078-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="14078-121">Skonfiguruj połączenie usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="14078-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="14078-122">Hello Azure moduł odczytuje zmiennej środowiskowej hello `AZURE_SERVICEBUS_CONNECTION_STRING` wymaganych informacji tooobtain tooService tooconnect magistrali.</span><span class="sxs-lookup"><span data-stu-id="14078-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="14078-123">Jeśli nie ustawiono tej zmiennej środowiskowej, należy określić informacje o koncie hello podczas wywoływania metody `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="14078-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="14078-124">Na przykład ustawienia zmiennych środowiskowych hello w pliku konfiguracji dla usługi w chmurze platformy Azure, zobacz [Node.js usługi chmury z magazynem][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="14078-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="14078-125">Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure] [ Azure portal] dla witryny sieci Web Azure, zobacz [aplikacji sieci Web Node.js z magazynem] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="14078-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="14078-126">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="14078-126">Create a queue</span></span>
<span data-ttu-id="14078-127">Witaj **ServiceBusService** obiektu umożliwia toowork z kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14078-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="14078-128">Witaj poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="14078-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="14078-129">Dodać u góry hello hello **server.js** pliku po hello instrukcji tooimport hello modułu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="14078-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="14078-130">Wywołując `createQueueIfNotExists` na powitania **ServiceBusService** obiekt hello określonej kolejki jest zwracany (jeśli istnieje) lub utworzeniu nowej kolejki o określonej nazwie hello.</span><span class="sxs-lookup"><span data-stu-id="14078-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="14078-131">Witaj poniższy kod używa `createQueueIfNotExists` toocreate lub łączenie toohello kolejki o nazwie `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="14078-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="14078-132">Witaj `createServiceBusService` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślne kolejki ustawienia, takie jak rozmiar kolejki toolive lub maksymalny czas wiadomości.</span><span class="sxs-lookup"><span data-stu-id="14078-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="14078-133">Witaj poniższy przykład ustawia hello kolejki maksymalny rozmiar too5 GB i toolive (TTL) wartość czasu wynoszącym 1 minutę:</span><span class="sxs-lookup"><span data-stu-id="14078-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="14078-134">Filtry</span><span class="sxs-lookup"><span data-stu-id="14078-134">Filters</span></span>
<span data-ttu-id="14078-135">Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="14078-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="14078-136">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="14078-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="14078-137">Po wykonaniu jej przetwarzanie wstępne opcje żądania hello, należy wywołać metodę hello `next`, przekazywanie wywołania zwrotnego z powitania po podpisaniu:</span><span class="sxs-lookup"><span data-stu-id="14078-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="14078-138">W tym wywołania zwrotnego i po hello przetwarzania `returnObject` (hello odpowiedzi z serwera toohello żądania hello), albo należy wywołać wywołania zwrotnego hello `next` on istnieje toocontinue przetwarzania inne filtry, czy po prostu Wywołaj `finalCallback`, której kończy się Witaj wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="14078-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="14078-139">Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, `ExponentialRetryPolicyFilter` i `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="14078-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="14078-140">Witaj poniższy kod tworzy `ServiceBusService` obiekt, który używa hello `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="14078-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="14078-141">Komunikaty tooa kolejki wysyłania</span><span class="sxs-lookup"><span data-stu-id="14078-141">Send messages tooa queue</span></span>
<span data-ttu-id="14078-142">toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `sendQueueMessage` metody na powitania **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="14078-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="14078-143">Komunikaty wysłane za (i odebrane z) usługi Service Bus są kolejki **BrokeredMessage** obiekty i mają zestaw właściwości standardowych (takich jak **etykiety** i **TimeToLive**), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14078-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="14078-144">Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie ciągu jako wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="14078-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="14078-145">Wszelkie wymagane właściwości standardowe są wypełniane przy użyciu wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="14078-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="14078-146">Witaj poniższym przykładzie pokazano, jak toosend toohello kolejki wiadomości testowej o nazwie `myqueue` przy użyciu `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="14078-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="14078-147">Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="14078-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="14078-148">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="14078-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="14078-149">Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="14078-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="14078-150">Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="14078-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="14078-151">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="14078-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="14078-152">Odbieranie komunikatów z kolejki</span><span class="sxs-lookup"><span data-stu-id="14078-152">Receive messages from a queue</span></span>
<span data-ttu-id="14078-153">Komunikaty są odbierane z kolejki przy użyciu hello `receiveQueueMessage` metody na powitania **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="14078-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="14078-154">Domyślnie są usuwane z kolejki hello one są w trybie do odczytu; można jednak odczytać (peek) i zablokować wiadomość hello bez jego usuwania z kolejki hello przez ustawienie opcjonalny parametr hello `isPeekLock` za**true**.</span><span class="sxs-lookup"><span data-stu-id="14078-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="14078-155">Witaj domyślne zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="14078-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="14078-156">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="14078-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="14078-157">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="14078-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="14078-158">Jeśli hello `isPeekLock` ustawiona jest zbyt**true**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="14078-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="14078-159">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14078-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="14078-160">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `deleteMessage` — metoda i zapewnianie toobe wiadomość hello usunąć jako parametr.</span><span class="sxs-lookup"><span data-stu-id="14078-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="14078-161">Witaj `deleteMessage` metoda oznacza hello komunikat jako wykorzystany i usunie go z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="14078-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="14078-162">Witaj poniższym przykładzie pokazano, jak tooreceive procesu wiadomości i przy użyciu `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="14078-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="14078-163">Hello przykład otrzymuje najpierw usuwa komunikat i otrzyma komunikat przy użyciu `isPeekLock` ustawić także**true**, a następnie usuwa hello komunikat przy użyciu `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="14078-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="14078-164">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="14078-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="14078-165">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="14078-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="14078-166">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na powitania **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="14078-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="14078-167">Spowoduje to spowodować wiadomości w kolejce hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="14078-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="14078-168">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli hello hello aplikacji kończy się niepowodzeniem, które tooprocess hello komunikatu przed przekroczenie limitu czasu blokady upływem (np. Jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="14078-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="14078-169">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="14078-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="14078-170">Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="14078-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="14078-171">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="14078-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="14078-172">Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="14078-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14078-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14078-173">Next steps</span></span>
<span data-ttu-id="14078-174">toolearn więcej informacji na temat kolejek, zobacz następujące zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="14078-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="14078-175">[Kolejki, tematy i subskrypcje][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="14078-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="14078-176">[Zestaw Azure SDK dla węzła] [ Azure SDK for Node] repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="14078-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="14078-177">Centrum deweloperów środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="14078-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
