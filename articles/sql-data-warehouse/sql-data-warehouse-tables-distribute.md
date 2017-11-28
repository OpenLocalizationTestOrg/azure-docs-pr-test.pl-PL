---
title: "tabele aaaDistributing w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="2fc7f-103">Dystrybucja tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2fc7f-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2fc7f-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="2fc7f-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="2fc7f-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="2fc7f-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-107">[Index][Index]</span></span>
> * <span data-ttu-id="2fc7f-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="2fc7f-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="2fc7f-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="2fc7f-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="2fc7f-111">Usługa SQL Data Warehouse to system rozproszonych baz danych o architekturze masowego przetwarzana równoległego (MPP).</span><span class="sxs-lookup"><span data-stu-id="2fc7f-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="2fc7f-112">Dzieląc dane i możliwości przetwarzania między wiele węzłów, usługa SQL Data Warehouse może zaoferować bardzo dużą skalowalność — znacznie większą niż w przypadku jakiegokolwiek pojedynczego systemu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="2fc7f-113">Przy wyborze sposobu toodistribute danych w magazynie danych SQL jest jedną z najważniejszych hello czynniki tooachieving optymalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="2fc7f-114">wydajności klucza toooptimal Hello jest minimalizowania przenoszenia danych i z kolei przenoszenia danych klucza toominimizing hello jest wybranie hello strategii prawa dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="2fc7f-115">Opis przenoszenia danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-115">Understanding data movement</span></span>
<span data-ttu-id="2fc7f-116">W systemie MPP hello danych z każdej tabeli jest dzielona między kilka podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="2fc7f-117">Witaj najbardziej zoptymalizowanych pod kątem zapytań w systemie MPP po prostu mogą zostać przekazane za pośrednictwem tooexecute na powitania pojedyncze rozproszonej bazy danych bez interakcji między hello innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="2fc7f-118">Załóżmy na przykład, że masz bazę danych danymi sprzedaży zawiera dwie tabele, sprzedaży i klientów.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="2fc7f-119">Jeśli masz kwerendę, która wymaga toojoin tabeli klienta tooyour tabeli sprzedaży i dzielenia sprzedaży i tabele klienta się przez numer klienta umieszczanie każdego klienta w oddzielnej bazy danych, w ramach każdej można rozwiązać żadnych zapytań, które przyłączyć sprzedaży i klienta bazy danych z żadnej znajomości hello innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="2fc7f-120">Z kolei danych sprzedaży rozdzielonych numer zamówienia i danych klienta przez numer klienta, następnie wszystkie danego bazy danych nie będzie zawierał hello odpowiednich danych dla każdego klienta, dlatego jeśli chce toojoin danych klienta tooyour danych sprzedaży, będzie potrzebny tooget hello danych dla każdego klienta z hello innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="2fc7f-121">W drugim przykładzie przenoszenia danych musi toooccur toomove powitania klienta toohello sprzedaży danych, tak, aby Witaj dwie tabele mogą zostać sprzężone.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="2fc7f-122">Przenoszenie danych zawsze jest zły element, czasami jest konieczne toosolve zapytania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="2fc7f-123">Jednak podczas tego dodatkowego kroku można uniknąć, naturalny zapytanie będzie szybsze.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="2fc7f-124">Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="2fc7f-125">Często konieczne toodo obu, gdy być może toooptimize jednym ze scenariuszy, takich jak sprzężenia, możesz nadal wymaga toohelp przepływu danych, które rozwiązywać dla hello innej sytuacji, takich jak agregacji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="2fc7f-126">Lewa Hello jest ustaleniem, czyli mniej pracy.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="2fc7f-127">W większości przypadków dystrybucja tabele faktów dużych często dołączonego do kolumny jest hello najbardziej efektywną metodę zmniejszenie hello większości przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="2fc7f-128">Dystrybucja danych na kolumn sprzężenia jest znacznie bardziej popularne przenoszenia danych tooreduce metody na niż dystrybucji danych kolumn uczestniczących w agregacji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="2fc7f-129">Wybieranie metody dystrybucji</span><span class="sxs-lookup"><span data-stu-id="2fc7f-129">Select distribution method</span></span>
<span data-ttu-id="2fc7f-130">Usługi SQL Data Warehouse tle hello dzieli dane 60 baz danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="2fc7f-131">Każdej poszczególne bazy danych jest określony tooas **dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="2fc7f-132">Podczas ładowania danych w każdej tabeli, Magazyn danych SQL ma tooknow jak toodivide danych przez tych 60 dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="2fc7f-133">Metoda dystrybucji Hello jest zdefiniowana na poziomie tabeli hello i obecnie dostępne są dwie możliwości:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="2fc7f-134">**Działanie okrężne** który równomiernie, ale losowo dystrybucji danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="2fc7f-135">**Skrótów rozproszone** która dystrybuuje oparte na tworzenie skrótów wartości z jednej kolumny danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="2fc7f-136">Domyślnie, gdy metoda dystrybucji danych, nie zostaną zdefiniowane tabeli będą dystrybuowane za pomocą hello **działanie okrężne** metoda dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="2fc7f-137">Jednak ponieważ staje się bardziej złożone w implementacji, można za pomocą tooconsider **rozpowszechniane skrót** tabele toominimize przenoszenia danych, który będzie z kolei optymalizacji wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="2fc7f-138">Działanie okrężne tabel</span><span class="sxs-lookup"><span data-stu-id="2fc7f-138">Round Robin Tables</span></span>
<span data-ttu-id="2fc7f-139">Przy użyciu hello okrężnego metoda dystrybucji danych jest znacznie, jak ich wymowy.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="2fc7f-140">Jak Twoje dane są ładowane, każdy wiersz po prostu są wysyłane toohello dystrybucji dalej.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="2fc7f-141">Ta metoda dystrybucji hello danych będzie zawsze losowo równomierne danych hello bardzo we wszystkich hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="2fc7f-142">Oznacza to, że istnieje sortowania nie gotowe podczas hello round działania okrężnego procesu, który umieszcza dane.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="2fc7f-143">Działanie okrężne dystrybucji jest niekiedy nazywany losowego wyznaczania wartości skrótu z tego powodu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="2fc7f-144">Z tabelą rozproszonej okrężnego nie ma żadnych danych hello toounderstand potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="2fc7f-145">Z tego powodu tabel okrężnego należy często dobrym ładowanie obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="2fc7f-146">Domyślnie, jeśli wybrano opcję Brak metody dystrybucji, hello okrężnego dystrybucji zostanie użyta metoda.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="2fc7f-147">Jednak działanie okrężne tabele są łatwe toouse, ponieważ danych jest rozłożona losowo systemu hello, oznacza to, że hello system nie może zagwarantować, które dystrybucji każdy wiersz jest na.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="2fc7f-148">Wynik, czasami systemu hello potrzeb tooinvoke toobetter operacji przenoszenia danych organizowania danych przed może rozpoznać zapytania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="2fc7f-149">Ten krok dodatkowe może to spowolnić zapytań.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="2fc7f-150">Rozważ użycie dystrybucji okrężnego dla tej tabeli w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="2fc7f-151">Gdy wprowadzenie jako punktu wyjścia proste</span><span class="sxs-lookup"><span data-stu-id="2fc7f-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="2fc7f-152">Jeśli oczywiste łącząca klucz nie istnieje</span><span class="sxs-lookup"><span data-stu-id="2fc7f-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="2fc7f-153">Jeśli nie ma kolumny odpowiednimi kandydatami do wyznaczania wartości skrótu dystrybucji hello tabeli</span><span class="sxs-lookup"><span data-stu-id="2fc7f-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="2fc7f-154">Jeśli hello tabeli nie udostępnia wspólny klucz sprzężenia z innych tabel</span><span class="sxs-lookup"><span data-stu-id="2fc7f-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="2fc7f-155">Jeśli sprzężenia hello jest mniej istotna niż inne sprzężeń w zapytaniu hello</span><span class="sxs-lookup"><span data-stu-id="2fc7f-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="2fc7f-156">Gdy tabeli hello jest tymczasowy tabeli przemieszczania</span><span class="sxs-lookup"><span data-stu-id="2fc7f-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="2fc7f-157">Oba te przykłady spowoduje utworzenie tabeli działanie okrężne:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="2fc7f-158">Gdy jest działanie okrężne typem tabeli domyślnym hello jest jawne w kod DDL jest uważany za najlepszym rozwiązaniem, wyczyść tooothers aby zamiarach hello układu tabeli.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="2fc7f-159">Rozproszone tabele hash</span><span class="sxs-lookup"><span data-stu-id="2fc7f-159">Hash Distributed Tables</span></span>
<span data-ttu-id="2fc7f-160">Przy użyciu **rozpowszechniane skrót** toodistribute algorytm tabel może poprawić wydajność w różnych scenariuszach ograniczając przenoszenie danych w czasie zapytania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="2fc7f-161">Tabele rozproszone są tabele, które są dzielone między hello skrótu rozproszonych baz danych przy użyciu algorytmu wyznaczania wartości skrótu w jednej kolumnie, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="2fc7f-162">Kolumna dystrybucji Hello jest, co określa, jak dane hello jest dzielona między rozproszonych baz danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="2fc7f-163">Funkcja wyznaczania wartości skrótu Hello używa hello dystrybucji kolumny tooassign wierszy toodistributions.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="2fc7f-164">Witaj algorytmu wyznaczania wartości skrótu i wynikowy dystrybucji jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="2fc7f-165">Oznacza to hello toohello ma tę samą wartość z tego samego typu danych będzie zawsze hello tego samego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="2fc7f-166">W tym przykładzie utworzy rozproszone na identyfikator tabeli:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="2fc7f-167">Wybierz kolumnę dystrybucji</span><span class="sxs-lookup"><span data-stu-id="2fc7f-167">Select distribution column</span></span>
<span data-ttu-id="2fc7f-168">Jeśli zdecydujesz się zbyt**skrótu dystrybucji** tabeli, konieczne będzie tooselect dystrybucji jednej kolumny.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="2fc7f-169">Podczas wybierania kolumn dystrybucji, istnieją trzy główne czynniki tooconsider.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="2fc7f-170">Wybrać pojedynczą kolumnę, która będzie:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-170">Select a single column which will:</span></span>

1. <span data-ttu-id="2fc7f-171">Nie można zaktualizować</span><span class="sxs-lookup"><span data-stu-id="2fc7f-171">Not be updated</span></span>
2. <span data-ttu-id="2fc7f-172">Równomierne danych, unikając pochylenia danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="2fc7f-173">Minimalizowanie przepływu danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="2fc7f-174">Wybierz kolumnę dystrybucji, które nie zostaną zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="2fc7f-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="2fc7f-175">Kolumny dystrybucji nie są aktualizowalne, w związku z tym, wybierz kolumnę o wartości statyczne.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="2fc7f-176">Jeśli kolumny, należy zaktualizować toobe, zwykle nie jest kandydatem dobrej.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="2fc7f-177">W przypadku przypadek, w którym należy zaktualizować kolumn dystrybucji, można to zrobić przez najpierw usunięcie hello wiersza, a następnie wstawienia nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="2fc7f-178">Wybierz kolumnę dystrybucji, który będzie równomierne danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="2fc7f-179">Ponieważ rozproszony system przeprowadza tylko tak szybko, jak jego najwolniejsze dystrybucji, jest ważne toodivide hello pracy równomiernie między dystrybucje hello kolejność wykonywania tooachieve zrównoważonym między hello systemu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="2fc7f-180">sposób Hello pracy hello jest podzielona na Rozproszony system jest oparty na którym mieszka hello danych dla poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="2fc7f-181">Dzięki temu tooselect bardzo ważne hello dystrybucji prawa kolumna dystrybucji hello danych tak, aby każdy dystrybucji ma taki sam pracy i będzie podjęcia hello tym samym czasie toocomplete część pracy hello.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="2fc7f-182">Podczas pracy dobrze jest dzielona między hello systemu, danych hello jest równoważone między hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="2fc7f-183">Gdy dane nie jest rozmieszczana równomiernie, nazywamy to **zegara danych**.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="2fc7f-184">dane toodivide równomiernie i uniknąć pochylenia danych, należy wziąć pod uwagę następujące powitania po wybraniu kolumny dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="2fc7f-185">Wybierz kolumny, która zawiera znaczące liczbę unikatowych wartości.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="2fc7f-186">Unikaj dystrybucji danych w kolumnach z kilku odrębnych wartości.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="2fc7f-187">Unikaj dystrybucji danych dla kolumn o wysokiej częstotliwości zawiera wartości null.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="2fc7f-188">Unikaj dystrybucji danych na kolumny daty.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="2fc7f-189">Ponieważ każda wartość skrótu too1 60 dystrybucji, nawet dystrybucji tooachieve można tooselect kolumny, która jest wysoce unikatowy i zawiera więcej niż 60 unikatowe wartości.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="2fc7f-190">tooillustrate, należy wziąć pod uwagę w przypadku, gdy kolumna zawiera tylko 40 unikatowe wartości.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="2fc7f-191">Jeśli ta kolumna została wybrana jako klucza dystrybucji hello, hello danych dla tej tabeli spowoduje grunt na 40 dystrybucje co najwyżej pozostawienie 20 dystrybucji żadnych danych i nie toodo przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="2fc7f-192">Z drugiej strony hello innych 40 dystrybucji mają więcej toodo pracy, że jeśli hello danych został równomierny dystrybucje ponad 60.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="2fc7f-193">Ten scenariusz jest przykładem danych pochylenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="2fc7f-194">W systemie MPP każdego kroku zapytania czeka na wszystkich toocomplete dystrybucje udziału hello pracy.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="2fc7f-195">Jeśli jeden dystrybucji jest więcej pracy niż hello innych użytkowników, a następnie hello zasobów hello innych dystrybucji są zasadniczo niewykorzystana właśnie trwa oczekiwanie na powitania dystrybucji zajęty.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="2fc7f-196">Podczas pracy nie jest równomiernie umieszczonych na wszystkie dystrybucje, nazywamy to **przetwarzania pochylenia**.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="2fc7f-197">Przetwarzanie zegara spowoduje wolniej niż Jeśli hello obciążenie może być równomierny dla wszystkich dystrybucje hello toorun zapytania.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="2fc7f-198">Pochylenie danych doprowadzi tooprocessing pochylenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="2fc7f-199">Nie udostępniaj wysokiej wartości Null kolumny jako wartości null hello wszystkie przeniesie na powitania sam dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="2fc7f-200">Dystrybucja na kolumnę dat może również spowodować przetwarzania pochylenia ponieważ wszystkie dane dla określonej daty przeniesie na powitania sam dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="2fc7f-201">W przypadku kilku użytkowników jest wykonywanie zapytań wszystkie filtrowania na powitania sama data, następnie tylko 1 dystrybucje 60 hello będzie realizacji wszystkich prac powitania od podanej daty będą tylko w jednej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="2fc7f-202">W tym scenariuszu zapytania hello prawdopodobnie zostanie uruchomiony 60 razy mniejsza niż Jeśli hello danych zostały jednakowo rozprzestrzeniać się wszystkie hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="2fc7f-203">Jeśli istnieją żadnych kolumn odpowiednimi kandydatami, należy rozważyć hello metoda dystrybucji przy użyciu okrężnego.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="2fc7f-204">Wybierz kolumny dystrybucji, która zostanie zminimalizowane przepływu danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="2fc7f-205">Minimalizując przenoszenia danych, wybierając kolumnę prawo dystrybucji hello jest jednym z najważniejszych strategii hello optymalizacji wydajności magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="2fc7f-206">Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="2fc7f-207">Kolumn używanych w `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` i `HAVING` klauzule wszystkie ułatwiają **dobrej** skrótów kandydatów dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="2fc7f-208">Witaj w drugiej kolumny w hello `WHERE` klauzuli **nie** wprowadzić kandydatów kolumny dobrej skrótu ponieważ ich ograniczenia, które dystrybucje uczestniczyć w zapytaniu hello, co powoduje przetwarzania pochylenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="2fc7f-209">Dobrym przykładem kolumny, która może być kuszące toodistribute na, ale często powodują tego pochylenia przetwarzania jest kolumny daty.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="2fc7f-210">Ogólnie rzecz biorąc Jeśli masz dwie tabele faktów dużych często zaangażowane w sprzężeniu, będzie uzyskasz hello większości wydajności przez dystrybucję obu tabel w jednym z hello kolumn sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="2fc7f-211">Jeśli masz tabelę, która nie jest nigdy tooanother dołączonego do tabeli faktów dużych Szukaj toocolumns, które są często stosowane w hello `GROUP BY` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="2fc7f-212">Istnieje kilka klucza kryteriów, które musi być niespełnienia tooavoid przenoszenia danych podczas sprzężenia:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="2fc7f-213">Hello tabel, których dotyczy hello sprzężenia musi być rozproszone na skrót **jeden** hello kolumn uczestniczących w hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="2fc7f-214">typy danych kolumn sprzężenia hello Hello musi odpowiadać między obu tabel.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="2fc7f-215">Witaj kolumn muszą być przyłączone z operatorem równości.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="2fc7f-216">Witaj typ sprzężenia mogą nie być `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="2fc7f-217">Rozwiązywanie problemów z danych pochylenia</span><span class="sxs-lookup"><span data-stu-id="2fc7f-217">Troubleshooting data skew</span></span>
<span data-ttu-id="2fc7f-218">Dane tabeli są przesyłane przy użyciu metody dystrybucji skrótu hello jest ryzyko, że będzie niektórych dystrybucji niesymetryczna toohave nieproporcjonalnie więcej danych niż inne.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="2fc7f-219">Pochylenia nadmiernej ilości danych może wpłynąć na wydajność zapytań, ponieważ hello końcowego wyniku zapytania rozproszonego musi czekać na hello najdłuższym uruchomionych dystrybucji toofinish.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="2fc7f-220">W zależności od stopnia hello danych hello pochylenia, może być konieczne tooaddress go.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="2fc7f-221">Identyfikowanie zegara</span><span class="sxs-lookup"><span data-stu-id="2fc7f-221">Identifying skew</span></span>
<span data-ttu-id="2fc7f-222">Prosty sposób tooidentify tabelę niesymetryczna jest toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="2fc7f-223">Jest to bardzo szybki i prosty sposób toosee hello liczba wierszy tabeli, które są przechowywane w każdym dystrybucje hello 60 bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="2fc7f-224">Należy pamiętać, że wydajności hello najbardziej zrównoważonym hello wierszy w tabeli rozproszonej należy można rozmieszczone równomiernie w obrębie wszystkie dystrybucje hello.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="2fc7f-225">Jednak w przypadku zapytania hello Azure SQL Data Warehouse dynamicznych widoków zarządzania (DMV) można przeprowadzić bardziej szczegółowej analizy.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="2fc7f-226">toostart, Utwórz widok hello [dbo.vTableSizes] [ dbo.vTableSizes] wyświetlić przy użyciu hello SQL z [omówienie tabeli] [ Overview] artykułu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="2fc7f-227">Po utworzeniu widoku hello Uruchom ten tooidentify zapytania tabel, które mają więcej niż 10% danych zegara.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="2fc7f-228">Rozpoznawanie pochylenia danych</span><span class="sxs-lookup"><span data-stu-id="2fc7f-228">Resolving data skew</span></span>
<span data-ttu-id="2fc7f-229">Nie wszystkie pochylenia jest za mało toowarrant poprawkę.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="2fc7f-230">W niektórych przypadkach wydajności hello tabeli niektórych kwerend może przeważają hello uszkodzenie danych pochylenia.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="2fc7f-231">pochylanie toodecide Jeśli danych powinien być rozpoznawany w tabeli, należy się dowiedzieć, jak to możliwe hello woluminów danych i zapytania w obciążenie.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="2fc7f-232">Kroki hello toouse hello jest jednokierunkowej toolook na powitania wpływ zegara [monitorowania zapytania] [ Query Monitoring] artykuł toomonitor hello skutki pochylenia wzdłuż wydajność zapytań, a w szczególności hello wpływ toohow długich zapytań zająć toocomplete hello poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="2fc7f-233">Dystrybucji danych polega na znajdowaniu hello kompromisu między minimalizując zegara danych i minimalizując przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="2fc7f-234">Te można przeciwne cele i czasem można danych tookeep pochylenia podczas przenoszenia danych tooreduce kolejności.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="2fc7f-235">Na przykład gdy kolumna dystrybucji hello jest często hello udostępnionego kolumną sprzęgania i agregacji, można będzie można minimalizację przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="2fc7f-236">Witaj o konieczności przenoszenia danych minimalnego hello może przeważają wpływ hello pochylanie danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="2fc7f-237">Typowym sposobem Hello tooresolve danych zegara wynosi toore — Utwórz hello tabelę z kolumną różnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="2fc7f-238">Ponieważ nie istnieje sposób toochange hello dystrybucji kolumny w istniejącej tabeli hello sposób toochange hello dystrybucji tabeli go toorecreate za pomocą [] [CTAS].</span><span class="sxs-lookup"><span data-stu-id="2fc7f-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="2fc7f-239">Poniżej przedstawiono dwa przykłady tego, jak rozpoznać pochylenia danych:</span><span class="sxs-lookup"><span data-stu-id="2fc7f-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="2fc7f-240">Przykład 1: Ponownie utwórz tabelę hello z nową kolumnę dystrybucji</span><span class="sxs-lookup"><span data-stu-id="2fc7f-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="2fc7f-241">W tym przykładzie użyto toore [] [CTAS]-tworzy tabelę z kolumną dystrybucji różnych wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="2fc7f-242">Przykład 2: Ponownie utwórz tabeli hello przy użyciu rozkładu okrężnego</span><span class="sxs-lookup"><span data-stu-id="2fc7f-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="2fc7f-243">W tym przykładzie użyto toore [] [CTAS]-tworzy tabelę z okrężnego zamiast dystrybucji wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="2fc7f-244">Ta zmiana spowoduje dystrybucji danych nawet kosztem hello przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="2fc7f-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2fc7f-245">Next steps</span></span>
<span data-ttu-id="2fc7f-246">toolearn więcej informacji o projektowaniu tabel, zobacz hello [dystrybucji][Distribute], [indeksu][Index], [partycji] [ Partition], [Typy danych][Data Types], [statystyki] [ Statistics] i [tabel tymczasowych] [ Temporary] artykułów.</span><span class="sxs-lookup"><span data-stu-id="2fc7f-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="2fc7f-247">Omówienie najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2fc7f-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
