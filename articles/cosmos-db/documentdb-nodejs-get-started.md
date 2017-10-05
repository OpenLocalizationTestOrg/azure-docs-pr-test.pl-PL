---
title: "Samouczek środowiska Node.js dotyczący interfejsu API usługi DocumentDB dla usługi Azure Cosmos DB | Microsoft Docs"
description: "Samouczek środowiska Node.js, który tworzy bazę danych Cosmos DB przy użyciu interfejsu API usługi DocumentDB."
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
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="f3822-104">Samouczek środowiska node.js: tworzenie aplikacji konsoli Node.js za pomocą interfejsu API usługi DocumentDB w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="f3822-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3822-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f3822-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f3822-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f3822-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f3822-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="f3822-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f3822-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3822-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f3822-109">Java</span><span class="sxs-lookup"><span data-stu-id="f3822-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f3822-110">C++</span><span class="sxs-lookup"><span data-stu-id="f3822-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f3822-111">Witamy w samouczku środowiska Node.js dla zestawu SDK środowiska Node.js usługi Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="f3822-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="f3822-112">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="f3822-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f3822-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f3822-113">We'll cover:</span></span>

* <span data-ttu-id="f3822-114">Tworzenie konta usługi Azure Cosmos DB i łączenie się z nim</span><span class="sxs-lookup"><span data-stu-id="f3822-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="f3822-115">Instalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f3822-115">Setting up your application</span></span>
* <span data-ttu-id="f3822-116">Tworzenie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="f3822-116">Creating a node database</span></span>
* <span data-ttu-id="f3822-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="f3822-117">Creating a collection</span></span>
* <span data-ttu-id="f3822-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="f3822-118">Creating JSON documents</span></span>
* <span data-ttu-id="f3822-119">Wykonywanie zapytań względem kolekcji</span><span class="sxs-lookup"><span data-stu-id="f3822-119">Querying the collection</span></span>
* <span data-ttu-id="f3822-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f3822-120">Replacing a document</span></span>
* <span data-ttu-id="f3822-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f3822-121">Deleting a document</span></span>
* <span data-ttu-id="f3822-122">Usuwanie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="f3822-122">Deleting the node database</span></span>

<span data-ttu-id="f3822-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="f3822-123">Don't have time?</span></span> <span data-ttu-id="f3822-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="f3822-124">Don't worry!</span></span> <span data-ttu-id="f3822-125">Kompletne rozwiązanie jest dostępne w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f3822-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="f3822-126">Przejdź do sekcji [Pobieranie kompletnego rozwiązania](#GetSolution), aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="f3822-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f3822-127">Po ukończeniu samouczka środowiska Node.js użyj przycisków głosowania u góry lub u dołu tej strony, aby przesłać nam swoją opinię.</span><span class="sxs-lookup"><span data-stu-id="f3822-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="f3822-128">Jeśli chcesz, abyśmy skontaktowali się z Tobą bezpośrednio, możesz w komentarzach podać swój adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="f3822-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="f3822-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="f3822-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="f3822-130">Wymagania wstępne dla samouczka środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="f3822-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="f3822-131">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="f3822-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="f3822-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f3822-132">An active Azure account.</span></span> <span data-ttu-id="f3822-133">Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3822-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="f3822-134">Na potrzeby tego samouczka możesz także użyć [emulatora usługi Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f3822-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="f3822-135">[Node.js](https://nodejs.org/) w wersji 0.10.29 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f3822-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f3822-136">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f3822-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f3822-137">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f3822-138">Jeśli masz już konto, którego chcesz użyć, możesz przejść od razu do [skonfigurować aplikację Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f3822-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="f3822-139">Jeśli używasz emulatora usługi Azure rozwiązania Cosmos bazy danych, wykonaj kroki opisane w temacie [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) skonfigurować emulatora i przejść od razu do [skonfigurować aplikację Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f3822-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f3822-140"><a id="SetupNode"></a>Krok 2: Konfigurowanie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="f3822-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="f3822-141">Otwórz swój ulubiony terminal.</span><span class="sxs-lookup"><span data-stu-id="f3822-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="f3822-142">Zlokalizuj folder lub katalog, w którym chcesz zapisać aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="f3822-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="f3822-143">Utwórz dwa puste pliki JavaScript za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="f3822-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="f3822-144">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="f3822-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="f3822-145">W systemie Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="f3822-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="f3822-146">Zainstaluj moduł documentdb za pomocą menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="f3822-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="f3822-147">Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f3822-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="f3822-148">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="f3822-148">Great!</span></span> <span data-ttu-id="f3822-149">Teraz, po zakończeniu instalacji, zacznijmy pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="f3822-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="f3822-150"><a id="Config"></a>Krok 3. Ustawianie konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="f3822-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="f3822-151">Otwórz plik ```config.js``` w ulubionym edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="f3822-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="f3822-152">Następnie, kopiowania i wklej poniższy fragment kodu oraz ustaw właściwości ```config.endpoint``` i ```config.primaryKey``` do bazy danych Azure rozwiązania Cosmos identyfikator uri punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="f3822-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="f3822-153">Obie te konfiguracje można znaleźć w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3822-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Samouczek środowiska node.js — wyróżniony zrzut ekranu portalu Azure przedstawiający konto bazy danych Azure rozwiązania Cosmos z AKTYWNYM Centrum, przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos i wartości identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wyróżnionymi w bloku klucze — Baza danych node][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="f3822-155">Skopiuj i wklej elementy ```database id```, ```collection id``` i ```JSON documents``` do obiektu ```config``` poniżej miejsca, w którym zostały ustawione właściwości ```config.endpoint``` i ```config.authKey```.</span><span class="sxs-lookup"><span data-stu-id="f3822-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="f3822-156">Jeśli masz już dane, które chcesz przechowywać w bazie danych, możesz użyć [narzędzia migracji danych](import-data.md) usługi Azure Cosmos DB zamiast dodawać definicje dokumentów.</span><span class="sxs-lookup"><span data-stu-id="f3822-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f3822-157">Bazy danych, kolekcji i definicje dokumentów będą pełnić funkcję bazy danych programu Azure rozwiązania Cosmos ```database id```, ```collection id```oraz danych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="f3822-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="f3822-158">Na koniec wyeksportuj obiekt ```config```, aby można było odwoływać się do niego w pliku ```app.js```.</span><span class="sxs-lookup"><span data-stu-id="f3822-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="f3822-159"><a id="Connect"></a> Krok 4. Łączenie się z kontem usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f3822-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="f3822-160">Otwórz pusty plik ```app.js``` w edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="f3822-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="f3822-161">Skopiuj i wklej kod poniżej, aby zaimportować moduł ```documentdb``` i nowo utworzony moduł ```config```.</span><span class="sxs-lookup"><span data-stu-id="f3822-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="f3822-162">Skopiuj i wklej kod, aby użyć wcześniej zapisanych właściwości ```config.endpoint``` i ```config.primaryKey``` do utworzenia nowego wystąpienia klasy DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="f3822-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="f3822-163">Teraz, gdy masz kod do zainicjowania klienta usługi Azure DB rozwiązania Cosmos Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3822-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="f3822-164">Krok 5. Tworzenie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="f3822-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="f3822-165">Skopiuj i wklej kod poniżej, aby ustawić stan HTTP, jeśli dane nie zostaną znalezione, adres URL bazy danych i adres URL kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f3822-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="f3822-166">Te adresy URL określają sposób klienta bazy danych rozwiązania Cosmos Azure znajdzie właściwej bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f3822-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="f3822-167">[Bazę danych](documentdb-resources.md#databases) można utworzyć za pomocą funkcji [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f3822-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f3822-168">Baza danych jest kontenerem logicznym magazynu dokumentów podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="f3822-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="f3822-169">Skopiuj i wklej funkcję **getDatabase** w celu utworzenia nowej bazy danych w pliku app.js z właściwością ```id``` określoną w obiekcie ```config```.</span><span class="sxs-lookup"><span data-stu-id="f3822-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f3822-170">Funkcja sprawdzi, czy istnieje baza danych o takim samym identyfikatorze ```FamilyRegistry```.</span><span class="sxs-lookup"><span data-stu-id="f3822-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="f3822-171">Jeśli istnieje, zostanie zwrócona ta baza danych zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="f3822-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f3822-172">Skopiuj i wklej kod poniżej miejsca ustawienia funkcji **getDatabase**, aby dodać funkcję pomocnika **exit**, która będzie drukować komunikat zakończenia i wywołanie funkcji **getDatabase**.</span><span class="sxs-lookup"><span data-stu-id="f3822-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-173">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-174">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-174">Congratulations!</span></span> <span data-ttu-id="f3822-175">Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="f3822-176"><a id="CreateColl"></a>Krok 6. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="f3822-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f3822-177">Metoda **CreateDocumentCollectionAsync** utworzy nową kolekcję, co ma implikacje cenowe.</span><span class="sxs-lookup"><span data-stu-id="f3822-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="f3822-178">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f3822-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="f3822-179">[Kolekcję](documentdb-resources.md#collections) można utworzyć za pomocą funkcji [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f3822-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f3822-180">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3822-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="f3822-181">Skopiuj i wklej funkcję **getCollection** poniżej funkcji **getDatabase** w pliku app.js w celu utworzenia nowej kolekcji z właściwością ```id``` określoną w obiekcie ```config```.</span><span class="sxs-lookup"><span data-stu-id="f3822-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f3822-182">Znowu sprawdzimy w celu upewnienia się, że kolekcja o takim samym identyfikatorze ```FamilyCollection``` jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f3822-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="f3822-183">Jeśli istnieje, zostanie zwrócona ta kolekcja zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="f3822-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f3822-184">Skopiuj i wklej kod poniżej wywołania funkcji **getDatabase**, aby wykonać funkcję **getCollection**.</span><span class="sxs-lookup"><span data-stu-id="f3822-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-185">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-186">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-186">Congratulations!</span></span> <span data-ttu-id="f3822-187">Pomyślnie utworzono kolekcję usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3822-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="f3822-188"><a id="CreateDoc"></a>Krok 7. Tworzenie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f3822-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="f3822-189">[Dokument](documentdb-resources.md#documents) można utworzyć za pomocą funkcji [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f3822-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f3822-190">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="f3822-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f3822-191">Teraz można wstawić dokument do usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="f3822-192">Skopiuj i wklej funkcję **getFamilyDocument** poniżej funkcji **getCollection** w celu utworzenia dokumentów zawierających dane JSON zapisane w obiekcie ```config```.</span><span class="sxs-lookup"><span data-stu-id="f3822-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="f3822-193">Znowu sprawdzimy w celu upewnienia się, że dokument o takim samym identyfikatorze jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f3822-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f3822-194">Skopiuj i wklej kod poniżej wywołania funkcji **getCollection**, aby wykonać funkcję **getFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f3822-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-195">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-196">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-196">Congratulations!</span></span> <span data-ttu-id="f3822-197">Pomyślnie utworzono dokument bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3822-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Samouczek środowiska Node.js — diagram pokazujący hierarchiczną relację między kontem, bazą danych, kolekcją i dokumentami — baza danych Node](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="f3822-199"><a id="Query"></a>Krok 8. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f3822-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f3822-200">Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f3822-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="f3822-201">Następujący przykładowy kod przedstawia zapytanie, które można uruchomić dla dokumentów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f3822-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="f3822-202">Skopiuj i wklej funkcję **queryCollection** poniżej funkcji **getFamilyDocument** w pliku app.js.</span><span class="sxs-lookup"><span data-stu-id="f3822-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="f3822-203">Azure DB rozwiązania Cosmos obsługuje zapytania przypominającego SQL, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f3822-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="f3822-204">Aby uzyskać więcej informacji na temat tworzenia złożonych zapytań, zobacz [plac zabaw dla zapytań](https://www.documentdb.com/sql/demo) i [dokumentację dotyczącą zapytań](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f3822-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f3822-205">Na poniższym diagramie przedstawiono, jak składnia zapytania SQL DB rozwiązania Cosmos Azure jest wywoływana względem kolekcji zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="f3822-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Samouczek środowiska Node.js — diagram pokazujący zakres i znaczenie zapytania — baza danych Node](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="f3822-207">[FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalne w zapytaniu, ponieważ zapytania bazy danych Azure rozwiązania Cosmos mają już zakres określony jako jedna kolekcja.</span><span class="sxs-lookup"><span data-stu-id="f3822-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="f3822-208">W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej.</span><span class="sxs-lookup"><span data-stu-id="f3822-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="f3822-209">Azure DB rozwiązania Cosmos będzie wywnioskować, że zmienne Families, root lub wybrana nazwa zmiennej, domyślnie odwołują się bieżącej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f3822-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="f3822-210">Skopiuj i wklej kod poniżej wywołania funkcji **getFamilyDocument**, aby wykonać funkcję **queryCollection**.</span><span class="sxs-lookup"><span data-stu-id="f3822-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-211">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-212">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-212">Congratulations!</span></span> <span data-ttu-id="f3822-213">Pomyślnie wykonano zapytanie względem dokumentów usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="f3822-214"><a id="ReplaceDocument"></a>Krok 9. Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f3822-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="f3822-215">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f3822-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="f3822-216">Skopiuj i wklej funkcję **replaceFamilyDocument** poniżej funkcji **queryCollection** w pliku app.js.</span><span class="sxs-lookup"><span data-stu-id="f3822-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f3822-217">Skopiuj i wklej kod poniżej wywołania funkcji **queryCollection**, aby wykonać funkcję **replaceDocument**.</span><span class="sxs-lookup"><span data-stu-id="f3822-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="f3822-218">Ponadto dodaj kod w celu ponownego wywołania funkcji **queryCollection**, aby sprawdzić, czy dokument został pomyślnie zmieniony.</span><span class="sxs-lookup"><span data-stu-id="f3822-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-219">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-220">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-220">Congratulations!</span></span> <span data-ttu-id="f3822-221">Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f3822-222"><a id="DeleteDocument"></a>Krok 10. Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f3822-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="f3822-223">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f3822-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="f3822-224">Skopiuj i wklej funkcję **deleteFamilyDocument** poniżej funkcji **replaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f3822-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f3822-225">Skopiuj i wklej kod poniżej wywołania drugiej funkcji **queryCollection**, aby wykonać funkcję **deleteDocument**.</span><span class="sxs-lookup"><span data-stu-id="f3822-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f3822-226">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-227">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-227">Congratulations!</span></span> <span data-ttu-id="f3822-228">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3822-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f3822-229"><a id="DeleteDatabase"></a>Krok 11. Usuwanie bazy danych Node</span><span class="sxs-lookup"><span data-stu-id="f3822-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="f3822-230">Usunięcie utworzonej bazy danych spowoduje usunięcie bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="f3822-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f3822-231">Skopiuj poniższą funkcję **cleanup** i wklej ją poniżej funkcji **deleteFamilyDocument**, aby usunąć bazę danych i wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="f3822-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="f3822-232">Skopiuj i wklej kod poniżej wywołania funkcji **deleteFamilyDocument**, aby wykonać funkcję **cleanup**.</span><span class="sxs-lookup"><span data-stu-id="f3822-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="f3822-233"><a id="Run"></a>Krok 12. Uruchamianie całej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="f3822-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="f3822-234">Cała sekwencja wywoływania funkcji powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="f3822-234">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="f3822-235">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f3822-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f3822-236">Powinny zostać wyświetlone dane wyjściowe aplikacji rozpoczynania pracy.</span><span class="sxs-lookup"><span data-stu-id="f3822-236">You should see the output of your get started app.</span></span> <span data-ttu-id="f3822-237">Dane wyjściowe powinny odpowiadać tekstowi przykładu poniżej.</span><span class="sxs-lookup"><span data-stu-id="f3822-237">The output should match the example text below.</span></span>

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
    Press any key to exit

<span data-ttu-id="f3822-238">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f3822-238">Congratulations!</span></span> <span data-ttu-id="f3822-239">Udało Ci się ukończyć samouczek środowiska Node.js i utworzyć swoją pierwszą aplikację konsolową usługi Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="f3822-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="f3822-240"><a id="GetSolution"></a>Pobieranie kompletnego rozwiązania samouczka środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="f3822-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="f3822-241">Jeśli nie masz czasu na ukończenie tego samouczka lub po prostu chcesz pobrać kod, możesz uzyskać go w serwisie [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f3822-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="f3822-242">Do uruchomienia rozwiązania GetStarted, które zawiera wszystkie przykłady znajdujące się w tym artykule, będą potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f3822-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="f3822-243">[Konto usługi Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="f3822-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="f3822-244">Rozwiązanie [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3822-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="f3822-245">Zainstaluj moduł **documentdb** za pomocą menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="f3822-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="f3822-246">Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f3822-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="f3822-247">Następnie w pliku ```config.js``` zaktualizuj wartości config.endpoint i config.authKey, zgodnie z opisem w sekcji [Krok 3. Ustawianie konfiguracji aplikacji](#Config).</span><span class="sxs-lookup"><span data-stu-id="f3822-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="f3822-248">W terminalu znajdź swój plik ```app.js```, a następnie uruchom polecenie: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f3822-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="f3822-249">To wszystko — skompiluj projekt i gotowe!</span><span class="sxs-lookup"><span data-stu-id="f3822-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f3822-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3822-250">Next steps</span></span>
* <span data-ttu-id="f3822-251">Potrzebujesz bardziej złożonego przykładu środowiska Node.js?</span><span class="sxs-lookup"><span data-stu-id="f3822-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="f3822-252">Zobacz [Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="f3822-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="f3822-253">Dowiedz się, jak [monitorować konto usługi Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f3822-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f3822-254">Uruchom zapytania względem naszego przykładowego zestawu danych na [placu zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f3822-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f3822-255">Dowiedz się więcej o modelu programowania w sekcji Dla deweloperów [strony dokumentacji usługi Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f3822-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
