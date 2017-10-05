---
title: "Tworzenie aplikacji bazy danych rozwiązania Cosmos Azure przy użyciu interfejsów API bazy danych MongoDB | Dokumentacja firmy Microsoft"
description: "Samouczek, która tworzy bazy danych online za pomocą interfejsów API usługi Azure rozwiązania Cosmos bazy danych dla bazy danych MongoDB."
keywords: "Przykłady bazy danych mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 433d2e585c884a10e7e923a0b27c179a95410d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="163b0-104">Tworzenie bazy danych Azure rozwiązania Cosmos: interfejs API dla aplikacji bazy danych MongoDB przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="163b0-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="163b0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="163b0-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="163b0-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="163b0-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="163b0-107">Java</span><span class="sxs-lookup"><span data-stu-id="163b0-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="163b0-108">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="163b0-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="163b0-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="163b0-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="163b0-110">C++</span><span class="sxs-lookup"><span data-stu-id="163b0-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="163b0-111">W tym przykładzie przedstawiono sposób tworzenia bazy danych Azure rozwiązania Cosmos: interfejs API dla aplikacji konsoli bazy danych MongoDB przy użyciu środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="163b0-111">This example shows you how to build an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="163b0-112">Aby użyć tego przykładu, należy:</span><span class="sxs-lookup"><span data-stu-id="163b0-112">To use this example, you must:</span></span>

* <span data-ttu-id="163b0-113">[Utwórz](create-mongodb-dotnet.md#create-account) bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="163b0-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="163b0-114">Pobieranie Twojej bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji.</span><span class="sxs-lookup"><span data-stu-id="163b0-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="163b0-115">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="163b0-115">Create the app</span></span>

1. <span data-ttu-id="163b0-116">Utwórz *app.js* pliku skopiuj i Wklej kod poniżej.</span><span class="sxs-lookup"><span data-stu-id="163b0-116">Create a *app.js* file and copy & paste the code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into the families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="163b0-117">Zmodyfikuj następujące zmienne w *app.js* plik na ustawienia konta (Znajdowanie użytkownika [ciąg połączenia](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="163b0-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="163b0-118">Otwórz swój ulubiony terminal, uruchom **npm zainstalować bazy danych mongodb — Zapisz**, następnie uruchom aplikację w usłudze **węzła app.js**</span><span class="sxs-lookup"><span data-stu-id="163b0-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="163b0-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="163b0-119">Next steps</span></span>
* <span data-ttu-id="163b0-120">Dowiedz się, jak [Użyj MongoChef](mongodb-mongochef.md) Twojego Azure DB rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="163b0-120">Learn how to [use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
