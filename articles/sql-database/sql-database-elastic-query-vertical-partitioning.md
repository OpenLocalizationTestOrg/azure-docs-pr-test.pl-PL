---
title: Zapytanie dla baz danych chmury z innym schematem | Dokumentacja firmy Microsoft
description: "jak skonfigurować zapytań między bazami danych za pośrednictwem partycji pionowej"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="a383b-103">Zapytanie dla baz danych chmury z różnych schematach (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a383b-103">Query across cloud databases with different schemas (preview)</span></span>
![Zapytanie między tabelami w różnych baz danych][1]

<span data-ttu-id="a383b-105">W pionie na partycje bazy danych używać różnych zestawów tabel na różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="a383b-106">Oznacza to, że schemat jest różne na różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="a383b-107">Na przykład wszystkie tabele spisu są na jedną bazę danych, gdy wszystkie tabele powiązane ewidencjonowania aktywności znajdują się w drugiej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a383b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a383b-108">Prerequisites</span></span>
* <span data-ttu-id="a383b-109">Użytkownik musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="a383b-110">To uprawnienie jest dołączany uprawnienie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="a383b-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="a383b-111">Aby odwołać się do źródła danych są potrzebne uprawnienia ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="a383b-112">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a383b-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="a383b-113">W odróżnieniu od z partycjonowania poziomy tych instrukcji DDL nie zależą od Definiowanie warstwą danych z mapą niezależnego fragmentu za pomocą biblioteki klienta elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="a383b-114">TWORZENIE KLUCZA GŁÓWNEGO</span><span class="sxs-lookup"><span data-stu-id="a383b-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="a383b-115">UTWÓRZ BAZĘ DANYCH O ZAKRESIE POŚWIADCZEŃ</span><span class="sxs-lookup"><span data-stu-id="a383b-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="a383b-116">TWORZENIE ZEWNĘTRZNEGO ŹRÓDŁA DANYCH</span><span class="sxs-lookup"><span data-stu-id="a383b-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="a383b-117">TWORZENIE TABELI ZEWNĘTRZNEJ</span><span class="sxs-lookup"><span data-stu-id="a383b-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="a383b-118">Tworzenie klucza głównego bazy danych i poświadczeń</span><span class="sxs-lookup"><span data-stu-id="a383b-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="a383b-119">Poświadczenie jest używany przez elastycznej zapytania do nawiązania połączenia zdalnego baz danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="a383b-120">Upewnij się, że `<username>` nie zawiera żadnych **"@servername"** sufiks.</span><span class="sxs-lookup"><span data-stu-id="a383b-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="a383b-121">Tworzenie zewnętrznych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="a383b-121">Create external data sources</span></span>
<span data-ttu-id="a383b-122">Składnia:</span><span class="sxs-lookup"><span data-stu-id="a383b-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="a383b-123">Parametr typu musi być ustawiony na **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="a383b-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="a383b-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="a383b-124">Example</span></span>
<span data-ttu-id="a383b-125">Poniższy przykład przedstawia użycie instrukcji CREATE dla zewnętrznych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="a383b-126">Aby pobrać listę bieżących źródeł danych zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="a383b-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="a383b-127">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="a383b-127">External Tables</span></span>
<span data-ttu-id="a383b-128">Składnia:</span><span class="sxs-lookup"><span data-stu-id="a383b-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="a383b-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="a383b-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="a383b-130">Poniższy przykład pokazuje, jak pobrać listę tabel zewnętrznych z bieżącej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="a383b-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="a383b-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a383b-131">Remarks</span></span>
<span data-ttu-id="a383b-132">Elastyczne zapytania rozszerza istniejący składni tabeli zewnętrznej do definiowania tabel zewnętrznych, korzystających z zewnętrznych źródeł danych typu RDBMS.</span><span class="sxs-lookup"><span data-stu-id="a383b-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="a383b-133">Definicja tabeli zewnętrznej dla partycjonowanie pionowe obejmuje następujące aspekty:</span><span class="sxs-lookup"><span data-stu-id="a383b-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="a383b-134">**Schemat**: tabeli zewnętrznej DDL definiuje schemat, który można użyć zapytań.</span><span class="sxs-lookup"><span data-stu-id="a383b-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="a383b-135">Wybrany schemat w definicji tabeli zewnętrznej musi pasuje do schematu tabel w zdalnej bazy danych, gdzie są przechowywane dane.</span><span class="sxs-lookup"><span data-stu-id="a383b-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="a383b-136">**Odwołanie do zdalnej bazy danych**: tabeli zewnętrznej DDL odwołuje się do zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="a383b-137">Zewnętrzne źródło danych określa nazwy serwera logicznego i bazy danych, zdalnego przechowywania danych rzeczywistych tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="a383b-138">Składnia służąca do tworzenia tabel zewnętrznych za pomocą zewnętrznego źródła danych, zgodnie z opisem w poprzedniej sekcji, jest następujący:</span><span class="sxs-lookup"><span data-stu-id="a383b-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="a383b-139">W klauzuli DATA_SOURCE definiuje zewnętrznego źródła danych (tj. zdalnej bazy danych w przypadku partycjonowanie pionowe) używany do tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="a383b-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="a383b-140">Klauzule SCHEMA_NAME i OBJECT_NAME zapewniają możliwość mapowania definicji tabeli zewnętrznej tabeli do innego schematu na zdalnej bazy danych lub tabeli o innej nazwie, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="a383b-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="a383b-141">Jest to przydatne, jeśli chcesz zdefiniować tabelę zewnętrzną widoku wykazu lub DMV na zdalnej bazy danych — lub w innej sytuacji, gdy nazwa tabeli zdalnej jest już zajęta lokalnie.</span><span class="sxs-lookup"><span data-stu-id="a383b-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="a383b-142">Następująca instrukcja DDL porzuca istniejącej definicji tabeli zewnętrznej z katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a383b-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="a383b-143">Nie ma ona wpływu zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="a383b-144">**Uprawnienia CREATE/DROP tabeli zewnętrznej**: potrzebne są uprawnienia ALTER ANY zewnętrznego źródła danych dla tabeli zewnętrznej DDL, który również jest wymagany do odwoływania się do źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="a383b-145">Zagadnienia związane z zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="a383b-145">Security considerations</span></span>
<span data-ttu-id="a383b-146">Użytkownicy z dostępem do tabeli zewnętrznej automatycznie uzyskują dostęp do tabel zdalnym w obszarze poświadczenia podane w definicji źródła danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="a383b-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="a383b-147">Aby zapobiec niepożądanemu podniesienia uprawnień przy użyciu poświadczeń do zewnętrznego źródła danych należy starannie zarządzanie dostępem do tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="a383b-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="a383b-148">Regularne SQL uprawnienia można PRZYDZIELIĆ lub ODWOŁAĆ dostęp do tabeli zewnętrznej, tak jakby był on zwykłą tabelę.</span><span class="sxs-lookup"><span data-stu-id="a383b-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="a383b-149">Przykład: zapytanie w pionie na partycje baz danych</span><span class="sxs-lookup"><span data-stu-id="a383b-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="a383b-150">Następujące zapytanie wykonuje trzystopniowego sprzężenie dwóch tabel lokalnych dla zleceń i kolejność wierszy w tabeli zdalnej dla klientów.</span><span class="sxs-lookup"><span data-stu-id="a383b-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="a383b-151">Jest to przykład przypadek użycia danych odwołania dla elastycznej zapytania:</span><span class="sxs-lookup"><span data-stu-id="a383b-151">This is an example of the reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="a383b-152">Przechowywana procedura zdalne wykonywanie kodu T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="a383b-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="a383b-153">Elastyczne zapytania wprowadza również procedury przechowywanej, która zapewnia bezpośredni dostęp do fragmentów.</span><span class="sxs-lookup"><span data-stu-id="a383b-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="a383b-154">Procedura składowana jest nazywany [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) i może służyć do wykonania zdalnego procedur składowanych lub kod T-SQL na zdalnym baz danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="a383b-155">Go przyjmuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="a383b-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="a383b-156">Nazwa źródła danych (nvarchar): Nazwa źródła danych zewnętrznych typu RDBMS.</span><span class="sxs-lookup"><span data-stu-id="a383b-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="a383b-157">Zapytania (nvarchar): zapytania T-SQL do wykonania na każdej niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="a383b-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="a383b-158">Deklaracja parametru (nvarchar) - opcjonalne: ciąg zawierający definicje typów danych parametrów parametr zapytania (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="a383b-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="a383b-159">Lista wartości parametrów - opcjonalne: rozdzielana przecinkami lista wartości parametrów (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="a383b-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="a383b-160">PS\_wykonania\_zdalnego używa zewnętrzne źródło danych podane w parametrów wywołania do wykonania danej instrukcji T-SQL na zdalnym baz danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="a383b-161">Łączenie się z bazy danych Menedżera shardmap i zdalnymi bazami danych używa poświadczeń do zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="a383b-162">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a383b-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="a383b-163">Połączenie narzędzi</span><span class="sxs-lookup"><span data-stu-id="a383b-163">Connectivity for tools</span></span>
<span data-ttu-id="a383b-164">Prawidłowe parametry połączenia SQL Server umożliwia połączenia narzędzi integracyjnych BI i danych do baz danych na serwerze bazy danych SQL, który ma elastycznej zapytania włączone i tabel zewnętrznych zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="a383b-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="a383b-165">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a383b-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="a383b-166">Następnie zobacz kwerendy elastycznej bazy danych i jego tabele zewnętrzne, podobnie jak wszystkie inne bazy danych SQL Server, które można połączyć się z narzędziem.</span><span class="sxs-lookup"><span data-stu-id="a383b-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="a383b-167">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="a383b-167">Best practices</span></span>
* <span data-ttu-id="a383b-168">Upewnij się, że elastycznej kwerendy bazy danych punktu końcowego ma dostęp do zdalnej bazy danych przez umożliwienie dostępu do usług platformy Azure w konfiguracji zapory bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a383b-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="a383b-169">Upewnij się również, że poświadczenia podane w definicji źródła danych zewnętrznych może pomyślnie zalogować się do zdalnej bazy danych i ma uprawnienia dostępu do tabeli zdalnej.</span><span class="sxs-lookup"><span data-stu-id="a383b-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="a383b-170">Zapytania elastycznej działa najlepiej dla zapytań gdzie na zdalnych baz danych można wykonać większość obliczenia.</span><span class="sxs-lookup"><span data-stu-id="a383b-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="a383b-171">Zwykle uzyskać najlepszą wydajność zapytań z predykatu filtru selektywnego, które można oszacować na zdalnych baz danych lub sprzężenia, które mogą być wykonywane całkowicie na zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a383b-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="a383b-172">Innymi wzorcami zapytań może być konieczne ładowania dużych ilości danych ze zdalną bazą danych i mogą działać nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="a383b-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a383b-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a383b-173">Next steps</span></span>

* <span data-ttu-id="a383b-174">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a383b-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="a383b-175">Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="a383b-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="a383b-176">Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a383b-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="a383b-177">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="a383b-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="a383b-178">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="a383b-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
