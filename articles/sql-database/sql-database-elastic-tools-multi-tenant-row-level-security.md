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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="57f9e-103">Aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="57f9e-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="57f9e-104">[Narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md) i [zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131) oferują zaawansowany zestaw możliwości elastyczne i wydajne skalowanie warstwy danych hello wielodostępnych aplikacji z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="57f9e-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="57f9e-105">Zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="57f9e-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="57f9e-106">W tym artykule przedstawiono sposób toouse te technologie toobuild razem z warstwą danych skalowalnej obsługuje wielodostępne odłamków, przy użyciu aplikacji **ADO.NET SqlClient** i/lub **programu Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="57f9e-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="57f9e-107">**Narzędzi elastycznej bazy danych** umożliwia deweloperom tooscale limit hello warstwy danych aplikacji za pośrednictwem standardowych dzielenia na fragmenty rozwiązania przy użyciu zestawu .NET bibliotek i szablony usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="57f9e-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="57f9e-108">Zarządzanie odłamków przy użyciu hello elastycznej bazy danych klienta biblioteki pomaga zautomatyzować i uprościć wielu zadań infrastrukturalne hello zwykle skojarzone z dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="57f9e-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="57f9e-109">**Wiersz poziomu zabezpieczeń** umożliwia deweloperom toostore danych dla wielu dzierżawców w hello sama baza danych przy użyciu toofilter zasady zabezpieczeń limit wierszy, które nie należą dzierżawy toohello wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="57f9e-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="57f9e-110">Scentralizowany dostęp logiki odświeżania wewnątrz hello bazy danych, a nie niż w aplikacji hello upraszcza konserwację i zmniejsza ryzyko hello błąd kodu aplikacji rozwoju.</span><span class="sxs-lookup"><span data-stu-id="57f9e-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="57f9e-111">Korzystanie z tych funkcji ze sobą, aplikacji mogą korzystać z koszt zyski oszczędności i wydajności, dane są przechowywane dla wielu dzierżawy w hello sam identyfikator niezależnego fragmentu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="57f9e-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="57f9e-112">Na powitania tym samym czasie, aplikacja nadal ma toooffer elastyczność hello odizolowane pojedynczego dzierżawcy fragmentów dla dzierżawcy "premium", którzy wymagają bardziej rygorystyczne gwarancji wydajności, ponieważ odłamków wielodostępne gwarantuje dystrybucji równy zasobów między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="57f9e-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="57f9e-113">Krótko mówiąc, hello biblioteki klienta elastycznej bazy danych [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) interfejsów API automatyczne łączenie z dzierżawcami toohello poprawny identyfikator niezależnego fragmentu bazy danych zawierającej klucz dzielenia na fragmenty (zazwyczaj "TenantId").</span><span class="sxs-lookup"><span data-stu-id="57f9e-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="57f9e-114">Po nawiązaniu połączenia zasady zabezpieczeń zabezpieczenia na poziomie wiersza w bazie danych hello zapewnia, że dzierżawców można tylko dostęp do wierszy zawierających ich identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="57f9e-115">Zakłada się, że wszystkie tabele zawierają wiersze, które należy dzierżawy tooeach tooindicate kolumny identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Architektura aplikacji obsługi blogów][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="57f9e-117">Pobierz hello przykładowy projekt</span><span class="sxs-lookup"><span data-stu-id="57f9e-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="57f9e-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="57f9e-118">Prerequisites</span></span>
* <span data-ttu-id="57f9e-119">Za pomocą programu Visual Studio (2012 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="57f9e-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="57f9e-120">Utwórz trzy bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="57f9e-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="57f9e-121">Pobierz przykładowy projekt: [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - odłamków wielodostępne](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="57f9e-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="57f9e-122">Wprowadź informacje powitania dla baz danych na początku hello **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="57f9e-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="57f9e-123">Ten projekt rozszerza hello, co opisano w [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - Entity Framework integracji](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) przez dodanie obsługi wielodostępne niezależnego fragmentu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="57f9e-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="57f9e-124">Tworzenia prostej aplikacji konsolowej do tworzenia blogów i wpisów, z czterech dzierżawców i dwóch niezależnych wielodostępnych baz danych zgodnie z opisami w hello powyżej diagramu.</span><span class="sxs-lookup"><span data-stu-id="57f9e-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="57f9e-125">Tworzenie i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="57f9e-125">Build and run hello application.</span></span> <span data-ttu-id="57f9e-126">Spowoduje to bootstrap narzędzi elastycznej bazy danych hello Menedżera mapy niezależnego fragmentu i wykonywania hello następujące testy:</span><span class="sxs-lookup"><span data-stu-id="57f9e-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="57f9e-127">Przy użyciu programu Entity Framework i LINQ, Utwórz nowy blog, a następnie Wyświetl wszystkie blogi dla każdego dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="57f9e-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="57f9e-128">Za pomocą ADO.NET SqlClient, wyświetlić wszystkie blogi dla dzierżawy</span><span class="sxs-lookup"><span data-stu-id="57f9e-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="57f9e-129">Spróbuj tooinsert blogu dla tooverify niewłaściwy dzierżawy hello, który jest zgłaszany błąd</span><span class="sxs-lookup"><span data-stu-id="57f9e-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="57f9e-130">Powiadomienie, że ponieważ zabezpieczenia na poziomie wiersza nie została jeszcze włączona w bazach danych niezależnych hello, tych testów ujawnia problem: dzierżaw są możliwe toosee blogów, które nie należą toothem i aplikacji hello nie uniemożliwia wstawianie blogu hello niewłaściwy dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="57f9e-131">Witaj dalszej części tego artykułu opisano sposób tooresolve tych problemów, wymuszając dzierżawy izolacji odświeżania.</span><span class="sxs-lookup"><span data-stu-id="57f9e-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="57f9e-132">Istnieją dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="57f9e-132">There are two steps:</span></span> 

1. <span data-ttu-id="57f9e-133">**Warstwy aplikacji**: Zmodyfikuj kod aplikacji hello zestaw tooalways hello bieżącego identyfikatora dzierżawcy w hello SESSION_CONTEXT po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="57f9e-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="57f9e-134">Witaj przykładowy projekt zawiera już zostało to zrobione.</span><span class="sxs-lookup"><span data-stu-id="57f9e-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="57f9e-135">**Warstwa danych**: Tworzenie zasad zabezpieczeń zabezpieczenia na poziomie wiersza w każdym toofilter bazy danych niezależnych wierszy oparty na powitania TenantId przechowywane w SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="57f9e-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="57f9e-136">Będzie on potrzebny toodo dla każdego niezależnego fragmentu baz danych, w przeciwnym razie wierszy w wielodostępnym odłamków nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="57f9e-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="57f9e-137">Warstwy aplikacji w kroku 1): Ustaw identyfikatora dzierżawcy w hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="57f9e-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="57f9e-138">Po łączącego tooa niezależnego fragmentu bazy danych przy użyciu danych biblioteki hello elastycznej bazy danych klienta, które nadal zależnych API routingu aplikacji hello wymaga bazy danych hello tootell TenantId, który jest za pomocą tego połączenia, dzięki czemu zabezpieczenia na poziomie wiersza zasady zabezpieczeń można odfiltrować wierszy przynależność tooother dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="57f9e-139">Witaj toopass zalecany sposób te informacje są toostore hello bieżącego identyfikatora dzierżawcy dla tego połączenia w hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f9e-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="57f9e-140">(Uwaga: Możesz też użyć [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ale SESSION_CONTEXT jest lepszym rozwiązaniem, ponieważ jest łatwiejsze toouse, zwraca wartość NULL, domyślnie i obsługuje pary klucz wartość.)</span><span class="sxs-lookup"><span data-stu-id="57f9e-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="57f9e-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="57f9e-141">Entity Framework</span></span>
<span data-ttu-id="57f9e-142">W przypadku aplikacji przy użyciu programu Entity Framework najłatwiejszy hello jest hello tooset SESSION_CONTEXT w hello ElasticScaleContext zastąpienia opisane w [danych zależnych routingu przy użyciu EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="57f9e-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="57f9e-143">Przed zwróceniem połączenia hello przeprowadzana za pośrednictwem danych zależnych routingu, tworzenie i wykonywanie SqlCommand, która ustawia "TenantId" w shardingKey toohello SESSION_CONTEXT hello określony dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="57f9e-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="57f9e-144">Dzięki temu wystarczy toowrite kod po tooset hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="57f9e-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

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

<span data-ttu-id="57f9e-145">Teraz automatycznie ustawiono hello SESSION_CONTEXT hello określony dla identyfikatora dzierżawcy przy każdym wywołaniu ElasticScaleContext:</span><span class="sxs-lookup"><span data-stu-id="57f9e-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="57f9e-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="57f9e-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="57f9e-147">Dla aplikacji za pomocą ADO.NET SqlClient hello zalecane podejście jest toocreate funkcji otoki wokół ShardMap.OpenConnectionForKey() automatycznie ustawiający "TenantId" w hello SESSION_CONTEXT toohello Popraw TenantId przed zwróceniem połączenie.</span><span class="sxs-lookup"><span data-stu-id="57f9e-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="57f9e-148">tooensure SESSION_CONTEXT zawsze ustawiona, należy otworzyć tylko połączeń za pomocą tej funkcji otoki.</span><span class="sxs-lookup"><span data-stu-id="57f9e-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="57f9e-149">Warstwa danych kroku 2): Tworzenie zasad zabezpieczeń na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="57f9e-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="57f9e-150">Utwórz wiersze, które mogą uzyskiwać dostęp do każdego dzierżawcy hello toofilter zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="57f9e-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="57f9e-151">Teraz, gdy aplikacja hello ustawia SESSION_CONTEXT z bieżącego identyfikatora dzierżawcy hello przed wykonaniem kwerendy, zabezpieczenia na poziomie wiersza zasady zabezpieczeń można filtrować zapytania i wykluczyć wiersze, które mają różne identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="57f9e-152">Kontrola dostępu jest zaimplementowana w T-SQL: hello logika dostępu definiuje funkcję zdefiniowaną przez użytkownika, i zasady zabezpieczeń wiąże funkcja ta tooany liczbę tabel.</span><span class="sxs-lookup"><span data-stu-id="57f9e-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="57f9e-153">Dla tego projektu funkcja hello po prostu Sprawdź, czy hello aplikacji (zamiast innego użytkownika SQL) jest połączonych toohello bazy danych, i że Witaj, "TenantId" przechowywany w hello SESSION_CONTEXT odpowiada hello TenantId danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="57f9e-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="57f9e-154">Predykat filtru umożliwi wiersze spełniające te warunki toopass za pośrednictwem hello filtr dla zapytania SELECT, UPDATE i DELETE; i zapobiega wiersze, które naruszają te warunki przed wstawione lub zaktualizowane predykat bloku.</span><span class="sxs-lookup"><span data-stu-id="57f9e-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="57f9e-155">Jeśli nie ustawiono SESSION_CONTEXT, zwróci wartość NULL i nie wierszy będą toobe widoczny, czy można wstawić.</span><span class="sxs-lookup"><span data-stu-id="57f9e-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="57f9e-156">tooenable zabezpieczenia na poziomie wiersza, wykonanie powitania po T-SQL na wszystkich odłamków przy użyciu albo program Visual Studio (SSDT), SSMS, lub hello skrypt programu PowerShell dołączony hello projektu (lub jeśli używasz [zadania elastyczne bazy danych](sql-database-elastic-jobs-overview.md), można użyć tooautomate wykonywania z tym T-SQL na wszystkich odłamków):</span><span class="sxs-lookup"><span data-stu-id="57f9e-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

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
> <span data-ttu-id="57f9e-157">Bardziej złożone projektów wymagające tooadd hello predykatu w setki tabel można użyć pomocnika przechowywane procedury, która automatycznie generuje zasady zabezpieczeń, dodawanie predykat dla wszystkich tabel w schemacie.</span><span class="sxs-lookup"><span data-stu-id="57f9e-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="57f9e-158">Zobacz [zastosowania zabezpieczeń na poziomie wiersza tooall tabel - pomocnika skryptu (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="57f9e-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="57f9e-159">Teraz po uruchomieniu aplikacji przykładowej hello ponownie dzierżawcy będzie toosee stanie tylko wiersze, które należy toothem.</span><span class="sxs-lookup"><span data-stu-id="57f9e-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="57f9e-160">Ponadto aplikacji hello nie można wstawić wierszy, do których należą tootenants innej niż baza danych niezależnych jeden toohello aktualnie połączonych hello i nie można zaktualizować toohave widocznych wierszy innego identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="57f9e-161">Jeśli aplikacja hello albo prób toodo, DbUpdateException zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="57f9e-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="57f9e-162">Jeśli później Dodaj nową tabelę po prostu ALTER hello zasady zabezpieczeń i dodać predykatów filtru i bloku je na powitania nową tabelę:</span><span class="sxs-lookup"><span data-stu-id="57f9e-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="57f9e-163">Dodaj domyślną tooautomatically ograniczenia wypełnić TenantId dla operacji wstawienia</span><span class="sxs-lookup"><span data-stu-id="57f9e-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="57f9e-164">Możesz też zaznaczyć domyślny ograniczenie dla każdej tabeli tooautomatically wypełnić hello identyfikatora dzierżawcy z hello wartości przechowywanych obecnie we SESSION_CONTEXT podczas wstawiania wierszy.</span><span class="sxs-lookup"><span data-stu-id="57f9e-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="57f9e-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="57f9e-165">For example:</span></span> 

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

<span data-ttu-id="57f9e-166">Teraz aplikacji hello nie jest konieczne toospecify TenantId podczas wstawiania wierszy:</span><span class="sxs-lookup"><span data-stu-id="57f9e-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="57f9e-167">Jeśli używasz domyślne ograniczenia dla projektu programu Entity Framework, zaleca się, że nie zawierają hello TenantId kolumny w modelu danych EF.</span><span class="sxs-lookup"><span data-stu-id="57f9e-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="57f9e-168">Jest to spowodowane zapytania programu Entity Framework automatyczne określanie wartości domyślnych, które zastąpią domyślne hello ograniczenia utworzone w T-SQL, korzystających z SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="57f9e-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="57f9e-169">toouse domyślne ograniczenia w hello przykładowe projektu, na przykład TenantId należy usunąć z DataClasses.cs (i wykonywania Add-Migration hello Konsola Menedżera pakietów) i istnieje tylko w tabelach bazy danych hello tooensure Użyj T-SQL, który hello pola.</span><span class="sxs-lookup"><span data-stu-id="57f9e-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="57f9e-170">W ten sposób EF nie automatycznie dostarcza niepoprawne wartości domyślne podczas wstawiania danych.</span><span class="sxs-lookup"><span data-stu-id="57f9e-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="57f9e-171">(Opcjonalnie) Włącz tooaccess "administratora" wszystkie wiersze</span><span class="sxs-lookup"><span data-stu-id="57f9e-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="57f9e-172">Niektóre aplikacje mogą być toocreate "administratora" kto ma dostęp do wszystkich wierszy, na przykład w kolejności tooenable raportowania przez wszystkich dzierżawców na wszystkich odłamków lub tooperform podziału/Merge operacje na odłamków obejmujących przenoszenie wierszy dzierżawy między bazami danych.</span><span class="sxs-lookup"><span data-stu-id="57f9e-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="57f9e-173">tooenable, należy utworzyć nowego użytkownika SQL ("superuser" w tym przykładzie) w każdym niezależnego fragmentu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="57f9e-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="57f9e-174">Następnie zmienić zasady zabezpieczeń hello z nową funkcję predykatu, która umożliwia tym tooaccess użytkownika wszystkie wiersze:</span><span class="sxs-lookup"><span data-stu-id="57f9e-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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


### <a name="maintenance"></a><span data-ttu-id="57f9e-175">Konserwacji</span><span class="sxs-lookup"><span data-stu-id="57f9e-175">Maintenance</span></span>
* <span data-ttu-id="57f9e-176">**Dodawanie nowych odłamków**: tooenable skryptu T-SQL hello zabezpieczenia na poziomie wiersza musi być wykonywany na wszelkich nowych fragmentów, w przeciwnym razie kwerendy dotyczące tych fragmentów nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="57f9e-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="57f9e-177">**Dodawanie nowych tabel**: należy dodać filtr i zablokować toohello predykatu zabezpieczeń zasady na wszystkich odłamków zawsze, gdy nowa tabela została utworzona, w przeciwnym razie zapytań w nowej tabeli hello nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="57f9e-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="57f9e-178">Ten można zautomatyzować za pomocą wyzwalacza DDL, zgodnie z opisem w [zastosowania zabezpieczeń na poziomie wiersza toonewly tworzone tabele (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f9e-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="57f9e-179">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="57f9e-179">Summary</span></span>
<span data-ttu-id="57f9e-180">Narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza mogą być używane razem tooscale limit aplikacji warstwy danych o obsługę zarówno wielodostępnej i jednym dzierżawcy fragmentów.</span><span class="sxs-lookup"><span data-stu-id="57f9e-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="57f9e-181">Wielodostępne odłamków może być toostore używanych danych wydajniej (szczególnie w przypadkach, gdy mają tylko kilka wierszy danych w dużej liczby dzierżawców), podczas jednego dzierżawcy fragmentów mogą być używane toosupport premium dzierżawców z bardziej rygorystyczne wydajności i izolacji wymagania.</span><span class="sxs-lookup"><span data-stu-id="57f9e-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="57f9e-182">Aby uzyskać więcej informacji, zobacz [informacje dotyczące zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="57f9e-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57f9e-183">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="57f9e-183">Additional resources</span></span>
* [<span data-ttu-id="57f9e-184">Co to jest puli elastycznej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="57f9e-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="57f9e-185">Scaling out with Azure SQL Database (Skalowanie w poziomie za pomocą usługi Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="57f9e-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="57f9e-186">Wzorce projektowe dla wielodostępnych aplikacji SaaS wykorzystujących usługę Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="57f9e-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="57f9e-187">Uwierzytelnianie w aplikacjach wielodostępnych za pomocą usługi Azure AD i OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="57f9e-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="57f9e-188">Aplikacja Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="57f9e-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="57f9e-189">Pytania i żądania funkcji</span><span class="sxs-lookup"><span data-stu-id="57f9e-189">Questions and Feature Requests</span></span>
<span data-ttu-id="57f9e-190">Odpowiedzi na pytania, proszę dotrzeć toous na powitania [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je toohello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="57f9e-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


