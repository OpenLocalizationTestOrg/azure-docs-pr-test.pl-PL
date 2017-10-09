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
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="df077-103">Migracja z tooSQL kodu SQL magazynu danych</span><span class="sxs-lookup"><span data-stu-id="df077-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="df077-104">W tym artykule opisano zmiany kodu, prawdopodobnie zajdzie toomake podczas migrowania kodu z innego tooSQL bazy danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="df077-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="df077-105">Niektóre funkcje usługi SQL Data Warehouse może znacznie poprawić wydajność, ponieważ są one toowork zaprojektowanych w sposób rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="df077-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="df077-106">Jednak toomaintain wydajność i skalę, niektóre funkcje również nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="df077-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="df077-107">Typowych ograniczeń T-SQL</span><span class="sxs-lookup"><span data-stu-id="df077-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="df077-108">Witaj następujące listy zawiera podsumowanie hello najczęściej używane funkcje, które nie obsługuje usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df077-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="df077-109">Witaj łącza prowadzą tooworkarounds hello nieobsługiwane funkcje:</span><span class="sxs-lookup"><span data-stu-id="df077-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="df077-110">[Sprzężenia ANSI na aktualizacje][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="df077-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="df077-111">[Sprzężenia ANSI na usuwaniu][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="df077-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="df077-112">[Instrukcja merge][merge statement]</span><span class="sxs-lookup"><span data-stu-id="df077-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="df077-113">sprzężenia między bazami danych</span><span class="sxs-lookup"><span data-stu-id="df077-113">cross-database joins</span></span>
* <span data-ttu-id="df077-114">[kursory][cursors]</span><span class="sxs-lookup"><span data-stu-id="df077-114">[cursors][cursors]</span></span>
* <span data-ttu-id="df077-115">[INSERT... EXEC][INSERT..EXEC]</span><span class="sxs-lookup"><span data-stu-id="df077-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="df077-116">klauzuli OUTPUT</span><span class="sxs-lookup"><span data-stu-id="df077-116">output clause</span></span>
* <span data-ttu-id="df077-117">wbudowane funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="df077-117">inline user-defined functions</span></span>
* <span data-ttu-id="df077-118">wiele instrukcji funkcji</span><span class="sxs-lookup"><span data-stu-id="df077-118">multi-statement functions</span></span>
* [<span data-ttu-id="df077-119">wspólnych wyrażeniach tabel</span><span class="sxs-lookup"><span data-stu-id="df077-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="df077-120">[cykliczne wspólnych wyrażeniach tabel (CTE)] (#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="df077-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="df077-121">Funkcje środowiska CLR i procedury</span><span class="sxs-lookup"><span data-stu-id="df077-121">CLR functions and procedures</span></span>
* <span data-ttu-id="df077-122">Funkcja $partition</span><span class="sxs-lookup"><span data-stu-id="df077-122">$partition function</span></span>
* <span data-ttu-id="df077-123">zmiennych tabel</span><span class="sxs-lookup"><span data-stu-id="df077-123">table variables</span></span>
* <span data-ttu-id="df077-124">Tabela wartości parametrów</span><span class="sxs-lookup"><span data-stu-id="df077-124">table value parameters</span></span>
* <span data-ttu-id="df077-125">Transakcje rozproszone</span><span class="sxs-lookup"><span data-stu-id="df077-125">distributed transactions</span></span>
* <span data-ttu-id="df077-126">Commit / rollback Praca</span><span class="sxs-lookup"><span data-stu-id="df077-126">commit / rollback work</span></span>
* <span data-ttu-id="df077-127">Zapisz transakcji</span><span class="sxs-lookup"><span data-stu-id="df077-127">save transaction</span></span>
* <span data-ttu-id="df077-128">Kontekst wykonywania (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="df077-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="df077-129">[Grupuj według klauzuli z pakietem zbiorczym / modułu / Ustawia opcje grupowania][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="df077-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="df077-130">[poziomów zagnieżdżenia niż 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="df077-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="df077-131">[aktualizowanie za pośrednictwem widoków][updating through views]</span><span class="sxs-lookup"><span data-stu-id="df077-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="df077-132">[Użycie wybierz przypisanie zmiennej][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="df077-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="df077-133">[Typ danych nie MAX dynamiczne ciągów SQL][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="df077-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="df077-134">Na szczęście wokół można pracować większość tych ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="df077-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="df077-135">Wyjaśnienia dotyczące znajdują się w hello programowanie odpowiednich artykułów wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="df077-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="df077-136">Obsługiwane funkcje CTE</span><span class="sxs-lookup"><span data-stu-id="df077-136">Supported CTE features</span></span>
<span data-ttu-id="df077-137">Wspólnych wyrażeniach tabel (wyrażeń CTE) są obsługiwane częściowo w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df077-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="df077-138">obecnie obsługiwane są następujące funkcje CTE Hello:</span><span class="sxs-lookup"><span data-stu-id="df077-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="df077-139">CTE można określić w instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="df077-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="df077-140">CTE można określić w instrukcji CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="df077-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="df077-141">CTE można określić w instrukcji tworzenia tabeli jako wybierz (CTAS).</span><span class="sxs-lookup"><span data-stu-id="df077-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="df077-142">CTE można określić w instrukcji tworzenia zdalnego tabeli jako wybierz (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="df077-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="df077-143">CTE można określić w instrukcji tworzenia zewnętrznego tabeli jako wybierz (CETAS).</span><span class="sxs-lookup"><span data-stu-id="df077-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="df077-144">Tabela zdalna mogą być przywoływane z CTE.</span><span class="sxs-lookup"><span data-stu-id="df077-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="df077-145">Tabeli zewnętrznej można odwoływać się z CTE.</span><span class="sxs-lookup"><span data-stu-id="df077-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="df077-146">Wiele definicji zapytania CTE można zdefiniować w CTE.</span><span class="sxs-lookup"><span data-stu-id="df077-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="df077-147">Ograniczenia CTE</span><span class="sxs-lookup"><span data-stu-id="df077-147">CTE Limitations</span></span>
<span data-ttu-id="df077-148">Wspólnego wyrażenia tabeli mają następujące ograniczenia z magazynu danych SQL, w tym:</span><span class="sxs-lookup"><span data-stu-id="df077-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="df077-149">CTE musi następować jednej instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="df077-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="df077-150">INSERT, UPDATE, DELETE i instrukcjach MERGE nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="df077-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="df077-151">Wspólne wyrażenie tabeli, zawierającą tooitself odwołań (cykliczne wspólne wyrażenie tabeli) nie jest obsługiwany (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="df077-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="df077-152">Określanie więcej niż jeden z klauzulą w CTE jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="df077-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="df077-153">Na przykład jeśli CTE_query_definition zawiera podzapytanie, że podzapytania nie może zawierać zagnieżdżoną z klauzulą definiujący CTE innego.</span><span class="sxs-lookup"><span data-stu-id="df077-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="df077-154">Nie można użyć klauzuli ORDER BY w hello CTE_query_definition, z wyjątkiem, gdy określono klauzulę TOP.</span><span class="sxs-lookup"><span data-stu-id="df077-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="df077-155">CTE jest używana w instrukcji, która jest częścią partii, instrukcja hello przed nią musi następować średnikiem.</span><span class="sxs-lookup"><span data-stu-id="df077-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="df077-156">W przypadku w instrukcjach przygotowane przez sp_prepare wspólnych wyrażeń tabel będą zachowywać się hello sam sposób jak inne instrukcji SELECT w PDW.</span><span class="sxs-lookup"><span data-stu-id="df077-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="df077-157">Jednak jeśli wspólnych wyrażeń tabel są używane jako część CETAS przygotowane przez sp_prepare, zachowanie hello może odroczyć z programu SQL Server i inne instrukcje PDW ze względu na sposób hello powiązania jest zaimplementowany dla sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="df077-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="df077-158">Wybierz OPCJĘ odwołania CTE wykorzystanie niewłaściwej kolumnie, która nie istnieje w CTE hello sp_prepare przechodzą bez wykrycia hello błąd, ale błąd hello zostanie zgłoszony podczas procedury składowanej sp_execute zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="df077-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="df077-159">Cyklicznych wspólnych wyrażeń tabel</span><span class="sxs-lookup"><span data-stu-id="df077-159">Recursive CTEs</span></span>
<span data-ttu-id="df077-160">Cyklicznych wspólnych wyrażeń tabel nie są obsługiwane w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df077-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="df077-161">Migracja Hello cykliczne CTE mogą być nieco złożone i proces najlepsze hello jest toobreak go do wielu kroków.</span><span class="sxs-lookup"><span data-stu-id="df077-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="df077-162">Zwykle można skorzystać z pętli i wypełniania tabeli tymczasowej jako iteracja tymczasowe kwerendy cykliczne hello.</span><span class="sxs-lookup"><span data-stu-id="df077-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="df077-163">Po zapełnieniu tabeli tymczasowej hello mogą następnie zwracać dane hello jako pojedynczy zestaw wyników.</span><span class="sxs-lookup"><span data-stu-id="df077-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="df077-164">Podejście podobne został użyty toosolve `GROUP BY WITH CUBE` w hello [Grupuj według klauzuli z pakietem zbiorczym / modułu / Ustawia opcje grupowania] [ group by clause with rollup / cube / grouping sets options] artykułu.</span><span class="sxs-lookup"><span data-stu-id="df077-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="df077-165">Nieobsługiwany system funkcji</span><span class="sxs-lookup"><span data-stu-id="df077-165">Unsupported system functions</span></span>
<span data-ttu-id="df077-166">Dostępne są także niektóre funkcje systemu, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="df077-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="df077-167">Hello podstawowe zwykle mogą być używane w magazynowania danych, należą:</span><span class="sxs-lookup"><span data-stu-id="df077-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="df077-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="df077-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="df077-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="df077-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="df077-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="df077-170">@@IDENTITY()</span></span>
* <span data-ttu-id="df077-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="df077-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="df077-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="df077-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="df077-173">ERROR_LINE() —</span><span class="sxs-lookup"><span data-stu-id="df077-173">ERROR_LINE()</span></span>

<span data-ttu-id="df077-174">Niektóre z tych problemów można pracować wokół.</span><span class="sxs-lookup"><span data-stu-id="df077-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="df077-175">@@ROWCOUNT obejście problemu</span><span class="sxs-lookup"><span data-stu-id="df077-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="df077-176">toowork wokół Brak obsługi @@ROWCOUNT, Tworzenie procedury przechowywanej, która będzie pobierać hello ostatniego liczba wierszy z sys.dm_pdw_request_steps, a następnie wykonaj `EXEC LastRowCount` po instrukcji DML.</span><span class="sxs-lookup"><span data-stu-id="df077-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="df077-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df077-177">Next steps</span></span>
<span data-ttu-id="df077-178">Aby uzyskać pełną listę wszystkich obsługiwanych instrukcje T-SQL, zobacz [tematy języka Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="df077-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
