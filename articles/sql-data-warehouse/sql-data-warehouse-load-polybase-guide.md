---
title: "Przewodnik dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="a3414-103">Przewodnik dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3414-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="a3414-104">Ten przewodnik zawiera informacje praktyczne dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3414-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="a3414-105">Aby rozpocząć, zobacz [ładowanie danych przy użyciu programu PolyBase] [ Load data with PolyBase] samouczka.</span><span class="sxs-lookup"><span data-stu-id="a3414-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="a3414-106">Obracanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="a3414-106">Rotating storage keys</span></span>
<span data-ttu-id="a3414-107">Od czasu do czasu można zmienić klucza dostępu do usługi magazynu obiektów blob ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="a3414-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="a3414-108">Najbardziej elegancki sposób wykonania tego zadania jest procedura jest znana jako "obracanie kluczy".</span><span class="sxs-lookup"><span data-stu-id="a3414-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="a3414-109">Można zauważyć ma dwa klucze magazynu dla konta magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="a3414-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="a3414-110">Jest to, aby można przejść</span><span class="sxs-lookup"><span data-stu-id="a3414-110">This is so that you can transition</span></span>

<span data-ttu-id="a3414-111">Obracanie klucze konta magazynu platformy Azure jest procesem prosty krok trzy</span><span class="sxs-lookup"><span data-stu-id="a3414-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="a3414-112">Utworzyć drugi poświadczeń o zakresie bazy danych na podstawie magazynu pomocniczego klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="a3414-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="a3414-113">Utworzyć drugi zewnętrznego źródła danych poza tym nowe poświadczenie</span><span class="sxs-lookup"><span data-stu-id="a3414-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="a3414-114">Usunąć i utworzyć tabel zewnętrznych, wskazujący nowe źródło danych zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="a3414-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="a3414-115">Po dokonaniu migracji że zewnętrzne tabel do nowego zewnętrznego źródła danych, a następnie można wykonać zadania czyszczenia:</span><span class="sxs-lookup"><span data-stu-id="a3414-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="a3414-116">Usuń pierwszy zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="a3414-116">Drop first external data source</span></span>
2. <span data-ttu-id="a3414-117">Poświadczenia magazynu podstawowy klucz dostępu w oparciu o zakresie pierwszy Porzuć bazę danych</span><span class="sxs-lookup"><span data-stu-id="a3414-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="a3414-118">Zaloguj się do platformy Azure i ponownie wygenerować podstawowy klucz dostępu gotowy do następnego</span><span class="sxs-lookup"><span data-stu-id="a3414-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="a3414-119">Zapytania na danych magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a3414-119">Query Azure blob storage data</span></span>
<span data-ttu-id="a3414-120">Zapytania dotyczące tabel zewnętrznych po prostu użyć nazwy tabeli tak, jakby był relacyjne tabeli.</span><span class="sxs-lookup"><span data-stu-id="a3414-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="a3414-121">Zapytania w tabeli zewnętrznej może zakończyć się niepowodzeniem z powodu błędu *"zapytanie zostało przerwane — Osiągnięto próg maksymalnej Odrzuć podczas odczytu z zewnętrznego źródła"*.</span><span class="sxs-lookup"><span data-stu-id="a3414-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="a3414-122">Oznacza to, że dane zewnętrzne zawiera *zanieczyszczone* rekordów.</span><span class="sxs-lookup"><span data-stu-id="a3414-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="a3414-123">Rekord danych jest uznawany za "zakłócone", jeśli dane rzeczywiste typy/liczba kolumn nie są zgodne z definicji kolumn tabeli zewnętrznej lub nie jest zgodny z określonego pliku zewnętrznego formatu danych.</span><span class="sxs-lookup"><span data-stu-id="a3414-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="a3414-124">Aby rozwiązać ten problem, sprawdź poprawność tabeli zewnętrznej i definicje format pliku zewnętrznego i zgodne dane zewnętrzne z tych definicji.</span><span class="sxs-lookup"><span data-stu-id="a3414-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="a3414-125">W przypadku, gdy podzbiór rekordów danych zewnętrznych zostały zmienione, można odrzucić tych rekordów dla zapytania przy użyciu opcji Odrzuć utworzyć DDL tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="a3414-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="a3414-126">Ładowanie danych usługi Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a3414-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="a3414-127">W tym przykładzie ładuje dane z magazynu obiektów blob platformy Azure do bazy danych magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a3414-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="a3414-128">Zapisywanie danych bezpośrednio usuwa czas transferu danych zapytań.</span><span class="sxs-lookup"><span data-stu-id="a3414-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="a3414-129">Przechowywanie danych z indeksem magazynu kolumn poprawia wydajność kwerend analizy zapytań przez maksymalnie 10 x.</span><span class="sxs-lookup"><span data-stu-id="a3414-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="a3414-130">W tym przykładzie używa instrukcji CREATE TABLE AS SELECT do wczytywania danych.</span><span class="sxs-lookup"><span data-stu-id="a3414-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="a3414-131">Nowa tabela dziedziczy kolumny o nazwie w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="a3414-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="a3414-132">Typy danych tych kolumn dziedziczy z definicji tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="a3414-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="a3414-133">CREATE TABLE AS SELECT jest wysokiej wydajności instrukcji języka Transact-SQL, który ładuje dane jednocześnie do wszystkich węzłów obliczeniowych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3414-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="a3414-134">Pierwotnie został opracowany dla aparatu masowego przetwarzania równoległego (MPP) w Analytics Platform System, a jest teraz w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3414-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="a3414-135">Zobacz [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="a3414-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="a3414-136">Tworzenie statystyk na nowo załadowanych danych</span><span class="sxs-lookup"><span data-stu-id="a3414-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="a3414-137">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="a3414-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="a3414-138">W celu uzyskania najlepszej wydajności zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu danych, a następnie po każdej istotnej zmianie.</span><span class="sxs-lookup"><span data-stu-id="a3414-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="a3414-139">Szczegółowy opis statystyk znajduje się w temacie [Statystyki][Statistics] w grupie artykułów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="a3414-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="a3414-140">Poniżej przedstawiono prosty przykład tworzenia statystyk dotyczących tabeli załadowanej w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a3414-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="a3414-141">Eksportuj dane do magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a3414-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="a3414-142">W tej sekcji przedstawiono sposób eksportowania danych z magazynu danych SQL do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3414-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="a3414-143">W tym przykładzie użyto, tworzenie zewnętrznych TABLE AS SELECT czyli wysokiej wydajności instrukcję Transact-SQL, aby wyeksportować dane równolegle z węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="a3414-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="a3414-144">Poniższy przykład tworzy tabelę zewnętrzną Weblogs2014 przy użyciu definicje kolumn i danych z dbo. Tabela dzienników sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a3414-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="a3414-145">W definicji tabeli zewnętrznej jest przechowywany w usłudze SQL Data Warehouse i wyników w instrukcji SELECT są eksportowane do katalogu "/ archiwum/log2014 /" w kontenerze obiektów blob, określony przez źródło danych.</span><span class="sxs-lookup"><span data-stu-id="a3414-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="a3414-146">Dane są eksportowane w formacie pliku określony tekst.</span><span class="sxs-lookup"><span data-stu-id="a3414-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="a3414-147">Izolowanie podczas ładowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="a3414-147">Isolate Loading Users</span></span>
<span data-ttu-id="a3414-148">Często jest potrzeba wielu użytkowników, które można załadować danych do magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a3414-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="a3414-149">Ponieważ [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] wymaga uprawnienia kontroli bazy danych, spowoduje utworzenie z wieloma użytkownikami z kontroli dostępu za pośrednictwem wszystkich schematów.</span><span class="sxs-lookup"><span data-stu-id="a3414-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="a3414-150">To ograniczenie, można użyć instrukcji sterowania ODMÓW.</span><span class="sxs-lookup"><span data-stu-id="a3414-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="a3414-151">Przykład: Należy wziąć pod uwagę schema_A schematów bazy danych dla działu A i schema_B dla działu B Let bazy danych użytkowników user_A i user_B można użytkowników dla ładowanie w Dział A i B, odpowiednio PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a3414-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="a3414-152">Oba przyznano uprawnienia kontroli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a3414-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="a3414-153">Twórcy blokady teraz A i B schematu w dół ich schematów przy użyciu odmowy:</span><span class="sxs-lookup"><span data-stu-id="a3414-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="a3414-154">O tym user_A i user_B powinna teraz zostać zablokowane ze schematu innego działu.</span><span class="sxs-lookup"><span data-stu-id="a3414-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="a3414-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3414-155">Next steps</span></span>
<span data-ttu-id="a3414-156">Aby dowiedzieć się więcej na temat przenoszenia danych do usługi SQL Data Warehouse, zobacz [Omówienie migracji danych][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="a3414-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
