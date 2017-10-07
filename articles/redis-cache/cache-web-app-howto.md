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
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Jak toocreate aplikacji sieci Web z pamięci podręcznej Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Ten samouczek pokazuje, jak toocreate i wdrażanie aplikacji sieci web tooa aplikacji sieci web ASP.NET w usłudze Azure App Service przy użyciu programu Visual Studio 2017 r. Hello przykładowej aplikacji zostanie wyświetlona lista statystyk zespołu z bazy danych i przedstawia różne sposoby toouse pamięć podręczna Redis Azure toostore i pobierania danych z pamięci podręcznej hello. Po ukończeniu samouczka hello masz uruchomionej aplikacji sieci web, która odczytuje i zapisuje tooa bazy danych, zoptymalizowane z pamięci podręcznej Redis Azure i hostowanej na platformie Azure.

Dowiesz się:

* Jak toocreate ASP.NET MVC 5 aplikacji sieci web w programie Visual Studio.
* Jak tooaccess danych z bazy danych przy użyciu programu Entity Framework.
* Jak tooimprove przepustowość i obniżyć obciążenie bazy danych przez przechowywania i pobierania danych przy użyciu pamięci podręcznej Redis Azure.
* Toouse Redis sortowania top zespoły 5 zestaw tooretrieve hello.
* Jak tooprovision hello zasobów Azure dla aplikacji hello przy użyciu szablonu usługi Resource Manager.
* Jak toopublish hello tooAzure aplikacji przy użyciu programu Visual Studio.

## <a name="prerequisites"></a>Wymagania wstępne
Samouczek hello toocomplete, musi mieć hello następujące wymagania wstępne.

* [Konto platformy Azure](#azure-account)
* [Visual Studio 2017 z hello Azure SDK dla platformy .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Konto platformy Azure
Należy samouczek hello toocomplete konto platformy Azure. Możesz:

* [Utworzyć bezpłatne konto platformy Azure ](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Otrzymasz kredyt, które mogą być używane tootry limit płatnej usług platformy Azure. Nawet po wyczerpaniu kredytu hello, można zachować hello konto i korzystać z bezpłatnych usług platformy Azure i funkcji.
* [Aktywować korzyści subskrybenta programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). W ramach subskrypcji MSDN co miesiąc otrzymasz środki, które możesz przeznaczyć na płatne usługi platformy Azure.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017 z hello Azure SDK dla platformy .NET
Witaj samouczek jest przeznaczony dla programu Visual Studio 2017 z hello [zestawu Azure SDK dla platformy .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Hello Azure SDK 2.9.5 jest dołączany hello Instalator Visual Studio.

Jeśli masz program Visual Studio 2015, możesz wykonać hello samouczek z hello [zestawu Azure SDK dla platformy .NET](../dotnet-sdk.md) 2.8.2 lub nowszym. [Pobieranie hello najnowszy zestaw Azure SDK dla programu Visual Studio 2015 tutaj](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio jest automatycznie instalowany z hello zestawu SDK, jeśli nie masz jeszcze go. Niektóre ekrany mogą różnić się z ilustracjami hello przedstawiona w tym samouczku.

Jeśli masz program Visual Studio 2013, możesz [pobierania hello najnowszy zestaw Azure SDK dla programu Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Niektóre ekrany mogą różnić się z ilustracjami hello przedstawiona w tym samouczku.

## <a name="create-hello-visual-studio-project"></a>Tworzenie projektu programu Visual Studio hello
1. Otwórz program Visual Studio i kliknij kolejno opcje **Plik**, **Nowy**, **Projekt**.
2. Rozwiń węzeł hello **Visual C#** węzła w hello **szablony** listy, wybierz **chmury**i kliknij przycisk **aplikacji sieci Web ASP.NET**. Upewnij się, że został wybrany program **.NET Framework 4.5.2** lub nowszy.  Typ **ContosoTeamStats** do hello **nazwa** pole tekstowe i kliknij przycisk **OK**.
   
    ![Tworzenie projektu][cache-create-project]
3. Wybierz **MVC** jako hello typu projektu. 

    Upewnij się, że **bez uwierzytelniania** określono hello **uwierzytelniania** ustawienia. W zależności od używanej wersji programu Visual Studio hello domyślne można ustawić toosomething else. toochange, kliknij przycisk **Zmień uwierzytelnianie** i wybierz **bez uwierzytelniania**.

    Jeśli wykonujesz wraz z programu Visual Studio 2015, wyczyść hello **Host w chmurze hello** wyboru. Po otwarciu [udostępniania hello zasobów Azure](#provision-the-azure-resources) i [publikowania tooAzure aplikacji hello](#publish-the-application-to-azure) w kolejnych krokach samouczka hello. Na przykład inicjowania obsługi administracyjnej aplikacji sieci web usługi aplikacji w programie Visual Studio, ponieważ powoduje pozostawienie **Host w chmurze hello** zaznaczone, zobacz [Rozpoczynanie pracy z aplikacjami sieci Web w usłudze Azure App Service przy użyciu platformy ASP.NET i Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Wybieranie szablonu projektu][cache-select-template]
4. Kliknij przycisk **OK** toocreate hello projektu.

## <a name="create-hello-aspnet-mvc-application"></a>Utwórz hello aplikacji ASP.NET MVC
W tej sekcji samouczka hello utworzysz hello podstawowe aplikacji, która odczytuje i wyświetla statystyki zespołu z bazy danych.

* [Dodaj pakiet NuGet programu Entity Framework hello](#add-the-entity-framework-nuget-package)
* [Dodaj hello model](#add-the-model)
* [Dodawanie kontrolera hello](#add-the-controller)
* [Konfigurowanie hello widoków](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Dodaj pakiet NuGet programu Entity Framework hello

1. Kliknij przycisk **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.
2. Uruchom hello następujące polecenie z hello **Konsola Menedżera pakietów** okna.
    
    ```
    Install-Package EntityFramework
    ```

Aby uzyskać więcej informacji o tym pakiecie, zobacz hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet strony.

### <a name="add-hello-model"></a>Dodaj hello model
1. Kliknij prawym przyciskiem myszy pozycję **Modele** w **Eksploratorze rozwiązań**, a następnie wybierz kolejno pozycje **Dodaj**, **Klasa**. 
   
    ![Dodawanie modelu][cache-model-add-class]
2. Wprowadź `Team` hello nazwę klasy i kliknij przycisk **Dodaj**.
   
    ![Dodawanie klasy modelu][cache-model-add-class-dialog]
3. Zastąp hello `using` instrukcji u góry hello hello `Team.cs` pliku następujący hello `using` instrukcje.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Zastąp definicję hello hello `Team` klas z następującego fragmentu kodu, który zawiera zaktualizowaną hello `Team` klasy definicji, a także kilka innych klas pomocniczych programu Entity Framework. Aby uzyskać więcej informacji dotyczących hello kod pierwszego podejścia tooEntity strukturę, która jest używana w tym samouczku, zobacz [kod pierwszego tooa nową bazę danych](https://msdn.microsoft.com/data/jj193542).

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


1. W **Eksploratora rozwiązań**, kliknij dwukrotnie **web.config** tooopen go.
   
    ![Web.config][cache-web-config]
2. Dodaj następujące hello `connectionStrings` sekcji. Hello nazwę parametrów połączenia hello musi odpowiadać nazwie hello hello klasy kontekstu bazy danych programu Entity Framework, która jest `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Możesz dodać nowe hello `connectionStrings` sekcji, aby wynika `configSections`, jak pokazano w hello poniższy przykład.

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
    > Parametry połączenia mogą być różne w zależności od wersji hello programu Visual Studio i samouczek hello toocomplete używać programu SQL Server Express edition. Szablon pliku web.config Hello powinien być skonfigurowany toomatch instalację i może zawierać `Data Source` wpisów, takich jak `(LocalDB)\v11.0` (z programu SQL Server Express 2012) lub `Data Source=(LocalDB)\MSSQLLocalDB` (z programu SQL Server 2014 Express i nowszych). Aby uzyskać więcej informacji o parametrach połączenia i wersjach programu SQL Express, zobacz [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Dodawanie kontrolera hello
1. Naciśnij klawisz **F6** toobuild hello projektu. 
2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **kontrolerów** folder i wybierz polecenie **Dodaj**, **kontrolera**.
   
    ![Dodawanie kontrolera][cache-add-controller]
3. Wybierz pozycję **Kontroler MVC 5 z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**. Jeśli błąd pojawia się po kliknięciu przycisku **Dodaj**, upewnij się najpierw skompilowany hello projektu.
   
    ![Dodawanie klasy kontrolera][cache-add-controller-class]
4. Wybierz **zespołu (ContosoTeamStats.Models)** z hello **klasa modelu** listy rozwijanej. Wybierz **TeamContext (ContosoTeamStats.Models)** z hello **klasa kontekstu danych** listy rozwijanej. Typ `TeamsController` w hello **kontrolera** tekstowe nazwy (Jeśli nie zostanie automatycznie wypełnione). Kliknij przycisk **Dodaj** toocreate hello klasy kontrolera i Dodaj hello widoki.
   
    ![Konfigurowanie kontrolera][cache-configure-controller]
5. W **Eksploratora rozwiązań**, rozwiń węzeł **Global.asax** i kliknij dwukrotnie **Global.asax.cs** tooopen go.
   
    ![Global.asax.cs][cache-global-asax]
6. Dodaj następujące dwie hello `using` instrukcji u góry pliku hello hello innych hello `using` instrukcje.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Dodaj następujące wiersz kodu na końcu hello hello hello `Application_Start` metody.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. W **Eksploratorze rozwiązań** rozwiń folder `App_Start` i kliknij dwukrotnie pozycję `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Zastąp `controller = "Home"` w hello następującego kodu w hello `RegisterRoutes` metody z `controller = "Teams"` pokazane na powitania poniższy przykład.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Konfigurowanie hello widoków
1. W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, a następnie hello **Shared** folder, a następnie kliknij dwukrotnie **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Zmień zawartość hello hello `title` elementu i zastępowanie `My ASP.NET Application` z `Contoso Team Stats` pokazane na powitania poniższy przykład.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. W hello `body` sekcji, najpierw zaktualizować hello `Html.ActionLink` instrukcji i Zamień `Application name` z `Contoso Team Stats` i Zastąp `Home` z `Teams`.
   
   * Przed: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Po: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Zmiany kodu][cache-layout-cshtml-code]
2. Naciśnij klawisz **Ctrl + F5** toobuild i uruchamianie aplikacji hello. Ta wersja aplikacji hello odczytuje wyniki hello bezpośrednio z bazy danych hello. Uwaga hello **Utwórz nowy**, **Edytuj**, **szczegóły**, i **usunąć** akcje, które były automatycznie dodawane toohello aplikacji przez hello **Kontroler MVC 5 z widokami używający narzędzia Entity Framework** szkieletu. W następnej sekcji hello hello samouczka możesz dodać dostępu do pamięci podręcznej Redis toooptimize hello danych i udostępnia dodatkowe funkcje toohello aplikacji.

![Aplikacja startowa][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Skonfiguruj toouse aplikacji hello pamięci podręcznej Redis
W tej sekcji samouczka hello, należy skonfigurować hello przykładowej aplikacji toostore i pobrać statystyk zespołu Contoso z wystąpienia pamięci podręcznej Redis Azure za pomocą hello [programie StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) pamięci podręcznej klienta.

* [Skonfiguruj toouse aplikacji hello programie StackExchange.Redis](#configure-the-application-to-use-stackexchangeredis)
* [Aktualizowanie hello TeamsController klasy tooreturn wyników z pamięci podręcznej hello lub hello bazy danych](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Zaktualizuj hello tworzenia, edycji i usunąć toowork metody z pamięci podręcznej hello](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Zaktualizuj toowork widoku indeksu zespoły hello z pamięci podręcznej hello](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Skonfiguruj toouse aplikacji hello programie StackExchange.Redis
1. tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu pakietu NuGet w programie StackExchange.Redis powitania kliknij **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu.
2. Uruchom hello następujące polecenie z hello `Package Manager Console` okna.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Witaj NuGet pakietu pliki do pobrania i dodaje hello jest wymagany odwołania do zestawów z tooaccess aplikacja klienta pamięci podręcznej Redis Azure z hello programie StackExchange.Redis pamięci podręcznej klienta. Jeśli wolisz toouse o silnych nazwach wersji hello `StackExchange.Redis` biblioteki klienta, instalacja hello `StackExchange.Redis.StrongName` pakietu.
3. W **Eksploratora rozwiązań**, rozwiń węzeł hello **kontrolerów** folder i kliknij dwukrotnie **TeamsController.cs** tooopen go.
   
    ![Kontroler zespołów][cache-teamscontroller]
4. Dodaj następujące dwie hello `using` instrukcje zbyt**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Dodaj następujące dwie właściwości toohello hello `TeamsController` klasy.

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

6. Utwórz plik na komputerze o nazwie `WebAppPlusCacheAppSecrets.config` i umieść go w lokalizacji, która nie będzie można zaewidencjonowane hello kodu źródłowego aplikacji przykładowej, należy określić toocheck go w innym miejscu. W tym hello przykład `AppSettingsSecrets.config` pliku znajduje się pod adresem `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Edytuj hello `WebAppPlusCacheAppSecrets.config` plik i dodać powitania po zawartości. Po uruchomieniu aplikacji hello lokalnie te informacje są używane tooconnect tooyour pamięć podręczna Redis Azure wystąpienia. Później w samouczku hello możesz udostępnić wystąpienia pamięci podręcznej Redis Azure i zaktualizuj hello pamięci podręcznej nazwy i hasła. Jeśli nie planujesz toorun hello przykładowej aplikacji lokalnie można pominąć tworzenie hello tego pliku i hello kolejne kroki odwołujących się hello pliku, ponieważ podczas wdrażania aplikacji hello tooAzure pobiera informacje o połączeniu pamięci podręcznej hello z aplikacji hello Ustawienie dla hello aplikacji sieci Web, a nie z tego pliku. Ponieważ hello `WebAppPlusCacheAppSecrets.config` nie została wdrożona tooAzure z aplikacją, nie trzeba go, chyba że ma toorun aplikacji hello lokalnie.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. W **Eksploratora rozwiązań**, kliknij dwukrotnie **web.config** tooopen go.
   
    ![Web.config][cache-web-config]
2. Dodaj następujące hello `file` atrybutu toohello `appSettings` elementu. Jeśli używasz innej nazwy pliku lub lokalizacji, należy zastąpić tych wartości hello pokazano w przykładzie hello z nich.
   
   * Przed: `<appSettings>`
   * Po: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   środowisko uruchomieniowe programu ASP.NET Hello Scala zawartość hello hello zewnętrznego pliku znaczników hello w hello `<appSettings>` elementu. środowiska uruchomieniowego Hello ignoruje hello atrybutu pliku, jeśli nie można odnaleźć określonego pliku hello. Tajnych (hello połączenia pamięci podręcznej tooyour ciągów) nie są dołączane jako część hello kod źródłowy aplikacji hello. Podczas wdrażania tooAzure aplikacji sieci web hello `WebAppPlusCacheAppSecrests.config` pliku nie zostaną wdrożone (do którego ma). Istnieje kilka sposobów toospecify tych kluczy tajnych na platformie Azure i w tym samouczku są konfigurowane automatycznie automatycznie podczas możesz [udostępniania hello zasobów platformy Azure](#provision-the-azure-resources) w kolejnym kroku samouczka. Aby uzyskać więcej informacji na temat pracy z kluczy tajnych na platformie Azure, zobacz [najlepsze rozwiązania dotyczące wdrażania haseł i innych danych poufnych tooASP.NET i usłudze Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Aktualizowanie hello TeamsController klasy tooreturn wyników z pamięci podręcznej hello lub hello bazy danych
W tym przykładzie statystyki zespołu może zostać pobrany z bazy danych hello lub hello pamięci podręcznej. Statystyki zespołu są przechowywane w pamięci podręcznej hello jako serializacji `List<Team>`, a także jako posortowany zestawu przy użyciu typów danych Redis. Podczas pobierania elementów z zestawu posortowanego możesz pobrać część z nich, wszystkie lub przesłać zapytanie o określone elementy. W tym przykładzie będzie zapytania zestawu hello sortowania dla zespołów 5 z najwyższym hello uszeregowane według liczby wins.

> [!NOTE]
> Nie jest wymagane toostore hello zespołu statystyk w wielu formatach w pamięci podręcznej hello w kolejności toouse pamięć podręczna Redis Azure. Ten samouczek używa wielu formatów toodemonstrate niektóre sposoby hello i różne typy danych mogą być używane toocache danych.
> 
> 

1. Dodaj następujące hello `using` toohello instrukcje `TeamsController.cs` plików u góry hello hello innych `using` instrukcje.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Zastąp bieżący hello `public ActionResult Index()` implementacji metody z powitania po implementacji.

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


1. Dodaj następujące trzy metody toohello hello `TeamsController` hello tooimplement klasy `playGames`, `clearCache`, i `rebuildDB` typów akcji z hello switch — instrukcja dodane w hello poprzedniego fragmentu kodu.
   
    Witaj `PlayGames` metody aktualizuje statystyki zespołu hello symulując sezonu gier, zapisuje hello bazy danych z wynikami toohello i czyści hello teraz przestarzałe dane z pamięci podręcznej hello.

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

    Witaj `RebuildDB` bazy danych hello ponowne metody z hello domyślny zestaw zespołów, generuje statystyki dla nich i czyści hello teraz przestarzałe dane z pamięci podręcznej hello.

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

    Witaj `ClearCachedTeams` metoda usuwa żadnych statystyk zespołu pamięci podręcznej z pamięci podręcznej hello.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Dodaj następujące cztery metody toohello hello `TeamsController` klasy tooimplement hello różne sposoby pobierania statystyki zespołu hello z pamięci podręcznej hello i hello bazy danych. Każda z tych metod zwraca `List<Team>` wyświetlone w widoku hello.
   
    Witaj `GetFromDB` — metoda odczytuje statystyki zespołu hello z hello bazy danych.
   
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

    Witaj `GetFromList` metoda odczytuje statystyki zespołu hello z pamięci podręcznej jako serializacji `List<Team>`. W przypadku Chybienie pamięci podręcznej, hello zespołu statystyki są odczytana z bazy danych hello i następnie przechowywane w pamięci podręcznej hello następnym razem. W tym przykładzie używamy JSON.NET serializacji tooserialize hello .NET obiektów tooand z pamięci podręcznej hello. Aby uzyskać więcej informacji, zobacz [jak toowork z platformą .NET obiektów w pamięci podręcznej Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

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

    Witaj `GetFromSortedSet` metoda odczytuje statystyki zespołu hello z pamięci podręcznej zestawu posortowane. W przypadku Chybienie pamięci podręcznej, hello zespołu statystyki są odczytana z bazy danych hello i przechowywane w pamięci podręcznej hello jako zestaw posortowane.

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

    Witaj `GetFromSortedSetTop5` — metoda odczytuje hello top zespoły 5 z pamięci podręcznej hello sortowane zestawu. Rozpocznie się sprawdzanie pamięci podręcznej hello hello istnienia hello `teamsSortedSet` klucza. Jeśli ten klucz nie jest obecny, hello `GetFromSortedSet` — metoda jest wywoływana tooread hello zespołu statystyk i zapisanie ich w pamięci podręcznej hello. Następnie hello pamięci podręcznej zestawu posortowane zostanie zapytany o hello top 5 zespołów, które są zwracane.

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

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Zaktualizuj hello tworzenia, edycji i usunąć toowork metody z pamięci podręcznej hello
Hello szkieletów kodu, który został wygenerowany jako część ten przykład zawiera metody tooadd, edytować lub usuwać zespołów. W dowolnym momencie zespołu dodać, edytować lub usunąć, hello danych w pamięci podręcznej hello staje się nieaktualne. W tej sekcji, które będzie modyfikować tych trzech metod tooclear hello buforowany zespołów, dzięki czemu hello pamięci podręcznej nie będzie zsynchronizowany z hello bazy danych.

1. Przeglądaj toohello `Create(Team team)` w hello metody `TeamsController` klasy. Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.

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


1. Przeglądaj toohello `Edit(Team team)` w hello metody `TeamsController` klasy. Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.

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


1. Przeglądaj toohello `DeleteConfirmed(int id)` w hello metody `TeamsController` klasy. Dodaj toohello wywołania `ClearCachedTeams` metody, jak pokazano w hello poniższy przykład.

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


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Zaktualizuj toowork widoku indeksu zespoły hello z pamięci podręcznej hello
1. W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, a następnie hello **zespołów** folder, a następnie kliknij dwukrotnie **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. U góry hello pliku hello poszukaj hello następującego elementu akapitu.
   
    ![Tabela akcji][cache-teams-index-table]
   
    Jest to toocreate łącze hello nowego zespołu. Zastąp element akapitu hello hello w poniższej tabeli. Ta tabela ma łącza akcji do tworzenia nowego zespołu odtwarzanie nowego sezonu gier, czyszczenie pamięci podręcznej hello, pobierania zespoły hello z pamięci podręcznej hello w wielu formatach, pobieranie zespoły hello z hello bazy danych i ponownie skompilować hello bazy danych z nową próbkę danych.

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


1. Przewiń w dół toohello hello **Index.cshtml** i dodaj następujące hello `tr` element, aby była hello ostatni wiersz w hello ostatniej tabeli w pliku hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Ten wiersz zawiera wartość hello `ViewBag.Msg` zawierającą raport o hello bieżącej operacji. Witaj `ViewBag.Msg` jest ustawiona, po kliknięciu dowolnej łącza akcji hello hello w poprzednim kroku.   
   
    ![Komunikat o stanie][cache-status-message]
2. Naciśnij klawisz **F6** toobuild hello projektu.

## <a name="provision-hello-azure-resources"></a>Zainicjuj obsługę hello zasobów platformy Azure
toohost aplikacji na platformie Azure, należy najpierw umożliwić hello usług platformy Azure wymagane przez aplikację. Witaj przykładowej aplikacji w tym samouczku używa hello następujących usług platformy Azure.

* Azure Redis Cache
* Aplikacja sieci Web usługi App Service
* SQL Database

toodeploy tych usług tooa nowy lub istniejący zasób grupy wybranych przez użytkownika, kliknij przycisk powitania po **wdrażanie tooAzure** przycisku.

[! [Wdrażanie tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

To **wdrażanie tooAzure** przycisk używa hello [tworzenie aplikacji sieci Web oraz pamięci podręcznej Redis oraz bazy danych SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) tooprovision szablonu tych usług i hello zestawu Parametry połączenia dla hello bazy danych SQL i hello ustawienie aplikacji hello parametry połączenia z pamięcią podręczną Redis Azure.

> [!NOTE]
> Jeśli nie masz konta platformy Azure, możesz [utworzyć bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) w zaledwie kilka minut.
> 
> 

Kliknięcie przycisku hello **wdrażanie tooAzure** przycisk przyjmuje toohello portalu Azure i inicjuje hello proces tworzenia zasobów hello opisanego przez hello szablonu.

![Wdrażanie tooAzure][cache-deploy-to-azure-step-1]

1. W hello **podstawy** sekcji, wybierz hello toouse subskrypcji platformy Azure, wybierz istniejącą grupę zasobów lub Utwórz nowy i określ lokalizacja grupy zasobów hello.
2. W hello **ustawienia** określ **logowania administratora** (nie należy używać **admin**), **hasło logowania administratora**i  **Nazwa bazy danych**. Hello inne parametry są konfigurowane pod kątem wolnego aplikacji usługi hostingu planu i tanie opcji hello bazy danych SQL i pamięcią podręczną Redis Azure, które nie pochodzą z warstwę bezpłatna.

    ![Wdrażanie tooAzure][cache-deploy-to-azure-step-2]

3. Po skonfigurowaniu ustawień hello potrzebne, przewiń koniec toohello hello strony, hello przeczytaj warunki i postanowienia, a następnie sprawdź hello **zgadzam się toohello warunki i postanowienia, o których wspomniano** wyboru.
4. Kliknij toobegin inicjowania obsługi administracyjnej zasobów hello, **zakupu**.

postęp hello tooview wdrożenia, kliknij ikonę powiadomienia hello i kliknij przycisk **rozpoczęto wdrażanie**.

![Wdrażanie rozpoczęte][cache-deployment-started]

Można wyświetlić stan hello wdrożenia na powitania **Microsoft.Template** bloku.

![Wdrażanie tooAzure][cache-deploy-to-azure-step-3]

Po zakończeniu inicjowania obsługi można opublikować tooAzure Twojej aplikacji w programie Visual Studio.

> [!NOTE]
> Wszelkie błędy, które mogą wystąpić podczas procesu udostępniania hello są wyświetlane na powitania **Microsoft.Template** bloku. Typowe błędy polegają na tym, że jest za dużo serwerów SQL Server lub za dużo planów hostowania Usługi aplikacji w warstwie Bezpłatna na subskrypcję. Usuń wszelkie błędy i ponownie uruchomić proces hello klikając **ponownie wdrożyć** na powitania **Microsoft.Template** bloku lub hello **wdrażanie tooAzure** przycisku w tym samouczku.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Publikowanie tooAzure aplikacji hello
W tym kroku samouczka hello możesz opublikować tooAzure aplikacji hello i uruchomić go w chmurze hello.

1. Kliknij prawym przyciskiem myszy hello **ContosoTeamStats** projekt w programie Visual Studio i wybierz pozycję **publikowania**.
   
    ![Publikowanie][cache-publish-app]
2. Kliknij przycisk **Usługa aplikacji Microsoft Azure**, wybierz pozycję **Wybierz istniejące**i kliknij przycisk **Opublikuj**.
   
    ![Publikowanie][cache-publish-to-app-service]
3. Wybierz subskrypcję hello używany podczas tworzenia hello zasobów platformy Azure, rozwiń grupę zasobów hello zawierającego zasoby hello i wybierz hello potrzeby aplikacji sieci Web. Jeśli używasz hello **wdrażanie tooAzure** przycisk nazwę aplikacji sieci Web, który rozpoczyna się od **witryny sieci Web** następuje niektóre dodatkowe znaki.
   
    ![Wybieranie aplikacji sieci Web][cache-select-web-app]
4. Kliknij przycisk **OK** hello toobegin procesu publikowania. Po kilku chwilach kończy hello procesu publikowania i przeglądarką jest uruchamiana z systemem Przykładowa aplikacja hello. Jeśli wyświetlony komunikat o błędzie DNS podczas sprawdzania poprawności lub publikowania i hello procesu dla udostępniania hello zasobów Azure dla aplikacji hello zostało niedawno ukończone, zaczekaj chwilę i spróbuj ponownie.
   
    ![Dodano pamięć podręczną][cache-added-to-application]

Witaj poniższej tabeli opisano każdego łącza akcji z hello przykładowej aplikacji.

| Akcja | Opis |
| --- | --- |
| Create New (Utwórz nowe) |Tworzenie nowego zespołu. |
| Play Season (Odtwarzaj sezon) |Odtwarzanie sezonu gier, Statystyka zespołu hello aktualizacji, i wyczyść nieaktualne żadnego zespołu danych z pamięci podręcznej hello. |
| Clear Cache (Wyczyść pamięć podręczną) |Statystyka zespołu hello Wyczyść z pamięci podręcznej hello. |
| List from Cache (Lista z pamięci podręcznej) |Pobierz Statystyka zespołu hello z pamięci podręcznej hello. W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej dla następnym razem. |
| Sorted Set from Cache (Zestaw posortowany z pamięci podręcznej) |Pobierz Statystyka zespołu hello z hello pamięci podręcznej przy użyciu zestawu posortowane. W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej przy użyciu zestawu posortowane. |
| Top 5 Teams from Cache (5 najlepszych zespołów z pamięci podręcznej) |Pobrać górnego zespoły 5 hello z pamięci podręcznej hello przy użyciu zestawu posortowane. W przypadku Chybienie pamięci podręcznej, załadować Statystyka hello z hello bazy danych i Zapisz toohello pamięci podręcznej przy użyciu zestawu posortowane. |
| Load from DB (Ładuj z bazy danych) |Statystyka zespołu hello należy pobrać hello bazy danych. |
| Rebuild DB (Odbuduj bazę danych) |Odbuduj hello bazy danych i załadować go ponownie z przykładowymi danymi zespołu. |
| Edytuj / Szczegóły / Usuń |Edytowanie zespołu, wyświetlanie szczegółów dla zespołu, usuwanie zespołu. |

Niektóre akcje powitania kliknij i eksperymentować pobieranie hello danych z różnych źródeł hello. Nie hello różnice w hello czas toocomplete hello różne sposoby pobierania hello danych z bazy danych hello i hello pamięci podręcznej.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Witaj zasoby zostaną usunięte po zakończeniu pracy z aplikacją hello
Po zakończeniu hello przykładowej samouczek aplikacji hello Azure można usunąć zasoby używane w kolejności tooconserve koszt i zasoby. Jeśli używasz hello **wdrażanie tooAzure** przycisku na powitania [udostępniania hello zasobów platformy Azure](#provision-the-azure-resources) sekcji i wszystkich zasobów objętych hello tej samej grupie zasobów, można je usunąć razem w jednym Operacja przez usunięcie hello grupy zasobów.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **grup zasobów**.
2. Typ hello nazwę grupy zasobów do hello **filtrować elementy...**  pola tekstowego.
3. Kliknij przycisk **...**  toohello prawo do swojej grupy zasobów.
4. Kliknij polecenie **Usuń**.
   
    ![Usuwanie][cache-delete-resource-group]
5. Typ hello nazwy grupy zasobów i kliknij przycisk **usunąć**.
   
    ![Potwierdzenie usunięcia][cache-delete-confirm]

Po kilku chwilach hello zasobów grupy i wszystkich zawartych w niej zasobów zostaną usunięte.

> [!IMPORTANT]
> Należy pamiętać, że usunięcie grupy zasobów jest nieodwracalna i że hello grupy zasobów i wszystkie zasoby hello w nim zostaną trwale usunięte. Upewnij się, że nie zostaną przypadkowo usunięte grupy zasobów niewłaściwy hello lub zasobów. Jeśli utworzono hello zasobów dla hostingu w tym przykładzie wewnątrz istniejącą grupę zasobów, możesz usunąć każdego zasobu indywidualnie z ich odpowiednich bloków.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Uruchom hello przykładowej aplikacji na komputerze lokalnym
Aplikacja hello toorun lokalnie na komputerze, należy pamięć podręczna Redis Azure wystąpienia, w których toocache danych. 

* Po opublikowaniu tooAzure Twojej aplikacji zgodnie z opisem w poprzedniej sekcji hello, możesz użyć wystąpienia pamięci podręcznej Redis Azure hello, udostępniony w tym kroku.
* Jeśli masz inne istniejące wystąpienie pamięci podręcznej Redis Azure możesz użyć tego toorun tego przykładu lokalnie.
* Jeśli potrzebujesz toocreate wystąpienia pamięci podręcznej Redis Azure, można wykonać kroki hello w [tworzenia pamięci podręcznej](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Po wybraniu lub utworzyć toouse pamięci podręcznej hello Przeglądaj toohello pamięci podręcznej w hello portalu Azure i pobrać hello [nazwy hosta](cache-configure.md#properties) i [klucze dostępu](cache-configure.md#access-keys) dla pamięci podręcznej. Instrukcje znajdują się w artykule [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings) (Konfigurowanie ustawień pamięci podręcznej Redis).

1. Otwórz hello `WebAppPlusCacheAppSecrets.config` pliku utworzonego podczas hello [skonfigurować toouse aplikacji hello pamięci podręcznej Redis](#configure-the-application-to-use-redis-cache) kroku w tym samouczku za pomocą dowolnego edytora hello.
2. Edytuj hello `value` atrybutu i Zastąp `MyCache.redis.cache.windows.net` z hello [nazwy hosta](cache-configure.md#properties) z pamięci podręcznej i określ albo hello [klucz podstawowy lub pomocniczy](cache-configure.md#access-keys) z pamięci podręcznej jako hello hasła.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Naciśnij klawisz **Ctrl + F5** toorun hello aplikacji.

> [!NOTE]
> Należy pamiętać, że ponieważ aplikacji hello, w tym hello bazy danych, jest uruchomiony lokalnie i hello pamięci podręcznej Redis jest hostowana na platformie Azure, hello pamięci podręcznej może pojawić się toounder — wykonaj hello bazy danych. Aby uzyskać najlepszą wydajność, hello aplikacji klienckiej, a wystąpienia pamięci podręcznej Redis Azure powinny być hello tej samej lokalizacji. 
> 
> 

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [wprowadzenie do platformy ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) na powitania [ASP.NET](http://asp.net/) lokacji.
* Więcej przykładów dotyczących tworzenia aplikacji sieci Web platformy ASP.NET w usłudze App Service, zobacz [tworzenie i wdrażanie aplikacji sieci web platformy ASP.NET w usłudze Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) z hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [pokaz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Przewodniki Szybki Start więcej z hello HealthClinic.biz demonstracyjnej, aby zapoznać [Przewodniki Szybki Start Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Dowiedz się więcej o hello [kod pierwszego tooa nową bazę danych](https://msdn.microsoft.com/data/jj193542) podejścia tooEntity strukturę, która jest używana w tym samouczku.
* Dowiedz się więcej na temat [aplikacji sieci Web w Usłudze aplikacji Azure](../app-service-web/app-service-web-overview.md).
* Dowiedz się, jak za[monitor](cache-how-to-monitor.md) pamięci podręcznej w hello portalu Azure.
* Poznaj funkcje Premium usługi Azure Redis Cache
  
  * [Jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md)
  * [Jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md)
  * [Jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md)
  * Zobacz hello [często zadawane pytania pamięci podręcznej Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) szczegółowe informacje o rozmiarze, przepływności i przepustowości z pamięci podręcznych premium.

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

