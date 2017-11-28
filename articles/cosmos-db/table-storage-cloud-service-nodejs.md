---
title: aaaWeb aplikacji z magazynem tabel (Node.js) | Dokumentacja firmy Microsoft
description: "Samouczek bazującą na powitania aplikacji sieci Web z samouczka Express przez dodanie usługi Azure Storage i hello modułu platformy Azure."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="a86ff-103">Aplikacja sieci Web node.js za pomocą magazynu</span><span class="sxs-lookup"><span data-stu-id="a86ff-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="a86ff-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a86ff-104">Overview</span></span>
<span data-ttu-id="a86ff-105">W tym samouczku hello aplikacji utworzony w [aplikacji sieci Web Node.js za pomocą ekspresowego] samouczka został rozszerzony za pomocą biblioteki klienta usługi Azure Microsoft hello dla toowork Node.js z usługami zarządzania danych.</span><span class="sxs-lookup"><span data-stu-id="a86ff-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="a86ff-106">Aplikację można rozszerzyć przez tworzenie wdrożenie tooAzure aplikacji opartych na sieci web listy zadań.</span><span class="sxs-lookup"><span data-stu-id="a86ff-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="a86ff-107">Lista zadań Hello pozwala użytkownikowi na pobieranie zadań, Dodaj nowe zadania i oznaczanie zadań jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="a86ff-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="a86ff-108">elementy zadań Hello są przechowywane w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a86ff-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="a86ff-109">Usługa Azure Storage udostępnia magazyn danych bez struktury, która jest odporna na uszkodzenia i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="a86ff-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="a86ff-110">Magazyn Azure obejmuje kilka struktury danych, gdzie można przechowywać i uzyskać dostęp do danych.</span><span class="sxs-lookup"><span data-stu-id="a86ff-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="a86ff-111">Można użyć usług magazynu hello z hello interfejsów API objęte hello Azure SDK dla środowiska Node.js lub za pośrednictwem interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="a86ff-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="a86ff-112">Aby uzyskać więcej informacji, zobacz [przechowywanie i uzyskiwanie dostępu do danych na platformie Azure].</span><span class="sxs-lookup"><span data-stu-id="a86ff-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="a86ff-113">Ten samouczek zakłada, że zostały wykonane hello [aplikacji sieci Web Node.js] i [Node.js z Express][aplikacji sieci Web Node.js za pomocą ekspresowego] samouczki.</span><span class="sxs-lookup"><span data-stu-id="a86ff-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="a86ff-114">Zawiera ona hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="a86ff-114">It contains hello following information:</span></span>

* <span data-ttu-id="a86ff-115">Jak toowork z hello aparatu Jade szablonu</span><span class="sxs-lookup"><span data-stu-id="a86ff-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="a86ff-116">Jak toowork z usługami Azure zarządzanie danymi</span><span class="sxs-lookup"><span data-stu-id="a86ff-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="a86ff-117">powitania po zrzut ekranu przedstawia aplikacji hello zakończone:</span><span class="sxs-lookup"><span data-stu-id="a86ff-117">hello following screenshot shows hello completed application:</span></span>

![Witaj ukończone strony sieci web w programie internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="a86ff-119">Ustawianie poświadczeń magazynu w pliku Web.Config</span><span class="sxs-lookup"><span data-stu-id="a86ff-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="a86ff-120">Należy podać w tooaccess poświadczenia magazynu usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a86ff-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="a86ff-121">Jest to realizowane przy użyciu ustawienia aplikacji hello pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="a86ff-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="a86ff-122">Ustawienia pliku web.config Hello są przekazywane jako tooNode zmienne środowiskowe, przypadków, które następnie są odczytywane przez hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="a86ff-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="a86ff-123">Poświadczenia magazynu są używane tylko w przypadku, gdy aplikacja hello jest tooAzure wdrożone.</span><span class="sxs-lookup"><span data-stu-id="a86ff-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="a86ff-124">Podczas uruchamiania w emulatorze hello, aplikacja hello używa hello emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="a86ff-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="a86ff-125">Wykonaj hello następujące poświadczenia konta magazynu hello tooretrieve czynności i dodaj je toohello ustawienia pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="a86ff-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="a86ff-126">Jeśli go nie jest jeszcze otwarty, należy uruchomić hello Azure PowerShell z hello **Start** menu rozwijając **wszystkie programy, Azure**, kliknij prawym przyciskiem myszy **programu Azure PowerShell**, a następnie wybierz  **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="a86ff-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="a86ff-127">Zmień katalogi toohello folderu zawierającego aplikację.</span><span class="sxs-lookup"><span data-stu-id="a86ff-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="a86ff-128">Na przykład C:\\węzła\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="a86ff-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="a86ff-129">Okno programu Azure Powershell hello wprowadź hello następujących informacji o koncie magazynu hello tooretrieve polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a86ff-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="a86ff-130">Witaj poprzednie polecenie cmdlet pobiera hello listę kont magazynu i klucze konta skojarzone z Twoją usługą hostowanej.</span><span class="sxs-lookup"><span data-stu-id="a86ff-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a86ff-131">Witaj zestawu Azure SDK tworzy konto magazynu, podczas wdrażania usługi, konto magazynu powinna już istnieć z wdrożenia aplikacji w poprzednim przewodnikach hello.</span><span class="sxs-lookup"><span data-stu-id="a86ff-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="a86ff-132">Otwórz hello **ServiceDefinition.csdef** pliku zawierającego ustawienia środowiska hello, które są używane, kiedy aplikacja hello jest wdrożony tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a86ff-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="a86ff-133">Wstaw hello poniższego bloku w obszarze **środowiska** elementu, zastępując {konta MAGAZYNU} i {klucz dostępu do MAGAZYNU} z nazwą konta hello i hello klucz podstawowy dla konta magazynu hello ma toouse wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="a86ff-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![zawartość pliku web.cloud.config Hello](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="a86ff-135">Zapisz plik hello i zamknij Notatnik.</span><span class="sxs-lookup"><span data-stu-id="a86ff-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="a86ff-136">Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="a86ff-136">Install additional modules</span></span>
1. <span data-ttu-id="a86ff-137">Hello Użyj następującego polecenia tooinstall hello [azure], [uuid węzła], [nconf] i [async] moduły lokalnie, jak również toosave wpis dla nich toohello **package.json** pliku:</span><span class="sxs-lookup"><span data-stu-id="a86ff-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="a86ff-138">Witaj dane wyjściowe tego polecenia powinien zostać wyświetlony podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a86ff-138">hello output of this command should appear similar toohello following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="a86ff-139">Przy użyciu usługi tabel hello w aplikacji node</span><span class="sxs-lookup"><span data-stu-id="a86ff-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="a86ff-140">W tej sekcji hello aplikacji w warstwie podstawowa utworzone przez hello **express** polecenia zostanie rozszerzony przez dodanie **task.js** plik zawierający hello model dla zadań.</span><span class="sxs-lookup"><span data-stu-id="a86ff-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="a86ff-141">Modyfikuj istniejący hello **app.js** plików i utworzyć nową **tasklist.js** pliku, który używa hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a86ff-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="a86ff-142">Tworzenie modelu hello</span><span class="sxs-lookup"><span data-stu-id="a86ff-142">Create hello model</span></span>
1. <span data-ttu-id="a86ff-143">W hello **WebRole1** katalogu, Utwórz nowy katalog o nazwie **modele**.</span><span class="sxs-lookup"><span data-stu-id="a86ff-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="a86ff-144">W hello **modele** katalogu, Utwórz nowy plik o nazwie **task.js**.</span><span class="sxs-lookup"><span data-stu-id="a86ff-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="a86ff-145">Ten plik zawiera model hello hello zadania utworzone przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="a86ff-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="a86ff-146">Na początku hello hello **task.js** plików, dodawanie hello następującego kodu tooreference wymagane biblioteki:</span><span class="sxs-lookup"><span data-stu-id="a86ff-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="a86ff-147">Następnie dodaj kod toodefine i wyeksportować hello obiektu zadania.</span><span class="sxs-lookup"><span data-stu-id="a86ff-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="a86ff-148">obiekt zadania Hello jest odpowiedzialny za łączenie toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="a86ff-148">hello Task object is responsible for connecting toohello table.</span></span>

    ```nodejs
    module.exports = Task;

    function Task(storageClient, tableName, partitionKey) {
      this.storageClient = storageClient;
      this.tableName = tableName;
      this.partitionKey = partitionKey;
      this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
        if(error) {
          throw error;
        }
      });
    };
    ```

5. <span data-ttu-id="a86ff-149">Następnie dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danymi przechowywanymi w tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="a86ff-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
          if(error) {
            callback(error);
          } else {
            callback(null, result.entries);
          }
        });
      },

      addItem: function(item, callback) {
        self = this;
        // use entityGenerator tooset types
        // NOTE: RowKey must be a string type, even though
        // it contains a GUID in this example.
        var itemDescriptor = {
          PartitionKey: entityGen.String(self.partitionKey),
          RowKey: entityGen.String(uuid()),
          name: entityGen.String(item.name),
          category: entityGen.String(item.category),
          completed: entityGen.Boolean(false)
        };

        self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
          if(error){
            callback(error);
          }
          callback(null);
        });
      },

      updateItem: function(rKey, callback) {
        self = this;
        self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
          if(error) {
            callback(error);
          }
          entity.completed._ = true;
          self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
            if(error) {
              callback(error);
            }
            callback(null);
          });
        });
      }
    }
    ```

6. <span data-ttu-id="a86ff-150">Zapisz i zamknij hello **task.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="a86ff-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="a86ff-151">Tworzenie kontrolera hello</span><span class="sxs-lookup"><span data-stu-id="a86ff-151">Create hello controller</span></span>
1. <span data-ttu-id="a86ff-152">W hello **WebRole1/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a86ff-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="a86ff-153">Dodaj hello zbyt następującego kodu**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a86ff-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="a86ff-154">Ten kod ładuje hello azure i modułów asynchronicznych, które są używane przez **tasklist.js** i definiuje hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** obiekt firma Microsoft zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="a86ff-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="a86ff-155">Kontynuować dodawanie toohello **tasklist.js** przez dodanie metody hello używane zbyt**showTasks**, **addTask**, i **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="a86ff-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
        var item = req.body.item;
        self.task.addItem(item, function itemAdded(error) {
          if(error) {
            throw error;
          }
          res.redirect('/');
        });
      },

      completeTask: function(req,res) {
        var self = this;
        var completedTasks = Object.keys(req.body);
        async.forEach(completedTasks, function taskIterator(completedTask, callback) {
          self.task.updateItem(completedTask, function itemsUpdated(error) {
            if(error){
              callback(error);
            } else {
              callback(null);
            }
          });
        }, function goHome(error){
          if(error) {
            throw error;
          } else {
            res.redirect('/');
          }
        });
      }
    }
    ```

4. <span data-ttu-id="a86ff-156">Zapisz hello **tasklist.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="a86ff-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="a86ff-157">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="a86ff-157">Modify app.js</span></span>
1. <span data-ttu-id="a86ff-158">W hello **WebRole1** hello katalogu, otwórz **app.js** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a86ff-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="a86ff-159">Na początku hello pliku hello, Dodaj powitania po tooload hello azure modułu i ustaw klucz nazwy i partycji tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="a86ff-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="a86ff-160">W pliku app.js hello, przewiń w dół toowhere widzisz hello następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="a86ff-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="a86ff-161">Zastąp hello poprzedzających wiersze z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="a86ff-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="a86ff-162">Ten kod inicjuje wystąpienie klasy <strong>zadań</strong> z kontem magazynu tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="a86ff-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="a86ff-163">Hello <strong>zadań</strong> jest przekazywany toohello <strong>TaskList</strong>, który używa on toocommunicate z usługi tabel hello:</span><span class="sxs-lookup"><span data-stu-id="a86ff-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="a86ff-164">Zapisz hello **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="a86ff-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="a86ff-165">Zmodyfikuj widok indeksu hello</span><span class="sxs-lookup"><span data-stu-id="a86ff-165">Modify hello index view</span></span>
1. <span data-ttu-id="a86ff-166">Zmień katalogi toohello **widoków** hello katalogu i Otwórz **index.jade** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a86ff-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="a86ff-167">Zamień zawartość hello hello **index.jade** pliku z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="a86ff-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="a86ff-168">Ten kod definiuje hello widok, aby wyświetlić istniejące zadania i definiuje formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="a86ff-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
    extends layout

    block content
      h1= title
      br

      form(action="/completetask", method="post")
        table.table.table-striped.table-bordered
          tr
            td Name
            td Category
            td Date
            td Complete
          if tasks != []
            tr
              td
          else
            each task in tasks
              tr
                td #{task.name._}
                td #{task.category._}
                - var day   = task.Timestamp._.getDate();
                - var month = task.Timestamp._.getMonth() + 1;
                - var year  = task.Timestamp._.getFullYear();
                td #{month + "/" + day + "/" + year}
                td
                  input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
        button.btn(type="submit") Update tasks
      hr
      form.well(action="/addtask", method="post")
        label Item Name:
        input(name="item[name]", type="textbox")
        label Item Category:
        input(name="item[category]", type="textbox")
        br
        button.btn(type="submit") Add item
    ```

3. <span data-ttu-id="a86ff-169">Zapisz i Zamknij **index.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="a86ff-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="a86ff-170">Modyfikuj hello układ globalne</span><span class="sxs-lookup"><span data-stu-id="a86ff-170">Modify hello global layout</span></span>
<span data-ttu-id="a86ff-171">Witaj **layout.jade** pliku w hello **widoków** katalog jest używany jako szablon globalny dla innych **jade** plików.</span><span class="sxs-lookup"><span data-stu-id="a86ff-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="a86ff-172">W tym kroku, należy zmodyfikować hello **layout.jade** pliku toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a86ff-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="a86ff-173">Pobierać i wyodrębniać pliki hello [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="a86ff-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="a86ff-174">Hello kopiowania **bootstrap.min.css** pliku z hello **bootstrap\\dist\\css** toohello folderu **publicznego\\arkusze stylów** Katalog aplikacji tasklist.</span><span class="sxs-lookup"><span data-stu-id="a86ff-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="a86ff-175">Z hello **widoków** folder, otwórz hello **layout.jade** plik w edytorze tekstu i Zastąp zawartość hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a86ff-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="a86ff-176">Tytuł head doctype html html = łącze do tytułu (rel = "stylesheet', href='/stylesheets/bootstrap.min.css) łącza (rel ="stylesheet', href='/stylesheets/style.css) body.app nav.navbar.navbar domyślną nagłówka div.navbar a.navbar-brand(href='/') zawartości bloku Moje zadania</span><span class="sxs-lookup"><span data-stu-id="a86ff-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="a86ff-177">Zapisz hello **layout.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="a86ff-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="a86ff-178">Uruchamianie aplikacji hello w hello emulatora</span><span class="sxs-lookup"><span data-stu-id="a86ff-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="a86ff-179">Użyj następującego polecenia toostart hello aplikacji w emulatorze hello hello.</span><span class="sxs-lookup"><span data-stu-id="a86ff-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="a86ff-180">Przeglądarka Hello otwiera i wyświetla hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="a86ff-180">hello browser opens and displays hello following page:</span></span>

![Sieć web stronicowanej zatytułowany Moje listy zadań z tabeli zawierającej tooadd zadania i pola nowe zadanie.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="a86ff-182">Użyj pozycji tooadd formularza hello, lub usuń istniejące elementy oznaczając je jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="a86ff-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="a86ff-183">Publikowanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a86ff-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="a86ff-184">W oknie programu Windows PowerShell hello wywołać hello następującego polecenia cmdlet tooredeploy tooAzure Twojego usługi hostowanej.</span><span class="sxs-lookup"><span data-stu-id="a86ff-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="a86ff-185">Zastąp **myuniquename** z unikatową nazwę dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a86ff-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="a86ff-186">Zastąp **datacentername** o nazwie hello centrum danych Azure, takich jak **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="a86ff-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="a86ff-187">Po zakończeniu wdrażania hello powinny być widoczne następujące toohello podobne odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="a86ff-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="a86ff-188">Określając hello **— uruchamianie** opcji hello poprzednie polecenie cmdlet przeglądarki hello otwiera i wyświetla aplikacji działających na platformie Azure po zakończeniu publikowania.</span><span class="sxs-lookup"><span data-stu-id="a86ff-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Strona Moje listy zadań hello okna przeglądarki.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="a86ff-191">Zatrzymywanie i usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a86ff-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="a86ff-192">Po wdrożeniu aplikacji, może być toodisable, można uniknąć kosztów lub tworzenia i wdrażania innych aplikacji w obrębie hello wolne okresu próbnego.</span><span class="sxs-lookup"><span data-stu-id="a86ff-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="a86ff-193">Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera.</span><span class="sxs-lookup"><span data-stu-id="a86ff-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="a86ff-194">Czas serwera jest używany, gdy aplikacja jest wdrażana, nawet jeśli wystąpienia nie zostały uruchomione i są w stanie hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="a86ff-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="a86ff-195">Witaj poniższej procedurze pokazano, jak toostop i usuwania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a86ff-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="a86ff-196">W oknie programu PowerShell Windows hello Zatrzymaj wdrożenie usługi hello utworzony w poprzedniej sekcji hello z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a86ff-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="a86ff-197">Zatrzymywanie usługi hello może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a86ff-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="a86ff-198">Witaj, usługa zostanie zatrzymana, pojawi się komunikat wskazujący, że usługa została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="a86ff-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="a86ff-199">Usługa hello toodelete, wywołanie hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a86ff-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="a86ff-200">Po wyświetleniu monitu wprowadź **Y** toodelete hello usługi.</span><span class="sxs-lookup"><span data-stu-id="a86ff-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="a86ff-201">Usuwanie hello usługi może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a86ff-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="a86ff-202">Po usunięciu usługi hello, zostanie wyświetlony komunikat informujący, że usługa hello została usunięta.</span><span class="sxs-lookup"><span data-stu-id="a86ff-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[aplikacji sieci Web Node.js za pomocą ekspresowego]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[przechowywanie i uzyskiwanie dostępu do danych na platformie Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplikacji sieci Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


