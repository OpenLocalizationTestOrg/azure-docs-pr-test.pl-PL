---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji sieci web z platformą .NET i hello bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod .NET, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="6cbb4-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z platformą .NET i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6cbb4-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="6cbb4-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6cbb4-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6cbb4-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="6cbb4-107">Będzie tworzenie i wdrażanie aplikacji sieci web listy zadań oparty na powitania [sterownik bazy danych MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="6cbb4-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6cbb4-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6cbb4-108">Prerequisites</span></span>

<span data-ttu-id="6cbb4-109">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6cbb4-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="6cbb4-110">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="6cbb4-111">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="6cbb4-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="6cbb4-112">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6cbb4-112">Clone hello sample application</span></span>

<span data-ttu-id="6cbb4-113">Teraz załóżmy aplikacji w klonowania API bazy danych MongoDB z witryny github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="6cbb4-114">Zobaczysz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="6cbb4-115">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="6cbb4-116">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="6cbb4-117">Następnie otwórz plik rozwiązania hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="6cbb4-118">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="6cbb4-118">Review hello code</span></span>

<span data-ttu-id="6cbb4-119">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="6cbb4-120">Otwórz hello **Dal.cs** plik pod hello **DAL** katalogu i można znaleźć, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="6cbb4-121">Inicjowanie powitania klienta Mongo.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-121">Initialize hello Mongo Client.</span></span>

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

* <span data-ttu-id="6cbb4-122">Pobrać hello bazy danych i kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="6cbb4-123">Pobieranie wszystkich dokumentów.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="6cbb4-124">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="6cbb4-124">Update your connection string</span></span>

<span data-ttu-id="6cbb4-125">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="6cbb4-126">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **ciąg połączenia**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6cbb4-127">Użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania nazwę użytkownika, hasło i hosta do pliku Dal.cs hello w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="6cbb4-128">Otwórz hello **Dal.cs** pliku w hello **DAL** katalogu.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="6cbb4-129">Kopiowania z **nazwy użytkownika** wartości z portalu hello (przy użyciu przycisku Kopiuj hello) i przekształcenie go w hello wartość hello **username** w Twojej **Dal.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="6cbb4-130">Następnie skopiuj z **hosta** wartości z portalu hello i zapewnić ich hello wartość hello **hosta** w Twojej **Dal.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="6cbb4-131">Koniec skopiować z **hasło** wartości z portalu hello i przekształcenie go w hello wartość hello **hasło** w Twojej **Dal.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="6cbb4-132">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="6cbb4-133">Uruchamianie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="6cbb4-133">Run hello web app</span></span>

1. <span data-ttu-id="6cbb4-134">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="6cbb4-135">W hello NuGet **Przeglądaj** wpisz *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="6cbb4-136">Wyniki hello zainstalować hello **MongoDB.Driver** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="6cbb4-137">Spowoduje to zainstalowanie pakietu MongoDB.Driver hello, a także wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="6cbb4-138">Kliknij polecenie CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="6cbb4-139">Aplikacja zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="6cbb4-140">Kliknij przycisk **Utwórz** w hello przeglądarki i Utwórz kilka nowych zadań w aplikacji listy zadań.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="6cbb4-141">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6cbb4-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6cbb4-142">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="6cbb4-142">Clean up resources</span></span>

<span data-ttu-id="6cbb4-143">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6cbb4-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="6cbb4-144">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="6cbb4-145">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cbb4-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cbb4-146">Next steps</span></span>

<span data-ttu-id="6cbb4-147">W tym szybkiego startu kiedy znasz już jak toocreate konta bazy danych Azure rozwiązania Cosmos i uruchomić aplikacji sieci web przy użyciu hello interfejsu API dla bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="6cbb4-148">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="6cbb4-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cbb4-149">Importowanie danych do bazy danych Azure rozwiązania Cosmos dla hello API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="6cbb4-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

