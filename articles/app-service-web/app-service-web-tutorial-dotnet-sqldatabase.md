---
title: "aaaBuild aplikacji ASP.NET na platformie Azure w usłudze SQL Database | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooget ASP.NET aplikacja działa na platformie Azure z tooa połączenia bazy danych SQL."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="053d8-103">Tworzenie aplikacji platformy ASP.NET na platformie Azure z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="053d8-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="053d8-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="053d8-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="053d8-105">W tym samouczku przedstawiono sposób toodeploy platformy ASP.NET opartych na danych aplikacji na platformie Azure w sieci web i połącz go za[bazy danych SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="053d8-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="053d8-106">Po zakończeniu, masz aplikację ASP.NET działającą w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) i połączone tooSQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="053d8-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="053d8-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="053d8-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="053d8-109">Tworzenie bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="053d8-110">Połącz tooSQL aplikacji ASP.NET bazy danych</span><span class="sxs-lookup"><span data-stu-id="053d8-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="053d8-111">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="053d8-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="053d8-112">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="053d8-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="053d8-113">Strumieniowe przesyłanie dzienników z Azure tooyour terminali</span><span class="sxs-lookup"><span data-stu-id="053d8-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="053d8-114">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="053d8-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="053d8-115">Prerequisites</span></span>

<span data-ttu-id="053d8-116">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="053d8-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="053d8-117">Zainstaluj [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello następujące obciążenia:</span><span class="sxs-lookup"><span data-stu-id="053d8-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="053d8-118">**Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych**</span><span class="sxs-lookup"><span data-stu-id="053d8-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="053d8-119">**Tworzenie aplikacji na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="053d8-119">**Azure development**</span></span>

  ![Tworzenie aplikacji na platformie ASP.NET i tworzenie aplikacji internetowych oraz tworzenie aplikacji na platformie Azure (w ramach Internetu i chmury)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="053d8-121">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="053d8-121">Download hello sample</span></span>

<span data-ttu-id="053d8-122">[Pobierz hello przykładowy projekt](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="053d8-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="053d8-123">Wyodrębnij (Rozpakuj) hello *dotnet-sqldb — samouczek master.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="053d8-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="053d8-124">Witaj przykładowy projekt zawiera basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Tworzenie odczytu aktualizowania i usuwania) aplikacji w usłudze [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="053d8-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="053d8-125">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="053d8-125">Run hello app</span></span>

<span data-ttu-id="053d8-126">Otwórz hello *dotnet-sqldb — samouczek — wzorzec/DotNetAppSqlDb.sln* pliku w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="053d8-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="053d8-127">Typ `Ctrl+F5` aplikacji hello toorun bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="053d8-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="053d8-128">Aplikacja Hello jest wyświetlana w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="053d8-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="053d8-129">Wybierz hello **Utwórz nowy** link i Utwórz kilka *zadań do wykonania* elementów.</span><span class="sxs-lookup"><span data-stu-id="053d8-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Okno dialogowe Nowy projekt ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="053d8-131">Test hello **Edytuj**, **szczegóły**, i **usunąć** łącza.</span><span class="sxs-lookup"><span data-stu-id="053d8-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="053d8-132">Aplikacja Hello używa tooconnect kontekst bazy danych z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="053d8-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="053d8-133">W tym przykładzie hello kontekst bazy danych używa parametrów połączenia o nazwie `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="053d8-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="053d8-134">Parametry połączenia Hello jest ustawiany w hello *Web.config* plików i hello zawartymi w *Models/MyDatabaseContext.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="053d8-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="053d8-135">Nazwa ciągu połączenia Hello jest używany w dalszej części hello samouczek tooconnect hello Azure web app tooan bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="053d8-136">Publikowanie tooAzure z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="053d8-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="053d8-137">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy użytkownika **DotNetAppSqlDb** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="053d8-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publikowanie z Eksploratora rozwiązań](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="053d8-139">Upewnij się, że jest zaznaczona usługa **Microsoft Azure App Service**, a następnie kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="053d8-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publikowanie ze strony przeglądu projektu](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="053d8-141">Publikowanie otwiera hello **Tworzenie usługi App Service** okna dialogowego, które ułatwia tworzenie wszystkich hello zasobów platformy Azure, należy toorun aplikacji sieci web platformy ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="053d8-142">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="053d8-142">Sign in tooAzure</span></span>

<span data-ttu-id="053d8-143">W hello **Tworzenie usługi App Service** okna dialogowego, kliknij przycisk **Dodaj konto**, a następnie zaloguj tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="053d8-144">Jeśli zalogowano się już do konta Microsoft, upewnij się, że to konto zawiera Twoją subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="053d8-145">Jeśli hello zalogowanego konta Microsoft nie ma subskrypcji platformy Azure, kliknij go, tooadd hello odpowiedniego konta.</span><span class="sxs-lookup"><span data-stu-id="053d8-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Zaloguj się tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="053d8-147">Po zalogowaniu, wszystko jest gotowe toocreate hello wszystkie zasoby, które są potrzebne dla aplikacji sieci web platformy Azure w tym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="053d8-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="053d8-148">Konfigurowanie nazwy aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="053d8-148">Configure hello web app name</span></span>

<span data-ttu-id="053d8-149">Zachowaj nazwę aplikacji sieci web hello wygenerowany lub zmień ją tooanother unikatową nazwę (prawidłowe znaki to `a-z`, `0-9`, i `-`).</span><span class="sxs-lookup"><span data-stu-id="053d8-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="053d8-150">Nazwa aplikacji sieci web Hello jest używany jako część hello domyślny adres URL aplikacji (`<app_name>.azurewebsites.net`, gdzie `<app_name>` oznacza nazwę aplikacji sieci web).</span><span class="sxs-lookup"><span data-stu-id="053d8-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="053d8-151">Nazwa aplikacji sieci web Hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Tworzenie aplikacji usługi z okna dialogowego](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="053d8-153">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="053d8-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="053d8-154">Następny zbyt**grupy zasobów**, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="053d8-154">Next too**Resource Group**, click **New**.</span></span>

![Następny tooResource grupy, kliknij przycisk Nowy.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="053d8-156">Nazwa grupy zasobów hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="053d8-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="053d8-157">Nie klikaj pozycji **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="053d8-157">Do not click **Create**.</span></span> <span data-ttu-id="053d8-158">Należy najpierw tooset bazy danych SQL w późniejszym kroku.</span><span class="sxs-lookup"><span data-stu-id="053d8-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="053d8-159">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="053d8-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="053d8-160">Następny zbyt**planu usługi App Service**, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="053d8-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="053d8-161">W hello **Konfigurowanie planu usługi aplikacji** okna dialogowego, skonfigurować nowy plan usługi aplikacji hello hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="053d8-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Tworzenie planu usługi App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="053d8-163">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="053d8-163">Setting</span></span>  | <span data-ttu-id="053d8-164">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="053d8-164">Suggested value</span></span> | <span data-ttu-id="053d8-165">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="053d8-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="053d8-166">**Plan usługi aplikacji**</span><span class="sxs-lookup"><span data-stu-id="053d8-166">**App Service Plan**</span></span>| <span data-ttu-id="053d8-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="053d8-167">myAppServicePlan</span></span> | [<span data-ttu-id="053d8-168">Plany usługi App Service</span><span class="sxs-lookup"><span data-stu-id="053d8-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="053d8-169">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="053d8-169">**Location**</span></span>| <span data-ttu-id="053d8-170">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="053d8-170">West Europe</span></span> | [<span data-ttu-id="053d8-171">Regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="053d8-172">**Rozmiar**</span><span class="sxs-lookup"><span data-stu-id="053d8-172">**Size**</span></span>| <span data-ttu-id="053d8-173">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="053d8-173">Free</span></span> | [<span data-ttu-id="053d8-174">Warstwa cenowa</span><span class="sxs-lookup"><span data-stu-id="053d8-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="053d8-175">Utwórz wystąpienie programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="053d8-175">Create a SQL Server instance</span></span>

<span data-ttu-id="053d8-176">Przed utworzeniem bazy danych, należy [serwera logicznego bazy danych SQL Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="053d8-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="053d8-177">Serwer logiczny zawiera grupę baz danych zarządzanych jako grupa.</span><span class="sxs-lookup"><span data-stu-id="053d8-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="053d8-178">Wybierz **Eksploruj dodatkowych usług Azure**.</span><span class="sxs-lookup"><span data-stu-id="053d8-178">Select **Explore additional Azure services**.</span></span>

![Konfigurowanie nazwy aplikacji sieci Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="053d8-180">W hello **usług** , kliknij pozycję hello  **+**  ikona dalej zbyt**bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="053d8-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Na karcie usług hello, kliknij przycisk Witaj + ikonę dalej tooSQL bazy danych.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="053d8-182">W hello **Konfigurowanie bazy danych SQL** okna dialogowego, kliknij przycisk **nowy** dalej zbyt**programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="053d8-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="053d8-183">Generowany jest unikatową nazwą serwera.</span><span class="sxs-lookup"><span data-stu-id="053d8-183">A unique server name is generated.</span></span> <span data-ttu-id="053d8-184">Ta nazwa jest używana jako część hello domyślny adres URL dla serwera logicznego, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="053d8-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="053d8-185">Musi być unikatowa we wszystkich wystąpieniach serwera logicznego w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="053d8-186">Możesz zmienić nazwę serwera hello, ale w tym samouczku, należy zachować wartość hello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="053d8-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="053d8-187">Dodaj użytkownika administratora i hasło, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="053d8-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="053d8-188">Wymagania dotyczące złożoności hasła, aby zapoznać [zasady haseł](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="053d8-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="053d8-189">Należy pamiętać, ta nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="053d8-189">Remember this username and password.</span></span> <span data-ttu-id="053d8-190">Należy je serwera logicznego toomanage hello później wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="053d8-190">You need them toomanage hello logical server instance later.</span></span>

![Utwórz wystąpienie programu SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="053d8-192">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="053d8-192">Create a SQL Database</span></span>

<span data-ttu-id="053d8-193">W hello **Konfigurowanie bazy danych SQL** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="053d8-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="053d8-194">Zachowaj domyślne hello wygenerowany **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="053d8-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="053d8-195">W **Nazwa ciągu połączenia**, typ *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="053d8-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="053d8-196">Ta nazwa musi być zgodna hello parametry połączenia, do którego odwołuje się w *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="053d8-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="053d8-197">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="053d8-197">Select **OK**.</span></span>

![Skonfiguruj bazę danych SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="053d8-199">Witaj **Tworzenie usługi App Service** okna dialogowego pokazuje hello zasoby po utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="053d8-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="053d8-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="053d8-200">Click **Create**.</span></span> 

![Witaj zasoby, które zostały utworzone](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="053d8-202">Po hello zakończeniu pracy Kreatora tworzenia hello Azure zasobów publikuje tooAzure aplikacji programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="053d8-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="053d8-203">Domyślnej przeglądarki jest uruchomiona z hello adresu URL toohello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="053d8-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="053d8-204">Dodaj kilka elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="053d8-204">Add a few to-do items.</span></span>

![Opublikowana aplikacja ASP.NET w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="053d8-206">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="053d8-206">Congratulations!</span></span> <span data-ttu-id="053d8-207">Aplikacja ASP.NET opartych na danych jest uruchomiona na żywo w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="053d8-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="053d8-208">Dostęp lokalnie hello bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="053d8-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="053d8-209">Program Visual Studio umożliwia Eksplorowanie i zarządzanie nimi z nowej bazy danych SQL, łatwo w hello **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="053d8-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="053d8-210">Utwórz połączenie z bazą danych</span><span class="sxs-lookup"><span data-stu-id="053d8-210">Create a database connection</span></span>

<span data-ttu-id="053d8-211">Z hello **widoku** menu, wybierz opcję **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="053d8-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="053d8-212">U góry hello **Eksplorator obiektów SQL Server**, kliknij przycisk hello **dodawania serwera SQL** przycisku.</span><span class="sxs-lookup"><span data-stu-id="053d8-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="053d8-213">Skonfiguruj połączenie bazy danych hello</span><span class="sxs-lookup"><span data-stu-id="053d8-213">Configure hello database connection</span></span>

<span data-ttu-id="053d8-214">W hello **Connect** okna dialogowego, rozwiń węzeł hello **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="053d8-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="053d8-215">Swoich wystąpień bazy danych SQL platformy Azure są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="053d8-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="053d8-216">Wybierz hello `DotNetAppSqlDb` bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="053d8-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="053d8-217">połączenie Hello, utworzony wcześniej jest automatycznie wypełniane u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="053d8-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="053d8-218">Wpisz hasło administratora bazy danych hello utworzone wcześniej, a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="053d8-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Skonfiguruj połączenie bazy danych z programu Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="053d8-220">Zezwalaj na połączenia klienckie z komputera</span><span class="sxs-lookup"><span data-stu-id="053d8-220">Allow client connection from your computer</span></span>

<span data-ttu-id="053d8-221">Witaj **Utwórz nową regułę zapory** otworzyć okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="053d8-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="053d8-222">Domyślnie wystąpienia bazy danych SQL umożliwia tylko połączeń z usługami Azure, takich jak aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="053d8-223">tooconnect tooyour bazy danych, należy utworzyć regułę zapory w hello wystąpienie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="053d8-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="053d8-224">Witaj, reguła zapory zezwala na powitania publicznego adresu IP komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="053d8-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="053d8-225">okno dialogowe Hello jest już wypełniony publiczny adres IP komputera.</span><span class="sxs-lookup"><span data-stu-id="053d8-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="053d8-226">Upewnij się, że **Dodaj mój adres IP klienta** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="053d8-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Ustaw zapory dla wystąpienia bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="053d8-228">Gdy program Visual Studio zakończy tworzenie hello ustawień zapory dla swojego wystąpienia bazy danych SQL, połączenia zostaną wyświetlone w **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="053d8-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="053d8-229">W tym miejscu można wykonywać hello najczęściej bazy danych operacji, takich jak wykonywania zapytania, Utwórz widoki i procedury składowane i inne.</span><span class="sxs-lookup"><span data-stu-id="053d8-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="053d8-230">Kliknij prawym przyciskiem myszy na powitania `Todoes` tabeli i wybierz **danych widoku**.</span><span class="sxs-lookup"><span data-stu-id="053d8-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Eksploruj obiektów bazy danych SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="053d8-232">Aktualizowanie aplikacji z migracje Code First</span><span class="sxs-lookup"><span data-stu-id="053d8-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="053d8-233">Można użyć znanych narzędzi hello w Visual Studio tooupdate aplikacji sieci web i bazy danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="053d8-234">W tym kroku migracje Code First jest używany w toomake Entity Framework zmiany schematu bazy danych tooyour i opublikować go tooAzure.</span><span class="sxs-lookup"><span data-stu-id="053d8-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="053d8-235">Aby uzyskać więcej informacji o używaniu migracje Code First Framework jednostki, zobacz [wprowadzenie do programu Entity Framework 6 Code First przy użyciu MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="053d8-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="053d8-236">Aktualizacja modelu danych</span><span class="sxs-lookup"><span data-stu-id="053d8-236">Update your data model</span></span>

<span data-ttu-id="053d8-237">Otwórz _Models\Todo.cs_ hello edytora kodu.</span><span class="sxs-lookup"><span data-stu-id="053d8-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="053d8-238">Dodaj następujące właściwości toohello hello `ToDo` klasy:</span><span class="sxs-lookup"><span data-stu-id="053d8-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="053d8-239">Uruchom lokalnie migracje Code First</span><span class="sxs-lookup"><span data-stu-id="053d8-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="053d8-240">Uruchom kilka poleceń toomake aktualizacje tooyour lokalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="053d8-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="053d8-241">Z hello **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="053d8-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="053d8-242">W oknie konsoli Menedżera pakietów hello należy włączyć migracje Code First:</span><span class="sxs-lookup"><span data-stu-id="053d8-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="053d8-243">Dodaj migracji:</span><span class="sxs-lookup"><span data-stu-id="053d8-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="053d8-244">Aktualizacja hello lokalnej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="053d8-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="053d8-245">Typ `Ctrl+F5` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="053d8-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="053d8-246">Test hello Edytuj szczegóły i utworzyć łącza.</span><span class="sxs-lookup"><span data-stu-id="053d8-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="053d8-247">Jeśli aplikacja hello ładuje bez błędów, następnie migracje Code First zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="053d8-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="053d8-248">Jednak Twój nadal wygląd strony hello sam ponieważ logiki aplikacji nie korzysta z tej nowej właściwości jeszcze.</span><span class="sxs-lookup"><span data-stu-id="053d8-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="053d8-249">Użyj hello nowej właściwości.</span><span class="sxs-lookup"><span data-stu-id="053d8-249">Use hello new property</span></span>

<span data-ttu-id="053d8-250">Niektóre zmiany w Twojej hello toouse kodu `Done` właściwości.</span><span class="sxs-lookup"><span data-stu-id="053d8-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="053d8-251">Dla uproszczenia w tym samouczku, tylko będzie toochange hello `Index` i `Create` widoków toosee hello właściwości działania.</span><span class="sxs-lookup"><span data-stu-id="053d8-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="053d8-252">Otwórz _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="053d8-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="053d8-253">Znajdź hello `Create()` — metoda i Dodaj `Done` toohello listę właściwości w hello `Bind` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="053d8-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="053d8-254">Gdy wszystko będzie gotowe, Twoje `Create()` podpis metody wygląda hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="053d8-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="053d8-255">Otwórz _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="053d8-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="053d8-256">W kodzie Razor hello, powinna zostać wyświetlona `<div class="form-group">` element, który używa `model.Description`, a następnie inne `<div class="form-group">` element, który używa `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="053d8-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="053d8-257">Bezpośrednio po tych dwóch elementów, dodać kolejne `<div class="form-group">` element, który używa `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="053d8-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="053d8-258">Otwórz _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="053d8-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="053d8-259">Wyszukaj hello pusty `<th></th>` elementu.</span><span class="sxs-lookup"><span data-stu-id="053d8-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="053d8-260">Powyżej tego elementu Dodaj następującego kodu Razor hello:</span><span class="sxs-lookup"><span data-stu-id="053d8-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="053d8-261">Znajdź hello `<td>` element, który zawiera hello `Html.ActionLink()` metody pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="053d8-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="053d8-262">Powyżej tego elementu Dodaj następującego kodu Razor hello:</span><span class="sxs-lookup"><span data-stu-id="053d8-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="053d8-263">To już wszystko, czego potrzebujesz toosee zmiany hello hello `Index` i `Create` widoków.</span><span class="sxs-lookup"><span data-stu-id="053d8-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="053d8-264">Typ `Ctrl+F5` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="053d8-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="053d8-265">Można teraz dodać element do wykonania i sprawdzić **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="053d8-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="053d8-266">Następnie go powinny być widoczne w strony głównej jako element ukończone.</span><span class="sxs-lookup"><span data-stu-id="053d8-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="053d8-267">Należy pamiętać, że hello `Edit` widoku nie wyświetla hello `Done` pól, ponieważ nie zmieniły hello `Edit` widoku.</span><span class="sxs-lookup"><span data-stu-id="053d8-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="053d8-268">Włącz migracje Code First na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="053d8-269">Teraz, gdy kod działa, łącznie z migracji bazy danych zmian opublikowania go w aplikacji sieci web platformy Azure tooyour i zbyt aktualizacji bazy danych SQL z migracje Code First.</span><span class="sxs-lookup"><span data-stu-id="053d8-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="053d8-270">Tak jak wcześniej, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="053d8-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="053d8-271">Kliknij przycisk **ustawienia** tooopen hello Kreator publikowania.</span><span class="sxs-lookup"><span data-stu-id="053d8-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Otwórz ustawienia publikowania](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="053d8-273">W Kreatorze powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="053d8-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="053d8-274">Sprawdź, czy te parametry połączenia hello w bazie danych SQL została wpisana **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="053d8-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="053d8-275">Może być konieczne tooselect hello **myToDoAppDb** bazy danych z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="053d8-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="053d8-276">Wybierz **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="053d8-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Włącz migracje Code First w aplikacji sieci web platformy Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="053d8-278">Opublikuj zmiany</span><span class="sxs-lookup"><span data-stu-id="053d8-278">Publish your changes</span></span>

<span data-ttu-id="053d8-279">Skoro migracje Code First jest włączone w aplikacji sieci web platformy Azure, Opublikuj zmiany kodu.</span><span class="sxs-lookup"><span data-stu-id="053d8-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="053d8-280">W hello strona publikowania, kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="053d8-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="053d8-281">Spróbuj ponownie dodać elementów do wykonania i wybierz **gotowe**, i powinny być widoczne w strony głównej jako element ukończone.</span><span class="sxs-lookup"><span data-stu-id="053d8-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplikacja sieci web platformy Azure po zakończeniu migracji pierwszy kodu](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="053d8-283">Nadal wyświetlane są wszystkie istniejące elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="053d8-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="053d8-284">Istniejące dane w bazie danych SQL ponownie opublikować aplikację ASP.NET nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="053d8-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="053d8-285">Ponadto migracje Code First zmienia tylko schemat danych hello i pozostawienie bez zmian do istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="053d8-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="053d8-286">Strumieniowe przesyłanie dzienników aplikacji</span><span class="sxs-lookup"><span data-stu-id="053d8-286">Stream application logs</span></span>

<span data-ttu-id="053d8-287">Bezpośrednio z programu tooVisual aplikacji sieci web platformy Azure Studio można przesłać strumieniowo śledzenia wiadomości.</span><span class="sxs-lookup"><span data-stu-id="053d8-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="053d8-288">Otwórz _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="053d8-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="053d8-289">Każda akcja rozpoczyna się od `Trace.WriteLine()` metody.</span><span class="sxs-lookup"><span data-stu-id="053d8-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="053d8-290">Ten kod jest dodawany tooshow należy jak tooadd śledzenia komunikatów tooyour aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="053d8-291">W Eksploratorze serwera Otwórz</span><span class="sxs-lookup"><span data-stu-id="053d8-291">Open Server Explorer</span></span>

<span data-ttu-id="053d8-292">Z hello **widoku** menu, wybierz opcję **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="053d8-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="053d8-293">Można skonfigurować rejestrowanie dla aplikacji sieci web platformy Azure na **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="053d8-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="053d8-294">Przesyłania strumieniowego dzienników</span><span class="sxs-lookup"><span data-stu-id="053d8-294">Enable log streaming</span></span>

<span data-ttu-id="053d8-295">W **Eksploratora serwera**, rozwiń węzeł **Azure** > **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="053d8-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="053d8-296">Rozwiń węzeł hello **myResourceGroup** grupy zasobów utworzone podczas tworzenia aplikacji sieci web platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="053d8-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="053d8-297">Kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **Wyświetl dzienniki przesyłania strumieniowego**.</span><span class="sxs-lookup"><span data-stu-id="053d8-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Przesyłania strumieniowego dzienników](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="053d8-299">Witaj dzienniki są teraz przesyłane strumieniowo do hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="053d8-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Dziennik przesyłania strumieniowego w oknie danych wyjściowych](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="053d8-301">Jednak nie widzisz tych wiadomości powitania śledzenia jeszcze.</span><span class="sxs-lookup"><span data-stu-id="053d8-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="053d8-302">To jest ponieważ najpierw wybranie **Wyświetl dzienniki przesyłania strumieniowego**, aplikacji sieci web platformy Azure ustawia poziom śledzenia hello zbyt`Error`, która rejestruje tylko zdarzenia błędów (z hello `Trace.TraceError()` — metoda).</span><span class="sxs-lookup"><span data-stu-id="053d8-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="053d8-303">Zmień poziomy śledzenia</span><span class="sxs-lookup"><span data-stu-id="053d8-303">Change trace levels</span></span>

<span data-ttu-id="053d8-304">toochange hello śledzenia poziomy toooutput inne komunikaty śledzenia, przejdź wstecz zbyt**Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="053d8-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="053d8-305">Ponownie kliknij prawym przyciskiem myszy aplikację sieci web platformy Azure i wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="053d8-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="053d8-306">W hello **rejestrowania aplikacji (w systemie plików)** listy rozwijanej wybierz **pełne**.</span><span class="sxs-lookup"><span data-stu-id="053d8-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="053d8-307">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="053d8-307">Click **Save**.</span></span>

![TooVerbose poziomu śledzenia zmian](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="053d8-309">Możesz eksperymentować z toosee poziomy śledzenia różne rodzaje komunikaty są wyświetlane dla każdego poziomu.</span><span class="sxs-lookup"><span data-stu-id="053d8-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="053d8-310">Na przykład Witaj **informacji** poziom obejmuje wszystkie dzienniki utworzone przez `Trace.TraceInformation()`, `Trace.TraceWarning()`, i `Trace.TraceError()`, ale nie Dzienniki tworzone przez `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="053d8-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="053d8-311">W przeglądarce spróbuj kliknięcie wokół hello aplikację listy zadań do wykonania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="053d8-312">wiadomości powitania śledzenia są teraz przesyłane strumieniowo toohello **dane wyjściowe** okna w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="053d8-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="053d8-313">Zatrzymaj dzienników przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="053d8-313">Stop log streaming</span></span>

<span data-ttu-id="053d8-314">toostop hello przesyłania strumieniowego dzienników usługi, kliknij przycisk hello **zatrzymać monitorowanie** przycisku na powitania **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="053d8-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Zatrzymaj dzienników przesyłania strumieniowego](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="053d8-316">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-316">Manage your Azure web app</span></span>

<span data-ttu-id="053d8-317">Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony.</span><span class="sxs-lookup"><span data-stu-id="053d8-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="053d8-318">W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="053d8-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="053d8-320">Jest strony aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="053d8-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="053d8-321">Domyślnie hello portal pokazuje hello **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="053d8-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="053d8-322">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="053d8-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="053d8-323">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="053d8-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="053d8-324">Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="053d8-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="053d8-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="053d8-326">Next steps</span></span>

<span data-ttu-id="053d8-327">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="053d8-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="053d8-328">Tworzenie bazy danych SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="053d8-329">Połącz tooSQL aplikacji ASP.NET bazy danych</span><span class="sxs-lookup"><span data-stu-id="053d8-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="053d8-330">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="053d8-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="053d8-331">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="053d8-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="053d8-332">Strumieniowe przesyłanie dzienników z Azure tooyour terminali</span><span class="sxs-lookup"><span data-stu-id="053d8-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="053d8-333">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="053d8-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="053d8-334">Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy toohello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="053d8-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="053d8-335">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="053d8-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
