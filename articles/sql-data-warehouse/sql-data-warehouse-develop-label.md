---
title: "Korzystanie z etykiet do dokumentu zapytania w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z etykiet do dokumentu zapytania w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="a89db-103">Korzystanie z etykiet do dokumentu zapytania w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a89db-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="a89db-104">Magazyn danych SQL obsługuje pojęcie o nazwie etykiety zapytania.</span><span class="sxs-lookup"><span data-stu-id="a89db-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="a89db-105">Przed przejściem do dowolnej głębokości teraz wyglądać na przykład jeden:</span><span class="sxs-lookup"><span data-stu-id="a89db-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="a89db-106">Ten ostatni wiersz znaczniki ciąg "Moje zapytania etykieta" w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="a89db-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="a89db-107">Jest to szczególnie przydatne, ponieważ etykieta to zapytanie może przy użyciu widoków DMV.</span><span class="sxs-lookup"><span data-stu-id="a89db-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="a89db-108">To zapewnia mechanizm do śledzenia zapytań problem, a także ułatwiają identyfikację postęp do uruchomienia ETL.</span><span class="sxs-lookup"><span data-stu-id="a89db-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="a89db-109">Dobrym konwencji nazewnictwa korzystnie tutaj.</span><span class="sxs-lookup"><span data-stu-id="a89db-109">A good naming convention really helps here.</span></span> <span data-ttu-id="a89db-110">Na przykład coś, takich jak "projektu: procedura: instrukcja: komentarz" byłaby pomocna do jednoznacznej identyfikacji zapytania w między cały kod w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a89db-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="a89db-111">Aby przeprowadzić wyszukiwanie według etykiety można Użyj następującego zapytania, który używa dynamicznych widoków zarządzania:</span><span class="sxs-lookup"><span data-stu-id="a89db-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="a89db-112">Istotne jest zawijany nawiasy kwadratowe lub cudzysłowów wokół etykiety word podczas wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="a89db-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="a89db-113">Etykieta jest słowem zastrzeżonym i będzie spowodowała błąd, jeśli nie został ograniczony.</span><span class="sxs-lookup"><span data-stu-id="a89db-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a89db-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a89db-114">Next steps</span></span>
<span data-ttu-id="a89db-115">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="a89db-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
