---
title: "Dystrybucja tabel w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do korzystania z dystrybucji tabel w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="02e49-103">Dystrybucja tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="02e49-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="02e49-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="02e49-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="02e49-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="02e49-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="02e49-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="02e49-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="02e49-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="02e49-107">[Index][Index]</span></span>
> * <span data-ttu-id="02e49-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="02e49-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="02e49-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="02e49-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="02e49-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="02e49-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="02e49-111">Usługa SQL Data Warehouse to system rozproszonych baz danych o architekturze masowego przetwarzana równoległego (MPP).</span><span class="sxs-lookup"><span data-stu-id="02e49-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="02e49-112">Dzieląc dane i możliwości przetwarzania między wiele węzłów, usługa SQL Data Warehouse może zaoferować bardzo dużą skalowalność — znacznie większą niż w przypadku jakiegokolwiek pojedynczego systemu.</span><span class="sxs-lookup"><span data-stu-id="02e49-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="02e49-113">Przy wyborze sposobu dystrybucji danych w magazynie danych programu SQL jest jednym z najważniejszych czynników do osiągnięcia optymalnej wydajności.</span><span class="sxs-lookup"><span data-stu-id="02e49-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="02e49-114">Klucz do uzyskania optymalnej wydajności to zminimalizowanie przenoszenia danych i z kolei wybiera strategii dystrybucji prawy klawisz, aby zminimalizować przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="02e49-115">Opis przenoszenia danych</span><span class="sxs-lookup"><span data-stu-id="02e49-115">Understanding data movement</span></span>
<span data-ttu-id="02e49-116">W systemie MPP danych z każdej tabeli jest dzielona między kilka podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="02e49-117">Najbardziej zoptymalizowane zapytania w systemie MPP można po prostu przekazywane do wykonania na pojedyncze rozproszonej bazy danych bez interakcji między bazami danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="02e49-118">Załóżmy na przykład, że masz bazę danych danymi sprzedaży zawiera dwie tabele, sprzedaży i klientów.</span><span class="sxs-lookup"><span data-stu-id="02e49-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="02e49-119">Jeśli zapytanie, które należy dołączyć sprzedaży tabeli do tabeli klientów i dzielenia sprzedaży i tabele klienta się przez numer klienta umieszczanie każdego klienta w oddzielnej bazy danych, można rozwiązać żadnych zapytań, które przyłączyć sprzedaży i klienta, w każdej bazie danych z żadnych informacji na temat innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="02e49-120">Z kolei danych sprzedaży rozdzielonych numer zamówienia i danych klienta przez numer klienta, następnie wszystkie danego bazy danych nie będzie zawierał odpowiednie dane dla każdego klienta, dlatego jeśli chcesz dołączyć sprzedaży danych do danych klienta, należy pobrać danych dla każdego klienta z innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="02e49-121">W drugim przykładzie przepływu danych musi wystąpić przenoszenia danych klienta z danymi sprzedaży, dzięki czemu można łączyć dwie tabele.</span><span class="sxs-lookup"><span data-stu-id="02e49-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="02e49-122">Przenoszenie danych zawsze jest zły element, czasami jest niezbędne dla rozwiązania zapytania.</span><span class="sxs-lookup"><span data-stu-id="02e49-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="02e49-123">Jednak podczas tego dodatkowego kroku można uniknąć, naturalny zapytanie będzie szybsze.</span><span class="sxs-lookup"><span data-stu-id="02e49-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="02e49-124">Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="02e49-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="02e49-125">Często należy wykonać, więc może być może zoptymalizować na jednym ze scenariuszy, takich jak sprzężenia, należy nadal przenoszenia danych, aby rozwiązać inne scenariusza, takich jak agregacji.</span><span class="sxs-lookup"><span data-stu-id="02e49-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="02e49-126">Lewy jest ustaleniem, czyli mniej pracy.</span><span class="sxs-lookup"><span data-stu-id="02e49-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="02e49-127">W większości przypadków dystrybucja tabele faktów dużych często dołączonego do kolumny jest najbardziej efektywną metodę zmniejszenia większości przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="02e49-128">Dystrybucja danych na kolumn sprzężenia jest bardziej powszechnie używaną metodą Aby zmniejszyć przenoszenia danych niż dystrybucji danych kolumn uczestniczących w agregacji.</span><span class="sxs-lookup"><span data-stu-id="02e49-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="02e49-129">Wybieranie metody dystrybucji</span><span class="sxs-lookup"><span data-stu-id="02e49-129">Select distribution method</span></span>
<span data-ttu-id="02e49-130">Magazyn danych SQL w tle dzieli dane 60 baz danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="02e49-131">Każdy jedna baza danych jest określany jako **dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="02e49-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="02e49-132">Po załadowaniu danych w każdej tabeli SQL Data Warehouse musi znać sposób podziału danych w tych 60 dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="02e49-133">Metoda dystrybucji jest zdefiniowana na poziomie tabeli, a obecnie dostępne są dwie możliwości:</span><span class="sxs-lookup"><span data-stu-id="02e49-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="02e49-134">**Działanie okrężne** który równomiernie, ale losowo dystrybucji danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="02e49-135">**Skrótów rozproszone** która dystrybuuje oparte na tworzenie skrótów wartości z jednej kolumny danych</span><span class="sxs-lookup"><span data-stu-id="02e49-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="02e49-136">Domyślnie, gdy metoda dystrybucji danych, nie zostaną zdefiniowane tabeli będą dystrybuowane za pomocą **działanie okrężne** metoda dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="02e49-137">Jednak jak staje się bardziej złożone w implementacji, należy rozważyć użycie **rozpowszechniane skrót** tabele, aby zminimalizować przenoszenia danych, który z kolei zoptymalizuje kwerendy wydajności.</span><span class="sxs-lookup"><span data-stu-id="02e49-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="02e49-138">Działanie okrężne tabel</span><span class="sxs-lookup"><span data-stu-id="02e49-138">Round Robin Tables</span></span>
<span data-ttu-id="02e49-139">Przy użyciu metody okrężne dystrybucji danych jest znacznie, jak ich wymowy.</span><span class="sxs-lookup"><span data-stu-id="02e49-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="02e49-140">Jak Twoje dane są ładowane, każdy wiersz po prostu są wysyłane do dystrybucji dalej.</span><span class="sxs-lookup"><span data-stu-id="02e49-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="02e49-141">Ta metoda dystrybucji danych będzie zawsze losowo równomierne danych bardzo we wszystkich dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="02e49-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="02e49-142">Oznacza to, że istnieje sortowania nie wykonywane podczas procesu działanie okrężne, który umieszcza dane.</span><span class="sxs-lookup"><span data-stu-id="02e49-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="02e49-143">Działanie okrężne dystrybucji jest niekiedy nazywany losowego wyznaczania wartości skrótu z tego powodu.</span><span class="sxs-lookup"><span data-stu-id="02e49-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="02e49-144">Z tabelą rozproszonej okrężnego jest niepotrzebna, aby zrozumieć dane.</span><span class="sxs-lookup"><span data-stu-id="02e49-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="02e49-145">Z tego powodu tabel okrężnego należy często dobrym ładowanie obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="02e49-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="02e49-146">Domyślnie, jeśli wybrano opcję Brak metody dystrybucji, działanie okrężne dystrybucji zostanie użyta metoda.</span><span class="sxs-lookup"><span data-stu-id="02e49-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="02e49-147">Jednak działanie okrężne tabele są łatwe w użyciu, ponieważ danych losowo jest dystrybuowana do systemu, oznacza to, że system nie może zagwarantować, które dystrybucji każdy wiersz jest na.</span><span class="sxs-lookup"><span data-stu-id="02e49-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="02e49-148">W związku z tym system musi czasami do wywołania operacji przepływu danych w celu lepszej organizacji danych przed może rozpoznać zapytania.</span><span class="sxs-lookup"><span data-stu-id="02e49-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="02e49-149">Ten krok dodatkowe może to spowolnić zapytań.</span><span class="sxs-lookup"><span data-stu-id="02e49-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="02e49-150">Rozważ użycie dystrybucji okrężnego dla tej tabeli w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="02e49-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="02e49-151">Gdy wprowadzenie jako punktu wyjścia proste</span><span class="sxs-lookup"><span data-stu-id="02e49-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="02e49-152">Jeśli oczywiste łącząca klucz nie istnieje</span><span class="sxs-lookup"><span data-stu-id="02e49-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="02e49-153">Jeśli nie ma kolumny odpowiednimi kandydatami do wyznaczania wartości skrótu dystrybucji tabeli</span><span class="sxs-lookup"><span data-stu-id="02e49-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="02e49-154">Jeśli tabela nie udostępniane wspólny klucz sprzężenia innych tabel</span><span class="sxs-lookup"><span data-stu-id="02e49-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="02e49-155">Jeśli sprzężenie jest mniej istotna niż inne sprzężeń w zapytaniu</span><span class="sxs-lookup"><span data-stu-id="02e49-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="02e49-156">Gdy jest tymczasowe Tabela przemieszczania</span><span class="sxs-lookup"><span data-stu-id="02e49-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="02e49-157">Oba te przykłady spowoduje utworzenie tabeli działanie okrężne:</span><span class="sxs-lookup"><span data-stu-id="02e49-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="02e49-158">Gdy jest działanie okrężne domyślny typ tabeli jest jawne w kod DDL jest traktowany jako najlepszym rozwiązaniem tak, aby były wyczyść innym zamiarach układu tabeli.</span><span class="sxs-lookup"><span data-stu-id="02e49-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="02e49-159">Rozproszone tabele hash</span><span class="sxs-lookup"><span data-stu-id="02e49-159">Hash Distributed Tables</span></span>
<span data-ttu-id="02e49-160">Przy użyciu **rozpowszechniane skrót** algorytmu do dystrybucji tabel może poprawić wydajność w różnych scenariuszach ograniczając przenoszenie danych w czasie zapytania.</span><span class="sxs-lookup"><span data-stu-id="02e49-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="02e49-161">Tabele hash rozproszone są tabele, które są dzielone między rozproszonej bazy danych przy użyciu algorytmu wyznaczania wartości skrótu w jednej kolumnie, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="02e49-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="02e49-162">Kolumna dystrybucji jest, co określa sposób podziału danych w sieci rozproszonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="02e49-163">Funkcja skrótu używa kolumny dystrybucji można przypisać podziału wierszy.</span><span class="sxs-lookup"><span data-stu-id="02e49-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="02e49-164">Algorytm wyznaczania wartości skrótu i wynikowy dystrybucji jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="02e49-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="02e49-165">To już taką samą wartość, tym samym typie danych będzie zawsze ma do tego samego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="02e49-166">W tym przykładzie utworzy rozproszone na identyfikator tabeli:</span><span class="sxs-lookup"><span data-stu-id="02e49-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="02e49-167">Wybierz kolumnę dystrybucji</span><span class="sxs-lookup"><span data-stu-id="02e49-167">Select distribution column</span></span>
<span data-ttu-id="02e49-168">Jeśli zdecydujesz się **skrótu dystrybucji** tabelę, musisz wybrać kolumnę pojedynczego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="02e49-169">Podczas wybierania kolumn dystrybucji, istnieją trzy główne czynniki, które należy wziąć pod uwagę.</span><span class="sxs-lookup"><span data-stu-id="02e49-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="02e49-170">Wybrać pojedynczą kolumnę, która będzie:</span><span class="sxs-lookup"><span data-stu-id="02e49-170">Select a single column which will:</span></span>

1. <span data-ttu-id="02e49-171">Nie można zaktualizować</span><span class="sxs-lookup"><span data-stu-id="02e49-171">Not be updated</span></span>
2. <span data-ttu-id="02e49-172">Równomierne danych, unikając pochylenia danych</span><span class="sxs-lookup"><span data-stu-id="02e49-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="02e49-173">Minimalizowanie przepływu danych</span><span class="sxs-lookup"><span data-stu-id="02e49-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="02e49-174">Wybierz kolumnę dystrybucji, które nie zostaną zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="02e49-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="02e49-175">Kolumny dystrybucji nie są aktualizowalne, w związku z tym, wybierz kolumnę o wartości statyczne.</span><span class="sxs-lookup"><span data-stu-id="02e49-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="02e49-176">Jeśli kolumna zostanie muszą zostać zaktualizowane, zwykle nie jest kandydatem dobrej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="02e49-177">W przypadku przypadek, w którym należy zaktualizować kolumn dystrybucji, można to zrobić przez usunięcie najpierw wiersza, a następnie wstawienia nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="02e49-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="02e49-178">Wybierz kolumnę dystrybucji, który będzie równomierne danych</span><span class="sxs-lookup"><span data-stu-id="02e49-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="02e49-179">Ponieważ rozproszony system przeprowadza tylko tak szybko, jak jego najwolniejsze dystrybucji, należy podzielić pracy równomiernie między dystrybucje aby osiągnąć zrównoważonym wykonywania przez system.</span><span class="sxs-lookup"><span data-stu-id="02e49-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="02e49-180">Sposób pracy jest podzielona na Rozproszony system jest oparty na którym mieszka danych dla poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="02e49-181">Dzięki temu można bardzo ważne, aby wybrać kolumnę dystrybucji prawo do dystrybucji danych, dzięki czemu każdej dystrybucji ma taki sam pracy i potrwa tym samym czasie, aby ukończyć jego część pracy.</span><span class="sxs-lookup"><span data-stu-id="02e49-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="02e49-182">Podczas pracy dobrze jest dzielona między systemu, danych jest równoważone między dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="02e49-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="02e49-183">Gdy dane nie jest rozmieszczana równomiernie, nazywamy to **zegara danych**.</span><span class="sxs-lookup"><span data-stu-id="02e49-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="02e49-184">Do dzielenia danych równomiernie i uniknąć pochylenia danych, należy rozważyć podczas wybierania kolumny dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="02e49-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="02e49-185">Wybierz kolumny, która zawiera znaczące liczbę unikatowych wartości.</span><span class="sxs-lookup"><span data-stu-id="02e49-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="02e49-186">Unikaj dystrybucji danych w kolumnach z kilku odrębnych wartości.</span><span class="sxs-lookup"><span data-stu-id="02e49-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="02e49-187">Unikaj dystrybucji danych dla kolumn o wysokiej częstotliwości zawiera wartości null.</span><span class="sxs-lookup"><span data-stu-id="02e49-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="02e49-188">Unikaj dystrybucji danych na kolumny daty.</span><span class="sxs-lookup"><span data-stu-id="02e49-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="02e49-189">Ponieważ każda wartość jest wartość skrótu, aby 1 60 dystrybucji, do osiągnięcia nawet dystrybucji można zaznaczyć kolumny, która jest unikatowa wysokiej i nie zawiera unikatowych wartości większej niż 60.</span><span class="sxs-lookup"><span data-stu-id="02e49-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="02e49-190">Aby zilustrować, należy wziąć pod uwagę przypadków, w których kolumna ma tylko 40 unikatowe wartości.</span><span class="sxs-lookup"><span data-stu-id="02e49-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="02e49-191">Jeśli ta kolumna została wybrana jako klucza dystrybucji, dane dla tej tabeli spowoduje grunt na 40 dystrybucje co najwyżej pozostawienie 20 dystrybucji żadnych danych i przetwarzania, nie należy.</span><span class="sxs-lookup"><span data-stu-id="02e49-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="02e49-192">Z drugiej strony 40 dystrybucji mają więcej pracy, aby to zrobić, jeśli dane został równomierny dystrybucje ponad 60.</span><span class="sxs-lookup"><span data-stu-id="02e49-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="02e49-193">Ten scenariusz jest przykładem danych pochylenia.</span><span class="sxs-lookup"><span data-stu-id="02e49-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="02e49-194">W systemie MPP każdego kroku zapytania czeka na wszystkie dystrybucje przeprowadzenie udziału w pracy.</span><span class="sxs-lookup"><span data-stu-id="02e49-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="02e49-195">Jeśli jeden dystrybucji jest więcej pracy od innych, następnie zasobu innych dystrybucji są zasadniczo niewykorzystana właśnie trwa oczekiwanie na zajęty dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="02e49-196">Podczas pracy nie jest równomiernie umieszczonych na wszystkie dystrybucje, nazywamy to **przetwarzania pochylenia**.</span><span class="sxs-lookup"><span data-stu-id="02e49-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="02e49-197">Przetwarzanie zegara spowoduje, że zapytania, aby działać wolniej niż jeśli obciążenie może być równomierny dla wszystkich dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="02e49-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="02e49-198">Dane pochylenia doprowadzi do przetwarzania pochylenia.</span><span class="sxs-lookup"><span data-stu-id="02e49-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="02e49-199">Unikaj dystrybucja wysokiej wartości Null kolumny jako wartości null spowoduje przejście na tym samym dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="02e49-200">Dystrybucja na kolumnę dat również może spowodować pochylenie przetwarzania, ponieważ na tym samym dystrybucji system przeniesie wszystkie dane dla określonej daty.</span><span class="sxs-lookup"><span data-stu-id="02e49-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="02e49-201">W przypadku kilku użytkowników jest wykonywanie zapytań wszystkich filtrowania tego samego dnia, a następnie tylko 1 60 dystrybucji będzie wykonanie wszystkich pracy od podanej daty będą tylko w jednej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="02e49-202">W tym scenariuszu zapytania prawdopodobnie zostanie uruchomiony 60 razy mniejsza niż Jeśli dane zostały równomiernie rozłożone wszystkie dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="02e49-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="02e49-203">Gdy brak kolumn odpowiednimi kandydatami istnieje, a następnie należy rozważyć użycie okrężnego jako metoda dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="02e49-204">Wybierz kolumny dystrybucji, która zostanie zminimalizowane przepływu danych</span><span class="sxs-lookup"><span data-stu-id="02e49-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="02e49-205">Minimalizując przenoszenia danych, wybierając kolumnę w prawo dystrybucji jest jednym z najważniejszych strategii dla optymalizacji wydajności magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="02e49-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="02e49-206">Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="02e49-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="02e49-207">Kolumn używanych w `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` i `HAVING` klauzule wszystkie ułatwiają **dobrej** skrótów kandydatów dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="02e49-208">Z drugiej strony, kolumn w `WHERE` klauzuli **nie** wprowadzić kandydatów kolumny dobrej skrótu ponieważ ich ograniczenia, które dystrybucje uczestniczyć w zapytaniu, co powoduje przetwarzania pochylenia.</span><span class="sxs-lookup"><span data-stu-id="02e49-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="02e49-209">Dobrym przykładem kolumny, która może być kuszące do dystrybucji na, ale często powodują tego pochylenia przetwarzania jest kolumny daty.</span><span class="sxs-lookup"><span data-stu-id="02e49-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="02e49-210">Ogólnie rzecz biorąc Jeśli masz dwie tabele faktów dużych często zaangażowane w sprzężeniu, będzie uzyskać większości wydajności przez dystrybucję obu tabel w jednej z kolumn sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="02e49-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="02e49-211">Jeśli masz tabelę, która nigdy nie jest przyłączona do innej tabeli faktów dużych, poszukaj kolumn, które są często w `GROUP BY` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="02e49-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="02e49-212">Istnieje kilka kluczowych kryteria, które muszą zostać spełnione, aby uniknąć przenoszenia danych podczas sprzężenia:</span><span class="sxs-lookup"><span data-stu-id="02e49-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="02e49-213">Tabele uwzględnione w sprzężeniu musi być rozproszone na skrót **jeden** kolumn uczestniczących w sprzężeniu.</span><span class="sxs-lookup"><span data-stu-id="02e49-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="02e49-214">Typy danych kolumn sprzężenia musi odpowiadać między obu tabel.</span><span class="sxs-lookup"><span data-stu-id="02e49-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="02e49-215">Kolumny musi być połączony z operatora równości.</span><span class="sxs-lookup"><span data-stu-id="02e49-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="02e49-216">Typ sprzężenia nie może być `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="02e49-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="02e49-217">Rozwiązywanie problemów z danych pochylenia</span><span class="sxs-lookup"><span data-stu-id="02e49-217">Troubleshooting data skew</span></span>
<span data-ttu-id="02e49-218">Gdy dane w tabeli są przesyłane przy użyciu metody dystrybucji skrót istnieje ryzyko, że niektórych dystrybucji będzie niesymetryczna nieproporcjonalnie więcej danych niż inne.</span><span class="sxs-lookup"><span data-stu-id="02e49-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="02e49-219">Pochylenie nadmiernej ilości danych może wpłynąć na wydajność zapytań, ponieważ wynik końcowy zapytań rozproszonych musi czekać na najdłużej działających dystrybucji zakończyć.</span><span class="sxs-lookup"><span data-stu-id="02e49-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="02e49-220">W zależności od stopnia pochylenie danych może być konieczne jego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="02e49-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="02e49-221">Identyfikowanie zegara</span><span class="sxs-lookup"><span data-stu-id="02e49-221">Identifying skew</span></span>
<span data-ttu-id="02e49-222">Prosty sposób, aby zidentyfikować tabelę jako niesymetryczna jest użycie `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="02e49-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="02e49-223">Jest to bardzo szybki i prosty sposób aby wyświetlić liczbę wierszy tabeli, które są przechowywane w każdym z 60 dystrybucje bazy danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="02e49-224">Należy pamiętać, że dla najbardziej zrównoważoną wydajność, wiersze w tabeli rozproszonej powinny być rozmieszczone równomiernie w obrębie wszystkie dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="02e49-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="02e49-225">Jednak w przypadku zapytań usługi Azure SQL Data Warehouse dynamicznych widoków zarządzania (DMV) można przeprowadzić bardziej szczegółowej analizy.</span><span class="sxs-lookup"><span data-stu-id="02e49-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="02e49-226">Aby rozpocząć, Utwórz widok [dbo.vTableSizes] [ dbo.vTableSizes] wyświetlić przy użyciu programu SQL z [omówienie tabeli] [ Overview] artykułu.</span><span class="sxs-lookup"><span data-stu-id="02e49-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="02e49-227">Po utworzeniu widoku wykonania tego zapytania, aby zidentyfikować tabel, które mają więcej niż 10% danych zegara.</span><span class="sxs-lookup"><span data-stu-id="02e49-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="02e49-228">Rozpoznawanie pochylenia danych</span><span class="sxs-lookup"><span data-stu-id="02e49-228">Resolving data skew</span></span>
<span data-ttu-id="02e49-229">Nie wszystkie pochylenia jest wystarczająca do zapewnienia liczbę poprawkę.</span><span class="sxs-lookup"><span data-stu-id="02e49-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="02e49-230">W niektórych przypadkach wydajności tabeli niektórych kwerend może przeważają uszkodzenie danych pochylenia.</span><span class="sxs-lookup"><span data-stu-id="02e49-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="02e49-231">Podjęcie decyzji, czy należy poprawić danych pochylenia w tabeli, należy zrozumieć jak to możliwe ilości danych i zapytania w obciążenie.</span><span class="sxs-lookup"><span data-stu-id="02e49-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="02e49-232">Jest jednym ze sposobów przyjrzeć się wpływ zegara do wykonania czynności w [monitorowania zapytania] [ Query Monitoring] artykuł, aby monitorować wpływ pochylenia wzdłuż wydajność zapytań i w szczególności wpływu jak długo wysyła zapytanie do podjęcia w poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="02e49-233">Dystrybucji danych polega na znajdowaniu kompromisu między minimalizując zegara danych i minimalizując przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="02e49-234">Te można przeciwne cele i czasem można przechowywać dane pochylenia w celu ograniczenia przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="02e49-235">Na przykład gdy kolumna dystrybucji jest często wspólnej kolumny sprzężenia i agregacji, można będzie można minimalizację przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="02e49-236">O konieczności przeniesienia minimalna ilość danych może być większe niż wpływ pochylanie danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="02e49-237">Typowy sposób rozwiązania zegara danych jest ponownie utwórz tabelę z kolumną różnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="02e49-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="02e49-238">Ponieważ nie można zmienić kolumny dystrybucji w istniejącej tabeli, sposób dystrybucji tabeli zmień ją utworzyć go ponownie [] [CTAS].</span><span class="sxs-lookup"><span data-stu-id="02e49-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="02e49-239">Poniżej przedstawiono dwa przykłady tego, jak rozpoznać pochylenia danych:</span><span class="sxs-lookup"><span data-stu-id="02e49-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="02e49-240">Przykład 1: Ponownie utwórz tabelę z kolumną nowe dystrybucji</span><span class="sxs-lookup"><span data-stu-id="02e49-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="02e49-241">W tym przykładzie użyto [] [CTAS] ponownie utworzyć tabelę z kolumną dystrybucji różnych wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="02e49-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="02e49-242">Przykład 2: Ponownie utwórz tabelę przy użyciu rozkładu okrężnego</span><span class="sxs-lookup"><span data-stu-id="02e49-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="02e49-243">W tym przykładzie użyto [] [CTAS], aby ponownie utworzyć tabelę z okrężnego zamiast dystrybucji wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="02e49-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="02e49-244">Ta zmiana spowoduje nawet danych dystrybucji kosztem przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="02e49-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="02e49-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02e49-245">Next steps</span></span>
<span data-ttu-id="02e49-246">Aby dowiedzieć się więcej o projektowaniu tabel, zobacz [dystrybucji][Distribute], [indeksu][Index], [partycji][Partition], [typy danych][Data Types], [statystyki] [ Statistics] i [tabel tymczasowych] [ Temporary] artykułów.</span><span class="sxs-lookup"><span data-stu-id="02e49-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="02e49-247">Omówienie najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="02e49-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
