---
title: "Tworzenie kluczy dwuskładnikowego przy użyciu tożsamości | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie korzystania z tożsamości do tworzenia kluczy Surogat na tabelach."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="337c7-103">Tworzenie kluczy dwuskładnikowego przy użyciu tożsamości</span><span class="sxs-lookup"><span data-stu-id="337c7-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="337c7-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="337c7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="337c7-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="337c7-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="337c7-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="337c7-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="337c7-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="337c7-107">[Index][Index]</span></span>
> * <span data-ttu-id="337c7-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="337c7-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="337c7-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="337c7-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="337c7-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="337c7-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="337c7-111">[Tożsamości][Identity]</span><span class="sxs-lookup"><span data-stu-id="337c7-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="337c7-112">Do tworzenia kluczy Surogat na ich tabel, podczas projektowania modeli magazynu danych, takich jak wiele Modelarze danych.</span><span class="sxs-lookup"><span data-stu-id="337c7-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="337c7-113">Właściwość IDENTITY można używać na osiągnięcie tego celu po prostu i efektywnie bez wpływu na wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="337c7-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="337c7-114">Rozpoczynanie pracy z tożsamości</span><span class="sxs-lookup"><span data-stu-id="337c7-114">Get started with IDENTITY</span></span>
<span data-ttu-id="337c7-115">Można zdefiniować tabelę jako mający właściwość IDENTITY podczas tworzenia tabeli za pomocą składni, która jest podobna do następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="337c7-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="337c7-116">Następnie można użyć `INSERT..SELECT` do wypełnienia tabeli.</span><span class="sxs-lookup"><span data-stu-id="337c7-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="337c7-117">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="337c7-117">Behavior</span></span>
<span data-ttu-id="337c7-118">Właściwość IDENTITY jest przeznaczona do skalują poza wszystkie dystrybucje w magazynie danych bez wpływu na wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="337c7-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="337c7-119">W związku z tym implementacja tożsamości jest zorientowany osiągnięcie tych celów.</span><span class="sxs-lookup"><span data-stu-id="337c7-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="337c7-120">W tej sekcji przedstawiono wszystkie szczegóły implementacji, aby ułatwić zrozumienie ich dokładniejszego.</span><span class="sxs-lookup"><span data-stu-id="337c7-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="337c7-121">Alokacja wartości</span><span class="sxs-lookup"><span data-stu-id="337c7-121">Allocation of values</span></span>
<span data-ttu-id="337c7-122">Właściwość IDENTITY nie gwarantuje kolejność, w którym są przydzielane wartości Surogat, odzwierciedla zachowanie programu SQL Server i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="337c7-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="337c7-123">Jednak w usłudze Azure SQL Data Warehouse, braku gwarancji jest większa.</span><span class="sxs-lookup"><span data-stu-id="337c7-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="337c7-124">Poniższy przykład jest ilustracji:</span><span class="sxs-lookup"><span data-stu-id="337c7-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="337c7-125">Dwa wiersze w powyższym przykładzie jest dystrybucji 1.</span><span class="sxs-lookup"><span data-stu-id="337c7-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="337c7-126">Pierwszy wiersz zawiera wartość dwuskładnikowego 1 w kolumnie `C1`, a drugi wiersz zawiera wartość zastępcza 61.</span><span class="sxs-lookup"><span data-stu-id="337c7-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="337c7-127">Obie te wartości zostały wygenerowane przez właściwość tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="337c7-128">Jednak alokacji wartości nie jest ciągły.</span><span class="sxs-lookup"><span data-stu-id="337c7-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="337c7-129">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="337c7-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="337c7-130">Spowodowałoby zafałszowanie danych</span><span class="sxs-lookup"><span data-stu-id="337c7-130">Skewed data</span></span> 
<span data-ttu-id="337c7-131">Zakres wartości dla typu danych są rozmieszczone równomiernie w obrębie dystrybucje.</span><span class="sxs-lookup"><span data-stu-id="337c7-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="337c7-132">Jeśli tabela rozproszona odczuwa spowodowałoby zafałszowanie danych, dostępna na typ danych wartości z zakresu można wyczerpane przedwcześnie.</span><span class="sxs-lookup"><span data-stu-id="337c7-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="337c7-133">Na przykład jeśli wszystkie dane kończy się w jednym dystrybucji, następnie efektywnie tabeli ma dostęp do tylko jednej szóstej wartości typu danych.</span><span class="sxs-lookup"><span data-stu-id="337c7-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="337c7-134">Z tego powodu właściwość IDENTITY jest ograniczona do `INT` i `BIGINT` tylko typy danych.</span><span class="sxs-lookup"><span data-stu-id="337c7-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="337c7-135">WYBIERZ... DO</span><span class="sxs-lookup"><span data-stu-id="337c7-135">SELECT..INTO</span></span>
<span data-ttu-id="337c7-136">Zaznaczenie istniejącej kolumny tożsamości do nowej tabeli nowej kolumny, która dziedziczy właściwości tożsamości, chyba że jest spełniony jeden z następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="337c7-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="337c7-137">Instrukcja SELECT zawiera sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="337c7-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="337c7-138">Wiele instrukcji "SELECT" są sprzęgane przy użyciu UNION.</span><span class="sxs-lookup"><span data-stu-id="337c7-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="337c7-139">Kolumna tożsamości jest wymieniona więcej niż jeden raz na liście wyboru.</span><span class="sxs-lookup"><span data-stu-id="337c7-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="337c7-140">Kolumna tożsamości jest częścią wyrażenia typu.</span><span class="sxs-lookup"><span data-stu-id="337c7-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="337c7-141">Jeśli jeden z tych warunków jest prawdziwy, kolumna jest tworzony NOT NULL zamiast dziedziczenia właściwości tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="337c7-142">UTWÓRZ TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="337c7-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="337c7-143">Tworzenie tabeli jako wybierz (CTAS) następuje tego samego zachowania programu SQL Server jest udokumentowany wybierz pozycję... DO.</span><span class="sxs-lookup"><span data-stu-id="337c7-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="337c7-144">Jednak nie można określić właściwości tożsamości w definicji kolumny `CREATE TABLE` element instrukcji.</span><span class="sxs-lookup"><span data-stu-id="337c7-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="337c7-145">Ponadto nie można używać funkcji IDENTITY w `SELECT` częścią CTAS.</span><span class="sxs-lookup"><span data-stu-id="337c7-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="337c7-146">Aby wypełnić tabeli, należy użyć `CREATE TABLE` do definiowania tabeli, a następnie `INSERT..SELECT` aby wypełnić go.</span><span class="sxs-lookup"><span data-stu-id="337c7-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="337c7-147">Jawnie wstawić wartości w kolumnie tożsamości</span><span class="sxs-lookup"><span data-stu-id="337c7-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="337c7-148">Magazyn danych SQL obsługuje `SET IDENTITY_INSERT <your table> ON|OFF` składni.</span><span class="sxs-lookup"><span data-stu-id="337c7-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="337c7-149">Ta składnia umożliwia jawnie wstawić wartości w kolumnie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="337c7-150">Aby użyć wstępnie zdefiniowanych wartości ujemnych dla niektórych wierszy wymiarami, takich jak wiele Modelarze danych.</span><span class="sxs-lookup"><span data-stu-id="337c7-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="337c7-151">Przykładem jest wiersza "Nieznany element członkowski" lub wartość -1.</span><span class="sxs-lookup"><span data-stu-id="337c7-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="337c7-152">Skrypt dalej pokazano, jak jawnie dodać ten wiersz za pomocą USTAWIĆ atrybut IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="337c7-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="337c7-153">Ładowanie danych do tabeli o tożsamości</span><span class="sxs-lookup"><span data-stu-id="337c7-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="337c7-154">Obecność właściwości tożsamości implikacje niektórych kodu ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="337c7-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="337c7-155">W tej sekcji opisano niektóre z wzorców podstawowych ładowania danych do tabel za pomocą tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="337c7-156">Ładowanie danych za pomocą usługi PolyBase</span><span class="sxs-lookup"><span data-stu-id="337c7-156">Load data with PolyBase</span></span>
<span data-ttu-id="337c7-157">Aby załadować dane do tabeli i generowanie klucza dwuskładnikowego przy użyciu tożsamości, należy utworzyć tabeli, a następnie użyć INSERT... Wybierz lub Wstaw... WARTOŚCI do wykonania obciążenia.</span><span class="sxs-lookup"><span data-stu-id="337c7-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="337c7-158">Poniższy przykład prezentuje podstawowy wzorzec:</span><span class="sxs-lookup"><span data-stu-id="337c7-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="337c7-159">Nie jest możliwe użycie `CREATE TABLE AS SELECT` obecnie, podczas ładowania danych do tabeli z kolumną tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="337c7-160">Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia (BCP) programu kopiowania zbiorczego zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="337c7-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="337c7-161">[Obciążenia przy użyciu programu PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="337c7-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="337c7-162">[Najlepsze rozwiązania w zakresie programu PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="337c7-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="337c7-163">Ładowanie danych za pomocą narzędzia BCP</span><span class="sxs-lookup"><span data-stu-id="337c7-163">Load data with BCP</span></span>
<span data-ttu-id="337c7-164">BCP jest narzędziem wiersza polecenia, które umożliwia ładowanie danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="337c7-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="337c7-165">Jeden z jego parametrów (-E) steruje zachowaniem BCP podczas ładowania danych do tabeli z kolumną tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="337c7-166">W przypadku -E wartości przechowywane w pliku wejściowym dla kolumny o tożsamości są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="337c7-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="337c7-167">Jeśli jest -E *nie* określone wartości w tej kolumnie są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="337c7-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="337c7-168">Jeśli w kolumnie tożsamości nie jest dołączony, dane są ładowane normalnego.</span><span class="sxs-lookup"><span data-stu-id="337c7-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="337c7-169">Wartości są generowane zgodnie z zasadami inkrementacji i inicjatora właściwości.</span><span class="sxs-lookup"><span data-stu-id="337c7-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="337c7-170">Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia BCP zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="337c7-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="337c7-171">[Obciążenia za pomocą narzędzia BCP][]</span><span class="sxs-lookup"><span data-stu-id="337c7-171">[Load with BCP][]</span></span>
- <span data-ttu-id="337c7-172">[Narzędzie BCP w witrynie MSDN][]</span><span class="sxs-lookup"><span data-stu-id="337c7-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="337c7-173">Widoków wykazu</span><span class="sxs-lookup"><span data-stu-id="337c7-173">Catalog views</span></span>
<span data-ttu-id="337c7-174">Magazyn danych SQL obsługuje `sys.identity_columns` widoku katalogu.</span><span class="sxs-lookup"><span data-stu-id="337c7-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="337c7-175">W tym widoku można zidentyfikować kolumny, która ma właściwość IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="337c7-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="337c7-176">Aby lepiej zrozumieć schemat bazy danych, w tym przykładzie pokazano, jak zintegrować `sys.identity_columns` z innymi widokami katalog systemu:</span><span class="sxs-lookup"><span data-stu-id="337c7-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="337c7-177">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="337c7-177">Limitations</span></span>
<span data-ttu-id="337c7-178">Właściwość IDENTITY nie można użyć w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="337c7-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="337c7-179">Gdy typ danych kolumny nie jest INT lub BIGINT</span><span class="sxs-lookup"><span data-stu-id="337c7-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="337c7-180">Gdzie kolumna jest również dystrybucji kluczy</span><span class="sxs-lookup"><span data-stu-id="337c7-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="337c7-181">Gdy tabela jest tabeli zewnętrznej</span><span class="sxs-lookup"><span data-stu-id="337c7-181">Where the table is an external table</span></span> 

<span data-ttu-id="337c7-182">Następujące funkcje pokrewne nie są obsługiwane w usłudze SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="337c7-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="337c7-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="337c7-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="337c7-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="337c7-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="337c7-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="337c7-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="337c7-186">[ATRYBUTU IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="337c7-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="337c7-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="337c7-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="337c7-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="337c7-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="337c7-189">[POLECENIE DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="337c7-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="337c7-190">Zadania</span><span class="sxs-lookup"><span data-stu-id="337c7-190">Tasks</span></span>

<span data-ttu-id="337c7-191">Ta sekcja zawiera niektóre przykładowy kod służący do wykonywania typowych zadań, podczas pracy z kolumn tożsamości.</span><span class="sxs-lookup"><span data-stu-id="337c7-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="337c7-192">Kolumna C1 jest tożsamość w następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="337c7-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="337c7-193">Znajdź największa wartość przydzielonego dla tabeli</span><span class="sxs-lookup"><span data-stu-id="337c7-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="337c7-194">Użyj `MAX()` funkcji, aby ustalić najwyższą wartość przydzielone dla tabeli rozproszonych:</span><span class="sxs-lookup"><span data-stu-id="337c7-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="337c7-195">Znajdź początkowej i wartości przyrostu dla właściwości tożsamości</span><span class="sxs-lookup"><span data-stu-id="337c7-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="337c7-196">Widokach katalogów służy do odnajdywania inkrementacji i inicjatora konfiguracji wartości tożsamości dla tabeli za pomocą następującej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="337c7-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="337c7-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="337c7-197">Next steps</span></span>

* <span data-ttu-id="337c7-198">Aby dowiedzieć się więcej na temat tworzenia tabel, zobacz [omówienie tabeli][Overview], [typów danych tabeli][Data Types], [dystrybucji tabeli] [ Distribute], [Indeksu tabeli][Index], [partycji tabeli][Partition], i [ Tabele tymczasowe][Temporary].</span><span class="sxs-lookup"><span data-stu-id="337c7-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="337c7-199">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="337c7-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="337c7-200">[Obciążenia za pomocą narzędzia bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="337c7-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="337c7-201">[Obciążenia przy użyciu programu PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="337c7-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="337c7-202">[Najlepsze rozwiązania w zakresie programu PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="337c7-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="337c7-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="337c7-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="337c7-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="337c7-206">[ATRYBUTU IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="337c7-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="337c7-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="337c7-209">[POLECENIE DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="337c7-210">[Narzędzie bcp w witrynie MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="337c7-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
