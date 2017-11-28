---
title: "wydajność indeksu magazynu kolumn aaaImprove SQL Azure | Dokumentacja firmy Microsoft"
description: "Zmniejsz wymagania dotyczące pamięci lub zwiększ hello dostępnej pamięci toomaximize hello liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="8ef8e-103">Maksymalizacja jakości i dla magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="8ef8e-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="8ef8e-104">Jakość i jest określana przez hello liczbę wierszy w grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="8ef8e-105">Zmniejsz wymagania dotyczące pamięci lub zwiększ hello dostępnej pamięci toomaximize hello liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="8ef8e-106">Użyj tych metody tooimprove kompresji szybkości i wydajności zapytań dla indeksów magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="8ef8e-107">Dlaczego hello i rozmiar ma znaczenie</span><span class="sxs-lookup"><span data-stu-id="8ef8e-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="8ef8e-108">Ponieważ indeks magazynu kolumn skanowania tabeli za pomocą skanowania segmentów kolumny z poszczególnych rowgroups, maksymalizacja hello liczbę wierszy w każdym i zwiększa wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="8ef8e-109">Gdy rowgroups ma dużą liczbę wierszy, kompresji danych zwiększa, co oznacza, że istnieje mniej tooread danych z dysku.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="8ef8e-110">Aby uzyskać więcej informacji o rowgroups, zobacz [przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="8ef8e-111">Rozmiar docelowy rowgroups</span><span class="sxs-lookup"><span data-stu-id="8ef8e-111">Target size for rowgroups</span></span>
<span data-ttu-id="8ef8e-112">Aby uzyskać najlepszą wydajność zapytań celem hello jest toomaximize hello liczba wierszy przypadających na grupy wierszy w indeksie magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="8ef8e-113">I może mieć maksymalnie 1 048 576 wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="8ef8e-114">Jego zgadzasz toonot ma hello maksymalna liczba wierszy przypadających na grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="8ef8e-115">Indeksy magazynu kolumn uzyskać dobrą wydajność, gdy rowgroups zawiera co najmniej 100 000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="8ef8e-116">Rowgroups można pobrać usuwane podczas kompresji</span><span class="sxs-lookup"><span data-stu-id="8ef8e-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="8ef8e-117">Podczas zbiorczego obciążenia lub magazynu kolumn odbudowywanie indeksu czasami nie ma wystarczającej ilości pamięci dostępnej toocompress hello wszystkie wiersze przeznaczone dla każdej grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="8ef8e-118">W przypadku wykorzystania pamięci indeksy magazynu kolumn trim hello rozmiary i dlatego może się powieść kompresji w hello magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="8ef8e-119">Usługi SQL Data Warehouse generuje błąd, w przypadku niewystarczającej ilości pamięci toocompress co najmniej 10 000 wierszy do każdej grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="8ef8e-120">Aby uzyskać więcej informacji dotyczących ładowania zbiorczego, zobacz [ładowanie zbiorcze do klastrowanego indeksu magazynu kolumn](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="8ef8e-121">Jak toomonitor i jakość</span><span class="sxs-lookup"><span data-stu-id="8ef8e-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="8ef8e-122">Brak udostępnia przydatne informacje, takie jak liczba wierszy w rowgroups i hello Przyczyna przycinanie, jeśli został przycinanie DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="8ef8e-123">Te informacje tooget DMV hello następującego widoku w postaci tooquery wygodny sposób można tworzyć na przycinanie grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="8ef8e-124">Hello trim_reason_desc informuje, czy został przycięty i hello (trim_reason_desc = NO_TRIM oznacza nie było żadnych przycinanie i grupę wierszy jest jakość).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="8ef8e-125">Witaj skutkiem przycinania oznaczać przedwczesny przycinanie i hello:</span><span class="sxs-lookup"><span data-stu-id="8ef8e-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="8ef8e-126">BULKLOAD: Z tego powodu przycinania jest używany podczas hello przychodzące partii wierszy dla obciążenia hello ma mniej niż 1 milion wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="8ef8e-127">Jeśli jest większa niż 100 000 wierszy wstawiane (w przeciwieństwie tooinserting do magazynu delta hello), ale zestawy hello tooBULKLOAD przycinania Przyczyna aparat Hello utworzy grupy wierszy skompresowane.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="8ef8e-128">W tym scenariuszu należy rozważyć zwiększenie tooaccumulate okna obciążenia sieci partii więcej wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="8ef8e-129">Ponadto obliczyć ponownie Twoje partycjonowania tooensure schematu nie jest zbyt szczegółowego jako grupy wierszy nie może obejmować granice partycji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="8ef8e-130">MEMORY_LIMITATION: toocreate grupy wiersza o 1 milion wierszy, określoną ilość pamięci roboczej jest wymagana przez aparat hello.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="8ef8e-131">Gdy dostępna pamięć hello ładowania sesji jest mniejszy niż wymagane hello pracy pamięci, grupy wierszy przedwcześnie uzyskać usuwane.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="8ef8e-132">następujące sekcje Hello Wyjaśnij, jak tooestimate pamięci wymagane i przydzielenie większej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="8ef8e-133">DICTIONARY_SIZE: Z tego powodu przycinania wskazuje, że przycinanie i wystąpił, ponieważ wystąpił co najmniej jednej kolumny typu string z ciągami Kardynalność szerokości i/lub wysokiego.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="8ef8e-134">Rozmiar słownika Hello jest ograniczona too16, który jest skompresowany MB w pamięci i po osiągnięciu tego limitu hello grupę wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="8ef8e-135">Jeśli zostanie uruchomione w tej sytuacji, należy wziąć pod uwagę izolowanie hello kolumny powodować problemy w osobnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="8ef8e-136">Jak tooestimate wymagania dotyczące pamięci</span><span class="sxs-lookup"><span data-stu-id="8ef8e-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="8ef8e-137">Witaj maksymalna ilość pamięci wymagana toocompress jednej grupy wierszy wynosi około</span><span class="sxs-lookup"><span data-stu-id="8ef8e-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="8ef8e-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="8ef8e-138">72 MB +</span></span>
- <span data-ttu-id="8ef8e-139">\#wiersze \* \#kolumn \* 8 bajtów +</span><span class="sxs-lookup"><span data-stu-id="8ef8e-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="8ef8e-140">\#wiersze \* \#krótki ciąg kolumn \* 32 bajtów +</span><span class="sxs-lookup"><span data-stu-id="8ef8e-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="8ef8e-141">\#długi ciąg kolumn \* 16 MB dla słownika kompresji</span><span class="sxs-lookup"><span data-stu-id="8ef8e-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="8ef8e-142">gdzie krótki ciąg kolumn używać typów danych ciąg < = 32 bajtów i użyj długi ciąg kolumn danych typu ciąg > 32 bajtów.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="8ef8e-143">Długie ciągi są kompresowane za pomocą metody kompresji przeznaczone do kompresowania tekstu.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="8ef8e-144">Ta metoda kompresji używa *słownika* toostore wzorce tekstu.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="8ef8e-145">Maksymalny rozmiar słownika Hello jest 16 MB.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="8ef8e-146">Istnieje tylko jeden słownika dla każdej kolumny długi ciąg hello grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="8ef8e-147">Szczegółowe omówienie wymagań pamięci magazynu kolumn, zobacz wideo [skalowania usługi Azure SQL Data Warehouse: wskazówki i konfiguracji](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="8ef8e-148">Wymagania dotyczące sposobów tooreduce pamięci</span><span class="sxs-lookup"><span data-stu-id="8ef8e-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="8ef8e-149">Użyj hello następujące techniki tooreduce hello wymagania dotyczące pamięci kompresowania rowgroups w indeksach magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="8ef8e-150">Użyj mniejszej liczby kolumn</span><span class="sxs-lookup"><span data-stu-id="8ef8e-150">Use fewer columns</span></span>
<span data-ttu-id="8ef8e-151">Jeśli to możliwe projektowanie hello tabeli z mniejszą liczbą kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="8ef8e-152">Podczas kompresji i do magazynu kolumn hello indeksu magazynu kolumn hello oddzielnie kompresuje każdego segmentu kolumny.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="8ef8e-153">Witaj w związku z tym wymagania dotyczące pamięci, które toocompress i zwiększyć jako hello liczba wzrasta kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="8ef8e-154">Użyj mniejszej liczby kolumn ciągu</span><span class="sxs-lookup"><span data-stu-id="8ef8e-154">Use fewer string columns</span></span>
<span data-ttu-id="8ef8e-155">Kolumny danych typu ciąg wymaga więcej pamięci niż liczbowych i typy danych Data.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="8ef8e-156">tooreduce wymagania dotyczące pamięci, rozważ usunięcie kolumny ciągu z tabel faktów i umieszczania ich w mniejszych tabele wymiarów.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="8ef8e-157">Wymagania dotyczące pamięci dodatkowe ciąg kompresji:</span><span class="sxs-lookup"><span data-stu-id="8ef8e-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="8ef8e-158">Typy danych parametry się znaki too32 może wymagać 32 bajtów dodatkowe na wartość.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="8ef8e-159">Typy danych ciąg z więcej niż 32 znaki są kompresowane przy użyciu metod słownika.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="8ef8e-160">Każda kolumna hello i może wymagać się tooan dodatkowe 16 MB toobuild hello słownika.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="8ef8e-161">Unikaj nadmiernego partycjonowania</span><span class="sxs-lookup"><span data-stu-id="8ef8e-161">Avoid over-partitioning</span></span>

<span data-ttu-id="8ef8e-162">Indeksy magazynu kolumn utworzyć rowgroups co najmniej jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="8ef8e-163">W usłudze SQL Data Warehouse hello liczby partycji rozwoju szybko ponieważ hello dane są przesyłane i każdej dystrybucji jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="8ef8e-164">Jeśli tabela hello ma zbyt wiele partycji, może nie być wystarczającej ilości rowgroups hello toofill wierszy.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="8ef8e-165">Brak Hello wierszy nie tworzy wykorzystania pamięci podczas kompresji, ale prowadzi toorowgroups, który nie będzie hello najlepszą wydajność zapytań magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="8ef8e-166">Inny Przyczyna tooavoid nadmiernie Partycjonowanie jest pamięci w czasie ładowania wierszy do indeksu magazynu kolumn dla partycjonowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="8ef8e-167">Podczas ładowania większej liczby partycji można odebrać hello przychodzących wierszy, które są przechowywane w pamięci, dopóki każda partycja ma za mało toobe wierszy skompresowane.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="8ef8e-168">Zbyt wiele partycji mających tworzy wykorzystania pamięci dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="8ef8e-169">Uproszczenie hello obciążenia zapytania</span><span class="sxs-lookup"><span data-stu-id="8ef8e-169">Simplify hello load query</span></span>

<span data-ttu-id="8ef8e-170">Witaj bazy danych udziałów hello przydział pamięci dla zapytania wśród wszystkich operatorów hello w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="8ef8e-171">Jeśli zapytanie obciążenia sortowania złożonego i sprzężeń, zostanie zmniejszona pamięci hello kompresji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="8ef8e-172">Projektowanie hello obciążenia zapytania toofocus tylko na ładowanie hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="8ef8e-173">Przekształcenia toorun na powitania danych, należy uruchomić je oddzielnie od hello obciążenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="8ef8e-174">Na przykład etap hello dane w tabeli sterty, uruchom przekształcenia hello, a następnie załadować hello Tabela przemieszczania do hello indeksu magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="8ef8e-175">Można również najpierw załadować dane hello, a następnie użyć hello MPP systemu tootransform hello danych.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="8ef8e-176">Dostosuj MAXDOP</span><span class="sxs-lookup"><span data-stu-id="8ef8e-176">Adjust MAXDOP</span></span>

<span data-ttu-id="8ef8e-177">Każdy dystrybucji kompresuje rowgroups do magazynu kolumn hello równoległe, gdy jest dostępna więcej niż jednego rdzenia procesora CPU na dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="8ef8e-178">Równoległość Hello wymaga dodatkowych zasobów pamięci, które mogą prowadzić toomemory wykorzystania i przycinanie i.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="8ef8e-179">tooreduce wykorzystania pamięci, można użyć hello MAXDOP zapytania wskazówka tooforce hello obciążenia operacji toorun w trybie serial w ramach poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="8ef8e-180">Sposoby tooallocate większej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="8ef8e-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="8ef8e-181">DWU rozmiaru i hello zasobów klasy użytkownika ze sobą określić ilość pamięci dostępnej dla zapytania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="8ef8e-182">tooincrease hello pamięci przyznać dla zapytania obciążenia, możesz zwiększyć hello liczby jednostek dwu lub zwiększyć hello klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="8ef8e-183">Witaj tooincrease jednostek dwu, zobacz [sposób skalowania wydajności?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="8ef8e-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="8ef8e-184">Klasa zasobów hello toochange dla zapytania, zobacz [zmienić przykład klasy zasobów użytkownika](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="8ef8e-185">Na przykład na DWU 100 użytkownika w klasie zasobu smallrc hello służy 100 MB pamięci dla poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="8ef8e-186">Aby hello uzyskać szczegółowe informacje, zobacz [współbieżność w usłudze SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="8ef8e-187">Załóżmy, że należy określić, czy potrzebujesz 700 MB pamięci tooget wysokiej jakości i rozmiary.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="8ef8e-188">Poniższe przykłady pokazują, jak można uruchomić zapytania obciążenia hello o wystarczającej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="8ef8e-189">Korzystając z DWU 1000 i mediumrc, Twoje przydział pamięci jest 800 MB</span><span class="sxs-lookup"><span data-stu-id="8ef8e-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="8ef8e-190">Korzystając z DWU 600 i largerc, Twoje przydział pamięci jest 800 MB.</span><span class="sxs-lookup"><span data-stu-id="8ef8e-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8ef8e-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ef8e-191">Next steps</span></span>

<span data-ttu-id="8ef8e-192">toofind więcej sposobów tooimprove wydajności w usłudze SQL Data Warehouse, zobacz hello [wydajności — omówienie](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="8ef8e-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
