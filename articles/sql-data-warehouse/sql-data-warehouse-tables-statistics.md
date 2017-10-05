---
title: "Zarządzanie statystyk dotyczących tabel w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do korzystania z statystyk dotyczących tabel w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1d5ded69e394643ddfc3de0c6d30dbd30c8e848f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="994cb-103">Zarządzanie statystyk dotyczących tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="994cb-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="994cb-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="994cb-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="994cb-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="994cb-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="994cb-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="994cb-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="994cb-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="994cb-107">[Index][Index]</span></span>
> * <span data-ttu-id="994cb-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="994cb-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="994cb-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="994cb-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="994cb-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="994cb-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="994cb-111">Im bardziej zna danych usługi SQL Data Warehouse, tym szybciej można wykonywać zapytań dotyczących danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="994cb-112">Metodą Poinformuj SQL Data Warehouse o danych, jest zbieranie statystyk dotyczących danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="994cb-113">Uzyskanie statystyki do danych jest jednym z najbardziej ważnych rzeczy, które można wykonać w celu zoptymalizowania zapytań.</span><span class="sxs-lookup"><span data-stu-id="994cb-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="994cb-114">Statystyki pomocy utworzyć plan optymalny dla zapytań usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="994cb-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="994cb-115">Jest to spowodowane Optymalizator zapytań SQL Data Warehouse jest Optymalizator na podstawie.</span><span class="sxs-lookup"><span data-stu-id="994cb-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="994cb-116">To, że porównuje koszt różne plany zapytań i następnie wybiera plan o najniższej cenie, należy również plan, który zostanie wykonany najszybsze.</span><span class="sxs-lookup"><span data-stu-id="994cb-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="994cb-117">Statystykę można tworzyć w jednej kolumnie, wiele kolumn lub indeksu tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="994cb-118">Statystyki są przechowywane w histogram, który przechwytuje zakresu i wybieralność wartości.</span><span class="sxs-lookup"><span data-stu-id="994cb-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="994cb-119">Jest to szczególne znaczenie podczas Optymalizator należy ocenić sprzężenia, GROUP BY, HAVING i klauzulach WHERE w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="994cb-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="994cb-120">Na przykład, jeśli Optymalizator szacuje, że data filtrowania kwerendy zwróci 1 wiersz, mogą wybrać, bardzo inny plan niż w przypadku jego szacuje, że ich daty należy wybrano będzie zwracać 1 milion wierszy.</span><span class="sxs-lookup"><span data-stu-id="994cb-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="994cb-121">Podczas tworzenia statystyk jest bardzo ważne, równie ważne jest, że statystyki *dokładnie* odzwierciedlały bieżący stan tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="994cb-122">Aktualne statystyki zapewnia, że dobry plan jest wybierany przez optymalizator.</span><span class="sxs-lookup"><span data-stu-id="994cb-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="994cb-123">Utworzonych przez optymalizator planów są tylko dobrą statystyk na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="994cb-124">Proces tworzenia i zaktualizowanie statystyk jest obecnie ręczny proces, ale jest bardzo prosty zrobić.</span><span class="sxs-lookup"><span data-stu-id="994cb-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="994cb-125">Jest to w przeciwieństwie do programu SQL Server, które automatycznie utworzy i aktualizuje statystyki dotyczące pojedynczego kolumn i indeksów.</span><span class="sxs-lookup"><span data-stu-id="994cb-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="994cb-126">Korzystając z poniższych informacji, można znacznie automatyzują zarządzanie statystyk na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="994cb-127">Wprowadzenie do statystyki</span><span class="sxs-lookup"><span data-stu-id="994cb-127">Getting started with statistics</span></span>
 <span data-ttu-id="994cb-128">Tworzenie statystyk próbki w każdej kolumnie jest łatwe Rozpoczynanie pracy z statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="994cb-129">Ponieważ jest równie ważne zapewnić aktualność statystyk, tradycyjne podejście może być aktualizowanie statystyk codziennie lub po każdej obciążenia.</span><span class="sxs-lookup"><span data-stu-id="994cb-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="994cb-130">Zawsze istnieje możliwość wypracowania kompromisu pomiędzy wydajnością a kosztami tworzenia i aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="994cb-131">Jeśli okaże się, że utrzymywanie wszystkich statystyk trwa zbyt długo, można spróbować wybrać tylko niektóre kolumny, dla których mają być prowadzone statystyki, lub wybrać kolumny, które wymagają częstego aktualizowania.</span><span class="sxs-lookup"><span data-stu-id="994cb-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="994cb-132">Na przykład można zaktualizować kolumn dat codziennie, jak mogą być dodawane nowe wartości, a nie po każdym załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="994cb-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="994cb-133">Ponownie, uzyska najlepiej wykorzystać przez uzyskanie statystyki do kolumn uczestniczących w sprzężenia, GROUP BY, HAVING i klauzulach WHERE.</span><span class="sxs-lookup"><span data-stu-id="994cb-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="994cb-134">Jeśli masz tabelę z dużą liczbą kolumn, które są używane tylko w klauzuli SELECT, statystyki dla tych kolumn nie może pomóc i wydatków nieco więcej starań, aby zidentyfikować kolumny, których pomoże statystyk, można skrócić czas do obsługi statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="994cb-135">Statystyki wielokolumnowego</span><span class="sxs-lookup"><span data-stu-id="994cb-135">Multi-column statistics</span></span>
<span data-ttu-id="994cb-136">Oprócz tworzenia statystyk dla pojedynczego kolumn, może się okazać, zapytań zyskają statystyki wielokolumnowych.</span><span class="sxs-lookup"><span data-stu-id="994cb-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="994cb-137">Statystyka wielokolumnowego jest statystyki tworzone na liście kolumn.</span><span class="sxs-lookup"><span data-stu-id="994cb-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="994cb-138">Obejmują one statystyki jednej kolumny w pierwszej kolumnie na liście, a także niektóre informacje o powiązaniu między kolumny o nazwie gęstości.</span><span class="sxs-lookup"><span data-stu-id="994cb-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="994cb-139">Na przykład jeśli masz tabeli, w której jest przyłączany do innego dwie kolumny, może się okazać, że usługi SQL Data Warehouse lepiej można zoptymalizować planu, jeśli sam relacji między kolumnami.</span><span class="sxs-lookup"><span data-stu-id="994cb-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="994cb-140">Statystyki wielokolumnowego może poprawiać wydajność zapytań dla niektórych operacji, takich jak złożonych sprzężeń i group by.</span><span class="sxs-lookup"><span data-stu-id="994cb-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="994cb-141">Zaktualizowanie statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-141">Updating statistics</span></span>
<span data-ttu-id="994cb-142">Zaktualizowanie statystyk jest ważnym elementem procedury zarządzania z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="994cb-143">Zmiany danych w bazie danych dystrybucji statystyki muszą zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="994cb-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="994cb-144">Nieaktualne statystyki doprowadzi do nieoptymalnych kwerendy wydajności.</span><span class="sxs-lookup"><span data-stu-id="994cb-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="994cb-145">Jeden najlepszym rozwiązaniem jest aktualizację statystyk dotyczących kolumn dat każdego dnia, gdy zostaną dodane nowe daty.</span><span class="sxs-lookup"><span data-stu-id="994cb-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="994cb-146">Każdy czas nowe wiersze są załadowane do magazynu danych, nowe obciążenia daty lub daty transakcji zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="994cb-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="994cb-147">Te zmiany dystrybucji danych i utworzyć statystyki nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="994cb-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="994cb-148">Z drugiej strony statystyki dotyczące kraju kolumny w tabeli klienta może nigdy nie muszą zostać zaktualizowane, jak rozkład wartości zwykle nie ulega zmianie.</span><span class="sxs-lookup"><span data-stu-id="994cb-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="994cb-149">Zakładając, że dystrybucja jest stałe między klientami, dodawanie nowych wierszy do zmiany tabeli nie jest będzie zmienić dystrybucji danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="994cb-150">Jednak jeśli magazyn danych zawiera tylko jeden kraj, należy przenieść dane z nowego kraju dane z różnych krajach przechowywane, następnie ostatecznie należy aktualizować statystyki w kolumnie kraju.</span><span class="sxs-lookup"><span data-stu-id="994cb-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="994cb-151">Jednym z pierwszym pytań podczas rozwiązywania problemów z kwerendy jest "Są aktualne statystyki?"</span><span class="sxs-lookup"><span data-stu-id="994cb-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="994cb-152">To pytanie nie jest taki, który należy odpowiedzieć przy wiek danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="994cb-153">Obiekt aktualne statystyki może być bardzo stare, jeśli nie ma w niej żadnych istotnych zmian w danych źródłowych.</span><span class="sxs-lookup"><span data-stu-id="994cb-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="994cb-154">Jeśli liczba wierszy zmienił znacząco lub istotne zmiany w dystrybucji wartości dla danej kolumny *następnie* nadszedł czas, aby zaktualizować statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="994cb-155">Odwołania **programu SQL Server** (nie SQL Data Warehouse) automatycznie aktualizuje statystyk w takich sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="994cb-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="994cb-156">Jeśli masz żadnych wierszy w tabeli, podczas dodawania wierszy, otrzymasz automatycznych aktualizacji statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="994cb-157">Po dodaniu więcej niż 500 wierszy do tabeli, począwszy od mniej niż 500 wierszy (np. na początku masz 499 i następnie dodać 500 wierszy w sumie 999 wierszy), zostanie wyświetlony aktualizacji automatycznych</span><span class="sxs-lookup"><span data-stu-id="994cb-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="994cb-158">Po wyświetleniu ponad 500 wierszy, należy dodać 500 dodatkowe wiersze + 20% rozmiar tabeli przed zobaczysz automatycznych aktualizacji na statystyki</span><span class="sxs-lookup"><span data-stu-id="994cb-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="994cb-159">Ponieważ nie ma żadnych DMV, aby określić, czy dane w tabeli zmienił się od czasu ostatniego statystyk czasu zostały zaktualizowane, wiedząc, wieku statystyk może umożliwić z część obrazu.</span><span class="sxs-lookup"><span data-stu-id="994cb-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="994cb-160">Następujące zapytanie służy do określenia czasu ostatniego statystyk w przypadku, gdy zaktualizowane w każdej tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="994cb-161">Należy pamiętać o tym, w przypadku istotnych zmian dystrybucja wartości dla danej kolumny, należy zaktualizować statystyk niezależnie od tego czasu, gdy są one zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="994cb-161">Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="994cb-162">Kolumn dat w magazynie danych, na przykład zwykle wymagają częstego aktualizacji statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="994cb-163">Każdy czas nowe wiersze są załadowane do magazynu danych, nowe obciążenia daty lub daty transakcji zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="994cb-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="994cb-164">Te zmiany dystrybucji danych i utworzyć statystyki nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="994cb-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="994cb-165">Z drugiej strony statystyk dotyczących płci kolumny w tabeli klienta nigdy nie może być konieczne do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="994cb-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="994cb-166">Zakładając, że dystrybucja jest stałe między klientami, dodawanie nowych wierszy do zmiany tabeli nie jest będzie zmienić dystrybucji danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="994cb-167">Jednak jeśli magazyn danych zawiera tylko jeden płci i nowe wyniki wymaganie w wielu płci ostatecznie należy aktualizować statystyki w kolumnie płci.</span><span class="sxs-lookup"><span data-stu-id="994cb-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="994cb-168">Aby uzyskać dokładniejsze objaśnienie, zobacz [statystyki] [ Statistics] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="994cb-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="994cb-169">Implementowanie zarządzania statystyki</span><span class="sxs-lookup"><span data-stu-id="994cb-169">Implementing statistics management</span></span>
<span data-ttu-id="994cb-170">Często jest dobrym pomysłem jest rozszerzenie procesu, aby upewnić się, że statystyki są aktualizowane na końcu obciążenia ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="994cb-171">Ładowanie danych jest tabel najczęściej zmiany ich rozmiaru i/lub ich rozkład wartości.</span><span class="sxs-lookup"><span data-stu-id="994cb-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="994cb-172">W związku z tym jest to logiczne miejsca do wykonania niektórych procesów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="994cb-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="994cb-173">Niektóre wytyczne są podane poniżej w celu zaktualizowania statystyk podczas procesu obciążenia:</span><span class="sxs-lookup"><span data-stu-id="994cb-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="994cb-174">Sprawdź, czy każdy załadowanej tabeli ma co najmniej jeden obiekt statystyki aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="994cb-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="994cb-175">Spowoduje to zaktualizowanie informacje o rozmiarze (liczba wierszy i liczba stron) tabel w ramach aktualizacji statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="994cb-176">Skupić się na kolumn uczestniczących w klauzuli sprzężenia, GROUP BY, ORDER BY i DISTINCT</span><span class="sxs-lookup"><span data-stu-id="994cb-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="994cb-177">Może być konieczna aktualizacja "rosnącej klucza" kolumn, takie jak transakcji więcej często wartości te nie zostaną uwzględnione w postaci histogramu statystyki daty.</span><span class="sxs-lookup"><span data-stu-id="994cb-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="994cb-178">Należy rozważyć aktualizowanie kolumn dystrybucji statycznych często.</span><span class="sxs-lookup"><span data-stu-id="994cb-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="994cb-179">Należy pamiętać, że każdy obiekt Statystyka jest aktualizowany w serii.</span><span class="sxs-lookup"><span data-stu-id="994cb-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="994cb-180">Po prostu implementacja `UPDATE STATISTICS <TABLE_NAME>` może nie być idealne — szczególnie w przypadku szerokie tabele z dużą liczbą obiektów statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="994cb-181">Więcej informacji na temat [rosnącej klucza] można znaleźć w dokumencie modelu szacowania kardynalności programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="994cb-181">For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="994cb-182">Aby uzyskać dokładniejsze objaśnienie, zobacz [szacowania kardynalności] [ Cardinality Estimation] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="994cb-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="994cb-183">Przykłady: Tworzenie statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-183">Examples: Create statistics</span></span>
<span data-ttu-id="994cb-184">Poniższe przykłady pokazują, jak tworzenie statystyk na użytek różnych opcji.</span><span class="sxs-lookup"><span data-stu-id="994cb-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="994cb-185">Opcje używane dla każdej kolumny są zależne od właściwości danych i jak kolumna będzie używane w zapytaniach.</span><span class="sxs-lookup"><span data-stu-id="994cb-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="994cb-186">A.</span><span class="sxs-lookup"><span data-stu-id="994cb-186">A.</span></span> <span data-ttu-id="994cb-187">Tworzenie statystyk pojedynczej kolumny z opcji domyślnych</span><span class="sxs-lookup"><span data-stu-id="994cb-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="994cb-188">Aby utworzyć statystyki dla kolumny, wystarczy podać nazwę obiektu statystyk i nazwę kolumny.</span><span class="sxs-lookup"><span data-stu-id="994cb-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="994cb-189">Ta składnia wykorzystuje wszystkie domyślne opcje.</span><span class="sxs-lookup"><span data-stu-id="994cb-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="994cb-190">Domyślnie 20 procent tabeli przykłady SQL Data Warehouse, podczas tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="994cb-191">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="994cb-192">B.</span><span class="sxs-lookup"><span data-stu-id="994cb-192">B.</span></span> <span data-ttu-id="994cb-193">Tworzenie statystyk pojedynczej kolumny, sprawdzając każdego wiersza</span><span class="sxs-lookup"><span data-stu-id="994cb-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="994cb-194">Domyślna częstotliwość próbkowania równy 20% jest wystarczające w większości sytuacji.</span><span class="sxs-lookup"><span data-stu-id="994cb-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="994cb-195">Można jednak dostosować częstotliwość próbkowania.</span><span class="sxs-lookup"><span data-stu-id="994cb-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="994cb-196">Do próbkowania pełne tabeli, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="994cb-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="994cb-197">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="994cb-198">C.</span><span class="sxs-lookup"><span data-stu-id="994cb-198">C.</span></span> <span data-ttu-id="994cb-199">Tworzenie statystyk pojedynczej kolumny, określając rozmiar próbki</span><span class="sxs-lookup"><span data-stu-id="994cb-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="994cb-200">Alternatywnie można określić rozmiar próbki w procentach:</span><span class="sxs-lookup"><span data-stu-id="994cb-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="994cb-201">D.</span><span class="sxs-lookup"><span data-stu-id="994cb-201">D.</span></span> <span data-ttu-id="994cb-202">Tworzenie statystyk pojedynczej kolumny dla niektórych wierszy</span><span class="sxs-lookup"><span data-stu-id="994cb-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="994cb-203">Inną opcją, można utworzyć statystyki w części wiersze w tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="994cb-204">Jest to filtrowane statystyki.</span><span class="sxs-lookup"><span data-stu-id="994cb-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="994cb-205">Można na przykład użyć statystykę filtrowaną, planując zapytania określonej partycji tabeli partycjonowanej duże.</span><span class="sxs-lookup"><span data-stu-id="994cb-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="994cb-206">Tworzenie statystyk na tylko wartości partycji, prawidłowość statystyki będzie poprawić, a w związku z tym poprawiać wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="994cb-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="994cb-207">Ten przykład tworzy statystyki zakresu wartości.</span><span class="sxs-lookup"><span data-stu-id="994cb-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="994cb-208">Wartości można łatwo ustawione w taki sposób, aby odpowiadały zakres wartości w partycji.</span><span class="sxs-lookup"><span data-stu-id="994cb-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="994cb-209">Optymalizator zapytań należy rozważyć użycie statystykę filtrowaną, gdy wybiera plan zapytania rozproszonego zapytanie musi mieścić się w definicji obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-209">For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object.</span></span> <span data-ttu-id="994cb-210">W poprzednim przykładzie, kwerendy gdzie należy określić wartości col1 między 2000101 i 20001231 klauzuli.</span><span class="sxs-lookup"><span data-stu-id="994cb-210">Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="994cb-211">E.</span><span class="sxs-lookup"><span data-stu-id="994cb-211">E.</span></span> <span data-ttu-id="994cb-212">Tworzenie statystyk pojedynczej kolumny przy użyciu opcji</span><span class="sxs-lookup"><span data-stu-id="994cb-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="994cb-213">Opcje można oczywiście łączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="994cb-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="994cb-214">Poniższy przykład tworzy obiekt statystykę filtrowaną z niestandardowych próbkowania:</span><span class="sxs-lookup"><span data-stu-id="994cb-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="994cb-215">Aby uzyskać pełną dokumentację, zobacz [instrukcji CREATE STATISTICS] [ CREATE STATISTICS] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="994cb-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="994cb-216">F.</span><span class="sxs-lookup"><span data-stu-id="994cb-216">F.</span></span> <span data-ttu-id="994cb-217">Tworzenie statystyk wielokolumnowego</span><span class="sxs-lookup"><span data-stu-id="994cb-217">Create multi-column statistics</span></span>
<span data-ttu-id="994cb-218">Tworzenie statystyk wielokolumnowego, po prostu użyć poprzednich przykładach, lecz określ większą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="994cb-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="994cb-219">Histogram, który jest używany do oszacować liczbę wierszy w wyniku zapytania, jest dostępna tylko dla pierwszej kolumny na liście definicji obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-219">The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.</span></span>
> 
> 

<span data-ttu-id="994cb-220">W tym przykładzie histogram znajduje się na *produktu\_kategorii*.</span><span class="sxs-lookup"><span data-stu-id="994cb-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="994cb-221">Statystyki między kolumny są obliczane na *produktu\_kategorii* i *produktu\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="994cb-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="994cb-222">Ponieważ korelacji między *produktu\_kategorii* i *produktu\_sub\_kategorii*, stat wielokolumnowego mogą być przydatne, jeśli te kolumny są dostępne. w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="994cb-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="994cb-223">G.</span><span class="sxs-lookup"><span data-stu-id="994cb-223">G.</span></span> <span data-ttu-id="994cb-224">Tworzenie statystyk dla wszystkich kolumn w tabeli</span><span class="sxs-lookup"><span data-stu-id="994cb-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="994cb-225">Jednym ze sposobów tworzenia statystyk ma problemy polecenia CREATE STATISTICS po utworzeniu tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="994cb-226">H.</span><span class="sxs-lookup"><span data-stu-id="994cb-226">H.</span></span> <span data-ttu-id="994cb-227">Użyj procedury składowanej utworzyć statystyki dla wszystkich kolumn w bazie danych</span><span class="sxs-lookup"><span data-stu-id="994cb-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="994cb-228">Magazyn danych SQL nie ma systemowej procedury składowanej odpowiednikiem [] [sp_create_stats] w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="994cb-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="994cb-229">Tę procedurę składowaną tworzy obiekt statystyki jednej kolumny w każdej kolumnie bazy danych, który nie ma jeszcze statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="994cb-230">Pomoże to wprowadzenie do projektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-230">This will help you get started with your database design.</span></span> <span data-ttu-id="994cb-231">Możesz dostosować go do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="994cb-231">Feel free to adapt it to your needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="994cb-232">Aby utworzyć statystyki dla wszystkich kolumn w tabeli z tej procedury, po prostu wywołania tej procedury.</span><span class="sxs-lookup"><span data-stu-id="994cb-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="994cb-233">Przykłady: Aktualizuj statystyki</span><span class="sxs-lookup"><span data-stu-id="994cb-233">Examples: update statistics</span></span>
<span data-ttu-id="994cb-234">Aby zaktualizować statystyk, można:</span><span class="sxs-lookup"><span data-stu-id="994cb-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="994cb-235">Zaktualizuj jeden obiekt statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-235">Update one statistics object.</span></span> <span data-ttu-id="994cb-236">Określ nazwę obiektu statystyk, które chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="994cb-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="994cb-237">Zaktualizuj wszystkie obiekty statystyki dla tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="994cb-238">Określ nazwę tabeli zamiast jeden obiekt poszczególnych statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="994cb-239">A.</span><span class="sxs-lookup"><span data-stu-id="994cb-239">A.</span></span> <span data-ttu-id="994cb-240">Zaktualizuj jeden obiekt poszczególnych statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-240">Update one specific statistics object</span></span>
<span data-ttu-id="994cb-241">Aby zaktualizować obiekt poszczególnych statystyk, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="994cb-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="994cb-242">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="994cb-243">Aktualizacja poszczególnych statystyk obiektów, można zminimalizować czas i zasoby wymagane do zarządzania statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="994cb-244">Wymaga to rozwagą, jednak, aby wybrać najlepsze obiekty statystyki aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="994cb-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="994cb-245">B.</span><span class="sxs-lookup"><span data-stu-id="994cb-245">B.</span></span> <span data-ttu-id="994cb-246">Aktualizuj wszystkie statystyki dla tabeli</span><span class="sxs-lookup"><span data-stu-id="994cb-246">Update all statistics on a table</span></span>
<span data-ttu-id="994cb-247">Oznacza to prosta metoda aktualizowania wszystkich obiektów statystyk tabeli.</span><span class="sxs-lookup"><span data-stu-id="994cb-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="994cb-248">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="994cb-249">Ta instrukcja jest łatwy w użyciu.</span><span class="sxs-lookup"><span data-stu-id="994cb-249">This statement is easy to use.</span></span> <span data-ttu-id="994cb-250">Pamiętaj tylko to aktualizuje wszystkie statystyki w tabeli i dlatego może wykonywać więcej pracy, niż jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="994cb-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="994cb-251">Jeśli wydajność nie stanowi to problemu, ostatecznie to najprostszy i najbardziej kompleksowe sposób gwarantuje, że dane statystyczne są aktualne.</span><span class="sxs-lookup"><span data-stu-id="994cb-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="994cb-252">Podczas aktualizowania wszystkich statystyk dotyczących tabeli, SQL Data Warehouse nie skanowanie w celu przykładowej tabeli dla poszczególnych statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-252">When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics.</span></span> <span data-ttu-id="994cb-253">Jeśli tabela jest duży, ma wiele kolumn i ilość danych statystycznych, może być bardziej wydajne, można zaktualizować poszczególnych statystyki, w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="994cb-253">If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="994cb-254">Dla implementacji `UPDATE STATISTICS` procedury można znaleźć pod adresem [tabel tymczasowych] [ Temporary] artykułu.</span><span class="sxs-lookup"><span data-stu-id="994cb-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="994cb-255">Metody wdrażania różni się nieznacznie się `CREATE STATISTICS` powyższą procedurę, ale wynik końcowy jest taki sam.</span><span class="sxs-lookup"><span data-stu-id="994cb-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="994cb-256">Dla pełnej składni, zobacz [Update Statistics] [ Update Statistics] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="994cb-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="994cb-257">Statystyki metadanych</span><span class="sxs-lookup"><span data-stu-id="994cb-257">Statistics metadata</span></span>
<span data-ttu-id="994cb-258">Istnieje kilka widok systemu i funkcje, które umożliwia znalezienie informacji na temat statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="994cb-259">Na przykład widać, jeśli obiekt statystyki może być nieaktualne za pomocą funkcji daty Statystyka wyświetlać podczas statystyki ostatnio zostały utworzone lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="994cb-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="994cb-260">Widoków wykazu statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-260">Catalog views for statistics</span></span>
<span data-ttu-id="994cb-261">Widoki te systemu zawierają informacje o statystyki:</span><span class="sxs-lookup"><span data-stu-id="994cb-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="994cb-262">Przeglądanie katalogu</span><span class="sxs-lookup"><span data-stu-id="994cb-262">Catalog View</span></span> | <span data-ttu-id="994cb-263">Opis</span><span class="sxs-lookup"><span data-stu-id="994cb-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="994cb-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="994cb-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="994cb-265">Jeden wiersz dla każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="994cb-265">One row for each column.</span></span> |
| <span data-ttu-id="994cb-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="994cb-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="994cb-267">Jeden wiersz dla każdego obiektu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="994cb-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="994cb-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="994cb-269">Jeden wiersz dla każdego schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="994cb-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="994cb-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="994cb-271">Jeden wiersz dla każdego obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="994cb-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="994cb-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="994cb-273">Jeden wiersz dla każdej kolumny w obiekcie statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="994cb-274">Łącza do sys.columns.</span><span class="sxs-lookup"><span data-stu-id="994cb-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="994cb-275">[Widok sys.Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="994cb-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="994cb-276">Jeden wiersz dla każdej tabeli (w tym tabel zewnętrznych).</span><span class="sxs-lookup"><span data-stu-id="994cb-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="994cb-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="994cb-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="994cb-278">Jeden wiersz dla każdego typu danych.</span><span class="sxs-lookup"><span data-stu-id="994cb-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="994cb-279">Funkcje systemu statystyk</span><span class="sxs-lookup"><span data-stu-id="994cb-279">System functions for statistics</span></span>
<span data-ttu-id="994cb-280">Funkcje systemu są przydatne w przypadku pracy z statystyki:</span><span class="sxs-lookup"><span data-stu-id="994cb-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="994cb-281">System — funkcja</span><span class="sxs-lookup"><span data-stu-id="994cb-281">System Function</span></span> | <span data-ttu-id="994cb-282">Opis</span><span class="sxs-lookup"><span data-stu-id="994cb-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="994cb-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="994cb-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="994cb-284">Data ostatniej aktualizacji obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="994cb-285">[POLECENIE DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="994cb-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="994cb-286">Zawiera podsumowanie poziomu i szczegółowe informacje o rozkład wartości rozumieniu obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="994cb-287">Łączenie statystyk kolumny i funkcji w jednym widoku</span><span class="sxs-lookup"><span data-stu-id="994cb-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="994cb-288">Ten widok zapewnia kolumn, które dotyczą statystyk i wyniki z funkcji [] [STATS_DATE()] razem.</span><span class="sxs-lookup"><span data-stu-id="994cb-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="994cb-289">Przykłady DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="994cb-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="994cb-290">Polecenie DBCC SHOW_STATISTICS() zawiera dane przechowywane w obiekcie statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="994cb-291">Te dane składa się z trzech części.</span><span class="sxs-lookup"><span data-stu-id="994cb-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="994cb-292">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="994cb-292">Header</span></span>
2. <span data-ttu-id="994cb-293">Wektor gęstość</span><span class="sxs-lookup"><span data-stu-id="994cb-293">Density Vector</span></span>
3. <span data-ttu-id="994cb-294">Histogram</span><span class="sxs-lookup"><span data-stu-id="994cb-294">Histogram</span></span>

<span data-ttu-id="994cb-295">Metadane nagłówka o statystyki.</span><span class="sxs-lookup"><span data-stu-id="994cb-295">The header metadata about the statistics.</span></span> <span data-ttu-id="994cb-296">Histogram przedstawia rozkład wartości z pierwszej kolumny klucza obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="994cb-297">Wektor gęstość mierzy korelacji między kolumny.</span><span class="sxs-lookup"><span data-stu-id="994cb-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="994cb-298">SQLDW oblicza szacowania kardynalności o dane w obiekcie statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="994cb-299">Pokaż nagłówka, gęstości i histogramu</span><span class="sxs-lookup"><span data-stu-id="994cb-299">Show header, density, and histogram</span></span>
<span data-ttu-id="994cb-300">Ten prosty przykład przedstawia wszystkich trzech części obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="994cb-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="994cb-301">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="994cb-302">Pokaż co najmniej jeden części DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="994cb-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="994cb-303">Jeśli interesuje Cię tylko wyświetlanie określonych części, użyj `WITH` klauzuli i określ części, które chcesz wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="994cb-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="994cb-304">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="994cb-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="994cb-305">Polecenie DBCC SHOW_STATISTICS() różnic</span><span class="sxs-lookup"><span data-stu-id="994cb-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="994cb-306">DBCC SHOW_STATISTICS() bardziej ściśle jest zaimplementowana w usłudze SQL Data Warehouse w porównaniu z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="994cb-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="994cb-307">Nieudokumentowanej funkcje nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="994cb-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="994cb-308">Nie można użyć Stats_stream</span><span class="sxs-lookup"><span data-stu-id="994cb-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="994cb-309">Nie można dołączyć wyniki konkretne podzestawy danych statystyki np. (STAT_HEADER sprzężenia DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="994cb-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="994cb-310">Nie można ustawić NO_INFOMSGS dla pomijania wiadomości</span><span class="sxs-lookup"><span data-stu-id="994cb-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="994cb-311">Nie można użyć nazwy statystyki nawiasy kwadratowe</span><span class="sxs-lookup"><span data-stu-id="994cb-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="994cb-312">Nie można użyć nazwy kolumn, aby zidentyfikować obiekty statystyki</span><span class="sxs-lookup"><span data-stu-id="994cb-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="994cb-313">Błąd niestandardowy 2767 nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="994cb-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="994cb-314">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="994cb-314">Next steps</span></span>
<span data-ttu-id="994cb-315">Aby uzyskać więcej informacji, zobacz [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="994cb-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="994cb-316">Aby dowiedzieć się więcej, zobacz artykuły w [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Indeksowania tabeli][Index], [partycjonowania tabeli] [ Partition] i [Tabel tymczasowych][Temporary].</span><span class="sxs-lookup"><span data-stu-id="994cb-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="994cb-317">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="994cb-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
