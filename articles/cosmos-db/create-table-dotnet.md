---
title: "aaaBuild aplikacji .NET DB rozwiązania Cosmos Azure przy użyciu hello tabeli interfejsu API | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z interfejsem API tabel usługi Azure Cosmos DB przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="97a8e-103">Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji platformy .NET przy użyciu hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="97a8e-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="97a8e-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="97a8e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="97a8e-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97a8e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="97a8e-106">Przedstawiono to szybki start jak toocreate bazy danych Azure rozwiązania Cosmos kont i Utwórz tabelę w ramach tego konta za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97a8e-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="97a8e-107">Zostanie następnie napisać kod tooinsert, aktualizacji i usuwania jednostek oraz Uruchom kilka zapytań przy użyciu nowego hello [systemu Windows Azure magazynu Premium tabeli](https://aka.ms/premiumtablenuget) pakietu (wersja zapoznawcza) z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="97a8e-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="97a8e-108">Ta biblioteka zawiera hello tej samej klasy i metody podpisy jako publiczny hello [zestawu SDK usługi Magazyn Azure z systemem Windows](https://www.nuget.org/packages/WindowsAzure.Storage), ale ma także hello możliwości tooconnect tooAzure DB rozwiązania Cosmos kont przy użyciu hello [tabeli interfejsu API](table-introduction.md) (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="97a8e-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="97a8e-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97a8e-109">Prerequisites</span></span>

<span data-ttu-id="97a8e-110">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="97a8e-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="97a8e-111">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="97a8e-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="97a8e-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="97a8e-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="97a8e-113">Dodawanie tabeli</span><span class="sxs-lookup"><span data-stu-id="97a8e-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="97a8e-114">Dodawanie danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="97a8e-114">Add sample data</span></span>

<span data-ttu-id="97a8e-115">Teraz można dodać danych tooyour nową tabelę za pomocą Eksploratora danych (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="97a8e-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="97a8e-116">W Eksploratorze danych rozwiń węzeł **sample-table**, kliknij pozycję **Jednostki**, a następnie kliknij przycisk **Dodaj jednostkę**.</span><span class="sxs-lookup"><span data-stu-id="97a8e-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Twórz nowe jednostki w Eksploratorze danych w hello portalu Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="97a8e-118">Teraz Dodaj danych toohello PartitionKey wartość pola i wartość RowKey i kliknij przycisk **Dodaj jednostki**.</span><span class="sxs-lookup"><span data-stu-id="97a8e-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Ustaw hello klucz partycji i klucz wiersza dla nowej jednostki](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="97a8e-120">Można teraz dodać więcej jednostek tooyour tabeli, edytować jednostki lub wyszukiwanie danych w Eksploratorze danych.</span><span class="sxs-lookup"><span data-stu-id="97a8e-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="97a8e-121">Eksplorator danych jest również, gdzie można skalować przepływność sieci i dodać procedury składowane, funkcje zdefiniowane przez użytkownika i wyzwalaczy tooyour tabeli.</span><span class="sxs-lookup"><span data-stu-id="97a8e-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="97a8e-122">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="97a8e-122">Clone hello sample application</span></span>

<span data-ttu-id="97a8e-123">Teraz załóżmy sklonować aplikacji przez tabelę z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="97a8e-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="97a8e-124">Zobaczysz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="97a8e-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="97a8e-125">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="97a8e-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="97a8e-126">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="97a8e-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="97a8e-127">Następnie otwórz plik rozwiązania hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97a8e-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="97a8e-128">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="97a8e-128">Review hello code</span></span>

<span data-ttu-id="97a8e-129">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="97a8e-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="97a8e-130">Hello Otwórz plik Program.cs i tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97a8e-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="97a8e-131">Witaj CloudTableClient został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="97a8e-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="97a8e-132">Tworzenie nowej tabeli, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="97a8e-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="97a8e-133">Tworzenie nowego kontenera tabeli.</span><span class="sxs-lookup"><span data-stu-id="97a8e-133">A new Table container is created.</span></span> <span data-ttu-id="97a8e-134">Można zauważyć ten kod tooregular bardzo podobne magazynu tabel Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="97a8e-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="97a8e-135">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="97a8e-135">Update your connection string</span></span>

<span data-ttu-id="97a8e-136">Teraz będziemy informować hello ciągu połączenia, aplikację można rozmawiać tooAzure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97a8e-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="97a8e-137">W programie Visual Studio Otwórz plik app.config hello.</span><span class="sxs-lookup"><span data-stu-id="97a8e-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="97a8e-138">W hello [portalu Azure](http://portal.azure.com/)w hello Azure DB rozwiązania Cosmos w lewo menu nawigacji, kliknij przycisk **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="97a8e-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="97a8e-139">W nowe okienko powitania kliknij przycisk Kopiuj hello hello ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="97a8e-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Wyświetlanie i kopiowanie w okienku połączenia ciąg hello hello punktu końcowego i klucz konta](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="97a8e-141">Wklej hello wartości w pliku app.config hello jako wartość hello hello PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="97a8e-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="97a8e-142">Możesz pozostawić hello StandardStorageConnectionString jest.</span><span class="sxs-lookup"><span data-stu-id="97a8e-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="97a8e-143">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97a8e-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="97a8e-144">Uruchamianie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="97a8e-144">Run hello web app</span></span>

1. <span data-ttu-id="97a8e-145">W programie Visual Studio, kliknij prawym przyciskiem myszy hello **PremiumTableGetStarted** projektu w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="97a8e-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="97a8e-146">W hello NuGet **Przeglądaj** wpisz *WindowsAzure.Storage PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="97a8e-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="97a8e-147">Sprawdź hello **Uwzględnij wersję wstępną** pole.</span><span class="sxs-lookup"><span data-stu-id="97a8e-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="97a8e-148">Wyniki hello zainstalować hello **WindowsAzure.Storage PremiumTable** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="97a8e-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="97a8e-149">Spowoduje to zainstalowanie Podgląd hello pakietu interfejsu API Azure rozwiązania Cosmos DB tabeli, a także wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="97a8e-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="97a8e-150">Należy pamiętać, że jest pakietem NuGet innego niż hello pakietu Windows Azure Storage używane przez Magazyn tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="97a8e-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="97a8e-151">Kliknij polecenie CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97a8e-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="97a8e-152">okno konsoli Hello wyświetla dane hello dodane, pobieranie, proszeni, zastąpione i usunięty z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="97a8e-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="97a8e-153">Po ukończeniu działania skryptu hello naciśnij dowolnego okna konsoli hello tooclose klucza.</span><span class="sxs-lookup"><span data-stu-id="97a8e-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Dane wyjściowe konsoli hello Szybki Start](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="97a8e-155">Jeśli chcesz, aby toosee hello nowe jednostki w Eksploratorze danych, po prostu komentarz linii 188 208 w pliku program.cs nie są one usunąć, następnie uruchom przykładowe hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="97a8e-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="97a8e-156">Teraz wróć do tooData Explorer, kliknij przycisk **Odśwież**, rozwiń hello **osób** tabeli, a następnie kliknij przycisk **jednostek**, a następnie pracy z tym nowych danych.</span><span class="sxs-lookup"><span data-stu-id="97a8e-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nowe jednostki w Eksploratorze danych](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="97a8e-158">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="97a8e-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="97a8e-159">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="97a8e-159">Clean up resources</span></span>

<span data-ttu-id="97a8e-160">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="97a8e-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="97a8e-161">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="97a8e-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="97a8e-162">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="97a8e-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97a8e-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97a8e-163">Next steps</span></span>

<span data-ttu-id="97a8e-164">W tym szybkiego startu kiedy znasz już jak tworzyć tabel za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="97a8e-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="97a8e-165">Teraz można badać danych przy użyciu hello tabeli interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="97a8e-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="97a8e-166">Zapytanie, używając hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="97a8e-166">Query using hello Table API</span></span>](tutorial-query-table.md)

