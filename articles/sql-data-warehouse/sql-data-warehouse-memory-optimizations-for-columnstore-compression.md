---
title: "Poprawić wydajność indeksu magazynu kolumn w Azure SQL | Dokumentacja firmy Microsoft"
description: "Zmniejsz wymagania dotyczące pamięci lub zwiększ ilość dostępnej pamięci, aby zmaksymalizować liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy."
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
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="fb800-103">Maksymalizacja jakości i dla magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="fb800-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="fb800-104">Jakość i zależy od liczby wierszy w grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="fb800-105">Zmniejsz wymagania dotyczące pamięci lub zwiększ ilość dostępnej pamięci, aby zmaksymalizować liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="fb800-106">Użycia tych metod w celu zwiększenia kompresji i zbadać wydajność dla indeksów magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="fb800-107">Dlaczego rozmiar i ma znaczenie</span><span class="sxs-lookup"><span data-stu-id="fb800-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="fb800-108">Ponieważ indeks magazynu kolumn skanowania tabeli za pomocą skanowania segmentów kolumny z poszczególnych rowgroups, maksymalizacja liczby wierszy w każdym i zwiększa wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="fb800-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="fb800-109">Gdy rowgroups ma dużą liczbę wierszy, kompresji danych zwiększa, co oznacza, że jest mniejsza ilość danych do odczytu z dysku.</span><span class="sxs-lookup"><span data-stu-id="fb800-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="fb800-110">Aby uzyskać więcej informacji o rowgroups, zobacz [przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb800-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="fb800-111">Rozmiar docelowy rowgroups</span><span class="sxs-lookup"><span data-stu-id="fb800-111">Target size for rowgroups</span></span>
<span data-ttu-id="fb800-112">Aby uzyskać najlepszą wydajność zapytań celem jest zwiększenie liczby wierszy na grupy wierszy w indeksie magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="fb800-113">I może mieć maksymalnie 1 048 576 wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="fb800-114">Ma nic złego, nie ma maksymalną liczbę wierszy na grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="fb800-115">Indeksy magazynu kolumn uzyskać dobrą wydajność, gdy rowgroups zawiera co najmniej 100 000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="fb800-116">Rowgroups można pobrać usuwane podczas kompresji</span><span class="sxs-lookup"><span data-stu-id="fb800-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="fb800-117">Podczas zbiorczego obciążenia lub magazynu kolumn odbudowywanie indeksu czasami nie ma wystarczającej ilości pamięci do skompresowania wszystkie wiersze, które są przeznaczone dla każdej grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="fb800-118">W przypadku wykorzystania pamięci indeksy magazynu kolumn trim rozmiary i dlatego może się powieść kompresji do magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="fb800-119">Jeśli jest za mało pamięci do skompresowania co najmniej 10 000 wierszy do każdej grupy wierszy, SQL Data Warehouse generuje błąd.</span><span class="sxs-lookup"><span data-stu-id="fb800-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="fb800-120">Aby uzyskać więcej informacji dotyczących ładowania zbiorczego, zobacz [ładowanie zbiorcze do klastrowanego indeksu magazynu kolumn](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="fb800-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="fb800-121">Jak monitorować i jakość</span><span class="sxs-lookup"><span data-stu-id="fb800-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="fb800-122">Brak udostępnia przydatne informacje, takie jak liczba wierszy w rowgroups i przyczynę przycinanie, jeśli został przycinanie DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats).</span><span class="sxs-lookup"><span data-stu-id="fb800-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="fb800-123">Można utworzyć następującego widoku jako wygodny sposób na zapytania DMV ten można pobrać informacji na temat przycinanie i.</span><span class="sxs-lookup"><span data-stu-id="fb800-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

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

<span data-ttu-id="fb800-124">Trim_reason_desc informuje, czy został przycięty grupy wierszy (trim_reason_desc = NO_TRIM oznacza nie było żadnych przycinanie i grupę wierszy jest jakość).</span><span class="sxs-lookup"><span data-stu-id="fb800-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="fb800-125">Skutkiem przycinania oznaczać przedwczesny przycinanie grupy wierszy:</span><span class="sxs-lookup"><span data-stu-id="fb800-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="fb800-126">BULKLOAD: Z tego powodu przycinania jest używany, gdy przychodzący partii wierszy obciążenia ma mniej niż 1 milion wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="fb800-127">Aparat spowoduje utworzenie grupy wierszy skompresowany, jeśli jest większa niż 100 000 wierszy wstawiane (zamiast wstawianie do magazynu delta), ale ustawia przycinania Przyczyna BULKLOAD.</span><span class="sxs-lookup"><span data-stu-id="fb800-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="fb800-128">W tym scenariuszu należy rozważyć zwiększenie obciążenia partii okna gromadzone więcej wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="fb800-129">Ponadto obliczyć ponownie Twoje schemat partycjonowania, aby upewnić się, że nie jest on zbyt szczegółowego jako grupy wierszy nie może obejmować granice partycji.</span><span class="sxs-lookup"><span data-stu-id="fb800-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="fb800-130">MEMORY_LIMITATION: Tworzenie grup wiersza o 1 milion wierszy, określoną ilość pamięci roboczej jest wymagana przez aparat.</span><span class="sxs-lookup"><span data-stu-id="fb800-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="fb800-131">Gdy dostępna pamięć sesji ładowania jest mniejsza od wymaganej pamięci pracy, grupy wierszy przedwcześnie uzyskać usuwane.</span><span class="sxs-lookup"><span data-stu-id="fb800-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="fb800-132">W poniższych sekcjach opisano sposób szacowania pamięci wymaganej i przydzielić więcej pamięci.</span><span class="sxs-lookup"><span data-stu-id="fb800-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="fb800-133">DICTIONARY_SIZE: Z tego powodu przycinania wskazuje, że przycinanie i wystąpił, ponieważ wystąpił co najmniej jednej kolumny typu string z ciągami Kardynalność szerokości i/lub wysokiego.</span><span class="sxs-lookup"><span data-stu-id="fb800-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="fb800-134">Rozmiar słownika może zawierać maksymalnie 16 MB pamięci i jest skompresowany po osiągnięciu tego limitu grupę wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="fb800-135">Jeśli zostanie uruchomione w tej sytuacji, należy wziąć pod uwagę izolowanie kolumnie powodować problemy w osobnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fb800-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="fb800-136">Sposób oszacować wymagania dotyczące pamięci</span><span class="sxs-lookup"><span data-stu-id="fb800-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="fb800-137">Maksymalna wymagana ilość pamięci do skompresowania i jeden wynosi około</span><span class="sxs-lookup"><span data-stu-id="fb800-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="fb800-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="fb800-138">72 MB +</span></span>
- <span data-ttu-id="fb800-139">\#wiersze \* \#kolumn \* 8 bajtów +</span><span class="sxs-lookup"><span data-stu-id="fb800-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="fb800-140">\#wiersze \* \#krótki ciąg kolumn \* 32 bajtów +</span><span class="sxs-lookup"><span data-stu-id="fb800-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="fb800-141">\#długi ciąg kolumn \* 16 MB dla słownika kompresji</span><span class="sxs-lookup"><span data-stu-id="fb800-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="fb800-142">gdzie krótki ciąg kolumn używać typów danych ciąg < = 32 bajtów i użyj długi ciąg kolumn danych typu ciąg > 32 bajtów.</span><span class="sxs-lookup"><span data-stu-id="fb800-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="fb800-143">Długie ciągi są kompresowane za pomocą metody kompresji przeznaczone do kompresowania tekstu.</span><span class="sxs-lookup"><span data-stu-id="fb800-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="fb800-144">Ta metoda kompresji używa *słownika* do przechowywania wzorce tekstu.</span><span class="sxs-lookup"><span data-stu-id="fb800-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="fb800-145">Maksymalny rozmiar słownik jest 16 MB.</span><span class="sxs-lookup"><span data-stu-id="fb800-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="fb800-146">Istnieje tylko jeden słownika dla każdej kolumny i długi ciąg.</span><span class="sxs-lookup"><span data-stu-id="fb800-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="fb800-147">Szczegółowe omówienie wymagań pamięci magazynu kolumn, zobacz wideo [skalowania usługi Azure SQL Data Warehouse: wskazówki i konfiguracji](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="fb800-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="fb800-148">Sposoby Zmniejsz wymagania dotyczące pamięci</span><span class="sxs-lookup"><span data-stu-id="fb800-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="fb800-149">Następujące techniki umożliwiają zmniejszyć wymagania dotyczące pamięci kompresowania rowgroups w indeksach magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="fb800-150">Użyj mniejszej liczby kolumn</span><span class="sxs-lookup"><span data-stu-id="fb800-150">Use fewer columns</span></span>
<span data-ttu-id="fb800-151">Jeśli to możliwe projektowanie tabeli z mniejszą liczbą kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="fb800-152">Podczas kompresowania i do magazynu kolumn, indeks magazynu kolumn kompresuje osobno każdy z segmentów kolumny.</span><span class="sxs-lookup"><span data-stu-id="fb800-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="fb800-153">W związku z tym wymagania dotyczące pamięci do skompresowania i zwiększyć jako liczba wzrasta kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="fb800-154">Użyj mniejszej liczby kolumn ciągu</span><span class="sxs-lookup"><span data-stu-id="fb800-154">Use fewer string columns</span></span>
<span data-ttu-id="fb800-155">Kolumny danych typu ciąg wymaga więcej pamięci niż liczbowych i typy danych Data.</span><span class="sxs-lookup"><span data-stu-id="fb800-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="fb800-156">Aby zmniejszyć wymagania dotyczące pamięci, rozważ usunięcie kolumny ciągu z tabel faktów i umieszczania ich w mniejszych tabele wymiarów.</span><span class="sxs-lookup"><span data-stu-id="fb800-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="fb800-157">Wymagania dotyczące pamięci dodatkowe ciąg kompresji:</span><span class="sxs-lookup"><span data-stu-id="fb800-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="fb800-158">Typy danych w ciągu maksymalnie 32 znaki może wymagać 32 bajtów dodatkowe na wartość.</span><span class="sxs-lookup"><span data-stu-id="fb800-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="fb800-159">Typy danych ciąg z więcej niż 32 znaki są kompresowane przy użyciu metod słownika.</span><span class="sxs-lookup"><span data-stu-id="fb800-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="fb800-160">Każda kolumna i może wymagać maksymalnie dodatkowe 16 MB do tworzenia słownika.</span><span class="sxs-lookup"><span data-stu-id="fb800-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="fb800-161">Unikaj nadmiernego partycjonowania</span><span class="sxs-lookup"><span data-stu-id="fb800-161">Avoid over-partitioning</span></span>

<span data-ttu-id="fb800-162">Indeksy magazynu kolumn utworzyć rowgroups co najmniej jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="fb800-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="fb800-163">W usłudze SQL Data Warehouse liczba partycji rozwoju szybko ponieważ dane są przesyłane i każdej dystrybucji jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="fb800-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="fb800-164">Jeśli tabela zawiera zbyt wiele partycji, może nie być wystarczająco dużo wierszy, aby wypełnić rowgroups.</span><span class="sxs-lookup"><span data-stu-id="fb800-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="fb800-165">Brak wierszy nie tworzy wykorzystania pamięci podczas kompresji, ale prowadzi do rowgroups, który nie będzie najlepszą wydajność zapytań magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="fb800-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="fb800-166">Kolejny powód, aby uniknąć nadmiernego partycjonowania jest pamięci w czasie ładowania wierszy do indeksu magazynu kolumn dla partycjonowanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fb800-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="fb800-167">Podczas ładowania większej liczby partycji można odebrać przychodzącego wiersze, które są przechowywane w pamięci, dopóki każda partycja ma wystarczająco dużo wierszy do skompresowania.</span><span class="sxs-lookup"><span data-stu-id="fb800-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="fb800-168">Zbyt wiele partycji mających tworzy wykorzystania pamięci dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="fb800-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="fb800-169">Uprość zapytanie obciążenia</span><span class="sxs-lookup"><span data-stu-id="fb800-169">Simplify the load query</span></span>

<span data-ttu-id="fb800-170">Bazy danych może mieć przydział pamięci dla zapytania wśród wszystkich operatorów w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="fb800-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="fb800-171">Jeśli zapytanie obciążenia sortowania złożonego i sprzężeń, zostanie zmniejszona pamięci dostępnej dla kompresji.</span><span class="sxs-lookup"><span data-stu-id="fb800-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="fb800-172">Projektowanie zapytania ładowania skupić się tylko na podczas ładowania zapytania.</span><span class="sxs-lookup"><span data-stu-id="fb800-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="fb800-173">Jeśli musisz uruchomić przekształcenia danych, należy uruchomić je oddzielnie od zapytania obciążenia.</span><span class="sxs-lookup"><span data-stu-id="fb800-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="fb800-174">Na przykład przemieszczanie danych w tabeli sterty, uruchom przekształceń, a następnie załadować do indeksu magazynu kolumn tabeli przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="fb800-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="fb800-175">Można również najpierw załadować dane, a następnie używać systemu MPP do przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="fb800-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="fb800-176">Dostosuj MAXDOP</span><span class="sxs-lookup"><span data-stu-id="fb800-176">Adjust MAXDOP</span></span>

<span data-ttu-id="fb800-177">Każdy dystrybucji kompresuje rowgroups do magazynu kolumn równoległe, gdy jest dostępna więcej niż jednego rdzenia procesora CPU na dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="fb800-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="fb800-178">Równoległość wymaga dodatkowych zasobów pamięci, co może prowadzić do wykorzystania pamięci i przycinanie grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb800-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="fb800-179">Aby zmniejszyć wykorzystanie pamięci, wskazówkę zapytania MAXDOP służy do wymusić operacji ładowania do pracy w trybie serial w ramach poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="fb800-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="fb800-180">Sposoby przydzielenie większej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="fb800-180">Ways to allocate more memory</span></span>

<span data-ttu-id="fb800-181">Rozmiar wartości DWU i klasa zasobów użytkownika razem określić ilość pamięci dostępnej dla zapytania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb800-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="fb800-182">Aby zwiększyć przydział pamięci dla zapytania obciążenia, należy zwiększyć liczbę jednostek dwu lub zwiększ klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fb800-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="fb800-183">Aby zwiększyć liczbę jednostek dwu, zobacz [sposób skalowania wydajności?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="fb800-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="fb800-184">Aby zmienić klasy zasobów dla zapytania, zobacz [zmienić przykład klasy zasobów użytkownika](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="fb800-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="fb800-185">Na przykład na DWU 100 użytkownika w klasie zasobu smallrc służy 100 MB pamięci dla poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="fb800-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="fb800-186">Aby uzyskać więcej informacji, zobacz [współbieżność w usłudze SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="fb800-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="fb800-187">Załóżmy, że należy określić, czy potrzebujesz 700 MB pamięci można pobrać rozmiarów i wysokiej jakości.</span><span class="sxs-lookup"><span data-stu-id="fb800-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="fb800-188">Poniższe przykłady pokazują, jak można uruchomić kwerendę obciążenia z wystarczającą ilość pamięci.</span><span class="sxs-lookup"><span data-stu-id="fb800-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="fb800-189">Korzystając z DWU 1000 i mediumrc, Twoje przydział pamięci jest 800 MB</span><span class="sxs-lookup"><span data-stu-id="fb800-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="fb800-190">Korzystając z DWU 600 i largerc, Twoje przydział pamięci jest 800 MB.</span><span class="sxs-lookup"><span data-stu-id="fb800-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb800-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb800-191">Next steps</span></span>

<span data-ttu-id="fb800-192">Aby znaleźć więcej sposobów poprawy wydajności w usłudze SQL Data Warehouse, zobacz [wydajności — omówienie](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="fb800-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
