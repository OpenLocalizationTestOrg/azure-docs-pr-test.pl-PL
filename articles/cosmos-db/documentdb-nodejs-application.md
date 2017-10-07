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
# <a name="_Toc395783175"></a>Tworzenie aplikacji internetowej Node.js za pomocą usługi Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

W tym samouczku środowiska Node.js pokazano, jak toouse bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB toostore i danymi dostępu z poziomu aplikacji Node.js Express hostowanej przez usługę Azure Websites. Utworzysz prostą, opartą na sieci Web aplikację do zarządzania zadaniami (aplikację ToDo), która umożliwia tworzenie, pobieranie i kończenie zadań. Witaj zadania są przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos. Ten samouczek przeprowadzi Cię przez kolejne hello tworzenia i wdrażania aplikacji hello i opisano, co dzieje się w każdym fragment kodu.

![Zrzut ekranu przedstawiający hello aplikacji My Todo List utworzonej w tym samouczku środowiska Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Nie masz czasu toocomplete hello samouczka i po prostu chcesz tooget hello kompletne rozwiązanie? Nie ma problemu, możesz uzyskać hello kompletne przykładowe rozwiązanie z [GitHub][GitHub]. Tylko odczytać hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) pliku, aby uzyskać instrukcje dotyczące sposobu toorun hello aplikacji.

## <a name="_Toc395783176"></a>Wymagania wstępne
> [!TIP]
> Ten samouczek środowiska Node.js zakłada, że masz już pewne doświadczenie w korzystaniu ze środowiska Node.js i usługi Azure Websites.
> 
> 

Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

   LUB

   Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) (tylko system Windows).
* [Node.js][Node.js] w wersji 0.10.29 lub nowszej.
* [Generator Express](http://www.expressjs.com/starter/generator.html) (można go zainstalować za pomocą polecenia `npm install express-generator -g`)
* [Git][Git].

## <a name="_Toc395637761"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB
Zacznijmy od utworzenia konta usługi Azure Cosmos DB. Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: Tworzenie nowej aplikacji Node.js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Krok 2: Tworzenie nowej aplikacji Node.js
Teraz nauczysz się toocreate podstawowego projektu Hello World Node.js przy użyciu hello [Express](http://expressjs.com/) framework.

1. Otwórz swój ulubiony terminal, takich jak wiersza polecenia Node.js hello.
2. Przejdź toohello katalogu, w którym mają toostore hello nowej aplikacji.
3. Użyj toogenerate express generator hello nową aplikację o nazwie **todo**.
   
        express todo
4. Otwórz nowy katalog **todo** i zainstaluj zależności.
   
        cd todo
        npm install
5. Uruchom nową aplikację.
   
        npm start
6. Możesz wyświetlić swoją nową aplikację, przechodząc w przeglądarce za[http://localhost: 3000](http://localhost:3000).
   
    ![Poznaj środowisko Node.js — zrzut ekranu przedstawiający hello aplikacji Hello World w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Następnie toostop hello aplikacji, naciśnij klawisze CTRL + C w hello okno terminalu, a następnie kliknij przycisk **y** tooterminate hello wsadowym.

## <a name="_Toc395783179"></a>Krok 3. Instalowanie dodatkowych modułów
Witaj **package.json** plik jest jeden z plików hello tworzone w katalogu głównym hello hello projektu. Ten plik zawiera listę dodatkowych modułów, które są wymagane dla aplikacji Node.js. Później podczas wdrażania tej aplikacji tooAzure witryn sieci Web, ten plik jest używany toodetermine, które moduły muszą toobe zainstalowanym Azure toosupport aplikacji. Nadal musisz tooinstall dwa pakiety dla tego samouczka.

1. W terminalu hello, zainstaluj hello **async** modułu za pomocą Menedżera npm.
   
        npm install async --save
2. Zainstaluj hello **documentdb** modułu za pomocą Menedżera npm. Jest to moduł hello gdzie sytuacji wszystkie hello Azure DB rozwiązania Cosmos magic.
   
        npm install documentdb --save
3. Szybkie sprawdzenie hello **package.json** pliku aplikacji hello powinny być widoczne w hello dodatkowych modułów. Ten plik będzie Poinformuj Azure toodownload pakiety, które i zainstalować podczas uruchamiania aplikacji. Powinien on przypominać przykład Witaj poniżej.
   
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
   
    W ten sposób węzeł (a potem platforma Azure) otrzyma informacje o tym, że aplikacja zależy od dodatkowych modułów.

## <a name="_Toc395783180"></a>Krok 4: Przy użyciu usługi Azure DB rozwiązania Cosmos hello w aplikacji node
Która zajmuje się wszystkie hello wstępną instalację i konfigurację, teraz załóżmy get dół toowhy jesteśmy tutaj i jest toowrite niektórych w kodzie za pomocą bazy danych Azure rozwiązania Cosmos.

### <a name="create-hello-model"></a>Tworzenie modelu hello
1. W katalogu projektu hello, Utwórz nowy katalog o nazwie **modele** hello — w tym samym katalogu co plik package.json hello.
2. W hello **modele** katalogu, Utwórz nowy plik o nazwie **taskDao.js**. Ten plik zawiera model hello hello zadań tworzonych przez naszą aplikację.
3. W hello sam **modele** katalogu, Utwórz nowy plik o nazwie **docdbUtils.js**. Ten plik będzie zawierał pewną ilość przydatnego kodu do ponownego wykorzystania, który będzie używany w naszej aplikacji. 
4. Kopiuj hello poniższy kod w zbyt**docdbUtils.js**
   
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
   
5. Zapisz i zamknij hello **docdbUtils.js** pliku.
6. Na początku hello hello **taskDao.js** plików, dodawanie hello następującego kodu tooreference hello **DocumentDBClient** i hello **docdbUtils.js** utworzyliśmy powyżej:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Następnie zostanie Dodaj kod toodefine i wyeksportować hello obiektu zadania. Jest on odpowiedzialny za inicjowanie obiektu Task oraz konfigurowanie hello bazy danych i kolekcji dokumentów, które będą używane.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Następnie dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.
   
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
9. Zapisz i zamknij hello **taskDao.js** pliku. 

### <a name="create-hello-controller"></a>Tworzenie kontrolera hello
1. W hello **tras** katalogu projektu Utwórz nowy plik o nazwie **tasklist.js**. 
2. Dodaj hello zbyt następującego kodu**tasklist.js**. Spowoduje to załadowanie modułów hello DocumentDBClient i async, które są używane przez **tasklist.js**. To też definiowany hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Kontynuować dodawanie toohello **tasklist.js** przez dodanie metody hello używane zbyt**showTasks, addTask**, i **completeTasks**:
   
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
4. Zapisz i zamknij hello **tasklist.js** pliku.

### <a name="add-configjs"></a>Dodawanie pliku config.js
1. W katalogu projektu utwórz nowy plik o nazwie **config.js**.
2. Dodaje hello zbyt**config.js**. Służy on do definiowania ustawień konfiguracji i wartości potrzebnych dla aplikacji.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. W hello **config.js** plików aktualizacji hello wartości HOST i AUTH_KEY przy użyciu wartości hello znajdujące się w bloku klucze hello konta bazy danych Azure rozwiązania Cosmos na powitania [portalu Microsoft Azure](https://portal.azure.com).
4. Zapisz i zamknij hello **config.js** pliku.

### <a name="modify-appjs"></a>Modyfikowanie pliku app.js
1. W katalogu projektu hello, otwórz hello **app.js** pliku. Ten plik został utworzony wcześniej podczas tworzenia aplikacji sieci web Express hello.
2. Dodaj następującego kodu toohello początku hello **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Ten kod definiuje toobe pliku config hello używane i przechodzi do niektóre zmienne, których będziemy wkrótce używać tooread wartości z tego pliku.
4. Zastąp następujące dwa wiersze w hello **app.js** pliku:
   
        app.use('/', index);
        app.use('/users', users); 
   
      z powitania po fragment kodu:
   
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
5. Te wiersze definiują nowe wystąpienie klasy naszych **TaskDao** obiektu z nowego tooAzure połączenia DB rozwiązania Cosmos (przy użyciu wartości hello odczytywać hello **config.js**), inicjowanie obiektu task hello i następnie wiążą akcje formularza toomethods na naszych **TaskList** kontrolera. 
6. Na koniec Zapisz i zamknij hello **app.js** pliku, już prawie koniec.

## <a name="_Toc395783181"></a>Krok 5. Tworzenie interfejsu użytkownika
Teraz możemy zacząć naszych interfejsu użytkownika hello toobuilding uwagi, użytkownik może faktycznie wchodzić w interakcję z naszą aplikacją. Witaj używa utworzona aplikacja Express **Jade** jako hello aparatu widoku. Aby uzyskać więcej informacji na temat Jade można znaleźć zbyt[http://jade-lang.com/](http://jade-lang.com/).

1. Witaj **layout.jade** pliku w hello **widoków** katalog jest używany jako szablon globalny dla innych **jade** plików. W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej witryny sieci Web. 
2. Otwórz hello **layout.jade** w hello można znaleźć pliku **widoków** folderu i Zastąp zawartość hello hello następujący:

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

    Informuje hello **Jade** aparat toorender kod HTML dla aplikacji i tworzy **bloku** o nazwie **zawartości** którym można udostępnić układ hello naszej zawartości strony.

    Zapisz i zamknij ten plik **layout.jade**.

3. Teraz Otwórz hello **index.jade** plik, hello widok, który będzie używany przez naszą aplikację i Zastąp zawartość pliku hello hello hello poniżej:
   
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
   

To rozszerza on układ i udostępnia zawartość dla hello **zawartości** symbolu zastępczego widzieliśmy w hello **layout.jade** wcześniej.
   
W tym układzie utworzyliśmy dwa formularze HTML.

Witaj pierwszy formularz zawiera tabelę danych i przycisk umożliwiający wykonywanie elementów tooupdate przez zbyt księgowej**/completetask** metody kontrolera.
    
Witaj drugi formularz zawiera dwa pola wejściowe i przycisk umożliwiający wykonywanie toocreate nowy element przez zbyt księgowej**/addtask** metody kontrolera.

Powinno to być wszystkie wymagane dla toowork naszej aplikacji.

## <a name="_Toc395783181"></a>Krok 6. Uruchamianie aplikacji lokalnie
1. Aplikacja hello tootest na komputerze lokalnym, uruchom `npm start` w hello terminali toostart aplikacji, a następnie Odśwież Twojej [http://localhost: 3000](http://localhost:3000) strona przeglądarki. Strona Hello powinna wyglądać tak jak hello obraz poniżej:
   
    ![Zrzut ekranu przedstawiający hello aplikacji MyTodo List w oknie przeglądarki](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Jeśli zostanie wyświetlony błąd o wcięcie hello w pliku layout.jade hello lub index.jade hello, upewnij się, że hello pierwsze dwa wiersze w obu plików jest wyrównane do lewej, nie może zawierać spacji. Jeśli istnieją spacje przed hello pierwsze dwa wiersze, usuń je, Zapisz oba pliki, a następnie odśwież okno przeglądarki. 

2. Użyj hello elementu, nazwę elementu i kategorii pól tooenter nowego zadania, a następnie kliknij przycisk **Dodaj element**. Spowoduje to utworzenie w usłudze Azure Cosmos DB dokumentu z tymi właściwościami. 
3. Strona Hello należy zaktualizować hello toodisplay nowo utworzony element na liście ToDo hello.
   
    ![Zrzut ekranu aplikacji hello z nowym elementem na liście ToDo hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete zadania, po prostu zaznacz pole wyboru hello w kolumnie pełną hello, a następnie kliknij **aktualizowanie zadań**. Spowoduje to zaktualizowanie dokumentu hello już utworzone.

5. Aplikacja hello toostop, naciśnij klawisze CTRL + C w hello okno terminalu, a następnie kliknij przycisk **Y** tooterminate hello wsadowym.

## <a name="_Toc395783182"></a>Krok 7: Wdrażanie tooAzure projektu Twojej aplikacji projektowanie witryn sieci Web
1. Jeśli jeszcze tego nie zrobiono, włącz repozytorium Git dla usługi Azure Websites. Instrukcje można znaleźć na temat toodo to w hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](../app-service-web/app-service-deploy-local-git.md) tematu.
2. Dodaj witrynę sieci Web platformy Azure jako element zdalny narzędzia Git.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Wdróż przez wypchnięcie toohello zdalnego.
   
        git push azure master
4. W ciągu kilku sekund git zakończy publikowanie aplikacji sieci web i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!

    Gratulacje! Możesz po prostu utworzone pierwszego Node.js Express aplikacji sieci Web przy użyciu bazy danych Azure rozwiązania Cosmos i opublikować ją tooAzure witryn sieci Web.

    Toodownload lub toohello kompletnej aplikacji referencyjnej można znaleźć w tym samouczku, można go pobrać z [GitHub][GitHub].

## <a name="_Toc395637775"></a>Następne kroki

* Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform? Zobacz [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) (Testowanie wydajności i skali w usłudze Azure Cosmos DB)
* Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* Eksploruj hello [dokumentacji bazy danych Azure rozwiązania Cosmos](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

