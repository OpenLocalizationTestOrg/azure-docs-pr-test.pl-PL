---
title: "toocreate aaaHow aplikacji sieci Web z pamięci podręcznej Redis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikacji sieci Web z pamięci podręcznej Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="26ac1-103">Jak toocreate aplikacji sieci Web z pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="26ac1-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26ac1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="26ac1-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="26ac1-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="26ac1-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="26ac1-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="26ac1-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="26ac1-107">Java</span><span class="sxs-lookup"><span data-stu-id="26ac1-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="26ac1-108">Python</span><span class="sxs-lookup"><span data-stu-id="26ac1-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="26ac1-109">Ten samouczek pokazuje, jak toocreate i wdrażanie aplikacji sieci web tooa aplikacji sieci web ASP.NET w usłudze Azure App Service przy użyciu programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="26ac1-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="26ac1-110">Hello przykładowej aplikacji zostanie wyświetlona lista statystyk zespołu z bazy danych i przedstawia różne sposoby toouse pamięć podręczna Redis Azure toostore i pobierania danych z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="26ac1-111">Po ukończeniu samouczka hello masz uruchomionej aplikacji sieci web, która odczytuje i zapisuje tooa bazy danych, zoptymalizowane z pamięci podręcznej Redis Azure i hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="26ac1-112">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="26ac1-112">You'll learn:</span></span>

* <span data-ttu-id="26ac1-113">Jak toocreate ASP.NET MVC 5 aplikacji sieci web w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26ac1-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="26ac1-114">Jak tooaccess danych z bazy danych przy użyciu programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="26ac1-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="26ac1-115">Jak tooimprove przepustowość i obniżyć obciążenie bazy danych przez przechowywania i pobierania danych przy użyciu pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="26ac1-116">Toouse Redis sortowania top zespoły 5 zestaw tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="26ac1-117">Jak tooprovision hello zasobów Azure dla aplikacji hello przy użyciu szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26ac1-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="26ac1-118">Jak toopublish hello tooAzure aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26ac1-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26ac1-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26ac1-119">Prerequisites</span></span>
<span data-ttu-id="26ac1-120">Samouczek hello toocomplete, musi mieć hello następujące wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="26ac1-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="26ac1-121">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26ac1-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="26ac1-122">Visual Studio 2017 z hello Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="26ac1-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="26ac1-123">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26ac1-123">Azure account</span></span>
<span data-ttu-id="26ac1-124">Należy samouczek hello toocomplete konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="26ac1-125">Możesz:</span><span class="sxs-lookup"><span data-stu-id="26ac1-125">You can:</span></span>

* <span data-ttu-id="26ac1-126">[Utworzyć bezpłatne konto platformy Azure ](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="26ac1-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="26ac1-127">Otrzymasz kredyt, które mogą być używane tootry limit płatnej usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="26ac1-128">Nawet po wyczerpaniu kredytu hello, można zachować hello konto i korzystać z bezpłatnych usług platformy Azure i funkcji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="26ac1-129">[Aktywować korzyści subskrybenta programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="26ac1-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="26ac1-130">W ramach subskrypcji MSDN co miesiąc otrzymasz środki, które możesz przeznaczyć na płatne usługi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="26ac1-131">Visual Studio 2017 z hello Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="26ac1-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="26ac1-132">Witaj samouczek jest przeznaczony dla programu Visual Studio 2017 z hello [zestawu Azure SDK dla platformy .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="26ac1-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="26ac1-133">Hello Azure SDK 2.9.5 jest dołączany hello Instalator Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26ac1-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="26ac1-134">Jeśli masz program Visual Studio 2015, możesz wykonać hello samouczek z hello [zestawu Azure SDK dla platformy .NET](../dotnet-sdk.md) 2.8.2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="26ac1-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="26ac1-135">[Pobieranie hello najnowszy zestaw Azure SDK dla programu Visual Studio 2015 tutaj](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="26ac1-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="26ac1-136">Visual Studio jest automatycznie instalowany z hello zestawu SDK, jeśli nie masz jeszcze go.</span><span class="sxs-lookup"><span data-stu-id="26ac1-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="26ac1-137">Niektóre ekrany mogą różnić się z ilustracjami hello przedstawiona w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="26ac1-138">Jeśli masz program Visual Studio 2013, możesz [pobierania hello najnowszy zestaw Azure SDK dla programu Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="26ac1-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="26ac1-139">Niektóre ekrany mogą różnić się z ilustracjami hello przedstawiona w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="26ac1-140">Tworzenie projektu programu Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="26ac1-141">Otwórz program Visual Studio i kliknij kolejno opcje **Plik**, **Nowy**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="26ac1-142">Rozwiń węzeł hello **Visual C#** węzła w hello **szablony** listy, wybierz **chmury**i kliknij przycisk **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="26ac1-143">Upewnij się, że został wybrany program **.NET Framework 4.5.2** lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="26ac1-144">Typ **ContosoTeamStats** do hello **nazwa** pole tekstowe i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Tworzenie projektu][cache-create-project]
3. <span data-ttu-id="26ac1-146">Wybierz **MVC** jako hello typu projektu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="26ac1-147">Upewnij się, że **bez uwierzytelniania** określono hello **uwierzytelniania** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="26ac1-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="26ac1-148">W zależności od używanej wersji programu Visual Studio hello domyślne można ustawić toosomething else.</span><span class="sxs-lookup"><span data-stu-id="26ac1-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="26ac1-149">toochange, kliknij przycisk **Zmień uwierzytelnianie** i wybierz **bez uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="26ac1-150">Jeśli wykonujesz wraz z programu Visual Studio 2015, wyczyść hello **Host w chmurze hello** wyboru.</span><span class="sxs-lookup"><span data-stu-id="26ac1-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="26ac1-151">Po otwarciu [udostępniania hello zasobów Azure](#provision-the-azure-resources) i [publikowania tooAzure aplikacji hello](#publish-the-application-to-azure) w kolejnych krokach samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="26ac1-152">Na przykład inicjowania obsługi administracyjnej aplikacji sieci web usługi aplikacji w programie Visual Studio, ponieważ powoduje pozostawienie **Host w chmurze hello** zaznaczone, zobacz [Rozpoczynanie pracy z aplikacjami sieci Web w usłudze Azure App Service przy użyciu platformy ASP.NET i Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="26ac1-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Wybieranie szablonu projektu][cache-select-template]
4. <span data-ttu-id="26ac1-154">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="26ac1-155">Utwórz hello aplikacji ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="26ac1-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="26ac1-156">W tej sekcji samouczka hello utworzysz hello podstawowe aplikacji, która odczytuje i wyświetla statystyki zespołu z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="26ac1-157">Dodaj pakiet NuGet programu Entity Framework hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="26ac1-158">Dodaj hello model</span><span class="sxs-lookup"><span data-stu-id="26ac1-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="26ac1-159">Dodawanie kontrolera hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="26ac1-160">Konfigurowanie hello widoków</span><span class="sxs-lookup"><span data-stu-id="26ac1-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="26ac1-161">Dodaj pakiet NuGet programu Entity Framework hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="26ac1-162">Kliknij przycisk **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="26ac1-163">Uruchom hello następujące polecenie z hello **Konsola Menedżera pakietów** okna.</span><span class="sxs-lookup"><span data-stu-id="26ac1-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="26ac1-164">Aby uzyskać więcej informacji o tym pakiecie, zobacz hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet strony.</span><span class="sxs-lookup"><span data-stu-id="26ac1-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="26ac1-165">Dodaj hello model</span><span class="sxs-lookup"><span data-stu-id="26ac1-165">Add hello model</span></span>
1. <span data-ttu-id="26ac1-166">Kliknij prawym przyciskiem myszy pozycję **Modele** w **Eksploratorze rozwiązań**, a następnie wybierz kolejno pozycje **Dodaj**, **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Dodawanie modelu][cache-model-add-class]
2. <span data-ttu-id="26ac1-168">Wprowadź `Team` hello nazwę klasy i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Dodawanie klasy modelu][cache-model-add-class-dialog]
3. <span data-ttu-id="26ac1-170">Zastąp hello `using` instrukcji u góry hello hello `Team.cs` pliku następujący hello `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="26ac1-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="26ac1-171">Zastąp definicję hello hello `Team` klas z następującego fragmentu kodu, który zawiera zaktualizowaną hello `Team` klasy definicji, a także kilka innych klas pomocniczych programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="26ac1-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="26ac1-172">Aby uzyskać więcej informacji dotyczących hello kod pierwszego podejścia tooEntity strukturę, która jest używana w tym samouczku, zobacz [kod pierwszego tooa nową bazę danych](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="26ac1-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="26ac1-173">W **Eksploratora rozwiązań**, kliknij dwukrotnie **web.config** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="26ac1-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="26ac1-175">Dodaj następujące hello `connectionStrings` sekcji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="26ac1-176">Hello nazwę parametrów połączenia hello musi odpowiadać nazwie hello hello klasy kontekstu bazy danych programu Entity Framework, która jest `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="26ac1-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="26ac1-177">Możesz dodać nowe hello `connectionStrings` sekcji, aby wynika `configSections`, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="26ac1-178">Parametry połączenia mogą być różne w zależności od wersji hello programu Visual Studio i samouczek hello toocomplete używać programu SQL Server Express edition.</span><span class="sxs-lookup"><span data-stu-id="26ac1-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="26ac1-179">Szablon pliku web.config Hello powinien być skonfigurowany toomatch instalację i może zawierać `Data Source` wpisów, takich jak `(LocalDB)\v11.0` (z programu SQL Server Express 2012) lub `Data Source=(LocalDB)\MSSQLLocalDB` (z programu SQL Server 2014 Express i nowszych).</span><span class="sxs-lookup"><span data-stu-id="26ac1-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="26ac1-180">Aby uzyskać więcej informacji o parametrach połączenia i wersjach programu SQL Express, zobacz [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="26ac1-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="26ac1-181">Dodawanie kontrolera hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-181">Add hello controller</span></span>
1. <span data-ttu-id="26ac1-182">Naciśnij klawisz **F6** toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="26ac1-183">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **kontrolerów** folder i wybierz polecenie **Dodaj**, **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Dodawanie kontrolera][cache-add-controller]
3. <span data-ttu-id="26ac1-185">Wybierz pozycję **Kontroler MVC 5 z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="26ac1-186">Jeśli błąd pojawia się po kliknięciu przycisku **Dodaj**, upewnij się najpierw skompilowany hello projektu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Dodawanie klasy kontrolera][cache-add-controller-class]
4. <span data-ttu-id="26ac1-188">Wybierz **zespołu (ContosoTeamStats.Models)** z hello **klasa modelu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="26ac1-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="26ac1-189">Wybierz **TeamContext (ContosoTeamStats.Models)** z hello **klasa kontekstu danych** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="26ac1-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="26ac1-190">Typ `TeamsController` w hello **kontrolera** tekstowe nazwy (Jeśli nie zostanie automatycznie wypełnione).</span><span class="sxs-lookup"><span data-stu-id="26ac1-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="26ac1-191">Kliknij przycisk **Dodaj** toocreate hello klasy kontrolera i Dodaj hello widoki.</span><span class="sxs-lookup"><span data-stu-id="26ac1-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Konfigurowanie kontrolera][cache-configure-controller]
5. <span data-ttu-id="26ac1-193">W **Eksploratora rozwiązań**, rozwiń węzeł **Global.asax** i kliknij dwukrotnie **Global.asax.cs** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="26ac1-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="26ac1-195">Dodaj następujące dwie hello `using` instrukcji u góry pliku hello hello innych hello `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="26ac1-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="26ac1-196">Dodaj następujące wiersz kodu na końcu hello hello hello `Application_Start` metody.</span><span class="sxs-lookup"><span data-stu-id="26ac1-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="26ac1-197">W **Eksploratorze rozwiązań** rozwiń folder `App_Start` i kliknij dwukrotnie pozycję `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="26ac1-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="26ac1-199">Zastąp `controller = "Home"` w hello następującego kodu w hello `RegisterRoutes` metody z `controller = "Teams"` pokazane na powitania poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="26ac1-200">Konfigurowanie hello widoków</span><span class="sxs-lookup"><span data-stu-id="26ac1-200">Configure hello views</span></span>
1. <span data-ttu-id="26ac1-201">W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, a następnie hello **Shared** folder, a następnie kliknij dwukrotnie **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="26ac1-203">Zmień zawartość hello hello `title` elementu i zastępowanie `My ASP.NET Application` z `Contoso Team Stats` pokazane na powitania poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="26ac1-204">W hello `body` sekcji, najpierw zaktualizować hello `Html.ActionLink` instrukcji i Zamień `Application name` z `Contoso Team Stats` i Zastąp `Home` z `Teams`.</span><span class="sxs-lookup"><span data-stu-id="26ac1-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="26ac1-205">Przed: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="26ac1-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="26ac1-206">Po: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="26ac1-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Zmiany kodu][cache-layout-cshtml-code]
2. <span data-ttu-id="26ac1-208">Naciśnij klawisz **Ctrl + F5** toobuild i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="26ac1-209">Ta wersja aplikacji hello odczytuje wyniki hello bezpośrednio z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="26ac1-210">Uwaga hello **Utwórz nowy**, **Edytuj**, **szczegóły**, i **usunąć** akcje, które były automatycznie dodawane toohello aplikacji przez hello **Kontroler MVC 5 z widokami używający narzędzia Entity Framework** szkieletu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="26ac1-211">W następnej sekcji hello hello samouczka możesz dodać dostępu do pamięci podręcznej Redis toooptimize hello danych i udostępnia dodatkowe funkcje toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Aplikacja startowa][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="26ac1-213">Skonfiguruj toouse aplikacji hello pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="26ac1-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="26ac1-214">W tej sekcji samouczka hello, należy skonfigurować hello przykładowej aplikacji toostore i pobrać statystyk zespołu Contoso z wystąpienia pamięci podręcznej Redis Azure za pomocą hello [programie StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) pamięci podręcznej klienta.</span><span class="sxs-lookup"><span data-stu-id="26ac1-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="26ac1-215">Skonfiguruj toouse aplikacji hello programie StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="26ac1-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="26ac1-216">Aktualizowanie hello TeamsController klasy tooreturn wyników z pamięci podręcznej hello lub hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="26ac1-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="26ac1-217">Zaktualizuj hello tworzenia, edycji i usunąć toowork metody z pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="26ac1-218">Zaktualizuj toowork widoku indeksu zespoły hello z pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="26ac1-219">Skonfiguruj toouse aplikacji hello programie StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="26ac1-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="26ac1-220">tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu pakietu NuGet w programie StackExchange.Redis powitania kliknij **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="26ac1-221">Uruchom hello następujące polecenie z hello `Package Manager Console` okna.</span><span class="sxs-lookup"><span data-stu-id="26ac1-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="26ac1-222">Witaj NuGet pakietu pliki do pobrania i dodaje hello jest wymagany odwołania do zestawów z tooaccess aplikacja klienta pamięci podręcznej Redis Azure z hello programie StackExchange.Redis pamięci podręcznej klienta.</span><span class="sxs-lookup"><span data-stu-id="26ac1-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="26ac1-223">Jeśli wolisz toouse o silnych nazwach wersji hello `StackExchange.Redis` biblioteki klienta, instalacja hello `StackExchange.Redis.StrongName` pakietu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="26ac1-224">W **Eksploratora rozwiązań**, rozwiń węzeł hello **kontrolerów** folder i kliknij dwukrotnie **TeamsController.cs** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="26ac1-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Kontroler zespołów][cache-teamscontroller]
4. <span data-ttu-id="26ac1-226">Dodaj następujące dwie hello `using` instrukcje zbyt**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="26ac1-227">Dodaj następujące dwie właściwości toohello hello `TeamsController` klasy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-227">Add hello following two properties toohello `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="26ac1-228">Utwórz plik na komputerze o nazwie `WebAppPlusCacheAppSecrets.config` i umieść go w lokalizacji, która nie będzie można zaewidencjonowane hello kodu źródłowego aplikacji przykładowej, należy określić toocheck go w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="26ac1-229">W tym hello przykład `AppSettingsSecrets.config` pliku znajduje się pod adresem `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="26ac1-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="26ac1-230">Edytuj hello `WebAppPlusCacheAppSecrets.config` plik i dodać powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="26ac1-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="26ac1-231">Po uruchomieniu aplikacji hello lokalnie te informacje są używane tooconnect tooyour pamięć podręczna Redis Azure wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="26ac1-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="26ac1-232">Później w samouczku hello możesz udostępnić wystąpienia pamięci podręcznej Redis Azure i zaktualizuj hello pamięci podręcznej nazwy i hasła.</span><span class="sxs-lookup"><span data-stu-id="26ac1-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="26ac1-233">Jeśli nie planujesz toorun hello przykładowej aplikacji lokalnie można pominąć tworzenie hello tego pliku i hello kolejne kroki odwołujących się hello pliku, ponieważ podczas wdrażania aplikacji hello tooAzure pobiera informacje o połączeniu pamięci podręcznej hello z aplikacji hello Ustawienie dla hello aplikacji sieci Web, a nie z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="26ac1-234">Ponieważ hello `WebAppPlusCacheAppSecrets.config` nie została wdrożona tooAzure z aplikacją, nie trzeba go, chyba że ma toorun aplikacji hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="26ac1-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="26ac1-235">W **Eksploratora rozwiązań**, kliknij dwukrotnie **web.config** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="26ac1-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="26ac1-237">Dodaj następujące hello `file` atrybutu toohello `appSettings` elementu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="26ac1-238">Jeśli używasz innej nazwy pliku lub lokalizacji, należy zastąpić tych wartości hello pokazano w przykładzie hello z nich.</span><span class="sxs-lookup"><span data-stu-id="26ac1-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="26ac1-239">Przed: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="26ac1-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="26ac1-240">Po: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="26ac1-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="26ac1-241">środowisko uruchomieniowe programu ASP.NET Hello Scala zawartość hello hello zewnętrznego pliku znaczników hello w hello `<appSettings>` elementu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="26ac1-242">środowiska uruchomieniowego Hello ignoruje hello atrybutu pliku, jeśli nie można odnaleźć określonego pliku hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="26ac1-243">Tajnych (hello połączenia pamięci podręcznej tooyour ciągów) nie są dołączane jako część hello kod źródłowy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="26ac1-244">Podczas wdrażania tooAzure aplikacji sieci web hello `WebAppPlusCacheAppSecrests.config` pliku nie zostaną wdrożone (do którego ma).</span><span class="sxs-lookup"><span data-stu-id="26ac1-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="26ac1-245">Istnieje kilka sposobów toospecify tych kluczy tajnych na platformie Azure i w tym samouczku są konfigurowane automatycznie automatycznie podczas możesz [udostępniania hello zasobów platformy Azure](#provision-the-azure-resources) w kolejnym kroku samouczka.</span><span class="sxs-lookup"><span data-stu-id="26ac1-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="26ac1-246">Aby uzyskać więcej informacji na temat pracy z kluczy tajnych na platformie Azure, zobacz [najlepsze rozwiązania dotyczące wdrażania haseł i innych danych poufnych tooASP.NET i usłudze Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="26ac1-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="26ac1-247">Aktualizowanie hello TeamsController klasy tooreturn wyników z pamięci podręcznej hello lub hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="26ac1-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="26ac1-248">W tym przykładzie statystyki zespołu może zostać pobrany z bazy danych hello lub hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="26ac1-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="26ac1-249">Statystyki zespołu są przechowywane w pamięci podręcznej hello jako serializacji `List<Team>`, a także jako posortowany zestawu przy użyciu typów danych Redis.</span><span class="sxs-lookup"><span data-stu-id="26ac1-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="26ac1-250">Podczas pobierania elementów z zestawu posortowanego możesz pobrać część z nich, wszystkie lub przesłać zapytanie o określone elementy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="26ac1-251">W tym przykładzie będzie zapytania zestawu hello sortowania dla zespołów 5 z najwyższym hello uszeregowane według liczby wins.</span><span class="sxs-lookup"><span data-stu-id="26ac1-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="26ac1-252">Nie jest wymagane toostore hello zespołu statystyk w wielu formatach w pamięci podręcznej hello w kolejności toouse pamięć podręczna Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="26ac1-253">Ten samouczek używa wielu formatów toodemonstrate niektóre sposoby hello i różne typy danych mogą być używane toocache danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="26ac1-254">Dodaj następujące hello `using` toohello instrukcje `TeamsController.cs` plików u góry hello hello innych `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="26ac1-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="26ac1-255">Zastąp bieżący hello `public ActionResult Index()` implementacji metody z powitania po implementacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="26ac1-256">Dodaj następujące trzy metody toohello hello `TeamsController` hello tooimplement klasy `playGames`, `clearCache`, i `rebuildDB` typów akcji z hello switch — instrukcja dodane w hello poprzedniego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="26ac1-257">Witaj `PlayGames` metody aktualizuje statystyki zespołu hello symulując sezonu gier, zapisuje hello bazy danych z wynikami toohello i czyści hello teraz przestarzałe dane z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="26ac1-258">Witaj `RebuildDB` bazy danych hello ponowne metody z hello domyślny zestaw zespołów, generuje statystyki dla nich i czyści hello teraz przestarzałe dane z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="26ac1-259">Witaj `ClearCachedTeams` metoda usuwa żadnych statystyk zespołu pamięci podręcznej z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="26ac1-260">Dodaj następujące cztery metody toohello hello `TeamsController` klasy tooimplement hello różne sposoby pobierania statystyki zespołu hello z pamięci podręcznej hello i hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="26ac1-261">Każda z tych metod zwraca `List<Team>` wyświetlone w widoku hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="26ac1-262">Witaj `GetFromDB` — metoda odczytuje statystyki zespołu hello z hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="26ac1-263">Witaj `GetFromList` metoda odczytuje statystyki zespołu hello z pamięci podręcznej jako serializacji `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="26ac1-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="26ac1-264">W przypadku Chybienie pamięci podręcznej, hello zespołu statystyki są odczytana z bazy danych hello i następnie przechowywane w pamięci podręcznej hello następnym razem.</span><span class="sxs-lookup"><span data-stu-id="26ac1-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="26ac1-265">W tym przykładzie używamy JSON.NET serializacji tooserialize hello .NET obiektów tooand z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="26ac1-266">Aby uzyskać więcej informacji, zobacz [jak toowork z platformą .NET obiektów w pamięci podręcznej Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="26ac1-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="26ac1-267">Witaj `GetFromSortedSet` metoda odczytuje statystyki zespołu hello z pamięci podręcznej zestawu posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="26ac1-268">W przypadku Chybienie pamięci podręcznej, hello zespołu statystyki są odczytana z bazy danych hello i przechowywane w pamięci podręcznej hello jako zestaw posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="26ac1-269">Witaj `GetFromSortedSetTop5` — metoda odczytuje hello top zespoły 5 z pamięci podręcznej hello sortowane zestawu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="26ac1-270">Rozpocznie się sprawdzanie pamięci podręcznej hello hello istnienia hello `teamsSortedSet` klucza.</span><span class="sxs-lookup"><span data-stu-id="26ac1-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="26ac1-271">Jeśli ten klucz nie jest obecny, hello `GetFromSortedSet` — metoda jest wywoływana tooread hello zespołu statystyk i zapisanie ich w pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="26ac1-272">Następnie hello pamięci podręcznej zestawu posortowane zostanie zapytany o hello top 5 zespołów, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="26ac1-273">Zaktualizuj hello tworzenia, edycji i usunąć toowork metody z pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="26ac1-274">Hello szkieletów kodu, który został wygenerowany jako część ten przykład zawiera metody tooadd, edytować lub usuwać zespołów.</span><span class="sxs-lookup"><span data-stu-id="26ac1-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="26ac1-275">W dowolnym momencie zespołu dodać, edytować lub usunąć, hello danych w pamięci podręcznej hello staje się nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="26ac1-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="26ac1-276">W tej sekcji, które będzie modyfikować tych trzech metod tooclear hello buforowany zespołów, dzięki czemu hello pamięci podręcznej nie będzie zsynchronizowany z hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="26ac1-277">Przeglądaj toohello `Create(Team team)` w hello metody `TeamsController` klasy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="26ac1-278">Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="26ac1-279">Przeglądaj toohello `Edit(Team team)` w hello metody `TeamsController` klasy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="26ac1-280">Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="26ac1-281">Przeglądaj toohello `DeleteConfirmed(int id)` w hello metody `TeamsController` klasy.</span><span class="sxs-lookup"><span data-stu-id="26ac1-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="26ac1-282">Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="26ac1-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="26ac1-283">Zaktualizuj toowork widoku indeksu zespoły hello z pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="26ac1-284">W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, a następnie hello **zespołów** folder, a następnie kliknij dwukrotnie **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="26ac1-286">U góry hello pliku hello poszukaj hello następującego elementu akapitu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Tabela akcji][cache-teams-index-table]
   
    <span data-ttu-id="26ac1-288">Jest to toocreate łącze hello nowego zespołu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="26ac1-289">Zastąp element akapitu hello hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="26ac1-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="26ac1-290">Ta tabela ma łącza akcji do tworzenia nowego zespołu odtwarzanie nowego sezonu gier, czyszczenie pamięci podręcznej hello, pobierania zespoły hello z pamięci podręcznej hello w wielu formatach, pobieranie zespoły hello z hello bazy danych i ponownie skompilować hello bazy danych z nową próbkę danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="26ac1-291">Przewiń w dół toohello hello **Index.cshtml** i dodaj następujące hello `tr` element, aby była hello ostatni wiersz w hello ostatniej tabeli w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="26ac1-292">Ten wiersz zawiera wartość hello `ViewBag.Msg` zawierającą raport o hello bieżącej operacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="26ac1-293">Witaj `ViewBag.Msg` jest ustawiona, po kliknięciu dowolnej łącza akcji hello hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Komunikat o stanie][cache-status-message]
2. <span data-ttu-id="26ac1-295">Naciśnij klawisz **F6** toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="26ac1-296">Zainicjuj obsługę hello zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26ac1-296">Provision hello Azure resources</span></span>
<span data-ttu-id="26ac1-297">toohost aplikacji na platformie Azure, należy najpierw umożliwić hello usług platformy Azure wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="26ac1-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="26ac1-298">Witaj przykładowej aplikacji w tym samouczku używa hello następujących usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="26ac1-299">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="26ac1-299">Azure Redis Cache</span></span>
* <span data-ttu-id="26ac1-300">Aplikacja sieci Web usługi App Service</span><span class="sxs-lookup"><span data-stu-id="26ac1-300">App Service Web App</span></span>
* <span data-ttu-id="26ac1-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="26ac1-301">SQL Database</span></span>

<span data-ttu-id="26ac1-302">toodeploy tych usług tooa nowy lub istniejący zasób grupy wybranych przez użytkownika, kliknij przycisk powitania po **wdrażanie tooAzure** przycisku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="26ac1-303">[! [Wdrażanie tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="26ac1-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="26ac1-304">To **wdrażanie tooAzure** przycisk używa hello [tworzenie aplikacji sieci Web oraz pamięci podręcznej Redis oraz bazy danych SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) tooprovision szablonu tych usług i hello zestawu Parametry połączenia dla hello bazy danych SQL i hello ustawienie aplikacji hello parametry połączenia z pamięcią podręczną Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="26ac1-305">Jeśli nie masz konta platformy Azure, możesz [utworzyć bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="26ac1-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="26ac1-306">Kliknięcie przycisku hello **wdrażanie tooAzure** przycisk przyjmuje toohello portalu Azure i inicjuje hello proces tworzenia zasobów hello opisanego przez hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Wdrażanie tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="26ac1-308">W hello **podstawy** sekcji, wybierz hello toouse subskrypcji platformy Azure, wybierz istniejącą grupę zasobów lub Utwórz nowy i określ lokalizacja grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="26ac1-309">W hello **ustawienia** określ **logowania administratora** (nie należy używać **admin**), **hasło logowania administratora**i  **Nazwa bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="26ac1-310">Hello inne parametry są konfigurowane pod kątem wolnego aplikacji usługi hostingu planu i tanie opcji hello bazy danych SQL i pamięcią podręczną Redis Azure, które nie pochodzą z warstwę bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="26ac1-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Wdrażanie tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="26ac1-312">Po skonfigurowaniu ustawień hello potrzebne, przewiń koniec toohello hello strony, hello przeczytaj warunki i postanowienia, a następnie sprawdź hello **zgadzam się toohello warunki i postanowienia, o których wspomniano** wyboru.</span><span class="sxs-lookup"><span data-stu-id="26ac1-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="26ac1-313">Kliknij toobegin inicjowania obsługi administracyjnej zasobów hello, **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="26ac1-314">postęp hello tooview wdrożenia, kliknij ikonę powiadomienia hello i kliknij przycisk **rozpoczęto wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Wdrażanie rozpoczęte][cache-deployment-started]

<span data-ttu-id="26ac1-316">Można wyświetlić stan hello wdrożenia na powitania **Microsoft.Template** bloku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Wdrażanie tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="26ac1-318">Po zakończeniu inicjowania obsługi można opublikować tooAzure Twojej aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26ac1-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="26ac1-319">Wszelkie błędy, które mogą wystąpić podczas procesu udostępniania hello są wyświetlane na powitania **Microsoft.Template** bloku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="26ac1-320">Typowe błędy polegają na tym, że jest za dużo serwerów SQL Server lub za dużo planów hostowania Usługi aplikacji w warstwie Bezpłatna na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="26ac1-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="26ac1-321">Usuń wszelkie błędy i ponownie uruchomić proces hello klikając **ponownie wdrożyć** na powitania **Microsoft.Template** bloku lub hello **wdrażanie tooAzure** przycisku w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="26ac1-322">Publikowanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="26ac1-323">W tym kroku samouczka hello możesz opublikować tooAzure aplikacji hello i uruchomić go w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="26ac1-324">Kliknij prawym przyciskiem myszy hello **ContosoTeamStats** projekt w programie Visual Studio i wybierz pozycję **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publikowanie][cache-publish-app]
2. <span data-ttu-id="26ac1-326">Kliknij przycisk **Usługa aplikacji Microsoft Azure**, wybierz pozycję **Wybierz istniejące**i kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publikowanie][cache-publish-to-app-service]
3. <span data-ttu-id="26ac1-328">Wybierz subskrypcję hello używany podczas tworzenia hello zasobów platformy Azure, rozwiń grupę zasobów hello zawierającego zasoby hello i wybierz hello potrzeby aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="26ac1-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="26ac1-329">Jeśli używasz hello **wdrażanie tooAzure** przycisk nazwę aplikacji sieci Web, który rozpoczyna się od **witryny sieci Web** następuje niektóre dodatkowe znaki.</span><span class="sxs-lookup"><span data-stu-id="26ac1-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Wybieranie aplikacji sieci Web][cache-select-web-app]
4. <span data-ttu-id="26ac1-331">Kliknij przycisk **OK** hello toobegin procesu publikowania.</span><span class="sxs-lookup"><span data-stu-id="26ac1-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="26ac1-332">Po kilku chwilach kończy hello procesu publikowania i przeglądarką jest uruchamiana z systemem Przykładowa aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="26ac1-333">Jeśli wyświetlony komunikat o błędzie DNS podczas sprawdzania poprawności lub publikowania i hello procesu dla udostępniania hello zasobów Azure dla aplikacji hello zostało niedawno ukończone, zaczekaj chwilę i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="26ac1-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Dodano pamięć podręczną][cache-added-to-application]

<span data-ttu-id="26ac1-335">Witaj poniższej tabeli opisano każdego łącza akcji z hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="26ac1-336">Akcja</span><span class="sxs-lookup"><span data-stu-id="26ac1-336">Action</span></span> | <span data-ttu-id="26ac1-337">Opis</span><span class="sxs-lookup"><span data-stu-id="26ac1-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26ac1-338">Create New (Utwórz nowe)</span><span class="sxs-lookup"><span data-stu-id="26ac1-338">Create New</span></span> |<span data-ttu-id="26ac1-339">Tworzenie nowego zespołu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-339">Create a new Team.</span></span> |
| <span data-ttu-id="26ac1-340">Play Season (Odtwarzaj sezon)</span><span class="sxs-lookup"><span data-stu-id="26ac1-340">Play Season</span></span> |<span data-ttu-id="26ac1-341">Odtwarzanie sezonu gier, Statystyka zespołu hello aktualizacji, i wyczyść nieaktualne żadnego zespołu danych z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="26ac1-342">Clear Cache (Wyczyść pamięć podręczną)</span><span class="sxs-lookup"><span data-stu-id="26ac1-342">Clear Cache</span></span> |<span data-ttu-id="26ac1-343">Statystyka zespołu hello Wyczyść z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="26ac1-344">List from Cache (Lista z pamięci podręcznej)</span><span class="sxs-lookup"><span data-stu-id="26ac1-344">List from Cache</span></span> |<span data-ttu-id="26ac1-345">Pobierz Statystyka zespołu hello z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="26ac1-346">W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej dla następnym razem.</span><span class="sxs-lookup"><span data-stu-id="26ac1-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="26ac1-347">Sorted Set from Cache (Zestaw posortowany z pamięci podręcznej)</span><span class="sxs-lookup"><span data-stu-id="26ac1-347">Sorted Set from Cache</span></span> |<span data-ttu-id="26ac1-348">Pobierz Statystyka zespołu hello z hello pamięci podręcznej przy użyciu zestawu posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="26ac1-349">W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej przy użyciu zestawu posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="26ac1-350">Top 5 Teams from Cache (5 najlepszych zespołów z pamięci podręcznej)</span><span class="sxs-lookup"><span data-stu-id="26ac1-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="26ac1-351">Pobrać górnego zespoły 5 hello z pamięci podręcznej hello przy użyciu zestawu posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="26ac1-352">W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej przy użyciu zestawu posortowane.</span><span class="sxs-lookup"><span data-stu-id="26ac1-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="26ac1-353">Load from DB (Ładuj z bazy danych)</span><span class="sxs-lookup"><span data-stu-id="26ac1-353">Load from DB</span></span> |<span data-ttu-id="26ac1-354">Statystyka zespołu hello należy pobrać hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="26ac1-355">Rebuild DB (Odbuduj bazę danych)</span><span class="sxs-lookup"><span data-stu-id="26ac1-355">Rebuild DB</span></span> |<span data-ttu-id="26ac1-356">Odbuduj hello bazy danych i załadować go ponownie z przykładowymi danymi zespołu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="26ac1-357">Edytuj / Szczegóły / Usuń</span><span class="sxs-lookup"><span data-stu-id="26ac1-357">Edit / Details / Delete</span></span> |<span data-ttu-id="26ac1-358">Edytowanie zespołu, wyświetlanie szczegółów dla zespołu, usuwanie zespołu.</span><span class="sxs-lookup"><span data-stu-id="26ac1-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="26ac1-359">Niektóre akcje powitania kliknij i eksperymentować pobieranie hello danych z różnych źródeł hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="26ac1-360">Nie hello różnice w hello czas toocomplete hello różne sposoby pobierania hello danych z bazy danych hello i hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="26ac1-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="26ac1-361">Witaj zasoby zostaną usunięte po zakończeniu pracy z aplikacją hello</span><span class="sxs-lookup"><span data-stu-id="26ac1-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="26ac1-362">Po zakończeniu hello przykładowej samouczek aplikacji hello Azure można usunąć zasoby używane w kolejności tooconserve koszt i zasoby.</span><span class="sxs-lookup"><span data-stu-id="26ac1-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="26ac1-363">Jeśli używasz hello **wdrażanie tooAzure** przycisku na powitania [udostępniania hello zasobów platformy Azure](#provision-the-azure-resources) sekcji i wszystkich zasobów objętych hello tej samej grupie zasobów, można je usunąć razem w jednym Operacja przez usunięcie hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="26ac1-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="26ac1-364">Zaloguj się toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="26ac1-365">Typ hello nazwę grupy zasobów do hello **filtrować elementy...**  pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="26ac1-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="26ac1-366">Kliknij przycisk **...**  toohello prawo do swojej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="26ac1-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="26ac1-367">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-367">Click **Delete**.</span></span>
   
    ![Usuwanie][cache-delete-resource-group]
5. <span data-ttu-id="26ac1-369">Typ hello nazwy grupy zasobów i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="26ac1-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Potwierdzenie usunięcia][cache-delete-confirm]

<span data-ttu-id="26ac1-371">Po kilku chwilach hello zasobów grupy i wszystkich zawartych w niej zasobów zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="26ac1-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26ac1-372">Należy pamiętać, że usunięcie grupy zasobów jest nieodwracalna i że hello grupy zasobów i wszystkie zasoby hello w nim zostaną trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="26ac1-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="26ac1-373">Upewnij się, że nie zostaną przypadkowo usunięte grupy zasobów niewłaściwy hello lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="26ac1-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="26ac1-374">Jeśli utworzono hello zasobów dla hostingu w tym przykładzie wewnątrz istniejącą grupę zasobów, możesz usunąć każdego zasobu indywidualnie z ich odpowiednich bloków.</span><span class="sxs-lookup"><span data-stu-id="26ac1-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="26ac1-375">Uruchom hello przykładowej aplikacji na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="26ac1-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="26ac1-376">Aplikacja hello toorun lokalnie na komputerze, należy pamięć podręczna Redis Azure wystąpienia, w których toocache danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="26ac1-377">Po opublikowaniu tooAzure Twojej aplikacji zgodnie z opisem w poprzedniej sekcji hello, możesz użyć wystąpienia pamięci podręcznej Redis Azure hello, udostępniony w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="26ac1-378">Jeśli masz inne istniejące wystąpienie pamięci podręcznej Redis Azure możesz użyć tego toorun tego przykładu lokalnie.</span><span class="sxs-lookup"><span data-stu-id="26ac1-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="26ac1-379">Jeśli potrzebujesz toocreate wystąpienia pamięci podręcznej Redis Azure, można wykonać kroki hello w [tworzenia pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="26ac1-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="26ac1-380">Po wybraniu lub utworzyć toouse pamięci podręcznej hello Przeglądaj toohello pamięci podręcznej w hello portalu Azure i pobrać hello [nazwy hosta](cache-configure.md#properties) i [klucze dostępu](cache-configure.md#access-keys) dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="26ac1-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="26ac1-381">Instrukcje znajdują się w artykule [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings) (Konfigurowanie ustawień pamięci podręcznej Redis).</span><span class="sxs-lookup"><span data-stu-id="26ac1-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="26ac1-382">Otwórz hello `WebAppPlusCacheAppSecrets.config` pliku utworzonego podczas hello [skonfigurować toouse aplikacji hello pamięci podręcznej Redis](#configure-the-application-to-use-redis-cache) kroku w tym samouczku za pomocą dowolnego edytora hello.</span><span class="sxs-lookup"><span data-stu-id="26ac1-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="26ac1-383">Edytuj hello `value` atrybutu i Zastąp `MyCache.redis.cache.windows.net` z hello [nazwy hosta](cache-configure.md#properties) z pamięci podręcznej i określ albo hello [klucz podstawowy lub pomocniczy](cache-configure.md#access-keys) z pamięci podręcznej jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="26ac1-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="26ac1-384">Naciśnij klawisz **Ctrl + F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="26ac1-385">Należy pamiętać, że ponieważ aplikacji hello, w tym hello bazy danych, jest uruchomiony lokalnie i hello pamięci podręcznej Redis jest hostowana na platformie Azure, hello pamięci podręcznej może pojawić się toounder — wykonaj hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="26ac1-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="26ac1-386">Aby uzyskać najlepszą wydajność, hello aplikacji klienckiej, a wystąpienia pamięci podręcznej Redis Azure powinny być hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="26ac1-387">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26ac1-387">Next steps</span></span>
* <span data-ttu-id="26ac1-388">Dowiedz się więcej o [wprowadzenie do platformy ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) na powitania [ASP.NET](http://asp.net/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="26ac1-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="26ac1-389">Więcej przykładów dotyczących tworzenia aplikacji sieci Web platformy ASP.NET w usłudze App Service, zobacz [tworzenie i wdrażanie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) z hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [pokaz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="26ac1-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="26ac1-390">Przewodniki Szybki Start więcej z hello HealthClinic.biz demonstracyjnej, aby zapoznać [Przewodniki Szybki Start Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="26ac1-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="26ac1-391">Dowiedz się więcej o hello [kod pierwszego tooa nową bazę danych](https://msdn.microsoft.com/data/jj193542) podejścia tooEntity strukturę, która jest używana w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="26ac1-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="26ac1-392">Dowiedz się więcej na temat [aplikacji sieci Web w Usłudze aplikacji Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26ac1-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="26ac1-393">Dowiedz się, jak za[monitor](cache-how-to-monitor.md) pamięci podręcznej w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac1-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="26ac1-394">Poznaj funkcje Premium usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="26ac1-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="26ac1-395">Jak tooconfigure trwałości dla podręczna Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="26ac1-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="26ac1-396">Jak tooconfigure klastrowania podręczna Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="26ac1-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="26ac1-397">Jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="26ac1-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="26ac1-398">Zobacz hello [często zadawane pytania pamięci podręcznej Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) szczegółowe informacje o rozmiarze, przepływności i przepustowości z pamięci podręcznych premium.</span><span class="sxs-lookup"><span data-stu-id="26ac1-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

