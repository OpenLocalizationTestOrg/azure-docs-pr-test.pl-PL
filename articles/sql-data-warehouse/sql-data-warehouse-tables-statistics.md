---
title: "statystyki aaaManaging w tabelach w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="5dcae-103">Zarządzanie statystyk dotyczących tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5dcae-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5dcae-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="5dcae-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="5dcae-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="5dcae-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="5dcae-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="5dcae-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="5dcae-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="5dcae-107">[Index][Index]</span></span>
> * <span data-ttu-id="5dcae-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="5dcae-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="5dcae-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="5dcae-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="5dcae-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="5dcae-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="5dcae-111">Hello więcej SQL Data Warehouse zna danych, hello szybciej go można wykonywać zapytania względem danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="5dcae-112">sposób Hello Poinformuj SQL Data Warehouse o danych, jest zbieranie statystyk dotyczących danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="5dcae-113">Uzyskanie statystyki do danych jest jednym z hello najważniejsze czynności można wykonać toooptimize zapytań.</span><span class="sxs-lookup"><span data-stu-id="5dcae-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="5dcae-114">Statystyki pomocy SQL Data Warehouse, Utwórz plan optymalny powitania dla zapytań.</span><span class="sxs-lookup"><span data-stu-id="5dcae-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="5dcae-115">Jest to spowodowane Optymalizator na podstawie zapytania SQL Data Warehouse hello Optymalizator jest koszt.</span><span class="sxs-lookup"><span data-stu-id="5dcae-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="5dcae-116">To, że porównuje koszt hello różnych planów zapytania i następnie wybiera planu hello o najniższej cenie hello, która powinna być również hello plan, który zostanie wykonany hello najszybszym.</span><span class="sxs-lookup"><span data-stu-id="5dcae-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="5dcae-117">Statystykę można tworzyć w jednej kolumnie, wiele kolumn lub indeksu tabeli.</span><span class="sxs-lookup"><span data-stu-id="5dcae-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="5dcae-118">Statystyki są przechowywane w histogram, który przechwytuje hello zakresu i wybieralność wartości.</span><span class="sxs-lookup"><span data-stu-id="5dcae-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="5dcae-119">To jest znaczący Optymalizator hello musi tooevaluate sprzężenia, GROUP BY, HAVING i klauzulach WHERE w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="5dcae-120">Na przykład, jeśli Optymalizator hello szacuje, że data hello filtrowania kwerendy zwróci 1 wiersz, mogą wybrać, bardzo inny plan niż wtedy, gdy jego szacuje, że ich daty należy wybrano będzie zwracać 1 milion wierszy.</span><span class="sxs-lookup"><span data-stu-id="5dcae-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="5dcae-121">Podczas tworzenia statystyk jest bardzo ważne, równie ważne jest, że statystyki *dokładnie* odzwierciedlały bieżący stan hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="5dcae-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="5dcae-122">Aktualne statystyki zapewnia, że dobry plan jest wybierany przez optymalizator hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="5dcae-123">utworzone przez optymalizator hello planów Hello są tylko dobrą hello statystyk na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="5dcae-124">Witaj proces tworzenia i zaktualizowanie statystyk jest obecnie ręczny proces, ale jest bardzo prosty toodo.</span><span class="sxs-lookup"><span data-stu-id="5dcae-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="5dcae-125">Jest to w przeciwieństwie do programu SQL Server, które automatycznie utworzy i aktualizuje statystyki dotyczące pojedynczego kolumn i indeksów.</span><span class="sxs-lookup"><span data-stu-id="5dcae-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="5dcae-126">Korzystając z poniższych informacji hello, można znacznie zautomatyzowanie zarządzania hello hello statystyk na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="5dcae-127">Wprowadzenie do statystyki</span><span class="sxs-lookup"><span data-stu-id="5dcae-127">Getting started with statistics</span></span>
 <span data-ttu-id="5dcae-128">Tworzenie statystyk próbki w każdej kolumnie jest tooget łatwy sposób pracy z statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="5dcae-129">Ponieważ jest równie ważne tookeep statystyki aktualne, tradycyjne podejście może być tooupdate statystyk codziennie lub po każdej obciążenia.</span><span class="sxs-lookup"><span data-stu-id="5dcae-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="5dcae-130">Zawsze są kompromis między wydajnością i hello koszt toocreate i aktualizację statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="5dcae-131">Jeśli okaże się, że trwa zbyt długo toomaintain wszystkich statystyk, możesz się, że toobe tootry więcej selektywnie, które kolumny mają statystyk lub kolumny, które wymagają częstego aktualizowania.</span><span class="sxs-lookup"><span data-stu-id="5dcae-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="5dcae-132">Na przykład można kolumn dat tooupdate codziennie, jak mogą być dodawane nowe wartości, a nie po każdym załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="5dcae-133">Ponownie zostanie uzyskasz hello największe korzyści przez uzyskanie statystyki do kolumn uczestniczących w sprzężenia, GROUP BY, HAVING i klauzulach WHERE.</span><span class="sxs-lookup"><span data-stu-id="5dcae-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="5dcae-134">Jeśli tabela jest z wielu kolumn, które są używane tylko w hello SELECT — klauzula, statystyki dla tych kolumn nie może pomóc, i wydatków nieco więcej tooidentify nakładu tylko kolumny hello gdzie pomoże statystyki może zmniejszyć toomaintain czasu hello statystyk .</span><span class="sxs-lookup"><span data-stu-id="5dcae-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="5dcae-135">Statystyki wielokolumnowego</span><span class="sxs-lookup"><span data-stu-id="5dcae-135">Multi-column statistics</span></span>
<span data-ttu-id="5dcae-136">Ponadto toocreating statystyk dotyczących jednej kolumny, może się okazać zapytań zyskają statystyki wielokolumnowych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="5dcae-137">Statystyka wielokolumnowego jest statystyki tworzone na liście kolumn.</span><span class="sxs-lookup"><span data-stu-id="5dcae-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="5dcae-138">Obejmują one statystyki jednej kolumny w pierwszej kolumnie hello hello na liście, a także niektóre informacje o powiązaniu między kolumny o nazwie gęstości.</span><span class="sxs-lookup"><span data-stu-id="5dcae-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="5dcae-139">Na przykład jeśli masz tabelę, której jest przyłączany tooanother dwie kolumny, może się okazać, że usługi SQL Data Warehouse lepiej zoptymalizować planu hello jeśli sam hello relacji między kolumnami.</span><span class="sxs-lookup"><span data-stu-id="5dcae-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="5dcae-140">Statystyki wielokolumnowego może poprawiać wydajność zapytań dla niektórych operacji, takich jak złożonych sprzężeń i group by.</span><span class="sxs-lookup"><span data-stu-id="5dcae-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="5dcae-141">Zaktualizowanie statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-141">Updating statistics</span></span>
<span data-ttu-id="5dcae-142">Zaktualizowanie statystyk jest ważnym elementem procedury zarządzania z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="5dcae-143">Po zmianie hello rozkład danych w bazie danych hello statystyki muszą toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="5dcae-144">Nieaktualne statystyki doprowadzi toosub optymalnego działania zapytań.</span><span class="sxs-lookup"><span data-stu-id="5dcae-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="5dcae-145">Jeden najlepszym rozwiązaniem jest tooupdate statystyk dotyczących kolumn dat każdego dnia po dodaniu nowego daty.</span><span class="sxs-lookup"><span data-stu-id="5dcae-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="5dcae-146">Każdy czas nowe wiersze są ładowane do magazynu danych hello, nowe obciążenia daty lub daty transakcji zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="5dcae-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="5dcae-147">Te zmiany hello danych dystrybucji i utworzyć statystyki hello nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="5dcae-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="5dcae-148">Z drugiej strony statystyki dotyczące kraju kolumny w tabeli klienta nigdy nie może być konieczne toobe aktualizacji, jak dystrybucji hello wartości zwykle nie ulega zmianie.</span><span class="sxs-lookup"><span data-stu-id="5dcae-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="5dcae-149">Zakładając, że dystrybucji hello jest stałe między klientami, dodawanie nowych wierszy toohello tabeli zmian nie będzie toochange hello danych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="5dcae-150">Jednak jeśli magazyn danych zawiera tylko jeden kraj, należy przenieść dane z nowego kraju dane z różnych krajach przechowywane, zdecydowanie należy tooupdate statystyk w kolumnie kraju hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="5dcae-151">Jeden hello pierwszy tooask pytania podczas rozwiązywania problemów z kwerendy jest "są statystyki hello aktualne?"</span><span class="sxs-lookup"><span data-stu-id="5dcae-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="5dcae-152">To pytanie nie jest taki, który należy odpowiedzieć przy hello wiek danych hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="5dcae-153">Obiekt się dane statystyczne toodate może być bardzo stare, jeśli nie było żadnych toohello istotnej zmiany podstawowego danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="5dcae-154">Gdy hello liczbę wierszy zmieniły się znacznie lub istotne zmiany w dystrybucji hello wartości dla danej kolumny *następnie* jest statystyki tooupdate czasu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="5dcae-155">Odwołania **programu SQL Server** (nie SQL Data Warehouse) automatycznie aktualizuje statystyk w takich sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="5dcae-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="5dcae-156">Jeśli masz żadnych wierszy w tabeli hello podczas dodawania wierszy, otrzymasz automatycznych aktualizacji statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="5dcae-157">Po dodaniu więcej niż 500 wierszy tabeli tooa, począwszy od mniej niż 500 wierszy (np. na początku masz 499 i następnie dodać 500 wierszy tooa całkowitej liczby wierszy 999), zostanie wyświetlony aktualizacji automatycznych</span><span class="sxs-lookup"><span data-stu-id="5dcae-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="5dcae-158">Po wyświetleniu ponad 500 wierszy trzeba będzie tooadd 500 dodatkowe wiersze + 20% hello rozmiar tabeli hello zanim zobaczysz automatycznych aktualizacji na powitania statystyki</span><span class="sxs-lookup"><span data-stu-id="5dcae-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="5dcae-159">Ponieważ nie istnieje żadne toodetermine DMV, jeśli dane w tabeli hello uległy zmianie od czasu ostatniego statystyk czasu hello zostały zaktualizowane, wiedząc, wieku hello statystyk może umożliwić z częścią obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="5dcae-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="5dcae-160">Można użyć następującego zapytania toodetermine hello ostatniego statystyk hello gdzie zaktualizowane w każdej tabeli.</span><span class="sxs-lookup"><span data-stu-id="5dcae-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="5dcae-161">Należy pamiętać o tym, w przypadku istotnych zmiany w dystrybucji hello wartości dla danej kolumny, należy zaktualizować statystyk niezależnie od hello czasu, gdy są one zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5dcae-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="5dcae-162">Kolumn dat w magazynie danych, na przykład zwykle wymagają częstego aktualizacji statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="5dcae-163">Każdy czas nowe wiersze są ładowane do magazynu danych hello, nowe obciążenia daty lub daty transakcji zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="5dcae-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="5dcae-164">Te zmiany hello danych dystrybucji i utworzyć statystyki hello nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="5dcae-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="5dcae-165">Z drugiej strony statystyk dotyczących płci kolumny w tabeli klienta nigdy nie może być konieczne toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="5dcae-166">Zakładając, że dystrybucji hello jest stałe między klientami, dodawanie nowych wierszy toohello tabeli zmian nie będzie toochange hello danych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="5dcae-167">Jednak jeśli magazyn danych zawiera tylko jeden płci i nowe wyniki wymaganie w wielu płci ostatecznie należy tooupdate statystyk na powitania płci kolumny.</span><span class="sxs-lookup"><span data-stu-id="5dcae-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="5dcae-168">Aby uzyskać dokładniejsze objaśnienie, zobacz [statystyki] [ Statistics] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dcae-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="5dcae-169">Implementowanie zarządzania statystyki</span><span class="sxs-lookup"><span data-stu-id="5dcae-169">Implementing statistics management</span></span>
<span data-ttu-id="5dcae-170">Często jest tooextend dobrze koniec obciążenia hello hello ładowania tooensure procesu, który statystyki są aktualizowane w danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="5dcae-171">Ładowanie danych Hello jest tabel najczęściej zmiany ich rozmiaru i/lub ich rozkład wartości.</span><span class="sxs-lookup"><span data-stu-id="5dcae-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="5dcae-172">W związku z tym jest to tooimplement logicznego miejsca niektóre procesy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="5dcae-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="5dcae-173">Niektóre wytyczne są podane poniżej w celu zaktualizowania statystyk podczas procesu obciążenia hello:</span><span class="sxs-lookup"><span data-stu-id="5dcae-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="5dcae-174">Sprawdź, czy każdy załadowanej tabeli ma co najmniej jeden obiekt statystyki aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="5dcae-175">Witaj tej aktualizacji tabel informacje o rozmiarze (liczba wierszy i liczba stron) jako część hello Statystyka aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="5dcae-176">Skupić się na kolumn uczestniczących w klauzuli sprzężenia, GROUP BY, ORDER BY i DISTINCT</span><span class="sxs-lookup"><span data-stu-id="5dcae-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="5dcae-177">Może być konieczna aktualizacja "rosnącej klucza" kolumn, takie jak transakcji więcej często wartości te nie zostaną uwzględnione w histogram statystyki hello daty.</span><span class="sxs-lookup"><span data-stu-id="5dcae-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="5dcae-178">Należy rozważyć aktualizowanie kolumn dystrybucji statycznych często.</span><span class="sxs-lookup"><span data-stu-id="5dcae-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="5dcae-179">Należy pamiętać, że każdy obiekt Statystyka jest aktualizowany w serii.</span><span class="sxs-lookup"><span data-stu-id="5dcae-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="5dcae-180">Po prostu implementacja `UPDATE STATISTICS <TABLE_NAME>` może nie być idealne — szczególnie w przypadku szerokie tabele z dużą liczbą obiektów statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="5dcae-181">Więcej informacji na temat [rosnącej klucza] można znaleźć w dokumencie modelu szacowania kardynalności toohello programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="5dcae-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="5dcae-182">Aby uzyskać dokładniejsze objaśnienie, zobacz [szacowania kardynalności] [ Cardinality Estimation] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dcae-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="5dcae-183">Przykłady: Tworzenie statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-183">Examples: Create statistics</span></span>
<span data-ttu-id="5dcae-184">Następujące przykłady przedstawiają sposób toouse różne opcje tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="5dcae-185">Opcje Hello Użyj dla każdej kolumny są zależne od właściwości hello danych i jak hello kolumny będą używane w zapytaniach.</span><span class="sxs-lookup"><span data-stu-id="5dcae-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="5dcae-186">A.</span><span class="sxs-lookup"><span data-stu-id="5dcae-186">A.</span></span> <span data-ttu-id="5dcae-187">Tworzenie statystyk pojedynczej kolumny z opcji domyślnych</span><span class="sxs-lookup"><span data-stu-id="5dcae-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="5dcae-188">statystyki toocreate od kolumny, wystarczy podać nazwę dla obiekt statystyki hello i nazwę hello hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="5dcae-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="5dcae-189">Ta składnia wykorzystuje wszystkie hello domyślne opcje.</span><span class="sxs-lookup"><span data-stu-id="5dcae-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="5dcae-190">Domyślnie usługa SQL Data Warehouse przykłady 20 procent tabeli hello podczas tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="5dcae-191">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="5dcae-192">B.</span><span class="sxs-lookup"><span data-stu-id="5dcae-192">B.</span></span> <span data-ttu-id="5dcae-193">Tworzenie statystyk pojedynczej kolumny, sprawdzając każdego wiersza</span><span class="sxs-lookup"><span data-stu-id="5dcae-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="5dcae-194">częstotliwość próbkowania domyślne Hello równy 20% jest wystarczające w większości sytuacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="5dcae-195">Można jednak dostosować częstotliwość próbkowania hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="5dcae-196">Pełna hello toosample tabeli, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="5dcae-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="5dcae-197">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="5dcae-198">C.</span><span class="sxs-lookup"><span data-stu-id="5dcae-198">C.</span></span> <span data-ttu-id="5dcae-199">Tworzenie statystyk pojedynczej kolumny, określając hello próbkowania</span><span class="sxs-lookup"><span data-stu-id="5dcae-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="5dcae-200">Alternatywnie można określić rozmiar próbki hello w procentach:</span><span class="sxs-lookup"><span data-stu-id="5dcae-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="5dcae-201">D.</span><span class="sxs-lookup"><span data-stu-id="5dcae-201">D.</span></span> <span data-ttu-id="5dcae-202">Tworzenie statystyk pojedynczej kolumny dla niektórych wierszy hello</span><span class="sxs-lookup"><span data-stu-id="5dcae-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="5dcae-203">Inną opcją, można utworzyć statystyki w części hello wierszy w tabeli.</span><span class="sxs-lookup"><span data-stu-id="5dcae-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="5dcae-204">Jest to filtrowane statystyki.</span><span class="sxs-lookup"><span data-stu-id="5dcae-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="5dcae-205">Można na przykład użyć statystykę filtrowaną, planując tooquery określonej partycji tabeli partycjonowanej duże.</span><span class="sxs-lookup"><span data-stu-id="5dcae-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="5dcae-206">Tworzenie statystyk na powitania tylko wartości partycji, dokładność hello statystyk hello będzie poprawić, a poprawić wydajność zapytań, w związku z tym.</span><span class="sxs-lookup"><span data-stu-id="5dcae-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="5dcae-207">Ten przykład tworzy statystyki zakresu wartości.</span><span class="sxs-lookup"><span data-stu-id="5dcae-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="5dcae-208">wartości Hello, może być zdefiniowana w partycji toomatch hello zakres wartości.</span><span class="sxs-lookup"><span data-stu-id="5dcae-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="5dcae-209">Dla hello tooconsider Optymalizator zapytań przy użyciu statystykę filtrowaną, gdy wybiera hello planu zapytania rozproszone hello zapytania musi mieścić się w definicji hello hello statystyki obiektu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="5dcae-210">Przy użyciu hello poprzedni przykład, hello kwerendy których klauzula wymaga wartości col1 toospecify między 2000101 i 20001231.</span><span class="sxs-lookup"><span data-stu-id="5dcae-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="5dcae-211">E.</span><span class="sxs-lookup"><span data-stu-id="5dcae-211">E.</span></span> <span data-ttu-id="5dcae-212">Tworzenie statystyk pojedynczej kolumny z wszystkimi opcjami hello</span><span class="sxs-lookup"><span data-stu-id="5dcae-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="5dcae-213">Opcje hello można oczywiście łączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="5dcae-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="5dcae-214">w poniższym przykładzie Hello tworzy obiekt statystykę filtrowaną z niestandardowych próbkowania:</span><span class="sxs-lookup"><span data-stu-id="5dcae-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="5dcae-215">Aby hello pełne informacje, zobacz [instrukcji CREATE STATISTICS] [ CREATE STATISTICS] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dcae-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="5dcae-216">F.</span><span class="sxs-lookup"><span data-stu-id="5dcae-216">F.</span></span> <span data-ttu-id="5dcae-217">Tworzenie statystyk wielokolumnowego</span><span class="sxs-lookup"><span data-stu-id="5dcae-217">Create multi-column statistics</span></span>
<span data-ttu-id="5dcae-218">toocreate statystyki wielokolumnowego, po prostu użyć hello poprzednich przykładach, ale Określ większą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="5dcae-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="5dcae-219">Witaj histogram, który jest używany tooestimate liczbę wierszy w wyniku zapytania hello, jest dostępny tylko dla pierwszej kolumny hello definicji obiektu statystyki hello na liście.</span><span class="sxs-lookup"><span data-stu-id="5dcae-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="5dcae-220">W tym przykładzie hello histogram znajduje się na *produktu\_kategorii*.</span><span class="sxs-lookup"><span data-stu-id="5dcae-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="5dcae-221">Statystyki między kolumny są obliczane na *produktu\_kategorii* i *produktu\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="5dcae-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="5dcae-222">Ponieważ korelacji między *produktu\_kategorii* i *produktu\_sub\_kategorii*, stat wielokolumnowego mogą być przydatne, jeśli te kolumny są dostępne. na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="5dcae-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="5dcae-223">G.</span><span class="sxs-lookup"><span data-stu-id="5dcae-223">G.</span></span> <span data-ttu-id="5dcae-224">Tworzenie statystyk dotyczących wszystkich hello kolumn w tabeli</span><span class="sxs-lookup"><span data-stu-id="5dcae-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="5dcae-225">Statystyki jednokierunkowej toocreate jest tooissues polecenia CREATE STATISTICS po utworzeniu tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="5dcae-226">H.</span><span class="sxs-lookup"><span data-stu-id="5dcae-226">H.</span></span> <span data-ttu-id="5dcae-227">Użyj statystyki toocreate procedury składowanej dla wszystkich kolumn w bazie danych</span><span class="sxs-lookup"><span data-stu-id="5dcae-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="5dcae-228">Magazyn danych SQL nie ma odpowiednika procedury składowanej systemu zbyt [] [sp_create_stats] w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dcae-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="5dcae-229">Tę procedurę składowaną tworzy obiekt statystyki jednej kolumny w każdej kolumnie hello bazy danych, który nie ma jeszcze statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="5dcae-230">Pomoże to wprowadzenie do projektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-230">This will help you get started with your database design.</span></span> <span data-ttu-id="5dcae-231">Możesz wolnego tooadapt go wymaga tooyour.</span><span class="sxs-lookup"><span data-stu-id="5dcae-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="5dcae-232">toocreate statystyki dla wszystkich kolumn w tabeli hello tę procedurę, po prostu wywoływanie procedury hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="5dcae-233">Przykłady: Aktualizuj statystyki</span><span class="sxs-lookup"><span data-stu-id="5dcae-233">Examples: update statistics</span></span>
<span data-ttu-id="5dcae-234">statystyki tooupdate, można:</span><span class="sxs-lookup"><span data-stu-id="5dcae-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="5dcae-235">Zaktualizuj jeden obiekt statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-235">Update one statistics object.</span></span> <span data-ttu-id="5dcae-236">Określ nazwę hello hello statystyki obiekt ma tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5dcae-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="5dcae-237">Zaktualizuj wszystkie obiekty statystyki dla tabeli.</span><span class="sxs-lookup"><span data-stu-id="5dcae-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="5dcae-238">Określ nazwę hello tabeli hello zamiast jeden obiekt poszczególnych statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="5dcae-239">A.</span><span class="sxs-lookup"><span data-stu-id="5dcae-239">A.</span></span> <span data-ttu-id="5dcae-240">Zaktualizuj jeden obiekt poszczególnych statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-240">Update one specific statistics object</span></span>
<span data-ttu-id="5dcae-241">Użyj następującej składni tooupdate obiektu poszczególnych statystyk hello:</span><span class="sxs-lookup"><span data-stu-id="5dcae-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="5dcae-242">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="5dcae-243">Aktualizacja poszczególnych statystyk obiektów, można zminimalizować hello statystyki toomanage wymagany czas i zasoby.</span><span class="sxs-lookup"><span data-stu-id="5dcae-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="5dcae-244">Wymaga to niektóre traktować, jednak toochoose hello najważniejsze dane statystyczne obiektów tooupdate.</span><span class="sxs-lookup"><span data-stu-id="5dcae-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="5dcae-245">B.</span><span class="sxs-lookup"><span data-stu-id="5dcae-245">B.</span></span> <span data-ttu-id="5dcae-246">Aktualizuj wszystkie statystyki dla tabeli</span><span class="sxs-lookup"><span data-stu-id="5dcae-246">Update all statistics on a table</span></span>
<span data-ttu-id="5dcae-247">Oznacza to prosta metoda aktualizowania wszystkich obiektów statystyki hello na tabelę.</span><span class="sxs-lookup"><span data-stu-id="5dcae-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="5dcae-248">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="5dcae-249">Ta instrukcja jest łatwe toouse.</span><span class="sxs-lookup"><span data-stu-id="5dcae-249">This statement is easy toouse.</span></span> <span data-ttu-id="5dcae-250">Pamiętaj tylko to aktualizuje wszystkie statystyki na powitania tabeli i dlatego może wykonać więcej pracy, niż jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5dcae-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="5dcae-251">Jeśli wydajność hello nie stanowi to problemu, jest ostatecznie hello najprostszym i najbardziej kompleksowe sposób tooguarantee statystyki są aktualne.</span><span class="sxs-lookup"><span data-stu-id="5dcae-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="5dcae-252">Podczas aktualizowania wszystkich statystyk dotyczących tabeli, SQL Data Warehouse nie skanowania tabeli hello toosample dla poszczególnych statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="5dcae-253">Jeśli tabela hello jest duży, ma wiele kolumn i ilość danych statystycznych, może być bardziej efektywne statystyki poszczególnych tooupdate zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="5dcae-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="5dcae-254">Dla implementacji `UPDATE STATISTICS` procedury można znaleźć pod adresem hello [tabel tymczasowych] [ Temporary] artykułu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="5dcae-255">Witaj implementacji metody jest nieco inne toohello `CREATE STATISTICS` powyższą procedurę, ale wynik końcowy hello jest hello takie same.</span><span class="sxs-lookup"><span data-stu-id="5dcae-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="5dcae-256">Aby hello pełnej składni, zobacz [Update Statistics] [ Update Statistics] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dcae-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="5dcae-257">Statystyki metadanych</span><span class="sxs-lookup"><span data-stu-id="5dcae-257">Statistics metadata</span></span>
<span data-ttu-id="5dcae-258">Istnieje kilka widok systemu i funkcje, których można używać toofind informacji na temat statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="5dcae-259">Na przykład widać, jeśli obiekt statystyki może być nieaktualne przy użyciu hello Data Statystyka funkcja toosee, gdy statystyki ostatnio zostały utworzone lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5dcae-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="5dcae-260">Widoków wykazu statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-260">Catalog views for statistics</span></span>
<span data-ttu-id="5dcae-261">Widoki te systemu zawierają informacje o statystyki:</span><span class="sxs-lookup"><span data-stu-id="5dcae-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="5dcae-262">Przeglądanie katalogu</span><span class="sxs-lookup"><span data-stu-id="5dcae-262">Catalog View</span></span> | <span data-ttu-id="5dcae-263">Opis</span><span class="sxs-lookup"><span data-stu-id="5dcae-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5dcae-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="5dcae-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="5dcae-265">Jeden wiersz dla każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="5dcae-265">One row for each column.</span></span> |
| <span data-ttu-id="5dcae-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="5dcae-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="5dcae-267">Jeden wiersz dla każdego obiektu w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="5dcae-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="5dcae-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="5dcae-269">Jeden wiersz dla każdego schematu hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="5dcae-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="5dcae-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="5dcae-271">Jeden wiersz dla każdego obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="5dcae-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="5dcae-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="5dcae-273">Jeden wiersz dla każdej kolumny w obiekcie statystyki hello.</span><span class="sxs-lookup"><span data-stu-id="5dcae-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="5dcae-274">Połączone ponownie toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="5dcae-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="5dcae-275">[Widok sys.Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="5dcae-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="5dcae-276">Jeden wiersz dla każdej tabeli (w tym tabel zewnętrznych).</span><span class="sxs-lookup"><span data-stu-id="5dcae-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="5dcae-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="5dcae-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="5dcae-278">Jeden wiersz dla każdego typu danych.</span><span class="sxs-lookup"><span data-stu-id="5dcae-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="5dcae-279">Funkcje systemu statystyk</span><span class="sxs-lookup"><span data-stu-id="5dcae-279">System functions for statistics</span></span>
<span data-ttu-id="5dcae-280">Funkcje systemu są przydatne w przypadku pracy z statystyki:</span><span class="sxs-lookup"><span data-stu-id="5dcae-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="5dcae-281">System — funkcja</span><span class="sxs-lookup"><span data-stu-id="5dcae-281">System Function</span></span> | <span data-ttu-id="5dcae-282">Opis</span><span class="sxs-lookup"><span data-stu-id="5dcae-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5dcae-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="5dcae-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="5dcae-284">Obiekt statystyki hello Data ostatniej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dcae-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="5dcae-285">[POLECENIE DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="5dcae-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="5dcae-286">Zawiera podsumowanie poziomu i szczegółowe informacje o dystrybucji hello wartości rozumieniu hello statystyki obiektu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="5dcae-287">Łączenie statystyk kolumny i funkcji w jednym widoku</span><span class="sxs-lookup"><span data-stu-id="5dcae-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="5dcae-288">Ten widok udostępnia kolumn ze sobą powiązane toostatistics i wyników z funkcji [] hello [STATS_DATE()].</span><span class="sxs-lookup"><span data-stu-id="5dcae-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="5dcae-289">Przykłady DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="5dcae-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="5dcae-290">DBCC SHOW_STATISTICS() zawiera dane hello przechowywane w obiekcie statystyki.</span><span class="sxs-lookup"><span data-stu-id="5dcae-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="5dcae-291">Te dane składa się z trzech części.</span><span class="sxs-lookup"><span data-stu-id="5dcae-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="5dcae-292">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="5dcae-292">Header</span></span>
2. <span data-ttu-id="5dcae-293">Wektor gęstość</span><span class="sxs-lookup"><span data-stu-id="5dcae-293">Density Vector</span></span>
3. <span data-ttu-id="5dcae-294">Histogram</span><span class="sxs-lookup"><span data-stu-id="5dcae-294">Histogram</span></span>

<span data-ttu-id="5dcae-295">Witaj nagłówka metadane dotyczące hello statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="5dcae-296">Hello histogram Wyświetla dystrybucji hello wartości w pierwszej kolumnie hello hello statystyki obiektu klucza.</span><span class="sxs-lookup"><span data-stu-id="5dcae-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="5dcae-297">Wektor gęstość Hello mierzy korelacji między kolumny.</span><span class="sxs-lookup"><span data-stu-id="5dcae-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="5dcae-298">SQLDW oblicza szacowania kardynalności o dowolne dane hello hello statystyki obiektu.</span><span class="sxs-lookup"><span data-stu-id="5dcae-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="5dcae-299">Pokaż nagłówka, gęstości i histogramu</span><span class="sxs-lookup"><span data-stu-id="5dcae-299">Show header, density, and histogram</span></span>
<span data-ttu-id="5dcae-300">Ten prosty przykład przedstawia wszystkich trzech części obiektu statystyk.</span><span class="sxs-lookup"><span data-stu-id="5dcae-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="5dcae-301">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="5dcae-302">Pokaż co najmniej jeden części DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="5dcae-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="5dcae-303">Jeśli interesuje Cię tylko wyświetlanie określonych części, użyj hello `WITH` klauzuli i określić, które części mają toosee:</span><span class="sxs-lookup"><span data-stu-id="5dcae-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="5dcae-304">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5dcae-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="5dcae-305">Polecenie DBCC SHOW_STATISTICS() różnic</span><span class="sxs-lookup"><span data-stu-id="5dcae-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="5dcae-306">Polecenie DBCC SHOW_STATISTICS() bardziej ściśle jest zaimplementowana w tooSQL porównaniu magazynu danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dcae-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="5dcae-307">Nieudokumentowanej funkcje nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5dcae-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="5dcae-308">Nie można użyć Stats_stream</span><span class="sxs-lookup"><span data-stu-id="5dcae-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="5dcae-309">Nie można dołączyć wyniki konkretne podzestawy danych statystyki np. (STAT_HEADER sprzężenia DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="5dcae-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="5dcae-310">Nie można ustawić NO_INFOMSGS dla pomijania wiadomości</span><span class="sxs-lookup"><span data-stu-id="5dcae-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="5dcae-311">Nie można użyć nazwy statystyki nawiasy kwadratowe</span><span class="sxs-lookup"><span data-stu-id="5dcae-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="5dcae-312">Nie można użyć kolumny nazw tooidentify statystyki obiektów</span><span class="sxs-lookup"><span data-stu-id="5dcae-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="5dcae-313">Błąd niestandardowy 2767 nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="5dcae-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dcae-314">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5dcae-314">Next steps</span></span>
<span data-ttu-id="5dcae-315">Aby uzyskać więcej informacji, zobacz [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5dcae-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="5dcae-316">toolearn więcej, zobacz artykuły hello na [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Indeksowania tabeli][Index], [partycjonowania tabeli] [ Partition] i [ Tabele tymczasowe][Temporary].</span><span class="sxs-lookup"><span data-stu-id="5dcae-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="5dcae-317">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="5dcae-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
