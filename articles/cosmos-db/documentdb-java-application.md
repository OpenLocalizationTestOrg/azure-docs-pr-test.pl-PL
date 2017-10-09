---
title: "samouczek tworzenia aplikacji aaaJava przy użyciu bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "W tym samouczku aplikacji sieci web Java pokazano, jak toouse hello Azure DB rozwiązania Cosmos hello toostore interfejsu API usługi DocumentDB i uzyskać dostęp do danych z aplikacji w języku Java hostowanej przez usługę Azure Websites."
keywords: Programowanie aplikacji, samouczek bazy danych, aplikacja Java, samouczek aplikacji sieci Web Java, DocumentDB, Azure, Microsoft Azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Tworzenie aplikacji sieci web Java, przy użyciu bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

W tym samouczku aplikacji sieci web Java przedstawiono sposób toouse hello [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) usługi toostore i danymi dostępu z poziomu aplikacji Java hostowanej przez aplikacje sieci Web usługi aplikacji Azure. W tym artykule przedstawiono:

* Jak toobuild prostą aplikację JavaServer stron (JSP) w programie Eclipse.
* Jak toowork z hello Azure DB rozwiązania Cosmos usługi przy użyciu hello [Azure rozwiązania Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).

W tym samouczku aplikacji Java przedstawiono sposób aplikację do zarządzania zadaniami toocreate opartą na sieci web, możesz toocreate, pobieranie i oznacz zadań jako ukończonych, pokazane na powitania po obrazu. Wszystkie zadania hello na liście ToDo hello są przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos.

![Aplikacja My ToDo List w języku Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> Ten samouczek tworzenia aplikacji zakłada, że masz już pewne doświadczenie w korzystaniu z języka Java. Nowe tooJava lub hello [wstępnie wymaganych narzędzi](#Prerequisites), zalecamy pobranie hello pełną [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projektu z usługi GitHub i skompilowanie go za pomocą [hello instrukcje na końcu hello to artykuł](#GetProject). Po jego skompilowaniu, można przejrzeć hello artykułu toogain wglądu na powitania kod w kontekście hello hello projektu.  
> 
> 

## <a id="Prerequisites"></a>Wymagania wstępne dotyczące tego samouczka aplikacji sieci Web w języku Java
Przed rozpoczęciem tego samouczka tworzenia aplikacji, musi mieć następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/)

    LUB

    Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).
* [Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Środowisko Eclipse IDE for Java EE Developers.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Witryna sieci Web Azure ze środowiskiem uruchomieniowym Java (np. Tomcat lub Jetty) włączone.](../app-service-web/web-sites-java-get-started.md)

Jeśli instalujesz te narzędzia dla powitania po raz pierwszy, witryna coreservlets.com zawiera omówienie procesu instalacji hello hello Szybki Start część ich [samouczek: zainstalowanie TomCat7 i używanie go z Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artykułu.

## <a id="CreateDB"></a>Krok 1: Tworzenie konta bazy danych Azure rozwiązania Cosmos
Zacznijmy od utworzenia konta usługi Azure Cosmos DB. Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: tworzenie aplikacji Java JSP hello](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Krok 2: Tworzenie aplikacji Java JSP hello
Witaj toocreate aplikację JSP:

1. Zacznijmy od utworzenia projektu języka Java. Uruchom środowisko Eclipse, a następnie w menu **File** (Plik) kliknij polecenie **New** (Nowy), a potem kliknij polecenie **Dynamic Web Project** (Dynamiczny projekt sieci Web). Jeśli nie widzisz **dynamiczny projekt sieci Web** na liście dostępnych projektów, hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu**..., rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.
   
    ![Tworzenie aplikacji Java JSP](./media/documentdb-java-application/image10.png)
2. Wprowadź nazwę projektu w hello **Nazwa projektu** pola w hello **docelowe środowisko uruchomieniowe** menu rozwijanego, opcjonalnie wybierz wartość (np. Apache Tomcat v7.0), a następnie kliknij przycisk **Zakończ**. Wybranie docelowego środowiska uruchomieniowego włącza toorun możesz projektu lokalnie za pośrednictwem środowiska Eclipse.
3. W środowisku Eclipse w widoku Project Explorer hello rozwiń projekt. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).
4. W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**. Zachowaj folder nadrzędny hello **WebContent**, jak pokazano w hello następującej ilustracji, a następnie kliknij przycisk **dalej**.
   
    ![Tworzenie nowego pliku JSP — samouczek aplikacji sieci Web w języku Java](./media/documentdb-java-application/image11.png)
5. W hello **wybierz szablon JSP** okno dialogowe hello w celu tego samouczka wybierz **New JSP File (html)**, a następnie kliknij przycisk **Zakończ**.
6. Po otwarciu pliku index.jsp hello w środowisku Eclipse Dodaj tekst toodisplay **Hello World!** w ramach istniejącego hello <body> elementu. Zaktualizowana <body> zawartość powinna wyglądać hello następującego kodu:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Zapisz plik index.jsp hello.
8. Jeśli ustawisz docelowe środowisko uruchomieniowe w kroku 2, możesz kliknąć **projektu** , a następnie **Uruchom** toorun aplikację JSP lokalnie:
   
    ![Witaj świecie – samouczek aplikacji w języku Java](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Krok 3: Instalowanie hello zestawu SDK Java usługi DocumentDB
Witaj Najprostszym sposobem toopull hello zestawu SDK Java usługi DocumentDB i jego zależności jest użycie [Apache Maven](http://maven.apache.org/).

toodo, konieczne będzie tooconvert maven tooa projekt, wykonując następujące kroki hello:

1. Kliknij prawym przyciskiem myszy projekt w hello Eksplorator projektów, kliknij przycisk **Konfiguruj**, kliknij przycisk **przekonwertować tooMaven projektu**.
2. W hello **tworzenie nowych POM** okna, zaakceptuj ustawienia domyślne hello i kliknij przycisk **Zakończ**.
3. W **Eksplorator projektów**, otwórz plik pom.xml hello.
4. Na powitania **zależności** na karcie hello **zależności** okienku, kliknij przycisk **Dodaj**.
5. W hello **wybierz zależności** oknie hello następujące:
   
   * W hello **identyfikator grupy** wprowadź com.microsoft.azure.
   * W hello **identyfikator artefaktu** wprowadź azure-documentdb.
   * W hello **wersji** wprowadź 1.5.1.
     
   ![Instalacja zestawu SDK Java usługi DocumentDB](./media/documentdb-java-application/image13.png)
     
   * Lub Dodaj zależności hello XML dla identyfikatora grupy i identyfikator artefaktu bezpośrednio toohello pom.xml za pomocą edytora tekstu:
     
        <dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency>
6. Kliknij przycisk **OK** i Maven zainstaluje hello zestawu SDK Java usługi DocumentDB.
7. Zapisz plik pom.xml hello.

## <a id="UseService"></a>Krok 4: Przy użyciu usługi Azure DB rozwiązania Cosmos hello w aplikacji Java
1. Najpierw zdefiniujmy obiekt TodoItem hello w TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    W tym projekcie użyto [projektu Lombok](http://projectlombok.org/) toogenerate hello konstruktora, metody pobierające, metody ustawiające i konstruktora. Możesz też ręcznie napisać ten kod lub ma wygenerowania hello IDE.
2. usługi bazy danych Azure rozwiązania Cosmos hello tooinvoke, trzeba utworzyć wystąpienie nowego **DocumentClient**. Ogólnie rzecz biorąc, jest najlepszym hello tooreuse **DocumentClient** — zamiast niż konstruować nowego klienta dla kolejnych żądań. Powitania klienta można ponownie użyć, opakowując powitania klienta w **DocumentClientFactory**. W DocumentClientFactory.java, potrzebujesz toopaste hello URI oraz PRIMARY KEY wartości zapisane tooyour Schowka w [krok 1](#CreateDB). Zastąp [YOUR\_ENDPOINT\_HERE] wartością URI, a [YOUR\_KEY\_HERE] zastąp wartością PRIMARY KEY.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Teraz Utwórzmy tooabstract obiekt DAO (Data Access), utrwalanie naszych tooAzure elementów ToDo DB rozwiązania Cosmos.
   
    W celu wykonania (ToDo) toosave tooa kolekcji należy powitania klienta tooknow które toopersist bazę danych i kolekcję zbyt (wskazywanej przez linki do samego siebie). Ogólnie rzecz biorąc, jest najlepszym toocache hello w bazie danych i kolekcji, jeśli to możliwe tooavoid dodatkowych połączeń toohello w bazie danych.
   
    Witaj poniższy kod ilustruje sposób tooretrieve bazę danych i kolekcji, jeśli istnieje, lub utworzyć nową, jeśli nie istnieje:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. Witaj, następnym krokiem jest toowrite niektórych kodu toopersist hello TodoItems w kolekcji toohello. W tym przykładzie używamy [Gson](https://code.google.com/p/google-gson/) tooserialize i zdeserializować dokumenty tooJSON TodoItem zwykły stare Java obiekty (Pojo).
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Podobnie jak do baz danych i kolekcji usługi Azure Cosmos DB, również do dokumentów można odwoływać się za pomocą linków do samego siebie. Witaj następujących pomocnika funkcja pozwala nam pobierania dokumentów przez inny atrybut (np. "id"), zamiast link do samego siebie:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Możemy użyć metody pomocniczej hello w kroku 5 tooretrieve dokumentu todoitem typu JSON przez identyfikator, a następnie do deserializacji tooa typu POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Możemy również użyć hello DocumentClient tooget kolekcję lub listę obiektów Todoitem przy użyciu usługi DocumentDB SQL:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Istnieje wiele sposobów tooupdate dokument z hello DocumentClient. W aplikacji zarządzającej listą chcemy tootoggle stanie toobe czy zadanie zostało ukończone. Można to osiągnąć przez zaktualizowanie atrybutu "complete" hello w dokumencie hello:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Wreszcie chcemy mieć hello możliwości toodelete czynność do wykonania z naszej listy. toodo, możemy użyć metody pomocnika hello napisaliśmy wcześniej tooretrieve hello link do samego siebie, a następnie powitania klienta toodelete go:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Krok 5: Dołączenie razem pozostałe hello hello projektu tworzenia aplikacji Java
Teraz, gdy już zakończyliśmy hello fun bits - pozostało jest toobuild interfejs użytkownika szybki i połączenie go z zapasowej tooour DAO.

1. Po pierwsze Zacznijmy od utworzenia toocall kontrolera DAO:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    W przypadku bardziej złożonych aplikacji hello kontroler może zawierać skomplikowaną logikę biznesową na powitania DAO.
2. Następnie utworzymy kontrolera toohello serwlet tooroute HTTP żądania:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Potrzebujemy użytkownika toohello toodisplay interfejs użytkownika sieci web. Napiszmy hello index.jsp utworzony wcześniej:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Na koniec, zapisywania i niektóre po stronie klienta JavaScript tootie hello interfejsem użytkownika, a hello serwlet razem:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Fantastycznie! Teraz pozostało to aplikacja hello tootest. Uruchamianie aplikacji hello lokalnie, a następnie dodaj jakieś zadania do wykonania wypełnianie nazwa elementu hello i kategorii, a następnie klikając polecenie **Dodaj zadanie**.
6. Gdy pojawi się element hello, możesz zaktualizować czy jest ono ukończone przełączanie hello wyboru, a następnie klikając polecenie **zadania aktualizacji**.

## <a id="Deploy"></a>Krok 6: Wdrażanie programu Java application tooAzure witryn sieci Web
Witryny sieci Web Azure sprawia, że wdrożenie aplikacji Java sprowadza wyeksportowania aplikacji jako plik WAR i przesłania go na serwer za pomocą kontroli źródła (np. Git) lub FTP.

1. tooexport aplikacji jako plik WAR, kliknij prawym przyciskiem myszy projekt w **Eksplorator projektów**, kliknij przycisk **wyeksportować**, a następnie kliknij przycisk **pliku WAR**.
2. W hello **wyeksportować plik WAR** oknie hello następujące:
   
   * W polu Projekt sieci Web hello wprowadź azure-documentdb-java-sample.
   * W polu miejsce docelowe hello wybierz plik WAR hello toosave docelowego.
   * Kliknij przycisk **Zakończ**.
3. Teraz, gdy masz na plik WAR, możesz po prostu przekazać go tooyour witryny sieci Web Azure **webapps** katalogu. Aby uzyskać instrukcje dotyczące przekazywania pliku hello, zobacz [dodać tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji](../app-service-web/web-sites-java-add-app.md).
   
    Pliku WAR powitania po przekazane toohello katalogu webapps środowisko uruchomieniowe hello wykryje został dodany i załaduje go automatycznie.
4. tooview Zakończono produktu, przejdź toohttp://YOUR\_LOKACJI\_NAME.azurewebsites.net/azure-java-sample/ i zacznij dodawać zadania!

## <a id="GetProject"></a>Pobierz hello projektu z usługi GitHub
Wszystkie przykłady hello w tym samouczku są objęte hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projektu w witrynie GitHub. Projekt todo hello tooimport do środowiska Eclipse, upewnij się, masz hello oprogramowanie i zasobów wymienionych w hello [wymagania wstępne](#Prerequisites) sekcji, a następnie hello następujące:

1. Zainstaluj [Projekt Lombok](http://projectlombok.org/). Lombok jest używane toogenerate konstruktorów, metod pobierających i ustawiających w projekcie hello. Po pobraniu pliku lombok.jar hello, kliknij go dwukrotnie tooinstall go lub go zainstalować z wiersza polecenia hello.
2. Jeśli środowisko Eclipse jest otwarte, zamknij ją i uruchom go ponownie tooload Lombok.
3. W środowisku Eclipse na powitania **pliku** menu, kliknij przycisk **importu**.
4. W hello **importu** okna, kliknij przycisk **Git**, kliknij przycisk **projekty z Git**, a następnie kliknij przycisk **dalej**.
5. Na powitania **wybierz źródło repozytorium** kliknij **identyfikatora URI w klonowania**.
6. Na powitania **źródło repozytorium Git** ekranie powitania **URI** wprowadź https://github.com/Azure-Samples/java-todo-app.git, a następnie kliknij przycisk **dalej**.
7. Na powitania **wybór gałęzi** ekranu, upewnij się, że **wzorca** jest zaznaczone, a następnie kliknij przycisk **dalej**.
8. Na powitania **lokalne miejsce docelowe** kliknij **Przeglądaj** tooselect folder, w którym mogą zostać skopiowane hello repozytorium, a następnie kliknij **dalej**.
9. Na powitania **wybierz toouse Kreatora importowania projektów** ekranu, upewnij się, że **importowanie istniejących projektów** jest zaznaczone, a następnie kliknij przycisk **dalej**.
10. Na powitania **Import projektów** ekranu, usuń zaznaczenie hello **DocumentDB** projektu, a następnie kliknij przycisk **Zakończ**. Projekt DocumentDB Hello zawiera hello Azure rozwiązania Cosmos DB Java SDK, który zostanie dodany jako zależność zamiast tego.
11. W **Eksplorator projektów**, przejdź tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java i Zastąp wartości HOST oraz MASTER_KEY hello hello URI oraz PRIMARY KEY dla Twoje konto bazy danych Azure rozwiązania Cosmos, a następnie zapisz plik hello. Aby uzyskać więcej informacji, zobacz [Krok 1. Tworzenie konta bazy danych Azure DB rozwiązania Cosmos](#CreateDB).
12. W **Eksplorator projektów**, powitania kliknij prawym przyciskiem myszy **azure-documentdb-java-sample**, kliknij przycisk **ścieżkę kompilacji**, a następnie kliknij przycisk **Konfigurowanie kompilacji ścieżki**.
13. Na powitania **ścieżka kompilacji języka Java** ekranu w okienku po prawej stronie powitania, wybierz hello **biblioteki** , a następnie kliknij pozycję **Dodaj zewnętrzne JARs**. Przejdź do lokalizacji pliku lombok.jar hello toohello, a następnie kliknij przycisk **Otwórz**, a następnie kliknij przycisk **OK**.
14. Użyj kroku 12 tooopen hello **właściwości** okna ponownie, a następnie w okienku po lewej stronie powitania kliknij **docelowe środowiska uruchomieniowe**.
15. Na powitania **docelowe środowiska uruchomieniowe** kliknij **nowy**, wybierz pozycję **Apache Tomcat v7.0**, a następnie kliknij przycisk **OK**.
16. Użyj kroku 12 tooopen hello **właściwości** okna ponownie, a następnie w okienku po lewej stronie powitania kliknij **aspekty projektu**.
17. Na powitania **aspekty projektu** ekranu wybierz **dynamiczny moduł sieci Web** i **Java**, a następnie kliknij przycisk **OK**.
18. Na powitania **serwerów** u dołu ekranu hello powitania kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost** , a następnie kliknij przycisk **Dodawanie i usuwanie**.
19. Na powitania **Dodawanie i usuwanie** okna, Przenieś **azure-documentdb-java-sample** toohello **skonfigurowana** , a następnie kliknij przycisk **Zakończ**.
20. W hello **serwerów** kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost**, a następnie kliknij przycisk **ponownego uruchomienia**.
21. W przeglądarce Przejdź toohttp://localhost:8080 / azure-documentdb-java-sample / i zacznij dodawać tooyour listy zadań. Należy pamiętać, że jeśli zmieniono domyślne wartości portów, Zmień wybraną wartość toohello 8080.
22. toodeploy tooan Twojego projektu witryny sieci web platformy Azure, zobacz [krok 6. Wdrażanie programu tooAzure aplikacji witryny sieci Web](#Deploy).

[1]: media/documentdb-java-application/keys.png
