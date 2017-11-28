---
title: "aaaGuide dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki i zalecenia dotyczące przy użyciu programu PolyBase w scenariuszach SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="df2c1-103">Przewodnik dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="df2c1-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="df2c1-104">Ten przewodnik zawiera informacje praktyczne dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df2c1-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="df2c1-105">tooget pracę, zobacz hello [ładowanie danych przy użyciu programu PolyBase] [ Load data with PolyBase] samouczka.</span><span class="sxs-lookup"><span data-stu-id="df2c1-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="df2c1-106">Obracanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="df2c1-106">Rotating storage keys</span></span>
<span data-ttu-id="df2c1-107">Od czasu tootime można magazynu obiektów blob klucza tooyour toochange hello dostęp ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="df2c1-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="df2c1-108">Witaj najbardziej elegancki tooperform sposób, to zadanie jest toofollow w ramach procesu nazywanego "obracanie klucze hello".</span><span class="sxs-lookup"><span data-stu-id="df2c1-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="df2c1-109">Można zauważyć ma dwa klucze magazynu dla konta magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="df2c1-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="df2c1-110">Jest to, aby można przejść</span><span class="sxs-lookup"><span data-stu-id="df2c1-110">This is so that you can transition</span></span>

<span data-ttu-id="df2c1-111">Obracanie klucze konta magazynu platformy Azure jest procesem prosty krok trzy</span><span class="sxs-lookup"><span data-stu-id="df2c1-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="df2c1-112">Utworzyć drugi poświadczeń o zakresie bazy danych na podstawie klucza dostępu do magazynu pomocniczego hello</span><span class="sxs-lookup"><span data-stu-id="df2c1-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="df2c1-113">Utworzyć drugi zewnętrznego źródła danych poza tym nowe poświadczenie</span><span class="sxs-lookup"><span data-stu-id="df2c1-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="df2c1-114">Usunąć i utworzyć tabel zewnętrznych hello wskazanie toohello nowego zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="df2c1-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="df2c1-115">Po dokonaniu migracji wszystkich tabel zewnętrznych toohello nowego zewnętrznego źródła danych, a następnie można wykonać hello wyczyścić zadań:</span><span class="sxs-lookup"><span data-stu-id="df2c1-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="df2c1-116">Usuń pierwszy zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="df2c1-116">Drop first external data source</span></span>
2. <span data-ttu-id="df2c1-117">Poświadczeń, klucz dostępu do magazynu podstawowego hello w oparciu o zakresie pierwszy Porzuć bazę danych</span><span class="sxs-lookup"><span data-stu-id="df2c1-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="df2c1-118">Zaloguj się do platformy Azure i ponownie wygenerować klucza dostępu podstawowy hello gotowe do hello następnym</span><span class="sxs-lookup"><span data-stu-id="df2c1-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="df2c1-119">Zapytania na danych magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="df2c1-119">Query Azure blob storage data</span></span>
<span data-ttu-id="df2c1-120">Zapytania dotyczące tabel zewnętrznych po prostu użyć nazwy tabeli hello tak, jakby był relacyjne tabeli.</span><span class="sxs-lookup"><span data-stu-id="df2c1-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="df2c1-121">Zapytania w tabeli zewnętrznej może zakończyć się niepowodzeniem z powodu błędu hello *"zapytanie zostało przerwane — podczas odczytu z zewnętrznego źródła Osiągnięto próg maksymalnej Odrzuć hello"*.</span><span class="sxs-lookup"><span data-stu-id="df2c1-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="df2c1-122">Oznacza to, że dane zewnętrzne zawiera *zanieczyszczone* rekordów.</span><span class="sxs-lookup"><span data-stu-id="df2c1-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="df2c1-123">Rekord danych jest uznawany za "zakłócone", jeśli hello rzeczywiste dane typy/liczba kolumn nie zgadzają hello definicje kolumn z tabeli zewnętrznej hello lub hello danych nie jest zgodna z toohello określonego zewnętrznego formatu pliku.</span><span class="sxs-lookup"><span data-stu-id="df2c1-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="df2c1-124">toofix, sprawdź, czy poprawność tabeli zewnętrznej i definicje format pliku zewnętrznego, jak i dane zewnętrzne zgodne toothese definicje.</span><span class="sxs-lookup"><span data-stu-id="df2c1-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="df2c1-125">W przypadku, gdy podzbiór rekordów danych zewnętrznych zostały zmienione, możesz wybrać tooreject te rekordy zapytań przy użyciu opcji Odrzuć hello utworzyć DDL tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="df2c1-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="df2c1-126">Ładowanie danych usługi Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="df2c1-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="df2c1-127">W tym przykładzie ładuje dane z bazy danych Data Warehouse tooSQL magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="df2c1-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="df2c1-128">Zapisywanie danych bezpośrednio usuwa hello czas transferu danych zapytań.</span><span class="sxs-lookup"><span data-stu-id="df2c1-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="df2c1-129">Przechowywanie danych z indeksem magazynu kolumn poprawia wydajność kwerendy analizy zapytań przez się too10x.</span><span class="sxs-lookup"><span data-stu-id="df2c1-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="df2c1-130">W tym przykładzie używane dane tooload instrukcji CREATE TABLE AS SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="df2c1-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="df2c1-131">Nowa tabela Hello dziedziczy hello kolumny o nazwie w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="df2c1-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="df2c1-132">W definicji tabeli zewnętrznej hello dziedziczy hello typy danych tych kolumn.</span><span class="sxs-lookup"><span data-stu-id="df2c1-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="df2c1-133">CREATE TABLE AS SELECT jest wysokiej wydajności instrukcji języka Transact-SQL, która ładuje dane hello w hello równoległych tooall obliczeniowe węzłów magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="df2c1-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="df2c1-134">Pierwotnie został opracowany dla aparatu masowego przetwarzania równoległego (MPP) hello w Analytics Platform System, a jest teraz w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df2c1-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="df2c1-135">Zobacz [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="df2c1-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="df2c1-136">Tworzenie statystyk na nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="df2c1-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="df2c1-137">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="df2c1-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="df2c1-138">W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.</span><span class="sxs-lookup"><span data-stu-id="df2c1-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="df2c1-139">Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.</span><span class="sxs-lookup"><span data-stu-id="df2c1-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="df2c1-140">Poniżej przedstawiono sposób toocreate statystyk na powitania przedłożenia załadowany w tym przykładzie przedstawiono prosty przykład.</span><span class="sxs-lookup"><span data-stu-id="df2c1-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="df2c1-141">Eksportowanie danych tooAzure obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="df2c1-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="df2c1-142">W tej sekcji przedstawiono, jak magazynu obiektów blob danych tooexport z tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df2c1-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="df2c1-143">W tym przykładzie użyto, tworzenie zewnętrznych TABLE AS SELECT czyli wysokiej wydajności języka Transact-SQL instrukcji tooexport hello danych równolegle z dowolnych węzłów obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="df2c1-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="df2c1-144">Witaj poniższy przykład tworzy tabelę zewnętrzną Weblogs2014 przy użyciu definicje kolumn i danych z dbo. Tabela dzienników sieci Web.</span><span class="sxs-lookup"><span data-stu-id="df2c1-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="df2c1-145">definicji tabeli zewnętrznej hello są przechowywane w magazynie danych SQL i wyniki hello instrukcji SELECT hello są wyeksportowanego toohello określony przez źródło danych hello kontener obiektów blob hello do katalogu "/ archiwum/log2014 /".</span><span class="sxs-lookup"><span data-stu-id="df2c1-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="df2c1-146">Witaj dane są eksportowane w formacie pliku hello określony tekst.</span><span class="sxs-lookup"><span data-stu-id="df2c1-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="df2c1-147">Izolowanie podczas ładowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="df2c1-147">Isolate Loading Users</span></span>
<span data-ttu-id="df2c1-148">Brak często toohave potrzeba wielu użytkowników, które można załadować danych do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="df2c1-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="df2c1-149">Ponieważ hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] wymaga uprawnienia kontroli hello bazy danych, spowoduje utworzenie z wieloma użytkownikami z kontroli dostępu za pośrednictwem wszystkich schematów.</span><span class="sxs-lookup"><span data-stu-id="df2c1-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="df2c1-150">toolimit, można użyć instrukcji sterowania ODMÓW hello.</span><span class="sxs-lookup"><span data-stu-id="df2c1-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="df2c1-151">Przykład: Należy wziąć pod uwagę schema_A schematów bazy danych dla działu A i schema_B dla działu B Let bazy danych użytkowników user_A i user_B można użytkowników dla ładowanie w Dział A i B, odpowiednio PolyBase.</span><span class="sxs-lookup"><span data-stu-id="df2c1-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="df2c1-152">Oba przyznano uprawnienia kontroli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="df2c1-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="df2c1-153">twórcy Hello schematu, A i B teraz zablokowanie ich schematów przy użyciu odmowy:</span><span class="sxs-lookup"><span data-stu-id="df2c1-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="df2c1-154">O tym, user_A i user_B powinna teraz zostać zablokowane z hello schematu innego działu.</span><span class="sxs-lookup"><span data-stu-id="df2c1-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="df2c1-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df2c1-155">Next steps</span></span>
<span data-ttu-id="df2c1-156">toolearn więcej informacji na temat przenoszenia tooSQL danych magazynu danych, zobacz hello [Omówienie migracji danych][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="df2c1-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
