---
title: toouse aaaHow magazynu tabel Azure w oprogramowaniu Node.js | Dokumentacja firmy Microsoft
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Jak toouse magazynu tabel Azure w oprogramowaniu Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Omówienie
W tym temacie przedstawiono, jak usługa tooperform typowych scenariuszy przy użyciu hello Azure tabeli w aplikacji Node.js.

Przykłady kodu Hello w tym temacie założono, że masz już aplikację Node.js. Aby uzyskać informacje na temat toocreate aplikacji Node.js na platformie Azure, zobacz jedną z poniższych tematów:

* [Tworzenie aplikacji sieci web Node.js w usłudze Azure App Service](../app-service-web/app-service-web-get-started-nodejs.md)
* [Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą programu WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (przy użyciu programu Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Konfigurowanie sieci tooaccess aplikacji usługi Azure Storage
toouse usługi Azure Storage, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Użyj pakietu hello tooinstall węzeł Menedżera pakietów (NPM)
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix) i przejdź do folderu toohello, w której utworzono aplikację.
2. Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello. Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład.

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
3. Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony. Wewnątrz tego folderu znajdują się hello **magazyn azure** pakiet, który zawiera biblioteki hello potrzebny jest magazyn tooaccess.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Dodaj następującego kodu toohello początku hello hello **server.js** plik w aplikacji:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
Moduł Hello azure odczyta zmiennych środowiskowych hello AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia \_Ciąg tooyour tooconnect informacje wymagane konto magazynu Azure. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **TableService**.

Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Tworzenie tabeli
Witaj poniższy kod tworzy **TableService** obiektu i używa go toocreate nową tabelę. Dodaj następujące hello u góry hello **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Witaj wywołanie za**createTableIfNotExists** spowoduje utworzenie nowej tabeli o określonej nazwie hello, jeśli jeszcze nie istnieje. Witaj poniższy przykład tworzy nową tabelę o nazwie "mytable", jeśli jeszcze nie istnieje:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Witaj `result.created` będzie `true` Jeśli nowa tabela została utworzona, oraz `false` Jeśli hello tabela już istnieje. Witaj `response` będzie zawierać informacje o żądaniu hello.

### <a name="filters"></a>Filtry
Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **TableService**. Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:

```nodejs
function handle (requestOptions, next)
```

Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall "dalej", przekazywanie wywołania zwrotnego z powitania po podpisaniu:

```nodejs
function (returnObject, finalCallback, next)
```

W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback inaczej hello tooend wywołania usługi.

Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**. tworzy następujące Hello **TableService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
tooadd jednostki, najpierw utwórz obiekt, który definiuje właściwości jednostki. Musi zawierać wszystkie jednostki **PartitionKey** i **RowKey**, które są unikatowych identyfikatorów dla jednostek hello.

* **PartitionKey** — Określa jednostki hello są przechowywane w partycji hello
* **RowKey** — unikatowo identyfikuje hello jednostek w partycji hello

Zarówno **PartitionKey** i **RowKey** muszą być ciągami. Aby uzyskać więcej informacji, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Witaj poniżej znajduje się przykład Definiowanie jednostki. Należy pamiętać, że **Data ukończenia** jest zdefiniowana jako typ **Edm.DateTime**. Określanie typu hello jest opcjonalny i typy będzie można wywnioskować, jeśli nie została określona.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Istnieje również **sygnatury czasowej** pola dla każdego rekordu, który jest ustawiony przez platformę Azure, gdy jednostki są wstawiane lub aktualizowane.
>
>

Można również użyć hello **entityGenerator** toocreate jednostek. Witaj poniższy przykład tworzy hello tej samej jednostki zadania przy użyciu hello **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd Tabela tooyour jednostek przekazać hello jednostki obiektu toohello **insertEntity** metody.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Jeśli hello operacja się powiodła, `result` będzie zawierać hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) z hello dodaje rekord i `response` będzie zawierać informacje na temat operacji hello.

Przykład odpowiedzi:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Domyślnie **insertEntity** nie zwraca jednostek hello wstawiony jako część hello `response` informacji. Jeśli planowane jest wykonywanie innych operacji w tej jednostce, lub chcesz informacji hello toocache, może być przydatne toohave zwrócony jako część hello `result`. Można to zrobić przez włączenie **echoContent** w następujący sposób:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Aktualizuj jednostkę
Istnieje wiele metod tooupdate dostępne istniejącego obiektu:

* **replaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki
* **mergeEntity** — aktualizuje istniejące jednostki przez scalenie nowej wartości właściwości istniejącej jednostki hello
* **insertOrReplaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki. Jeśli jednostka nie istnieje, zostanie wstawiony nowy
* **insertOrMergeEntity** -aktualizacji przez scalenie istniejących hello nowej wartości właściwości istniejącej jednostki. Jeśli jednostka nie istnieje, zostanie wstawiony nowy

Witaj poniższym przykładzie pokazano aktualizowanie jednostki przy użyciu **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Domyślnie aktualizowania jednostki nie sprawdza toosee Jeśli danych hello aktualizowana wcześniej został zmodyfikowany przez inny proces. toosupport równoczesnych aktualizacji:
>
> 1. Pobierz hello ETag aktualizowany obiekt hello. Ten błąd jest zwracany jako część hello `response` do żadnej operacji powiązanych jednostek i mogą zostać pobrane za pośrednictwem `response['.metadata'].etag`.
> 2. Podczas wykonywania operacji update na jednostkę, Dodaj hello ETag pobrać informacji o wcześniej toohello nowej jednostki. Na przykład:
>
>       entity2 .etag [.metadata] = currentEtag;
> 3. Wykonaj operację aktualizacji hello. Jeśli jednostka hello został zmodyfikowany od czasu pobrania hello wartość ETag, takich jak inne wystąpienie aplikacji, `error` zostaną zwrócone z informacją hello aktualizacji warunek określony w żądaniu hello nie był spełniony.
>
>

Z **replaceEntity** i **mergeEntity**, jeśli hello jednostki, która jest aktualizowana nie istnieje, operacja aktualizacji hello zakończy się niepowodzeniem. Dlatego w razie potrzeby toostore jednostki niezależnie od tego, czy istnieje już używać **insertOrReplaceEntity** lub **insertOrMergeEntity**.

Witaj `result` aktualizacji pomyślnych operacji będzie zawierać hello **Etag** z hello aktualizacji jednostki.

## <a name="work-with-groups-of-entities"></a>Praca z grupami jednostek
Czasami powoduje toosubmit znaczeniu wiele operacji razem w tooensure partii przetwarzania przez serwer hello atomic. tooaccomplish, który Użyj hello **TableBatch** klasy toocreate partii, a następnie użyć hello **executeBatch** metody **TableService** tooperform hello umieścić w zadaniu wsadowym operacji.

 Witaj poniższy przykład przedstawia przesyłanie dwie jednostki w partii:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Dla operacji wsadowych pomyślne `result` będzie zawierać informacje dla każdej operacji w partii hello.

### <a name="work-with-batched-operations"></a>Praca z operacji wsadowych
Operacje dodane partii tooa mogą być kontrolowane przez wyświetlanie hello `operations` właściwości. Można także użyć hello następujące metody toowork z operacjami:

* **Wyczyść** — usuwa wszystkie operacje z partii
* **getOperations** -pobiera operację z hello partii
* **hasOperations** — zwraca wartość true, jeśli hello partia zawiera operacje
* **removeOperations** — usuwa operacji
* **rozmiar** — zwraca hello liczba operacji w partii hello

## <a name="retrieve-an-entity-by-key"></a>Pobrać jednostek według klucza
określonej jednostki oparte na powitania tooreturn **PartitionKey** i **RowKey**, użyj hello **retrieveEntity** — metoda.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Po zakończeniu tej operacji `result` będzie zawierać hello jednostki.

## <a name="query-a-set-of-entities"></a>Zapytanie zestawu jednostek
tooquery tabelę, użyj hello **TableQuery** obiekt toobuild się przy użyciu powitania po klauzule wyrażenia zapytania:

* **Wybierz** -toobe pola hello zwracane z kwerendy hello
* **gdzie** — Witaj gdzie klauzuli

  * **i** — `and` warunek where
  * **lub** — `or` warunek where
* **TOP** — Witaj liczbę elementów toofetch

Witaj poniższy przykład tworzy kwerendę, która zwróci hello top pięć elementów PartitionKey "hometasks".

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Ponieważ **wybierz** nie jest używany, zostaną zwrócone wszystkie pola. tooperform hello zapytania dotyczącego tabeli, użyj **queryEntities**. Witaj poniższym przykładzie użyto jednostek tooreturn tego zapytania z "mytable".

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

W przypadku powodzenia `result.entries` będzie zawierać tablicę jednostek spełniających hello kwerendy. Jeśli zapytanie hello tooreturn wszystkie jednostki `result.continuationToken` będzie z systemem innym niż*null* i można go używać jako trzeci parametr funkcji hello **queryEntities** tooretrieve więcej wyników. Witaj początkowego zapytania można użyć *null* dla hello trzeci parametr.

### <a name="query-a-subset-of-entity-properties"></a>Tworzenie zapytania do podzbioru właściwości jednostki
Tabela tooa kwerend może pobrać kilka pól jednostki.
To redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek. Użyj hello **wybierz** zwrócił klauzuli i przekazać nazwy hello hello toobe pola. Na przykład hello następującej kwerendy zwróci tylko hello **opis** i **Data ukończenia** pola.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Usuwanie jednostki
Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza. W tym przykładzie hello **task1** obiekt zawiera hello **RowKey** i **PartitionKey** wartości toobe jednostki hello usunięte. Następnie obiekt hello jest przekazywany toohello **deleteEntity** metody.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Należy rozważyć użycie elementy etag, gdy usunięcie elementów, tooensure, który hello elementu nie została zmodyfikowana przez inny proces. Zobacz [Aktualizuj jednostkę](#update-an-entity) informacji na temat używania elementy ETag.
>
>

## <a name="delete-a-table"></a>Usuwanie tabeli
Witaj następującego kodu usuwa tabelę z konta magazynu.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Jeśli masz pewności, czy tabela hello istnieje, użyj **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Używaj tokenów kontynuacji
Podczas wykonywania zapytań dotyczących tabel w przypadku dużych ilości wyników, należy wyszukać kontynuacji tokenów. Może istnieć dużych ilości danych dostępne dla tej kwerendy, czy użytkownik może nie należy pamiętać, jeśli nie Konstruuj toorecognize, gdy token kontynuacji jest obecna.

Obiekt Hello wyniki zwrócone podczas wykonywania zapytania zestawów jednostek `continuationToken` właściwości, gdy obecny jest takie tokenu. Następnie można to podczas przeprowadzania toomove toocontinue zapytania na powitania partycji i tabela jednostek.

Podczas wykonywania zapytania, można podać parametru continuationToken między wystąpienie obiektu hello zapytania i funkcja wywołania zwrotnego hello:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Jeśli inspekcja hello `continuationToken` obiektu, można znaleźć właściwości takich jak `nextPartitionKey`, `nextRowKey` i `targetLocation`, które mogą być używane tooiterate przez wszystkie wyniki hello.

Istnieje również kontynuacji próbki w ramach hello repozytorium Node.js magazynu Azure w serwisie GitHub. Wyszukaj `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Praca z sygnatury dostępu współdzielonego
Sygnatury dostępu współdzielonego (SAS) są tootables szczegółowego dostępu tooprovide bezpieczny sposób, bez konieczności podawania Twojej nazwy konta magazynu lub kluczy. Skojarzenia zabezpieczeń są często używane tooprovide ograniczony dostęp tooyour dane, takie jak stosowanie aplikacji mobilnej tooquery rekordów.

Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnaturę dostępu Współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **TableService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji przykład aplikacji mobilnej. Hello sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello SAS jest prawidłowy, a także hello posiadacz SAS toohello nadanego poziomu dostępu.

Witaj poniższy przykład generuje nowe zasady dostępu współdzielonego, które umożliwią hello SAS posiadacz tooquery (r) hello tabeli i wygasa 100 minut po uruchomieniu hello jest tworzona.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz SAS hello prób tooaccess hello tabeli.

Witaj aplikacji klienckiej, a następnie używa hello SAS z **TableServiceWithSAS** tooperform operacji względem tabeli hello. Poniższy przykład Hello połączenie tabeli toohello i wykonuje zapytania.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Ponieważ hello wygenerowano sygnaturę dostępu Współdzielonego tylko zapytania dostęp, próba dokonane tooinsert, aktualizowanie lub usuwanie jednostek, czy zwracany błąd.

### <a name="access-control-lists"></a>Listy kontroli dostępu
Umożliwia także zasad dostępu hello tooset listy kontroli dostępu (ACL) dla sygnatury dostępu Współdzielonego. Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess hello tabeli, ale zawiera różne zasady dostępu dla każdego klienta.

Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady. Poniższy przykład Hello definiuje dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

powitania po pobiera przykład Witaj bieżącej listy ACL dla hello **hometasks** tabeli, a następnie dodanie nowych zasad hello przy użyciu **setTableAcl**. Takie podejście umożliwia:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Raz hello ustawione listy ACL, następnie można utworzyć sygnatury dostępu Współdzielonego na podstawie Identyfikatora hello zasad. Witaj poniższy przykład powoduje utworzenie nowej sygnatury dostępu Współdzielonego dla "uzytkownik2":

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello.

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Zestaw Azure SDK magazynu dla węzła](https://github.com/Azure/azure-storage-node) repozytorium w witrynie GitHub.
* [Centrum deweloperów środowiska Node.js](/develop/nodejs/)
* [Tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure](../app-service-web/app-service-web-get-started-nodejs.md)
