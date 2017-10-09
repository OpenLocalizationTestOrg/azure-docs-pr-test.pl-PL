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
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="2395f-103">W przypadku usługi SQL Data Warehouse pętle</span><span class="sxs-lookup"><span data-stu-id="2395f-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="2395f-104">Magazyn danych SQL obsługuje hello [podczas][podczas] pętli wielokrotnie wykonywania bloków instrukcji.</span><span class="sxs-lookup"><span data-stu-id="2395f-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="2395f-105">Operacja będzie kontynuowana dla tak długo, jak hello określone warunki są spełnione, lub do czasu hello kodu w szczególności kończy pętlę hello przy użyciu hello `BREAK` — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="2395f-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="2395f-106">Pętle są szczególnie użyteczne w przypadku zastępowania kursory zdefiniowany w języku SQL.</span><span class="sxs-lookup"><span data-stu-id="2395f-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="2395f-107">Na szczęście prawie wszystkie kursorów, które zostały napisane w języku SQL z hello szybkiego do przodu, odczytać tylko odmiany.</span><span class="sxs-lookup"><span data-stu-id="2395f-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="2395f-108">W związku z tym [podczas] pętle są doskonałą alternatywę, jeśli okaże się, że o tooreplace jeden.</span><span class="sxs-lookup"><span data-stu-id="2395f-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="2395f-109">Wykorzystanie pętle i zastępowanie kursory w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2395f-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="2395f-110">Jednak przed rozpoczęciem pracy w head należy poprosić samodzielnie hello następujące zapytania: "tego kursora można ponownie zapisywane toouse oparty zestaw operacji?".</span><span class="sxs-lookup"><span data-stu-id="2395f-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="2395f-111">W wielu przypadkach odpowiedzi hello będzie tak i jest często najlepszym podejściem hello.</span><span class="sxs-lookup"><span data-stu-id="2395f-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="2395f-112">Na podstawie operację często wykonuje się znacznie szybciej niż przy użyciu metody iteracyjne, wiersz po wierszu.</span><span class="sxs-lookup"><span data-stu-id="2395f-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="2395f-113">Przewijanie kursory tylko do odczytu mogą łatwo zastępowane z konstrukcji pętli.</span><span class="sxs-lookup"><span data-stu-id="2395f-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="2395f-114">Poniżej przedstawiono prosty przykład.</span><span class="sxs-lookup"><span data-stu-id="2395f-114">Below is a simple example.</span></span> <span data-ttu-id="2395f-115">Ten przykładowy kod aktualizuje statystyki powitania dla każdej tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="2395f-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="2395f-116">Przez Iterowanie po hello tabel w pętli hello możemy są możliwe tooexecute każde polecenie w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="2395f-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="2395f-117">Najpierw należy utworzyć tymczasowy tabelę zawierającą wiersz unikatowy numer tooidentify używane hello pojedyncze instrukcje:</span><span class="sxs-lookup"><span data-stu-id="2395f-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="2395f-118">Po drugie zainicjować hello zmienne wymagane tooperform hello pętli:</span><span class="sxs-lookup"><span data-stu-id="2395f-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="2395f-119">Teraz pętli instrukcje wykonywania jedną jednocześnie:</span><span class="sxs-lookup"><span data-stu-id="2395f-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="2395f-120">Na koniec porzucić hello Tabela tymczasowa utworzona w pierwszym kroku hello</span><span class="sxs-lookup"><span data-stu-id="2395f-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="2395f-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2395f-121">Next steps</span></span>
<span data-ttu-id="2395f-122">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="2395f-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[podczas]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
