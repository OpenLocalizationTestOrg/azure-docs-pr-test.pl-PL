---
title: toouse aaaHow magazynu kolejek w oprogramowaniu Node.js | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate usługi kolejek platformy Azure hello toouse i usuwania kolejki oraz insert, Pobierz i usunąć wiadomości. Przykłady zapisywane w środowisku Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Jak toouse magazynu kolejek w oprogramowaniu Node.js
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku pokazano, jak tooperform typowych scenariuszy przy użyciu hello usługi Microsoft Azure kolejki. Hello przykłady są napisane przy użyciu hello interfejsu API środowiska Node.js. Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Tworzenie aplikacji Node.js
Utwórz pustą aplikację Node.js. Aby uzyskać instrukcje tworzenia aplikacji Node.js, zobacz [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service], [tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure] przy użyciu programu Windows PowerShell lub [ Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web].

## <a name="configure-your-application-tooaccess-storage"></a>Skonfiguruj tooAccess Twoja aplikacja magazynu
toouse magazynu Azure, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu toohello, w której utworzono aplikację przykładową.
2. Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello. Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony. Wewnątrz tego folderu znajdują się hello **magazyn azure** pakiet, który zawiera biblioteki hello muszą uzyskać dostęp do magazynu.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello **server.js** pliku aplikacji hello, w którym ma toouse magazynu:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Ustawienia połączenia z magazynem Azure
Moduł Hello azure odczyta zmiennych środowiskowych hello AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia \_Ciąg tooyour tooconnect informacje wymagane konto magazynu Azure. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **createQueueService**.

Na przykład ustawienia zmiennych środowiskowych hello w hello [Azure Portal](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel].

## <a name="how-to-create-a-queue"></a>Porady: Tworzenie kolejki
Witaj poniższy kod tworzy **QueueService** obiektu, który pozwala toowork z kolejki.

```
var queueSvc = azure.createQueueService();
```

Użyj hello **createQueueIfNotExists** metody, która zwraca hello określoną kolejkę, jeśli już istnieje lub tworzy nową kolejkę o określonej nazwie hello, jeśli jeszcze nie istnieje.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Jeśli kolejka hello jest tworzona, `result.created` ma wartość true. Jeśli istnieje kolejka hello, `result.created` ma wartość false.

### <a name="filters"></a>Filtry
Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **QueueService**. Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:

```
function handle (requestOptions, next)
```

Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall przycisk Dalej, przekazywanie wywołania zwrotnego z powitania po podpisaniu:

```
function (returnObject, finalCallback, next)
```

W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback w przeciwnym razie tooend się hello wywołania usługi.

Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**. tworzy następujące Hello **QueueService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Porady: Wstawianie komunikatu do kolejki
tooinsert wiadomości do kolejki, użyj hello **polecenie createMessage** metodę, aby utworzyć nową wiadomość i dodać go toohello kolejki.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Porady: Podgląd hello następny komunikat
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peekMessages** metody. Domyślnie **peekMessages** wglądu w pojedynczym komunikacie.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Witaj `result` zawiera wiadomość hello.

> [!NOTE]
> Przy użyciu **peekMessages** gdy nie ma żadnych komunikatów w kolejce hello nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Porady: Hello następny komunikat usuwania z kolejki
Przetwarza komunikat jest procesem dwuetapowym:

1. Wiadomości powitania usuwania z kolejki.
2. Usuń wiadomość hello.

Użyj toodequeue komunikat **getMessages**. Dzięki temu wiadomości powitania niewidoczne w kolejce hello, więc może je przetwarzać żadnych innych klientów. Po przetworzeniu komunikatu aplikacji wywołać **deleteMessage** toodelete ją z kolejki hello. Poniższy przykład Hello pobiera komunikat, a następnie usuwa je:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Domyślnie komunikat jest ukryty tylko przez 30 sekund, po których jest widoczna tooother klientów. Określ inną wartość, przy użyciu `options.visibilityTimeout` z **getMessages**.
> 
> [!NOTE]
> Przy użyciu **getMessages** gdy nie ma żadnych komunikatów w kolejce hello nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Porady: Zmiana zawartości hello wiadomości w kolejce
Możesz zmienić zawartość komunikatu w miejscu przy użyciu kolejki hello hello **updateMessage**. Poniższy przykład Hello aktualizuje tekst wiadomości powitania:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Porady: Dodatkowych opcji usuwania komunikatów
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki:

* `options.numOfMessages`-Pobrać partii komunikatów (w górę too32).
* `options.visibilityTimeout`-Ustawienia limit czasu niewidoczności dłuższy lub krótszy.

Witaj poniższym przykładzie użyto hello **getMessages** metody tooget 15 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli for. Ustawia również minut toofive limitu czasu niewidoczności hello wszystkie komunikaty zwracane przez tę metodę.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Porady: Uzyskiwanie hello długość kolejki
Witaj **getQueueMetadata** zwraca metadane dotyczące kolejki hello, łącznie z hello przybliżoną liczbę komunikatów oczekujących w kolejce hello.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Porady: Lista kolejek
Lista kolejek, użyj tooretrieve **listQueuesSegmented**. tooretrieve listy filtrowane według określonego prefiksu, użyj **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Jeśli nie można zwrócić wszystkich kolejek, `result.continuationToken` mogą służyć jako pierwszy parametr hello **listQueuesSegmented** lub hello drugi parametr funkcji **listQueuesSegmentedWithPrefix** tooretrieve więcej wyników.

## <a name="how-to-delete-a-queue"></a>Porady: Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **deleteQueue** metody dla obiekt kolejki hello.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

Użyj wszystkich wiadomości z kolejki usuwając, tooclear **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Porady: Praca z sygnatury dostępu współdzielonego
Udostępniony sygnatur dostępu (SAS) są tooqueues szczegółowego dostępu tooprovide bezpieczny sposób, bez konieczności podawania Twojej nazwy konta magazynu lub kluczy. Skojarzenia zabezpieczeń są często używane tooprovide ograniczone dostępu tooyour kolejki, na przykład pozwala aplikacji mobilnej toosubmit wiadomości.

Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnaturę dostępu Współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **QueueService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji. Na przykład aplikacji mobilnej. Hello sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello SAS jest prawidłowy, a także hello posiadacz SAS toohello nadanego poziomu dostępu.

Poniższy przykład Hello generuje nowe zasady dostępu współdzielonego, które umożliwią hello SAS posiadacz tooadd wiadomości toohello kolejki i wygasa 100 minut po uruchomieniu hello jest tworzona.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz SAS hello prób tooaccess hello kolejki.

Witaj aplikacji klienckiej, a następnie używa hello SAS z **QueueServiceWithSAS** tooperform operacji względem hello kolejki. Poniższy przykład Hello łączy toohello kolejki i tworzy komunikat.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Ponieważ hello SAS został wygenerowany z Dodawanie dostępu, jeśli próba wprowadzono tooread, aktualizowanie lub usuwanie wiadomości, czy zwracany błąd.

### <a name="access-control-lists"></a>Listy kontroli dostępu
Umożliwia także zasad dostępu hello tooset listy kontroli dostępu (ACL) dla sygnatury dostępu Współdzielonego. Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess hello kolejki, ale zawiera różne zasady dostępu dla każdego klienta.

Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady. Poniższy przykład Hello definiuje dwie zasady; jeden dla "Użytkownik1" i jeden dla "uzytkownik2":

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

powitania po pobiera przykład Witaj bieżącej listy ACL dla **Moja_kolejka**, następnie dodaje nowe zasady hello przy użyciu **setQueueAcl**. Takie podejście umożliwia:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Raz hello ustawione listy ACL, następnie można utworzyć sygnatury dostępu Współdzielonego na podstawie Identyfikatora hello zasad. Witaj poniższy przykład powoduje utworzenie nowej sygnatury dostępu Współdzielonego dla "uzytkownik2":

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* Odwiedź hello [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog].
* Odwiedź hello [zestawu SDK usługi Magazyn Azure dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[tworzenie aplikacji sieci web Node.js w usłudze Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[aplikacji sieci web Node.js w usłudze hello Azure usługa tabel]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
