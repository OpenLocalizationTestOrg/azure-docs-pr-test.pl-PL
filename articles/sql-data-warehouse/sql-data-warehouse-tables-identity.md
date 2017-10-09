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
# <a name="create-surrogate-keys-by-using-identity"></a>Tworzenie kluczy dwuskładnikowego przy użyciu tożsamości
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Typy danych][Data Types]
> * [Dystrybuuj][Distribute]
> * [Indeks][Index]
> * [Partycji][Partition]
> * [Statystyki][Statistics]
> * [Tymczasowe][Temporary]
> * [Tożsamości][Identity]
> 
> 

Wiele Modelarze danych, takich jak klucze Surogat toocreate na ich tabel podczas projektowania modeli magazynu danych. Umożliwia tooachieve właściwość IDENTITY hello w tym celu po prostu i efektywnie bez wpływu na wydajność obciążenia. 

## <a name="get-started-with-identity"></a>Rozpoczynanie pracy z tożsamości
Można zdefiniować tabelę jako mający właściwość IDENTITY hello podczas tworzenia tabeli hello przy użyciu składni, która jest podobne toohello następującej instrukcji:

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

Następnie można użyć `INSERT..SELECT` toopopulate hello tabeli.

## <a name="behavior"></a>Zachowanie
Hello właściwość IDENTITY jest zaprojektowana tooscale się we wszystkich dystrybucje hello w magazynie danych hello bez wpływu na wydajność obciążenia. W związku z tym implementacja hello tożsamości jest zorientowany osiągnięcie tych celów. W tej sekcji przedstawiono wszystkie szczegóły hello z toohelp implementacji hello rozumiesz je w pełnym.  

### <a name="allocation-of-values"></a>Alokacja wartości
Witaj właściwość IDENTITY nie gwarantuje kolejności hello w których hello Surogat wartości są przydzielone, która odzwierciedla hello zachowanie programu SQL Server i bazy danych SQL Azure. Jednak w usłudze Azure SQL Data Warehouse, braku hello gwarancji jest większa. 

Poniższy przykład Hello jest ilustracji:

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

Dwa wiersze w hello poprzedzających przykładzie, jest dystrybucji 1. Hello pierwszy wiersz zawiera wartość zastępcza hello 1 w kolumnie `C1`, a drugim wierszu hello ma wartość zastępcza hello 61. Obie te wartości zostały wygenerowane przez hello właściwość IDENTITY. Jednak alokacji hello hello wartości nie jest ciągły. To zachowanie jest celowe.

### <a name="skewed-data"></a>Spowodowałoby zafałszowanie danych 
zakres wartości dla typu danych hello Hello są rozmieszczone równomiernie w obrębie hello dystrybucji. Jeśli tabela rozproszona odczuwa spowodowałoby zafałszowanie danych, następnie hello zakres wartości, które można wyczerpany przedwcześnie datatype toohello dostępne. Na przykład, jeśli wszystkie dane hello kończy się w jednym dystrybucji, następnie efektywnie hello tabela ma dostęp tooonly jednej szóstej hello wartości typu danych hello. Z tego powodu hello właściwość IDENTITY jest ograniczona zbyt`INT` i `BIGINT` tylko typy danych.

### <a name="selectinto"></a>WYBIERZ... DO
Po wybraniu istniejące kolumny tożsamości do nowej tabeli hello nowa kolumna dziedziczy właściwość IDENTITY hello, chyba że jest spełniony jeden z hello następujące warunki:
- Instrukcja SELECT Hello zawiera sprzężenia.
- Wiele instrukcji "SELECT" są sprzęgane przy użyciu UNION.
- Kolumna tożsamości Hello jest wymieniona więcej niż jeden raz na liście wyboru hello.
- Kolumna tożsamości Hello jest częścią wyrażenia.
    
Jeśli jeden z tych warunków jest prawdziwy, kolumny hello jest tworzony NOT NULL zamiast dziedziczenia hello właściwość IDENTITY.

### <a name="create-table-as-select"></a>UTWÓRZ TABLE AS SELECT
Sposób tworzenia tabeli jako wybierz (CTAS) hello takie samo zachowanie programu SQL Server, który opisano w wybierz... DO. Jednak nie można określić właściwości tożsamości w definicji kolumny hello hello `CREATE TABLE` element hello instrukcji. Można także nie można użyć funkcji IDENTITY hello w hello `SELECT` częścią hello CTAS. toopopulate tabeli, potrzebujesz toouse `CREATE TABLE` toodefine hello tabeli następuje `INSERT..SELECT` toopopulate go.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Jawnie wstawić wartości w kolumnie tożsamości 
Magazyn danych SQL obsługuje `SET IDENTITY_INSERT <your table> ON|OFF` składni. Możesz użyć tej składni tooexplicitly Wstaw wartości w kolumnie tożsamości hello.

Wiele Modelarze danych jak toouse ujemna wstępnie zdefiniowanych wartości dla niektórych wierszy wymiarami. Przykładem jest hello -1 lub "Nieznany element członkowski" wiersza. 

skrypt dalej Hello pokazuje, jak dodać ten wiersz tooexplicitly przy użyciu USTAWIONY atrybut IDENTITY_INSERT:

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

## <a name="load-data-into-a-table-with-identity"></a>Ładowanie danych do tabeli o tożsamości

obecność Hello hello właściwość IDENTITY ma niektórych kod ładowania danych tooyour skutki. W tej sekcji opisano niektóre z wzorców podstawowych ładowania danych do tabel za pomocą tożsamości. 

### <a name="load-data-with-polybase"></a>Ładowanie danych za pomocą usługi PolyBase
tooload dane do tabeli i generowanie klucza dwuskładnikowego przy użyciu tożsamości, Utwórz tabelę hello, a następnie użyć INSERT... Wybierz lub Wstaw... WARTOŚCI tooperform hello obciążenia.

Witaj poniższy przykład prezentuje hello podstawowy wzorzec:
 
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
> Nie jest możliwe toouse `CREATE TABLE AS SELECT` obecnie, podczas ładowania danych do tabeli z kolumną tożsamości.
> 

Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia (BCP) programu do kopiowania zbiorczego hello zobacz następujące artykuły hello:

- [Obciążenia przy użyciu programu PolyBase][]
- [Najlepsze rozwiązania w zakresie programu PolyBase][]

### <a name="load-data-with-bcp"></a>Ładowanie danych za pomocą narzędzia BCP
BCP jest narzędziem wiersza polecenia, których można używać tooload danych do usługi SQL Data Warehouse. Jeden z jego parametrów (-E) kontrolki hello zachowanie BCP podczas ładowania danych do tabeli z kolumną tożsamości. 

W przypadku -E hello wartości przechowywane w pliku wejściowym hello hello kolumny o tożsamości są zachowywane. Jeśli jest -E *nie* określone wartości hello w tej kolumnie są ignorowane. Jeśli nie dołączono hello kolumny tożsamości, dane hello są ładowane normalnego. wartości Hello są generowane, zgodnie z toohello inkrementacji i inicjatora zasad hello właściwości.

Aby uzyskać więcej informacji na ładowanie danych przy użyciu narzędzia BCP Zobacz hello następujące artykuły:

- [Obciążenia za pomocą narzędzia BCP][]
- [Narzędzie BCP w witrynie MSDN][]

## <a name="catalog-views"></a>Widoków wykazu
Magazyn danych SQL obsługuje hello `sys.identity_columns` widoku katalogu. Ten widok może być używane tooidentify kolumny, która ma właściwość IDENTITY hello.

toohelp lepiej zrozumieć hello schematu bazy danych, w tym przykładzie pokazano sposób toointegrate `sys.identity_columns` z innymi widokami katalog systemu:

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

## <a name="limitations"></a>Ograniczenia
Nie można użyć Hello właściwość IDENTITY w hello następujące scenariusze:
- Gdzie hello kolumny danych nie jest typu INT lub BIGINT
- Kiedy kolumny hello jest również hello dystrybucji kluczy
- Gdy tabela hello jest tabeli zewnętrznej 

następujące funkcje pokrewne Hello nie są obsługiwane w usłudze SQL Data Warehouse:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [ATRYBUTU IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [POLECENIE DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Zadania

Ta sekcja zawiera niektóre przykładowy kod tooperform typowych zadań można użyć podczas pracy z kolumn tożsamości.

> [!NOTE] 
> Kolumna C1 jest hello tożsamości w hello wszystkie następujące zadania.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Znajdź wartość hello najwyższy przydzielone dla tabeli
Użyj hello `MAX()` funkcji toodetermine hello najwyższą wartość przydzielone dla tabeli rozproszonych:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Znaleźć hello początkowej i wartości przyrostu hello właściwość IDENTITY
Możesz użyć hello katalogu widoków toodiscover hello tożsamości inkrementacji i inicjatora konfiguracji wartości dla tabeli za pomocą hello następujące zapytania: 

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

## <a name="next-steps"></a>Następne kroki

* toolearn więcej informacji na temat tworzenia tabel, zobacz [omówienie tabeli][Overview], [typów danych tabeli][Data Types], [dystrybucji tabeli] [ Distribute], [Indeksu tabeli][Index], [partycji tabeli][Partition], i [ Tabele tymczasowe][Temporary]. 
* Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse][SQL Data Warehouse Best Practices].  

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
