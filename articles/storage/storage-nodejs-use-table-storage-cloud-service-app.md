---
title: aaaWeb aplikacji z magazynem tabel (Node.js) | Dokumentacja firmy Microsoft
description: "Samouczek bazującą na powitania aplikacji sieci Web z samouczka Express przez dodanie usługi Azure Storage i hello modułu platformy Azure."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="cef81-103">Aplikacja sieci Web node.js za pomocą magazynu</span><span class="sxs-lookup"><span data-stu-id="cef81-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="cef81-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cef81-104">Overview</span></span>
<span data-ttu-id="cef81-105">W tym samouczku rozszerzy utworzony w aplikacji hello [aplikacji sieci Web Node.js za pomocą ekspresowego] samouczka za pomocą biblioteki klienta usługi Azure Microsoft hello toowork Node.js z usługami zarządzania danych.</span><span class="sxs-lookup"><span data-stu-id="cef81-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="cef81-106">Toocreate Twojej aplikacji może trwać do aplikacji opartych na sieci web listy zadań wdrożenie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cef81-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="cef81-107">Lista zadań Hello pozwala użytkownikowi na pobieranie zadań, Dodaj nowe zadania i oznaczanie zadań jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="cef81-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="cef81-108">elementy zadań Hello są przechowywane w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cef81-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="cef81-109">Usługa Azure Storage udostępnia magazyn danych bez struktury, która jest odporna na uszkodzenia i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="cef81-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="cef81-110">Magazyn Azure obejmuje kilka struktury danych, gdzie można przechowywać i uzyskiwanie dostępu do danych, a mogą korzystać z usług magazynu hello z hello interfejsów API objęte hello Azure SDK dla środowiska Node.js lub za pośrednictwem interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="cef81-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="cef81-111">Aby uzyskać więcej informacji, zobacz [przechowywanie i uzyskiwanie dostępu do danych na platformie Azure].</span><span class="sxs-lookup"><span data-stu-id="cef81-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="cef81-112">Ten samouczek zakłada, że zostały wykonane hello [aplikacji sieci Web Node.js] i [Node.js z Express][aplikacji sieci Web Node.js za pomocą ekspresowego] samouczki.</span><span class="sxs-lookup"><span data-stu-id="cef81-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="cef81-113">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="cef81-113">You will learn:</span></span>

* <span data-ttu-id="cef81-114">Jak toowork z hello aparatu Jade szablonu</span><span class="sxs-lookup"><span data-stu-id="cef81-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="cef81-115">Jak toowork z usługami Azure zarządzanie danymi</span><span class="sxs-lookup"><span data-stu-id="cef81-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="cef81-116">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="cef81-116">A screenshot of hello completed application is below:</span></span>

![Witaj ukończone strony sieci web w programie internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="cef81-118">Ustawianie poświadczeń magazynu w pliku Web.Config</span><span class="sxs-lookup"><span data-stu-id="cef81-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="cef81-119">tooaccess usługi Azure Storage, należy toopass poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="cef81-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="cef81-120">toodo, korzystanie z ustawienia pliku web.config aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cef81-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="cef81-121">Te ustawienia zostaną przekazane jako tooNode zmienne środowiskowe, które następnie są odczytywane przez hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="cef81-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="cef81-122">Poświadczenia magazynu są używane tylko w przypadku, gdy aplikacja hello jest tooAzure wdrożone.</span><span class="sxs-lookup"><span data-stu-id="cef81-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="cef81-123">Podczas uruchamiania w emulatorze hello, aplikacja hello użyje hello emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="cef81-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="cef81-124">Wykonaj hello następujące poświadczenia konta magazynu hello tooretrieve czynności i dodaj je toohello ustawienia pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="cef81-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="cef81-125">Jeśli go nie jest jeszcze otwarty, należy uruchomić hello Azure PowerShell z hello **Start** menu rozwijając **wszystkie programy, Azure**, kliknij prawym przyciskiem myszy **programu Azure PowerShell**, a następnie wybierz  **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="cef81-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="cef81-126">Zmień katalogi toohello folderu zawierającego aplikację.</span><span class="sxs-lookup"><span data-stu-id="cef81-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="cef81-127">Na przykład C:\\węzła\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="cef81-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="cef81-128">Z okna programu Azure Powershell hello wprowadź hello następujących informacji o koncie magazynu hello tooretrieve polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cef81-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="cef81-129">Pobiera to hello listę kont magazynu i konto klucze skojarzone z usługi hostowanej.</span><span class="sxs-lookup"><span data-stu-id="cef81-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cef81-130">Witaj zestawu Azure SDK tworzy konto magazynu, podczas wdrażania usługi, konto magazynu powinna już istnieć z wdrożenia aplikacji w poprzednim przewodnikach hello.</span><span class="sxs-lookup"><span data-stu-id="cef81-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="cef81-131">Otwórz hello **ServiceDefinition.csdef** pliku zawierającego ustawienia środowiska hello, które są używane, kiedy aplikacja hello jest wdrożony tooAzure:</span><span class="sxs-lookup"><span data-stu-id="cef81-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="cef81-132">Wstaw hello poniższego bloku w obszarze **środowiska** elementu, zastępując {konta MAGAZYNU} i {klucz dostępu do MAGAZYNU} z nazwą konta hello i hello klucz podstawowy dla konta magazynu hello ma toouse wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="cef81-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![zawartość pliku web.cloud.config Hello](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="cef81-134">Zapisz plik hello i zamknij Notatnik.</span><span class="sxs-lookup"><span data-stu-id="cef81-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="cef81-135">Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="cef81-135">Install additional modules</span></span>
1. <span data-ttu-id="cef81-136">Hello Użyj następującego polecenia tooinstall hello [azure], [uuid węzła], [nconf] i [async] moduły lokalnie, jak również toosave wpis dla nich toohello **package.json** pliku:</span><span class="sxs-lookup"><span data-stu-id="cef81-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="cef81-137">Witaj dane wyjściowe tego polecenia powinien zostać wyświetlony podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cef81-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="cef81-138">Przy użyciu usługi tabel hello w aplikacji node</span><span class="sxs-lookup"><span data-stu-id="cef81-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="cef81-139">W tej sekcji rozszerzy aplikacji w warstwie podstawowa hello utworzone przez hello **express** polecenie, dodając **task.js** pliku, który zawiera hello model dla zadań.</span><span class="sxs-lookup"><span data-stu-id="cef81-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="cef81-140">Należy również zmodyfikować istniejące hello **app.js** i utworzyć nową **tasklist.js** pliku, który używa hello modelu.</span><span class="sxs-lookup"><span data-stu-id="cef81-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="cef81-141">Tworzenie modelu hello</span><span class="sxs-lookup"><span data-stu-id="cef81-141">Create hello model</span></span>
1. <span data-ttu-id="cef81-142">W hello **WebRole1** katalogu, Utwórz nowy katalog o nazwie **modele**.</span><span class="sxs-lookup"><span data-stu-id="cef81-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="cef81-143">W hello **modele** katalogu, Utwórz nowy plik o nazwie **task.js**.</span><span class="sxs-lookup"><span data-stu-id="cef81-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="cef81-144">Ten plik będzie zawierać hello model dla zadań hello utworzonych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="cef81-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="cef81-145">Na początku hello hello **task.js** plików, dodawanie hello następującego kodu tooreference wymagane biblioteki:</span><span class="sxs-lookup"><span data-stu-id="cef81-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="cef81-146">Następnie zostanie Dodaj kod toodefine i wyeksportować hello obiektu zadania.</span><span class="sxs-lookup"><span data-stu-id="cef81-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="cef81-147">Ten obiekt jest odpowiedzialny za łączenie toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="cef81-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="cef81-148">Następnie dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danymi przechowywanymi w tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="cef81-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="cef81-149">Zapisz i zamknij hello **task.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="cef81-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="cef81-150">Tworzenie kontrolera hello</span><span class="sxs-lookup"><span data-stu-id="cef81-150">Create hello controller</span></span>
1. <span data-ttu-id="cef81-151">W hello **WebRole1/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="cef81-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="cef81-152">Dodaj hello zbyt następującego kodu**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="cef81-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="cef81-153">Spowoduje to załadowanie modułów hello azure i async, które są używane przez **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="cef81-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="cef81-154">Definiuje również hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="cef81-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="cef81-155">Kontynuować dodawanie toohello **tasklist.js** przez dodanie metody hello używane zbyt**showTasks**, **addTask**, i **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="cef81-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="cef81-156">Zapisz hello **tasklist.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="cef81-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="cef81-157">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="cef81-157">Modify app.js</span></span>
1. <span data-ttu-id="cef81-158">W hello **WebRole1** hello katalogu, otwórz **app.js** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="cef81-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="cef81-159">Na początku hello pliku hello, Dodaj powitania po tooload hello azure modułu i ustaw klucz nazwy i partycji tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="cef81-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="cef81-160">W pliku app.js hello, przewiń w dół toowhere widzisz hello następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="cef81-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="cef81-161">Zastąp hello powyżej wierszy kodu hello pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cef81-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="cef81-162">Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z kontem magazynu tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="cef81-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="cef81-163">To jest przekazywany toohello <strong>TaskList</strong>, którego użyje on toocommunicate z hello usługa tabel:</span><span class="sxs-lookup"><span data-stu-id="cef81-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="cef81-164">Zapisz hello **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="cef81-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="cef81-165">Zmodyfikuj widok indeksu hello</span><span class="sxs-lookup"><span data-stu-id="cef81-165">Modify hello index view</span></span>
1. <span data-ttu-id="cef81-166">Zmień katalogi toohello **widoków** hello katalogu i Otwórz **index.jade** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="cef81-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="cef81-167">Zamień zawartość hello hello **index.jade** pliku z kodem hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="cef81-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="cef81-168">Definiuje hello widok, aby wyświetlić istniejące zadania, a także formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="cef81-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="cef81-169">Zapisz i Zamknij **index.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="cef81-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="cef81-170">Modyfikuj hello układ globalne</span><span class="sxs-lookup"><span data-stu-id="cef81-170">Modify hello global layout</span></span>
<span data-ttu-id="cef81-171">Witaj **layout.jade** pliku w hello **widoków** katalog jest używany jako szablon globalny dla innych **jade** plików.</span><span class="sxs-lookup"><span data-stu-id="cef81-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="cef81-172">W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cef81-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="cef81-173">Pobierać i wyodrębniać pliki hello [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="cef81-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="cef81-174">Hello kopiowania **bootstrap.min.css** pliku z hello **bootstrap\\dist\\css** toohello folderu **publicznego\\arkusze stylów** Katalog aplikacji tasklist.</span><span class="sxs-lookup"><span data-stu-id="cef81-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="cef81-175">Z hello **widoków** folder, otwórz hello **layout.jade** w Twojej edytora i Zamień hello zawartość tekstową hello następujący:</span><span class="sxs-lookup"><span data-stu-id="cef81-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="cef81-176">Tytuł head doctype html html = łącze do tytułu (rel = "stylesheet', href='/stylesheets/bootstrap.min.css) łącza (rel ="stylesheet', href='/stylesheets/style.css) body.app nav.navbar.navbar domyślną nagłówka div.navbar a.navbar-brand(href='/') zawartości bloku Moje zadania</span><span class="sxs-lookup"><span data-stu-id="cef81-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="cef81-177">Zapisz hello **layout.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="cef81-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="cef81-178">Uruchamianie aplikacji hello w hello emulatora</span><span class="sxs-lookup"><span data-stu-id="cef81-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="cef81-179">Użyj następującego polecenia toostart hello aplikacji w emulatorze hello hello.</span><span class="sxs-lookup"><span data-stu-id="cef81-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="cef81-180">Przeglądarka Hello zostanie otwarty i wyświetla hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="cef81-180">hello browser will open and displays hello following page:</span></span>

![Sieć web stronicowanej zatytułowany Moje listy zadań z tabeli zawierającej tooadd zadania i pola nowe zadanie.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="cef81-182">Użyj pozycji tooadd formularza hello, lub usuń istniejące elementy oznaczając je jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="cef81-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="cef81-183">Publikowanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="cef81-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="cef81-184">W oknie programu Windows PowerShell hello wywołać hello następującego polecenia cmdlet tooredeploy tooAzure Twojego usługi hostowanej.</span><span class="sxs-lookup"><span data-stu-id="cef81-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="cef81-185">Zastąp **myuniquename** z unikatową nazwę dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cef81-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="cef81-186">Zastąp **datacentername** o nazwie hello centrum danych Azure, takich jak **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="cef81-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="cef81-187">Po zakończeniu wdrażania hello powinny być widoczne następujące toohello podobne odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="cef81-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="cef81-188">Jak wcześniej ponieważ określona hello **— uruchamianie** opcji otwiera hello przeglądarki i wyświetla aplikacji działających na platformie Azure po zakończeniu publikowania.</span><span class="sxs-lookup"><span data-stu-id="cef81-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Strona Moje listy zadań hello okna przeglądarki.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="cef81-191">Zatrzymywanie i usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cef81-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="cef81-192">Po wdrożeniu aplikacji, może być toodisable, można uniknąć kosztów lub tworzenia i wdrażania innych aplikacji w obrębie hello wolne okresu próbnego.</span><span class="sxs-lookup"><span data-stu-id="cef81-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="cef81-193">Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera.</span><span class="sxs-lookup"><span data-stu-id="cef81-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="cef81-194">Czas serwera jest używany, gdy aplikacja jest wdrażana, nawet jeśli wystąpienia nie zostały uruchomione i są w stanie hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="cef81-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="cef81-195">Witaj poniższej procedurze pokazano, jak toostop i usuwania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cef81-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="cef81-196">W oknie programu PowerShell Windows hello Zatrzymaj wdrożenie usługi hello utworzony w poprzedniej sekcji hello z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cef81-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="cef81-197">Zatrzymywanie usługi hello może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cef81-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="cef81-198">Witaj, usługa zostanie zatrzymana, pojawi się komunikat wskazujący, że usługa została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="cef81-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="cef81-199">Usługa hello toodelete, wywołanie hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cef81-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="cef81-200">Po wyświetleniu monitu wprowadź **Y** toodelete hello usługi.</span><span class="sxs-lookup"><span data-stu-id="cef81-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="cef81-201">Usuwanie hello usługi może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cef81-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="cef81-202">Po usunięciu hello usługi pojawi się komunikat wskazujący, że usługa hello została usunięta.</span><span class="sxs-lookup"><span data-stu-id="cef81-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[aplikacji sieci Web Node.js za pomocą ekspresowego]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[przechowywanie i uzyskiwanie dostępu do danych na platformie Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplikacji sieci Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


