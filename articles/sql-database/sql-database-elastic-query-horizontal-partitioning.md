---
title: aaaReporting dla baz danych w chmurze skalowalnych w poziomie | Dokumentacja firmy Microsoft
description: "jak tooset się elastycznej zapytania dotyczące poziomych partycji"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="6834c-103">Raportowanie w chmurze skalowalnych w poziomie bazy danych (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="6834c-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Wysyłanie zapytań na odłamków][1]

<span data-ttu-id="6834c-105">Bazy danych podzielonej rozpowszechniają wiersze danych skalowanej warstwy.</span><span class="sxs-lookup"><span data-stu-id="6834c-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="6834c-106">Schemat Hello jest takie same na wszystkich uczestniczących baz danych, nazywany również poziomych partycji.</span><span class="sxs-lookup"><span data-stu-id="6834c-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="6834c-107">Przy użyciu elastycznej kwerendy, możesz utworzyć raporty, obejmujące wszystkie bazy danych podzielonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="6834c-108">Aby uzyskać szybki start, zobacz [raportowania dla baz danych w chmurze skalowalnych w poziomie](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="6834c-109">Podzielonej baz danych, zobacz [zapytania dla baz danych chmury z różnych schematach](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6834c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6834c-110">Prerequisites</span></span>
* <span data-ttu-id="6834c-111">Tworzenie za pomocą biblioteki klienta elastycznej bazy danych hello mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="6834c-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="6834c-112">zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="6834c-113">Lub użyj hello przykładową aplikację w [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="6834c-114">Zobacz też [migracji istniejącej bazy danych bazy danych poza tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="6834c-115">Witaj, użytkownik musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="6834c-116">To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="6834c-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="6834c-117">Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="6834c-118">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6834c-118">Overview</span></span>
<span data-ttu-id="6834c-119">Te instrukcje utwórz warstwę danych podzielonej reprezentację metadanych hello w hello elastycznej zapytanie do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="6834c-120">TWORZENIE KLUCZA GŁÓWNEGO</span><span class="sxs-lookup"><span data-stu-id="6834c-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="6834c-121">UTWÓRZ BAZĘ DANYCH O ZAKRESIE POŚWIADCZEŃ</span><span class="sxs-lookup"><span data-stu-id="6834c-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="6834c-122">TWORZENIE ZEWNĘTRZNEGO ŹRÓDŁA DANYCH</span><span class="sxs-lookup"><span data-stu-id="6834c-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="6834c-123">TWORZENIE TABELI ZEWNĘTRZNEJ</span><span class="sxs-lookup"><span data-stu-id="6834c-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="6834c-124">1.1 utworzyć klucz główny bazy danych i poświadczeń</span><span class="sxs-lookup"><span data-stu-id="6834c-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="6834c-125">poświadczenie Hello jest używany przez hello elastycznej zapytania tooconnect tooyour zdalnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="6834c-126">Upewnij się, że hello *"\<username\>"* nie zawiera żadnych *"@servername"* sufiks.</span><span class="sxs-lookup"><span data-stu-id="6834c-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="6834c-127">1.2 Tworzenie zewnętrznych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="6834c-127">1.2 Create external data sources</span></span>
<span data-ttu-id="6834c-128">Składnia:</span><span class="sxs-lookup"><span data-stu-id="6834c-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="6834c-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="6834c-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="6834c-130">Pobieranie listy hello bieżącego zewnętrznych źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="6834c-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="6834c-131">Witaj zewnętrznego źródła danych odwołuje się do mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="6834c-131">hello external data source references your shard map.</span></span> <span data-ttu-id="6834c-132">Elastyczne zapytanie używa następnie hello zewnętrznego źródła danych i hello źródłowego niezależnego fragmentu mapy tooenumerate hello bazy danych należące do warstwy danych hello.</span><span class="sxs-lookup"><span data-stu-id="6834c-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="6834c-133">Hello tych samych poświadczeń są używane tooread hello niezależnego fragmentu mapy i tooaccess hello danych na powitania odłamków podczas przetwarzania hello elastycznej zapytania.</span><span class="sxs-lookup"><span data-stu-id="6834c-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="6834c-134">1.3 tworzenia tabel zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="6834c-134">1.3 Create external tables</span></span>
<span data-ttu-id="6834c-135">Składnia:</span><span class="sxs-lookup"><span data-stu-id="6834c-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="6834c-136">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="6834c-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="6834c-137">Pobieranie listy hello tabel zewnętrznych z hello bieżąca baza danych:</span><span class="sxs-lookup"><span data-stu-id="6834c-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="6834c-138">toodrop tabel zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="6834c-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="6834c-139">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6834c-139">Remarks</span></span>
<span data-ttu-id="6834c-140">Witaj danych\_hello zewnętrznego źródła danych (mapy niezależnego fragmentu) używany do tabeli zewnętrznej hello definiuje klauzuli źródła.</span><span class="sxs-lookup"><span data-stu-id="6834c-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="6834c-141">Witaj SCHEMATU\_nazwy i obiektu\_klauzule Nazwa mapy Tabela tooa definicji tabeli zewnętrznej hello w innym schematem.</span><span class="sxs-lookup"><span data-stu-id="6834c-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="6834c-142">Pominięcie schematu hello obiektu zdalnego hello przyjęto, że toobe "właściciela" i jego nazwa przyjęto, że nazwa tabeli zewnętrznej identyczne toohello toobe definiowanego.</span><span class="sxs-lookup"><span data-stu-id="6834c-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="6834c-143">Jest to przydatne, zajętej hello nazwę zdalnego tabeli w bazie danych hello w odpowiednim miejscu toocreate hello zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="6834c-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="6834c-144">Na przykład chcesz toodefine tooget tabeli zewnętrznej zagregowany widok widoków wykazu lub widoków DMV skalowanej danych w warstwie.</span><span class="sxs-lookup"><span data-stu-id="6834c-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="6834c-145">Ponieważ widoków wykazu i widoków DMV już istnieje lokalnie, nie można używać ich nazwy hello definicji tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="6834c-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="6834c-146">Zamiast tego użyj innej nazwy i użyj widoku wykazu hello lub hello DMV jego nazwę w hello SCHEMATU\_nazwę i/lub obiekt\_klauzule nazwy.</span><span class="sxs-lookup"><span data-stu-id="6834c-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="6834c-147">(Zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="6834c-147">(See hello example below.)</span></span> 

<span data-ttu-id="6834c-148">Klauzula dystrybucji Hello określa hello danych dystrybucji używany dla tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6834c-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="6834c-149">procesor zapytań Hello wykorzystuje hello informacji dostępnych w hello dystrybucji klauzuli toobuild hello najbardziej efektywny plany zapytań.</span><span class="sxs-lookup"><span data-stu-id="6834c-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="6834c-150">**PODZIELONEJ** oznacza danych jest poziomo podzielonym na partycje w hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="6834c-151">Partycjonowanie klucza dystrybucji danych hello jest hello Hello **< sharding_column_name >** parametru.</span><span class="sxs-lookup"><span data-stu-id="6834c-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="6834c-152">**REPLIKOWANE** oznacza, że identycznych kopii tabeli hello są obecne w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="6834c-153">Jest Twoje tooensure odpowiedzialność hello repliki są identyczne dla hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="6834c-154">**ROUND\_działania OKRĘŻNEGO** oznacza tabeli hello poziomo na partycje za pomocą metody dystrybucji aplikacji zależnych.</span><span class="sxs-lookup"><span data-stu-id="6834c-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="6834c-155">**Odwołanie do warstwy danych**: hello tabeli zewnętrznej DDL odwołuje się tooan zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="6834c-156">Witaj zewnętrznego źródła danych określa mapy niezależnego fragmentu, dzięki czemu dostępne tabeli zewnętrznej hello toolocate niezbędne informacje hello wszystkich baz danych hello warstwę danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="6834c-157">Zagadnienia związane z zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="6834c-157">Security considerations</span></span>
<span data-ttu-id="6834c-158">Użytkownicy z tabeli zewnętrznej toohello dostępu jest automatycznie uzyskują dostęp toohello zdalnego tabel w obszarze hello poświadczenia podane w definicji źródła danych zewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="6834c-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="6834c-159">Unikaj niepożądane podniesienia uprawnień za pomocą hello poświadczenia hello zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="6834c-160">Użyj GRANT lub REVOKE dla tabeli zewnętrznej, tak jakby był on zwykłą tabelę.</span><span class="sxs-lookup"><span data-stu-id="6834c-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="6834c-161">Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne mogą teraz używać pełnej T-SQL w tabelach zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="6834c-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="6834c-162">Przykład: badanie poziome partycjonowane baz danych</span><span class="sxs-lookup"><span data-stu-id="6834c-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="6834c-163">Hello następujące zapytanie wykonuje sprzężenie trzystopniowo magazynów, zamówienia i kolejność wierszy i używa kilku wartości zagregowanych i selektywnego filtru.</span><span class="sxs-lookup"><span data-stu-id="6834c-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="6834c-164">Zakłada się (1) poziomych partycji (dzielenia na fragmenty), a (2) magazynów, zamówienia i kolejność wierszy są podzielonej przez hello w kolumnie Identyfikator magazynu, a hello zapytania elastycznej mogą kolokuj sprzężenia hello na powitania odłamków i przetwarzać hello kosztowne część zapytania hello na powitania odłamków równolegle.</span><span class="sxs-lookup"><span data-stu-id="6834c-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="6834c-165">Przechowywana procedura zdalne wykonywanie kodu T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="6834c-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="6834c-166">Elastyczne zapytania wprowadza również procedury przechowywanej, która zapewnia bezpośredni dostęp odłamków toohello.</span><span class="sxs-lookup"><span data-stu-id="6834c-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="6834c-167">Hello jest wywoływana procedura składowana [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) i tooexecute używane zdalne procedury składowane lub kod T-SQL na powitania zdalnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="6834c-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="6834c-168">Trwa hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6834c-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="6834c-169">Nazwa źródła danych (nvarchar): Nazwa hello hello zewnętrznego źródła danych RDBMS typu.</span><span class="sxs-lookup"><span data-stu-id="6834c-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="6834c-170">Zapytania (nvarchar): hello T-SQL toobe zapytanie wykonywane na każdej niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="6834c-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="6834c-171">Deklaracja parametru (nvarchar) - opcjonalne: ciąg zawierający definicje typów danych parametrów hello hello parametr zapytania (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="6834c-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="6834c-172">Lista wartości parametrów - opcjonalne: rozdzielana przecinkami lista wartości parametrów (na przykład sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="6834c-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="6834c-173">Hello sp\_wykonania\_zewnętrzne źródło danych podane w podanej instrukcji T-SQL w bazach danych, zdalnego hello hello wywołania parametry tooexecute hello hello używa zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6834c-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="6834c-174">Poświadczenie hello hello dane zewnętrzne źródło tooconnect toohello shardmap Menedżera bazy danych i baz danych, zdalnego hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="6834c-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="6834c-175">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6834c-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="6834c-176">Połączenie narzędzi</span><span class="sxs-lookup"><span data-stu-id="6834c-176">Connectivity for tools</span></span>
<span data-ttu-id="6834c-177">Użyj regularne tooconnect ciągów połączenia programu SQL Server aplikacji, danych i BI integracji narzędzia toohello bazy danych za pomocą definicji tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="6834c-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="6834c-178">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="6834c-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="6834c-179">Odwoływanie hello elastycznej kwerendy bazy danych jak dowolnego innego programu SQL Server połączone bazy danych toohello narzędzia, a następnie użyj tabel zewnętrznych z narzędzia lub aplikacji, tak jakby były lokalne tabele.</span><span class="sxs-lookup"><span data-stu-id="6834c-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="6834c-180">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="6834c-180">Best practices</span></span>
* <span data-ttu-id="6834c-181">Upewnij się, że podano tej bazy danych punktu końcowego elastycznej zapytania hello shardmap toohello dostępu do bazy danych i wszystkie odłamków za pośrednictwem powitalne zapory bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6834c-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="6834c-182">Sprawdza, czy lub wymusić hello danych dystrybucji zdefiniowanych przez tabelę zewnętrzną hello.</span><span class="sxs-lookup"><span data-stu-id="6834c-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="6834c-183">Jeśli dystrybucji rzeczywiste dane jest inna niż określona w definicji tabeli dystrybucji hello, kwerend może dać nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="6834c-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="6834c-184">Elastyczne zapytania aktualnie nie wykonuje eliminacji niezależnego fragmentu podczas predykaty za pośrednictwem klucza dzielenia na fragmenty hello pozwala Wyklucz toosafely niektórych odłamków z przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="6834c-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="6834c-185">Zapytania elastycznej działa najlepiej dla zapytań gdzie na powitania odłamków można wykonać większość obliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="6834c-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="6834c-186">Zwykle uzyskać hello najlepszą wydajność zapytań z predykatu filtru selektywnego, które może przyjąć odłamków hello lub sprzężenia za pośrednictwem hello partycjonowania kluczy, które mogą być wykonywane w sposób wyrównany do partycji na wszystkich fragmentów.</span><span class="sxs-lookup"><span data-stu-id="6834c-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="6834c-187">Innymi wzorcami zapytań może być konieczne tooload dużych ilości danych z węzłem głównym hello odłamków toohello i mogą działać nieprawidłowo</span><span class="sxs-lookup"><span data-stu-id="6834c-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="6834c-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6834c-188">Next steps</span></span>

* <span data-ttu-id="6834c-189">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="6834c-190">Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="6834c-191">Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="6834c-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="6834c-192">Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6834c-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="6834c-193">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="6834c-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
