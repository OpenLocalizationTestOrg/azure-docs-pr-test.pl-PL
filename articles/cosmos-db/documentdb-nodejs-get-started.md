---
title: "Samouczek aaaNode.js dla interfejsu API usługi DocumentDB dla bazy danych Azure rozwiązania Cosmos hello | Dokumentacja firmy Microsoft"
description: "Samouczek środowiska Node.js, która tworzy DB rozwiązania Cosmos z hello interfejsu API usługi DocumentDB."
keywords: samouczek node.js, baza danych node
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Samouczek środowiska node.js: hello Użyj interfejsu API usługi DocumentDB w toocreate bazy danych Azure rozwiązania Cosmos aplikacja konsolowa Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js dla MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Witaj toohello samouczek środowiska Node.js dla hello Azure rozwiązania Cosmos DB Node.js SDK! W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.

Omówione zostaną następujące czynności:

* Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos
* Instalowanie aplikacji
* Tworzenie bazy danych Node
* Tworzenie kolekcji
* Tworzenie dokumentów JSON
* Wykonywanie zapytania hello kolekcji
* Zastępowanie dokumentu
* Usuwanie dokumentu
* Usuwanie bazy danych node hello

Nie masz czasu? Nie martw się! Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Zobacz [uzyskać kompletne rozwiązanie hello](#GetSolution) Aby uzyskać krótkie instrukcje.

Po ukończeniu samouczka środowiska Node.js hello, proszę głosowania hello użyj przycisków na powitania góry i u dołu tej strony toogive nam opinii. Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.

Teraz do dzieła!

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Wymagania wstępne dotyczące samouczka środowiska Node.js hello
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
    * Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.
* [Node.js](https://nodejs.org/) w wersji 0.10.29 lub nowszej.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Krok 1. Tworzenie konta usługi Azure Cosmos DB
Utwórzmy konto usługi Azure Cosmos DB. Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[skonfigurować aplikację Node.js](#SetupNode). Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[skonfigurować aplikację Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Krok 2: Konfigurowanie aplikacji Node.js
1. Otwórz swój ulubiony terminal.
2. Zlokalizuj hello folder lub katalog, w którym chcesz toosave aplikacji Node.js.
3. Utwórz dwa puste pliki JavaScript z hello następującego polecenia:
   * W systemie Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * W systemie Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Zainstaluj moduł documentdb hello za pomocą programu npm. Witaj Użyj następującego polecenia:
   * ```npm install documentdb --save```

Wspaniale! Teraz, po zakończeniu instalacji, zacznijmy pisanie kodu.

## <a id="Config"></a>Krok 3. Ustawianie konfiguracji aplikacji
Otwórz plik ```config.js``` w ulubionym edytorze tekstu.

Następnie, kopiowania i wklejania hello poniższy fragment kodu i ustawić właściwości ```config.endpoint``` i ```config.primaryKey``` tooyour bazy danych Azure rozwiązania Cosmos identyfikator uri punktu końcowego i klucz podstawowy. Obie te konfiguracje można znaleźć w hello [portalu Azure](https://portal.azure.com).

![Samouczek środowiska node.js — zrzut ekranu przedstawiający hello portalu Azure przedstawiający konto bazy danych Azure rozwiązania Cosmos z AKTYWNYM Centrum hello wyróżnione hello przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello hello identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wartości i wyróżnione na powitania Bloku klucze — baza danych Node][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Skopiuj i Wklej hello ```database id```, ```collection id```, i ```JSON documents``` tooyour ```config``` obiekt poniżej, których wartość Twojej ```config.endpoint``` i ```config.authKey``` właściwości. Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md) zamiast dodawać definicje dokumentów hello.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hello bazy danych, kolekcji i definicje dokumentów będą pełnić funkcję bazy danych programu Azure rozwiązania Cosmos ```database id```, ```collection id```oraz danych dokumentów.

Koniec wyeksportuj Twojej ```config``` obiektu, dzięki czemu można odwoływać się do niej w hello ```app.js``` pliku.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Krok 4: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos
Otwórz pusty ```app.js``` plik w edytorze tekstu hello. Skopiuj i Wklej kod hello poniżej tooimport hello ```documentdb``` modułu i nowo utworzony ```config``` modułu.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Skopiuj i Wklej hello toouse kodu hello wcześniej zapisany ```config.endpoint``` i ```config.primaryKey``` toocreate nowego wystąpienia klasy DocumentClient.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Teraz, gdy masz hello kodu tooinitialize hello Azure DB rozwiązania Cosmos klienta Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.

## <a name="step-5-create-a-node-database"></a>Krok 5. Tworzenie bazy danych Node
Skopiuj i Wklej kod hello poniżej hello tooset stan HTTP nie można odnaleźć, hello url bazy danych i adres url kolekcji hello. Te adresy URL określają sposób powitania klienta bazy danych rozwiązania Cosmos Azure znajdzie hello właściwej bazy danych i kolekcji.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [metody createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy. Baza danych jest hello kontenerem logicznym magazynu dokumentów podzielonym na partycje w kolekcjach.

Skopiuj i Wklej hello **getDatabase** funkcji do utworzenia nowej bazy danych w pliku app.js hello hello ```id``` określone w hello ```config``` obiektu. Witaj funkcja sprawdzi, czy hello bazy danych z hello sam ```FamilyRegistry``` identyfikator nie istnieje. Jeśli istnieje, zostanie zwrócona ta baza danych zamiast tworzenia nowej.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Skopiuj i wklej poniższy kod hello, których wartość hello **getDatabase** działania funkcji Pomocnik hello tooadd **zakończyć** która będzie drukować komunikat zakończenia hello i wywołanie hello zbyt**getDatabase** funkcji.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.

## <a id="CreateColl"></a>Krok 6. Tworzenie kolekcji
> [!WARNING]
> Metoda **CreateDocumentCollectionAsync** utworzy nową kolekcję, co ma implikacje cenowe. Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy. Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.

Skopiuj i Wklej hello **getCollection** funkcja poniżej hello **getDatabase** działać w toocreate pliku app.js hello nowej kolekcji z hello ```id``` określone w hello ```config```obiektu. Ponownie sprawdzimy toomake się, że kolekcja o hello sam ```FamilyCollection``` identyfikator nie istnieje. Jeśli istnieje, zostanie zwrócona ta kolekcja zamiast tworzenia nowej.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getDatabase** tooexecute hello **getCollection** funkcji.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie utworzono kolekcję usługi Azure DB rozwiązania Cosmos.

## <a id="CreateDoc"></a>Krok 7. Tworzenie dokumentu
A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy. Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Teraz można wstawić dokument do usługi Azure Cosmos DB.

Skopiuj i Wklej hello **getFamilyDocument** funkcja poniżej hello **getCollection** funkcji tworzenia hello dokumentów zawierających dane JSON hello zapisane w hello ```config``` obiektu. Ponownie sprawdzimy toomake się, że dokument o hello, w tym samym identyfikatorze jeszcze nie istnieje.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getCollection** tooexecute hello **getFamilyDocument** funkcji.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie utworzono dokument bazy danych Azure rozwiązania Cosmos.

![Bazy danych węzła — Diagram pokazujący hello hierarchiczną relację między hello konta, hello bazy danych, hello kolekcji i dokumentów hello — samouczek środowiska node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Krok 8. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB
Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji. Witaj następujący przykładowy kod przedstawia zapytanie, które można uruchomić względem dokumentów hello w kolekcji.

Skopiuj i Wklej hello **queryCollection** funkcja poniżej hello **getFamilyDocument** funkcji w pliku app.js hello. Azure DB rozwiązania Cosmos obsługuje zapytania przypominającego SQL, jak pokazano poniżej. Aby uzyskać więcej informacji dotyczących tworzenia złożonych kwerend, zapoznaj się hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo) i hello [dokumentację dotyczącą zapytań](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


powitania po diagram ilustruje sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony.

![Bazy danych węzła — Diagram pokazujący hello zakres i znaczenie zapytania hello — samouczek środowiska node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji. W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej. Azure DB rozwiązania Cosmos wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.

Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getFamilyDocument** tooexecute hello **queryCollection** funkcji.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie wykonano zapytanie względem dokumentów usługi Azure Cosmos DB.

## <a id="ReplaceDocument"></a>Krok 9. Zastępowanie dokumentu
Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.

Skopiuj i Wklej hello **replaceFamilyDocument** funkcja poniżej hello **queryCollection** funkcji w pliku app.js hello.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**queryCollection** tooexecute hello **replaceDocument** funkcji. Ponadto Dodaj toocall kodu hello **queryCollection** ponownie tooverify hello dokumentu został pomyślnie zmieniony.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.

## <a id="DeleteDocument"></a>Krok 10. Usuwanie dokumentu
Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.

Skopiuj i Wklej hello **deleteFamilyDocument** funkcja poniżej hello **replaceFamilyDocument** funkcji.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Skopiuj i Wklej kod hello poniżej toohello wywołania hello drugi **queryCollection** tooexecute hello **deleteDocument** funkcji.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Gratulacje! Pomyślnie usunięto dokument usługi Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Krok 11: Usuwanie bazy danych Node hello
Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).

Skopiuj i Wklej hello **oczyszczania** funkcja poniżej hello **deleteFamilyDocument** działanie tooremove hello w bazie danych i wszystkie zasoby podrzędne hello.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**deleteFamilyDocument** tooexecute hello **oczyszczania** funkcji.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Krok 12. Uruchamianie całej aplikacji Node.js
Cała sekwencja hello wywoływania funkcji powinna wyglądać następująco:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```

Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy hello. Witaj dane wyjściowe powinny odpowiadać tekstowi przykładu hello poniżej.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Gratulacje! Utworzoną ukończeniu samouczka środowiska Node.js hello i ma swoją pierwszą aplikację konsoli bazy danych rozwiązania Cosmos Azure!

## <a id="GetSolution"></a>Pobierz kompletnego rozwiązania samouczka hello Node.js
Jeśli nie masz czasu toocomplete hello kroków w tym samouczku, albo po prostu chcesz toodownload hello kodu, możesz pobrać go z [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

rozwiązania GetStarted hello toorun, który zawiera wszystkie przykłady hello w tym artykule, będą potrzebne następujące hello:

* [Konto usługi Azure Cosmos DB][create-account].
* Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) rozwiązanie jest dostępne w witrynie GitHub.

Zainstaluj hello **documentdb** modułu za pomocą Menedżera npm. Witaj Użyj następującego polecenia:

* ```npm install documentdb --save```

Następnie w hello ```config.js``` pliku wartości config.endpoint i config.authKey hello aktualizacji zgodnie z opisem w [krok 3: Ustawianie konfiguracji aplikacji](#Config). 

Następnie w terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello: ```node app.js```.

To wszystko — skompiluj projekt i gotowe! 

## <a name="next-steps"></a>Następne kroki
* Potrzebujesz bardziej złożonego przykładu środowiska Node.js? Zobacz [Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB](documentdb-nodejs-application.md).
* Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
