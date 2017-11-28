---
title: "Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania Xamarin z uwierzytelnianiem serwisu Facebook | Microsoft Docs"
description: "Przedstawia przykładowy kod .NET, można użyć tooconnect tooand zapytania bazy danych Azure rozwiązania Cosmos"
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="bc541-103">Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania .NET, Xamarin i uwierzytelniania serwisu Facebook</span><span class="sxs-lookup"><span data-stu-id="bc541-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="bc541-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bc541-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bc541-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bc541-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bc541-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bc541-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="bc541-107">Będzie tworzenie i wdrażanie aplikacji sieci web listy todo oparty na powitania [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)i hello Azure DB rozwiązania Cosmos autoryzacji aparatu.</span><span class="sxs-lookup"><span data-stu-id="bc541-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="bc541-108">Aplikacja sieci web listy rzeczy do zrobienia Hello implementuje wzorzec danych użytkownika, który umożliwia toologin użytkowników przy użyciu uwierzytelniania serwisu Facebook i zarządzaj nimi własnych elementów toodo.</span><span class="sxs-lookup"><span data-stu-id="bc541-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc541-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc541-109">Prerequisites</span></span>

<span data-ttu-id="bc541-110">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bc541-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bc541-111">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bc541-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="bc541-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="bc541-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="bc541-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bc541-114">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bc541-114">Clone hello sample application</span></span>

<span data-ttu-id="bc541-115">Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="bc541-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="bc541-116">Zobaczysz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="bc541-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="bc541-117">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="bc541-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="bc541-118">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bc541-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="bc541-119">Następnie otwórz plik DocumentDBTodo.sln hello z folderu samples/xamarin/UserItems/xamarin.forms hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc541-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="bc541-120">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="bc541-120">Review hello code</span></span>

<span data-ttu-id="bc541-121">Witaj w folderze Xamarin hello w kodzie:</span><span class="sxs-lookup"><span data-stu-id="bc541-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="bc541-122">Aplikacja platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bc541-122">Xamarin app.</span></span> <span data-ttu-id="bc541-123">Aplikacja Hello przechowuje elementy hello użytkownika w podzielonym na partycje kolekcję o nazwie UserItems.</span><span class="sxs-lookup"><span data-stu-id="bc541-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="bc541-124">Interfejs API brokera tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="bc541-124">Resource token broker API.</span></span> <span data-ttu-id="bc541-125">Proste zasobów bazy danych Azure rozwiązania Cosmos toobroker ASP.NET Web API tokeny toohello zalogowani użytkownicy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="bc541-126">Tokeny zasobu to tokeny dostępu krótkim okresie udostępnianie aplikacji hello hello toohello dostęp zalogowany danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc541-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="bc541-127">Przepływ uwierzytelniania i danych Hello przedstawiono na poniższym diagramie hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="bc541-128">Witaj UserItems kolekcji jest tworzony z kluczem partycji hello "/ Nazwa użytkownika".</span><span class="sxs-lookup"><span data-stu-id="bc541-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="bc541-129">Określanie klucza partycji dla kolekcji umożliwia tooscale bazy danych Azure rozwiązania Cosmos nieograniczonej jako hello wielu użytkowników oraz elementy rozwoju.</span><span class="sxs-lookup"><span data-stu-id="bc541-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="bc541-130">Aplikacja Xamarin Hello umożliwia toologin użytkowników przy użyciu poświadczeń usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="bc541-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="bc541-131">Aplikacja Xamarin Hello używa tooauthenticate token dostępu usługi Facebook z interfejsem API ResourceTokenBroker</span><span class="sxs-lookup"><span data-stu-id="bc541-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="bc541-132">broker tokenu Hello zasobu interfejsu API uwierzytelnia hello żądania przy użyciu funkcji uwierzytelniania usługi aplikacji i żądania tokenu zasobów bazy danych Azure rozwiązania Cosmos z dokumentami tooall dostęp do odczytu/zapisu udostępniania klucza partycji hello uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc541-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="bc541-133">Zasób brokera tokenu zwraca hello zasobów toohello tokenu klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc541-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="bc541-134">Aplikacja Hello uzyskuje dostęp do elementów todo hello użytkownika za pomocą hello token zasobu.</span><span class="sxs-lookup"><span data-stu-id="bc541-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="bc541-136">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="bc541-136">Update your connection string</span></span>

<span data-ttu-id="bc541-137">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="bc541-138">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="bc541-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bc541-139">W pliku Web.config hello w następnym kroku hello użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania identyfikatora URI oraz Primary Key.</span><span class="sxs-lookup"><span data-stu-id="bc541-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="bc541-141">W programie Visual Studio 2017 r Otwórz plik Web.config hello hello azure-documentdb-dotnet/przykłady/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folderu.</span><span class="sxs-lookup"><span data-stu-id="bc541-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="bc541-142">Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość accountUrl hello w pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="bc541-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="bc541-143">Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość accountKey hello w Web.congif.</span><span class="sxs-lookup"><span data-stu-id="bc541-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="bc541-144">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bc541-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="bc541-145">Tworzenie i wdrażanie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="bc541-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="bc541-146">Tworzenie aplikacji witryny sieci Web toohost hello zasobów tokenu brokera usług interfejsu API hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bc541-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="bc541-147">Hello portalu Azure Otwórz blok ustawień aplikacji hello brokera tokenu hello zasobów witryny sieci Web interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bc541-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="bc541-148">Wypełnij następujące ustawienia aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="bc541-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="bc541-149">accountUrl — adres URL konta bazy danych Azure rozwiązania Cosmos hello klucze hello na karcie Konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bc541-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="bc541-150">accountKey - klucza głównego konta bazy danych Azure rozwiązania Cosmos hello klucze hello na karcie Konto bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bc541-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="bc541-151">Identyfikatory databaseId i collectionId utworzonej bazy danych oraz kolekcji.</span><span class="sxs-lookup"><span data-stu-id="bc541-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="bc541-152">Opublikuj hello tooyour rozwiązania ResourceTokenBroker utworzyć witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bc541-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="bc541-153">Otwórz projekt Xamarin hello, a następnie przejdź tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="bc541-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="bc541-154">Podaj wartości hello accountURL, collectionId, databaseId, a także resourceTokenBrokerURL jako adres url https podstawowej hello hello zasobu brokera tokenu witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bc541-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="bc541-155">Pełną hello [jak tooconfigure logowanie Facebook toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup samouczka uwierzytelniania serwisu Facebook i konfigurować witrynę ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="bc541-156">Uruchamianie aplikacji platformy Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="bc541-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="bc541-157">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bc541-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bc541-158">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="bc541-158">Clean up resources</span></span>

<span data-ttu-id="bc541-159">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bc541-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="bc541-160">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="bc541-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="bc541-161">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="bc541-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc541-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc541-162">Next steps</span></span>

<span data-ttu-id="bc541-163">W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos Utwórz kolekcję przy użyciu hello Eksploratora danych i tworzenia i wdrażania aplikacji platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bc541-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="bc541-164">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="bc541-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc541-165">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bc541-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
