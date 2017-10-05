---
title: "Azure Cosmos DB: Tworzenie aplikacji sieci Web za pomocą programu .NET i interfejsu API usługi MongoDB | Microsoft Docs"
description: "Przykładowy kod programu .NET, którego można używać do nawiązywania połączeń z interfejsem API MongoDB usługi Azure Cosmos DB i wykonywania względem niego zapytań"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="e60d7-103">Azure Cosmos DB: Tworzenie aplikacji sieci Web interfejsu API usługi MongoDB za pomocą programu .NET i witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e60d7-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="e60d7-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e60d7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e60d7-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="e60d7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e60d7-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e60d7-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="e60d7-107">Następnie utworzysz i wdrożysz aplikację sieci Web listy zadań w oparciu o [sterownik .NET MongoDB](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="e60d7-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e60d7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e60d7-108">Prerequisites</span></span>

<span data-ttu-id="e60d7-109">Jeśli nie masz jeszcze zainstalowanego programu Visual Studio 2017, możesz pobrać program [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) i używać go **bezpłatnie**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e60d7-110">Podczas instalacji programu Visual Studio upewnij się, że jest włączona opcja **Programowanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="e60d7-111">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="e60d7-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="e60d7-112">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e60d7-112">Clone the sample application</span></span>

<span data-ttu-id="e60d7-113">Teraz sklonujemy aplikację interfejsu API usługi MongoDB z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="e60d7-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="e60d7-114">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="e60d7-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="e60d7-115">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e60d7-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="e60d7-116">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="e60d7-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="e60d7-117">Następnie otwórz plik rozwiązania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e60d7-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="e60d7-118">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="e60d7-118">Review the code</span></span>

<span data-ttu-id="e60d7-119">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e60d7-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="e60d7-120">Otwórz plik **Dal.cs** w katalogu **DAL** i zobacz, że następujące wiersze kodu tworzą zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e60d7-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="e60d7-121">Inicjowanie klienta Mongo.</span><span class="sxs-lookup"><span data-stu-id="e60d7-121">Initialize the Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="e60d7-122">Pobieranie bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e60d7-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="e60d7-123">Pobieranie wszystkich dokumentów.</span><span class="sxs-lookup"><span data-stu-id="e60d7-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="e60d7-124">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="e60d7-124">Update your connection string</span></span>

<span data-ttu-id="e60d7-125">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e60d7-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="e60d7-126">W witrynie [Azure Portal](http://portal.azure.com/), korzystając ze swojego konta usługi Azure Cosmos DB, kliknij na lewym panelu nawigacyjnym pozycję **Parametry połączenia**, a następnie pozycję **Klucze odczytu i zapisu**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e60d7-127">W następnym kroku, korzystając z przycisków kopiowania dostępnych po prawej stronie ekranu, skopiujesz nazwę użytkownika, hasło i hosta do pliku Dal.cs.</span><span class="sxs-lookup"><span data-stu-id="e60d7-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="e60d7-128">Otwórz plik **Dal.cs** w katalogu **DAL**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="e60d7-129">Skopiuj wartość **username** z portalu (przy użyciu przycisku kopiowania) i przypisz ją do klucza **username** w Twoim pliku **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="e60d7-130">Następnie skopiuj wartość **host** z portalu i przypisz ją do klucza **host** w Twoim pliku **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="e60d7-131">Na końcu skopiuj wartość **password** z portalu i przypisz ją do klucza **password** w Twoim pliku **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="e60d7-132">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e60d7-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="e60d7-133">Uruchamianie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="e60d7-133">Run the web app</span></span>

1. <span data-ttu-id="e60d7-134">W programie Visual Studio kliknij projekt prawym przyciskiem myszy w **Eksploratorze rozwiązań**, a następnie kliknij polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="e60d7-135">W polu **Przeglądaj** obszaru pakietów NuGet wpisz ciąg *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="e60d7-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="e60d7-136">Korzystając z wyników, zainstaluj bibliotekę **MongoDB.Driver**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="e60d7-137">Spowoduje to zainstalowanie pakietu MongoDB.Driver, a także wszystkich zależności.</span><span class="sxs-lookup"><span data-stu-id="e60d7-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="e60d7-138">Naciśnij klawisze CTRL + F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="e60d7-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="e60d7-139">Aplikacja zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="e60d7-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="e60d7-140">Kliknij pozycję **Utwórz** w przeglądarce i utwórz kilka nowych zadań w swojej aplikacji listy zadań.</span><span class="sxs-lookup"><span data-stu-id="e60d7-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="e60d7-141">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e60d7-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e60d7-142">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="e60d7-142">Clean up resources</span></span>

<span data-ttu-id="e60d7-143">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="e60d7-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="e60d7-144">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="e60d7-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="e60d7-145">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="e60d7-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e60d7-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e60d7-146">Next steps</span></span>

<span data-ttu-id="e60d7-147">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB i uruchamiania aplikacji sieci Web za pomocą interfejsu API dla usługi MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e60d7-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="e60d7-148">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e60d7-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e60d7-149">Importuj dane do usługi Azure Cosmos DB na potrzeby interfejsu API usługi MongoDB</span><span class="sxs-lookup"><span data-stu-id="e60d7-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

