---
title: "Programowanie JavaScript po stronie aaaServer dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toowrite bazy danych Azure rozwiązania Cosmos toouse procedury składowane, wyzwalacze bazy danych i funkcje zdefiniowane przez użytkownika (UDF) w języku JavaScript. Pobierz porady programing bazy danych i inne."
keywords: "Wyzwalacze bazy danych, procedury składowanej, procedury składowanej, program bazy danych, sproc, documentdb, azure, platformy Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Programowanie po stronie serwera w usłudze Azure DB rozwiązania Cosmos: procedury składowane, wyzwalacze bazy danych i funkcji UDF
Dowiedz się, jak zintegrować języka Azure rozwiązania Cosmos DB, transakcyjne wykonywanie kodu JavaScript umożliwia deweloperom pisanie **procedur składowanych**, **wyzwalaczy** i **funkcje zdefiniowane przez użytkownika** natywnie w [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript. Dzięki temu toowrite bazy danych programu aplikacji logiki, które mogą być dostarczane i wykonywane bezpośrednio na powitania bazy danych magazynu partycji. 

Zaleca się wprowadzenie uruchomione przez oglądaniu powitania po wideo, gdzie Andrew Liu zapewnia model programowania po stronie serwera bazy danych tooCosmos krótkie wprowadzenie dla bazy danych. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Następnie wróć toothis artykułu, w którym poznasz toohello odpowiedzi hello następujące pytania:  

* Jak zapisać procedury składowanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika przy użyciu języka JavaScript?
* Sposób rozwiązania Cosmos DB zagwarantować kwasu?
* Jak działają transakcji w bazie danych rozwiązania Cosmos
* Co to są wstępnie wyzwala i jest wyzwalane po i jak jedną zapisać?
* Jak zarejestrować i wykonać procedury przechowywanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika w sposób RESTful za pośrednictwem protokołu HTTP?
* Co rozwiązania Cosmos SDK bazy danych są dostępne toocreate i wykonywanie przechowywanych procedur, wyzwalaczy i funkcji UDF?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Wprowadzenie tooStored procedury i programowania funkcji zdefiniowanej przez użytkownika
To podejście *"JavaScript jako nowoczesnego dzień T-SQL"* zwalnia deweloperzy aplikacji od złożoności hello niezgodności typu systemu i technologii mapowania relacyjnego obiektu. Ponadto wprowadzono szereg korzyści wewnętrzne, które mogą być wykorzystywane toobuild rozbudowanych aplikacji:  

* **Logika proceduralna:** JavaScript jako wysokiego poziomu języka programowania, zapewnia tooexpress interfejs zaawansowanych, znanych logiki biznesowej. Można wykonywać złożonych sekwencji operacji bliżej toohello danych.
* **Niepodzielne transakcji:** gwarancje rozwiązania Cosmos bazy danych, które bazy danych operacji wewnątrz jednej procedury składowanej lub wyzwalacza są atomic. Dzięki temu aplikacja łączy pokrewnych operacje w pojedynczej partii, dzięki czemu wszystkie z nich poprawne albo żadna z nich powiodło się. 
* **Wydajność:** hello na fakt, że JSON jest system typów języka Javascript leżą zamapowanych toohello i jest również hello podstawowa jednostka przestrzeni dyskowej w bazie danych rozwiązania Cosmos umożliwia kilka optymalizacji, takich jak opóźnieniem materialization o JSON dokumentów w buforze hello Pula i nadawania dostępne toohello na żądanie wykonywanie kodu. Istnieje więcej korzyści wydajności związanych z wysyłanie bazy danych toohello logiki biznesowej:
  
  * Przetwarzanie wsadowe — deweloperzy mogą grupy operacje, takie jak wstawia i przesyłanie ich zbiorczo. Opóźnienie ruchu sieci Hello kosztów i zmniejszone hello magazynu narzutów toocreate oddzielne transakcje. 
  * Wstępna kompilacja — rozwiązania Cosmos DB precompiles procedur składowanych, wyzwalaczy i tooavoid funkcje zdefiniowane przez użytkownika koszt kompilacji języka JavaScript dla każdego wywołania. Witaj koszty tworzenia kodu bajtowego hello jest logiki procedurach hello amortyzowanego tooa minimalnej wartości.
  * Sekwencjonowanie — wiele operacji potrzeby efekt uboczny ("wyzwalacza") która potencjalnie obejmuje wykonanie jednej lub wielu operacji dodatkowej magazynu. Jako uzupełnienie niepodzielność, to wydajność więcej po przeniesieniu toohello serwera. 
* **Hermetyzacja:** przechowywane procedury mogą być używane toogroup logiki biznesowej w jednym miejscu. Daje to dwie następujące korzyści:
  * Dodaje warstwy abstrakcji na powitania nieprzetworzone dane, co umożliwia ich aplikacji niezależnie od danych hello tooevolve architektów danych. Jest to szczególnie korzystne w przypadku, gdy dane hello przynależy schematu, powodu toohello łamliwa założeń, które może być konieczne toobe rozszerzania do aplikacji hello, jeśli mają bezpośrednio toodeal z danymi.  
  * Ta warstwa abstrakcji pozwala chronić swoje dane usprawnienie dostępu hello ze skryptów hello przedsiębiorstwa.  

Witaj tworzenia i uruchamiania wyzwalaczy bazy danych, procedury składowane i operatory zapytań niestandardowych jest obsługiwany za pośrednictwem hello [interfejsu API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), i [zestawówSDKklienta](documentdb-sdk-dotnet.md) na wielu platformach, w tym .NET, Node.js oraz JavaScript.

W tym samouczku używana hello [Node.js SDK z ze zobowiązania Q](http://azure.github.io/azure-documentdb-node-q/) tooillustrate składni i użycia procedur składowanych, wyzwalaczy i funkcji UDF.   

## <a name="stored-procedures"></a>Procedury składowane
### <a name="example-write-a-simple-stored-procedure"></a>Przykład: Napisać prosty procedury składowanej
Zacznijmy od prostego procedury przechowywanej, która zwraca odpowiedź "Hello World".

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Procedury składowane są rejestrowane w jednej kolekcji i może działać na dokumentów i załączników w tej kolekcji. Hello poniższy fragment kodu przedstawia sposób tooregister hello helloWorld przechowywane procedury z kolekcją. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Po zarejestrowaniu hello przechowywane procedury możemy ją wykonać hello kolekcji i przeczytaj wyniki hello zwrotnego na powitania klienta. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


Obiekt kontekstu Hello zapewnia dostęp tooall operacje, które można wykonywać w dyskowej rozwiązania Cosmos bazy danych, a także uzyskiwać dostęp do obiektów toohello żądań i odpowiedzi. W takim przypadku użyliśmy hello obiektu tooset hello treść odpowiedzi hello odpowiedzi, która została wysłana wstecz toohello klienta. Aby uzyskać więcej informacji, zobacz toohello [serwera Azure rozwiązania Cosmos DB JavaScript dokumentacji zestawu SDK](http://azure.github.io/azure-documentdb-js-server/).  

Daj nam rozwiń w tym przykładzie i dodać więcej bazy danych związanych z nimi funkcji toohello procedury składowanej. Procedury składowane można tworzenie, aktualizowanie, odczytu, zapytania i usuwać dokumenty i załączniki wewnątrz hello kolekcji.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Przykład: Napisania toocreate procedury składowanej dokumentu
fragment dalej Hello pokazuje, jak toouse hello toointeract obiektu kontekstu z zasobami DB rozwiązania Cosmos.

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


Tę procedurę składowaną przyjmuje jako documentToCreate wejściowych, treści hello toobe dokumentu, utworzone w bieżącej kolekcji hello. Wszystkie operacje są asynchroniczne i zależą od wywołania zwrotne funkcji JavaScript. Funkcja wywołania zwrotnego Hello ma dwa parametry: jeden dla obiekt błędu hello w przypadku, gdy operacja hello kończy się niepowodzeniem i jeden dla hello utworzony obiekt. Wewnątrz wywołania zwrotnego hello użytkowników można obsłużyć wyjątek hello lub zgłosić błąd. W przypadku, gdy wywołanie zwrotne nie zostanie podana, i występuje błąd, hello Azure DB rozwiązania Cosmos w czasie wykonywania zgłasza błąd.   

W powyższym przykładzie hello wywołania zwrotnego hello zgłasza błąd, jeśli hello operacja nie powiodła się. W przeciwnym razie Ustawia identyfikator hello hello dokument utworzony jako treść hello hello odpowiedzi toohello klienta. Oto, jak wykonaniem tej procedury składowanej z parametrami wejściowymi.

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


Należy pamiętać, że procedurę składowaną można zmodyfikowanych tootake tablicę treści dokumentu jako dane wejściowe i je utworzyć w hello sam przechowywane procedury wykonywania zamiast wielu sieci żądań toocreate ich osobno. Może to być używane tooimplement importer zbiorczego wydajne rozwiązania Cosmos bazy danych (omówiony w dalszej części tego samouczka).   

przykład Witaj opisane przedstawiono, jak toouse procedur składowanych. Później w samouczku hello omówimy wyzwalaczy i funkcji zdefiniowanych przez użytkownika (UDF).

## <a name="database-program-transactions"></a>Transakcji w bazie danych programu
Transakcji w typowej bazy danych można zdefiniować jako sekwencja operacji wykonywanych jako pojedyncza jednostka logiczna pracy. Udostępnia każdą transakcję **ACID gwarancje**. KWAS jest dobrze znanego akronim, zawiera cztery właściwości — niepodzielność, spójności, izolacji i trwałości.  

Krótko mówiąc, niepodzielność gwarantuje, że wszystkie hello pracy wewnątrz transakcji jest traktowany jako pojedyncza jednostka gdzie albo wszystkie dba lub none. Spójności upewnia się, że hello dane są zawsze w dobrym stanie wewnętrznego na przez transakcje. Izolacja gwarantuje, że żadne transakcje dwóch koliduje ze sobą — ogólnie rzecz biorąc, większość komercyjnych systemów zapewniają wiele poziomów izolacji, które mogą być używane zgodnie z wymaganiami aplikacji hello. Trwałość zapewnia żadnych zmian, które zostaje zatwierdzona w bazie danych hello zawsze będzie obecne.   

W bazie danych rozwiązania Cosmos, JavaScript jest hostowana na powitania tej samej przestrzeni pamięci jako hello bazy danych. W związku z tym żądań w ramach procedury składowane i wyzwalaczy wykonywany w hello sam zakresem sesji bazy danych. Dzięki temu DB rozwiązania Cosmos tooguarantee kwasu dla wszystkich operacji, które są częścią jednego procedury składowanej/wyzwalacza. Należy wziąć pod uwagę następujące hello przechowywane Definicja procedury:

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

Tę procedurę składowaną używa transakcji w elementach tootrade aplikacji gier, między dwóch graczy w ramach jednej operacji. Witaj przechowywane procedury prób tooread dwa dokumenty, które gracz toohello odpowiednie identyfikatory przekazany jako argument. Jeśli oba dokumenty player zostaną znalezione, następnie hello przechowywane procedury aktualizacji hello dokumentów przez zamianę ich elementów. Jeśli nie zostaną napotkane błędy wzdłuż sposób hello, zgłasza wyjątek JavaScript, która niejawnie przerywa hello transakcji.

Jeśli hello kolekcji hello przechowywane procedury został zarejestrowany przed to kolekcja jednej partycji, a następnie hello transakcji jest zakresem tooall hello dokumentów w kolekcji hello. Jeśli kolekcja hello jest podzielona na partycje, procedury składowane są wykonywane w zakresie transakcji hello klucza jednej partycji. Każdy składowanych, wykonywanie procedury następnie musi zawierać wartość klucza partycji odpowiedniej toohello zakresu hello transakcji musi być uruchamiana. Aby uzyskać więcej informacji, zobacz [Azure rozwiązania Cosmos DB partycjonowania](partition-data.md).

### <a name="commit-and-rollback"></a>Przekazywania i wycofywania
Transakcje są głęboko i natywnie zintegrowane model programowania JavaScript DB rozwiązania Cosmos. Wewnątrz funkcji JavaScript wszystkie operacje są automatycznie zawijany w ramach jednej transakcji. Jeśli hello JavaScript zostaje ukończona bez żadnych wyjątków, bazy danych toohello operacji hello są zatwierdzone. W efekcie instrukcje "BEGIN TRANSACTION" i "COMMIT TRANSACTION" hello w relacyjnych baz danych są niejawne w bazie danych rozwiązania Cosmos.  

W przypadku dowolnego wyjątek, który jest propagowana ze skryptu hello środowiska wykonawczego języka JavaScript DB rozwiązania Cosmos cofnie hello cała transakcja. Jak pokazano wcześniej hello przykład generowania wyjątku jest skutecznie równoważne tooa "ROLLBACK TRANSACTION" w bazie danych rozwiązania Cosmos.

### <a name="data-consistency"></a>Spójność danych
Procedury składowane i wyzwalaczy są zawsze wykonywane na hello repliki podstawowej hello Azure DB rozwiązania Cosmos kontenera. Dzięki temu, że odczyty z wewnątrz przechowywane procedury oferta wysoki poziom spójności. Zapytania przy użyciu funkcji zdefiniowanych przez użytkownika mogą być wykonywane na powitania podstawowe lub pomocnicze repliki, ale Upewniamy się toomeet hello żądanego poziomu spójności, wybierając odpowiednie repliki hello.

## <a name="bounded-execution"></a>Ograniczonego wykonania
Wszystkie operacje rozwiązania Cosmos bazy danych należy wykonać w ramach serwera hello określony limit czasu żądania. To ograniczenie dotyczy również funkcje tooJavaScript (procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika). Jeśli operacja nie została zakończona z limitem czasu, hello transakcja zostanie wycofana. Funkcje kodu JavaScript musi zakończyć się przed upływem limitu czasu hello, lub zaimplementuj kontynuacji na podstawie modelu toobatch/wznawia wykonywanie.  

W kolejności toosimplify programowanie przechowywanych procedur i wyzwalaczy toohandle terminów, wszystkie funkcje w obiekcie kolekcji hello (dla tworzenia, odczytu, zastępowanie i usuwanie dokumentów i załączników) zwracają wartość logiczna, która reprezentuje czy który Operacja zostanie wykonana. Jeśli ta wartość wynosi false, to wskazanie, że limit czasu hello o tooexpire i tą procedurą hello musi dobiega końca wykonywania.  Pierwszy operacji magazynu niezaakceptowanych operacji w kolejce toohello wcześniejsze dotrą toocomplete, jeśli procedura przechowywana hello jest przeprowadzany w czasie i więcej żądań w kolejce.  

JavaScript — funkcje są również ograniczona zużycia zasobów. Rozwiązania cosmos DB rezerwuje przepływności na kolekcję na podstawie rozmiaru hello zainicjowano obsługę administracyjną konta bazy danych. Przepływność wyrażonych znormalizowane jednostki Procesora, pamięci i wywołać jednostki żądania lub RUs zużycie we/wy. Funkcje kodu JavaScript potencjalnie może zużywać dużą liczbę RUs w krótkim czasie i mogą zostać ograniczony szybkość po osiągnięciu limitu hello kolekcji. Procedury składowane znacznym zasobów może być również dostępność poddane kwarantannie tooensure operacji w bazie danych pierwotnych.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Przykład: Zbiorcze importowanie danych do programu bazy danych
Poniżej przedstawiono przykład procedury przechowywanej, która jest zapisywane dokumenty toobulk importu do kolekcji. Uwaga jak hello przechowywane procedury uchwytów ograniczonego wykonania sprawdzając hello Boolean wartość zwracana z createDocument, a następnie używa hello liczbę dokumentów dodaje w każdym wywołaniu hello przechowywane procedury postępu tootrack i Wznów w partiach.

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <a id="trigger"></a>Wyzwalacze bazy danych
### <a name="database-pre-triggers"></a>Wyzwalacze wstępne bazy danych
Rozwiązania cosmos DB udostępnia wyzwalacze, które są wykonywane lub wyzwolone przez operację na dokument. Na przykład można określić wstępne wyzwalacza, podczas tworzenia dokumentu — wstępne wyzwalacz zostanie uruchomiony przed utworzeniem hello dokumentu. Witaj poniżej przedstawiono przykładowy sposób wstępnego Wyzwalacze mogą być używane toovalidate hello właściwości dokumentu, który jest tworzony:

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


I hello odpowiadającego kodu Node.js rejestracji po stronie klienta dla wyzwalacza hello:

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


Wstępne wyzwalaczy nie może mieć parametrów wejściowych. Obiekt żądania Hello może być komunikat żądania hello używane toomanipulate skojarzony z hello operacji. W tym miejscu wyzwalacza wstępne hello jest uruchamiana z hello tworzenia dokumentu i treści komunikatu żądania hello zawiera toobe dokumentu hello utworzony w formacie JSON.   

Gdy wyzwalacze są zarejestrowane, użytkownicy mogą określić hello operacje, które można uruchomić z. Wyzwalacz został utworzony z TriggerOperation.Create, co oznacza, że następujące hello jest niedozwolone.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Wyzwalacze po bazy danych
Po wyzwalaczy, takich jak wstępne wyzwalacze są skojarzone z operacji w dokumencie i nie przyjmuje żadnych parametrów wejściowych. Zakres ich działania **po** hello operacja została zakończona i mają dostęp toohello odpowiedzi wysyłany komunikat toohello klienta.   

Hello poniższy przykład przedstawia po Wyzwalacze w akcji:

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


jak pokazano w hello następujące przykładowe można zarejestrować Hello wyzwalacza.

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


Wyzwalacz wysyła zapytanie hello dokument metadanych i aktualizuje ze szczegółami hello nowo utworzonego dokumentu.  

Rzecz, istotne hello jest toonote **transakcyjnych** wykonanie wyzwalaczy w bazie danych rozwiązania Cosmos. Po wyzwalacz uruchamia hello w ramach jednej transakcji, jak tworzenie hello hello oryginalnego dokumentu. W związku z tym jeśli z powitania po wyzwalacza (jeśli są nam dokument metadanych hello tooupdate powiedzieć) firma Microsoft zgłosić wyjątek, cała transakcja hello zakończy się niepowodzeniem i wycofana. Dokument nie zostanie utworzona i zostanie zwrócony wyjątek.  

## <a id="udf"></a>Funkcje zdefiniowane przez użytkownika
Funkcje zdefiniowane przez użytkownika (UDF) są gramatyki języka zapytań SQL usługi DocumentDB interfejsu API hello tooextend używane i implementować niestandardowe reguły biznesowe. Mogą one wywołać tylko z wewnątrz zapytań. Nie mają obiektu context toohello dostępu i mają toobe używany jako tylko do obliczeń JavaScript. W związku z tym funkcje UDF może działać w replikach pomocniczych hello usługi DB rozwiązania Cosmos.  

Hello poniższy przykład tworzy UDF toocalculate podatkowych oparte na szybkości dla różnych nawiasy przychodów, a następnie używa on wewnątrz toofind zapytania wszystkich osób, które płatnej ponad 20 000 $ w podatki.

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


Witaj UDF później mogą być używane w zapytaniach, podobnie jak w hello następujące przykładowe:

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a>Zapytanie o języku zintegrowanym JavaScript API
Ponadto tooissuing zapytania przy użyciu gramatyki SQL usługi DocumentDB, hello po stronie serwera SDK pozwala tooperform zoptymalizowanych pod kątem zapytań przy użyciu interfejs fluent JavaScript bez żadnych wiedzy programu SQL Server. Hello JavaScript zapytania interfejsu API pozwala tooprogrammatically kompilacji zapytań przez przekazanie funkcji predykatu w funkcji chainable wywołuje built-ins tablicy i popularnych bibliotek JavaScript, takich jak lodash składni znanych tooECMAScript5 firmy. Zapytania są analizowane przez toobe środowiska wykonawczego języka JavaScript hello wykonywane efektywne wykorzystanie indeksów Azure rozwiązania Cosmos DB.

> [!NOTE]
> `__`(o podwójnej precyzji podkreślenie) jest zbyt alias`getContext().getCollection()`.
> <br/>
> Innymi słowy, można użyć `__` lub `getContext().getCollection()` tooaccess hello JavaScript API zapytania.
> 
> 

Obsługiwane funkcje obejmują:

<ul>
<li>
<b>Chain().... wartość ([wywołania zwrotnego] [, opcje])</b>
<ul>
<li>
Rozpoczyna się value() od łańcuchowa wywołanie, które musi zostać zakończone.
</li>
</ul>
</li>
<li>
<b>Filtr (predicateFunction [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Filtruje hello wejściowych przy użyciu funkcji predykatu, która zwraca wartość PRAWDA/FAŁSZ w kolejności toofilter dokumentów wejściowych we/wy na powitania Wynikowy zestaw. Działa to podobnie tooa klauzuli WHERE instrukcji SQL.
</li>
</ul>
</li>
<li>
<b>mapy (transformationFunction [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Stosuje projekcji podane przekształcenia, która mapuje każdego elementu wejściowego tooa JavaScript obiektu lub wartości. To zachowanie podobne tooa klauzuli SELECT w języku SQL.
</li>
</ul>
</li>
<li>
<b>pluck ([propertyName] [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Jest to skrót do mapy, który wyodrębni hello wartość właściwości jednego z każdego elementu wejściowego.
</li>
</ul>
</li>
<li>
<b>spłaszczanie ([isShallow] [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Łączy i spłaszcza tablic z każdego elementu wejściowego w pojedynczą tablicę tooa. Podobne tooSelectMany w składniku LINQ to zachowanie.
</li>
</ul>
</li>
<li>
<b>sortBy ([predicate] [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Tworzy nowy zestaw dokumentów, sortując hello dokumentów w strumieniu dokument wejściowy hello rosnąco przy użyciu hello danego predykatu. To zachowanie podobne tooa klauzuli ORDER BY w języku SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending ([predicate] [, opcje] [, wywołania zwrotnego])</b>
<ul>
<li>
Tworzy nowy zestaw dokumentów, sortując hello dokumentów w strumieniu dokument wejściowy hello w kolejności malejącej, używając hello danego predykatu. To zachowanie podobne klauzuli ORDER BY x DESC tooa w języku SQL.
</li>
</ul>
</li>
</ul>


Podczas się wewnątrz predykatu lub selektora funkcje, hello następujące konstrukcje JavaScript uzyskać automatycznie zoptymalizowane toorun bezpośrednio na indeksy bazy danych rozwiązania Cosmos Azure:

* Operatory prosty: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Literały, w tym literału obiektu hello: {}
* var return

Witaj, który tworzy następujące JavaScript nie pobrać zoptymalizowane pod kątem indeksy bazy danych Azure rozwiązania Cosmos:

* Przepływ kontroli (np. Jeśli, podczas gdy)
* Wywołania funkcji

Aby uzyskać więcej informacji, zobacz nasze [JSDocs po stronie serwera](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Przykład: Zapisu przy użyciu interfejsu API zapytania JavaScript hello procedury składowanej
powitania po przykładowy kod jest przykładem sposobu użycia hello JavaScript API zapytania w kontekście hello procedury składowanej. Witaj procedury składowanej wstawia dokumentu, określonego przez parametr wejściowy i aktualizuje dokument metadanych, przy użyciu hello `__.filter()` metody minSize, maxSize i totalSize ustalane na podstawie właściwości size hello dokument wejściowy.

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a>Arkusz ze wskazówkami dotyczącymi tooJavascript SQL
Witaj poniższej tabeli przedstawiono różne zapytania SQL i hello odpowiednich zapytań języka JavaScript.

Z kwerendy SQL dokumentu klucze właściwości (np. `doc.id`) jest rozróżniana wielkość liter.

|SQL| JavaScript zapytania interfejsu API|Poniższy opis|
|---|---|---|
|WYBIERZ *<br>Z dokumentów| __.map(Function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc;<br>});|1|
|Wybierz docs.id, docs.message jako msg, docs.actions <br>Z dokumentów|__.map(Function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;Zwraca {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identyfikator: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|WYBIERZ *<br>Z dokumentów<br>WHERE docs.id="X998_Y998"|__.Filter(Function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc.id === "X998_Y998";<br>});|3|
|WYBIERZ *<br>Z dokumentów<br>GDZIE ARRAY_CONTAINS (dokumentów. Tagi, 123)|__.Filter(Function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;Zwraca x.Tags & & x.Tags.indexOf(123) > -1;<br>});|4|
|Wybierz docs.id, docs.message jako msg<br>Z dokumentów<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.Filter(Function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc.id === "X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(Function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identyfikator: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.Value();|5|
|Wybierz wartość tagu<br>Z dokumentów<br>Dołącz do dokumentów w tagu. Tagi<br>Docs._ts ORDER BY|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.Filter(Function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwróć dokumentu. Tagi & & Array.IsArray — (dokumentu. Znaczniki);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.Value()|6|

Witaj poniższymi opisami wyjaśnić, każdego zapytania w powyższej tabeli hello.
1. To powoduje wszystkie dokumenty (podzielony na strony z token kontynuacji) jako.
2. Identyfikator hello projektów, wiadomości (aliasem toomsg) i akcji z wszystkie dokumenty.
3. Zapytania dotyczące dokumentów za pomocą predykatu hello: id = "X998_Y998".
4. Zapytania dotyczące dokumentów, których właściwość tagów i tagów jest tablicą zawierającą wartość hello 123.
5. Zapytania dotyczące dokumentów z predykatem, id = "X998_Y998", a następnie identyfikator hello projektów i komunikatów (aliasem toomsg).
6. Filtry dla dokumentów, które mają właściwości tablicy, tagi, i sortuje hello wynikowy dokumentów przez właściwość sygnatury czasowej systemu _ts hello i następnie projektów + spłaszcza hello tagi tablicy.


## <a name="runtime-support"></a>Obsługa środowiska uruchomieniowego
[Interfejs API po stronie serwera usługi DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) zapewnia obsługę hello większość hello Typowe projektowanie funkcjami języka JavaScript jako standardowych przez [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Bezpieczeństwo
Procedury składowane JavaScript i wyzwalacze są w trybie piaskownicy tak, aby hello skutków skrypt nie nastąpił przeciek toohello innych bez pośrednictwa izolacji transakcji snapshot hello na poziomie bazy danych hello. środowiska wykonawcze Hello w puli, ale czyszczone kontekstu powitania po każdym uruchomieniu. Dlatego jest gwarantowane toobe bezpieczne z dowolnym niezamierzone skutki uboczne od siebie.

### <a name="pre-compilation"></a>Wstępna kompilacja
Procedur składowanych, wyzwalaczy i funkcji UDF są niejawnie prekompilowany toohello formatu kodu bajtów w kolejności tooavoid kompilacji koszt w momencie hello każde wywołanie skryptu. Dzięki temu wywołań procedury składowane są szybkie i ma niewielki rozmiar.

## <a name="client-sdk-support"></a>Obsługa zestawu SDK klienta
W przypadku dodawania toohello interfejsu API usługi DocumentDB dla [Node.js](documentdb-sdk-node.md) klienta, bazy danych Azure rozwiązania Cosmos jest [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), i [zestawów SDK Python](documentdb-sdk-python.md) dla hello interfejsu API usługi DocumentDB. Procedur składowanych, wyzwalaczy i funkcji UDF można tworzyć i wykonywane przy użyciu dowolnej z tych zestawów SDK oraz. powitania po przykładzie pokazano, jak toocreate i wykonywanie procedury przechowywanej za pomocą powitania klienta .NET. Należy zauważyć, jak typów .NET hello są przekazywane do hello procedurę składowaną w formacie JSON i odczytywania.

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


W tym przykładzie pokazano sposób toouse hello [interfejsu API platformy .NET usługi DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate wstępne wyzwalacza i Utwórz dokument z wyzwalaczem hello włączone. 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


I hello poniższy przykład przedstawia sposób toocreate użytkownika definiowania funkcji (UDF) i używać go w [zapytań SQL usługi DocumentDB interfejsu API](documentdb-sql-query.md).

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a>Interfejs API REST
Wszystkie operacje bazy danych rozwiązania Cosmos Azure mogą być wykonywane w sposób RESTful. Procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika może być zarejestrowany w kolekcji przy użyciu metody POST protokołu HTTP. Witaj poniżej przedstawiono przykładowy sposób tooregister procedury składowanej:

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


Witaj procedury składowanej jest zarejestrowany, wykonując przed hello identyfikatora URI żądania POST bazami danych/programu testdb/colls/testColl/sprocs z zawierających treść hello hello toocreate procedury składowanej. Wyzwalaczy i funkcji UDF można zarejestrować podobnie, wysyłając odpowiednio POST przed/wyzwalacze i /udfs.
To przechowywane procedury może następnie być wykonywane przez wystawienie żądania POST przed jego link do zasobu:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


W tym miejscu hello toohello wejściowe, przechowywane procedury są przekazywane w treści żądania hello. Należy pamiętać, że dane wejściowe hello jest przekazywany jako tablica JSON parametrów wejściowych. Hello pierwszej danej wejściowej procedury przyjmuje hello są przechowywane jako dokument, który jest treść odpowiedzi. Otrzymaliśmy odpowiedzi Hello jest następujący:

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


Wyzwalacze, w przeciwieństwie do procedur składowanych, nie można wykonać bezpośrednio. Zamiast tego są one wykonywane w ramach operacji w dokumencie. Można określić toorun wyzwalaczy hello z żądaniem korzystanie z nagłówków HTTP. Oto Hello toocreate żądania dokumentu.

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


Tutaj toobe wstępne wyzwalacza hello Uruchom z żądaniem hello jest określony w nagłówku x-ms-documentdb-pre-trigger-include hello. Odpowiednio żadne po wyzwalacze są podane w nagłówku x-ms-documentdb-post-trigger-include hello. Należy pamiętać, że zarówno przed i po wyzwalaczy można określić dla danego żądania.

## <a name="sample-code"></a>Przykładowy kod
Można znaleźć więcej przykładów kodu po stronie serwera (w tym [usuwanie zbiorcze](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), i [aktualizacji](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) na naszych [repozytorium GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Chcesz tooshare Twojego świetny procedury składowanej? Wyślij żądanie ściągnięcia! 

## <a name="next-steps"></a>Następne kroki
Po utworzeniu jednego lub więcej procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika utworzonych można załadować je i je wyświetlić w portalu Azure za pomocą Eksploratora danych hello.

Można również znaleźć hello następujących odwołań i zasoby przydatne w Twojej więcej informacji na temat programowania po stronie serwera bazy danych Azure rozwiązania Cosmos toolearn ścieżki:

* [Zestawy SDK Azure rozwiązania Cosmos bazy danych](documentdb-sdk-dotnet.md)
* [Studio usługi DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Rozszerzalność bezpieczne i przenośnych bazy danych](http://dl.acm.org/citation.cfm?id=276339) 
* [Architektura bazy danych zorientowane na usługę](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Hosting hello środowiska uruchomieniowego .NET programu Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

