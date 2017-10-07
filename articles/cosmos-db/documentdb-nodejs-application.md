---
title: "Aplikacja sieci web Node.js dla bazy danych Azure rozwiązania Cosmos aaaBuild | Dokumentacja firmy Microsoft"
description: "W tym samouczku środowiska Node.js opisuje, jak toouse bazy danych programu Microsoft Azure rozwiązania Cosmos toostore i dostępu do danych z aplikacji sieci web Node.js Express hostowanej przez usługę Azure Websites."
keywords: "Projektowanie aplikacji, samouczek bazy danych, Poznaj środowisko node.js, samouczek środowiska node.js"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="27519-104"><a name="_Toc395783175"></a>Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="27519-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27519-105">.NET</span><span class="sxs-lookup"><span data-stu-id="27519-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="27519-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="27519-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="27519-107">Java</span><span class="sxs-lookup"><span data-stu-id="27519-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="27519-108">Python</span><span class="sxs-lookup"><span data-stu-id="27519-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="27519-109">W tym samouczku środowiska Node.js pokazano, jak toouse bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB toostore i danymi dostępu z poziomu aplikacji Node.js Express hostowanej przez usługę Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="27519-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="27519-110">Utworzysz prostą, opartą na sieci Web aplikację do zarządzania zadaniami (aplikację ToDo), która umożliwia tworzenie, pobieranie i kończenie zadań.</span><span class="sxs-lookup"><span data-stu-id="27519-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="27519-111">Witaj zadania są przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="27519-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="27519-112">Ten samouczek przeprowadzi Cię przez kolejne hello tworzenia i wdrażania aplikacji hello i opisano, co dzieje się w każdym fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="27519-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Zrzut ekranu przedstawiający hello aplikacji My Todo List utworzonej w tym samouczku środowiska Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="27519-114">Nie masz czasu toocomplete hello samouczka i po prostu chcesz tooget hello kompletne rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="27519-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="27519-115">Nie ma problemu, możesz uzyskać hello kompletne przykładowe rozwiązanie z [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="27519-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="27519-116">Tylko odczytać hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) pliku, aby uzyskać instrukcje dotyczące sposobu toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="27519-117"><a name="_Toc395783176"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="27519-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="27519-118">Ten samouczek środowiska Node.js zakłada, że masz już pewne doświadczenie w korzystaniu ze środowiska Node.js i usługi Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="27519-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="27519-119">Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="27519-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="27519-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="27519-120">An active Azure account.</span></span> <span data-ttu-id="27519-121">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="27519-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="27519-122">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27519-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="27519-123">LUB</span><span class="sxs-lookup"><span data-stu-id="27519-123">OR</span></span>

   <span data-ttu-id="27519-124">Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) (tylko system Windows).</span><span class="sxs-lookup"><span data-stu-id="27519-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="27519-125">[Node.js][Node.js] w wersji 0.10.29 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="27519-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="27519-126">[Generator Express](http://www.expressjs.com/starter/generator.html) (można go zainstalować za pomocą polecenia `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="27519-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="27519-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="27519-127">[Git][Git].</span></span>

## <span data-ttu-id="27519-128"><a name="_Toc395637761"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="27519-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="27519-129">Zacznijmy od utworzenia konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="27519-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="27519-130">Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: Tworzenie nowej aplikacji Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="27519-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="27519-131"><a name="_Toc395783178"></a>Krok 2: Tworzenie nowej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="27519-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="27519-132">Teraz nauczysz się toocreate podstawowego projektu Hello World Node.js przy użyciu hello [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="27519-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="27519-133">Otwórz swój ulubiony terminal, takich jak wiersza polecenia Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="27519-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="27519-134">Przejdź toohello katalogu, w którym mają toostore hello nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="27519-135">Użyj toogenerate express generator hello nową aplikację o nazwie **todo**.</span><span class="sxs-lookup"><span data-stu-id="27519-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="27519-136">Otwórz nowy katalog **todo** i zainstaluj zależności.</span><span class="sxs-lookup"><span data-stu-id="27519-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="27519-137">Uruchom nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="27519-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="27519-138">Możesz wyświetlić swoją nową aplikację, przechodząc w przeglądarce za[http://localhost: 3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="27519-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Poznaj środowisko Node.js — zrzut ekranu przedstawiający hello aplikacji Hello World w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="27519-140">Następnie toostop hello aplikacji, naciśnij klawisze CTRL + C w hello okno terminalu, a następnie kliknij przycisk **y** tooterminate hello wsadowym.</span><span class="sxs-lookup"><span data-stu-id="27519-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="27519-141"><a name="_Toc395783179"></a>Krok 3. Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="27519-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="27519-142">Witaj **package.json** plik jest jeden z plików hello tworzone w katalogu głównym hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="27519-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="27519-143">Ten plik zawiera listę dodatkowych modułów, które są wymagane dla aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="27519-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="27519-144">Później podczas wdrażania tej aplikacji tooAzure witryn sieci Web, ten plik jest używany toodetermine, które moduły muszą toobe zainstalowanym Azure toosupport aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="27519-145">Nadal musisz tooinstall dwa pakiety dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="27519-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="27519-146">W terminalu hello, zainstaluj hello **async** modułu za pomocą Menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="27519-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="27519-147">Zainstaluj hello **documentdb** modułu za pomocą Menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="27519-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="27519-148">Jest to moduł hello gdzie sytuacji wszystkie hello Azure DB rozwiązania Cosmos magic.</span><span class="sxs-lookup"><span data-stu-id="27519-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="27519-149">Szybkie sprawdzenie hello **package.json** pliku aplikacji hello powinny być widoczne w hello dodatkowych modułów.</span><span class="sxs-lookup"><span data-stu-id="27519-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="27519-150">Ten plik będzie Poinformuj Azure toodownload pakiety, które i zainstalować podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="27519-151">Powinien on przypominać przykład Witaj poniżej.</span><span class="sxs-lookup"><span data-stu-id="27519-151">It should resemble hello example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="27519-152">W ten sposób węzeł (a potem platforma Azure) otrzyma informacje o tym, że aplikacja zależy od dodatkowych modułów.</span><span class="sxs-lookup"><span data-stu-id="27519-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="27519-153"><a name="_Toc395783180"></a>Krok 4: Przy użyciu usługi Azure DB rozwiązania Cosmos hello w aplikacji node</span><span class="sxs-lookup"><span data-stu-id="27519-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="27519-154">Która zajmuje się wszystkie hello wstępną instalację i konfigurację, teraz załóżmy get dół toowhy jesteśmy tutaj i jest toowrite niektórych w kodzie za pomocą bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="27519-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="27519-155">Tworzenie modelu hello</span><span class="sxs-lookup"><span data-stu-id="27519-155">Create hello model</span></span>
1. <span data-ttu-id="27519-156">W katalogu projektu hello, Utwórz nowy katalog o nazwie **modele** hello — w tym samym katalogu co plik package.json hello.</span><span class="sxs-lookup"><span data-stu-id="27519-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="27519-157">W hello **modele** katalogu, Utwórz nowy plik o nazwie **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="27519-158">Ten plik zawiera model hello hello zadań tworzonych przez naszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="27519-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="27519-159">W hello sam **modele** katalogu, Utwórz nowy plik o nazwie **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="27519-160">Ten plik będzie zawierał pewną ilość przydatnego kodu do ponownego wykorzystania, który będzie używany w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="27519-161">Kopiuj hello poniższy kod w zbyt**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="27519-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="27519-162">Zapisz i zamknij hello **docdbUtils.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="27519-163">Na początku hello hello **taskDao.js** plików, dodawanie hello następującego kodu tooreference hello **DocumentDBClient** i hello **docdbUtils.js** utworzyliśmy powyżej:</span><span class="sxs-lookup"><span data-stu-id="27519-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="27519-164">Następnie zostanie Dodaj kod toodefine i wyeksportować hello obiektu zadania.</span><span class="sxs-lookup"><span data-stu-id="27519-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="27519-165">Jest on odpowiedzialny za inicjowanie obiektu Task oraz konfigurowanie hello bazy danych i kolekcji dokumentów, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="27519-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="27519-166">Następnie dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="27519-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="27519-167">Zapisz i zamknij hello **taskDao.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="27519-168">Tworzenie kontrolera hello</span><span class="sxs-lookup"><span data-stu-id="27519-168">Create hello controller</span></span>
1. <span data-ttu-id="27519-169">W hello **tras** katalogu projektu Utwórz nowy plik o nazwie **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="27519-170">Dodaj hello zbyt następującego kodu**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="27519-171">Spowoduje to załadowanie modułów hello DocumentDBClient i async, które są używane przez **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="27519-172">To też definiowany hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="27519-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="27519-173">Kontynuować dodawanie toohello **tasklist.js** przez dodanie metody hello używane zbyt**showTasks, addTask**, i **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="27519-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="27519-174">Zapisz i zamknij hello **tasklist.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="27519-175">Dodawanie pliku config.js</span><span class="sxs-lookup"><span data-stu-id="27519-175">Add config.js</span></span>
1. <span data-ttu-id="27519-176">W katalogu projektu utwórz nowy plik o nazwie **config.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="27519-177">Dodaje hello zbyt**config.js**.</span><span class="sxs-lookup"><span data-stu-id="27519-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="27519-178">Służy on do definiowania ustawień konfiguracji i wartości potrzebnych dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="27519-179">W hello **config.js** plików aktualizacji hello wartości HOST i AUTH_KEY przy użyciu wartości hello znajdujące się w bloku klucze hello konta bazy danych Azure rozwiązania Cosmos na powitania [portalu Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27519-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="27519-180">Zapisz i zamknij hello **config.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="27519-181">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="27519-181">Modify app.js</span></span>
1. <span data-ttu-id="27519-182">W katalogu projektu hello, otwórz hello **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="27519-183">Ten plik został utworzony wcześniej podczas tworzenia aplikacji sieci web Express hello.</span><span class="sxs-lookup"><span data-stu-id="27519-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="27519-184">Dodaj następującego kodu toohello początku hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="27519-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="27519-185">Ten kod definiuje toobe pliku config hello używane i przechodzi do niektóre zmienne, których będziemy wkrótce używać tooread wartości z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="27519-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="27519-186">Zastąp następujące dwa wiersze w hello **app.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="27519-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="27519-187">z powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="27519-187">with hello following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="27519-188">Te wiersze definiują nowe wystąpienie klasy naszych **TaskDao** obiektu z nowego tooAzure połączenia DB rozwiązania Cosmos (przy użyciu wartości hello odczytywać hello **config.js**), inicjowanie obiektu task hello i następnie wiążą akcje formularza toomethods na naszych **TaskList** kontrolera.</span><span class="sxs-lookup"><span data-stu-id="27519-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="27519-189">Na koniec Zapisz i zamknij hello **app.js** pliku, już prawie koniec.</span><span class="sxs-lookup"><span data-stu-id="27519-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="27519-190"><a name="_Toc395783181"></a>Krok 5. Tworzenie interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="27519-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="27519-191">Teraz możemy zacząć naszych interfejsu użytkownika hello toobuilding uwagi, użytkownik może faktycznie wchodzić w interakcję z naszą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="27519-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="27519-192">Witaj używa utworzona aplikacja Express **Jade** jako hello aparatu widoku.</span><span class="sxs-lookup"><span data-stu-id="27519-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="27519-193">Aby uzyskać więcej informacji na temat Jade można znaleźć zbyt[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="27519-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="27519-194">Witaj **layout.jade** pliku w hello **widoków** katalog jest używany jako szablon globalny dla innych **jade** plików.</span><span class="sxs-lookup"><span data-stu-id="27519-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="27519-195">W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="27519-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="27519-196">Otwórz hello **layout.jade** w hello można znaleźć pliku **widoków** folderu i Zastąp zawartość hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="27519-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="27519-197">Informuje hello **Jade** aparat toorender kod HTML dla aplikacji i tworzy **bloku** o nazwie **zawartości** którym można udostępnić układ hello naszej zawartości strony.</span><span class="sxs-lookup"><span data-stu-id="27519-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="27519-198">Zapisz i zamknij ten plik **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="27519-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="27519-199">Teraz Otwórz hello **index.jade** plik, hello widok, który będzie używany przez naszą aplikację i Zastąp zawartość pliku hello hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="27519-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="27519-200">To rozszerza on układ i udostępnia zawartość dla hello **zawartości** symbolu zastępczego widzieliśmy w hello **layout.jade** wcześniej.</span><span class="sxs-lookup"><span data-stu-id="27519-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="27519-201">W tym układzie utworzyliśmy dwa formularze HTML.</span><span class="sxs-lookup"><span data-stu-id="27519-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="27519-202">Witaj pierwszy formularz zawiera tabelę danych i przycisk umożliwiający wykonywanie elementów tooupdate przez zbyt księgowej**/completetask** metody kontrolera.</span><span class="sxs-lookup"><span data-stu-id="27519-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="27519-203">Witaj drugi formularz zawiera dwa pola wejściowe i przycisk umożliwiający wykonywanie toocreate nowy element przez zbyt księgowej**/addtask** metody kontrolera.</span><span class="sxs-lookup"><span data-stu-id="27519-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="27519-204">Powinno to być wszystkie wymagane dla toowork naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27519-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="27519-205"><a name="_Toc395783181"></a>Krok 6. Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="27519-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="27519-206">Aplikacja hello tootest na komputerze lokalnym, uruchom `npm start` w hello terminali toostart aplikacji, a następnie Odśwież Twojej [http://localhost: 3000](http://localhost:3000) strona przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="27519-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="27519-207">Strona Hello powinna wyglądać tak jak hello obraz poniżej:</span><span class="sxs-lookup"><span data-stu-id="27519-207">hello page should now look like hello image below:</span></span>
   
    ![Zrzut ekranu przedstawiający hello aplikacji MyTodo List w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="27519-209">Jeśli zostanie wyświetlony błąd o wcięcie hello w pliku layout.jade hello lub index.jade hello, upewnij się, że hello pierwsze dwa wiersze w obu plików jest wyrównane do lewej, nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="27519-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="27519-210">Jeśli istnieją spacje przed hello pierwsze dwa wiersze, usuń je, Zapisz oba pliki, a następnie odśwież okno przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="27519-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="27519-211">Użyj hello elementu, nazwę elementu i kategorii pól tooenter nowego zadania, a następnie kliknij przycisk **Dodaj element**.</span><span class="sxs-lookup"><span data-stu-id="27519-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="27519-212">Spowoduje to utworzenie w usłudze Azure Cosmos DB dokumentu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="27519-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="27519-213">Strona Hello należy zaktualizować hello toodisplay nowo utworzony element na liście ToDo hello.</span><span class="sxs-lookup"><span data-stu-id="27519-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Zrzut ekranu aplikacji hello z nowym elementem na liście ToDo hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="27519-215">toocomplete zadania, po prostu zaznacz pole wyboru hello w kolumnie pełną hello, a następnie kliknij **aktualizowanie zadań**.</span><span class="sxs-lookup"><span data-stu-id="27519-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="27519-216">Spowoduje to zaktualizowanie dokumentu hello już utworzone.</span><span class="sxs-lookup"><span data-stu-id="27519-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="27519-217">Aplikacja hello toostop, naciśnij klawisze CTRL + C w hello okno terminalu, a następnie kliknij przycisk **Y** tooterminate hello wsadowym.</span><span class="sxs-lookup"><span data-stu-id="27519-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="27519-218"><a name="_Toc395783182"></a>Krok 7: Wdrażanie tooAzure projektu Twojej aplikacji projektowanie witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="27519-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="27519-219">Jeśli jeszcze tego nie zrobiono, włącz repozytorium Git dla usługi Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="27519-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="27519-220">Instrukcje można znaleźć na temat toodo to w hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](../app-service-web/app-service-deploy-local-git.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="27519-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="27519-221">Dodaj witrynę sieci Web platformy Azure jako element zdalny narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="27519-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="27519-222">Wdróż przez wypchnięcie toohello zdalnego.</span><span class="sxs-lookup"><span data-stu-id="27519-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="27519-223">W ciągu kilku sekund git zakończy publikowanie aplikacji sieci web i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="27519-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="27519-224">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="27519-224">Congratulations!</span></span> <span data-ttu-id="27519-225">Możesz po prostu utworzone pierwszego Node.js Express aplikacji sieci Web przy użyciu bazy danych Azure rozwiązania Cosmos i opublikować ją tooAzure witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="27519-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="27519-226">Toodownload lub toohello kompletnej aplikacji referencyjnej można znaleźć w tym samouczku, można go pobrać z [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="27519-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="27519-227"><a name="_Toc395637775"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27519-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="27519-228">Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform?</span><span class="sxs-lookup"><span data-stu-id="27519-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="27519-229">Zobacz [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) (Testowanie wydajności i skali w usłudze Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="27519-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="27519-230">Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="27519-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="27519-231">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="27519-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="27519-232">Eksploruj hello [dokumentacji bazy danych Azure rozwiązania Cosmos](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="27519-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

