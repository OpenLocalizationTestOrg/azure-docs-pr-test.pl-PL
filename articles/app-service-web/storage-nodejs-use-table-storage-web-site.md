---
title: "aaaNode.js aplikacji sieci web przy użyciu hello Azure usługa tabel"
description: "Ten samouczek zawiera wskazówki dotyczące sposobu hello toouse tabel Azure usługi toostore danych z aplikacji Node.js, który jest obsługiwany w aplikacji sieci Web usługi aplikacji Azure."
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Aplikacja sieci web node.js za pomocą hello Azure usługa tabel
## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak usługa tabel toouse udostępniane przez zarządzanie danymi Azure toostore i dostępu do danych z [węzła] aplikacji hostowanej w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web. W tym samouczku założono, że pewne doświadczenie w korzystaniu z węzła i [Git].

Dowiesz się:

* Jak tooinstall npm (węzeł Menedżera pakietów) toouse hello modułów węzła
* Jak toowork z hello usługi tabeli platformy Azure
* Jak toouse hello toocreate wiersza polecenia platformy Azure, aplikacji sieci web.

W ramach tego samouczka, utworzysz prostą opartych na sieci web aplikacji "Lista zadań do wykonania", która umożliwia tworzenie, pobieranie i kończenie zadań. Witaj zadania są przechowywane w hello usługi tabel.

Oto aplikacji hello zakończone:

![Strona sieci web tasklist pusty][node-table-finished]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem powitalne instrukcje w tym artykule, upewnij się, że mają zainstalowane następujące hello:

* [węzła] wersji 0.10.24 lub nowszej
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
Utworzenie konta magazynu platformy Azure. Aplikacja Hello będzie używać tego konta toostore hello zadaniach do wykonania.

1. Zaloguj się do hello [Azure Portal](https://portal.azure.com/).
2. Kliknij przycisk hello **nowy** ikony na dole hello pozostałych hello portalu, kliknij przycisk **dane i magazyn** > **magazynu**. Nadaj unikatową nazwę konta magazynu hello i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.
   
      ![Przycisk Nowy](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Po utworzeniu konta magazynu hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu hello jest otwarty tooshow należy toohello nowy zasób grupy utworzony.
3. W bloku konto magazynu powitania kliknij **ustawienia** > **klucze**. Kopiuj hello Schowka toohello klucza podstawowego dostępu.
   
    ![Klucz dostępu][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Zainstaluj moduły i Generowanie szkieletów
W tej sekcji utworzysz nową aplikację węzła i za pomocą programu npm tooadd modułu pakietów. Dla tej aplikacji będzie używać hello [Express] i [Azure] modułów. Hello modułu Express zapewnia platformę kontrolera widoku modelu dla węzła, podczas hello modułów Azure udostępnia usługi tabel toohello łączności.

### <a name="install-express-and-generate-scaffolding"></a>Zainstaluj express i Generowanie szkieletów
1. Z wiersza polecenia hello, Utwórz nowy katalog o nazwie **tasklist** i katalog toothat przełącznika.  
2. Wprowadź hello następujące polecenia tooinstall hello Express modułu.
   
        npm install express-generator@4.2.0 -g
   
    W zależności od systemu operacyjnego hello może być konieczne tooput 'sudo' przed wykonaniem polecenia hello:
   
        sudo npm install express-generator@4.2.0 -g
   
    dane wyjściowe Hello pojawia się toohello podobnie poniższy przykład:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Witaj "-g" parametr instaluje moduł hello globalnie. W ten sposób możemy użyć **express** toogenerate funkcja szkieletów aplikacji sieci web bez konieczności tootype w dodatkowe informacje o ścieżce.
   > 
   > 
3. toocreate hello szkieletów dla aplikacji hello wprowadź hello **express** polecenia:
   
        express
   
    Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Masz teraz kilka nowych katalogów i plików w hello **tasklist** katalogu.

### <a name="install-additional-modules"></a>Instalowanie dodatkowych modułów
Jeden z hello pliki **express** tworzy jest **package.json**. Ten plik zawiera listę zależności modułu. Później podczas wdrażania tooApp aplikacji hello usługi aplikacje sieci Web, ten plik Określa, które moduły muszą toobe zainstalowane na platformie Azure.

Z wiersza polecenia hello, wprowadź następujące moduły hello tooinstall polecenia opisanego w hello hello **package.json** pliku. Może być konieczne toouse "sudo".

    npm install

Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Następnie wprowadź następujące polecenie tooinstall hello hello [azure], [uuid węzła], [nconf] i [async] modułów:

    npm install azure-storage node-uuid async nconf --save

Witaj **— zapisywanie** Flaga Dodaje wpisy dla tych modułów toohello **package.json** pliku.

Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Tworzenie aplikacji hello
Jest teraz gotowy toobuild hello aplikacji.

### <a name="create-a-model"></a>Tworzenie modelu
A *modelu* jest obiekt, który reprezentuje dane hello w aplikacji. Dla aplikacji hello modelu tylko hello jest obiekt zadania, który reprezentuje element w hello listy zadań do wykonania. Zadania mają hello następujące pola:

* PartitionKey
* RowKey
* Nazwa (ciąg)
* Kategoria (ciąg)
* Ukończono (wartość logiczna)

**PartitionKey** i **RowKey** są używane przez usługi tabel hello jako klucze tabeli. Aby uzyskać więcej informacji, zobacz [modelu danych usługi tabel hello opis](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. W hello **tasklist** katalogu, Utwórz nowy katalog o nazwie **modele**.
2. W hello **modele** katalogu, Utwórz nowy plik o nazwie **task.js**. Ten plik będzie zawierać hello model dla zadań hello utworzonych przez aplikację.
3. Na początku hello hello **task.js** plików, dodawanie hello następującego kodu tooreference wymagane biblioteki:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Dodaj następujący hello code toodefine i wyeksportować hello obiektu zadania. Ten obiekt jest odpowiedzialny za łączenie toohello tabeli.
   
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
5. Dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danymi przechowywanymi w tabeli hello:
   
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
6. Zapisz i zamknij hello **task.js** pliku.

### <a name="create-a-controller"></a>Tworzenie kontrolera
A *kontrolera* obsługi żądań HTTP i renderuje odpowiedź hello HTML.

1. W hello **tasklist/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.
2. Dodaj hello zbyt następującego kodu**tasklist.js**. Spowoduje to załadowanie modułów hello azure i async, które są używane przez **tasklist.js**. Definiuje również hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Zdefiniuj **TaskList** obiektu.
   
        function TaskList(task) {
          this.task = task;
        }
4. Dodaj następujące metody zbyt hello**TaskList**:
   
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
1. Z hello **tasklist** hello katalogu, otwórz **app.js** pliku. Ten plik został utworzony wcześniej przez uruchomienie hello **express** polecenia.
2. Na początku hello pliku hello, Dodaj powitania po tooload hello azure modułu, nazwa tabeli hello zestawu klucz partycji i poświadczenia magazynu hello zestaw używany w tym przykładzie:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf załaduje hello konfiguracji wartości zmiennych środowiskowych lub hello **config.json** pliku, który zostanie utworzony później.
   > 
   > 
3. W pliku app.js hello, przewiń w dół toowhere widzisz hello następujący wiersz:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Zastąp hello powyżej wierszy kodu hello pokazano poniżej. Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z kontem magazynu tooyour połączenia. To jest przekazywany toohello <strong>TaskList</strong>, którego użyje on toocommunicate z hello usługa tabel:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Zapisz hello **app.js** pliku.

### <a name="modify-hello-index-view"></a>Zmodyfikuj widok indeksu hello
1. Otwórz hello **tasklist/views/index.jade** plik w edytorze tekstów.
2. Zastąp całą zawartość pliku hello hello hello następującego kodu. Określa widok, w którym wyświetlane istniejące zadania oraz formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.
   
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

### <a name="modify-hello-global-layout"></a>Modyfikuj hello układ globalne
Witaj **layout.jade** pliku w hello **widoków** katalog jest szablon globalny dla innych **jade** plików. W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej aplikacji sieci web.

Pobierać i wyodrębniać pliki hello [Twitter Bootstrap](http://getbootstrap.com/). Hello kopiowania **bootstrap.min.css** pliku z hello Bootstrap **css** folderu do hello **publiczne/arkusze stylów** katalogu aplikacji.

Z hello **widoków** folder, otwórz **layout.jade** i Zastąp całą zawartość hello hello następujące czynności:

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
toorun lokalnie aplikacji hello, będzie testujemy poświadczeń usługi Azure Storage w pliku konfiguracji. Utwórz plik o nazwie **config.json* * z powitania po JSON:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Zastąp **nazwy konta magazynu** o nazwie hello magazynu hello konta utworzonego wcześniej i Zastąp **klucz dostępu do magazynu** z hello podstawowy klucz dostępu dla konta magazynu. Na przykład:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Zapisz ten plik *poziomu katalogów wyższych* niż hello **tasklist** katalogu w następujący sposób:

    parent/
      |-- config.json
      |-- tasklist/

Przyczyna Hello w ten sposób jest tooavoid sprawdzanie hello pliku konfiguracji do kontroli źródła, gdzie mogą być publiczny. Firma Microsoft wdrażania tooAzure aplikacji hello, użyjemy zmienne środowiskowe zamiast pliku konfiguracji.

## <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie
Aplikacja hello tootest na komputerze lokalnym, wykonywać hello następujące kroki:

1. Z wiersza polecenia hello, zmień katalogi toohello **tasklist** katalogu.
2. Użyj hello następujące polecenie lokalnie aplikacji hello toolaunch:
   
        npm start
3. Otwórz przeglądarkę sieci web i przejdź toohttp://127.0.0.1:3000.
   
    Zostanie wyświetlona strona sieci web toohello podobne, poniższy przykład.
   
    ![Wyświetlanie tasklist puste strony sieci Web][node-table-finished]
4. toocreate nowe zadanie do wykonania, wprowadź nazwę i kategorii i kliknij przycisk **Dodaj element**. 
5. zadanie jako zakończone, sprawdź toomark **Complete** i kliknij przycisk **zadania aktualizacji**.
   
    ![Obraz powitania nowy element hello listy zadań][node-table-list-items]

Mimo że aplikacja hello działa lokalnie, hello danych jest przechowywana w hello usługi tabel Azure.

## <a name="deploy-your-application-tooazure"></a>Wdrażanie tooAzure Twojej aplikacji
kroki Hello w tej sekcji Użyj toocreate narzędzi wiersza polecenia platformy Azure hello nowej aplikacji sieci web w usłudze App Service, a następnie użyj Git toodeploy aplikacji. tooperform następujące kroki, musi mieć subskrypcję platformy Azure.

> [!NOTE]
> Można także wykonać te czynności przy użyciu hello [Azure Portal](https://portal.azure.com/). Zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].
> 
> Jeśli jest to hello pierwszej aplikacji sieci web utworzone, należy użyć hello toodeploy Azure Portal tej aplikacji.
> 
> 

tooget pracę, zainstaluj hello [interfejsu wiersza polecenia Azure] , wprowadzając następujące polecenie z wiersza polecenia hello hello:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importowanie ustawień publikowania
W tym kroku pobierze plik zawierający informacje o Twojej subskrypcji.

1. Wprowadź hello następujące polecenie:
   
        azure login
   
    To polecenie spowoduje uruchomienie przeglądarki i przechodzi do strony pobierania toohello. W przypadku wyświetlenia monitu zaloguj się przy użyciu konta hello skojarzonego z subskrypcją platformy Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    Pobieranie pliku Hello rozpoczyna się automatycznie. Jeśli nie, mogą kliknąć link hello na początku hello hello strony toomanually pobierania hello pliku. Zapisz hello plików i Uwaga hello ścieżkę pliku.
2. Wprowadź następujące ustawienia hello tooimport polecenia hello:
   
        azure account import <path-to-file>
   
    Podaj nazwę i ścieżka pliku hello hello publikowania w poprzednim kroku hello pobranego pliku ustawień.
3. Zaimportowane ustawienia hello usunąć hello pliku ustawień publikowania. Nie jest już potrzebne i zawiera poufne informacje dotyczące subskrypcji platformy Azure.

### <a name="create-an-app-service-web-app"></a>Tworzenie aplikacji sieci web usługi aplikacji
1. Z wiersza polecenia hello, zmień katalogi toohello **tasklist** katalogu.
2. Użyj hello następujące polecenia toocreate nowej aplikacji sieci web.
   
        azure site create --git
   
    Pojawi się monit dla nazwy aplikacji sieci web hello i lokalizacji. Podaj unikatową nazwę i wybierz hello tej samej lokalizacji geograficznej co konto magazynu Azure.
   
    Witaj `--git` parametru tworzy repozytorium Git na platformie Azure dla tej aplikacji sieci web. Inicjuje również repozytorium Git w bieżącym katalogu hello Jeśli brak istnieje i dodaje [zdalnego Git] o nazwie "azure", która jest tooAzure aplikacji hello toopublish używane. Na koniec tworzy **web.config** pliku, który zawiera ustawienia używane przez aplikacje węzła toohost platformy Azure. W przypadku pominięcia hello `--git` parametr, ale hello katalog zawiera repozytorium Git, polecenie hello nadal utworzy zdalnego hello "azure".
   
    Po ukończeniu tego polecenia, zostanie wyświetlone dane wyjściowe podobne toohello poniżej. Należy pamiętać, że powitania od wiersza z **witryny sieci Web utworzonego w dniu** zawiera adres URL hello hello aplikacji sieci web.
   
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
   > Jeśli jest to hello pierwszej aplikacji usługi aplikacji sieci web dla Twojej subskrypcji, będzie aplikacji sieci web hello toocreate instrukcją toouse hello portalu Azure. Aby uzyskać więcej informacji, zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>Ustaw zmienne środowiskowe
W tym kroku zostaną dodane konfiguracji aplikacji sieci web tooyour zmienne środowiskowe na platformie Azure.
Z wiersza polecenia hello wprowadź następujące hello:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Zastąp  **<storage account name>**  o nazwie hello magazynu hello konta utworzonego wcześniej i Zastąp  **<storage access key>**  z hello podstawowy klucz dostępu dla konta magazynu. (Użyj hello takie same wartości jak wcześniej utworzony plik config.json hello).

Alternatywnie można ustawić zmienne środowiskowe w hello [Azure Portal](https://portal.azure.com/):

1. Otwarcie bloku aplikacji sieci web hello klikając **Przeglądaj** > **aplikacje sieci Web** > Nazwa aplikacji sieci web.
2. W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Przewiń w dół toohello **ustawień aplikacji** i Dodaj hello pary klucz wartość.
   
     ![Ustawienia aplikacji](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Kliknij przycisk **SAVE** (Zapisz).

### <a name="publish-hello-application"></a>Publikowanie aplikacji hello
Aplikacja hello toopublish, zatwierdzić tooGit plików kodu hello, a następnie Wypchnij tooazure/główną.

1. Ustaw poświadczenia wdrażania.
   
        azure site deployment user set <name> <password>
2. Dodaj i zatwierdź plików aplikacji.
   
        git add .
        git commit -m "adding files"
3. Wypchnij hello zatwierdzania toohello aplikacji sieci web usługi aplikacji:
   
        git push azure master
   
    Użyj **wzorca** jako hello gałęzi docelowej. Na końcu hello hello wdrożenia zobacz temat instrukcji toohello podobne, poniższy przykład:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Po zakończeniu operacji push hello Przeglądaj URL aplikacji sieci web toohello wcześniej zwrócony przez hello `azure create site` polecenia tooview aplikacji.

## <a name="next-steps"></a>Następne kroki
Gdy hello w tym artykule opisano przy użyciu informacji o toostore usługi tabel hello, można również użyć [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Dodatkowe zasoby
[interfejsu wiersza polecenia Azure]

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

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

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
