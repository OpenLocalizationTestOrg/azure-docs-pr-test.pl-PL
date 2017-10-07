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
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Jak kolejki usługi Service Bus toouse za pomocą języka Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

W tym artykule opisano, jak kolejki usługi Service Bus toouse za pomocą języka Node.js. Witaj przykłady są napisane w języku JavaScript i użyj hello modułu Node.js Azure. Witaj omówione scenariusze obejmują **tworzenie kolejek**, **wysyłania i odbierania wiadomości**, i **usuwanie kolejek**. Aby uzyskać więcej informacji dotyczących kolejek, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js
Utwórz pustą aplikację Node.js. Aby uzyskać instrukcje dotyczące toocreate aplikacji Node.js, zobacz [tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure][Create and deploy a Node.js application tooan Azure Website], lub [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
toouse usługi Azure Service Bus, pobranie i użycie hello Node.js Azure pakietu. Ten pakiet zawiera zestaw bibliotek, które komunikują się z usługi Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)
1. Użyj hello **środowiska Windows PowerShell dla środowiska Node.js** toohello toonavigate okno polecenia **c:\\węzła\\sbqueues\\WebRole1** folder, w którym został utworzony z Przykładowa aplikacja.
2. Typ **azure instalacji narzędzia npm** w oknie polecenia hello, co powinno spowodować dane wyjściowe podobne toohello poniżej:

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
3. Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **node_modules** folder został utworzony. W tym hello Znajdź folder **azure** pakiet, który zawiera biblioteki hello należy tooaccess kolejek usługi Service Bus.

### <a name="import-hello-module"></a>Moduł hello importu
Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Skonfiguruj połączenie usługi Azure Service Bus
Hello Azure moduł odczytuje zmiennej środowiskowej hello `AZURE_SERVICEBUS_CONNECTION_STRING` wymaganych informacji tooobtain tooService tooconnect magistrali. Jeśli nie ustawiono tej zmiennej środowiskowej, należy określić informacje o koncie hello podczas wywoływania metody `createServiceBusService`.

Na przykład ustawienia zmiennych środowiskowych hello w pliku konfiguracji dla usługi w chmurze platformy Azure, zobacz [Node.js usługi chmury z magazynem][Node.js Cloud Service with Storage].

Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure] [ Azure portal] dla witryny sieci Web Azure, zobacz [aplikacji sieci Web Node.js z magazynem] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Tworzenie kolejki
Witaj **ServiceBusService** obiektu umożliwia toowork z kolejek usługi Service Bus. Witaj poniższy kod tworzy **ServiceBusService** obiektu. Dodać u góry hello hello **server.js** pliku po hello instrukcji tooimport hello modułu platformy Azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Wywołując `createQueueIfNotExists` na powitania **ServiceBusService** obiekt hello określonej kolejki jest zwracany (jeśli istnieje) lub utworzeniu nowej kolejki o określonej nazwie hello. Witaj poniższy kod używa `createQueueIfNotExists` toocreate lub łączenie toohello kolejki o nazwie `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Witaj `createServiceBusService` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślne kolejki ustawienia, takie jak rozmiar kolejki toolive lub maksymalny czas wiadomości. Witaj poniższy przykład ustawia hello kolejki maksymalny rozmiar too5 GB i toolive (TTL) wartość czasu wynoszącym 1 minutę:

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

### <a name="filters"></a>Filtry
Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **ServiceBusService**. Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:

```javascript
function handle (requestOptions, next)
```

Po wykonaniu jej przetwarzanie wstępne opcje żądania hello, należy wywołać metodę hello `next`, przekazywanie wywołania zwrotnego z powitania po podpisaniu:

```javascript
function (returnObject, finalCallback, next)
```

W tym wywołania zwrotnego i po hello przetwarzania `returnObject` (hello odpowiedzi z serwera toohello żądania hello), albo należy wywołać wywołania zwrotnego hello `next` on istnieje toocontinue przetwarzania inne filtry, czy po prostu Wywołaj `finalCallback`, której kończy się Witaj wywołania usługi.

Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, `ExponentialRetryPolicyFilter` i `LinearRetryPolicyFilter`. Witaj poniższy kod tworzy `ServiceBusService` obiekt, który używa hello `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Komunikaty tooa kolejki wysyłania
toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `sendQueueMessage` metody na powitania **ServiceBusService** obiektu. Komunikaty wysłane za (i odebrane z) usługi Service Bus są kolejki **BrokeredMessage** obiekty i mają zestaw właściwości standardowych (takich jak **etykiety** i **TimeToLive**), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji. Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie ciągu jako wiadomość hello. Wszelkie wymagane właściwości standardowe są wypełniane przy użyciu wartości domyślnych.

Witaj poniższym przykładzie pokazano, jak toosend toohello kolejki wiadomości testowej o nazwie `myqueue` przy użyciu `sendQueueMessage`:

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

Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello. Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB. Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Odbieranie komunikatów z kolejki
Komunikaty są odbierane z kolejki przy użyciu hello `receiveQueueMessage` metody na powitania **ServiceBusService** obiektu. Domyślnie są usuwane z kolejki hello one są w trybie do odczytu; można jednak odczytać (peek) i zablokować wiadomość hello bez jego usuwania z kolejki hello przez ustawienie opcjonalny parametr hello `isPeekLock` za**true**.

Witaj domyślne zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

Jeśli hello `isPeekLock` ustawiona jest zbyt**true**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `deleteMessage` — metoda i zapewnianie toobe wiadomość hello usunąć jako parametr. Witaj `deleteMessage` metoda oznacza hello komunikat jako wykorzystany i usunie go z kolejki hello.

Witaj poniższym przykładzie pokazano, jak tooreceive procesu wiadomości i przy użyciu `receiveQueueMessage`. Hello przykład otrzymuje najpierw usuwa komunikat i otrzyma komunikat przy użyciu `isPeekLock` ustawić także**true**, a następnie usuwa hello komunikat przy użyciu `deleteMessage`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metody na powitania **ServiceBusService** obiektu. Spowoduje to spowodować wiadomości w kolejce hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli hello hello aplikacji kończy się niepowodzeniem, które tooprocess hello komunikatu przed przekroczenie limitu czasu blokady upływem (np. Jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat kolejek, zobacz następujące zasoby hello.

* [Kolejki, tematy i subskrypcje][Queues, topics, and subscriptions]
* [Zestaw Azure SDK dla węzła] [ Azure SDK for Node] repozytorium w witrynie GitHub
* [Centrum deweloperów środowiska Node.js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
