---
title: "Samouczek tworzenia aplikacji w języku Java za pomocą usługi Azure Cosmos DB | Microsoft Docs"
description: "W tym samouczku aplikacji sieci web Java pokazano, jak używać bazy danych rozwiązania Cosmos Azure i interfejsu API SQL do przechowywania i uzyskiwanie dostępu do danych z aplikacji w języku Java hostowanej przez usługę Azure Websites."
keywords: Projektowanie aplikacji, samouczek bazy danych, aplikacji java, samouczek aplikacji sieci web java, azure, platformy Microsoft azure
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
ms.openlocfilehash: 8507b772c537ac50bd40367fbde260a8d72375ca
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-sql-api"></a>Tworzenie aplikacji sieci web Java, przy użyciu bazy danych rozwiązania Cosmos Azure i interfejsu API SQL
> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Java](sql-api-java-application.md)
> * [Python](sql-api-python-application.md)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

W tym samouczku aplikacji sieci web Java przedstawia sposób użycia [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) Usługa do przechowywania i uzyskać dostęp do danych z poziomu aplikacji Java hostowanej przez aplikacje sieci Web usługi aplikacji Azure. W tym artykule przedstawiono:

* Jak utworzyć prostą aplikację JavaServer stron (JSP) w programie Eclipse.
* Jak pracować z usługą Azure Cosmos DB przy użyciu [zestawu SDK języka Java dla usługi Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).

W tym samouczku aplikacji w języku Java pokazano, jak utworzyć aplikację do zarządzania zadaniami opartą na sieci Web, która pozwala na tworzenie, pobieranie i oznaczanie zadań jako ukończonych, jak pokazano na poniższej ilustracji. Każde z zadań z listy zadań do wykonania będzie przechowywane jako dokument JSON w usłudze Azure Cosmos DB.

![Aplikacja My ToDo List w języku Java](./media/sql-api-java-application/image1.png)

> [!TIP]
> Ten samouczek tworzenia aplikacji zakłada, że masz już pewne doświadczenie w korzystaniu z języka Java. Jeśli nie znasz języka Java lub [wstępnie wymaganych narzędzi](#Prerequisites), zalecamy pobranie kompletnego projektu [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) z usługi GitHub i skompilowanie go zgodnie z [instrukcjami znajdującymi się na końcu artykułu](#GetProject). Po jego skompilowaniu możesz przejrzeć ten artykuł, aby przeanalizować kod w kontekście projektu.  
> 
> 

## <a id="Prerequisites"></a>Wymagania wstępne dotyczące tego samouczka aplikacji sieci Web w języku Java
Przed rozpoczęciem korzystania z tego samouczka tworzenia aplikacji należy dysponować następującymi elementami:

*  Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Środowisko Eclipse IDE for Java EE Developers.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Witryna sieci Web Azure ze środowiskiem uruchomieniowym Java (np. Tomcat lub Jetty) włączone.](../app-service/app-service-web-get-started-java.md)

Jeśli instalujesz te narzędzia po raz pierwszy, witryna coreservlets.com zawiera omówienie procesu instalacji w artykule [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) (Samouczek: Instalacja środowiska TomCat7 i używanie go ze środowiskiem Eclipse) w sekcji Quick Start (Szybki start).

## <a id="CreateDB"></a>Krok 1: Tworzenie konta bazy danych Azure rozwiązania Cosmos
Zacznijmy od utworzenia konta usługi Azure Cosmos DB. Jeśli masz już konto lub jeśli korzystasz z emulatora usługi Azure Cosmos DB na potrzeby tego samouczka, możesz od razu przejść do sekcji [Krok 2. Tworzenie aplikacji Java JSP](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Krok 2. Tworzenie aplikacji Java JSP
Aby utworzyć aplikację JSP:

1. Zacznijmy od utworzenia projektu języka Java. Uruchom środowisko Eclipse, a następnie w menu **File** (Plik) kliknij polecenie **New** (Nowy), a potem kliknij polecenie **Dynamic Web Project** (Dynamiczny projekt sieci Web). Jeśli nie widzisz polecenia **Dynamic Web Project** (Dynamiczny projekt sieci Web) na liście dostępnych projektów, wykonaj następujące czynności: w menu **File** (Plik) kliknij polecenie **New** (Nowy), kliknij polecenie **Project**... (Projekt...), rozwiń pozycję **Web** (Sieć Web), kliknij pozycję **Dynamic Web Project** (Dynamiczny projekt sieci Web) i kliknij przycisk **Next** (Dalej).
   
    ![Tworzenie aplikacji Java JSP](./media/sql-api-java-application/image10.png)
2. Wprowadź nazwę projektu w polu **Project name** (Nazwa projektu) i z menu rozwijanego **Target Runtime** (Docelowe środowisko uruchomieniowe) opcjonalnie wybierz wartość (np. Apache Tomcat v7.0), a następnie kliknij przycisk **Finish** (Zakończ). Wybranie docelowego środowiska uruchomieniowego umożliwia uruchamianie projektu lokalnie za pośrednictwem środowiska Eclipse.
3. W środowisku Eclipse w widoku Project Explorer (Eksplorator projektów) rozwiń projekt. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).
4. W oknie dialogowym **New JSP File** (Nowy plik JSP) nazwij plik **index.jsp**. Pozostaw folder **WebContent** jako folder nadrzędny, w sposób pokazany na poniższej ilustracji, a następnie kliknij przycisk **Next** (Dalej).
   
    ![Tworzenie nowego pliku JSP — samouczek aplikacji sieci Web w języku Java](./media/sql-api-java-application/image11.png)
5. W oknie dialogowym **Select JSP Template** (Wybierz szablon pliku JSP) na potrzeby tego samouczka wybierz szablon **New JSP File (html)**, a następnie kliknij przycisk **Finish** (Zakończ).
6. Po otwarciu pliku index.jsp w środowisku Eclipse dodaj tekst do wyświetlenia **Hello World!** wewnątrz istniejącego elementu <body>. Zaktualizowana zawartość elementu <body> powinna wyglądać podobnie do następującego kodu:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Zapisz plik index.jsp.
8. Jeśli docelowe środowisko uruchomieniowe zostało ustawione w kroku 2, możesz kliknąć pozycję **Project** (Projekt), a następnie pozycję **Run** (Uruchom), aby uruchomić aplikację JSP lokalnie:
   
    ![Witaj świecie – samouczek aplikacji w języku Java](./media/sql-api-java-application/image12.png)

## <a id="InstallSDK"></a>Krok 3: Instalowanie SQL Java SDK
Najprostszym sposobem pobrania zestawu SDK Java SQL i jego zależności jest użycie [Apache Maven](http://maven.apache.org/).

Aby to zrobić, należy przekonwertować projekt na projekt maven, wykonując następujące kroki:

1. Kliknij prawym przyciskiem myszy projekt w widoku Project Explorer (Eksplorator projektów), kliknij polecenie **Configure** (Konfiguruj), kliknij pozycję **Convert to Maven Project** (Konwertuj na projekt Maven).
2. W oknie **Create new POM** (Utwórz nowy plik POM) zaakceptuj wartości domyślne i kliknij przycisk **Finish** (Zakończ).
3. W widoku **Project Explorer** (Eksplorator projektów) otwórz plik pom.xml.
4. Na karcie **Dependencies** (Zależności) w okienku **Dependencies** (Zależności) kliknij pozycję **Add** (Dodaj).
5. W oknie **Select Dependency** (Wybierz zależność) wykonaj następujące czynności:
   
   * W **identyfikator grupy** wprowadź com.microsoft.azure.
   * W **identyfikator artefaktu** wprowadź azure-documentdb.
   * W **wersji** wprowadź 1.5.1.
     
   ![Instalowanie aplikacji Java SQL zestawu SDK](./media/sql-api-java-application/image13.png)
     
   * Lub Dodaj kod XML zależności dla identyfikatora grupy i identyfikator artefaktu bezpośrednio do pliku pom.xml za pomocą edytora tekstu:
     
        <dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency>
6. Kliknij przycisk **OK** i Maven zostanie zainstalowany zestaw SDK Java SQL.
7. Zapisz plik pom.xml.

## <a id="UseService"></a>Krok 4. Korzystanie z usługi Azure Cosmos DB w aplikacji Java
1. Najpierw zdefiniujmy obiekt TodoItem w TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    W tym projekcie użyto [Projektu Lombok](http://projectlombok.org/), aby wygenerować konstruktor, metody pobierające, metody ustawiające i budowniczego. Można też ręcznie napisać ten kod lub wygenerować go za pomocą środowiska IDE.
2. Aby wywołać usługę Azure Cosmos DB, trzeba utworzyć obiekt klasy **DocumentClient**. Ogólnie rzecz biorąc, lepiej jest użyć ponownie obiektu **DocumentClient** niż konstruować nowego klienta dla kolejnych żądań. Klienta można ponownie użyć, opakowując go w **DocumentClientFactory**. W DocumentClientFactory.java, należy wkleić wartości URI oraz PRIMARY KEY, zapisane do Schowka w [krok 1](#CreateDB). Zastąp [YOUR\_ENDPOINT\_HERE] wartością URI, a [YOUR\_KEY\_HERE] zastąp wartością PRIMARY KEY.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Teraz utwórzmy obiekt dostępu do danych (DAO, Data Access Object), aby uabstrakcyjnić utrwalanie zadań do wykonania w usłudze Azure Cosmos DB.
   
    Aby zapisać zadania do wykonania w kolekcji, klient musi wiedzieć, w której bazie danych i kolekcji powinien je zachowywać (jak to jest wskazane przez linki do samego siebie). Ogólnie rzecz biorąc, najlepiej jest zapisać w pamięci podręcznej obiekty bazy danych i kolekcji, tam gdzie to jest możliwe, aby uniknąć dodatkowych połączeń do bazy danych.
   
    Poniższy kod ilustruje, w jaki sposób pobrać bazę danych i kolekcję, jeśli one istnieją, lub utworzyć nowe obiekty, jeśli nie istnieją:
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. Następnym krokiem jest napisanie kodu, który zachowuje obiekty TodoItem w kolekcji. W tym przykładzie używamy narzędzia [Gson](https://code.google.com/p/google-gson/) do serializacji i deserializacji obiektów TodoItem typu Plain Old Java Objects (POJO) do dokumentów JSON.
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Podobnie jak do baz danych i kolekcji usługi Azure Cosmos DB, również do dokumentów można odwoływać się za pomocą linków do samego siebie. Poniższa funkcja pomocnicza pozwala nam pobrać dokumenty przy użyciu innego atrybutu (np. „id”), zamiast linku do samego siebie:
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. Możemy użyć metody pomocniczej z kroku 5 do pobrania dokumentu TodoItem typu JSON przy użyciu atrybutu id, a następnie do deserializacji do obiektu typu POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Możemy również użyć obiektu DocumentClient, aby uzyskać kolekcję lub listę obiektów Todoitem przy użyciu programu SQL:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Istnieje wiele sposobów, aby zaktualizować dokument za pomocą obiektu DocumentClient. W aplikacji zarządzającej listą zadań do wykonania chcemy mieć możliwość przełączania, czy zadanie zostało ukończone. Można to osiągnąć przez zaktualizowanie atrybutu „complete” w dokumencie:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Wreszcie chcemy mieć możliwość usunięcia zadania do wykonania z naszej listy. W tym celu możemy użyć metody pomocniczej, którą napisaliśmy wcześniej, aby pobrać link do samego siebie, a następnie usunąć go za pomocą klienta:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Krok 5. Dołączenie pozostałej części projektu tworzenia aplikacji w języku Java
Teraz, gdy już zakończyliśmy fun bits - pozostało jest tworzenie interfejsu użytkownika szybki i połączenie go z obiektem DAO.

1. Zacznijmy od utworzenia kontrolera do wywoływania obiektu DAO:
   
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
   
    W bardziej złożonej aplikacji kontroler może zawierać skomplikowaną logikę biznesową nałożoną na obiekt DAO.
2. Następnie utworzymy serwlet do rozsyłania żądań HTTP do kontrolera:
   
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
3. Potrzebujemy interfejsu użytkownika sieci web do wyświetlenia dla użytkownika. Napiszmy od nowa utworzony wcześniej plik index.jsp:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. I na koniec fragmentów kodu JavaScript po stronie klienta powiązać interfejs użytkownika sieci web i serwlet razem:
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. Fantastycznie! Teraz pozostało już tylko przetestować aplikację. Uruchom aplikację lokalnie, a następnie dodaj jakieś zadania do wykonania, wpisując nazwę zadania oraz jego kategorię i klikając przycisk **Add Task** (Dodaj zadanie).
6. Gdy zadanie zostanie wyświetlone, można zaktualizować, czy jest ono ukończone, klikając pole wyboru, a następnie klikając przycisk **Update Tasks** (Zaktualizuj zadania).

## <a id="Deploy"></a>Krok 6: Wdrażanie aplikacji w języku Java do witryn sieci Web Azure
Witryny sieci Web Azure sprawia, że wdrożenie aplikacji Java sprowadza wyeksportowania aplikacji jako plik WAR i przesłania go na serwer za pomocą kontroli źródła (np. Git) lub FTP.

1. Aby wyeksportować aplikację jako plik WAR, kliknij prawym przyciskiem myszy projekt w **Eksplorator projektów**, kliknij przycisk **wyeksportować**, a następnie kliknij przycisk **pliku WAR**.
2. W oknie **WAR Export** (Eksport pliku WAR) wykonaj następujące czynności:
   
   * W polu Projekt sieci Web wprowadź tekst azure-documentdb-java-sample.
   * W polu Miejsce docelowe wybierz miejsce zapisania pliku WAR.
   * Kliknij przycisk **Zakończ**.
3. Teraz, gdy masz na plik WAR, możesz po prostu przekazać go do platformy Azure witryny sieci Web **webapps** katalogu. Aby uzyskać instrukcje dotyczące przekazywania pliku, zobacz [dodawania aplikacji Java do aplikacji sieci Web usługi aplikacji Azure](../app-service/web-sites-java-add-app.md).
   
    Po przesłaniu pliku WAR do katalogu webapps środowisko uruchomieniowe wykryje, że plik został dodany, i załaduje go automatycznie.
4. Aby wyświetlić Zakończono produktu, przejdź do http://YOUR\_LOKACJI\_NAME.azurewebsites.net/azure-java-sample/ i zacznij dodawać zadania!

## <a id="GetProject"></a>Pobieranie projektu z usługi GitHub
Wszystkie przykłady w tym samouczku są zawarte w projekcie [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) w usłudze GitHub. Aby zaimportować projekt todo do środowiska Eclipse, upewnij się, że dysponujesz oprogramowaniem i zasobami wymienionymi w sekcji [Wymagania wstępne](#Prerequisites), a następnie wykonaj następujące czynności:

1. Zainstaluj [Projekt Lombok](http://projectlombok.org/). Lombok służy w projekcie do generowania konstruktorów, metod pobierających i ustawiających. Po pobraniu pliku lombok.jar kliknij go dwukrotnie, aby go zainstalować, lub zainstaluj go przy użyciu wiersza polecenia.
2. Jeśli środowisko Eclipse jest otwarte, zamknij je i uruchom ponownie, aby załadować Lombok.
3. W środowisku Eclipse w menu **File** (Plik) kliknij pozycję **Import** (Importuj).
4. W okienku **Import** (Import), kliknij pozycję **Git** (Usługa Git), kliknij pozycję **Projects from Git** (Projekty z usługi Git), a następnie kliknij przycisk **Next** (Dalej).
5. Na ekranie **Select Repository Source** (Wybierz źródło repozytorium) kliknij pozycję **Clone URI** (Klonuj URI).
6. Na **źródło repozytorium Git** ekranu w **URI** wprowadź https://github.com/Azure-Samples/java-todo-app.git, a następnie kliknij przycisk **dalej**.
7. Na ekranie **Branch Selection** (Wybór gałęzi) upewnij się, że jest wybrana gałąź **master**, a następnie kliknij przycisk **Next** (Dalej).
8. Na ekranie **Local Destination** (Lokalne miejsce docelowe) kliknij przycisk **Browse** (Przeglądaj), aby wybrać folder, do którego można skopiować repozytorium, a następnie kliknij przycisk **Next** (Dalej).
9. Na ekranie **Select a wizard to use for importing projects** (Wybór kreatora importującego projekty) upewnij się, że jest zaznaczona opcja **Import existing projects** (Importuj istniejące projekty), a następnie kliknij przycisk **Next** (Dalej).
10. Na ekranie **Import Projects** (Import projektów) usuń zaznaczenie przy projekcie **DocumentDB**, a następnie kliknij przycisk **Finish** (Zakończ). Projekt DocumentDB zawiera Azure rozwiązania Cosmos DB Java SDK, który zostanie dodany jako zależność zamiast tego.
11. W **Eksplorator projektów**, przejdź do azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java i Zastąp wartości HOST oraz MASTER_KEY URI oraz PRIMARY KEY dla użytkownika Azure DB rozwiązania Cosmos konta, a następnie zapisz plik. Aby uzyskać więcej informacji, zobacz [Krok 1. Tworzenie konta bazy danych Azure DB rozwiązania Cosmos](#CreateDB).
12. W widoku **Project Explorer** (Eksplorator projektów) kliknij prawym przyciskiem myszy pozycję **azure-documentdb-java-sample**, kliknij pozycję **Build Path** (Ścieżka kompilacji), a następnie kliknij pozycję **Configure Build Path** (Konfiguruj ścieżkę kompilacji).
13. Na ekranie **Java Build Path** (Ścieżka kompilacji języka Java) w oknie po prawej stronie wybierz kartę **Libraries** (Biblioteki), a następnie kliknij pozycję **Add External JARs** (Dodaj zewnętrzne pliki JAR). Przejdź do lokalizacji pliku lombok.jar, kliknij przycisk **Open** (Otwórz), a następnie kliknij przycisk **OK**.
14. Użyj kroku 12, aby otworzyć ponownie okno **Properties** (Właściwości), a następnie w oknie po lewej stronie kliknij pozycję **Targeted Runtimes** (Docelowe środowiska uruchomieniowe).
15. Na ekranie **Targeted Runtimes** (Docelowe środowiska uruchomieniowe) kliknij pozycję **New** (Nowy), wybierz pozycję **Apache Tomcat v7.0**, a następnie kliknij przycisk **OK**.
16. Użyj kroku 12, aby otworzyć ponownie okno **Properties** (Właściwości), a następnie w oknie po lewej stronie kliknij pozycję **Project Facets** (Aspekty projektu).
17. Na ekranie **Project Facets** (Aspekty projektu) wybierz pozycję **Dynamic Web Module** (Dynamiczny moduł sieci Web) oraz pozycję **Java**, a następnie kliknij pozycję **OK**.
18. Na karcie **Servers** (Serwery) w dolnej części ekranu kliknij prawym przyciskiem myszy pozycję **Tomcat v7.0 Server at localhost**, a następnie kliknij pozycję **Add and Remove** (Dodaj i usuń).
19. W oknie **Add and Remove** (Dodaj i usuń) przenieś pozycję **azure-documentdb-java-sample** w pole **Configured** (Skonfigurowane), a następnie kliknij przycisk **Finish** (Zakończ).
20. W **serwerów** kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost**, a następnie kliknij przycisk **ponownego uruchomienia**.
21. W przeglądarce przejdź do http://localhost:8080/azure-documentdb-java-sample/ i zacznij dodawać zadania do listy. Należy pamiętać, że jeśli zmieniono domyślne wartości portów, zmień 8080 na wybraną wartość.
22. Aby wdrożyć projekt w witrynie sieci Web platformy Azure, zobacz [Krok 6. Wdrażanie aplikacji do witryny sieci Web Azure](#Deploy).

