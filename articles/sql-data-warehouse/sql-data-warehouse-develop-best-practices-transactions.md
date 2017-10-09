---
title: "Transakcje aaaOptimizing dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Najlepszych rozwiązań o pisaniu aktualizacje wydajne transakcji w magazynie danych SQL Azure"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="7e24c-103">Optymalizacja transakcji dla magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="7e24c-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="7e24c-104">W tym artykule opisano, jak toooptimize hello wydajności kodu transakcyjnego przy jednoczesnym zmniejszeniu ryzyka dla długich cofnięcia.</span><span class="sxs-lookup"><span data-stu-id="7e24c-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="7e24c-105">Rejestrowanie i transakcji</span><span class="sxs-lookup"><span data-stu-id="7e24c-105">Transactions and logging</span></span>
<span data-ttu-id="7e24c-106">Transakcje są ważne składnika aparacie relacyjnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="7e24c-107">Usługa SQL Data Warehouse używa transakcji podczas modyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="7e24c-108">Te transakcje można jawnych ani niejawnych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="7e24c-109">Pojedynczy `INSERT`, `UPDATE` i `DELETE` instrukcje są wszystkie przykłady w transakcji niejawnej.</span><span class="sxs-lookup"><span data-stu-id="7e24c-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="7e24c-110">Jawnych transakcji są zapisywane bezpośrednio przez dewelopera przy użyciu `BEGIN TRAN`, `COMMIT TRAN` lub `ROLLBACK TRAN` i są zazwyczaj używane do wielu instrukcji modyfikacji muszą toobe powiązane razem w jednym Atomowej jednostki.</span><span class="sxs-lookup"><span data-stu-id="7e24c-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="7e24c-111">Usługa Azure SQL Data Warehouse zatwierdza przy użyciu dzienników transakcji toohello zmian w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="7e24c-112">Rozkład każdy ma własny dziennik transakcji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="7e24c-113">Zapisy dziennika transakcji są automatyczne.</span><span class="sxs-lookup"><span data-stu-id="7e24c-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="7e24c-114">Nie jest wymagana żadna konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="7e24c-114">There is no configuration required.</span></span> <span data-ttu-id="7e24c-115">Jednak podczas tego procesu gwarantuje zapisu hello go wprowadzić obciążenia w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="7e24c-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="7e24c-116">Pisanie kodu transakcyjnie wydajne, można zminimalizować wpływ ten.</span><span class="sxs-lookup"><span data-stu-id="7e24c-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="7e24c-117">Transakcyjnie efektywne zasadniczo mieszczą się na dwie kategorie.</span><span class="sxs-lookup"><span data-stu-id="7e24c-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="7e24c-118">Korzystaj z konstrukcji minimalne rejestrowanie, jeśli jest to możliwe</span><span class="sxs-lookup"><span data-stu-id="7e24c-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="7e24c-119">Przetwarzania danych przy użyciu pojedynczego tooavoid zakresie partie długotrwałe transakcje</span><span class="sxs-lookup"><span data-stu-id="7e24c-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="7e24c-120">Przyjmuje partycji przełączania wzorca dla dużych modyfikacje tooa podane partycji</span><span class="sxs-lookup"><span data-stu-id="7e24c-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="7e24c-121">Minimalny a pełne rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="7e24c-121">Minimal vs. full logging</span></span>
<span data-ttu-id="7e24c-122">W przeciwieństwie do pełni zarejestrowanych operacji, korzystających z hello transakcji dziennika tookeep Śledź każdy wiersz zmiany, minimalny zestaw zarejestrowanych operacji zachować informacje o zakresie alokacji i tylko zmiany metadanych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="7e24c-123">W związku z tym minimalne rejestrowanie obejmuje hello tylko te informacje, które są wymagane toorollback hello transakcji w przypadku hello awarii lub jawnego żądania rejestrowania (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="7e24c-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="7e24c-124">Jak znacznie mniej informacje są śledzone w dzienniku transakcji hello, minimalny zestaw zarejestrowanych operacji działa lepiej niż podobnie rozmiarze pełni zarejestrowanych operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="7e24c-125">Ponadto ponieważ zapisy mniejszą liczbę przejść hello dziennika transakcji, generowany jest znacznie mniejszą ilość danych dziennika, i dlatego jest efektywne więcej operacji We/Wy.</span><span class="sxs-lookup"><span data-stu-id="7e24c-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="7e24c-126">limity bezpieczeństwa transakcji Hello mają zastosowanie tylko operacje toofully rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="7e24c-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="7e24c-127">Minimalny zestaw zarejestrowanych operacji mogą uczestniczyć w jawnych transakcji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="7e24c-128">Wszystkie zmiany w alokacji struktur są śledzone, jest możliwe tooroll wstecz minimalny rejestrowane operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="7e24c-129">Jest ważne, rejestrowana toounderstand, że zmiana hello jest "minimalny zestaw" nie jest, które nie zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="7e24c-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="7e24c-130">Minimalny zestaw zarejestrowanych operacji</span><span class="sxs-lookup"><span data-stu-id="7e24c-130">Minimally logged operations</span></span>
<span data-ttu-id="7e24c-131">Hello są w stanie są rejestrowane następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="7e24c-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="7e24c-132">UTWÓRZ TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="7e24c-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="7e24c-133">INSERT... WYBIERZ</span><span class="sxs-lookup"><span data-stu-id="7e24c-133">INSERT..SELECT</span></span>
* <span data-ttu-id="7e24c-134">TWORZENIE INDEKSU</span><span class="sxs-lookup"><span data-stu-id="7e24c-134">CREATE INDEX</span></span>
* <span data-ttu-id="7e24c-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="7e24c-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="7e24c-136">INDEKS</span><span class="sxs-lookup"><span data-stu-id="7e24c-136">DROP INDEX</span></span>
* <span data-ttu-id="7e24c-137">OBCIĄĆ TABELI</span><span class="sxs-lookup"><span data-stu-id="7e24c-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="7e24c-138">TABELĘ</span><span class="sxs-lookup"><span data-stu-id="7e24c-138">DROP TABLE</span></span>
* <span data-ttu-id="7e24c-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="7e24c-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="7e24c-140">Operacje przenoszenia danych wewnętrznych (takich jak `BROADCAST` i `SHUFFLE`) nie dotyczy limitu bezpieczeństwa transakcji hello.</span><span class="sxs-lookup"><span data-stu-id="7e24c-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="7e24c-141">Minimalne rejestrowanie z ładowanie zbiorcze</span><span class="sxs-lookup"><span data-stu-id="7e24c-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="7e24c-142">`CTAS`i `INSERT...SELECT` zarówno zbiorcze operacje obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7e24c-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="7e24c-143">Jednak zarówno wpływało definicji tabeli docelowej hello i zależą od scenariusza obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="7e24c-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="7e24c-144">Poniżej znajduje się tabela, która wyjaśnia, jeśli operacji zbiorczej zostanie całkowicie lub minimalny zarejestrowane:</span><span class="sxs-lookup"><span data-stu-id="7e24c-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="7e24c-145">Podstawowy indeks</span><span class="sxs-lookup"><span data-stu-id="7e24c-145">Primary Index</span></span> | <span data-ttu-id="7e24c-146">Scenariusz obciążenia</span><span class="sxs-lookup"><span data-stu-id="7e24c-146">Load Scenario</span></span> | <span data-ttu-id="7e24c-147">Tryb rejestrowania</span><span class="sxs-lookup"><span data-stu-id="7e24c-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e24c-148">Sterty</span><span class="sxs-lookup"><span data-stu-id="7e24c-148">Heap</span></span> |<span data-ttu-id="7e24c-149">Dowolne</span><span class="sxs-lookup"><span data-stu-id="7e24c-149">Any</span></span> |<span data-ttu-id="7e24c-150">**Minimalny**</span><span class="sxs-lookup"><span data-stu-id="7e24c-150">**Minimal**</span></span> |
| <span data-ttu-id="7e24c-151">Indeks klastrowany</span><span class="sxs-lookup"><span data-stu-id="7e24c-151">Clustered Index</span></span> |<span data-ttu-id="7e24c-152">Tabela docelowa pusty</span><span class="sxs-lookup"><span data-stu-id="7e24c-152">Empty target table</span></span> |<span data-ttu-id="7e24c-153">**Minimalny**</span><span class="sxs-lookup"><span data-stu-id="7e24c-153">**Minimal**</span></span> |
| <span data-ttu-id="7e24c-154">Indeks klastrowany</span><span class="sxs-lookup"><span data-stu-id="7e24c-154">Clustered Index</span></span> |<span data-ttu-id="7e24c-155">Załadować wierszy nie pokrywają się z istniejących stron w lokalizacji docelowej</span><span class="sxs-lookup"><span data-stu-id="7e24c-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="7e24c-156">**Minimalny**</span><span class="sxs-lookup"><span data-stu-id="7e24c-156">**Minimal**</span></span> |
| <span data-ttu-id="7e24c-157">Indeks klastrowany</span><span class="sxs-lookup"><span data-stu-id="7e24c-157">Clustered Index</span></span> |<span data-ttu-id="7e24c-158">Nakładanie się załadować wierszy z istniejących stron w lokalizacji docelowej</span><span class="sxs-lookup"><span data-stu-id="7e24c-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="7e24c-159">Pełne</span><span class="sxs-lookup"><span data-stu-id="7e24c-159">Full</span></span> |
| <span data-ttu-id="7e24c-160">Klastrowany indeks magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="7e24c-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="7e24c-161">Rozmiar partii > = 102400 na partycji wyrównane dystrybucji</span><span class="sxs-lookup"><span data-stu-id="7e24c-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="7e24c-162">**Minimalny**</span><span class="sxs-lookup"><span data-stu-id="7e24c-162">**Minimal**</span></span> |
| <span data-ttu-id="7e24c-163">Klastrowany indeks magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="7e24c-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="7e24c-164">Rozmiar < 102400 na partycji wyrównane dystrybucji partii</span><span class="sxs-lookup"><span data-stu-id="7e24c-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="7e24c-165">Pełne</span><span class="sxs-lookup"><span data-stu-id="7e24c-165">Full</span></span> |

<span data-ttu-id="7e24c-166">Warto zauważyć, że wszystkie zapisy tooupdate dodatkowej lub nieklastrowanych indeksów zawsze będą pełni rejestrowane operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e24c-167">Magazyn danych SQL ma 60 dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="7e24c-168">W związku z tym zakładając, że wszystkie wiersze są równomiernie, a kierowanych do jednej partycji, Twoje partii musi toocontain 6,144,000 wierszy lub większy toobe minimalny rejestrowane podczas zapisywania tooa klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="7e24c-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="7e24c-169">Jeśli hello tabela jest podzielona na partycje i wierszy hello wstawiane span granice partycji, wymagana będzie 6,144,000 wierszy na granicy partycji przy założeniu nawet danych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="7e24c-170">Każdej partycji w każdej dystrybucji niezależnie przekraczać hello 102 400 wiersza próg toobe insert hello rejestrowane w hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="7e24c-171">Ładowanie danych do niepustej tabeli z indeksem klastrowanym często może zawierać mieszaninę pełni zarejestrowane i zarejestrowane minimalny zestaw wierszy.</span><span class="sxs-lookup"><span data-stu-id="7e24c-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="7e24c-172">Indeks klastrowany jest drzewo zrównoważony (b drzewa) stron.</span><span class="sxs-lookup"><span data-stu-id="7e24c-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="7e24c-173">Jeśli strona hello zapisywana tooalready zawiera wiersze z innej transakcji, następnie zapisuje te będą pełni rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="7e24c-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="7e24c-174">Jednak jeśli strona hello jest pusty następnie hello zapisu toothat strona zostanie minimalny zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="7e24c-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="7e24c-175">Optymalizacja usuwa</span><span class="sxs-lookup"><span data-stu-id="7e24c-175">Optimizing deletes</span></span>
<span data-ttu-id="7e24c-176">`DELETE`jest całkowicie zarejestrowanych operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="7e24c-177">Jeśli potrzebujesz toodelete dużej ilości danych w tabeli lub partycję, często warto więcej zbyt`SELECT` hello danych mają tookeep, które mogą być uruchamiane jako minimalny zestaw zarejestrowanych operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="7e24c-178">tooaccomplish, Utwórz nową tabelę z [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="7e24c-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="7e24c-179">Po utworzeniu, użyj [zmienić] [ RENAME] tooswap limit starego tabeli z tabelą hello nowo utworzona.</span><span class="sxs-lookup"><span data-stu-id="7e24c-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="7e24c-180">Optymalizacja aktualizacji</span><span class="sxs-lookup"><span data-stu-id="7e24c-180">Optimizing updates</span></span>
<span data-ttu-id="7e24c-181">`UPDATE`jest całkowicie zarejestrowanych operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="7e24c-182">Jeśli potrzebujesz tooupdate dużą liczbę wierszy w tabeli lub partycję często jest znacznie bardziej wydajne toouse minimalny zestaw zarejestrowanych operacji takich jak [CTAS] [ CTAS] toodo tak.</span><span class="sxs-lookup"><span data-stu-id="7e24c-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="7e24c-183">W hello przykładzie poniżej aktualizacji pełnej tabeli został przekonwertowany tooa `CTAS` , dzięki czemu możliwe jest minimalnym rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="7e24c-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="7e24c-184">W takim przypadku retrospektywnie dodajemy sprzedaży toohello dyskontowa kwota w tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="7e24c-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="7e24c-185">Ponowne tworzenie dużych tabel mogą korzystać z funkcji zarządzania obciążenie SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e24c-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="7e24c-186">Dla bardziej szczegółowe informacje można znaleźć w sekcji Zarządzanie obciążenia toohello w hello [współbieżności] [ concurrency] artykułu.</span><span class="sxs-lookup"><span data-stu-id="7e24c-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="7e24c-187">Optymalizacja przełączania partycji</span><span class="sxs-lookup"><span data-stu-id="7e24c-187">Optimizing with partition switching</span></span>
<span data-ttu-id="7e24c-188">W przypadku zastosowania zmian dużą skalę w [tabeli partycji][table partition], partycji przełączania wzorca tworzy wiele znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="7e24c-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="7e24c-189">Jeśli hello modyfikacji danych jest znacząca i obejmuje wiele partycji, po prostu Iterowanie za pośrednictwem partycje hello osiąga hello takiego samego wyniku.</span><span class="sxs-lookup"><span data-stu-id="7e24c-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="7e24c-190">tooperform kroki Hello przełącznik partycji są następujące:</span><span class="sxs-lookup"><span data-stu-id="7e24c-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="7e24c-191">Utwórz pustą z partycji</span><span class="sxs-lookup"><span data-stu-id="7e24c-191">Create an empty out partition</span></span>
2. <span data-ttu-id="7e24c-192">Przeprowadź aktualizację"hello" CTAS</span><span class="sxs-lookup"><span data-stu-id="7e24c-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="7e24c-193">Przełącz się hello istniejących danych toohello limit tabeli</span><span class="sxs-lookup"><span data-stu-id="7e24c-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="7e24c-194">Przełącz hello nowe dane.</span><span class="sxs-lookup"><span data-stu-id="7e24c-194">Switch in hello new data</span></span>
5. <span data-ttu-id="7e24c-195">Czyszczenie danych hello</span><span class="sxs-lookup"><span data-stu-id="7e24c-195">Clean up hello data</span></span>

<span data-ttu-id="7e24c-196">Jednak toohelp zidentyfikować tooswitch partycje hello zostanie najpierw musimy toobuild procedury pomocnika, takich jak hello jedną poniżej.</span><span class="sxs-lookup"><span data-stu-id="7e24c-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="7e24c-197">Ta procedura maksymalizuje ponownego użycia kodu i przechowuje przełączania przykład mniejszych hello partycji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="7e24c-198">Poniższy kod Hello pokazuje, że hello pięć kroków wymienionych powyżej tooachieve pełne partycji przełączania procedury.</span><span class="sxs-lookup"><span data-stu-id="7e24c-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="7e24c-199">Minimalizowanie rejestrowanie z małych partii</span><span class="sxs-lookup"><span data-stu-id="7e24c-199">Minimize logging with small batches</span></span>
<span data-ttu-id="7e24c-200">W przypadku operacji modyfikacji dużej ilości danych może dokonać znaczeniu toodivide hello operacji na fragmenty lub partie jednostki hello tooscope pracy.</span><span class="sxs-lookup"><span data-stu-id="7e24c-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="7e24c-201">Poniżej znajduje się przykład pracy.</span><span class="sxs-lookup"><span data-stu-id="7e24c-201">A working example is provided below.</span></span> <span data-ttu-id="7e24c-202">rozmiar partii Hello ustawiono tooa trivial numer toohighlight hello technik.</span><span class="sxs-lookup"><span data-stu-id="7e24c-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="7e24c-203">W rzeczywistości rozmiar partii hello jest znacznie większe.</span><span class="sxs-lookup"><span data-stu-id="7e24c-203">In reality hello batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="7e24c-204">Wstrzymywanie i skalowanie wskazówki</span><span class="sxs-lookup"><span data-stu-id="7e24c-204">Pause and scaling guidance</span></span>
<span data-ttu-id="7e24c-205">Usługa Azure SQL Data Warehouse pozwala wstrzymać, wznowić i skalowanie magazynu danych na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7e24c-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="7e24c-206">Po wstrzymaniu lub skalować magazyn danych SQL jest ważne toounderstand wszystkich transakcji locie kończą natychmiast; powoduje toobe wszystkie otwarte transakcje wycofana.</span><span class="sxs-lookup"><span data-stu-id="7e24c-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="7e24c-207">Jeśli obciążenie wystawił długotrwałe i modyfikacji niepełne dane przed Wstrzymaj toohello lub operacji skalowania, a następnie tej pracy należy toobe cofnięta.</span><span class="sxs-lookup"><span data-stu-id="7e24c-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="7e24c-208">Może to mieć wpływ na powitania czas toopause lub skalowania bazy danych magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7e24c-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7e24c-209">Zarówno `UPDATE` i `DELETE` są całkowicie zarejestrowanych operacji i dlatego te Cofnij/ponów operacji może potrwać znacznie dłużej, niż równoważne rejestrowane operacji.</span><span class="sxs-lookup"><span data-stu-id="7e24c-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="7e24c-210">najlepszym scenariuszu Hello jest toolet transmitowane danych modyfikacji transakcji ukończone przed toopausing lub skalowania SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e24c-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="7e24c-211">Jednak to może nie zawsze być praktyczne.</span><span class="sxs-lookup"><span data-stu-id="7e24c-211">However, this may not always be practical.</span></span> <span data-ttu-id="7e24c-212">ryzyka hello toomitigate wycofania długie, weź pod uwagę jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="7e24c-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="7e24c-213">Napisz ponownie przy użyciu długotrwałe operacje [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="7e24c-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="7e24c-214">Operacja hello podziału na fragmenty o różnych; korzysta z podzbioru hello wierszy</span><span class="sxs-lookup"><span data-stu-id="7e24c-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e24c-215">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e24c-215">Next steps</span></span>
<span data-ttu-id="7e24c-216">Zobacz [transakcje w usłudze SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn więcej informacji na temat poziomów izolacji i limity transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="7e24c-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="7e24c-217">Omówienie innych najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7e24c-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

