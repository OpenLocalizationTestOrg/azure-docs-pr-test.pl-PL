---
title: "Aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza"
description: "Dowiedz się, jak utworzyć aplikację z warstwą danych skalowalnej bazie danych SQL Azure, która obsługuje wielodostępne odłamków za pomocą narzędzi elastycznej bazy danych wraz z zabezpieczeniami na poziomie wiersza."
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
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="761e4-103">Aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="761e4-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="761e4-104">[Narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md) i [zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131) oferują zaawansowany zestaw możliwości elastyczne i wydajne skalowanie warstwy danych wielodostępnych aplikacji z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="761e4-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="761e4-105">Zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="761e4-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="761e4-106">W tym artykule przedstawiono sposób używania tych technologii jednocześnie do tworzenia aplikacji z warstwą danych skalowalnej obsługuje wielodostępne odłamków, za pomocą **ADO.NET SqlClient** i/lub **programu Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="761e4-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="761e4-107">**Narzędzi elastycznej bazy danych** umożliwia deweloperom skalowania warstwy danych aplikacji za pośrednictwem standardowych dzielenia na fragmenty rozwiązania przy użyciu zestawu .NET bibliotek i szablony usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="761e4-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="761e4-108">Zarządzanie odłamków z za pomocą biblioteki klienta elastycznej bazy danych pozwala zautomatyzować i uprościć wiele zadań infrastrukturalne zwykle skojarzone z dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="761e4-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="761e4-109">**Wiersz poziomu zabezpieczeń** umożliwia deweloperom przechowywania danych dla wielu dzierżawców w tej samej bazy danych za pomocą zasad zabezpieczeń, aby odfiltrować wiersze, które nie należą do dzierżawy wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="761e4-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="761e4-110">Scentralizowany dostęp logiki odświeżania w bazie danych, a nie w aplikacji upraszcza konserwację i zmniejsza ryzyko błędu ścieżce bazowej kodu aplikacji rozwoju.</span><span class="sxs-lookup"><span data-stu-id="761e4-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="761e4-111">Razem z tych funkcji, aplikacji mogą korzystać z koszt zyski oszczędności i wydajności, dane są przechowywane dla wielu dzierżawców w bazie danych sam identyfikator niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="761e4-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="761e4-112">W tym samym czasie aplikacji nadal ma możliwość oferuje izolowanym, pojedynczego dzierżawcy fragmentów dla dzierżawcy "premium", którzy wymagają bardziej rygorystyczne gwarancji wydajności, ponieważ odłamków wielodostępne gwarantuje dystrybucji równy zasobów między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="761e4-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="761e4-113">Krótko mówiąc, elastyczne bazy danych biblioteki klienta [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) interfejsów API automatycznie łączyć dzierżaw poprawny identyfikator niezależnego fragmentu bazy danych zawierającej klucz dzielenia na fragmenty (zazwyczaj "TenantId").</span><span class="sxs-lookup"><span data-stu-id="761e4-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="761e4-114">Po nawiązaniu połączenia zasady zabezpieczeń zabezpieczenia na poziomie wiersza w bazie danych zapewnia, że dzierżawców można tylko dostęp do wierszy zawierających ich identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="761e4-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="761e4-115">Zakłada się, że wszystkie tabele zawierają kolumnę TenantId wskazują wiersze, które należą do każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="761e4-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![Architektura aplikacji obsługi blogów][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="761e4-117">Pobierz przykładowy projekt</span><span class="sxs-lookup"><span data-stu-id="761e4-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="761e4-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="761e4-118">Prerequisites</span></span>
* <span data-ttu-id="761e4-119">Za pomocą programu Visual Studio (2012 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="761e4-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="761e4-120">Utwórz trzy bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="761e4-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="761e4-121">Pobierz przykładowy projekt: [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - odłamków wielodostępne](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="761e4-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="761e4-122">Wprowadź informacje dla baz danych na początku **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="761e4-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="761e4-123">Ten projekt rozszerza opisanych w [elastyczne narzędzia bazy danych dla bazy danych SQL Azure - Entity Framework integracji](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) przez dodanie obsługi wielodostępne niezależnego fragmentu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="761e4-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="761e4-124">Tworzenia prostej aplikacji konsolowej do tworzenia blogów i wpisów, z czterech dzierżawców i dwóch niezależnych wielodostępnych baz danych jak pokazano na powyższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="761e4-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="761e4-125">Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="761e4-125">Build and run the application.</span></span> <span data-ttu-id="761e4-126">Spowoduje to ładowania początkowego menedżera map niezależnego fragmentu narzędzi elastycznej bazy danych i uruchom następujące testy:</span><span class="sxs-lookup"><span data-stu-id="761e4-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="761e4-127">Przy użyciu programu Entity Framework i LINQ, Utwórz nowy blog, a następnie Wyświetl wszystkie blogi dla każdego dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="761e4-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="761e4-128">Za pomocą ADO.NET SqlClient, wyświetlić wszystkie blogi dla dzierżawy</span><span class="sxs-lookup"><span data-stu-id="761e4-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="761e4-129">Próba wstawienia blogu dla niewłaściwego dzierżawcy sprawdzić, czy błąd jest zgłaszany</span><span class="sxs-lookup"><span data-stu-id="761e4-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="761e4-130">Powiadomienie, że ponieważ zabezpieczenia na poziomie wiersza nie została jeszcze włączona w bazach danych niezależnego fragmentu, tych testów ujawnia problem: dzierżawcy będą mogli zobaczyć blogów, które nie należą do nich, a aplikacja nie będzie mógł Wstawianie blogu dla niewłaściwego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="761e4-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="761e4-131">W dalszej części tego artykułu opisano, jak rozwiązać te problemy przez wymuszania izolacji dzierżawców odświeżania.</span><span class="sxs-lookup"><span data-stu-id="761e4-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="761e4-132">Istnieją dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="761e4-132">There are two steps:</span></span> 

1. <span data-ttu-id="761e4-133">**Warstwy aplikacji**: modyfikowanie kodu aplikacji, aby zawsze ustawić bieżącego identyfikatora dzierżawcy w SESSION_CONTEXT po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="761e4-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="761e4-134">Przykładowy projekt zawiera już zostało to zrobione.</span><span class="sxs-lookup"><span data-stu-id="761e4-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="761e4-135">**Warstwa danych**: Tworzenie zasad zabezpieczeń zabezpieczenia na poziomie wiersza każdego niezależnego fragmentu bazy danych oparte na TenantId przechowywane w SESSION_CONTEXT wierszy filtru.</span><span class="sxs-lookup"><span data-stu-id="761e4-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="761e4-136">Należy to zrobić dla każdego niezależnego fragmentu baz danych, w przeciwnym razie wierszy w wielodostępnym odłamków nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="761e4-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="761e4-137">Warstwy aplikacji w kroku 1): Ustaw TenantId w SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="761e4-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="761e4-138">Po nawiązaniu połączenia z bazą danych niezależnych przy użyciu zależnych API routingu aplikacji nadal wymaga mówić bazy danych biblioteki klienta elastycznej bazy danych które TenantId używa tego połączenia, aby zabezpieczenia na poziomie wiersza zasady zabezpieczeń można odfiltrować wierszy należące do innych dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="761e4-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="761e4-139">Zalecanym sposobem przekazać te informacje jest przechowywanie bieżącego identyfikatora dzierżawy dla tego połączenia w [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="761e4-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="761e4-140">(Uwaga: Możesz też użyć [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ale SESSION_CONTEXT jest lepszym rozwiązaniem, ponieważ jest łatwiejsza w użyciu, zwraca wartość NULL, domyślnie i obsługuje pary klucz wartość.)</span><span class="sxs-lookup"><span data-stu-id="761e4-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="761e4-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="761e4-141">Entity Framework</span></span>
<span data-ttu-id="761e4-142">Dla aplikacji za pomocą programu Entity Framework, najprostszym podejście jest skonfigurowanie SESSION_CONTEXT w zastąpienie ElasticScaleContext opisanego w [danych zależnych routingu przy użyciu EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="761e4-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="761e4-143">Przed zwróceniem połączenia przeprowadzana za pośrednictwem danych zależnych routingu, tworzenie i wykonywanie SqlCommand, która ustawia "TenantId" w SESSION_CONTEXT do shardingKey określony dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="761e4-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="761e4-144">Dzięki temu wystarczy raz napisać kod, aby ustawić SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="761e4-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

<span data-ttu-id="761e4-145">Teraz SESSION_CONTEXT jest ustawiany automatycznie z określonego identyfikatora dzierżawcy przy każdym wywołaniu ElasticScaleContext:</span><span class="sxs-lookup"><span data-stu-id="761e4-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="761e4-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="761e4-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="761e4-147">Dla aplikacji za pomocą ADO.NET SqlClient Zalecanym podejściem jest tworzenie funkcji otoki wokół ShardMap.OpenConnectionForKey() ustawiający automatycznie "TenantId" w SESSION_CONTEXT do poprawne TenantId przed zwróceniem połączenia.</span><span class="sxs-lookup"><span data-stu-id="761e4-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="761e4-148">Aby upewnić się, że SESSION_CONTEXT ma zawsze wartość, należy otworzyć tylko połączeń za pomocą tej funkcji otoki.</span><span class="sxs-lookup"><span data-stu-id="761e4-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="761e4-149">Warstwa danych kroku 2): Tworzenie zasad zabezpieczeń na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="761e4-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="761e4-150">Tworzenie zasad zabezpieczeń, aby filtrować wiersze, które mogą uzyskiwać dostęp do każdego dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="761e4-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="761e4-151">Teraz, gdy aplikacja jest ustawienie SESSION_CONTEXT z bieżącego identyfikatora dzierżawcy przed wykonaniem kwerendy, zabezpieczenia na poziomie wiersza zasady zabezpieczeń można filtrować zapytania i wykluczyć wiersze, które mają różne identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="761e4-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="761e4-152">Kontrola dostępu jest zaimplementowana w T-SQL: logika dostępu definiuje funkcję zdefiniowaną przez użytkownika i zasady zabezpieczeń powiązanie tej funkcji z dowolną liczbę tabel.</span><span class="sxs-lookup"><span data-stu-id="761e4-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="761e4-153">Dla tego projektu funkcja po prostu Sprawdź, czy aplikacji (zamiast innego użytkownika SQL) jest połączona z bazą danych, i że TenantId przechowywane w SESSION_CONTEXT TenantId danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="761e4-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="761e4-154">Predykat filtru umożliwi wiersze spełniające te warunki, które przechodzą przez filtr dla zapytania SELECT, UPDATE i DELETE; i zapobiega wiersze, które naruszają te warunki przed wstawione lub zaktualizowane predykat bloku.</span><span class="sxs-lookup"><span data-stu-id="761e4-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="761e4-155">Jeśli nie ustawiono SESSION_CONTEXT, zwróci wartość NULL i nie wierszy będą widoczne lub możliwe do wstawienia.</span><span class="sxs-lookup"><span data-stu-id="761e4-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="761e4-156">Aby włączyć zabezpieczenia na poziomie wiersza, należy wykonać T-SQL na wszystkich odłamków przy użyciu programu Visual Studio (SSDT), SSMS lub skrypt programu PowerShell dołączony do projektu (lub jeśli używasz [zadania elastyczne bazy danych](sql-database-elastic-jobs-overview.md), służy do automatyzacji wykonywania tego T-SQL na wszystkich odłamków):</span><span class="sxs-lookup"><span data-stu-id="761e4-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="761e4-157">Bardziej złożone projektów, które trzeba dodać predykat na setki tabel można użyć procedury przechowywane pomocnika, która automatycznie generuje zasady zabezpieczeń, dodawanie predykat dla wszystkich tabel w schemacie.</span><span class="sxs-lookup"><span data-stu-id="761e4-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="761e4-158">Zobacz [zastosowania zabezpieczeń na poziomie wiersza do wszystkich tabel - pomocnika skryptu (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="761e4-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="761e4-159">Teraz po uruchomieniu aplikacji przykładowej ponownie dzierżawcy będą widoczne tylko wiersze, które należą do nich.</span><span class="sxs-lookup"><span data-stu-id="761e4-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="761e4-160">Ponadto aplikacja nie można wstawić wierszy, które należą do dzierżawcy innych niż ten, który jest aktualnie połączony z niezależnego fragmentu bazy danych i nie można zaktualizować widocznych wierszy, które mają różne identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="761e4-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="761e4-161">Jeśli aplikacja próbuje zrobić, DbUpdateException zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="761e4-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="761e4-162">Jeśli później Dodaj nową tabelę, po prostu zmienić zasady zabezpieczeń i Dodaj filtr i zablokować predykaty w nowej tabeli:</span><span class="sxs-lookup"><span data-stu-id="761e4-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="761e4-163">Dodaj domyślne ograniczenia, aby automatycznie wypełnić TenantId dla operacji wstawienia</span><span class="sxs-lookup"><span data-stu-id="761e4-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="761e4-164">Możesz też zaznaczyć ograniczeniu domyślnym w każdej tabeli, aby automatycznie wypełnić TenantId o wartości przechowywanych obecnie we SESSION_CONTEXT podczas wstawiania wierszy.</span><span class="sxs-lookup"><span data-stu-id="761e4-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="761e4-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="761e4-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="761e4-166">Teraz aplikacji nie trzeba określać identyfikatora dzierżawcy podczas wstawiania wierszy:</span><span class="sxs-lookup"><span data-stu-id="761e4-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="761e4-167">Użycie domyślne ograniczenia dla projektu programu Entity Framework, zaleca się, że kolumna identyfikatora dzierżawcy nie zostanie uwzględniony w modelu danych EF.</span><span class="sxs-lookup"><span data-stu-id="761e4-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="761e4-168">Jest to spowodowane zapytania programu Entity Framework automatyczne określanie wartości domyślnych, które zastąpią domyślne ograniczenia utworzone w T-SQL używających SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="761e4-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="761e4-169">Aby użyć domyślnego ograniczenia w przykładowy projekt, na przykład, należy usunąć TenantId z DataClasses.cs (i wykonywania Add-Migration w konsoli Menedżera pakietów) i użyj T-SQL, aby upewnić się, że pole istnieje tylko w tabelach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="761e4-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="761e4-170">W ten sposób EF nie automatycznie dostarcza niepoprawne wartości domyślne podczas wstawiania danych.</span><span class="sxs-lookup"><span data-stu-id="761e4-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="761e4-171">(Opcjonalnie) Włącz "administratora" można uzyskać dostępu do wszystkich wierszy</span><span class="sxs-lookup"><span data-stu-id="761e4-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="761e4-172">Niektóre aplikacje warto utworzyć "administratora" kto mogą uzyskiwać dostęp do wszystkich wierszy, na przykład, aby włączyć raportowanie dla wszystkich dzierżawców w odłamków wszystkich lub do wykonywania operacji podziału/Merge na odłamków obejmujących przesuwanie wierszy dzierżawy między bazami danych.</span><span class="sxs-lookup"><span data-stu-id="761e4-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="761e4-173">Aby włączyć tę opcję, należy utworzyć nowego użytkownika SQL ("superuser" w tym przykładzie) w każdym niezależnego fragmentu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="761e4-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="761e4-174">Następnie należy zmienić zasady zabezpieczeń z nowej funkcji predykatu, która umożliwia użytkownikom dostęp do wszystkich wierszy:</span><span class="sxs-lookup"><span data-stu-id="761e4-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

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

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="761e4-175">Konserwacji</span><span class="sxs-lookup"><span data-stu-id="761e4-175">Maintenance</span></span>
* <span data-ttu-id="761e4-176">**Dodawanie nowych odłamków**: należy wykonać skryptu T-SQL, aby włączyć zabezpieczenia na poziomie wiersza na wszelkich nowych fragmentów, w przeciwnym razie kwerendy dotyczące tych fragmentów nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="761e4-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="761e4-177">**Dodawanie nowych tabel**: należy dodać predykat filtru i bloku zasady zabezpieczeń na wszystkich odłamków zawsze, gdy nowa tabela została utworzona, w przeciwnym razie zapytań w nowej tabeli nie będą filtrowane.</span><span class="sxs-lookup"><span data-stu-id="761e4-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="761e4-178">Ten można zautomatyzować za pomocą wyzwalacza DDL, zgodnie z opisem w [zastosowania zabezpieczeń na poziomie wiersza automatycznie na nowo utworzony tabele (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="761e4-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="761e4-179">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="761e4-179">Summary</span></span>
<span data-ttu-id="761e4-180">Narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza mogą być używane razem do skalowania aplikacji warstwy danych o obsługę zarówno wielodostępnych i pojedynczego dzierżawcy fragmentów.</span><span class="sxs-lookup"><span data-stu-id="761e4-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="761e4-181">Wielodostępne odłamków może służyć do przechowywania danych wydajniej (szczególnie w przypadkach, gdy mają tylko kilka wierszy danych w dużej liczby dzierżawców), podczas jednego dzierżawcy fragmentów może służyć do obsługi dzierżawców premium z bardziej rygorystyczne wydajności i izolacja wymagania.</span><span class="sxs-lookup"><span data-stu-id="761e4-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="761e4-182">Aby uzyskać więcej informacji, zobacz [informacje dotyczące zabezpieczeń na poziomie wiersza](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="761e4-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="761e4-183">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="761e4-183">Additional resources</span></span>
* [<span data-ttu-id="761e4-184">Co to jest puli elastycznej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="761e4-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="761e4-185">Scaling out with Azure SQL Database (Skalowanie w poziomie za pomocą usługi Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="761e4-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="761e4-186">Wzorce projektowe dla wielodostępnych aplikacji SaaS wykorzystujących usługę Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="761e4-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="761e4-187">Uwierzytelnianie w aplikacjach wielodostępnych za pomocą usługi Azure AD i OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="761e4-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="761e4-188">Aplikacja Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="761e4-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="761e4-189">Pytania i żądania funkcji</span><span class="sxs-lookup"><span data-stu-id="761e4-189">Questions and Feature Requests</span></span>
<span data-ttu-id="761e4-190">Odpowiedzi na pytania, proszę dotrzeć do nas na [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je do [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="761e4-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


