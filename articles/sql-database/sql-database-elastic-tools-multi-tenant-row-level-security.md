---
title: "aaaMulti dzierżawy aplikacji za pomocą narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza"
description: "Dowiedz się, jak toouse narzędzi elastycznej bazy danych wraz z poziomu wiersza toobuild zabezpieczeń aplikacji z warstwą skalowalnej danych w bazie danych SQL Azure obsługującym odłamków wielodostępnej."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza
[Narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md) i [zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131) oferują zaawansowany zestaw możliwości elastyczne i wydajne skalowanie warstwy danych hello wielodostępnych aplikacji z bazy danych SQL Azure. Zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) Aby uzyskać więcej informacji. 

W tym artykule przedstawiono sposób toouse te technologie toobuild razem z warstwą danych skalowalnej obsługuje wielodostępne odłamków, przy użyciu aplikacji **ADO.NET SqlClient** i/lub **programu Entity Framework**.  

* **Narzędzi elastycznej bazy danych** umożliwia deweloperom tooscale limit hello warstwy danych aplikacji za pośrednictwem standardowych dzielenia na fragmenty rozwiązania przy użyciu zestawu .NET bibliotek i szablony usługi Azure. Zarządzanie odłamków przy użyciu hello elastycznej bazy danych klienta biblioteki pomaga zautomatyzować i uprościć wielu zadań infrastrukturalne hello zwykle skojarzone z dzielenia na fragmenty. 
* **Wiersz poziomu zabezpieczeń** umożliwia deweloperom toostore danych dla wielu dzierżawców w hello sama baza danych przy użyciu toofilter zasady zabezpieczeń limit wierszy, które nie należą dzierżawy toohello wykonywanie zapytania. Scentralizowany dostęp logiki odświeżania wewnątrz hello bazy danych, a nie niż w aplikacji hello upraszcza konserwację i zmniejsza ryzyko hello błąd kodu aplikacji rozwoju. 

Korzystanie z tych funkcji ze sobą, aplikacji mogą korzystać z koszt zyski oszczędności i wydajności, dane są przechowywane dla wielu dzierżawy w hello sam identyfikator niezależnego fragmentu bazy danych. Na powitania tym samym czasie, aplikacja nadal ma toooffer elastyczność hello odizolowane pojedynczego dzierżawcy fragmentów dla dzierżawcy "premium", którzy wymagają bardziej rygorystyczne gwarancji wydajności, ponieważ odłamków wielodostępne gwarantuje dystrybucji równy zasobów między dzierżawcami.  

Krótko mówiąc, hello biblioteki klienta elastycznej bazy danych [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) interfejsów API automatyczne łączenie z dzierżawcami toohello poprawny identyfikator niezależnego fragmentu bazy danych zawierającej klucz dzielenia na fragmenty (zazwyczaj "TenantId"). Po nawiązaniu połączenia zasady zabezpieczeń zabezpieczenia na poziomie wiersza w bazie danych hello zapewnia, że dzierżawców można tylko dostęp do wierszy zawierających ich identyfikatora dzierżawcy. Zakłada się, że wszystkie tabele zawierają wiersze, które należy dzierżawy tooeach tooindicate kolumny identyfikatora dzierżawcy. 

![Architektura aplikacji obsługi blogów][1]

## <a name="download-hello-sample-project"></a>Pobierz hello przykładowy projekt
### <a name="prerequisites"></a>Wymagania wstępne
* Za pomocą programu Visual Studio (2012 lub nowszy) 
* Utwórz trzy bazy danych SQL Azure 
* Pobierz przykładowy projekt: [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - odłamków wielodostępne](http://go.microsoft.com/?linkid=9888163)
  * Wprowadź informacje powitania dla baz danych na początku hello **Program.cs** 

Ten projekt rozszerza hello, co opisano w [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - Entity Framework integracji](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) przez dodanie obsługi wielodostępne niezależnego fragmentu bazy danych. Tworzenia prostej aplikacji konsolowej do tworzenia blogów i wpisów, z czterech dzierżawców i dwóch niezależnych wielodostępnych baz danych zgodnie z opisami w hello powyżej diagramu. 

Tworzenie i uruchamianie aplikacji hello. Spowoduje to bootstrap narzędzi elastycznej bazy danych hello Menedżera mapy niezależnego fragmentu i wykonywania hello następujące testy: 

1. Przy użyciu programu Entity Framework i LINQ, Utwórz nowy blog, a następnie Wyświetl wszystkie blogi dla każdego dzierżawcy
2. Za pomocą ADO.NET SqlClient, wyświetlić wszystkie blogi dla dzierżawy
3. Spróbuj tooinsert blogu dla tooverify niewłaściwy dzierżawy hello, który jest zgłaszany błąd  

Powiadomienie, że ponieważ zabezpieczenia na poziomie wiersza nie została jeszcze włączona w bazach danych niezależnych hello, tych testów ujawnia problem: dzierżaw są możliwe toosee blogów, które nie należą toothem i aplikacji hello nie uniemożliwia wstawianie blogu hello niewłaściwy dzierżawcy. Witaj dalszej części tego artykułu opisano sposób tooresolve tych problemów, wymuszając dzierżawy izolacji odświeżania. Istnieją dwa kroki: 

1. **Warstwy aplikacji**: Zmodyfikuj kod aplikacji hello zestaw tooalways hello bieżącego identyfikatora dzierżawcy w hello SESSION_CONTEXT po otwarciu połączenia. Witaj przykładowy projekt zawiera już zostało to zrobione. 
2. **Warstwa danych**: Tworzenie zasad zabezpieczeń zabezpieczenia na poziomie wiersza w każdym toofilter bazy danych niezależnych wierszy oparty na powitania TenantId przechowywane w SESSION_CONTEXT. Będzie on potrzebny toodo dla każdego niezależnego fragmentu baz danych, w przeciwnym razie wierszy w wielodostępnym odłamków nie będą filtrowane. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Warstwy aplikacji w kroku 1): Ustaw identyfikatora dzierżawcy w hello SESSION_CONTEXT
Po łączącego tooa niezależnego fragmentu bazy danych przy użyciu danych biblioteki hello elastycznej bazy danych klienta, które nadal zależnych API routingu aplikacji hello wymaga bazy danych hello tootell TenantId, który jest za pomocą tego połączenia, dzięki czemu zabezpieczenia na poziomie wiersza zasady zabezpieczeń można odfiltrować wierszy przynależność tooother dzierżawcy. Witaj toopass zalecany sposób te informacje są toostore hello bieżącego identyfikatora dzierżawcy dla tego połączenia w hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Uwaga: Możesz też użyć [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ale SESSION_CONTEXT jest lepszym rozwiązaniem, ponieważ jest łatwiejsze toouse, zwraca wartość NULL, domyślnie i obsługuje pary klucz wartość.)

### <a name="entity-framework"></a>Entity Framework
W przypadku aplikacji przy użyciu programu Entity Framework najłatwiejszy hello jest hello tooset SESSION_CONTEXT w hello ElasticScaleContext zastąpienia opisane w [danych zależnych routingu przy użyciu EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Przed zwróceniem połączenia hello przeprowadzana za pośrednictwem danych zależnych routingu, tworzenie i wykonywanie SqlCommand, która ustawia "TenantId" w shardingKey toohello SESSION_CONTEXT hello określony dla tego połączenia. Dzięki temu wystarczy toowrite kod po tooset hello SESSION_CONTEXT. 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

Teraz automatycznie ustawiono hello SESSION_CONTEXT hello określony dla identyfikatora dzierżawcy przy każdym wywołaniu ElasticScaleContext: 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
Dla aplikacji za pomocą ADO.NET SqlClient hello zalecane podejście jest toocreate funkcji otoki wokół ShardMap.OpenConnectionForKey() automatycznie ustawiający "TenantId" w hello SESSION_CONTEXT toohello Popraw TenantId przed zwróceniem połączenie. tooensure SESSION_CONTEXT zawsze ustawiona, należy otworzyć tylko połączeń za pomocą tej funkcji otoki.

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Warstwa danych kroku 2): Tworzenie zasad zabezpieczeń na poziomie wiersza
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Utwórz wiersze, które mogą uzyskiwać dostęp do każdego dzierżawcy hello toofilter zasad zabezpieczeń
Teraz, gdy aplikacja hello ustawia SESSION_CONTEXT z bieżącego identyfikatora dzierżawcy hello przed wykonaniem kwerendy, zabezpieczenia na poziomie wiersza zasady zabezpieczeń można filtrować zapytania i wykluczyć wiersze, które mają różne identyfikatora dzierżawcy.  

Kontrola dostępu jest zaimplementowana w T-SQL: hello logika dostępu definiuje funkcję zdefiniowaną przez użytkownika, i zasady zabezpieczeń wiąże funkcja ta tooany liczbę tabel. Dla tego projektu funkcja hello po prostu Sprawdź, czy hello aplikacji (zamiast innego użytkownika SQL) jest połączonych toohello bazy danych, i że Witaj, "TenantId" przechowywany w hello SESSION_CONTEXT odpowiada hello TenantId danego wiersza. Predykat filtru umożliwi wiersze spełniające te warunki toopass za pośrednictwem hello filtr dla zapytania SELECT, UPDATE i DELETE; i zapobiega wiersze, które naruszają te warunki przed wstawione lub zaktualizowane predykat bloku. Jeśli nie ustawiono SESSION_CONTEXT, zwróci wartość NULL i nie wierszy będą toobe widoczny, czy można wstawić. 

tooenable zabezpieczenia na poziomie wiersza, wykonanie powitania po T-SQL na wszystkich odłamków przy użyciu albo program Visual Studio (SSDT), SSMS, lub hello skrypt programu PowerShell dołączony hello projektu (lub jeśli używasz [zadania elastyczne bazy danych](sql-database-elastic-jobs-overview.md), można użyć tooautomate wykonywania z tym T-SQL na wszystkich odłamków): 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> Bardziej złożone projektów wymagające tooadd hello predykatu w setki tabel można użyć pomocnika przechowywane procedury, która automatycznie generuje zasady zabezpieczeń, dodawanie predykat dla wszystkich tabel w schemacie. Zobacz [zastosowania zabezpieczeń na poziomie wiersza tooall tabel - pomocnika skryptu (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Teraz po uruchomieniu aplikacji przykładowej hello ponownie dzierżawcy będzie toosee stanie tylko wiersze, które należy toothem. Ponadto aplikacji hello nie można wstawić wierszy, do których należą tootenants innej niż baza danych niezależnych jeden toohello aktualnie połączonych hello i nie można zaktualizować toohave widocznych wierszy innego identyfikatora dzierżawcy. Jeśli aplikacja hello albo prób toodo, DbUpdateException zostanie wygenerowany.

Jeśli później Dodaj nową tabelę po prostu ALTER hello zasady zabezpieczeń i dodać predykatów filtru i bloku je na powitania nową tabelę: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Dodaj domyślną tooautomatically ograniczenia wypełnić TenantId dla operacji wstawienia
Możesz też zaznaczyć domyślny ograniczenie dla każdej tabeli tooautomatically wypełnić hello identyfikatora dzierżawcy z hello wartości przechowywanych obecnie we SESSION_CONTEXT podczas wstawiania wierszy. Na przykład: 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

Teraz aplikacji hello nie jest konieczne toospecify TenantId podczas wstawiania wierszy: 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> Jeśli używasz domyślne ograniczenia dla projektu programu Entity Framework, zaleca się, że nie zawierają hello TenantId kolumny w modelu danych EF. Jest to spowodowane zapytania programu Entity Framework automatyczne określanie wartości domyślnych, które zastąpią domyślne hello ograniczenia utworzone w T-SQL, korzystających z SESSION_CONTEXT. toouse domyślne ograniczenia w hello przykładowe projektu, na przykład TenantId należy usunąć z DataClasses.cs (i wykonywania Add-Migration hello Konsola Menedżera pakietów) i istnieje tylko w tabelach bazy danych hello tooensure Użyj T-SQL, który hello pola. W ten sposób EF nie automatycznie dostarcza niepoprawne wartości domyślne podczas wstawiania danych. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Opcjonalnie) Włącz tooaccess "administratora" wszystkie wiersze
Niektóre aplikacje mogą być toocreate "administratora" kto ma dostęp do wszystkich wierszy, na przykład w kolejności tooenable raportowania przez wszystkich dzierżawców na wszystkich odłamków lub tooperform podziału/Merge operacje na odłamków obejmujących przenoszenie wierszy dzierżawy między bazami danych. tooenable, należy utworzyć nowego użytkownika SQL ("superuser" w tym przykładzie) w każdym niezależnego fragmentu bazy danych. Następnie zmienić zasady zabezpieczeń hello z nową funkcję predykatu, która umożliwia tym tooaccess użytkownika wszystkie wiersze:

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a>Konserwacji
* **Dodawanie nowych odłamków**: tooenable skryptu T-SQL hello zabezpieczenia na poziomie wiersza musi być wykonywany na wszelkich nowych fragmentów, w przeciwnym razie kwerendy dotyczące tych fragmentów nie będą filtrowane.
* **Dodawanie nowych tabel**: należy dodać filtr i zablokować toohello predykatu zabezpieczeń zasady na wszystkich odłamków zawsze, gdy nowa tabela została utworzona, w przeciwnym razie zapytań w nowej tabeli hello nie będą filtrowane. Ten można zautomatyzować za pomocą wyzwalacza DDL, zgodnie z opisem w [zastosowania zabezpieczeń na poziomie wiersza toonewly tworzone tabele (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Podsumowanie
Narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza mogą być używane razem tooscale limit aplikacji warstwy danych o obsługę zarówno wielodostępnej i jednym dzierżawcy fragmentów. Wielodostępne odłamków może być toostore używanych danych wydajniej (szczególnie w przypadkach, gdy mają tylko kilka wierszy danych w dużej liczby dzierżawców), podczas jednego dzierżawcy fragmentów mogą być używane toosupport premium dzierżawców z bardziej rygorystyczne wydajności i izolacji wymagania.  Aby uzyskać więcej informacji, zobacz [informacje dotyczące zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Co to jest puli elastycznej platformy Azure?](sql-database-elastic-pool.md)
* [Scaling out with Azure SQL Database (Skalowanie w poziomie za pomocą usługi Azure SQL Database)](sql-database-elastic-scale-introduction.md)
* [Wzorce projektowe dla wielodostępnych aplikacji SaaS wykorzystujących usługę Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Uwierzytelnianie w aplikacjach wielodostępnych za pomocą usługi Azure AD i OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplikacja Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Pytania i żądania funkcji
Odpowiedzi na pytania, proszę dotrzeć toous na powitania [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je toohello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


