---
title: "klucze Surogat aaaCreate przy użyciu tożsamości | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse tożsamości toocreate Surogat kluczy w tabelach."
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="65eb4-103">Tworzenie kluczy dwuskładnikowego przy użyciu tożsamości</span><span class="sxs-lookup"><span data-stu-id="65eb4-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="65eb4-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="65eb4-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="65eb4-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="65eb4-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="65eb4-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="65eb4-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="65eb4-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="65eb4-107">[Index][Index]</span></span>
> * <span data-ttu-id="65eb4-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="65eb4-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="65eb4-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="65eb4-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="65eb4-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="65eb4-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="65eb4-111">[Tożsamości][Identity]</span><span class="sxs-lookup"><span data-stu-id="65eb4-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="65eb4-112">Wiele Modelarze danych, takich jak klucze Surogat toocreate na ich tabel podczas projektowania modeli magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="65eb4-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="65eb4-113">Umożliwia tooachieve właściwość IDENTITY hello w tym celu po prostu i efektywnie bez wpływu na wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="65eb4-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="65eb4-114">Rozpoczynanie pracy z tożsamości</span><span class="sxs-lookup"><span data-stu-id="65eb4-114">Get started with IDENTITY</span></span>
<span data-ttu-id="65eb4-115">Można zdefiniować tabelę jako mający właściwość IDENTITY hello podczas tworzenia tabeli hello przy użyciu składni, która jest podobne toohello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="65eb4-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="65eb4-116">Następnie można użyć `INSERT..SELECT` toopopulate hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="65eb4-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="65eb4-117">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="65eb4-117">Behavior</span></span>
<span data-ttu-id="65eb4-118">Hello właściwość IDENTITY jest zaprojektowana tooscale się we wszystkich dystrybucje hello w magazynie danych hello bez wpływu na wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="65eb4-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="65eb4-119">W związku z tym implementacja hello tożsamości jest zorientowany osiągnięcie tych celów.</span><span class="sxs-lookup"><span data-stu-id="65eb4-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="65eb4-120">W tej sekcji przedstawiono wszystkie szczegóły hello z toohelp implementacji hello rozumiesz je w pełnym.</span><span class="sxs-lookup"><span data-stu-id="65eb4-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="65eb4-121">Alokacja wartości</span><span class="sxs-lookup"><span data-stu-id="65eb4-121">Allocation of values</span></span>
<span data-ttu-id="65eb4-122">Witaj właściwość IDENTITY nie gwarantuje kolejności hello w których hello Surogat wartości są przydzielone, która odzwierciedla hello zachowanie programu SQL Server i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="65eb4-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="65eb4-123">Jednak w usłudze Azure SQL Data Warehouse, braku hello gwarancji jest większa.</span><span class="sxs-lookup"><span data-stu-id="65eb4-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="65eb4-124">Poniższy przykład Hello jest ilustracji:</span><span class="sxs-lookup"><span data-stu-id="65eb4-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="65eb4-125">Dwa wiersze w hello poprzedzających przykładzie, jest dystrybucji 1.</span><span class="sxs-lookup"><span data-stu-id="65eb4-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="65eb4-126">Hello pierwszy wiersz zawiera wartość zastępcza hello 1 w kolumnie `C1`, a drugim wierszu hello ma wartość zastępcza hello 61.</span><span class="sxs-lookup"><span data-stu-id="65eb4-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="65eb4-127">Obie te wartości zostały wygenerowane przez hello właściwość IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="65eb4-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="65eb4-128">Jednak alokacji hello hello wartości nie jest ciągły.</span><span class="sxs-lookup"><span data-stu-id="65eb4-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="65eb4-129">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="65eb4-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="65eb4-130">Spowodowałoby zafałszowanie danych</span><span class="sxs-lookup"><span data-stu-id="65eb4-130">Skewed data</span></span> 
<span data-ttu-id="65eb4-131">zakres wartości dla typu danych hello Hello są rozmieszczone równomiernie w obrębie hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="65eb4-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="65eb4-132">Jeśli tabela rozproszona odczuwa spowodowałoby zafałszowanie danych, następnie hello zakres wartości, które można wyczerpany przedwcześnie datatype toohello dostępne.</span><span class="sxs-lookup"><span data-stu-id="65eb4-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="65eb4-133">Na przykład, jeśli wszystkie dane hello kończy się w jednym dystrybucji, następnie efektywnie hello tabela ma dostęp tooonly jednej szóstej hello wartości typu danych hello.</span><span class="sxs-lookup"><span data-stu-id="65eb4-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="65eb4-134">Z tego powodu hello właściwość IDENTITY jest ograniczona zbyt`INT` i `BIGINT` tylko typy danych.</span><span class="sxs-lookup"><span data-stu-id="65eb4-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="65eb4-135">WYBIERZ... DO</span><span class="sxs-lookup"><span data-stu-id="65eb4-135">SELECT..INTO</span></span>
<span data-ttu-id="65eb4-136">Po wybraniu istniejące kolumny tożsamości do nowej tabeli hello nowa kolumna dziedziczy właściwość IDENTITY hello, chyba że jest spełniony jeden z hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="65eb4-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="65eb4-137">Instrukcja SELECT Hello zawiera sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="65eb4-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="65eb4-138">Wiele instrukcji "SELECT" są sprzęgane przy użyciu UNION.</span><span class="sxs-lookup"><span data-stu-id="65eb4-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="65eb4-139">Kolumna tożsamości Hello jest wymieniona więcej niż jeden raz na liście wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="65eb4-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="65eb4-140">Kolumna tożsamości Hello jest częścią wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="65eb4-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="65eb4-141">Jeśli jeden z tych warunków jest prawdziwy, kolumny hello jest tworzony NOT NULL zamiast dziedziczenia hello właściwość IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="65eb4-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="65eb4-142">UTWÓRZ TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="65eb4-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="65eb4-143">Sposób tworzenia tabeli jako wybierz (CTAS) hello takie samo zachowanie programu SQL Server, który opisano w wybierz... DO.</span><span class="sxs-lookup"><span data-stu-id="65eb4-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="65eb4-144">Jednak nie można określić właściwości tożsamości w definicji kolumny hello hello `CREATE TABLE` element hello instrukcji.</span><span class="sxs-lookup"><span data-stu-id="65eb4-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="65eb4-145">Można także nie można użyć funkcji IDENTITY hello w hello `SELECT` częścią hello CTAS.</span><span class="sxs-lookup"><span data-stu-id="65eb4-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="65eb4-146">toopopulate tabeli, potrzebujesz toouse `CREATE TABLE` toodefine hello tabeli następuje `INSERT..SELECT` toopopulate go.</span><span class="sxs-lookup"><span data-stu-id="65eb4-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="65eb4-147">Jawnie wstawić wartości w kolumnie tożsamości</span><span class="sxs-lookup"><span data-stu-id="65eb4-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="65eb4-148">Magazyn danych SQL obsługuje `SET IDENTITY_INSERT <your table> ON|OFF` składni.</span><span class="sxs-lookup"><span data-stu-id="65eb4-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="65eb4-149">Możesz użyć tej składni tooexplicitly Wstaw wartości w kolumnie tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="65eb4-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="65eb4-150">Wiele Modelarze danych jak toouse ujemna wstępnie zdefiniowanych wartości dla niektórych wierszy wymiarami.</span><span class="sxs-lookup"><span data-stu-id="65eb4-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="65eb4-151">Przykładem jest hello -1 lub "Nieznany element członkowski" wiersza.</span><span class="sxs-lookup"><span data-stu-id="65eb4-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="65eb4-152">skrypt dalej Hello pokazuje, jak dodać ten wiersz tooexplicitly przy użyciu USTAWIONY atrybut IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="65eb4-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="65eb4-153">Ładowanie danych do tabeli o tożsamości</span><span class="sxs-lookup"><span data-stu-id="65eb4-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="65eb4-154">obecność Hello hello właściwość IDENTITY ma niektórych kod ładowania danych tooyour skutki.</span><span class="sxs-lookup"><span data-stu-id="65eb4-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="65eb4-155">W tej sekcji opisano niektóre z wzorców podstawowych ładowania danych do tabel za pomocą tożsamości.</span><span class="sxs-lookup"><span data-stu-id="65eb4-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="65eb4-156">Ładowanie danych za pomocą usługi PolyBase</span><span class="sxs-lookup"><span data-stu-id="65eb4-156">Load data with PolyBase</span></span>
<span data-ttu-id="65eb4-157">tooload dane do tabeli i generowanie klucza dwuskładnikowego przy użyciu tożsamości, Utwórz tabelę hello, a następnie użyć INSERT... Wybierz lub Wstaw... WARTOŚCI tooperform hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="65eb4-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="65eb4-158">Witaj poniższy przykład prezentuje hello podstawowy wzorzec:</span><span class="sxs-lookup"><span data-stu-id="65eb4-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="65eb4-159">Nie jest możliwe toouse `CREATE TABLE AS SELECT` obecnie, podczas ładowania danych do tabeli z kolumną tożsamości.</span><span class="sxs-lookup"><span data-stu-id="65eb4-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="65eb4-160">Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia (BCP) programu do kopiowania zbiorczego hello zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="65eb4-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="65eb4-161">[Obciążenia przy użyciu programu PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="65eb4-162">[Najlepsze rozwiązania w zakresie programu PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="65eb4-163">Ładowanie danych za pomocą narzędzia BCP</span><span class="sxs-lookup"><span data-stu-id="65eb4-163">Load data with BCP</span></span>
<span data-ttu-id="65eb4-164">BCP jest narzędziem wiersza polecenia, których można używać tooload danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65eb4-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="65eb4-165">Jeden z jego parametrów (-E) kontrolki hello zachowanie BCP podczas ładowania danych do tabeli z kolumną tożsamości.</span><span class="sxs-lookup"><span data-stu-id="65eb4-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="65eb4-166">W przypadku -E hello wartości przechowywane w pliku wejściowym hello hello kolumny o tożsamości są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="65eb4-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="65eb4-167">Jeśli jest -E *nie* określone wartości hello w tej kolumnie są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="65eb4-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="65eb4-168">Jeśli nie dołączono hello kolumny tożsamości, dane hello są ładowane normalnego.</span><span class="sxs-lookup"><span data-stu-id="65eb4-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="65eb4-169">wartości Hello są generowane, zgodnie z toohello inkrementacji i inicjatora zasad hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="65eb4-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="65eb4-170">Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia BCP Zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="65eb4-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="65eb4-171">[Obciążenia za pomocą narzędzia BCP][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-171">[Load with BCP][]</span></span>
- <span data-ttu-id="65eb4-172">[Narzędzie BCP w witrynie MSDN][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="65eb4-173">Widoków wykazu</span><span class="sxs-lookup"><span data-stu-id="65eb4-173">Catalog views</span></span>
<span data-ttu-id="65eb4-174">Magazyn danych SQL obsługuje hello `sys.identity_columns` widoku katalogu.</span><span class="sxs-lookup"><span data-stu-id="65eb4-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="65eb4-175">Ten widok może być używane tooidentify kolumny, która ma właściwość IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="65eb4-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="65eb4-176">toohelp lepiej zrozumieć hello schematu bazy danych, w tym przykładzie pokazano sposób toointegrate `sys.identity_columns` z innymi widokami katalog systemu:</span><span class="sxs-lookup"><span data-stu-id="65eb4-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="65eb4-177">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="65eb4-177">Limitations</span></span>
<span data-ttu-id="65eb4-178">Nie można użyć Hello właściwość IDENTITY w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="65eb4-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="65eb4-179">Gdzie hello kolumny danych nie jest typu INT lub BIGINT</span><span class="sxs-lookup"><span data-stu-id="65eb4-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="65eb4-180">Kiedy kolumny hello jest również hello dystrybucji kluczy</span><span class="sxs-lookup"><span data-stu-id="65eb4-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="65eb4-181">Gdy tabela hello jest tabeli zewnętrznej</span><span class="sxs-lookup"><span data-stu-id="65eb4-181">Where hello table is an external table</span></span> 

<span data-ttu-id="65eb4-182">następujące funkcje pokrewne Hello nie są obsługiwane w usłudze SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="65eb4-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="65eb4-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="65eb4-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="65eb4-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="65eb4-186">[ATRYBUTU IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="65eb4-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="65eb4-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="65eb4-189">[POLECENIE DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="65eb4-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="65eb4-190">Zadania</span><span class="sxs-lookup"><span data-stu-id="65eb4-190">Tasks</span></span>

<span data-ttu-id="65eb4-191">Ta sekcja zawiera niektóre przykładowy kod tooperform typowych zadań można użyć podczas pracy z kolumn tożsamości.</span><span class="sxs-lookup"><span data-stu-id="65eb4-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="65eb4-192">Kolumna C1 jest hello tożsamości w hello wszystkie następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="65eb4-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="65eb4-193">Znajdź wartość hello najwyższy przydzielone dla tabeli</span><span class="sxs-lookup"><span data-stu-id="65eb4-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="65eb4-194">Użyj hello `MAX()` funkcji toodetermine hello najwyższą wartość przydzielone dla tabeli rozproszonych:</span><span class="sxs-lookup"><span data-stu-id="65eb4-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="65eb4-195">Znaleźć hello początkowej i wartości przyrostu hello właściwość IDENTITY</span><span class="sxs-lookup"><span data-stu-id="65eb4-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="65eb4-196">Możesz użyć hello katalogu widoków toodiscover hello tożsamości inkrementacji i inicjatora konfiguracji wartości dla tabeli za pomocą hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="65eb4-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="65eb4-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65eb4-197">Next steps</span></span>

* <span data-ttu-id="65eb4-198">toolearn więcej informacji na temat tworzenia tabel, zobacz [omówienie tabeli][Overview], [typów danych tabeli][Data Types], [dystrybucji tabeli] [ Distribute], [Indeksu tabeli][Index], [partycji tabeli][Partition], i [ Tabele tymczasowe][Temporary].</span><span class="sxs-lookup"><span data-stu-id="65eb4-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="65eb4-199">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="65eb4-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[Obciążenia za pomocą narzędzia bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Obciążenia przy użyciu programu PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Najlepsze rozwiązania w zakresie programu PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[ATRYBUTU IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[POLECENIE DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[Narzędzie bcp w witrynie MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
