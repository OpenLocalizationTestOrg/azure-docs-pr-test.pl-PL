---
title: aaaMigrate Twojego tooSQL kodu SQL Data Warehouse | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące migrowania związane z opracowywaniem rozwiązań programu SQL tooAzure kodu SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Migracja z tooSQL kodu SQL magazynu danych
W tym artykule opisano zmiany kodu, prawdopodobnie zajdzie toomake podczas migrowania kodu z innego tooSQL bazy danych magazynu danych. Niektóre funkcje usługi SQL Data Warehouse może znacznie poprawić wydajność, ponieważ są one toowork zaprojektowanych w sposób rozproszonych. Jednak toomaintain wydajność i skalę, niektóre funkcje również nie są dostępne.

## <a name="common-t-sql-limitations"></a>Typowych ograniczeń T-SQL
Witaj następujące listy zawiera podsumowanie hello najczęściej używane funkcje, które nie obsługuje usługi SQL Data Warehouse. Witaj łącza prowadzą tooworkarounds hello nieobsługiwane funkcje:

* [Sprzężenia ANSI na aktualizacje][ANSI joins on updates]
* [Sprzężenia ANSI na usuwaniu][ANSI joins on deletes]
* [Instrukcja merge][merge statement]
* sprzężenia między bazami danych
* [kursory][cursors]
* [INSERT... EXEC][INSERT..EXEC]
* klauzuli OUTPUT
* wbudowane funkcje zdefiniowane przez użytkownika
* wiele instrukcji funkcji
* [wspólnych wyrażeniach tabel](#Common-table-expressions)
* [cykliczne wspólnych wyrażeniach tabel (CTE)] (#Recursive-common-table-expressions-(CTE)
* Funkcje środowiska CLR i procedury
* Funkcja $partition
* zmiennych tabel
* Tabela wartości parametrów
* Transakcje rozproszone
* Commit / rollback Praca
* Zapisz transakcji
* Kontekst wykonywania (EXECUTE AS)
* [Grupuj według klauzuli z pakietem zbiorczym / modułu / Ustawia opcje grupowania][group by clause with rollup / cube / grouping sets options]
* [poziomów zagnieżdżenia niż 8][nesting levels beyond 8]
* [aktualizowanie za pośrednictwem widoków][updating through views]
* [Użycie wybierz przypisanie zmiennej][use of select for variable assignment]
* [Typ danych nie MAX dynamiczne ciągów SQL][no MAX data type for dynamic SQL strings]

Na szczęście wokół można pracować większość tych ograniczeń. Wyjaśnienia dotyczące znajdują się w hello programowanie odpowiednich artykułów wymienionych powyżej.

## <a name="supported-cte-features"></a>Obsługiwane funkcje CTE
Wspólnych wyrażeniach tabel (wyrażeń CTE) są obsługiwane częściowo w usłudze SQL Data Warehouse.  obecnie obsługiwane są następujące funkcje CTE Hello:

* CTE można określić w instrukcji SELECT.
* CTE można określić w instrukcji CREATE VIEW.
* CTE można określić w instrukcji tworzenia tabeli jako wybierz (CTAS).
* CTE można określić w instrukcji tworzenia zdalnego tabeli jako wybierz (CRTAS).
* CTE można określić w instrukcji tworzenia zewnętrznego tabeli jako wybierz (CETAS).
* Tabela zdalna mogą być przywoływane z CTE.
* Tabeli zewnętrznej można odwoływać się z CTE.
* Wiele definicji zapytania CTE można zdefiniować w CTE.

## <a name="cte-limitations"></a>Ograniczenia CTE
Wspólnego wyrażenia tabeli mają następujące ograniczenia z magazynu danych SQL, w tym:

* CTE musi następować jednej instrukcji SELECT. INSERT, UPDATE, DELETE i instrukcjach MERGE nie są obsługiwane.
* Wspólne wyrażenie tabeli, zawierającą tooitself odwołań (cykliczne wspólne wyrażenie tabeli) nie jest obsługiwany (patrz poniżej).
* Określanie więcej niż jeden z klauzulą w CTE jest niedozwolone. Na przykład jeśli CTE_query_definition zawiera podzapytanie, że podzapytania nie może zawierać zagnieżdżoną z klauzulą definiujący CTE innego.
* Nie można użyć klauzuli ORDER BY w hello CTE_query_definition, z wyjątkiem, gdy określono klauzulę TOP.
* CTE jest używana w instrukcji, która jest częścią partii, instrukcja hello przed nią musi następować średnikiem.
* W przypadku w instrukcjach przygotowane przez sp_prepare wspólnych wyrażeń tabel będą zachowywać się hello sam sposób jak inne instrukcji SELECT w PDW. Jednak jeśli wspólnych wyrażeń tabel są używane jako część CETAS przygotowane przez sp_prepare, zachowanie hello może odroczyć z programu SQL Server i inne instrukcje PDW ze względu na sposób hello powiązania jest zaimplementowany dla sp_prepare. Wybierz OPCJĘ odwołania CTE wykorzystanie niewłaściwej kolumnie, która nie istnieje w CTE hello sp_prepare przechodzą bez wykrycia hello błąd, ale błąd hello zostanie zgłoszony podczas procedury składowanej sp_execute zamiast tego.

## <a name="recursive-ctes"></a>Cyklicznych wspólnych wyrażeń tabel
Cyklicznych wspólnych wyrażeń tabel nie są obsługiwane w usłudze SQL Data Warehouse.  Migracja Hello cykliczne CTE mogą być nieco złożone i proces najlepsze hello jest toobreak go do wielu kroków. Zwykle można skorzystać z pętli i wypełniania tabeli tymczasowej jako iteracja tymczasowe kwerendy cykliczne hello. Po zapełnieniu tabeli tymczasowej hello mogą następnie zwracać dane hello jako pojedynczy zestaw wyników. Podejście podobne został użyty toosolve `GROUP BY WITH CUBE` w hello [Grupuj według klauzuli z pakietem zbiorczym / modułu / Ustawia opcje grupowania] [ group by clause with rollup / cube / grouping sets options] artykułu.

## <a name="unsupported-system-functions"></a>Nieobsługiwany system funkcji
Dostępne są także niektóre funkcje systemu, które nie są obsługiwane. Hello podstawowe zwykle mogą być używane w magazynowania danych, należą:

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE() —

Niektóre z tych problemów można pracować wokół.

## <a name="rowcount-workaround"></a>@@ROWCOUNT obejście problemu
toowork wokół Brak obsługi @@ROWCOUNT, Tworzenie procedury przechowywanej, która będzie pobierać hello ostatniego liczba wierszy z sys.dm_pdw_request_steps, a następnie wykonaj `EXEC LastRowCount` po instrukcji DML.

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać pełną listę wszystkich obsługiwanych instrukcje T-SQL, zobacz [tematy języka Transact-SQL][Transact-SQL topics].

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
