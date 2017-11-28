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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="20013-104">Samouczek środowiska node.js: hello Użyj interfejsu API usługi DocumentDB w toocreate bazy danych Azure rozwiązania Cosmos aplikacja konsolowa Node.js</span><span class="sxs-lookup"><span data-stu-id="20013-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20013-105">.NET</span><span class="sxs-lookup"><span data-stu-id="20013-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="20013-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="20013-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="20013-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="20013-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="20013-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="20013-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="20013-109">Java</span><span class="sxs-lookup"><span data-stu-id="20013-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="20013-110">C++</span><span class="sxs-lookup"><span data-stu-id="20013-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="20013-111">Witaj toohello samouczek środowiska Node.js dla hello Azure rozwiązania Cosmos DB Node.js SDK!</span><span class="sxs-lookup"><span data-stu-id="20013-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="20013-112">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="20013-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="20013-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20013-113">We'll cover:</span></span>

* <span data-ttu-id="20013-114">Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="20013-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="20013-115">Instalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="20013-115">Setting up your application</span></span>
* <span data-ttu-id="20013-116">Tworzenie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="20013-116">Creating a node database</span></span>
* <span data-ttu-id="20013-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="20013-117">Creating a collection</span></span>
* <span data-ttu-id="20013-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="20013-118">Creating JSON documents</span></span>
* <span data-ttu-id="20013-119">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="20013-119">Querying hello collection</span></span>
* <span data-ttu-id="20013-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="20013-120">Replacing a document</span></span>
* <span data-ttu-id="20013-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="20013-121">Deleting a document</span></span>
* <span data-ttu-id="20013-122">Usuwanie bazy danych node hello</span><span class="sxs-lookup"><span data-stu-id="20013-122">Deleting hello node database</span></span>

<span data-ttu-id="20013-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="20013-123">Don't have time?</span></span> <span data-ttu-id="20013-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="20013-124">Don't worry!</span></span> <span data-ttu-id="20013-125">Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="20013-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="20013-126">Zobacz [uzyskać kompletne rozwiązanie hello](#GetSolution) Aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="20013-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="20013-127">Po ukończeniu samouczka środowiska Node.js hello, proszę głosowania hello użyj przycisków na powitania góry i u dołu tej strony toogive nam opinii.</span><span class="sxs-lookup"><span data-stu-id="20013-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="20013-128">Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.</span><span class="sxs-lookup"><span data-stu-id="20013-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="20013-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="20013-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="20013-130">Wymagania wstępne dotyczące samouczka środowiska Node.js hello</span><span class="sxs-lookup"><span data-stu-id="20013-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="20013-131">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="20013-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="20013-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20013-132">An active Azure account.</span></span> <span data-ttu-id="20013-133">Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20013-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="20013-134">Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="20013-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="20013-135">[Node.js](https://nodejs.org/) w wersji 0.10.29 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="20013-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="20013-136">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="20013-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="20013-137">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="20013-138">Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[skonfigurować aplikację Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="20013-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="20013-139">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[skonfigurować aplikację Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="20013-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="20013-140"><a id="SetupNode"></a>Krok 2: Konfigurowanie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="20013-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="20013-141">Otwórz swój ulubiony terminal.</span><span class="sxs-lookup"><span data-stu-id="20013-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="20013-142">Zlokalizuj hello folder lub katalog, w którym chcesz toosave aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="20013-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="20013-143">Utwórz dwa puste pliki JavaScript z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="20013-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="20013-144">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="20013-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="20013-145">W systemie Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="20013-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="20013-146">Zainstaluj moduł documentdb hello za pomocą programu npm.</span><span class="sxs-lookup"><span data-stu-id="20013-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="20013-147">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="20013-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="20013-148">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="20013-148">Great!</span></span> <span data-ttu-id="20013-149">Teraz, po zakończeniu instalacji, zacznijmy pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="20013-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="20013-150"><a id="Config"></a>Krok 3. Ustawianie konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="20013-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="20013-151">Otwórz plik ```config.js``` w ulubionym edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="20013-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="20013-152">Następnie, kopiowania i wklejania hello poniższy fragment kodu i ustawić właściwości ```config.endpoint``` i ```config.primaryKey``` tooyour bazy danych Azure rozwiązania Cosmos identyfikator uri punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="20013-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="20013-153">Obie te konfiguracje można znaleźć w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20013-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Samouczek środowiska node.js — zrzut ekranu przedstawiający hello portalu Azure przedstawiający konto bazy danych Azure rozwiązania Cosmos z AKTYWNYM Centrum hello wyróżnione hello przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello hello identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wartości i wyróżnione na powitania Bloku klucze — baza danych Node][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="20013-155">Skopiuj i Wklej hello ```database id```, ```collection id```, i ```JSON documents``` tooyour ```config``` obiekt poniżej, których wartość Twojej ```config.endpoint``` i ```config.authKey``` właściwości.</span><span class="sxs-lookup"><span data-stu-id="20013-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="20013-156">Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md) zamiast dodawać definicje dokumentów hello.</span><span class="sxs-lookup"><span data-stu-id="20013-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

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


<span data-ttu-id="20013-157">Hello bazy danych, kolekcji i definicje dokumentów będą pełnić funkcję bazy danych programu Azure rozwiązania Cosmos ```database id```, ```collection id```oraz danych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="20013-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="20013-158">Koniec wyeksportuj Twojej ```config``` obiektu, dzięki czemu można odwoływać się do niej w hello ```app.js``` pliku.</span><span class="sxs-lookup"><span data-stu-id="20013-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="20013-159"><a id="Connect"></a>Krok 4: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="20013-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="20013-160">Otwórz pusty ```app.js``` plik w edytorze tekstu hello.</span><span class="sxs-lookup"><span data-stu-id="20013-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="20013-161">Skopiuj i Wklej kod hello poniżej tooimport hello ```documentdb``` modułu i nowo utworzony ```config``` modułu.</span><span class="sxs-lookup"><span data-stu-id="20013-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="20013-162">Skopiuj i Wklej hello toouse kodu hello wcześniej zapisany ```config.endpoint``` i ```config.primaryKey``` toocreate nowego wystąpienia klasy DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="20013-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="20013-163">Teraz, gdy masz hello kodu tooinitialize hello Azure DB rozwiązania Cosmos klienta Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="20013-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="20013-164">Krok 5. Tworzenie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="20013-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="20013-165">Skopiuj i Wklej kod hello poniżej hello tooset stan HTTP nie można odnaleźć, hello url bazy danych i adres url kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="20013-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="20013-166">Te adresy URL określają sposób powitania klienta bazy danych rozwiązania Cosmos Azure znajdzie hello właściwej bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="20013-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="20013-167">A [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [metody createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="20013-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="20013-168">Baza danych jest hello kontenerem logicznym magazynu dokumentów podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="20013-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="20013-169">Skopiuj i Wklej hello **getDatabase** funkcji do utworzenia nowej bazy danych w pliku app.js hello hello ```id``` określone w hello ```config``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="20013-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="20013-170">Witaj funkcja sprawdzi, czy hello bazy danych z hello sam ```FamilyRegistry``` identyfikator nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="20013-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="20013-171">Jeśli istnieje, zostanie zwrócona ta baza danych zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="20013-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

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

<span data-ttu-id="20013-172">Skopiuj i wklej poniższy kod hello, których wartość hello **getDatabase** działania funkcji Pomocnik hello tooadd **zakończyć** która będzie drukować komunikat zakończenia hello i wywołanie hello zbyt**getDatabase** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

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

<span data-ttu-id="20013-173">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-174">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-174">Congratulations!</span></span> <span data-ttu-id="20013-175">Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="20013-176"><a id="CreateColl"></a>Krok 6. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="20013-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="20013-177">Metoda **CreateDocumentCollectionAsync** utworzy nową kolekcję, co ma implikacje cenowe.</span><span class="sxs-lookup"><span data-stu-id="20013-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="20013-178">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="20013-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="20013-179">A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="20013-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="20013-180">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="20013-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="20013-181">Skopiuj i Wklej hello **getCollection** funkcja poniżej hello **getDatabase** działać w toocreate pliku app.js hello nowej kolekcji z hello ```id``` określone w hello ```config```obiektu.</span><span class="sxs-lookup"><span data-stu-id="20013-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="20013-182">Ponownie sprawdzimy toomake się, że kolekcja o hello sam ```FamilyCollection``` identyfikator nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="20013-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="20013-183">Jeśli istnieje, zostanie zwrócona ta kolekcja zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="20013-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

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

<span data-ttu-id="20013-184">Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getDatabase** tooexecute hello **getCollection** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="20013-185">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-186">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-186">Congratulations!</span></span> <span data-ttu-id="20013-187">Pomyślnie utworzono kolekcję usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="20013-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="20013-188"><a id="CreateDoc"></a>Krok 7. Tworzenie dokumentu</span><span class="sxs-lookup"><span data-stu-id="20013-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="20013-189">A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funkcja hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="20013-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="20013-190">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="20013-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="20013-191">Teraz można wstawić dokument do usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="20013-192">Skopiuj i Wklej hello **getFamilyDocument** funkcja poniżej hello **getCollection** funkcji tworzenia hello dokumentów zawierających dane JSON hello zapisane w hello ```config``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="20013-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="20013-193">Ponownie sprawdzimy toomake się, że dokument o hello, w tym samym identyfikatorze jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="20013-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

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

<span data-ttu-id="20013-194">Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getCollection** tooexecute hello **getFamilyDocument** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="20013-195">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-196">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-196">Congratulations!</span></span> <span data-ttu-id="20013-197">Pomyślnie utworzono dokument bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="20013-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Bazy danych węzła — Diagram pokazujący hello hierarchiczną relację między hello konta, hello bazy danych, hello kolekcji i dokumentów hello — samouczek środowiska node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="20013-199"><a id="Query"></a>Krok 8. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="20013-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="20013-200">Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="20013-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="20013-201">Witaj następujący przykładowy kod przedstawia zapytanie, które można uruchomić względem dokumentów hello w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="20013-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="20013-202">Skopiuj i Wklej hello **queryCollection** funkcja poniżej hello **getFamilyDocument** funkcji w pliku app.js hello.</span><span class="sxs-lookup"><span data-stu-id="20013-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="20013-203">Azure DB rozwiązania Cosmos obsługuje zapytania przypominającego SQL, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="20013-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="20013-204">Aby uzyskać więcej informacji dotyczących tworzenia złożonych kwerend, zapoznaj się hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo) i hello [dokumentację dotyczącą zapytań](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="20013-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

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


<span data-ttu-id="20013-205">powitania po diagram ilustruje sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="20013-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Bazy danych węzła — Diagram pokazujący hello zakres i znaczenie zapytania hello — samouczek środowiska node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="20013-207">Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="20013-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="20013-208">W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej.</span><span class="sxs-lookup"><span data-stu-id="20013-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="20013-209">Azure DB rozwiązania Cosmos wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="20013-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="20013-210">Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**getFamilyDocument** tooexecute hello **queryCollection** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="20013-211">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-212">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-212">Congratulations!</span></span> <span data-ttu-id="20013-213">Pomyślnie wykonano zapytanie względem dokumentów usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="20013-214"><a id="ReplaceDocument"></a>Krok 9. Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="20013-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="20013-215">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="20013-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="20013-216">Skopiuj i Wklej hello **replaceFamilyDocument** funkcja poniżej hello **queryCollection** funkcji w pliku app.js hello.</span><span class="sxs-lookup"><span data-stu-id="20013-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

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

<span data-ttu-id="20013-217">Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**queryCollection** tooexecute hello **replaceDocument** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="20013-218">Ponadto Dodaj toocall kodu hello **queryCollection** ponownie tooverify hello dokumentu został pomyślnie zmieniony.</span><span class="sxs-lookup"><span data-stu-id="20013-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="20013-219">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-220">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-220">Congratulations!</span></span> <span data-ttu-id="20013-221">Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="20013-222"><a id="DeleteDocument"></a>Krok 10. Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="20013-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="20013-223">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="20013-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="20013-224">Skopiuj i Wklej hello **deleteFamilyDocument** funkcja poniżej hello **replaceFamilyDocument** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

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

<span data-ttu-id="20013-225">Skopiuj i Wklej kod hello poniżej toohello wywołania hello drugi **queryCollection** tooexecute hello **deleteDocument** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="20013-226">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-227">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-227">Congratulations!</span></span> <span data-ttu-id="20013-228">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20013-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="20013-229"><a id="DeleteDatabase"></a>Krok 11: Usuwanie bazy danych Node hello</span><span class="sxs-lookup"><span data-stu-id="20013-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="20013-230">Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="20013-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="20013-231">Skopiuj i Wklej hello **oczyszczania** funkcja poniżej hello **deleteFamilyDocument** działanie tooremove hello w bazie danych i wszystkie zasoby podrzędne hello.</span><span class="sxs-lookup"><span data-stu-id="20013-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

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

<span data-ttu-id="20013-232">Skopiuj i Wklej hello kod poniżej wywołania hello zbyt**deleteFamilyDocument** tooexecute hello **oczyszczania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="20013-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="20013-233"><a id="Run"></a>Krok 12. Uruchamianie całej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="20013-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="20013-234">Cała sekwencja hello wywoływania funkcji powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="20013-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="20013-235">W terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="20013-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="20013-236">Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy hello.</span><span class="sxs-lookup"><span data-stu-id="20013-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="20013-237">Witaj dane wyjściowe powinny odpowiadać tekstowi przykładu hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="20013-237">hello output should match hello example text below.</span></span>

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

<span data-ttu-id="20013-238">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="20013-238">Congratulations!</span></span> <span data-ttu-id="20013-239">Utworzoną ukończeniu samouczka środowiska Node.js hello i ma swoją pierwszą aplikację konsoli bazy danych rozwiązania Cosmos Azure!</span><span class="sxs-lookup"><span data-stu-id="20013-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="20013-240"><a id="GetSolution"></a>Pobierz kompletnego rozwiązania samouczka hello Node.js</span><span class="sxs-lookup"><span data-stu-id="20013-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="20013-241">Jeśli nie masz czasu toocomplete hello kroków w tym samouczku, albo po prostu chcesz toodownload hello kodu, możesz pobrać go z [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="20013-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="20013-242">rozwiązania GetStarted hello toorun, który zawiera wszystkie przykłady hello w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="20013-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="20013-243">[Konto usługi Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="20013-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="20013-244">Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) rozwiązanie jest dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="20013-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="20013-245">Zainstaluj hello **documentdb** modułu za pomocą Menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="20013-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="20013-246">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="20013-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="20013-247">Następnie w hello ```config.js``` pliku wartości config.endpoint i config.authKey hello aktualizacji zgodnie z opisem w [krok 3: Ustawianie konfiguracji aplikacji](#Config).</span><span class="sxs-lookup"><span data-stu-id="20013-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="20013-248">Następnie w terminalu Znajdź Twojej ```app.js``` pliku i uruchom polecenie hello: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="20013-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="20013-249">To wszystko — skompiluj projekt i gotowe!</span><span class="sxs-lookup"><span data-stu-id="20013-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="20013-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20013-250">Next steps</span></span>
* <span data-ttu-id="20013-251">Potrzebujesz bardziej złożonego przykładu środowiska Node.js?</span><span class="sxs-lookup"><span data-stu-id="20013-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="20013-252">Zobacz [Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="20013-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="20013-253">Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="20013-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="20013-254">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="20013-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="20013-255">Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="20013-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
