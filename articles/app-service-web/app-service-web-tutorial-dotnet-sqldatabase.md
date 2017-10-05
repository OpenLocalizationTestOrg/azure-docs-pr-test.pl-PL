---
title: "Tworzenie aplikacji platformy ASP.NET na platformie Azure w usłudze SQL Database | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pobrać aplikację ASP.NET, działa na platformie Azure w ramach połączenia z bazą danych SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="724f2-103">Tworzenie aplikacji platformy ASP.NET na platformie Azure z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="724f2-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="724f2-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="724f2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="724f2-105">Ten samouczek pokazuje, jak wdrożyć aplikację sieci web platformy ASP.NET opartych na danych na platformie Azure i połącz go z [bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="724f2-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="724f2-106">Po zakończeniu, masz aplikację ASP.NET działającą w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) i połączona z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="724f2-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="724f2-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="724f2-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="724f2-109">Tworzenie bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="724f2-110">Połącz aplikację ASP.NET do bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="724f2-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="724f2-111">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="724f2-112">Aktualizacja modelu danych i ponownie wdrożyć aplikację</span><span class="sxs-lookup"><span data-stu-id="724f2-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="724f2-113">Strumieniowe przesyłanie dzienników z platformy Azure na terminalu</span><span class="sxs-lookup"><span data-stu-id="724f2-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="724f2-114">Zarządzanie aplikacją w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="724f2-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="724f2-115">Prerequisites</span></span>

<span data-ttu-id="724f2-116">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="724f2-116">To complete this tutorial:</span></span>

* <span data-ttu-id="724f2-117">Zainstaluj program [Visual Studio 2017](https://www.visualstudio.com/downloads/) z następującymi pakietami roboczymi:</span><span class="sxs-lookup"><span data-stu-id="724f2-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="724f2-118">**Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych**</span><span class="sxs-lookup"><span data-stu-id="724f2-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="724f2-119">**Tworzenie aplikacji na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="724f2-119">**Azure development**</span></span>

  ![Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych oraz tworzenie aplikacji na platformie Azure (w ramach Internetu i chmury)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="724f2-121">Pobierz przykład</span><span class="sxs-lookup"><span data-stu-id="724f2-121">Download the sample</span></span>

<span data-ttu-id="724f2-122">[Pobierz przykładowy projekt](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="724f2-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="724f2-123">Wyodrębnij (Rozpakuj) *dotnet-sqldb — samouczek master.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="724f2-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="724f2-124">Przykładowy projekt zawiera basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Tworzenie odczytu aktualizowania i usuwania) aplikacji w usłudze [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="724f2-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="724f2-125">Uruchomienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="724f2-125">Run the app</span></span>

<span data-ttu-id="724f2-126">Otwórz *dotnet-sqldb — samouczek — wzorzec/DotNetAppSqlDb.sln* pliku w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724f2-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="724f2-127">Typ `Ctrl+F5` do uruchomienia aplikacji bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="724f2-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="724f2-128">Aplikacja jest wyświetlana w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="724f2-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="724f2-129">Wybierz **Utwórz nowy** link i Utwórz kilka *zadań do wykonania* elementów.</span><span class="sxs-lookup"><span data-stu-id="724f2-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Okno dialogowe Nowy projekt ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="724f2-131">Test **Edytuj**, **szczegóły**, i **usunąć** łącza.</span><span class="sxs-lookup"><span data-stu-id="724f2-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="724f2-132">Aplikacja używa kontekstu bazy danych do połączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="724f2-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="724f2-133">W tym przykładzie kontekst bazy danych używa parametrów połączenia o nazwie `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="724f2-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="724f2-134">Ustawiono parametrów połączenia *Web.config* plików i do którego odwołuje się *Models/MyDatabaseContext.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="724f2-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="724f2-135">Nazwa ciągu połączenia jest używany w dalszej części samouczka Aby połączyć aplikację sieci web platformy Azure z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="724f2-136">Publikowanie na platformie Azure z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="724f2-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="724f2-137">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy użytkownika **DotNetAppSqlDb** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="724f2-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publikowanie z Eksploratora rozwiązań](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="724f2-139">Upewnij się, że jest zaznaczona usługa **Microsoft Azure App Service**, a następnie kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="724f2-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publikowanie ze strony przeglądu projektu](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="724f2-141">Publikowanie otwiera **Tworzenie usługi App Service** okno dialogowe, które ułatwia tworzenie zasobów Azure należy uruchomić aplikację sieci web programu ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="724f2-142">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-142">Sign in to Azure</span></span>

<span data-ttu-id="724f2-143">W oknie dialogowym **Tworzenie usługi App Service** kliknij pozycję **Dodaj konto**, a następnie zaloguj się do swojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="724f2-144">Jeśli zalogowano się już do konta Microsoft, upewnij się, że to konto zawiera Twoją subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="724f2-145">Jeśli użyte do logowania konto Microsoft nie ma subskrypcji platformy Azure, kliknij je, aby dodać prawidłowe konto.</span><span class="sxs-lookup"><span data-stu-id="724f2-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Logowanie do platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="724f2-147">Po zalogowaniu możesz w tym oknie dialogowym utworzyć wszystkie zasoby potrzebne dla aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="724f2-148">Konfigurowanie nazwy aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="724f2-148">Configure the web app name</span></span>

<span data-ttu-id="724f2-149">Zachowaj nazwę aplikacji sieci web wygenerowany lub zmień ją na inną nazwę unikatową (prawidłowe znaki to `a-z`, `0-9`, i `-`).</span><span class="sxs-lookup"><span data-stu-id="724f2-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="724f2-150">Nazwa aplikacji sieci web jest używana jako część domyślnego adresu URL dla aplikacji (`<app_name>.azurewebsites.net`, gdzie `<app_name>` oznacza nazwę aplikacji sieci web).</span><span class="sxs-lookup"><span data-stu-id="724f2-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="724f2-151">Nazwa aplikacji sieci web musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Tworzenie aplikacji usługi z okna dialogowego](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="724f2-153">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="724f2-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="724f2-154">Obok pozycji **Grupa zasobów** kliknij przycisk **Nowa**.</span><span class="sxs-lookup"><span data-stu-id="724f2-154">Next to **Resource Group**, click **New**.</span></span>

![Obok grupy zasobów kliknij przycisk Nowy.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="724f2-156">Określ nazwę grupy zasobów **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="724f2-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="724f2-157">Nie klikaj pozycji **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="724f2-157">Do not click **Create**.</span></span> <span data-ttu-id="724f2-158">Należy najpierw skonfigurować bazy danych SQL w późniejszym kroku.</span><span class="sxs-lookup"><span data-stu-id="724f2-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="724f2-159">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="724f2-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="724f2-160">Obok pozycji **Plan usługi App Service** kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="724f2-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="724f2-161">W oknie dialogowym **Konfiguruj plan usługi App Service** skonfiguruj nowy plan usługi App Service przy użyciu następujących ustawień:</span><span class="sxs-lookup"><span data-stu-id="724f2-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Tworzenie planu usługi App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="724f2-163">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="724f2-163">Setting</span></span>  | <span data-ttu-id="724f2-164">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="724f2-164">Suggested value</span></span> | <span data-ttu-id="724f2-165">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="724f2-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="724f2-166">**Plan usługi aplikacji**</span><span class="sxs-lookup"><span data-stu-id="724f2-166">**App Service Plan**</span></span>| <span data-ttu-id="724f2-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="724f2-167">myAppServicePlan</span></span> | [<span data-ttu-id="724f2-168">Plany usługi App Service</span><span class="sxs-lookup"><span data-stu-id="724f2-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="724f2-169">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="724f2-169">**Location**</span></span>| <span data-ttu-id="724f2-170">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="724f2-170">West Europe</span></span> | [<span data-ttu-id="724f2-171">Regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="724f2-172">**Rozmiar**</span><span class="sxs-lookup"><span data-stu-id="724f2-172">**Size**</span></span>| <span data-ttu-id="724f2-173">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="724f2-173">Free</span></span> | [<span data-ttu-id="724f2-174">Warstwa cenowa</span><span class="sxs-lookup"><span data-stu-id="724f2-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="724f2-175">Utwórz wystąpienie programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="724f2-175">Create a SQL Server instance</span></span>

<span data-ttu-id="724f2-176">Przed utworzeniem bazy danych, należy [serwera logicznego bazy danych SQL Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="724f2-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="724f2-177">Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="724f2-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="724f2-178">Wybierz **Eksploruj dodatkowych usług Azure**.</span><span class="sxs-lookup"><span data-stu-id="724f2-178">Select **Explore additional Azure services**.</span></span>

![Konfigurowanie nazwy aplikacji sieci Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="724f2-180">W **usług** , kliknij pozycję  **+**  obok opcji **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="724f2-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Na karcie usługi kliknij pozycję + ikona obok bazy danych SQL.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="724f2-182">W **Konfigurowanie bazy danych SQL** okna dialogowego, kliknij przycisk **nowy** obok **programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="724f2-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="724f2-183">Generowany jest unikatową nazwą serwera.</span><span class="sxs-lookup"><span data-stu-id="724f2-183">A unique server name is generated.</span></span> <span data-ttu-id="724f2-184">Ta nazwa jest używana jako część domyślnego adresu URL dla serwera logicznego, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="724f2-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="724f2-185">Musi być unikatowa we wszystkich wystąpieniach serwera logicznego w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="724f2-186">Możesz zmienić nazwę serwera, ale w tym samouczku, należy zachować wartość wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="724f2-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="724f2-187">Dodaj użytkownika administratora i hasło, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="724f2-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="724f2-188">Wymagania dotyczące złożoności hasła, aby zapoznać [zasady haseł](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="724f2-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="724f2-189">Należy pamiętać, ta nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="724f2-189">Remember this username and password.</span></span> <span data-ttu-id="724f2-190">Należy je później zarządzać wystąpienia serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="724f2-190">You need them to manage the logical server instance later.</span></span>

![Utwórz wystąpienie programu SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="724f2-192">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="724f2-192">Create a SQL Database</span></span>

<span data-ttu-id="724f2-193">W **Konfigurowanie bazy danych SQL** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="724f2-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="724f2-194">Zachowaj domyślne wygenerowany **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="724f2-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="724f2-195">W **Nazwa ciągu połączenia**, typ *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="724f2-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="724f2-196">Ta nazwa musi być zgodna parametry połączenia, które odwołują się *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="724f2-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="724f2-197">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="724f2-197">Select **OK**.</span></span>

![Skonfiguruj bazę danych SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="724f2-199">**Tworzenie usługi App Service** okno dialogowe zawiera zasoby po utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="724f2-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="724f2-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="724f2-200">Click **Create**.</span></span> 

![zasoby, które zostały utworzone](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="724f2-202">Po zakończeniu pracy Kreatora tworzenia zasobów platformy Azure, publikowanie aplikacji ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="724f2-203">Domyślnej przeglądarki jest uruchamiana z adresem URL do wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="724f2-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="724f2-204">Dodaj kilka elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="724f2-204">Add a few to-do items.</span></span>

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="724f2-206">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="724f2-206">Congratulations!</span></span> <span data-ttu-id="724f2-207">Aplikacja ASP.NET opartych na danych jest uruchomiona na żywo w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="724f2-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="724f2-208">Dostęp do bazy danych SQL lokalnie</span><span class="sxs-lookup"><span data-stu-id="724f2-208">Access the SQL Database locally</span></span>

<span data-ttu-id="724f2-209">Visual Studio umożliwia Eksplorowanie i nowej bazy danych SQL w prosty sposób zarządzać **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="724f2-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="724f2-210">Utwórz połączenie z bazą danych</span><span class="sxs-lookup"><span data-stu-id="724f2-210">Create a database connection</span></span>

<span data-ttu-id="724f2-211">Z **widoku** menu, wybierz opcję **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="724f2-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="724f2-212">W górnej części **Eksplorator obiektów SQL Server**, kliknij przycisk **dodawania serwera SQL** przycisku.</span><span class="sxs-lookup"><span data-stu-id="724f2-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="724f2-213">Skonfiguruj połączenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="724f2-213">Configure the database connection</span></span>

<span data-ttu-id="724f2-214">W **Connect** okna dialogowego, rozwiń węzeł **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="724f2-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="724f2-215">Swoich wystąpień bazy danych SQL platformy Azure są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="724f2-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="724f2-216">Wybierz `DotNetAppSqlDb` bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="724f2-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="724f2-217">Połączenie utworzony wcześniej jest automatycznie wypełniane u dołu.</span><span class="sxs-lookup"><span data-stu-id="724f2-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="724f2-218">Wpisz hasło administratora bazy danych utworzone wcześniej, a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="724f2-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Skonfiguruj połączenie bazy danych z programu Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="724f2-220">Zezwalaj na połączenia klienckie z komputera</span><span class="sxs-lookup"><span data-stu-id="724f2-220">Allow client connection from your computer</span></span>

<span data-ttu-id="724f2-221">**Utwórz nową regułę zapory** otworzyć okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="724f2-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="724f2-222">Domyślnie wystąpienia bazy danych SQL umożliwia tylko połączeń z usługami Azure, takich jak aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="724f2-223">Aby połączyć się z bazą danych, należy utworzyć regułę zapory w wystąpieniu bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="724f2-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="724f2-224">Reguła zapory zezwala na publiczny adres IP komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="724f2-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="724f2-225">Okno dialogowe jest już wypełniony publiczny adres IP tego komputera.</span><span class="sxs-lookup"><span data-stu-id="724f2-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="724f2-226">Upewnij się, że **Dodaj mój adres IP klienta** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="724f2-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Ustaw zapory dla wystąpienia bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="724f2-228">Po zakończeniu tworzenia ustawień zapory dla swojego wystąpienia bazy danych SQL programu Visual Studio połączenia zostaną wyświetlone w **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="724f2-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="724f2-229">W tym miejscu można wykonywać najbardziej typowe operacje bazy danych, takie jak wykonywania zapytania, Utwórz widoki i procedury składowane i inne.</span><span class="sxs-lookup"><span data-stu-id="724f2-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="724f2-230">Kliknij prawym przyciskiem myszy `Todoes` tabeli i wybierz **danych widoku**.</span><span class="sxs-lookup"><span data-stu-id="724f2-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Eksploruj obiektów bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="724f2-232">Aktualizowanie aplikacji z migracje Code First</span><span class="sxs-lookup"><span data-stu-id="724f2-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="724f2-233">Znanych narzędzi programu Visual Studio umożliwia aktualizacji aplikacji sieci web i bazy danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="724f2-234">W tym kroku użyjesz migracje Code First w Entity Framework zmiany do schematu bazy danych, a następnie opublikuj ją do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="724f2-235">Aby uzyskać więcej informacji o używaniu migracje Code First Framework jednostki, zobacz [wprowadzenie do programu Entity Framework 6 Code First przy użyciu MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="724f2-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="724f2-236">Aktualizacja modelu danych</span><span class="sxs-lookup"><span data-stu-id="724f2-236">Update your data model</span></span>

<span data-ttu-id="724f2-237">Otwórz _Models\Todo.cs_ w edytorze kodu.</span><span class="sxs-lookup"><span data-stu-id="724f2-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="724f2-238">Dodaj następujące właściwości do `ToDo` klasy:</span><span class="sxs-lookup"><span data-stu-id="724f2-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="724f2-239">Uruchom lokalnie migracje Code First</span><span class="sxs-lookup"><span data-stu-id="724f2-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="724f2-240">Uruchomienie kilku poleceń, aby aktualizacje z lokalną bazą danych.</span><span class="sxs-lookup"><span data-stu-id="724f2-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="724f2-241">Z **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="724f2-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="724f2-242">W oknie Konsola Menedżera pakietów należy włączyć migracje Code First:</span><span class="sxs-lookup"><span data-stu-id="724f2-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="724f2-243">Dodaj migracji:</span><span class="sxs-lookup"><span data-stu-id="724f2-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="724f2-244">Aktualizacja lokalnej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="724f2-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="724f2-245">Typ `Ctrl+F5` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="724f2-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="724f2-246">Testowanie edycji, uzyskać szczegółowe informacje i utworzyć łącza.</span><span class="sxs-lookup"><span data-stu-id="724f2-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="724f2-247">Jeśli bez błędów ładowania aplikacji powiodła się migracje Code First.</span><span class="sxs-lookup"><span data-stu-id="724f2-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="724f2-248">Jednak ze strony nadal jest taki sam ponieważ logiki aplikacji nie korzysta z tej nowej właściwości jeszcze.</span><span class="sxs-lookup"><span data-stu-id="724f2-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="724f2-249">Użyj nowej właściwości</span><span class="sxs-lookup"><span data-stu-id="724f2-249">Use the new property</span></span>

<span data-ttu-id="724f2-250">Niektóre zmiany w kodzie do użycia `Done` właściwości.</span><span class="sxs-lookup"><span data-stu-id="724f2-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="724f2-251">Dla uproszczenia w tym samouczku, tylko zamierzasz zmienić `Index` i `Create` widoków, aby wyświetlić właściwości działania.</span><span class="sxs-lookup"><span data-stu-id="724f2-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="724f2-252">Otwórz _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="724f2-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="724f2-253">Znajdź `Create()` — metoda i Dodaj `Done` do listy właściwości w `Bind` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="724f2-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="724f2-254">Gdy wszystko będzie gotowe, Twoje `Create()` podpis metody wygląda podobnie do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="724f2-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="724f2-255">Otwórz _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="724f2-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="724f2-256">W kodzie Razor, powinna zostać wyświetlona `<div class="form-group">` element, który używa `model.Description`, a następnie inne `<div class="form-group">` element, który używa `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="724f2-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="724f2-257">Bezpośrednio po tych dwóch elementów, dodać kolejne `<div class="form-group">` element, który używa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="724f2-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="724f2-258">Otwórz _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="724f2-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="724f2-259">Poszukaj pustych `<th></th>` elementu.</span><span class="sxs-lookup"><span data-stu-id="724f2-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="724f2-260">Powyżej tego elementu Dodaj następujący kod Razor:</span><span class="sxs-lookup"><span data-stu-id="724f2-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="724f2-261">Znajdź `<td>` element, który zawiera `Html.ActionLink()` metody pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="724f2-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="724f2-262">Powyżej tego elementu Dodaj następujący kod Razor:</span><span class="sxs-lookup"><span data-stu-id="724f2-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="724f2-263">To już wszystko, czego potrzebujesz, aby zobaczyć zmiany w `Index` i `Create` widoków.</span><span class="sxs-lookup"><span data-stu-id="724f2-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="724f2-264">Typ `Ctrl+F5` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="724f2-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="724f2-265">Można teraz dodać element do wykonania i sprawdzić **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="724f2-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="724f2-266">Następnie go powinny być widoczne w strony głównej jako element ukończone.</span><span class="sxs-lookup"><span data-stu-id="724f2-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="724f2-267">Należy pamiętać, że `Edit` nie wyświetla widok `Done` pól, ponieważ nie zmieniły `Edit` widoku.</span><span class="sxs-lookup"><span data-stu-id="724f2-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="724f2-268">Włącz migracje Code First na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="724f2-269">Teraz, gdy kod działa, łącznie z migracji bazy danych zmian przed opublikowaniem aplikacji sieci web platformy Azure i zbyt aktualizacji bazy danych SQL z migracje Code First.</span><span class="sxs-lookup"><span data-stu-id="724f2-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="724f2-270">Tak jak wcześniej, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="724f2-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="724f2-271">Kliknij przycisk **ustawienia** aby otworzyć Kreatora publikowania.</span><span class="sxs-lookup"><span data-stu-id="724f2-271">Click **Settings** to open the publish wizard.</span></span>

![Otwórz ustawienia publikowania](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="724f2-273">W kreatorze kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="724f2-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="724f2-274">Upewnij się, że parametry połączenia bazy danych SQL jest wypełniana w **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="724f2-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="724f2-275">Musisz wybrać **myToDoAppDb** bazy danych z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="724f2-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="724f2-276">Wybierz **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="724f2-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Włącz migracje Code First w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="724f2-278">Opublikuj zmiany</span><span class="sxs-lookup"><span data-stu-id="724f2-278">Publish your changes</span></span>

<span data-ttu-id="724f2-279">Skoro migracje Code First jest włączone w aplikacji sieci web platformy Azure, Opublikuj zmiany kodu.</span><span class="sxs-lookup"><span data-stu-id="724f2-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="724f2-280">Na stronie publikowania kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="724f2-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="724f2-281">Spróbuj ponownie dodać elementów do wykonania i wybierz **gotowe**, i powinny być widoczne w strony głównej jako element ukończone.</span><span class="sxs-lookup"><span data-stu-id="724f2-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplikacja sieci web platformy Azure po zakończeniu migracji pierwszy kodu](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="724f2-283">Nadal wyświetlane są wszystkie istniejące elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="724f2-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="724f2-284">Istniejące dane w bazie danych SQL ponownie opublikować aplikację ASP.NET nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="724f2-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="724f2-285">Ponadto migracje Code First tylko zmiany schematu danych oraz pozostawia niezmienione istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="724f2-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="724f2-286">Strumieniowe przesyłanie dzienników aplikacji</span><span class="sxs-lookup"><span data-stu-id="724f2-286">Stream application logs</span></span>

<span data-ttu-id="724f2-287">Wiadomości śledzenia można strumienia bezpośrednio z aplikacji sieci web platformy Azure dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724f2-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="724f2-288">Otwórz _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="724f2-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="724f2-289">Każda akcja rozpoczyna się od `Trace.WriteLine()` metody.</span><span class="sxs-lookup"><span data-stu-id="724f2-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="724f2-290">Ten kod jest dodawany do pokazano, jak dodawać komunikaty śledzenia do aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="724f2-291">W Eksploratorze serwera Otwórz</span><span class="sxs-lookup"><span data-stu-id="724f2-291">Open Server Explorer</span></span>

<span data-ttu-id="724f2-292">Z **widoku** menu, wybierz opcję **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="724f2-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="724f2-293">Można skonfigurować rejestrowanie dla aplikacji sieci web platformy Azure na **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="724f2-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="724f2-294">Przesyłania strumieniowego dzienników</span><span class="sxs-lookup"><span data-stu-id="724f2-294">Enable log streaming</span></span>

<span data-ttu-id="724f2-295">W **Eksploratora serwera**, rozwiń węzeł **Azure** > **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="724f2-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="724f2-296">Rozwiń węzeł **myResourceGroup** grupy zasobów utworzone podczas tworzenia aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="724f2-297">Kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **Wyświetl dzienniki przesyłania strumieniowego**.</span><span class="sxs-lookup"><span data-stu-id="724f2-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Przesyłania strumieniowego dzienników](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="724f2-299">Dzienniki są teraz przesyłane strumieniowo do **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="724f2-299">The logs are now streamed into the **Output** window.</span></span> 

![Dziennik przesyłania strumieniowego w oknie danych wyjściowych](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="724f2-301">Jednak nie widzisz żadnych komunikatów śledzenia jeszcze.</span><span class="sxs-lookup"><span data-stu-id="724f2-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="724f2-302">To jest ponieważ po wybraniu **Wyświetl dzienniki przesyłania strumieniowego**, aplikacji sieci web platformy Azure ustawia poziom śledzenia `Error`, która rejestruje tylko zdarzenia błędów (z `Trace.TraceError()` metody).</span><span class="sxs-lookup"><span data-stu-id="724f2-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="724f2-303">Zmień poziomy śledzenia</span><span class="sxs-lookup"><span data-stu-id="724f2-303">Change trace levels</span></span>

<span data-ttu-id="724f2-304">Aby zmienić poziom śledzenia do wyjściowego inne komunikaty śledzenia, przejdź wstecz do **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="724f2-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="724f2-305">Ponownie kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="724f2-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="724f2-306">W **rejestrowania aplikacji (w systemie plików)** listy rozwijanej wybierz **pełne**.</span><span class="sxs-lookup"><span data-stu-id="724f2-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="724f2-307">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="724f2-307">Click **Save**.</span></span>

![Poziom śledzenia zmian Verbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="724f2-309">Możesz eksperymentować z poziomów śledzenia różnych, aby zobaczyć, jakie komunikaty są wyświetlane dla każdego poziomu.</span><span class="sxs-lookup"><span data-stu-id="724f2-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="724f2-310">Na przykład **informacji** poziom obejmuje wszystkie dzienniki utworzone przez `Trace.TraceInformation()`, `Trace.TraceWarning()`, i `Trace.TraceError()`, ale nie Dzienniki tworzone przez `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="724f2-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="724f2-311">W przeglądarce spróbuj kliknięcie wokół aplikacji listy zadań do wykonania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="724f2-312">Wiadomości śledzenia są teraz przesyłane strumieniowo do **dane wyjściowe** okna w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724f2-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="724f2-313">Zatrzymaj dzienników przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="724f2-313">Stop log streaming</span></span>

<span data-ttu-id="724f2-314">Aby zatrzymać usługę przesyłania strumieniowego dzienników, kliknij przycisk **zatrzymać monitorowanie** przycisk **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="724f2-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Zatrzymaj dzienników przesyłania strumieniowego](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="724f2-316">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-316">Manage your Azure web app</span></span>

<span data-ttu-id="724f2-317">Przejdź do [portalu Azure](https://portal.azure.com) zobaczyć aplikacji sieci web został utworzony.</span><span class="sxs-lookup"><span data-stu-id="724f2-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="724f2-318">W lewym menu kliknij pozycję **App Service**, a następnie kliknij nazwę swojej aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="724f2-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="724f2-320">Jest strony aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="724f2-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="724f2-321">Domyślnie przedstawia portalu **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="724f2-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="724f2-322">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="724f2-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="724f2-323">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="724f2-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="724f2-324">W lewej części strony kartach stron innej konfiguracji może być otwarty.</span><span class="sxs-lookup"><span data-stu-id="724f2-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="724f2-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="724f2-326">Next steps</span></span>

<span data-ttu-id="724f2-327">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="724f2-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="724f2-328">Tworzenie bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="724f2-329">Połącz aplikację ASP.NET do bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="724f2-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="724f2-330">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="724f2-331">Aktualizacja modelu danych i ponownie wdrożyć aplikację</span><span class="sxs-lookup"><span data-stu-id="724f2-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="724f2-332">Strumieniowe przesyłanie dzienników z platformy Azure na terminalu</span><span class="sxs-lookup"><span data-stu-id="724f2-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="724f2-333">Zarządzanie aplikacją w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="724f2-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="724f2-334">Przejdź do następnego samouczkiem, aby dowiedzieć się, jak zamapować niestandardową nazwę DNS w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="724f2-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="724f2-335">Map an existing custom DNS name to Azure Web Apps (Mapowanie istniejącej niestandardowej nazwy DNS na aplikacje internetowe platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="724f2-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
