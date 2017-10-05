---
title: "Aplikacja sieci Web w technologii Node.js wykorzystująca usługę Azure Table Service"
description: "W tym samouczku jest przedstawienie sposobu korzystania z usługi tabel Azure do przechowywania danych z aplikacji Node.js, która jest hostowana w aplikacji sieci Web usługi aplikacji Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a>Aplikacja sieci Web w technologii Node.js wykorzystująca usługę Azure Table Service
## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak korzystać z usługi tabeli przez zarządzanie danymi Azure do przechowywania i uzyskać dostęp do danych z [węzła] aplikacji hostowanej w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web. W tym samouczku założono, że pewne doświadczenie w korzystaniu z węzła i [Git].

Dowiesz się:

* Jak używać programu npm (węzeł Menedżera pakietów) Aby zainstalować moduły węzła
* Jak pracować z usługą Azure tabeli
* Jak utworzyć aplikację sieci web za pomocą wiersza polecenia platformy Azure.

W ramach tego samouczka, utworzysz prostą opartych na sieci web aplikacji "Lista zadań do wykonania", która umożliwia tworzenie, pobieranie i kończenie zadań. Zadania są przechowywane w usłudze tabel.

W tym miejscu jest ukończona aplikacja:

![Strona sieci web tasklist pusty][node-table-finished]

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed wykonaniem instrukcji zawartych w tym artykule, upewnij się, że masz następujące elementy:

* [węzła] wersji 0.10.24 lub nowszej
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
Utworzenie konta magazynu platformy Azure. Aplikacja będzie używać tego konta do przechowywania elementów do wykonania.

1. Zaloguj się do [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowy** pozostałych ikony w dolnej części portalu, kliknij przycisk **dane i magazyn** > **magazynu**. Nadaj unikatową nazwę konta magazynu i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.
   
      ![Przycisk Nowy](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Po utworzeniu konta magazynu, **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu jest otwarty, aby pokazać, że należy on do tworzenia nowej grupy zasobów.
3. W bloku konto magazynu, kliknij **ustawienia** > **klucze**. Skopiuj podstawowy klucz dostępu do Schowka.
   
    ![Klucz dostępu][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Zainstaluj moduły i Generowanie szkieletów
W tej sekcji utworzysz nową aplikację węzła i umożliwia dodawanie pakietów moduł npm. Ta aplikacja będzie używać [Express] i [Azure] modułów. Modułu Express zapewnia platformę kontrolera widoku modelu dla węzła, gdy moduł Azure zapewnia łączność z usługą tabeli.

### <a name="install-express-and-generate-scaffolding"></a>Zainstaluj express i Generowanie szkieletów
1. W wierszu polecenia Utwórz nowy katalog o nazwie **tasklist** i przełączać się do tego katalogu.  
2. Wprowadź następujące polecenie, aby zainstalować moduł Express.
   
        npm install express-generator@4.2.0 -g
   
    W zależności od systemu operacyjnego może być konieczne umieszczanie 'sudo' przed wykonaniem polecenia:
   
        sudo npm install express-generator@4.2.0 -g
   
    Dane wyjściowe wygląda podobnie do poniższego przykładu:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > "-G" parametr instaluje moduł globalnie. W ten sposób możemy użyć **express** do generowania szkieletu aplikacji sieci web bez konieczności wpisz dodatkowe informacje o ścieżce.
   > 
   > 
3. Aby utworzyć szkielet aplikacji, wprowadź **express** polecenia:
   
        express
   
    Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    Masz teraz kilka nowych katalogów i plików w **tasklist** katalogu.

### <a name="install-additional-modules"></a>Instalowanie dodatkowych modułów
Jeden z plików który **express** tworzy jest **package.json**. Ten plik zawiera listę zależności modułu. Później podczas wdrażania aplikacji do aplikacji usługi sieci Web aplikacji, ten plik Określa, które moduły muszą być zainstalowane na platformie Azure.

W wierszu polecenia wprowadź następujące polecenie, aby zainstalować moduły opisanego w **package.json** pliku. Może być konieczne użycie "sudo".

    npm install

Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Następnie wprowadź następujące polecenie, aby zainstalować [azure], [uuid węzła], [nconf] i [async] modułów:

    npm install azure-storage node-uuid async nconf --save

**— Zapisywanie** Flaga Dodaje wpisy dla tych modułów, aby **package.json** pliku.

Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a>Tworzenie aplikacji
Teraz już wszystko gotowe do tworzenia aplikacji.

### <a name="create-a-model"></a>Tworzenie modelu
A *modelu* jest obiekt, który reprezentuje dane w aplikacji. Dla aplikacji tylko model jest obiekt zadania, który reprezentuje element na liście zadań do wykonania. Zadania będzie zawierać następujące pola:

* PartitionKey
* RowKey
* Nazwa (ciąg)
* Kategoria (ciąg)
* Ukończono (wartość logiczna)

**PartitionKey** i **RowKey** są używane przez usługę tabeli jako klucze tabeli. Aby uzyskać więcej informacji, zobacz [opis modelu danych usługi tabel](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. W **tasklist** katalogu, Utwórz nowy katalog o nazwie **modele**.
2. W **modele** katalogu, Utwórz nowy plik o nazwie **task.js**. Ten plik zawiera model dla zadań tworzonych przez aplikację.
3. Na początku **task.js** pliku, Dodaj następujący kod, aby odwołać wymagane biblioteki:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Dodaj następujący kod w celu zdefiniowania i wyeksportowania obiektu Task. Ten obiekt jest odpowiedzialny za nawiązywania połączenia z tabeli.
   
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
5. Dodaj następujący kod, aby zdefiniować dodatkowe metody dla obiektu Task umożliwiające interakcje z danymi przechowywanymi w tabeli:
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
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
6. Zapisz i Zamknij **task.js** pliku.

### <a name="create-a-controller"></a>Tworzenie kontrolera
A *kontrolera* obsługi żądań HTTP i renderuje odpowiedzi HTML.

1. W **tasklist/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.
2. Dodaj następujący kod do pliku **tasklist.js**. Spowoduje to załadowanie modułów azure i async, które są używane przez **tasklist.js**. Definiuje również **TaskList** funkcji, która została przekazana wystąpienia **zadań** zdefiniowanego wcześniej:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Zdefiniuj **TaskList** obiektu.
   
        function TaskList(task) {
          this.task = task;
        }
4. Dodaj następujące metody umożliwiające **TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
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

### <a name="modify-appjs"></a>Modyfikowanie pliku app.js
1. Z **tasklist** katalogu, otwórz **app.js** pliku. Ten plik został utworzony wcześniej przez uruchomienie **express** polecenia.
2. Na początku pliku Dodaj następujące polecenie, aby załadować moduł azure, ustaw nazwę tabeli klucza partycji i Ustaw poświadczenia magazynu użyte w tym przykładzie:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf załaduje wartości konfiguracji z obu zmiennych środowiskowych lub **config.json** pliku, który zostanie utworzony później.
   > 
   > 
3. W pliku app.js przewiń w dół, do której występuje następujący wiersz:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Zamień wiersze powyżej kodu pokazano poniżej. Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z połączeniem z konta magazynu. To jest przekazywana do <strong>TaskList</strong>, który zostanie użyty do komunikowania się z usługą tabeli:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Zapisz **app.js** pliku.

### <a name="modify-the-index-view"></a>Zmodyfikuj widok indeksu
1. Otwórz **tasklist/views/index.jade** plik w edytorze tekstów.
2. Zastąp całą zawartość pliku następującym kodem. Określa widok, w którym wyświetlane istniejące zadania oraz formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.
   
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
              if (typeof tasks === "undefined")
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
3. Zapisz i Zamknij **index.jade** pliku.

### <a name="modify-the-global-layout"></a>Modyfikowanie globalnych układu
**Layout.jade** w pliku **widoków** katalog jest szablon globalny dla innych **jade** plików. W tym kroku zmodyfikujesz go do korzystania ze [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi ułatwiającym projektowanie nieuprzywilejowany wyglądającej aplikacji sieci web.

Pobierz i Wyodrębnij pliki do [Twitter Bootstrap](http://getbootstrap.com/). Kopiuj **bootstrap.min.css** pliku z ładowania początkowego programu **css** do folderu **publiczne/arkusze stylów** katalogu aplikacji.

Z **widoków** folder, otwórz **layout.jade** i Zastąp całą zawartość następującym kodem:

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Utwórz plik konfiguracji
Aby uruchomić aplikację lokalnie, będzie testujemy poświadczeń usługi Azure Storage w pliku konfiguracji. Utwórz plik o nazwie **config.json* * z następujących JSON:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Zastąp **nazwy konta magazynu** o nazwie magazynu konta utworzonego wcześniej i Zastąp **klucz dostępu do magazynu** z podstawowy klucz dostępu dla konta magazynu. Na przykład:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Zapisz ten plik *poziomu katalogów wyższych* niż **tasklist** katalogu w następujący sposób:

    parent/
      |-- config.json
      |-- tasklist/

Przyczyna w ten sposób jest uniknięcie sprawdzania pliku konfiguracji do kontroli źródła, gdzie mogą być publiczny. Firma Microsoft wdrażania aplikacji na platformie Azure, użyjemy zmienne środowiskowe zamiast pliku konfiguracji.

## <a name="run-the-application-locally"></a>Uruchamianie aplikacji lokalnie
Aby przetestować aplikację na komputerze lokalnym, wykonaj następujące czynności:

1. W wierszu polecenia Zmień katalog na **tasklist** katalogu.
2. Aby uruchomić aplikację lokalnie, użyj następującego polecenia:
   
        npm start
3. Otwórz przeglądarkę sieci web i przejdź do http://127.0.0.1:3000.
   
    Zostanie wyświetlona strona sieci web podobny do poniższego przykładu.
   
    ![Wyświetlanie tasklist puste strony sieci Web][node-table-finished]
4. Aby utworzyć nowe zadanie do wykonania, wprowadź nazwę i kategorii, a następnie kliknij przycisk **Dodaj element**. 
5. Aby oznaczyć zadanie jako zakończone, sprawdź **Complete** i kliknij przycisk **zadania aktualizacji**.
   
    ![Obraz nowego elementu na liście zadań][node-table-list-items]

Mimo że aplikacja działa lokalnie, danych jest przechowywana w usłudze tabel Azure.

## <a name="deploy-your-application-to-azure"></a>Wdrażanie aplikacji na platformie Azure
Kroki opisane w tej sekcji umożliwiają tworzenie nowej aplikacji sieci web w usłudze App Service narzędzia wiersza polecenia platformy Azure, a następnie użyj Git do wdrożenia aplikacji. Aby wykonać te czynności musi mieć subskrypcję platformy Azure.

> [!NOTE]
> Można także wykonać te czynności przy użyciu [Azure Portal](https://portal.azure.com/). Zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].
> 
> Jeśli jest to pierwszej aplikacji sieci web, które zostały utworzone, należy wdrożyć tę aplikację za pomocą portalu Azure.
> 
> 

Aby rozpocząć pracę, należy zainstalować [interfejsu wiersza polecenia Azure] , wprowadzając następujące polecenie w wierszu polecenia:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importowanie ustawień publikowania
W tym kroku pobierze plik zawierający informacje o Twojej subskrypcji.

1. Wprowadź następujące polecenie:
   
        azure login
   
    To polecenie spowoduje uruchomienie przeglądarki i przechodzi do strony pobierania. W przypadku wyświetlenia monitu zaloguj się przy użyciu konta skojarzonego z subskrypcją platformy Azure.
   
    <!-- ![The download page][download-publishing-settings] -->
   
    Pobieranie pliku rozpoczyna się automatycznie. Jeśli nie, kliknięcie łącza na początku strony, aby ręcznie pobrać plik. Zapisz plik i Zanotuj ścieżkę pliku.
2. Wprowadź następujące polecenie, aby zaimportować ustawienia:
   
        azure account import <path-to-file>
   
    Określ ścieżkę i nazwę pliku ustawień publikowania, który został pobrany w poprzednim kroku.
3. Zaimportowane ustawienia, należy usunąć plik ustawień publikowania. Nie jest już potrzebne i zawiera poufne informacje dotyczące subskrypcji platformy Azure.

### <a name="create-an-app-service-web-app"></a>Tworzenie aplikacji sieci web usługi aplikacji
1. W wierszu polecenia Zmień katalog na **tasklist** katalogu.
2. Użyj następującego polecenia, aby utworzyć nową aplikację sieci web.
   
        azure site create --git
   
    Pojawi się monit dla nazwy aplikacji sieci web i lokalizacji. Podaj unikatową nazwę i wybierz tej samej lokalizacji geograficznej co konto magazynu Azure.
   
    `--git` Parametr tworzy repozytorium Git na platformie Azure dla tej aplikacji sieci web. Inicjuje również repozytorium Git w bieżącym katalogu, jeśli nie istnieje i dodaje [zdalnego Git] o nazwie "azure", która jest używana do publikowania aplikacji na platformie Azure. Na koniec tworzy **web.config** pliku, który zawiera ustawienia używane przez usługę Azure umożliwia obsługę aplikacji węzła. W przypadku pominięcia `--git` parametr, ale katalog zawiera repozytorium Git, polecenie nadal utworzy azure zdalnego.
   
    Po ukończeniu tego polecenia, zostanie wyświetlone dane wyjściowe podobne do następującego. Należy pamiętać, że wiersz, począwszy od **witryny sieci Web utworzonego w dniu** zawiera adres URL aplikacji sieci web.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > Jeśli jest to pierwszej aplikacji sieci web usługi aplikacji — dla Twojej subskrypcji, pojawi się instrukcja za pomocą portalu Azure do utworzenia aplikacji sieci web. Aby uzyskać więcej informacji, zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>Ustaw zmienne środowiskowe
W tym kroku zmiennych środowiskowych zostaną dodane do konfiguracji aplikacji sieci web na platformie Azure.
W wierszu polecenia wprowadź następujące informacje:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Zastąp  **<storage account name>**  o nazwie magazynu konta utworzonego wcześniej i Zastąp  **<storage access key>**  z podstawowy klucz dostępu dla konta magazynu. (Użyj tej samej wartości jako plik config.json, który został utworzony wcześniej).

Alternatywnie można ustawić zmienne środowiskowe [Azure Portal](https://portal.azure.com/):

1. Otwarcie bloku aplikacji sieci web, klikając **Przeglądaj** > **aplikacje sieci Web** > Nazwa aplikacji sieci web.
2. W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Przewiń w dół do **ustawień aplikacji** i Dodaj pary klucz wartość.
   
     ![Ustawienia aplikacji](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Kliknij przycisk **SAVE** (Zapisz).

### <a name="publish-the-application"></a>Publikowanie aplikacji
Aby opublikować aplikację, Przekaż plików kodu do Git, a następnie Wypchnij azure/wzorzec.

1. Ustaw poświadczenia wdrażania.
   
        azure site deployment user set <name> <password>
2. Dodaj i zatwierdź plików aplikacji.
   
        git add .
        git commit -m "adding files"
3. Wypchnij zatwierdzenia do aplikacji sieci web usługi aplikacji:
   
        git push azure master
   
    Użyj **wzorca** jako gałęzi docelowej. Po zakończeniu wdrażania zobacz temat instrukcję podobny do poniższego przykładu:
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Po ukończeniu operacji wypychania, przejdź do adresu URL aplikacji sieci web, które zostały wcześniej zwrócony przez `azure create site` polecenie, aby wyświetlić aplikację.

## <a name="next-steps"></a>Następne kroki
Podczas czynności opisane w tym artykule opisano przy użyciu usługi tabel do przechowywania informacji, można również użyć [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Dodatkowe zasoby
[interfejsu wiersza polecenia Azure]

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

<!-- URLs -->

[tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[węzła]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[zdalnego Git]: http://git-scm.com/docs/git-remote

[interfejsu wiersza polecenia Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid węzła]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
