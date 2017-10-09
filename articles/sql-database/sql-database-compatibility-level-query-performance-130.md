---
title: "poziom zgodności aaaDatabase 130 — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule firma Microsoft Poznaj zalety hello systemem 130 na poziomie zgodności bazy danych SQL Azure i wykorzystanie zalet hello hello nowy Optymalizator zapytań i wyszukiwać funkcje procesora. Możemy także spełnić hello efekty uboczne na wydajność zapytań hello hello istniejących aplikacji SQL."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="b5937-104">Zwiększona wydajność zapytań ze zgodnością 130 poziom w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b5937-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="b5937-105">Baza danych SQL Azure działa niewidocznie setki tysięcy baz danych na wielu poziomach różnych zgodności, zachowania i gwarantujących hello zgodności z poprzednimi wersjami toohello odpowiednią wersję programu Microsoft SQL Server dla wszystkich klientów!</span><span class="sxs-lookup"><span data-stu-id="b5937-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="b5937-106">W tym artykule firma Microsoft Poznaj zalety hello uruchomiona z Databse SQL Azure na poziomie zgodności 130 i wykorzystanie zalet hello hello nowy Optymalizator zapytań i wyszukiwać funkcje procesora.</span><span class="sxs-lookup"><span data-stu-id="b5937-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="b5937-107">Możemy także spełnić hello efekty uboczne na wydajność zapytań hello hello istniejących aplikacji SQL.</span><span class="sxs-lookup"><span data-stu-id="b5937-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="b5937-108">Dla przypomnienia historii wyrównanie hello poziomy zgodności toodefault wersji programu SQL są następujące:</span><span class="sxs-lookup"><span data-stu-id="b5937-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="b5937-109">100: w programie SQL Server 2008 i Azure SQL bazy danych V11.</span><span class="sxs-lookup"><span data-stu-id="b5937-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="b5937-110">110: w programie SQL Server 2012 i Azure SQL bazy danych V11.</span><span class="sxs-lookup"><span data-stu-id="b5937-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="b5937-111">120: w programie SQL Server 2014 i Azure SQL bazy danych w wersji 12.</span><span class="sxs-lookup"><span data-stu-id="b5937-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="b5937-112">130: w programie SQL Server 2016 i Azure SQL bazy danych w wersji 12.</span><span class="sxs-lookup"><span data-stu-id="b5937-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5937-113">Począwszy od **środek czerwca 2016**, w bazie danych SQL Azure, hello domyślny poziom zgodności będzie 130 zamiast 120 dla **nowo utworzony** baz danych.</span><span class="sxs-lookup"><span data-stu-id="b5937-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="b5937-114">Bazy danych utworzone przed środek czerwca 2016 r. zostanie *nie* zmian i będzie utrzymywać ich bieżący poziom zgodności (100, 110 lub 120).</span><span class="sxs-lookup"><span data-stu-id="b5937-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="b5937-115">Bazy danych, które są migrowane z bazy danych SQL Azure w wersji V11 tooV12 ma poziom zgodności 100 lub 110.</span><span class="sxs-lookup"><span data-stu-id="b5937-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="b5937-116">O poziomie zgodności 130</span><span class="sxs-lookup"><span data-stu-id="b5937-116">About compatibility level 130</span></span>
<span data-ttu-id="b5937-117">Najpierw Jeśli chcesz tooknow hello bieżący poziom zgodności bazy danych, należy wykonać hello następującej instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b5937-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="b5937-118">Przed wprowadzeniem tej zmiany toolevel 130 odbywa się w **nowo** teraz utworzony baz danych, przejrzyj ta zmiana jest wszystko, za pośrednictwem przykładowe zapytanie bardzo proste, a Zobacz każdy korzyści z niej.</span><span class="sxs-lookup"><span data-stu-id="b5937-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="b5937-119">Przetwarzanie zapytań w relacyjnych baz danych może być bardzo skomplikowane i może prowadzić toolots komputera nauki i matematyce toounderstand hello związanego z używaniem decyzji projektowych i zachowania.</span><span class="sxs-lookup"><span data-stu-id="b5937-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="b5937-120">W tym dokumencie hello zawartość została celowo uproszczona tooensure, że każda osoba mająca minimalne informacje techniczne zrozumienie wpływu zmiany poziomu zgodności hello hello i określić, jak też korzystać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b5937-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="b5937-121">Załóżmy ma poziom zgodności hello 130 łączy w tabeli hello krótki przegląd.</span><span class="sxs-lookup"><span data-stu-id="b5937-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="b5937-122">Można znaleźć więcej szczegółów na [zmienić poziom zgodności bazy danych (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), ale poniżej przedstawiono krótkie podsumowanie:</span><span class="sxs-lookup"><span data-stu-id="b5937-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="b5937-123">Hello operacji wstawiania instrukcji Insert select może być wielowątkowych lub może mieć plan równoległy podczas przed jednowątkowe tej operacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="b5937-124">Pamięci tabela zoptymalizowana i tabeli Zmienne zapytania można teraz mieć równoległych planów podczas zanim ta operacja została również jednowątkowego.</span><span class="sxs-lookup"><span data-stu-id="b5937-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="b5937-125">Statystyki dla tabel zoptymalizowanych pod kątem pamięci może być próbkowany i są aktualizowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b5937-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="b5937-126">Zobacz [What's New in aparatu bazy danych: OLTP w pamięci](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="b5937-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="b5937-127">Zmiany trybu wiersza v trybu partii/s z indeksami magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="b5937-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="b5937-128">Sortuje w tabeli z indeksem magazynu kolumn są dostępne w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="b5937-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="b5937-129">Agreguje okien działał w trybie wsadowym, takie jak instrukcje TSQL opóźnienie/realizacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="b5937-130">Zapytania w tabelach magazynu kolumn z wielu różnych klauzule działają w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="b5937-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="b5937-131">Zapytań wykonywanych w ramach DOP = 1 lub z planem serial również wykonać w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="b5937-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="b5937-132">Ostatnio ulepszenia szacowania kardynalności faktycznie pochodzą z poziomem zgodności 120, ale dla osób, które z poziomu zgodności niższy (tj. 100 lub 110), hello przenoszenia toocompatibility poziom 130 również wywoła te ulepszenia i mogą również korzyści hello wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="b5937-133">Ćwiczenie poziom zgodności 130</span><span class="sxs-lookup"><span data-stu-id="b5937-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="b5937-134">Pierwszy Załóż niektórych tabel, indeksy i losowe dane utworzone toopractice niektóre z nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b5937-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="b5937-135">Przykłady skryptów TSQL Hello mogą być wykonywane w ramach programu SQL Server 2016, lub baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b5937-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="b5937-136">Jednak podczas tworzenia bazy danych Azure SQL, upewnij się, wybierz na powitania minimalna P2 bazy danych, ponieważ należy co najmniej kilka wielowątkowości tooallow rdzeni i w związku z tym korzystanie z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b5937-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="b5937-137">Teraz załóżmy ma toosome wygląd, pochodzących z poziomem zgodności 130 funkcji przetwarzania zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="b5937-138">Wstaw równoległych</span><span class="sxs-lookup"><span data-stu-id="b5937-138">Parallel INSERT</span></span>
<span data-ttu-id="b5937-139">Wykonywanie instrukcji TSQL hello poniżej wykonuje hello operacja WSTAWIANIA w obszarze poziom zgodności 120 i 130, które odpowiednio wykonuje hello operacja WSTAWIANIA w jednym modelu wątków (120) i w modelu wielowątkowych (130).</span><span class="sxs-lookup"><span data-stu-id="b5937-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-140">Przez zażądanie planu zapytania rzeczywiste hello hello spojrzenie na jej reprezentację albo jej zawartość XML, można określić, które szacowania kardynalności funkcja znajduje się na play.</span><span class="sxs-lookup"><span data-stu-id="b5937-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="b5937-141">Spojrzenie na powitania planów side-by-side na rysunku 1, firma Microsoft może wyraźnie Zobacz tego hello wykonywania Wstaw magazynu kolumn zawiera z serial w 120 tooparallel 130.</span><span class="sxs-lookup"><span data-stu-id="b5937-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="b5937-142">Zauważ również, taka zmiana hello hello iteratora ikony w planie 130 hello przedstawiający dwa strzałki równoległe, pokazujący hello fakt, że teraz hello wykonywania iteratora jest w rzeczywistości równoległych.</span><span class="sxs-lookup"><span data-stu-id="b5937-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="b5937-143">Jeśli masz dużą toocomplete operacji INSERT hello wykonywanie równoległe, połączonego toohello liczba rdzeni posiadanego Twojej dyspozycji hello bazy danych, będą działać lepiej; zapasowej tooa 100 razy szybsze w zależności od sytuacji!</span><span class="sxs-lookup"><span data-stu-id="b5937-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="b5937-144">*Rysunek 1: Wstaw operację zmiany z serial tooparallel o poziomie zgodności 130.*</span><span class="sxs-lookup"><span data-stu-id="b5937-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![Rysunek 1.](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="b5937-146">Tryb SERIAL partii</span><span class="sxs-lookup"><span data-stu-id="b5937-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="b5937-147">Podobnie przenoszenie poziom toocompatibility 130 podczas przetwarzania wierszy danych umożliwia przetwarzanie wsadowe tryb.</span><span class="sxs-lookup"><span data-stu-id="b5937-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="b5937-148">Po pierwsze operacji w trybie wsadowym są dostępne tylko podczas ma indeks magazynu kolumn w miejscu.</span><span class="sxs-lookup"><span data-stu-id="b5937-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="b5937-149">Po drugie, partii zazwyczaj reprezentuje ~ 900 wierszy i używa logiki kodu, zoptymalizowana pod kątem wielordzeniowych procesorów, wyższej przepustowości pamięci i bezpośrednio wykorzystanie hello skompresowane dane hello magazynu kolumn zawsze, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="b5937-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="b5937-150">W tych warunkach SQL Server 2016 może przetwarzać ~ 900 wierszy jednocześnie, zamiast 1 wiersz w czasie hello, i w konsekwencji hello ogólne zmniejszenie kosztów operacji hello jest udostępniany przez całą partię hello, zmniejszenie hello ogólne koszty według wierszy.</span><span class="sxs-lookup"><span data-stu-id="b5937-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="b5937-151">Udostępniony ilość połączonymi z kompresji magazynu kolumny hello zasadniczo zmniejsza opóźnienia hello związanego z operacją tryb Wybierz partii.</span><span class="sxs-lookup"><span data-stu-id="b5937-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="b5937-152">Można znaleźć więcej informacji o magazynie kolumny hello i tryb w partii [przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5937-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-153">Jako widoczny poniżej obserwując hello zapytania planów side-by-side na rysunku 2, zobaczysz, że tryb przetwarzania hello została zmieniona z poziomem zgodności hello, i w konsekwencji podczas wykonywania zapytania hello w obu poziom zgodności całkowicie, firma Microsoft można stwierdzić, że w większości przypadków przetwarzania hello jest przeznaczony na wiersz (86%) w porównaniu toohello partii tryb (14%), gdzie zostaną przetworzone partie 2.</span><span class="sxs-lookup"><span data-stu-id="b5937-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="b5937-154">Zwiększ hello zestawu danych, hello korzyści zwiększy.</span><span class="sxs-lookup"><span data-stu-id="b5937-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="b5937-155">*Rysunek 2: Wybierz operację zmiany z trybu serial toobatch o poziomie zgodności 130.*</span><span class="sxs-lookup"><span data-stu-id="b5937-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Rysunek 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="b5937-157">Trybie wsadowym na wykonanie sortowania</span><span class="sxs-lookup"><span data-stu-id="b5937-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="b5937-158">Podobne toohello powyżej, ale operacja sortowania tooa zastosowane, przejście powitania od wiersza (poziom zgodności 120) toobatch trybami (poziom zgodności 130) poprawia wydajność hello hello operacja sortowania dla hello przyczyny.</span><span class="sxs-lookup"><span data-stu-id="b5937-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-159">Widoczne side-by-side na rysunku 3, zobaczysz, że operacja sortowania hello w trybie wierszowym reprezentuje 81% hello koszt podczas w trybie wsadowym hello tylko reprezentuje % 19 kosztu hello (odpowiednio 81% i % 56 sortowania hello, sam).</span><span class="sxs-lookup"><span data-stu-id="b5937-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="b5937-160">*Rysunek 3: Operacja sortowania zmienia tryb toobatch wiersza o poziomie zgodności 130.*</span><span class="sxs-lookup"><span data-stu-id="b5937-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Rysunek 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="b5937-162">Oczywiście te przykłady zawierają tylko dziesiątki tysięcy wierszy, które ma podczas przeglądania danych hello dostępne w większości serwerów SQL te dni.</span><span class="sxs-lookup"><span data-stu-id="b5937-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="b5937-163">Tylko projektu są względem miliony wierszy zamiast tego, a to może dokonywać translacji za kilka minut wykonywania oszczędza codziennie oczekujących hello rodzaju obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b5937-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="b5937-164">Ulepszenia (CE) szacowania kardynalności</span><span class="sxs-lookup"><span data-stu-id="b5937-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="b5937-165">Wszystkie bazy danych uruchomiony na poziomie zgodności 120 lub powyżej wprowadzonego w programie SQL Server 2014, będzie korzystać z nowych funkcji szacowania kardynalności hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="b5937-166">Zasadniczo szacowania kardynalności jest logiki hello używany jak programu SQL server będzie wykonywać zapytania na podstawie jej kosztu szacowany toodetermine.</span><span class="sxs-lookup"><span data-stu-id="b5937-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="b5937-167">Szacowanie Hello jest obliczana przy użyciu danych wejściowych z statystyki związane z obiektami związanego z tej kwerendy.</span><span class="sxs-lookup"><span data-stu-id="b5937-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="b5937-168">W praktyce, w wysokiego poziomu, funkcje szacowania kardynalności są wartościami szacunkowymi liczby wierszy wraz z informacjami o dystrybucji hello hello wartości liczby unikatowych wartości i liczby zduplikowane zawarte w hello tabele i obiekty, do których odwołuje się zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="b5937-169">Uzyskiwanie szacunków błąd, może to prowadzić We/Wy dysku w toounnecessary powodu tooinsufficient przyznaje pamięci (tj. bazy danych TempDB wyciekami) lub tooa wybór wykonanie planu szeregowych, za pośrednictwem równoległego zaplanować wykonanie, tooname kilka.</span><span class="sxs-lookup"><span data-stu-id="b5937-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="b5937-170">Zawarcia, niepoprawny szacuje może prowadzić tooan ogólną spadek wydajności hello wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="b5937-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="b5937-171">Na powitania drugiej stronie lepiej szacuje, dokładniejsze szacuje, potencjalnych klientów toobetter zapytania wykonaniami!</span><span class="sxs-lookup"><span data-stu-id="b5937-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="b5937-172">Jak wspomniano wcześniej, optymalizację zapytania i szacuje są sprawy złożonych, ale ma więcej informacji na temat planów kwerend i narzędzia do szacowania kardynalności toolearn mogą odwoływać się dokumentu toohello [optymalizacji Your plany zapytań z hello programu SQL Server 2014 Narzędzia do szacowania kardynalności](https://msdn.microsoft.com/library/dn673537.aspx) dla bardziej zgłębić temat.</span><span class="sxs-lookup"><span data-stu-id="b5937-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="b5937-173">Które szacowania kardynalności obecnie używasz?</span><span class="sxs-lookup"><span data-stu-id="b5937-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="b5937-174">toodetermine, w których działają zapytań szacowania kardynalności, umożliwia po prostu użyj hello zapytania przykłady poniżej.</span><span class="sxs-lookup"><span data-stu-id="b5937-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="b5937-175">Należy pamiętać, że w tym przykładzie pierwsze będą uruchamiane na poziomie zgodności 110, co oznacza użycie hello hello starego szacowania kardynalności funkcji.</span><span class="sxs-lookup"><span data-stu-id="b5937-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-176">Po zakończeniu wykonywania, kliknij łącze XML hello i przyjrzyj hello właściwości iteratora pierwszy hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b5937-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="b5937-177">Zanotuj nazwę właściwości hello o nazwie CardinalityEstimationModelVersion aktualnie ustawione na 70.</span><span class="sxs-lookup"><span data-stu-id="b5937-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="b5937-178">Nie oznacza to, że poziom zgodności bazy danych hello jest ustawiona wersja programu SQL Server 7.0 toohello (jest ustawiona na 110 jako widoczny w instrukcjach języka TSQL hello powyżej), ale hello wartość 70 po prostu reprezentuje hello starszych szacowania kardynalności funkcje dostępne od SQL Serwer 7.0, który miał żadnych głównych poprawek do programu SQL Server 2014 (który pochodzi z poziomem zgodności 120).</span><span class="sxs-lookup"><span data-stu-id="b5937-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="b5937-179">*Rysunek 4: hello CardinalityEstimationModelVersion ustawiono too70 używając poziomie zgodności 110 lub poniżej.*</span><span class="sxs-lookup"><span data-stu-id="b5937-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Rysunek 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="b5937-181">Alternatywnie można zmienić too130 poziomu zgodności hello i wyłączyć hello korzystanie z nowej funkcji szacowania kardynalności hello przy użyciu hello LEGACY_CARDINALITY_ESTIMATION ustawić tooON z [ALTER konfiguracji bazy danych o zakresie](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5937-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="b5937-182">To będzie można dokładnie hello taki sam jak przy użyciu 110 z szacowania kardynalności funkcja punktu widzenia, używając najnowszej kwerendy hello przetwarzania poziom zgodności.</span><span class="sxs-lookup"><span data-stu-id="b5937-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="b5937-183">Dzięki temu można korzystać z nowej kwerendy hello przetwarzania funkcje pochodzące z najnowszą hello poziom zgodności (tj. w trybie wsadowym), ale nadal zależne od hello starego szacowania kardynalności funkcji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="b5937-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-184">Po prostu przenoszenie poziom zgodności toohello 120 lub 130 umożliwia hello nowych funkcji szacowania kardynalności.</span><span class="sxs-lookup"><span data-stu-id="b5937-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="b5937-185">W takim przypadku domyślnego hello CardinalityEstimationModelVersion zostanie ustawiona odpowiednio too120 lub 130 jako widoczna poniżej.</span><span class="sxs-lookup"><span data-stu-id="b5937-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-186">*Rysunek 5: hello CardinalityEstimationModelVersion ustawiono too130 korzystając z poziomu zgodności 130.*</span><span class="sxs-lookup"><span data-stu-id="b5937-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Rysunek 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="b5937-188">Naocznych kontrolach hello szacowania kardynalności różnic</span><span class="sxs-lookup"><span data-stu-id="b5937-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="b5937-189">Teraz umożliwia uruchamianie nieco bardziej złożone zapytania dotyczące INNER JOIN z klauzuli WHERE, z niektórych predykaty i Przyjrzyjmy się szacowana liczba wierszy powitania od starego funkcja szacowania kardynalności hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="b5937-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-190">Wykonywanie tej kwerendy skutecznie zwraca 200,704 wierszy podczas szacowania wiersza hello z hello starego szacowania kardynalności funkcji oświadczeń 194,284 wierszy.</span><span class="sxs-lookup"><span data-stu-id="b5937-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="b5937-191">Oczywiście jak już wspomniano, przed, te wyniki liczby wierszy również zależy od częstotliwości uruchomiono hello poprzedniej próbki, który wypełnia hello Przykładowe tabele wielokrotnie przy każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="b5937-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="b5937-192">Oczywiście predykaty hello kwerendy będą także mieć wpływ na rzeczywiste szacowania hello jako uzupełnienie hello tabeli kształtu, danych i jak te dane są faktycznie skorelowania ze sobą.</span><span class="sxs-lookup"><span data-stu-id="b5937-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="b5937-193">*Rysunek 6: hello wiersza liczba szacuje się, 194,284 lub 6000 wierszy poza hello wierszy 200,704 oczekiwano.*</span><span class="sxs-lookup"><span data-stu-id="b5937-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Rysunek 6.](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="b5937-195">W hello tak samo, umożliwia teraz wykonywanie hello samo zapytanie z nowych funkcji szacowania kardynalności hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="b5937-196">Spojrzenie na powitania poniżej, możemy teraz Zobacz tego hello wiersza szacuje się, że 202,877, lub znacznie ściślejszej i wyższe niż hello starego szacowania kardynalności.</span><span class="sxs-lookup"><span data-stu-id="b5937-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="b5937-197">*Rysunek 7: szacowana liczba wierszy hello jest teraz 202,877 zamiast 194,284.*</span><span class="sxs-lookup"><span data-stu-id="b5937-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Rysunek 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="b5937-199">W rzeczywistości hello zestaw wyników jest 200,704 wierszy (ale wszystkie zależy, jak często zostało uruchomione hello zapytań hello ich w poprzedniej próbki, ale co ważniejsze, ponieważ hello TSQL używa instrukcji RAND() hello, hello rzeczywiste wartości zwracane mogą się różnić od jednego toohello uruchomienia obok).</span><span class="sxs-lookup"><span data-stu-id="b5937-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="b5937-200">W związku z tym w tym przykładzie hello nowego szacowania kardynalności oznacza lepsze zadania na szacowanie hello liczbę wierszy, ponieważ 202,877 jest znacznie bliżej too200, 704, niż 194,284!</span><span class="sxs-lookup"><span data-stu-id="b5937-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="b5937-201">Ostatnia zmiana hello klauzuli WHERE predykaty tooequality (zamiast ">" dla wystąpienia), to może spowodować szacuje hello między hello starych i nowych funkcji Kardynalność jeszcze bardziej różne, w zależności od tego, ile dopasowań można uzyskać.</span><span class="sxs-lookup"><span data-stu-id="b5937-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="b5937-202">Oczywiście w tym przypadku jest wierszy ~ 6000 poza od rzeczywistej liczby nie reprezentuje dużą ilość danych w niektórych sytuacjach.</span><span class="sxs-lookup"><span data-stu-id="b5937-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="b5937-203">Teraz, Przestaw tego toomillions wierszy w kilku tabel i bardziej złożonych kwerend i w czasie hello szacowania można wyłączyć przez miliony wierszy i w związku z tym hello ryzyka błędne plan wykonania lub żądanie za mało pamięci przyznaje wiodące hello pobrania w górę wyciekami tooTempDB i dlatego więcej operacji We/Wy są znacznie wyższa.</span><span class="sxs-lookup"><span data-stu-id="b5937-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="b5937-204">Jeśli masz możliwość hello ćwiczenie to porównanie z najbardziej typowych zapytania i zestawy danych i zobacz, przez ile niektóre hello szacuje stary i nowy jest narażony, gdy niektóre można tylko staną się bardziej off w rzeczywistości hello lub niektóre inne wystarczy po prostu bliżej toohello wiersza rzeczywistej liczby faktycznie zwracane w zestawach wyników hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="b5937-205">Wszystkie z nich zależy od kształtu hello zapytania, właściwości bazy danych Azure SQL hello, charakter hello i rozmiar hello zestawów danych i dostępne o nich statystyki hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="b5937-206">Jeśli właśnie utworzony z wystąpienie bazy danych SQL Azure, zapytania hello Optymalizator będzie mieć toobuild uruchamia jej wiedzy od początku zamiast ponowne używanie statystyki z hello poprzednie zapytanie.</span><span class="sxs-lookup"><span data-stu-id="b5937-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="b5937-207">Tak szacuje hello są bardzo kontekstowe i prawie określonych tooevery sytuacji serwera i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="b5937-208">Jest istotnym elementem tookeep pamiętać!</span><span class="sxs-lookup"><span data-stu-id="b5937-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="b5937-209">Niektóre tootake uwagi pod uwagę</span><span class="sxs-lookup"><span data-stu-id="b5937-209">Some considerations tootake into account</span></span>
<span data-ttu-id="b5937-210">Mimo że większość obciążeń korzystałby z poziomu zgodności hello 130, przed przyjmowanie hello poziom zgodności dla środowiska produkcyjnego, masz zasadniczo 3 opcje:</span><span class="sxs-lookup"><span data-stu-id="b5937-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="b5937-211">Przenieś poziom toocompatibility 130 i zobacz, jak wykonać czynności.</span><span class="sxs-lookup"><span data-stu-id="b5937-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="b5937-212">W przypadku można zauważyć pewne regresji, wystarczy po prostu ustawić tooits wstecz poziomu zgodności hello oryginalnego poziomu lub 130, a ich anulować tylko hello szacowania kardynalności wstecz toohello ze starszej wersji trybu (zgodnie z powyższymi wskazówkami, to samodzielnie można rozwiązać hello problem).</span><span class="sxs-lookup"><span data-stu-id="b5937-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="b5937-213">Należy dokładnie przetestować istniejących aplikacji pod obciążeniem produkcji podobne, dostrojenia i Zweryfikuj wydajność hello przed przejściem tooproduction.</span><span class="sxs-lookup"><span data-stu-id="b5937-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="b5937-214">W przypadku problemów taki sam jak powyżej, możesz zawsze wrócić do poprzedniej strony toohello oryginalnego poziom zgodności, lub po prostu odwrócić hello szacowania kardynalności wstecz toohello ze starszej wersji trybu.</span><span class="sxs-lookup"><span data-stu-id="b5937-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="b5937-215">Jako ostatnia opcja i hello najnowszych tooaddress sposób te pytania, jest magazyn zapytań hello tooleverage.</span><span class="sxs-lookup"><span data-stu-id="b5937-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="b5937-216">To zalecana opcja współczesnych!</span><span class="sxs-lookup"><span data-stu-id="b5937-216">That’s today’s recommended option!</span></span> <span data-ttu-id="b5937-217">Analiza hello tooassist zapytań w obszarze zgodności poziomie 120 lub poniżej i 130, nie zachęcamy za mało toouse magazynu zapytań.</span><span class="sxs-lookup"><span data-stu-id="b5937-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="b5937-218">Magazyn zapytań jest dostępne w najnowszej wersji bazy danych SQL Azure V12 hello i jest przeznaczona toohelp możesz z rozwiązywaniem problemów wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="b5937-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="b5937-219">Witaj magazynu zapytań można traktować jako rejestrator danych zbierania i prezentować szczegółowe informacje historyczne na temat wszystkich zapytań bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5937-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="b5937-220">To znacznie upraszcza dowodowe wydajność dzięki zmniejszeniu hello czas toodiagnose i rozwiązać problemy.</span><span class="sxs-lookup"><span data-stu-id="b5937-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="b5937-221">Więcej informacji można znaleźć [magazyn zapytań: Rejestrator danych dla bazy danych](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="b5937-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="b5937-222">Na powitania wysokiego poziomu, jeśli już masz zestaw baz danych uruchomionych na poziomie zgodności 120 lub poniżej i Zaplanuj toomove niektóre z nich too130, lub ponieważ obciążenie automatycznie obsługi administracyjnej nowych baz danych, które będą wkrótce będzie można ustawić domyślnego too130, rozważ Witaj następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="b5937-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="b5937-223">Przed zmianą toohello nowy poziom zgodności w środowisku produkcyjnym, Włącz magazyn zapytań.</span><span class="sxs-lookup"><span data-stu-id="b5937-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="b5937-224">Można odwoływać się za[zmienić hello trybu zgodności bazy danych i użyj hello magazynu zapytań](https://msdn.microsoft.com/library/bb895281.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="b5937-225">Następnie przetestuj wszystkich krytycznych obciążeń przy użyciu danych reprezentatywnych i zapytań środowiska przypominającej środowisko produkcyjne, i porównaj hello wydajności wystąpił i jako zgłoszony przez Magazyn zapytań.</span><span class="sxs-lookup"><span data-stu-id="b5937-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="b5937-226">Jeśli występują pewne regresji, można go zidentyfikować hello uwzględniona zapytania z hello magazyn zapytań i użyj planu hello wymuszania opcję magazynu zapytań (Planowanie alias przypinanie).</span><span class="sxs-lookup"><span data-stu-id="b5937-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="b5937-227">W takim przypadku możesz ostatecznie pozostać o poziomie zgodności hello 130 i użyć planu zapytania wcześniejsze hello sugerowanej hello magazynu zapytań.</span><span class="sxs-lookup"><span data-stu-id="b5937-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="b5937-228">Tooleverage nowe funkcje i możliwości usługi Azure SQL Database (na którym jest uruchomiony program SQL Server 2016), ale są toochanges poufnych przez 130, poziom zgodności hello w ostateczności można rozważyć wymuszania hello wstecz poziom zgodności poziom toohello pasujące obciążenia przy użyciu instrukcji ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="b5937-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="b5937-229">Najpierw należy jednak pamiętać, że plan magazynu zapytań hello przypinanie opcji jest najlepszym wyjściem, ponieważ nie używa 130 przebywa zasadniczo na poziomie funkcjonalności hello w starszej wersji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b5937-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="b5937-230">Jeśli masz wielodostępnych aplikacji obejmujących wiele baz danych, może być konieczne tooupdate hello inicjowania obsługi logiki tooensure Twojego baz danych poziom zgodności spójne dla wszystkich baz danych; stary i nowo aprowizowanej z nich.</span><span class="sxs-lookup"><span data-stu-id="b5937-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="b5937-231">Na wydajność obciążenia aplikacji może być poufnych toohello fakt, że niektóre bazy danych są uruchomione na zgodność z różnych poziomach i w związku z tym spójności poziomu zgodności przez wszystkie bazy danych może być wymagane w porządku tooprovide hello takie same środowisko klientów tooyour wszystkie między hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="b5937-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="b5937-232">Należy pamiętać, że nie ma upoważnienia naprawdę jest zależna od wpływ hello poziom zgodności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5937-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="b5937-233">Ostatnio, dotyczące hello szacowania kardynalności oraz jak zmiana poziomu zgodności hello, przed kontynuowaniem w środowisku produkcyjnym, jest zalecane tootest obciążenie produkcji w obszarze hello nowe warunki toodetermine, jeśli aplikacja korzysta z ulepszenia szacowania kardynalności Hello.</span><span class="sxs-lookup"><span data-stu-id="b5937-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b5937-234">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b5937-234">Conclusion</span></span>
<span data-ttu-id="b5937-235">Za pomocą usługi Azure SQL Database toobenefit z wszystkie rozszerzenia SQL Server 2016 wyraźnie może zwiększyć Twojej wykonania zapytania.</span><span class="sxs-lookup"><span data-stu-id="b5937-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="b5937-236">Podobnie jak-jest!</span><span class="sxs-lookup"><span data-stu-id="b5937-236">Just as-is!</span></span> <span data-ttu-id="b5937-237">Oczywiście takich jak nowa funkcja poprawna ocena muszą być konfigurowane toodetermine hello dokładne warunki na jakich obciążenie bazy danych działa hello najlepiej.</span><span class="sxs-lookup"><span data-stu-id="b5937-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="b5937-238">Środowisko informuje, że większość obciążeń umożliwiają oczekiwanego tooat najmniej uruchamiana niewidocznie poziom zgodności 130, podczas korzystania z nowego zapytania przetwarzania, funkcje i nowego szacowania kardynalności.</span><span class="sxs-lookup"><span data-stu-id="b5937-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="b5937-239">Będący powiedział realistycznie rzecz biorąc, są zawsze niektóre wyjątki i wykonując prawidłowego ukończenia starannością toodetermine oceny ważne, ile będzie można korzystać z tych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="b5937-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="b5937-240">I ponownie hello magazynu zapytań może być dużą pomocy w tym tę pracę!</span><span class="sxs-lookup"><span data-stu-id="b5937-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="b5937-241">W miarę rozwoju środowisko SQL Azure, można oczekiwać, że poziom zgodności 140 w hello przyszłych.</span><span class="sxs-lookup"><span data-stu-id="b5937-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="b5937-242">Gdy czas jest odpowiednie, firma Microsoft rozpocznie się mówić co ten poziom zgodności w przyszłości 140 zostanie wyświetlone, tak samo, jak pokrótce omówiono tutaj 130 poziom zgodności jest Przywracanie dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="b5937-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="b5937-243">Teraz załóżmy nie zapomnij, od czerwca 2016 r. bazy danych SQL Azure ulegnie zmianie hello domyślny poziom zgodności z too130 120 dla nowo utworzonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5937-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="b5937-244">Należy pamiętać!</span><span class="sxs-lookup"><span data-stu-id="b5937-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="b5937-245">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="b5937-245">References</span></span>
* [<span data-ttu-id="b5937-246">Nowości w aparacie bazy danych</span><span class="sxs-lookup"><span data-stu-id="b5937-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="b5937-247">Blog: Magazyn zapytań: Rejestrator danych dla bazy danych, przez Borko Novakovic, czerwca 2016 8</span><span class="sxs-lookup"><span data-stu-id="b5937-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="b5937-248">Poziom zgodności bazy danych zmiany (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="b5937-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="b5937-249">ZMIANY W ZAKRESIE KONFIGURACJI BAZY DANYCH</span><span class="sxs-lookup"><span data-stu-id="b5937-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="b5937-250">Poziom zgodności 130 bazy danych Azure SQL V12</span><span class="sxs-lookup"><span data-stu-id="b5937-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="b5937-251">Optymalizacja Your plany zapytań z programu SQL Server 2014 narzędzia do szacowania kardynalności hello</span><span class="sxs-lookup"><span data-stu-id="b5937-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="b5937-252">Przewodnik indeksy magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="b5937-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="b5937-253">Blog: Ulepszone zapytania wydajności o poziomie zgodności 130 w bazie danych Azure SQL, przez Alain Lissoir maj 2016 6</span><span class="sxs-lookup"><span data-stu-id="b5937-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
