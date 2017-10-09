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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Użyj etykiety tooinstrument zapytania w usłudze SQL Data Warehouse
Magazyn danych SQL obsługuje pojęcie o nazwie etykiety zapytania. Przed przejściem do dowolnej głębokości teraz wyglądać na przykład jeden:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Ten ostatni wiersz znaczniki hello ciąg "Moje zapytania etykieta" toohello zapytania. Jest to szczególnie przydatne, ponieważ etykieta hello jest zapytania mogli za pośrednictwem hello widoków DMV. To zapewnia tootrack mechanizmu, dół zapytania problem, a także toohelp identyfikują postęp do uruchomienia ETL.

Dobrym konwencji nazewnictwa korzystnie tutaj. Na przykład coś, takich jak "projektu: procedura: instrukcji: komentarz" byłaby pomocna toouniquely identyfikator kwerendy hello w między cały kod hello w kontroli źródła.

toosearch przez etykietę można użyć następującego zapytania, który używa hello hello dynamicznych widoków zarządzania:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Istotne jest zawijany nawiasy kwadratowe lub cudzysłowów wokół etykiety word hello podczas wykonywania zapytania. Etykieta jest słowem zastrzeżonym i będzie spowodowała błąd, jeśli nie został ograniczony.
> 
> 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
