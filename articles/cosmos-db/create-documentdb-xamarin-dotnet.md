---
title: "Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania Xamarin z uwierzytelnianiem serwisu Facebook | Microsoft Docs"
description: "Przykładowy kod programu .NET, którego można używać do nawiązywania połączeń z usługą Azure Cosmos DB i wykonywania w niej zapytań"
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="cbd6c-103">Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania .NET, Xamarin i uwierzytelniania serwisu Facebook</span><span class="sxs-lookup"><span data-stu-id="cbd6c-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="cbd6c-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cbd6c-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cbd6c-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="cbd6c-107">Następnie zbudujesz i wdrożysz aplikację sieci Web z listą zadań do wykonania bazującą na [interfejsie API usługi DocumentDB platformy .NET](documentdb-sdk-dotnet.md), oprogramowaniu [Xamarin](https://www.xamarin.com/) oraz aparacie uwierzytelniania usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="cbd6c-108">Aplikacja sieci Web z listą zadań do wykonania implementuje wzorzec danych dla poszczególnych użytkowników, który umożliwia użytkownikom zalogowanie się przy użyciu uwierzytelniania serwisu Facebook i zarządzanie własnymi zadaniami do wykonania.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbd6c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cbd6c-109">Prerequisites</span></span>

<span data-ttu-id="cbd6c-110">Jeśli nie masz jeszcze zainstalowanego programu Visual Studio 2017, możesz pobrać program [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) i używać go **bezpłatnie**.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="cbd6c-111">Podczas instalacji programu Visual Studio upewnij się, że jest włączona opcja **Programowanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="cbd6c-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="cbd6c-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="cbd6c-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="cbd6c-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="cbd6c-114">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="cbd6c-114">Clone the sample application</span></span>

<span data-ttu-id="cbd6c-115">Teraz sklonujemy aplikację interfejsu API usługi DocumentDB z repozytorium github, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="cbd6c-116">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="cbd6c-117">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="cbd6c-118">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="cbd6c-119">Następnie w programie Visual Studio otwórz plik DocumentDBTodo.sln z folderu samples/xamarin/UserItems/xamarin.forms.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="cbd6c-120">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="cbd6c-120">Review the code</span></span>

<span data-ttu-id="cbd6c-121">Kod w folderze Xamarin zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cbd6c-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="cbd6c-122">Aplikacja platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-122">Xamarin app.</span></span> <span data-ttu-id="cbd6c-123">Ta aplikacja przechowuje zadania do wykonania użytkownika w partycjonowanej kolekcji o nazwie UserItems.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="cbd6c-124">Interfejs API brokera tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-124">Resource token broker API.</span></span> <span data-ttu-id="cbd6c-125">Prosty interfejs API ASP.NET sieci Web brokera tokenów zasobów usługi Azure Cosmos DB dla zalogowanych użytkowników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="cbd6c-126">Tokeny zasobów to krótkotrwałe tokeny dostępu zapewniające aplikacji dostęp do danych zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="cbd6c-127">Proces uwierzytelniania i przepływu danych zilustrowano na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="cbd6c-128">Kolekcja UserItems została utworzona za pomocą klucza partycji „/userid”.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="cbd6c-129">Określenie klucza partycji dla kolekcji umożliwia usłudze Azure Cosmos DB skalowanie w nieskończoność w miarę zwiększania się liczby użytkowników i zadań.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="cbd6c-130">Aplikacja Xamarin umożliwia użytkownikom logowanie się przy użyciu poświadczeń serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="cbd6c-131">Aplikacja Xamarin używa tokenu dostępu serwisu Facebook do uwierzytelniania za pomocą interfejsu API ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="cbd6c-132">Interfejs API brokera tokenu zasobów uwierzytelnia żądanie przy użyciu funkcji uwierzytelniania usługi App Service i żąda tokenu zasobów usługi Azure Cosmos DB z dostępem do odczytu i zapisu do wszystkich dokumentów korzystających z klucza partycji uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="cbd6c-133">Broker tokenu zasobów zwraca token zasobów dla aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="cbd6c-134">Aplikacja uzyskuje dostęp do zadań do wykonania użytkownika przy użyciu tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-134">The app accesses the user's todo items using the resource token.</span></span>

![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="cbd6c-136">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="cbd6c-136">Update your connection string</span></span>

<span data-ttu-id="cbd6c-137">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="cbd6c-138">W witrynie [Azure Portal](http://portal.azure.com/), korzystając ze swojego konta usługi Azure Cosmos DB, kliknij na lewym panelu nawigacyjnym pozycję **Klucze**, a następnie pozycję **Klucze odczytu i zapisu**.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="cbd6c-139">W następnym kroku, korzystając z przycisków kopiowania dostępnych po prawej stronie ekranu, skopiujesz identyfikator URI i klucz podstawowy do pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="cbd6c-141">W programie Visual Studio 2017 otwórz plik Web.config z folderu azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="cbd6c-142">Skopiuj wartość identyfikatora URI z portalu (przy użyciu przycisku kopiowania) i przypisz ją do klucza accountUrl w pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="cbd6c-143">Następnie skopiuj wartość klucza podstawowego z portalu i przypisz ją do klucza accountKey w pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="cbd6c-144">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="cbd6c-145">Budowanie i wdrażanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cbd6c-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="cbd6c-146">W witrynie Azure Portal utwórz witrynę sieci Web usługi App Service, która będzie hostowała interfejs API brokera tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="cbd6c-147">W witrynie Azure Portal otwórz blok Ustawienia aplikacji witryny sieci Web interfejsu API brokera tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="cbd6c-148">Wypełnij następujące ustawienia aplikacji:</span><span class="sxs-lookup"><span data-stu-id="cbd6c-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="cbd6c-149">accountUrl — adres URL konta usługi Azure Cosmos DB z karty Klucze konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="cbd6c-150">accountKey — klucz główny konta usługi Azure Cosmos DB z karty Klucze konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="cbd6c-151">Identyfikatory databaseId i collectionId utworzonej bazy danych oraz kolekcji.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="cbd6c-152">Opublikuj rozwiązanie ResourceTokenBroker w utworzonej witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="cbd6c-153">Otwórz projekt Xamarin i przejdź do pliku TodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="cbd6c-154">Podaj wartości dla właściwości accountURL, collectionId i databaseId, a także dla właściwości resourceTokenBrokerURL będącej podstawowym adresem URL HTTPS witryny sieci Web brokera tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="cbd6c-155">Ukończ samouczek [Jak skonfigurować aplikację App Service, aby używała logowania do usługi Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md), aby skonfigurować uwierzytelnianie serwisu Facebook i witrynę sieci Web ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="cbd6c-156">Uruchom aplikację platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="cbd6c-157">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cbd6c-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cbd6c-158">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="cbd6c-158">Clean up resources</span></span>

<span data-ttu-id="cbd6c-159">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="cbd6c-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="cbd6c-160">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego właśnie zasobu.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="cbd6c-161">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbd6c-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cbd6c-162">Next steps</span></span>

<span data-ttu-id="cbd6c-163">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia kolekcji za pomocą Eksploratora danych i budowania oraz wdrażania aplikacji platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="cbd6c-164">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cbd6c-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cbd6c-165">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cbd6c-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
