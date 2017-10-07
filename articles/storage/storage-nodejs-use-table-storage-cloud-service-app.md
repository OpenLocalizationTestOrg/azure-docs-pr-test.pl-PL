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
# <a name="nodejs-web-application-using-storage"></a>Aplikacja sieci Web node.js za pomocą magazynu
## <a name="overview"></a>Omówienie
W tym samouczku rozszerzy utworzony w aplikacji hello [aplikacji sieci Web Node.js za pomocą ekspresowego] samouczka za pomocą biblioteki klienta usługi Azure Microsoft hello toowork Node.js z usługami zarządzania danych. Toocreate Twojej aplikacji może trwać do aplikacji opartych na sieci web listy zadań wdrożenie tooAzure. Lista zadań Hello pozwala użytkownikowi na pobieranie zadań, Dodaj nowe zadania i oznaczanie zadań jako ukończone.

elementy zadań Hello są przechowywane w usłudze Azure Storage. Usługa Azure Storage udostępnia magazyn danych bez struktury, która jest odporna na uszkodzenia i wysokiej dostępności. Magazyn Azure obejmuje kilka struktury danych, gdzie można przechowywać i uzyskiwanie dostępu do danych, a mogą korzystać z usług magazynu hello z hello interfejsów API objęte hello Azure SDK dla środowiska Node.js lub za pośrednictwem interfejsów API REST. Aby uzyskać więcej informacji, zobacz [przechowywanie i uzyskiwanie dostępu do danych na platformie Azure].

Ten samouczek zakłada, że zostały wykonane hello [aplikacji sieci Web Node.js] i [Node.js z Express][aplikacji sieci Web Node.js za pomocą ekspresowego] samouczki.

Dowiesz się:

* Jak toowork z hello aparatu Jade szablonu
* Jak toowork z usługami Azure zarządzanie danymi

Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Witaj ukończone strony sieci web w programie internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Ustawianie poświadczeń magazynu w pliku Web.Config
tooaccess usługi Azure Storage, należy toopass poświadczenia magazynu. toodo, korzystanie z ustawienia pliku web.config aplikacji.
Te ustawienia zostaną przekazane jako tooNode zmienne środowiskowe, które następnie są odczytywane przez hello Azure SDK.

> [!NOTE]
> Poświadczenia magazynu są używane tylko w przypadku, gdy aplikacja hello jest tooAzure wdrożone. Podczas uruchamiania w emulatorze hello, aplikacja hello użyje hello emulatora magazynu.
>
>

Wykonaj hello następujące poświadczenia konta magazynu hello tooretrieve czynności i dodaj je toohello ustawienia pliku web.config:

1. Jeśli go nie jest jeszcze otwarty, należy uruchomić hello Azure PowerShell z hello **Start** menu rozwijając **wszystkie programy, Azure**, kliknij prawym przyciskiem myszy **programu Azure PowerShell**, a następnie wybierz  **Uruchom jako Administrator**.
2. Zmień katalogi toohello folderu zawierającego aplikację. Na przykład C:\\węzła\\tasklist\\WebRole1.
3. Z okna programu Azure Powershell hello wprowadź hello następujących informacji o koncie magazynu hello tooretrieve polecenia cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Pobiera to hello listę kont magazynu i konto klucze skojarzone z usługi hostowanej.

   > [!NOTE]
   > Witaj zestawu Azure SDK tworzy konto magazynu, podczas wdrażania usługi, konto magazynu powinna już istnieć z wdrożenia aplikacji w poprzednim przewodnikach hello.
   >
   >
4. Otwórz hello **ServiceDefinition.csdef** pliku zawierającego ustawienia środowiska hello, które są używane, kiedy aplikacja hello jest wdrożony tooAzure:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Wstaw hello poniższego bloku w obszarze **środowiska** elementu, zastępując {konta MAGAZYNU} i {klucz dostępu do MAGAZYNU} z nazwą konta hello i hello klucz podstawowy dla konta magazynu hello ma toouse wdrożenia:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![zawartość pliku web.cloud.config Hello](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. Zapisz plik hello i zamknij Notatnik.

### <a name="install-additional-modules"></a>Instalowanie dodatkowych modułów
1. Hello Użyj następującego polecenia tooinstall hello [azure], [uuid węzła], [nconf] i [async] moduły lokalnie, jak również toosave wpis dla nich toohello **package.json** pliku:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  Witaj dane wyjściowe tego polecenia powinien zostać wyświetlony podobne toohello następujące czynności:

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

## <a name="using-hello-table-service-in-a-node-application"></a>Przy użyciu usługi tabel hello w aplikacji node
W tej sekcji rozszerzy aplikacji w warstwie podstawowa hello utworzone przez hello **express** polecenie, dodając **task.js** pliku, który zawiera hello model dla zadań. Należy również zmodyfikować istniejące hello **app.js** i utworzyć nową **tasklist.js** pliku, który używa hello modelu.

### <a name="create-hello-model"></a>Tworzenie modelu hello
1. W hello **WebRole1** katalogu, Utwórz nowy katalog o nazwie **modele**.
2. W hello **modele** katalogu, Utwórz nowy plik o nazwie **task.js**. Ten plik będzie zawierać hello model dla zadań hello utworzonych przez aplikację.
3. Na początku hello hello **task.js** plików, dodawanie hello następującego kodu tooreference wymagane biblioteki:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Następnie zostanie Dodaj kod toodefine i wyeksportować hello obiektu zadania. Ten obiekt jest odpowiedzialny za łączenie toohello tabeli.

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

5. Następnie dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danymi przechowywanymi w tabeli hello:

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

6. Zapisz i zamknij hello **task.js** pliku.

### <a name="create-hello-controller"></a>Tworzenie kontrolera hello
1. W hello **WebRole1/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.
2. Dodaj hello zbyt następującego kodu**tasklist.js**. Spowoduje to załadowanie modułów hello azure i async, które są używane przez **tasklist.js**. Definiuje również hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Kontynuować dodawanie toohello **tasklist.js** przez dodanie metody hello używane zbyt**showTasks**, **addTask**, i **completeTasks**:

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

4. Zapisz hello **tasklist.js** pliku.

### <a name="modify-appjs"></a>Modyfikowanie pliku app.js
1. W hello **WebRole1** hello katalogu, otwórz **app.js** plik w edytorze tekstów.
2. Na początku hello pliku hello, Dodaj powitania po tooload hello azure modułu i ustaw klucz nazwy i partycji tabeli hello:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. W pliku app.js hello, przewiń w dół toowhere widzisz hello następujący wiersz:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Zastąp hello powyżej wierszy kodu hello pokazano poniżej. Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z kontem magazynu tooyour połączenia. To jest przekazywany toohello <strong>TaskList</strong>, którego użyje on toocommunicate z hello usługa tabel:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Zapisz hello **app.js** pliku.

### <a name="modify-hello-index-view"></a>Zmodyfikuj widok indeksu hello
1. Zmień katalogi toohello **widoków** hello katalogu i Otwórz **index.jade** plik w edytorze tekstów.
2. Zamień zawartość hello hello **index.jade** pliku z kodem hello poniżej. Definiuje hello widok, aby wyświetlić istniejące zadania, a także formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.

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

3. Zapisz i Zamknij **index.jade** pliku.

### <a name="modify-hello-global-layout"></a>Modyfikuj hello układ globalne
Witaj **layout.jade** pliku w hello **widoków** katalog jest używany jako szablon globalny dla innych **jade** plików. W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej witryny sieci Web.

1. Pobierać i wyodrębniać pliki hello [Twitter Bootstrap](http://getbootstrap.com/). Hello kopiowania **bootstrap.min.css** pliku z hello **bootstrap\\dist\\css** toohello folderu **publicznego\\arkusze stylów** Katalog aplikacji tasklist.
2. Z hello **widoków** folder, otwórz hello **layout.jade** w Twojej edytora i Zamień hello zawartość tekstową hello następujący:

    Tytuł head doctype html html = łącze do tytułu (rel = "stylesheet', href='/stylesheets/bootstrap.min.css) łącza (rel ="stylesheet', href='/stylesheets/style.css) body.app nav.navbar.navbar domyślną nagłówka div.navbar a.navbar-brand(href='/') zawartości bloku Moje zadania

3. Zapisz hello **layout.jade** pliku.

### <a name="running-hello-application-in-hello-emulator"></a>Uruchamianie aplikacji hello w hello emulatora
Użyj następującego polecenia toostart hello aplikacji w emulatorze hello hello.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

Przeglądarka Hello zostanie otwarty i wyświetla hello następujące strony:

![Sieć web stronicowanej zatytułowany Moje listy zadań z tabeli zawierającej tooadd zadania i pola nowe zadanie.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

Użyj pozycji tooadd formularza hello, lub usuń istniejące elementy oznaczając je jako ukończone.

## <a name="publishing-hello-application-tooazure"></a>Publikowanie tooAzure aplikacji hello
W oknie programu Windows PowerShell hello wywołać hello następującego polecenia cmdlet tooredeploy tooAzure Twojego usługi hostowanej.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Zastąp **myuniquename** z unikatową nazwę dla tej aplikacji. Zastąp **datacentername** o nazwie hello centrum danych Azure, takich jak **zachodnie stany USA**.

Po zakończeniu wdrażania hello powinny być widoczne następujące toohello podobne odpowiedzi:

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

Jak wcześniej ponieważ określona hello **— uruchamianie** opcji otwiera hello przeglądarki i wyświetla aplikacji działających na platformie Azure po zakończeniu publikowania.

![Strona Moje listy zadań hello okna przeglądarki. adres URL Hello wskazuje, że strona hello jest teraz obsługiwana na platformie Azure.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Zatrzymywanie i usuwanie aplikacji
Po wdrożeniu aplikacji, może być toodisable, można uniknąć kosztów lub tworzenia i wdrażania innych aplikacji w obrębie hello wolne okresu próbnego.

Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera.
Czas serwera jest używany, gdy aplikacja jest wdrażana, nawet jeśli wystąpienia nie zostały uruchomione i są w stanie hello zatrzymana.

Witaj poniższej procedurze pokazano, jak toostop i usuwania aplikacji.

1. W oknie programu PowerShell Windows hello Zatrzymaj wdrożenie usługi hello utworzony w poprzedniej sekcji hello z hello następującego polecenia cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Zatrzymywanie usługi hello może potrwać kilka minut. Witaj, usługa zostanie zatrzymana, pojawi się komunikat wskazujący, że usługa została zatrzymana.

2. Usługa hello toodelete, wywołanie hello następującego polecenia cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Po wyświetleniu monitu wprowadź **Y** toodelete hello usługi.

   Usuwanie hello usługi może potrwać kilka minut. Po usunięciu hello usługi pojawi się komunikat wskazujący, że usługa hello została usunięta.

[aplikacji sieci Web Node.js za pomocą ekspresowego]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[przechowywanie i uzyskiwanie dostępu do danych na platformie Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplikacji sieci Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


