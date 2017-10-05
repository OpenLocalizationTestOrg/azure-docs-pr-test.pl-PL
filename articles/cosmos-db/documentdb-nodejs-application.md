---
title: "Tworzenie aplikacji sieci web Node.js dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "W tym samouczku środowiska Node.js opisuje sposób korzystania z bazy danych programu Microsoft Azure rozwiązania Cosmos w celu przechowywania i uzyskiwanie dostępu do danych z aplikacji sieci web Node.js Express hostowanej przez usługę Azure Websites."
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
ms.openlocfilehash: 1a98509a98bcd2a5de593eb006f905766fe72966
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="85e1c-104"><a name="_Toc395783175"></a>Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85e1c-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85e1c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="85e1c-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="85e1c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="85e1c-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="85e1c-107">Java</span><span class="sxs-lookup"><span data-stu-id="85e1c-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="85e1c-108">Python</span><span class="sxs-lookup"><span data-stu-id="85e1c-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="85e1c-109">W tym samouczku środowiska Node.js pokazano sposób korzystania z bazy danych rozwiązania Cosmos Azure i interfejsu API usługi DocumentDB do przechowywania i uzyskiwanie dostępu do danych z poziomu aplikacji Node.js Express hostowanej przez usługę Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="85e1c-109">This Node.js tutorial shows you how to use Azure Cosmos DB and the DocumentDB API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="85e1c-110">Utworzysz prostą, opartą na sieci Web aplikację do zarządzania zadaniami (aplikację ToDo), która umożliwia tworzenie, pobieranie i kończenie zadań.</span><span class="sxs-lookup"><span data-stu-id="85e1c-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="85e1c-111">Zadania są przechowywane jako dokumenty JSON w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85e1c-111">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="85e1c-112">Ten samouczek zawiera szczegółowe omówienie tworzenia i rozwoju aplikacji oraz objaśnienie poszczególnych fragmentów kodu.</span><span class="sxs-lookup"><span data-stu-id="85e1c-112">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![Zrzut ekranu aplikacji My Todo List utworzonej w tym samouczku środowiska Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="85e1c-114">Nie masz czasu na ukończenie tego samouczka i po prostu chcesz uzyskać kompletne rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="85e1c-114">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="85e1c-115">Nie ma problemu, możesz pobrać kompletne przykładowe rozwiązanie z witryny [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="85e1c-115">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="85e1c-116">Aby uzyskać instrukcje dotyczące uruchomienia aplikacji, wystarczy przeczytać plik [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="85e1c-116">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <span data-ttu-id="85e1c-117"><a name="_Toc395783176"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="85e1c-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="85e1c-118">Ten samouczek środowiska Node.js zakłada, że masz już pewne doświadczenie w korzystaniu ze środowiska Node.js i usługi Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="85e1c-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="85e1c-119">Przed wykonaniem instrukcji zawartych w tym artykule upewnij się, że masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="85e1c-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="85e1c-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85e1c-120">An active Azure account.</span></span> <span data-ttu-id="85e1c-121">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="85e1c-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="85e1c-122">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85e1c-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="85e1c-123">LUB</span><span class="sxs-lookup"><span data-stu-id="85e1c-123">OR</span></span>

   <span data-ttu-id="85e1c-124">Lokalna instalacja [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) (tylko system Windows).</span><span class="sxs-lookup"><span data-stu-id="85e1c-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="85e1c-125">[Node.js][Node.js] w wersji 0.10.29 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="85e1c-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="85e1c-126">[Generator Express](http://www.expressjs.com/starter/generator.html) (można go zainstalować za pomocą polecenia `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="85e1c-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="85e1c-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="85e1c-127">[Git][Git].</span></span>

## <span data-ttu-id="85e1c-128"><a name="_Toc395637761"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85e1c-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="85e1c-129">Zacznijmy od utworzenia konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85e1c-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="85e1c-130">Jeśli masz już konto lub jeśli korzystasz z emulatora usługi Azure Cosmos DB na potrzeby tego samouczka, możesz od razu przejść do sekcji [Krok 2. Tworzenie nowej aplikacji Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="85e1c-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="85e1c-131"><a name="_Toc395783178"></a>Krok 2: Tworzenie nowej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="85e1c-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="85e1c-132">Teraz nauczysz się, jak utworzyć podstawowy projekt aplikacji Hello World w środowisku Node.js przy użyciu platformy [Express](http://expressjs.com/).</span><span class="sxs-lookup"><span data-stu-id="85e1c-132">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="85e1c-133">Otwórz swój ulubiony terminal, na przykład wiersz polecenia środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="85e1c-133">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="85e1c-134">Przejdź do katalogu, w którym chcesz przechowywać nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="85e1c-134">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="85e1c-135">Użyj generatora platformy Express, aby wygenerować nową aplikację o nazwie **todo**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-135">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="85e1c-136">Otwórz nowy katalog **todo** i zainstaluj zależności.</span><span class="sxs-lookup"><span data-stu-id="85e1c-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="85e1c-137">Uruchom nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="85e1c-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="85e1c-138">Swoją nową aplikację możesz wyświetlić, przechodząc w przeglądarce na adres [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="85e1c-138">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Poznaj środowisko Node.js — zrzut ekranu aplikacji Hello World w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="85e1c-140">Następnie, aby zatrzymać aplikację, w oknie terminalu naciśnij klawisze CTRL+C, po czym naciśnij klawisz **Y** w celu zakończenia zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="85e1c-140">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <span data-ttu-id="85e1c-141"><a name="_Toc395783179"></a>Krok 3. Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="85e1c-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="85e1c-142">Plik **package.json** jest jednym z plików utworzonych w folderze głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="85e1c-142">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="85e1c-143">Ten plik zawiera listę dodatkowych modułów, które są wymagane dla aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="85e1c-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="85e1c-144">Później podczas wdrażania tej aplikacji w usłudze Azure Websites, ten plik jest używany do określenia, które moduły muszą być zainstalowane na platformie Azure w celu obsługi tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85e1c-144">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="85e1c-145">Nadal trzeba zainstalować jeszcze dwa pakiety dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="85e1c-145">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="85e1c-146">Z poziomu terminala zainstaluj moduł **async** za pośrednictwem menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="85e1c-146">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="85e1c-147">Zainstaluj moduł **documentdb** za pomocą menedżera npm.</span><span class="sxs-lookup"><span data-stu-id="85e1c-147">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="85e1c-148">To jest moduł, gdzie sytuacji wszystkie magic bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="85e1c-148">This is the module where all the Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="85e1c-149">Szybkie sprawdzenie pliku **package.json** aplikacji powinno pokazać dodatkowe moduły.</span><span class="sxs-lookup"><span data-stu-id="85e1c-149">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="85e1c-150">Ten plik poinformuje platformę Azure, które pakiety pobrać i zainstalować podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85e1c-150">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="85e1c-151">Powinien on przypominać przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="85e1c-151">It should resemble the example below.</span></span>
   
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
   
    <span data-ttu-id="85e1c-152">W ten sposób węzeł (a potem platforma Azure) otrzyma informacje o tym, że aplikacja zależy od dodatkowych modułów.</span><span class="sxs-lookup"><span data-stu-id="85e1c-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="85e1c-153"><a name="_Toc395783180"></a>Krok 4. Korzystanie z usługi Azure Cosmos DB w aplikacji Node</span><span class="sxs-lookup"><span data-stu-id="85e1c-153"><a name="_Toc395783180"></a>Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="85e1c-154">To kończy całą wstępną instalację i konfigurację. Teraz przejdźmy do najważniejszej części tego samouczka, czyli napisania kodu za pomocą usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85e1c-154">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="85e1c-155">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="85e1c-155">Create the model</span></span>
1. <span data-ttu-id="85e1c-156">W katalogu projektu utwórz nowy katalog o nazwie **models** w tym samym katalogu, w którym znajduje się plik package.json.</span><span class="sxs-lookup"><span data-stu-id="85e1c-156">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="85e1c-157">W katalogu **models** utwórz nowy plik o nazwie **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-157">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="85e1c-158">Ten plik zawiera model dla zadań tworzonych przez naszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="85e1c-158">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="85e1c-159">W tym samym katalogu **models** utwórz nowy plik o nazwie **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-159">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="85e1c-160">Ten plik będzie zawierał pewną ilość przydatnego kodu do ponownego wykorzystania, który będzie używany w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85e1c-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="85e1c-161">Skopiuj poniższy kod do pliku**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="85e1c-161">Copy the following code in to **docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="85e1c-162">Zapisz i zamknij plik **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-162">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="85e1c-163">Na początku pliku **taskDao.js** dodaj następujący kod, aby odwołać się do elementu **DocumentDBClient** i pliku **docdbUtils.js**, które zostały utworzone powyżej:</span><span class="sxs-lookup"><span data-stu-id="85e1c-163">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="85e1c-164">Następnie dodasz kod w celu zdefiniowania i wyeksportowania obiektu Task.</span><span class="sxs-lookup"><span data-stu-id="85e1c-164">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="85e1c-165">Jest on odpowiedzialny za inicjowanie obiektu Task oraz konfigurowanie bazy danych i kolekcji dokumentów, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="85e1c-165">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="85e1c-166">Następnie dodaj poniższy kod, aby zdefiniować dodatkowe metody dla obiektu Task umożliwiające interakcje z danymi przechowywanymi w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85e1c-166">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="85e1c-167">Zapisz i zamknij plik **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-167">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="85e1c-168">Tworzenie kontrolera</span><span class="sxs-lookup"><span data-stu-id="85e1c-168">Create the controller</span></span>
1. <span data-ttu-id="85e1c-169">W katalogu **routes** projektu utwórz nowy plik o nazwie **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-169">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="85e1c-170">Dodaj następujący kod do pliku **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-170">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="85e1c-171">Służy on do ładowania modułów DocumentDBClient i async, które są używane przez plik **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-171">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="85e1c-172">Definiuje również funkcję **TaskList**, która przekazuje wystąpienie obiektu **Task** zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="85e1c-172">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="85e1c-173">Kontynuuj dodawanie do pliku **tasklist.js** przez dodanie metod **showTasks, addTask** i **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="85e1c-173">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="85e1c-174">Zapisz i zamknij plik **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-174">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="85e1c-175">Dodawanie pliku config.js</span><span class="sxs-lookup"><span data-stu-id="85e1c-175">Add config.js</span></span>
1. <span data-ttu-id="85e1c-176">W katalogu projektu utwórz nowy plik o nazwie **config.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="85e1c-177">Dodaj następujący kod do pliku **config.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-177">Add the following to **config.js**.</span></span> <span data-ttu-id="85e1c-178">Służy on do definiowania ustawień konfiguracji i wartości potrzebnych dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85e1c-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="85e1c-179">W pliku **config.js** zaktualizuj wartości kluczy HOST i AUTH_KEY przy użyciu wartości znajdujących się w bloku Klucze Twojego konta usługi Azure Cosmos DB w witrynie [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85e1c-179">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="85e1c-180">Zapisz i zamknij plik **config.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-180">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="85e1c-181">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="85e1c-181">Modify app.js</span></span>
1. <span data-ttu-id="85e1c-182">W katalogu projektu otwórz plik **app.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-182">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="85e1c-183">Ten plik został utworzony wcześniej podczas tworzenia aplikacji sieci Web platformy Express.</span><span class="sxs-lookup"><span data-stu-id="85e1c-183">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="85e1c-184">Dodaj następujący kod na górze pliku **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-184">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="85e1c-185">Ten kod definiuje plik konfiguracji, który ma być używany, oraz odczytuje wartości z tego pliku i umieszcza je w pewnych zmiennych, których będziemy wkrótce używać.</span><span class="sxs-lookup"><span data-stu-id="85e1c-185">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="85e1c-186">Zastąp następujące dwa wiersze w pliku **app.js**:</span><span class="sxs-lookup"><span data-stu-id="85e1c-186">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="85e1c-187">następującym fragmentem kodu:</span><span class="sxs-lookup"><span data-stu-id="85e1c-187">with the following snippet:</span></span>
   
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
5. <span data-ttu-id="85e1c-188">Te wiersze definiują nowe wystąpienie obiektu **TaskDao** z nowym połączeniem z usługą Azure Cosmos DB (przy użyciu wartości odczytanych z pliku **config.js**), inicjują obiekt zadania, a następnie wiążą akcje formularza z metodami w kontrolerze **TaskList**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-188">These lines define a new instance of our **TaskDao** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="85e1c-189">Na koniec zapisz i zamknij plik **app.js**. To już prawie koniec.</span><span class="sxs-lookup"><span data-stu-id="85e1c-189">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="85e1c-190"><a name="_Toc395783181"></a>Krok 5. Tworzenie interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="85e1c-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="85e1c-191">Teraz skupimy się na tworzeniu interfejsu użytkownika, aby użytkownik mógł faktycznie wchodzić w interakcję z naszą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="85e1c-191">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="85e1c-192">Utworzona aplikacja Express używa aparatu widoku **Jade**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-192">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="85e1c-193">Więcej informacji na temat aparatu Jade można znaleźć w witrynie [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="85e1c-193">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="85e1c-194">Plik **layout.jade** w katalogu **views** jest używany jako szablon globalny dla innych plików **jade**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-194">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="85e1c-195">W tym kroku zmodyfikujesz go w celu używania struktury [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi ułatwiającym projektowanie dobrze wyglądającej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="85e1c-195">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="85e1c-196">Otwórz plik **layout.jade** znajdujący się w folderze **views** i zastąp jego zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="85e1c-196">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

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

    <span data-ttu-id="85e1c-197">Ten kod w praktyce określa, że aparat **Jade** ma renderować kod HTML dla aplikacji, i tworzy **blok** o nazwie **content**, w którym można udostępnić układ dla stron zawartości.</span><span class="sxs-lookup"><span data-stu-id="85e1c-197">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="85e1c-198">Zapisz i zamknij ten plik **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="85e1c-199">Teraz otwórz plik **index.jade**, definiujący widok, który będzie używany przez naszą aplikację, i zastąp zawartość pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="85e1c-199">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
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
   

<span data-ttu-id="85e1c-200">Rozszerza on układ i udostępnia zawartość dla symbolu zastępczego **content**, który wcześniej widzieliśmy w pliku **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="85e1c-200">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="85e1c-201">W tym układzie utworzyliśmy dwa formularze HTML.</span><span class="sxs-lookup"><span data-stu-id="85e1c-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="85e1c-202">Pierwszy formularz zawiera tabelę danych i przycisk umożliwiający aktualizowanie elementów przez publikowanie do metody **/completetask** kontrolera.</span><span class="sxs-lookup"><span data-stu-id="85e1c-202">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="85e1c-203">Drugi formularz zawiera dwa pola wejściowe i przycisk umożliwiający utworzenie nowego elementu przez publikowanie do metody **/addtask** kontrolera.</span><span class="sxs-lookup"><span data-stu-id="85e1c-203">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="85e1c-204">To powinno być wszystko, czego potrzebujemy, aby nasza aplikacja działała.</span><span class="sxs-lookup"><span data-stu-id="85e1c-204">This should be all that we need for our application to work.</span></span>

## <span data-ttu-id="85e1c-205"><a name="_Toc395783181"></a>Krok 6. Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="85e1c-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="85e1c-206">Aby przetestować aplikację na komputerze lokalnym, w terminalu wykonaj polecenie `npm start` w celu uruchomienia aplikacji, a następnie odśwież stronę przeglądarki [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="85e1c-206">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="85e1c-207">Strona powinna teraz wyglądać podobnie jak na poniższym obrazie:</span><span class="sxs-lookup"><span data-stu-id="85e1c-207">The page should now look like the image below:</span></span>
   
    ![Zrzut ekranu aplikacji MyTodo List w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="85e1c-209">W przypadku wystąpienia błędu dotyczącego wcięcia w pliku layout.jade bądź index.jade upewnij się, że dwa pierwsze wiersze w obu plikach są wyrównane do lewej, bez spacji.</span><span class="sxs-lookup"><span data-stu-id="85e1c-209">If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="85e1c-210">Jeśli przed dwoma pierwszymi wierszami występują spacje, usuń je, zapisz oba pliki, a następnie odśwież okno przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="85e1c-210">If there are spaces before the first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="85e1c-211">Wprowadź nowe zadanie przy użyciu pól Item (Element), Item Name (Nazwa elementu) i Category (Kategoria), a następnie kliknij przycisk **Add Item** (Dodaj element).</span><span class="sxs-lookup"><span data-stu-id="85e1c-211">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="85e1c-212">Spowoduje to utworzenie w usłudze Azure Cosmos DB dokumentu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="85e1c-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="85e1c-213">Ta strona powinna zostać zaktualizowana w celu wyświetlenia nowo utworzonego elementu na liście ToDo.</span><span class="sxs-lookup"><span data-stu-id="85e1c-213">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Zrzut ekranu aplikacji z nowym elementem na liście ToDo](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="85e1c-215">Aby zakończyć zadanie, po prostu zaznacz pole wyboru w kolumnie Complete (Zakończ), a następnie kliknij przycisk **Update tasks** (Aktualizuj zadania).</span><span class="sxs-lookup"><span data-stu-id="85e1c-215">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="85e1c-216">Spowoduje to zaktualizowanie utworzonego już dokumentu.</span><span class="sxs-lookup"><span data-stu-id="85e1c-216">This updates the document you already created.</span></span>

5. <span data-ttu-id="85e1c-217">Aby zatrzymać aplikację, naciśnij klawisze CTRL+C w oknie terminalu, po czym naciśnij klawisz **Y** w celu zakończenia zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="85e1c-217">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <span data-ttu-id="85e1c-218"><a name="_Toc395783182"></a>Krok 7. Wdrażanie projektu tworzenia aplikacji w usłudze Azure Websites</span><span class="sxs-lookup"><span data-stu-id="85e1c-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="85e1c-219">Jeśli jeszcze tego nie zrobiono, włącz repozytorium Git dla usługi Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="85e1c-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="85e1c-220">Instrukcje, jak to zrobić, można znaleźć w temacie [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="85e1c-220">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="85e1c-221">Dodaj witrynę sieci Web platformy Azure jako element zdalny narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="85e1c-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="85e1c-222">Wdróż przez wypchnięcie do elementu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="85e1c-222">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="85e1c-223">W ciągu kilku sekund git zakończy publikowanie aplikacji sieci web i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="85e1c-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="85e1c-224">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="85e1c-224">Congratulations!</span></span> <span data-ttu-id="85e1c-225">Udało Ci się utworzyć swoją pierwszą aplikację internetową Node.js Express za pomocą usługi Azure Cosmos DB i opublikować ją w usłudze Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="85e1c-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="85e1c-226">Jeśli chcesz pobrać kompletną aplikację referencyjną dla tego samouczka lub się do niej odwołać, to jest ona dostępna do pobrania w repozytorium [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="85e1c-226">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="85e1c-227"><a name="_Toc395637775"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85e1c-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="85e1c-228">Czy chcesz wykonać testowanie wydajności i skalowania przy użyciu usługi Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="85e1c-228">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="85e1c-229">Zobacz [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) (Testowanie wydajności i skali w usłudze Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="85e1c-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="85e1c-230">Dowiedz się, jak [monitorować konto usługi Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="85e1c-230">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="85e1c-231">Uruchom zapytania względem naszego przykładowego zestawu danych na [placu zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="85e1c-231">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="85e1c-232">Zapoznaj się z [dokumentacją usługi Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="85e1c-232">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

