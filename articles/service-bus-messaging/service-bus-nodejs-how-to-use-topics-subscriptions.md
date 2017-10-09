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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Jak tooUse usługi Service Bus tematów i subskrypcji za pomocą języka Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

W tym przewodniku opisano sposób toouse usługi Service Bus tematów i subskrypcji z poziomu aplikacji Node.js. Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości** tematu tooa **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**. Aby uzyskać więcej informacji o tematach i subskrypcjach, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js
Utwórz pustą aplikację Node.js. Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure], [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu systemu Windows Programu PowerShell lub witryny sieci Web za pomocą programu WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
toouse usługi Service Bus, Pobierz hello Node.js Azure pakietu. Ten pakiet zawiera zestaw bibliotek, które komunikują się z usługi Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu toohello, w której utworzono aplikację przykładową.
2. Typ **azure instalacji narzędzia npm** w oknie polecenia hello, co powinno spowodować hello następujące dane wyjściowe:

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
3. Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony. W tym folderze znaleźć **azure** pakiet, który zawiera biblioteki hello należy tooaccess tematów usługi Service Bus.

### <a name="import-hello-module"></a>Moduł hello importu
Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Skonfiguruj połączenie usługi Service Bus
Hello Azure moduł odczytuje zmiennych środowiskowych hello `AZURE_SERVICEBUS_NAMESPACE` i `AZURE_SERVICEBUS_ACCESS_KEY` informacji wymaganych tooService tooconnect magistrali. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody `createServiceBusService`.

Na przykład ustawienia zmiennych środowiskowych powitania dla usługi w chmurze platformy Azure, zobacz [Node.js usługi chmury z magazynem][Node.js Cloud Service with Storage].

Na przykład ustawienia hello zmiennych środowiskowych dla witryny sieci Web platformy Azure, zobacz [aplikacji sieci Web Node.js z magazynem][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Tworzenie tematu
Witaj **ServiceBusService** obiektu umożliwia toowork z tematów. Poniższy kod tworzy **ServiceBusService** obiektu. Dodaj ją w górnej części hello **server.js** pliku po hello instrukcji tooimport hello azure modułu:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Wywołując `createTopicIfNotExists` na powitania **ServiceBusService** obiekt hello określony temat zostanie zwrócony (jeśli istnieje) lub zostanie utworzony nowy temat o określonej nazwie hello. Witaj poniższy kod używa `createTopicIfNotExists` toocreate lub łączenie toohello temat o nazwie `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Witaj `createServiceBusService` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślny temat ustawienia, takie jak czas wygaśnięcia wiadomości lub temat maksymalny rozmiar. Witaj poniższy przykład przedstawia hello tematu maksymalny rozmiar too5GB z czasem toolive wynoszącym 1 minutę:

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

### <a name="filters"></a>Filtry
Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **ServiceBusService**. Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:

```javascript
function handle (requestOptions, next)
```

Po wykonaniu przetwarzanie wstępne opcje żądania hello, hello wywołania metody `next`, przekazywanie wywołania zwrotnego z powitania po podpisaniu:

```javascript
function (returnObject, finalCallback, next)
```

W tym wywołania zwrotnego i po hello przetwarzania `returnObject` (hello odpowiedzi z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub wywołanie `finalCallback` w przeciwnym razie hello tooend wywołania usługi.

Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**. tworzy następujące Hello **ServiceBusService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Tworzenie subskrypcji
Subskrypcje tematu są również tworzone za pomocą hello **ServiceBusService** obiektu. Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.

> [!NOTE]
> Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello tematu one są skojarzone z, zostaną usunięte. Jeśli aplikacja zawiera logikę toocreate subskrypcję, jej należy najpierw sprawdź, czy hello subskrypcji już istnieje przy użyciu `getSubscription` metody.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello
Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji. Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji. Witaj poniższy przykład tworzy subskrypcję o nazwie "AllMessages" i używa hello domyślne **MatchAll** filtru.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Tworzenie subskrypcji z filtrami
Istnieje również możliwość utworzenia filtrów, które pozwalają tooscope wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.

Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **SqlFilter**, która implementuje podzbiór standardu SQL92. Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu. Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.

Filtry można dodać subskrypcji tooa przy użyciu hello `createRule` metody hello **ServiceBusService** obiektu. Ta metoda umożliwia dodawanie nowych filtrów tooan istniejącej subskrypcji.

> [!NOTE]
> Ponieważ hello domyślnego filtru jest stosowane automatycznie tooall nowych subskrypcji, należy najpierw usunąć hello domyślnego filtru lub **MatchAll** zastępują inne filtry, można określić. Można usunąć reguły domyślnej hello przy użyciu hello `deleteRule` metody **ServiceBusService** obiektu.
>
>

Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `messagenumber` właściwości wyższej niż 3:

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

Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają `messagenumber` właściwości mniejszą lub równą too3:

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

Kiedy wiadomość jest teraz wysyłane za`MyTopic`, zawsze zostanie dostarczona do odbiorców mających subskrypcję toohello `AllMessages` subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` subskrypcje tematu (w zależności od zawartości wiadomość hello).

## <a name="how-toosend-messages-tooa-topic"></a>Jak toosend wiadomości tooa tematu
toosend tematu usługi Service Bus tooa wiadomości, aplikacja musi używać `sendTopicMessage` metody hello **ServiceBusService** obiektu.
Komunikaty wysyłane są tematy magistrali tooService **BrokeredMessage** obiektów.
**BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `Label` i `TimeToLive`), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść danych ciągu. Aplikacja możne ustawić treść wiadomości powitania hello przez przekazanie wartości ciągu na powitania `sendTopicMessage` i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.

Witaj poniższym przykładzie pokazano, jak toosend pięciu testowych komunikatów do `MyTopic`. Należy pamiętać, że hello `messagenumber` wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (umożliwi to określenie subskrypcje, które go otrzymają):

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

Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello. Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
Komunikaty są odbierane z subskrypcją za pomocą `receiveSubscriptionMessage` metody na powitania **ServiceBusService** obiektu. Domyślnie są usuwane z subskrypcji hello one są w trybie do odczytu; można jednak odczytać (peek) i zablokować wiadomość hello bez usuwania go z subskrypcji hello przez ustawienie opcjonalny parametr hello `isPeekLock` za**true**.

Witaj domyślne zachowanie odczytywanie i usuwanie wiadomości powitania jako część operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii. toounderstand, Rozważmy scenariusz, w którym hello problemów konsumenta mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

Jeśli hello `isPeekLock` ustawiona jest zbyt**true**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.
Po hello aplikacja zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje hello drugi etap procesu odbierania przez wywołanie metody **deleteMessage** — metoda i zapewnianie toobe wiadomości usunąć jako parametr. Witaj **deleteMessage** metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z hello subskrypcji.

Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receiveSubscriptionMessage`. Witaj przykład otrzymuje najpierw usuwa komunikat z subskrypcji "LowMessages" hello i następnie odbiera wiadomości z przy użyciu subskrypcji "HighMessages" hello `isPeekLock` ustawić tootrue. Następnie usuwa wiadomość hello przy użyciu `deleteMessage`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlockMessage` metoda **ServiceBusService** obiektu. Spowoduje to spowodować komunikatu w subskrypcji hello toounlock usługi Service Bus i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji i jeśli aplikacja hello nie powiedzie się wiadomość hello tooprocess przed hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), następnie usługi Service Bus umożliwia odblokowanie wiadomość hello automatycznie i ułatwia dostępne toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `deleteMessage` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="delete-topics-and-subscriptions"></a>Usuwanie tematów i subskrypcji
Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo.
Witaj poniższym przykładzie pokazano sposób nazywania tematu hello toodelete `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu. Subskrypcje mogą być również usuwane niezależnie. W poniższym przykładzie pokazano, jak toodelete subskrypcję o nazwie `HighMessages` z hello `MyTopic` tematu:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.

* Zobacz [kolejki, tematy i subskrypcje][Queues, topics, and subscriptions].
* Dokumentacja interfejsów API dla elementu [SqlFilter][SqlFilter].
* Odwiedź hello [zestawu Azure SDK dla węzła] [ Azure SDK for Node] repozytorium w witrynie GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
