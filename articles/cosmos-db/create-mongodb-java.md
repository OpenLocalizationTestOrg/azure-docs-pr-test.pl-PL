---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji konsoli z językiem Java i hello bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod języka Java, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="b9b3d-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji konsoli API bazy danych MongoDB z językiem Java i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b9b3d-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="b9b3d-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b9b3d-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b9b3d-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="b9b3d-107">Będzie tworzenie i wdrażanie aplikacji konsoli oparty na powitania [sterownik bazy danych MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="b9b3d-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b9b3d-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9b3d-108">Prerequisites</span></span>

* <span data-ttu-id="b9b3d-109">Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="b9b3d-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="b9b3d-110">Zestaw JDK 1.7 lub nowszy (uruchom polecenie `apt-get install default-jdk`, jeśli zestaw JDK nie jest zainstalowany)</span><span class="sxs-lookup"><span data-stu-id="b9b3d-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="b9b3d-111">Narzędzie Maven (uruchom polecenie `apt-get install maven`, jeśli narzędzie Maven nie jest zainstalowane)</span><span class="sxs-lookup"><span data-stu-id="b9b3d-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b9b3d-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="b9b3d-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b9b3d-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="b9b3d-113">Add a collection</span></span>

<span data-ttu-id="b9b3d-114">Nadaj nazwę **db** nowej bazie danych i nazwę **coll** nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b9b3d-115">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b9b3d-115">Clone hello sample application</span></span>

<span data-ttu-id="b9b3d-116">Teraz załóżmy aplikacji w klonowania API bazy danych MongoDB z witryny github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="b9b3d-117">Zobaczysz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b9b3d-118">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="b9b3d-119">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="b9b3d-120">Następnie otwórz plik rozwiązania hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="b9b3d-121">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="b9b3d-121">Review hello code</span></span>

<span data-ttu-id="b9b3d-122">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b9b3d-123">Otwórz hello `Program.cs` pliku, a dane znajdziesz, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b9b3d-124">zainicjowano Hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="b9b3d-125">Tworzenie nowej bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="b9b3d-126">Wstawianie dokumentów za pomocą metody `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="b9b3d-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="b9b3d-127">Wykonywanie zapytań za pomocą metody `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="b9b3d-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b9b3d-128">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="b9b3d-128">Update your connection string</span></span>

<span data-ttu-id="b9b3d-129">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="b9b3d-130">Hello konta, zaznacz **Szybki Start**, wybierz Java, a następnie skopiuj do Schowka tooyour ciąg połączenia hello</span><span class="sxs-lookup"><span data-stu-id="b9b3d-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="b9b3d-131">Otwórz hello `Program.java` plików, Zamień Konstruktor MongoClientURI toohello argument hello hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="b9b3d-132">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="b9b3d-133">Uruchamianie aplikacji konsoli hello</span><span class="sxs-lookup"><span data-stu-id="b9b3d-133">Run hello console app</span></span>

1. <span data-ttu-id="b9b3d-134">Uruchom `mvn package` w terminalu tooinstall wymagane moduły npm</span><span class="sxs-lookup"><span data-stu-id="b9b3d-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="b9b3d-135">Uruchom `mvn exec:java -D exec.mainClass=GetStarted.Program` w terminalu toostart aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="b9b3d-136">Można teraz używać [Robomongo](mongodb-robomongo.md) / [3T w Studio](mongodb-mongochef.md) tooquery, modyfikowania i pracy z tym nowych danych.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b9b3d-137">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b9b3d-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b9b3d-138">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="b9b3d-138">Clean up resources</span></span>

<span data-ttu-id="b9b3d-139">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b9b3d-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="b9b3d-140">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b9b3d-141">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9b3d-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9b3d-142">Next steps</span></span>

<span data-ttu-id="b9b3d-143">W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchamianie aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="b9b3d-144">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="b9b3d-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9b3d-145">Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b9b3d-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


