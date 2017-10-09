---
title: "aaaDesign wskazówki dotyczące zreplikowane tabele - Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówek dotyczących projektowania zreplikowane tabele w schemat magazyn danych SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="2396b-103">Wskazówki dotyczące projektowania dotyczące używania zreplikowane tabele w magazynie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="2396b-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="2396b-104">Ten artykuł zawiera zalecenia dotyczące projektowania zreplikowanych tabel w schematu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2396b-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="2396b-105">Aby użyć wydajność zapytań tooimprove te zalecenia zmniejsza się złożoność danych przemieszczania i zapytań.</span><span class="sxs-lookup"><span data-stu-id="2396b-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="2396b-106">Funkcja zreplikowanej tabeli Hello jest obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="2396b-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="2396b-107">Niektóre zachowania są toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="2396b-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="2396b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2396b-108">Prerequisites</span></span>
<span data-ttu-id="2396b-109">W tym artykule przyjęto założenie, że znasz z danych dystrybucji i koncepcje przepływu danych w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2396b-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="2396b-110">Aby uzyskać więcej informacji, zobacz [rozproszonych danych](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="2396b-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="2396b-111">W ramach projektowaniu tabel Dowiedz się, jak to możliwe danych i jak danych hello jest poddawany kwerendzie.</span><span class="sxs-lookup"><span data-stu-id="2396b-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="2396b-112">Na przykład wziąć pod uwagę następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="2396b-112">For example, consider these questions:</span></span>

- <span data-ttu-id="2396b-113">Jak duże jest tabela hello?</span><span class="sxs-lookup"><span data-stu-id="2396b-113">How large is hello table?</span></span>   
- <span data-ttu-id="2396b-114">Częstotliwość odświeżania tabeli hello?</span><span class="sxs-lookup"><span data-stu-id="2396b-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="2396b-115">Tabele faktów i wymiarów są dostępne w magazynie danych?</span><span class="sxs-lookup"><span data-stu-id="2396b-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="2396b-116">Co to jest zreplikowanej tabeli?</span><span class="sxs-lookup"><span data-stu-id="2396b-116">What is a replicated table?</span></span>
<span data-ttu-id="2396b-117">Zreplikowanej tabeli ma pełną kopię tabeli hello jest dostępny w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="2396b-118">Replikowanie tabeli usuwa hello potrzeby tootransfer danych między węzłami obliczeniowymi przed join lub agregacji.</span><span class="sxs-lookup"><span data-stu-id="2396b-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="2396b-119">Ponieważ hello tabela ma wiele kopii, zreplikowanych tabelach działają najlepiej, gdy rozmiar tabeli hello jest mniejszy niż 2 GB skompresowane.</span><span class="sxs-lookup"><span data-stu-id="2396b-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="2396b-120">Witaj Poniższy diagram przedstawia zreplikowanej tabeli, która jest dostępna w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="2396b-121">W usłudze SQL Data Warehouse zreplikowanej tabeli hello jest bazy danych dystrybucji tooa całkowicie skopiowane na każdym węźle obliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="2396b-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="2396b-122">![Tabela zreplikowane](media/guidance-for-using-replicated-tables/replicated-table.png "zreplikowane tabeli")</span><span class="sxs-lookup"><span data-stu-id="2396b-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="2396b-123">Replikowane tabele pracy efektywne w przypadku tabel wymiarów małych w schemat gwiazdy.</span><span class="sxs-lookup"><span data-stu-id="2396b-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="2396b-124">Tabele wymiarów zwykle mają rozmiar, dzięki którym możliwe toostore i obsługa wielu kopii.</span><span class="sxs-lookup"><span data-stu-id="2396b-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="2396b-125">Wymiary przechowywać opisowe dane, które zmienia się powoli, takie jak nazwa klienta i adresem i szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2396b-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="2396b-126">Hello powoli zmiana rodzaju danych hello prowadzi toofewer odbudowuje hello zreplikowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="2396b-127">Należy rozważyć użycie zreplikowanej tabeli, gdy:</span><span class="sxs-lookup"><span data-stu-id="2396b-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="2396b-128">rozmiar tabeli Hello na dysku jest mniejszy niż 2 GB, niezależnie od hello liczbę wierszy.</span><span class="sxs-lookup"><span data-stu-id="2396b-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="2396b-129">rozmiar hello toofind tabeli, można użyć hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) polecenia: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="2396b-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="2396b-130">Tabela Hello jest używana w sprzężeniu, które w przeciwnym razie wymaga przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2396b-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="2396b-131">Na przykład sprzężenia w tabelach rozpowszechniane skrót wymaga przenoszenia danych, gdy hello łącząca kolumn nie są hello tej samej kolumnie dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2396b-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="2396b-132">Jedną z tabel rozpowszechniane skrót hello jest mały, należy wziąć pod uwagę zreplikowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="2396b-133">Sprzężenia w tabeli okrężnego wymaga przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2396b-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="2396b-134">Zalecamy używanie zamiast okrężnego tabel w większości przypadków zreplikowanych tabelach.</span><span class="sxs-lookup"><span data-stu-id="2396b-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="2396b-135">Należy wziąć pod uwagę Konwertowanie istniejącej rozproszonej tooa tabeli replikowane tabeli, gdy:</span><span class="sxs-lookup"><span data-stu-id="2396b-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="2396b-136">Zapytanie plany operacje przenoszenia danych użycia, które emisji węzły obliczeniowe hello tooall danych hello.</span><span class="sxs-lookup"><span data-stu-id="2396b-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="2396b-137">Hello BroadcastMoveOperation jest kosztowne i zmniejsza wydajność kwerend.</span><span class="sxs-lookup"><span data-stu-id="2396b-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="2396b-138">Użyj tooview operacje przenoszenia danych w planie zapytania [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="2396b-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="2396b-139">Zreplikowane tabele nie mogą użyć instrukcji yield hello najlepszą wydajność zapytań po:</span><span class="sxs-lookup"><span data-stu-id="2396b-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="2396b-140">Tabela Hello ma częste wstawiania, aktualizowania i usuwania działań.</span><span class="sxs-lookup"><span data-stu-id="2396b-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="2396b-141">Te operacje języka manipulacji danych wymaga odbudowania hello replikowane tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="2396b-142">Ponowne kompilowanie często powodują mniejszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="2396b-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="2396b-143">Magazyn danych Hello jest skalowana często.</span><span class="sxs-lookup"><span data-stu-id="2396b-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="2396b-144">Skalowanie hurtowni danych zmienia hello liczbę węzłów obliczeniowych, co wiąże się z odbudowie.</span><span class="sxs-lookup"><span data-stu-id="2396b-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="2396b-145">Tabela Hello ma dużą liczbę kolumn, ale operacje na danych zwykle uzyskują dostęp do niewielkiej liczby kolumn.</span><span class="sxs-lookup"><span data-stu-id="2396b-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="2396b-146">W tym scenariuszu, zamiast replikować całą tabelę hello, może być toohash bardziej efektywnej dystrybucji hello tabeli, a następnie utworzyć indeks kolumny hello często używane.</span><span class="sxs-lookup"><span data-stu-id="2396b-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="2396b-147">Gdy zapytanie wymaga przenoszenia danych, Magazyn danych SQL tylko przenosi dane w hello żądanej kolumny.</span><span class="sxs-lookup"><span data-stu-id="2396b-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="2396b-148">Zreplikowane tabele za pomocą prostego zapytania predykatów</span><span class="sxs-lookup"><span data-stu-id="2396b-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="2396b-149">Przed wybierz toodistribute lub replikacji tabeli, należy zastanowić hello typy zapytań, które mają toorun hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="2396b-150">Jeśli to możliwe,</span><span class="sxs-lookup"><span data-stu-id="2396b-150">Whenever possible,</span></span>

- <span data-ttu-id="2396b-151">Użyj zreplikowanych tabel dla zapytań z predykaty prostego zapytania, takie jak równości i nierówności.</span><span class="sxs-lookup"><span data-stu-id="2396b-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="2396b-152">Użyj tabel rozproszone dla zapytań z predykaty złożonego zapytania, takie jak podobne lub nie, takich jak.</span><span class="sxs-lookup"><span data-stu-id="2396b-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="2396b-153">Użycie Procesora CPU zapytania wykonywane najlepiej, jeśli praca hello jest dystrybuowana do wszystkich węzłów obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="2396b-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="2396b-154">Na przykład zapytania uruchamiane obliczenia w każdym wierszu tabeli działać lepiej w tabelach rozproszonej niż zreplikowanych tabelach.</span><span class="sxs-lookup"><span data-stu-id="2396b-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="2396b-155">Ponieważ zreplikowanej tabeli są przechowywane w całości w każdym węźle obliczeń, użycie Procesora CPU zapytanie zreplikowanej tabeli jest uruchamiana dla całej tabeli hello w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="2396b-156">Hello dodatkowe obliczeń może zmniejszyć wydajność wykonywania zapytań.</span><span class="sxs-lookup"><span data-stu-id="2396b-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="2396b-157">Na przykład ta kwerenda zawiera złożone predykatu.</span><span class="sxs-lookup"><span data-stu-id="2396b-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="2396b-158">Uruchamia szybciej gdy dostawca jest tabela rozproszona zamiast zreplikowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="2396b-159">W tym przykładzie dostawcy mogą być dystrybuowane wyznaczania wartości skrótu, albo rozproszone okrężnego.</span><span class="sxs-lookup"><span data-stu-id="2396b-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="2396b-160">Konwertowanie istniejących tabel tooreplicated tabel okrężnego</span><span class="sxs-lookup"><span data-stu-id="2396b-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="2396b-161">Jeśli masz już okrężnego tabel, zaleca się ich konwertowania tooreplicated tabel, gdy spełniają kryteria opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2396b-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="2396b-162">Zreplikowane tabele zwiększyć wydajność w przypadku tabel okrężnego, ponieważ eliminuje konieczność hello przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2396b-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="2396b-163">Tabela okrężnego zawsze wymaga przenoszenia danych sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="2396b-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="2396b-164">W tym przykładzie użyto [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabeli tooa replikowane tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="2396b-165">W tym przykładzie działa niezależnie od tego, czy DimSalesTerritory rozpowszechniane skrót lub okrężnego.</span><span class="sxs-lookup"><span data-stu-id="2396b-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="2396b-166">Przykład wydajności kwerendy okrężnego i replikowane</span><span class="sxs-lookup"><span data-stu-id="2396b-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="2396b-167">Zreplikowanej tabeli nie wymaga przenoszenia żadnych danych dla sprzężeń, ponieważ hello cała tabela jest już obecny w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="2396b-168">Jeśli tabele wymiarów hello okrężnego rozproszonych, sprzężenia kopiuje hello tabeli wymiarów w węźle obliczeń tooeach pełna.</span><span class="sxs-lookup"><span data-stu-id="2396b-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="2396b-169">dane hello toomove, hello planu zapytania zawiera operacji o nazwie BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="2396b-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="2396b-170">Ten typ operacji przenoszenia danych zmniejsza wydajność zapytań i wyeliminowania przy użyciu zreplikowanych tabelach.</span><span class="sxs-lookup"><span data-stu-id="2396b-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="2396b-171">tooview kroki planu zapytania, użyj hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) widoku wykazu systemu.</span><span class="sxs-lookup"><span data-stu-id="2396b-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="2396b-172">Na przykład, w następującej kwerendy względem schematu AdventureWorks hello hello ` FactInternetSales` tabela jest dystrybuowane wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="2396b-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="2396b-173">Witaj `DimDate` i `DimSalesTerritory` tabele są mniejsze tabele wymiarów.</span><span class="sxs-lookup"><span data-stu-id="2396b-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="2396b-174">Ta kwerenda zwraca hello sprzedaży w Ameryce Północnej, dla roku obrachunkowego 2004:</span><span class="sxs-lookup"><span data-stu-id="2396b-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="2396b-175">Ponownie utworzono `DimDate` i `DimSalesTerritory` jako tabele okrężnego.</span><span class="sxs-lookup"><span data-stu-id="2396b-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="2396b-176">W związku z tym hello zapytania wykazało hello planu zapytania, który ma wiele emisji operacje są przenoszone z następujących:</span><span class="sxs-lookup"><span data-stu-id="2396b-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Plan zapytania okrężnego](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="2396b-178">Ponownie utworzono `DimDate` i `DimSalesTerritory` jako zreplikowane tabele i ponownie uruchomiono hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="2396b-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="2396b-179">Wynikowa planu zapytania Hello jest znacznie krótszy i nie ma żadnego emituje przenosi.</span><span class="sxs-lookup"><span data-stu-id="2396b-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Replikowane planu zapytania](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="2396b-181">Zagadnienia dotyczące wydajności modyfikowania zreplikowanych tabelach</span><span class="sxs-lookup"><span data-stu-id="2396b-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="2396b-182">Usługa SQL Data Warehouse implementuje zreplikowanej tabeli dzięki utrzymywaniu głównej wersji hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="2396b-183">Kopiuje bazy danych dystrybucji tooone głównej wersji hello w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="2396b-184">W przypadku zmiany SQL Data Warehouse najpierw aktualizuje hello wzorcowej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="2396b-185">Następnie wymaga odbudowania hello tabel w każdym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="2396b-186">Kompilowania zreplikowanej tabeli obejmuje kopiowanie węzeł obliczeniowy tooeach hello w tabeli, a następnie odbudowanie hello indeksów.</span><span class="sxs-lookup"><span data-stu-id="2396b-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="2396b-187">Odtwarza są wymagane po:</span><span class="sxs-lookup"><span data-stu-id="2396b-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="2396b-188">Dane są ładowane lub zmodyfikowane</span><span class="sxs-lookup"><span data-stu-id="2396b-188">Data is loaded or modified</span></span>
- <span data-ttu-id="2396b-189">Hello data warehouse jest skalowaną tooa różnych wartości DWU ustawienia</span><span class="sxs-lookup"><span data-stu-id="2396b-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="2396b-190">Definicja tabeli jest aktualizowany</span><span class="sxs-lookup"><span data-stu-id="2396b-190">Table definition is updated</span></span>

<span data-ttu-id="2396b-191">Odtwarza nie są wymagane po:</span><span class="sxs-lookup"><span data-stu-id="2396b-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="2396b-192">Operację wstrzymywania</span><span class="sxs-lookup"><span data-stu-id="2396b-192">Pause operation</span></span>
- <span data-ttu-id="2396b-193">Wznawia działania</span><span class="sxs-lookup"><span data-stu-id="2396b-193">Resume operation</span></span>

<span data-ttu-id="2396b-194">Odbuduj Hello nie odbywa się natychmiast po zmodyfikowaniu danych.</span><span class="sxs-lookup"><span data-stu-id="2396b-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="2396b-195">Zamiast tego wyzwoleniu odbudowy hello hello wybiera zapytania z tabeli powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="2396b-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="2396b-196">W ramach początkowego instrukcji select hello z tabeli hello są kroki toorebuild hello zreplikowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="2396b-197">Ponieważ Odbuduj hello jest wykonywana w ramach zapytania hello, początkowego instrukcji select hello wpływ toohello może być istotne w zależności od wielkości hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="2396b-198">Jeśli wiele zreplikowanych tabelach są zaangażowane wymagające kompilowania, każda kopia zostanie odtworzony pojedynczo jako kroków w ramach instrukcji hello.</span><span class="sxs-lookup"><span data-stu-id="2396b-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="2396b-199">spójność danych toomaintain podczas kompilowania hello hello replikowane wyłącznej blokady jest wykonywana na tabeli hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="2396b-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="2396b-200">Blokada Hello zapobiega wszystkich tabeli toohello dostępu na czas trwania hello hello odbudowy.</span><span class="sxs-lookup"><span data-stu-id="2396b-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="2396b-201">Użyj konserwatywnie indeksów</span><span class="sxs-lookup"><span data-stu-id="2396b-201">Use indexes conservatively</span></span>
<span data-ttu-id="2396b-202">Rozwiązania w zakresie indeksowania standardowe mają zastosowanie tooreplicated tabel.</span><span class="sxs-lookup"><span data-stu-id="2396b-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="2396b-203">Usługi SQL Data Warehouse odbudowuje każdy indeks zreplikowanej tabeli jako część hello ponownej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2396b-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="2396b-204">Indeksy należy używać tylko w przypadku bardziej wydajne hello podejścia są większe niż koszty hello ponowne tworzenie indeksów hello.</span><span class="sxs-lookup"><span data-stu-id="2396b-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="2396b-205">Ilości danych w partii</span><span class="sxs-lookup"><span data-stu-id="2396b-205">Batch data loads</span></span>
<span data-ttu-id="2396b-206">Podczas ładowania danych w zreplikowanych tabelach, spróbuj odtwarza toominimize razem przetwarzanie wsadowe obciążeń.</span><span class="sxs-lookup"><span data-stu-id="2396b-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="2396b-207">Wykonaj wszystkie obciążenia hello umieścić w zadaniu wsadowym przed uruchomieniem instrukcji "select".</span><span class="sxs-lookup"><span data-stu-id="2396b-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="2396b-208">Na przykład tego wzorca obciążenia ładuje dane z czterech źródeł i wywołuje cztery odtwarza.</span><span class="sxs-lookup"><span data-stu-id="2396b-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="2396b-209">Załaduj ze źródła 1.</span><span class="sxs-lookup"><span data-stu-id="2396b-209">Load from source 1.</span></span>
- <span data-ttu-id="2396b-210">Instrukcja SELECT wyzwalaczy odbudować 1.</span><span class="sxs-lookup"><span data-stu-id="2396b-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="2396b-211">Załaduj ze źródła 2.</span><span class="sxs-lookup"><span data-stu-id="2396b-211">Load from source 2.</span></span>
- <span data-ttu-id="2396b-212">Instrukcja SELECT wyzwalaczy odbudować 2.</span><span class="sxs-lookup"><span data-stu-id="2396b-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="2396b-213">Załaduj ze źródła 3.</span><span class="sxs-lookup"><span data-stu-id="2396b-213">Load from source 3.</span></span>
- <span data-ttu-id="2396b-214">Instrukcja SELECT wyzwalaczy odbudować 3.</span><span class="sxs-lookup"><span data-stu-id="2396b-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="2396b-215">Załaduj ze źródła 4.</span><span class="sxs-lookup"><span data-stu-id="2396b-215">Load from source 4.</span></span>
- <span data-ttu-id="2396b-216">Instrukcja SELECT wyzwalaczy odbudować 4.</span><span class="sxs-lookup"><span data-stu-id="2396b-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="2396b-217">Na przykład tego wzorca obciążenia ładuje z czterech źródeł danych, ale tylko wywołuje jeden ponownej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2396b-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="2396b-218">Załaduj ze źródła 1.</span><span class="sxs-lookup"><span data-stu-id="2396b-218">Load from source 1.</span></span>
- <span data-ttu-id="2396b-219">Załaduj ze źródła 2.</span><span class="sxs-lookup"><span data-stu-id="2396b-219">Load from source 2.</span></span>
- <span data-ttu-id="2396b-220">Załaduj ze źródła 3.</span><span class="sxs-lookup"><span data-stu-id="2396b-220">Load from source 3.</span></span>
- <span data-ttu-id="2396b-221">Załaduj ze źródła 4.</span><span class="sxs-lookup"><span data-stu-id="2396b-221">Load from source 4.</span></span>
- <span data-ttu-id="2396b-222">Odbuduj wyzwalaczy instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="2396b-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="2396b-223">Odbuduj zreplikowanej tabeli po załadowaniu partii</span><span class="sxs-lookup"><span data-stu-id="2396b-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="2396b-224">czas wykonywania zapytania spójne tooensure, zaleca się wymuszanie odświeżania tabel hello replikowane po załadowaniu partii.</span><span class="sxs-lookup"><span data-stu-id="2396b-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="2396b-225">W przeciwnym razie hello pierwszego zapytania należy poczekać hello toorefresh tabel, która obejmuje ponowne tworzenie indeksów hello.</span><span class="sxs-lookup"><span data-stu-id="2396b-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="2396b-226">W zależności od rozmiaru hello i liczby zreplikowanych tabel, których to dotyczy hello wpływ na wydajność może być istotne.</span><span class="sxs-lookup"><span data-stu-id="2396b-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="2396b-227">To zapytanie używa hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello zreplikowane tabele, które zostały zmodyfikowane, ale nie został odbudowany.</span><span class="sxs-lookup"><span data-stu-id="2396b-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="2396b-228">tooforce kompilowania, uruchom powitania po instrukcji w każdej tabeli w hello poprzedzających danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2396b-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="2396b-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2396b-229">Next steps</span></span> 
<span data-ttu-id="2396b-230">toocreate zreplikowanej tabeli, użyj jednej z tych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="2396b-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="2396b-231">Utwórz tabelę (magazyn danych Azure SQL)</span><span class="sxs-lookup"><span data-stu-id="2396b-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="2396b-232">Utwórz TABLE AS SELECT (magazyn danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="2396b-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="2396b-233">Omówienie rozproszonej tabel, zobacz [rozproszonych tabel](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="2396b-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



