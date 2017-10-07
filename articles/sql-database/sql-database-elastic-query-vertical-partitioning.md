---
title: aaaQuery w chmurze baz danych z innym schematem | Dokumentacja firmy Microsoft
description: "jak tooset się kwerendy między bazami danych z partycji pionowej"
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
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="48aff-103">Zapytanie dla baz danych chmury z różnych schematach (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="48aff-103">Query across cloud databases with different schemas (preview)</span></span>
![Zapytanie między tabelami w różnych baz danych][1]

<span data-ttu-id="48aff-105">W pionie na partycje bazy danych używać różnych zestawów tabel na różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="48aff-106">Oznacza to, że schemat hello różni się w różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="48aff-107">Na przykład wszystkie tabele spisu są na jedną bazę danych, gdy wszystkie tabele powiązane ewidencjonowania aktywności znajdują się w drugiej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48aff-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="48aff-108">Prerequisites</span></span>
* <span data-ttu-id="48aff-109">Witaj, użytkownik musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="48aff-110">To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="48aff-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="48aff-111">Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="48aff-112">Omówienie</span><span class="sxs-lookup"><span data-stu-id="48aff-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="48aff-113">W odróżnieniu od z partycjonowania poziomy tych instrukcji DDL nie zależą od Definiowanie warstwą danych z mapą niezależnego fragmentu za pomocą biblioteki klienta elastycznej bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="48aff-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="48aff-114">TWORZENIE KLUCZA GŁÓWNEGO</span><span class="sxs-lookup"><span data-stu-id="48aff-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="48aff-115">UTWÓRZ BAZĘ DANYCH O ZAKRESIE POŚWIADCZEŃ</span><span class="sxs-lookup"><span data-stu-id="48aff-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="48aff-116">TWORZENIE ZEWNĘTRZNEGO ŹRÓDŁA DANYCH</span><span class="sxs-lookup"><span data-stu-id="48aff-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="48aff-117">TWORZENIE TABELI ZEWNĘTRZNEJ</span><span class="sxs-lookup"><span data-stu-id="48aff-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="48aff-118">Tworzenie klucza głównego bazy danych i poświadczeń</span><span class="sxs-lookup"><span data-stu-id="48aff-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="48aff-119">poświadczenie Hello jest używany przez hello elastycznej zapytania tooconnect tooyour zdalnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="48aff-120">Upewnij się, że hello `<username>` nie zawiera żadnych **"@servername"** sufiks.</span><span class="sxs-lookup"><span data-stu-id="48aff-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="48aff-121">Tworzenie zewnętrznych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="48aff-121">Create external data sources</span></span>
<span data-ttu-id="48aff-122">Składnia:</span><span class="sxs-lookup"><span data-stu-id="48aff-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="48aff-123">Parametr typu Hello musi ustawić także**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="48aff-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="48aff-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="48aff-124">Example</span></span>
<span data-ttu-id="48aff-125">Witaj poniższy przykład przedstawia użycie hello hello instrukcji CREATE zewnętrznych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="48aff-126">tooretrieve hello listę bieżących źródeł danych zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="48aff-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="48aff-127">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="48aff-127">External Tables</span></span>
<span data-ttu-id="48aff-128">Składnia:</span><span class="sxs-lookup"><span data-stu-id="48aff-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="48aff-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="48aff-129">Example</span></span>
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

<span data-ttu-id="48aff-130">Hello poniższy przykład przedstawia, jak tooretrieve hello listy tabel zewnętrznych z hello bieżąca baza danych:</span><span class="sxs-lookup"><span data-stu-id="48aff-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="48aff-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="48aff-131">Remarks</span></span>
<span data-ttu-id="48aff-132">Elastyczne zapytania rozszerza hello istniejącej tabeli zewnętrznej składni toodefine tabel zewnętrznych korzystających z zewnętrznych źródeł danych typu RDBMS.</span><span class="sxs-lookup"><span data-stu-id="48aff-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="48aff-133">Definicja tabeli zewnętrznej dla partycjonowanie pionowe obejmuje hello następujące aspekty:</span><span class="sxs-lookup"><span data-stu-id="48aff-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="48aff-134">**Schemat**: hello tabeli zewnętrznej DDL definiuje schemat, który można użyć zapytań.</span><span class="sxs-lookup"><span data-stu-id="48aff-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="48aff-135">Schemat Hello w definicji tabeli zewnętrznej wymaga schematu hello toomatch hello tabel w zdalnej bazy danych hello przechowywania hello rzeczywiste dane.</span><span class="sxs-lookup"><span data-stu-id="48aff-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="48aff-136">**Odwołanie do zdalnej bazy danych**: hello tabeli zewnętrznej DDL odwołuje się tooan zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="48aff-137">Witaj zewnętrznego źródła danych określa nazwę serwera logicznego hello i zdalnej bazy danych hello przechowywania danych rzeczywistych tabeli hello Nazwa bazy danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="48aff-138">Za pomocą zewnętrznego źródła danych, zgodnie z opisem w poprzedniej sekcji hello, hello tabel zewnętrznych toocreate składnia jest następująca:</span><span class="sxs-lookup"><span data-stu-id="48aff-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="48aff-139">Klauzula DATA_SOURCE Hello definiuje hello zewnętrznego źródła danych (tj. hello zdalnej bazy danych w przypadku partycjonowanie pionowe) służący do hello tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="48aff-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="48aff-140">klauzule SCHEMA_NAME i OBJECT_NAME Hello odpowiednio zawierają hello możliwości toomap hello tabeli zewnętrznej definicji tooa tabeli do innego schematu na hello zdalnej bazy danych lub tabeli tooa pod inną nazwą.</span><span class="sxs-lookup"><span data-stu-id="48aff-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="48aff-141">Jest to przydatne, jeśli chcesz toodefine widoku wykazu tooa tabeli zewnętrznej lub DMV na zdalnej bazy danych — lub w innej sytuacji, gdy nazwa tabeli zdalnej hello jest już zajęta lokalnie.</span><span class="sxs-lookup"><span data-stu-id="48aff-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="48aff-142">Witaj następująca instrukcja DDL porzuca istniejącej definicji tabeli zewnętrznej z katalogu lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="48aff-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="48aff-143">Nie ma ona wpływu hello zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="48aff-144">**Uprawnienia CREATE/DROP tabeli zewnętrznej**: dla tabeli zewnętrznej DDL, który jest także niezbędne toorefer toohello źródła danych, potrzebne są uprawnienia ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="48aff-145">Zagadnienia związane z zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="48aff-145">Security considerations</span></span>
<span data-ttu-id="48aff-146">Użytkownicy z tabeli zewnętrznej toohello dostępu jest automatycznie uzyskują dostęp toohello zdalnego tabel w obszarze hello poświadczenia podane w definicji źródła danych zewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="48aff-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="48aff-147">Należy uważnie zarządzać tabeli zewnętrznej toohello dostępu w kolejności tooavoid niepożądane podniesienie uprawnień poprzez hello poświadczenia hello zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="48aff-148">Regularne uprawnienia SQL można tooGRANT używane lub ODWOŁAĆ dostępu tooan zewnętrzna tabela, tak jakby był on zwykłą tabelę.</span><span class="sxs-lookup"><span data-stu-id="48aff-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="48aff-149">Przykład: zapytanie w pionie na partycje baz danych</span><span class="sxs-lookup"><span data-stu-id="48aff-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="48aff-150">Witaj następujące zapytanie wykonuje trzystopniowego sprzężenie hello dwóch tabel lokalnych dla zleceń i kolejność wierszy tabeli zdalnej hello dla klientów.</span><span class="sxs-lookup"><span data-stu-id="48aff-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="48aff-151">Jest to przykład przypadek użycia danych hello odwołania dla elastycznej zapytania:</span><span class="sxs-lookup"><span data-stu-id="48aff-151">This is an example of hello reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="48aff-152">Przechowywana procedura zdalne wykonywanie kodu T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="48aff-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="48aff-153">Elastyczne zapytania wprowadza również procedury przechowywanej, która zapewnia bezpośredni dostęp odłamków toohello.</span><span class="sxs-lookup"><span data-stu-id="48aff-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="48aff-154">Hello jest wywoływana procedura składowana [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) i tooexecute używane zdalne procedury składowane lub kod T-SQL na powitania zdalnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="48aff-155">Trwa hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="48aff-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="48aff-156">Nazwa źródła danych (nvarchar): Nazwa hello hello zewnętrznego źródła danych RDBMS typu.</span><span class="sxs-lookup"><span data-stu-id="48aff-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="48aff-157">Zapytania (nvarchar): hello T-SQL toobe zapytanie wykonywane na każdej niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="48aff-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="48aff-158">Deklaracja parametru (nvarchar) - opcjonalne: ciąg zawierający definicje typów danych parametrów hello hello parametr zapytania (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="48aff-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="48aff-159">Lista wartości parametrów - opcjonalne: rozdzielana przecinkami lista wartości parametrów (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="48aff-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="48aff-160">Hello sp\_wykonania\_zewnętrzne źródło danych podane w podanej instrukcji T-SQL w bazach danych, zdalnego hello hello wywołania parametry tooexecute hello hello używa zdalnego.</span><span class="sxs-lookup"><span data-stu-id="48aff-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="48aff-161">Poświadczenie hello hello dane zewnętrzne źródło tooconnect toohello shardmap Menedżera bazy danych i baz danych, zdalnego hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="48aff-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="48aff-162">Przykład:</span><span class="sxs-lookup"><span data-stu-id="48aff-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="48aff-163">Połączenie narzędzi</span><span class="sxs-lookup"><span data-stu-id="48aff-163">Connectivity for tools</span></span>
<span data-ttu-id="48aff-164">Regularne tooconnect ciągów połączenia programu SQL Server można użyć toodatabases narzędzi integracji BI i danych na serwerze bazy danych SQL hello, który ma elastycznej zapytań włączone i tabel zewnętrznych zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="48aff-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="48aff-165">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="48aff-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="48aff-166">Następnie można znaleźć toohello elastycznej zapytanie do bazy danych i jego tabele zewnętrzne, podobnie jak wszystkie inne bazy danych SQL Server czy można połączyć toowith własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="48aff-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="48aff-167">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="48aff-167">Best practices</span></span>
* <span data-ttu-id="48aff-168">Upewnij się, że tej bazy danych punktu końcowego elastycznej zapytania hello została podana zdalnej bazy danych programu access toohello przez umożliwienie dostępu do usług platformy Azure w konfiguracji zapory bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="48aff-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="48aff-169">Upewnij się również to poświadczenie hello danych zewnętrznych hello definicji źródła może pomyślnie zalogować się do zdalnej bazy danych hello i ma tabeli zdalnej tooaccess hello hello uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="48aff-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="48aff-170">Zapytania elastycznej działa najlepiej dla zapytań gdzie na powitania zdalnych baz danych można wykonać większość obliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="48aff-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="48aff-171">Zwykle uzyskać najlepszą wydajność zapytań hello z predykatu filtru selektywnego, które można oszacować na powitania zdalnych baz danych lub sprzężenia, które mogą być wykonywane całkowicie na powitania zdalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="48aff-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="48aff-172">Innymi wzorcami zapytań może być konieczne tooload dużych ilości danych z hello zdalnej bazy danych i mogą działać nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="48aff-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="48aff-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48aff-173">Next steps</span></span>

* <span data-ttu-id="48aff-174">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48aff-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="48aff-175">Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="48aff-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="48aff-176">Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="48aff-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="48aff-177">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="48aff-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="48aff-178">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="48aff-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
