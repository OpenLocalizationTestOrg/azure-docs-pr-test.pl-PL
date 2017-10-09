---
title: "aaaUse etykiet tooinstrument zapytania w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z etykiet tooinstrument zapytania w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
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
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="1cc73-103">Użyj etykiety tooinstrument zapytania w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1cc73-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="1cc73-104">Magazyn danych SQL obsługuje pojęcie o nazwie etykiety zapytania.</span><span class="sxs-lookup"><span data-stu-id="1cc73-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="1cc73-105">Przed przejściem do dowolnej głębokości teraz wyglądać na przykład jeden:</span><span class="sxs-lookup"><span data-stu-id="1cc73-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="1cc73-106">Ten ostatni wiersz znaczniki hello ciąg "Moje zapytania etykieta" toohello zapytania.</span><span class="sxs-lookup"><span data-stu-id="1cc73-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="1cc73-107">Jest to szczególnie przydatne, ponieważ etykieta hello jest zapytania mogli za pośrednictwem hello widoków DMV.</span><span class="sxs-lookup"><span data-stu-id="1cc73-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="1cc73-108">To zapewnia tootrack mechanizmu, dół zapytania problem, a także toohelp identyfikują postęp do uruchomienia ETL.</span><span class="sxs-lookup"><span data-stu-id="1cc73-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="1cc73-109">Dobrym konwencji nazewnictwa korzystnie tutaj.</span><span class="sxs-lookup"><span data-stu-id="1cc73-109">A good naming convention really helps here.</span></span> <span data-ttu-id="1cc73-110">Na przykład coś, takich jak "projektu: procedura: instrukcji: komentarz" byłaby pomocna toouniquely identyfikator kwerendy hello w między cały kod hello w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="1cc73-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="1cc73-111">toosearch przez etykietę można użyć następującego zapytania, który używa hello hello dynamicznych widoków zarządzania:</span><span class="sxs-lookup"><span data-stu-id="1cc73-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="1cc73-112">Istotne jest zawijany nawiasy kwadratowe lub cudzysłowów wokół etykiety word hello podczas wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="1cc73-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="1cc73-113">Etykieta jest słowem zastrzeżonym i będzie spowodowała błąd, jeśli nie został ograniczony.</span><span class="sxs-lookup"><span data-stu-id="1cc73-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1cc73-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cc73-114">Next steps</span></span>
<span data-ttu-id="1cc73-115">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="1cc73-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
