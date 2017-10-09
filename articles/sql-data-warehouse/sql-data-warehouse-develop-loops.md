---
title: "aaaLeverage T-SQL wykonuje pętlę w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące języka Transact-SQL pętli i zastąpienie kursory w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>W przypadku usługi SQL Data Warehouse pętle
Magazyn danych SQL obsługuje hello [podczas][podczas] pętli wielokrotnie wykonywania bloków instrukcji. Operacja będzie kontynuowana dla tak długo, jak hello określone warunki są spełnione, lub do czasu hello kodu w szczególności kończy pętlę hello przy użyciu hello `BREAK` — słowo kluczowe. Pętle są szczególnie użyteczne w przypadku zastępowania kursory zdefiniowany w języku SQL. Na szczęście prawie wszystkie kursorów, które zostały napisane w języku SQL z hello szybkiego do przodu, odczytać tylko odmiany. W związku z tym [podczas] pętle są doskonałą alternatywę, jeśli okaże się, że o tooreplace jeden.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Wykorzystanie pętle i zastępowanie kursory w usłudze SQL Data Warehouse
Jednak przed rozpoczęciem pracy w head należy poprosić samodzielnie hello następujące zapytania: "tego kursora można ponownie zapisywane toouse oparty zestaw operacji?". W wielu przypadkach odpowiedzi hello będzie tak i jest często najlepszym podejściem hello. Na podstawie operację często wykonuje się znacznie szybciej niż przy użyciu metody iteracyjne, wiersz po wierszu.

Przewijanie kursory tylko do odczytu mogą łatwo zastępowane z konstrukcji pętli. Poniżej przedstawiono prosty przykład. Ten przykładowy kod aktualizuje statystyki powitania dla każdej tabeli w bazie danych hello. Przez Iterowanie po hello tabel w pętli hello możemy są możliwe tooexecute każde polecenie w sekwencji.

Najpierw należy utworzyć tymczasowy tabelę zawierającą wiersz unikatowy numer tooidentify używane hello pojedyncze instrukcje:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

Po drugie zainicjować hello zmienne wymagane tooperform hello pętli:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Teraz pętli instrukcje wykonywania jedną jednocześnie:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Na koniec porzucić hello Tabela tymczasowa utworzona w pierwszym kroku hello

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[podczas]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
