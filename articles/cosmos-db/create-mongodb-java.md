---
title: "Azure Cosmos DB: Tworzenie aplikacji konsolowej przy użyciu języka Java i interfejsu API usługi MongoDB | Microsoft Docs"
description: "Przykładowy kod Java, którego można używać do nawiązywania połączeń z interfejsem API MongoDB usługi Azure Cosmos DB i wykonywania względem niego zapytań"
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
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="2d455-103">Azure Cosmos DB: Tworzenie aplikacji konsolowej interfejsu API usługi MongoDB przy użyciu języka Java i witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2d455-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="2d455-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2d455-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2d455-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="2d455-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2d455-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2d455-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="2d455-107">Następnie utworzysz i wdrożysz aplikację konsolową w oparciu o [sterownik Java MongoDB](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="2d455-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d455-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2d455-108">Prerequisites</span></span>

* <span data-ttu-id="2d455-109">Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="2d455-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="2d455-110">Zestaw JDK 1.7 lub nowszy (uruchom polecenie `apt-get install default-jdk`, jeśli zestaw JDK nie jest zainstalowany)</span><span class="sxs-lookup"><span data-stu-id="2d455-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="2d455-111">Narzędzie Maven (uruchom polecenie `apt-get install maven`, jeśli narzędzie Maven nie jest zainstalowane)</span><span class="sxs-lookup"><span data-stu-id="2d455-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="2d455-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="2d455-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="2d455-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="2d455-113">Add a collection</span></span>

<span data-ttu-id="2d455-114">Nadaj nazwę **db** nowej bazie danych i nazwę **coll** nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2d455-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="2d455-115">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="2d455-115">Clone the sample application</span></span>

<span data-ttu-id="2d455-116">Teraz sklonujemy aplikację interfejsu API usługi MongoDB z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="2d455-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="2d455-117">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="2d455-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="2d455-118">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="2d455-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="2d455-119">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="2d455-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="2d455-120">Następnie otwórz plik rozwiązania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d455-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="2d455-121">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="2d455-121">Review the code</span></span>

<span data-ttu-id="2d455-122">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d455-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="2d455-123">Otwórz plik `Program.cs` i zobacz, że następujące wiersze kodu tworzą zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d455-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="2d455-124">Inicjowanie klienta DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="2d455-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="2d455-125">Tworzenie nowej bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2d455-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="2d455-126">Wstawianie dokumentów za pomocą metody `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="2d455-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="2d455-127">Wykonywanie zapytań za pomocą metody `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="2d455-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="2d455-128">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="2d455-128">Update your connection string</span></span>

<span data-ttu-id="2d455-129">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d455-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="2d455-130">Z poziomu konta wybierz pozycję **Szybki start** i Java, a następnie skopiuj parametry połączenia do Schowka</span><span class="sxs-lookup"><span data-stu-id="2d455-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="2d455-131">Otwórz plik `Program.java` i zastąp argument konstruktora MongoClientURI za pomocą parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="2d455-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="2d455-132">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d455-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="2d455-133">Uruchamianie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="2d455-133">Run the console app</span></span>

1. <span data-ttu-id="2d455-134">Uruchom polecenie `mvn package` w terminalu, aby zainstalować wymagane moduły npm</span><span class="sxs-lookup"><span data-stu-id="2d455-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="2d455-135">Uruchom polecenie `mvn exec:java -D exec.mainClass=GetStarted.Program` w terminalu, aby uruchomić aplikację Java.</span><span class="sxs-lookup"><span data-stu-id="2d455-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="2d455-136">Teraz możesz używać narzędzia [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) do modyfikowania nowych danych, wykonywania zapytań względem nich i pracowania z nimi.</span><span class="sxs-lookup"><span data-stu-id="2d455-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="2d455-137">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2d455-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="2d455-138">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="2d455-138">Clean up resources</span></span>

<span data-ttu-id="2d455-139">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="2d455-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="2d455-140">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="2d455-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="2d455-141">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="2d455-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d455-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d455-142">Next steps</span></span>

<span data-ttu-id="2d455-143">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia kolekcji za pomocą Eksploratora danych i uruchamiania aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="2d455-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="2d455-144">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d455-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d455-145">Importuj dane usługi MongoDB do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2d455-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


