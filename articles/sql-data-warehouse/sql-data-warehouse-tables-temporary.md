---
title: "tabele aaaTemporary w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do tabel tymczasowych w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="e1777-103">Tabele tymczasowe w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e1777-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e1777-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="e1777-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e1777-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="e1777-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="e1777-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="e1777-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="e1777-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="e1777-107">[Index][Index]</span></span>
> * <span data-ttu-id="e1777-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="e1777-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="e1777-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="e1777-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="e1777-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="e1777-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="e1777-111">Tabele tymczasowe są bardzo przydatne podczas przetwarzania danych — szczególnie podczas transformacji skutkującej przejściowej hello pośrednich wyników.</span><span class="sxs-lookup"><span data-stu-id="e1777-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="e1777-112">W usłudze SQL Data Warehouse tabel tymczasowych istnieją na poziomie sesji hello.</span><span class="sxs-lookup"><span data-stu-id="e1777-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="e1777-113">Są one tylko widoczne toohello sesji w której zostały utworzone i są automatycznie usuwane po wylogowaniu tej sesji.</span><span class="sxs-lookup"><span data-stu-id="e1777-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="e1777-114">Tabele tymczasowe oferują poprawiać wydajność, ponieważ ich wyniki są zapisywane toolocal zamiast Magazyn zdalny.</span><span class="sxs-lookup"><span data-stu-id="e1777-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="e1777-115">Tabele tymczasowe są nieco inne w usłudze Azure SQL Data Warehouse niż baza danych SQL Azure, ponieważ są one dostępne z dowolnego miejsca w sesji hello, w tym wewnątrz oraz poza procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="e1777-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="e1777-116">Ten artykuł zawiera podstawowe wskazówki dotyczące korzystania z tabel tymczasowych i zaznacza hello zasadami poziomu tabel tymczasowych sesji.</span><span class="sxs-lookup"><span data-stu-id="e1777-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="e1777-117">Korzystając z informacji hello w tym artykule może pomóc modularyzacji kodu, poprawy zarówno możliwość ponownego wykorzystania i łatwości obsługi kodu.</span><span class="sxs-lookup"><span data-stu-id="e1777-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="e1777-118">Tworzenie tabeli tymczasowej</span><span class="sxs-lookup"><span data-stu-id="e1777-118">Create a temporary table</span></span>
<span data-ttu-id="e1777-119">Tabele tymczasowe są tworzone po prostu dodając nazwy tabeli z `#`.</span><span class="sxs-lookup"><span data-stu-id="e1777-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="e1777-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e1777-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="e1777-121">Można również tworzyć tabel tymczasowych z `CTAS` przy użyciu dokładnie hello same podejście:</span><span class="sxs-lookup"><span data-stu-id="e1777-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="e1777-122">`CTAS`to polecenie bardzo zaawansowane i hello dodał zaletą jest bardzo wydajny przy jego użyciu miejsca w dzienniku transakcji.</span><span class="sxs-lookup"><span data-stu-id="e1777-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="e1777-123">Porzucanie tabel tymczasowych</span><span class="sxs-lookup"><span data-stu-id="e1777-123">Dropping temporary tables</span></span>
<span data-ttu-id="e1777-124">Po utworzeniu nowej sesji, powinny istnieć nie tabel tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="e1777-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="e1777-125">Jednak jeśli wywołujesz hello takie same przechowywane procedury, która tworzy tymczasowy z hello tej samej nazwy, tooensure który z `CREATE TABLE` instrukcje są pomyślnie proste Sprawdzanie istnienia wstępne z `DROP` można używać tak jak hello w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e1777-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="e1777-126">Kodowanie spójności, jest dobre praktyki toouse tego wzorca dla tabel i tabelach tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="e1777-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="e1777-127">Istnieje również toouse dobrze `DROP TABLE` tabel tymczasowych tooremove po zakończeniu z nimi w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e1777-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="e1777-128">Programowanie procedury składowanej jest dość często toosee hello poleceń drop powiązane ze sobą na końcu hello tooensure procedury się, że te obiekty są czyszczone.</span><span class="sxs-lookup"><span data-stu-id="e1777-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="e1777-129">Modularizing kodu</span><span class="sxs-lookup"><span data-stu-id="e1777-129">Modularizing code</span></span>
<span data-ttu-id="e1777-130">Ponieważ tabele tymczasowe są widoczne dowolne miejsce w sesji użytkownika, może to być wykorzystanej toohelp modularyzacji kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1777-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="e1777-131">Na przykład hello poniżej procedura składowana zgromadzono hello zalecane rozwiązania powyższego toogenerate DDL, który zaktualizuje wszystkie statystyki w bazie danych hello według nazwy statystyki.</span><span class="sxs-lookup"><span data-stu-id="e1777-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="e1777-132">Na tym etapie hello jedyną akcją, która nastąpiła jest hello tworzenia procedury składowanej, które będą generowane po prostu tabeli tymczasowej stats_ddl #, z instrukcji DDL.</span><span class="sxs-lookup"><span data-stu-id="e1777-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="e1777-133">Tę procedurę składowaną spowoduje porzucenie #stats_ddl, jeśli istnieje już tooensure, który go nie wystąpi niepowodzenie uruchamiania więcej niż raz w ramach sesji.</span><span class="sxs-lookup"><span data-stu-id="e1777-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="e1777-134">Jednak ponieważ nie istnieje żadne `DROP TABLE` końcem hello hello przechowywane procedury zakończeniu hello procedury składowanej, pozostawia tabelę hello utworzone, dzięki czemu mogą być odczytywane poza hello przechowywane procedury.</span><span class="sxs-lookup"><span data-stu-id="e1777-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="e1777-135">W usłudze SQL Data Warehouse w przeciwieństwie do innych baz danych programu SQL Server, jest możliwe toouse tabeli tymczasowej hello poza procedury hello, który go utworzył.</span><span class="sxs-lookup"><span data-stu-id="e1777-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="e1777-136">Tabele tymczasowe SQL Data Warehouse może służyć **dowolnym** wewnątrz hello sesji.</span><span class="sxs-lookup"><span data-stu-id="e1777-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="e1777-137">Może to spowodować toomore moduły i łatwą w obsłudze kodu jak hello w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e1777-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="e1777-138">Ograniczenia tabeli tymczasowej</span><span class="sxs-lookup"><span data-stu-id="e1777-138">Temporary table limitations</span></span>
<span data-ttu-id="e1777-139">Usługa SQL Data Warehouse nakładają kilka ograniczeń podczas implementowania tabel tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="e1777-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="e1777-140">Obecnie tylko sesji zakresami tabel tymczasowych są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e1777-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="e1777-141">Globalne tabele tymczasowe są nieobsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e1777-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="e1777-142">Ponadto widoków nie można utworzyć na tabelach tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="e1777-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1777-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1777-143">Next steps</span></span>
<span data-ttu-id="e1777-144">toolearn więcej, zobacz artykuły hello na [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Indeksowania tabeli][Index], [partycjonowania tabeli] [ Partition] i [ Obsługa statystyk tabeli][Statistics].</span><span class="sxs-lookup"><span data-stu-id="e1777-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="e1777-145">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="e1777-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
