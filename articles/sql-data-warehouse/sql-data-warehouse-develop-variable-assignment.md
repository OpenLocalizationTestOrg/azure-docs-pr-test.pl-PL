---
title: "zmienne aaaAssign w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące przypisywania zmienne języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Przypisz zmiennych w usłudze SQL Data Warehouse
Zmienne w usłudze SQL Data Warehouse są ustawiane przy użyciu hello `DECLARE` instrukcji lub hello `SET` instrukcji.

Wszystkie z następujących hello są doskonale prawidłowe metody tooset wartość zmiennej:

## <a name="setting-variables-with-declare"></a>Ustawienia zmiennych z DECLARE
Inicjowanie zmiennych z DECLARE jest jednym z najbardziej elastycznym hello tooset sposoby wartość zmiennej w magazynie danych programu SQL.

```sql
DECLARE @v  int = 0
;
```

Umożliwia także DECLARE tooset więcej niż jedną zmienną w czasie. Nie można użyć `SELECT` lub `UPDATE` toodo to:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Nie można zainicjować i użyć zmiennej w hello tej samej instrukcji DECLARE. Poniższy przykład hello punktu hello tooillustrate jest **nie** jako @p1 jest zainicjowany i używane w hello tej samej instrukcji DECLARE. To spowoduje błąd.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Ustawienie wartości z zestawu
Zestaw to częsta metoda do ustawiania zmiennej.

Poniższe przykłady hello są prawidłowe metody ustawienia zmiennej z ZESTAWEM:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

Z zestawu jednej zmiennej można ustawić tylko w czasie. Jednak jak podano powyżej złożone operatory jest dopuszczalna.

## <a name="limitations"></a>Ograniczenia
Wybierz lub aktualizacji nie można użyć zmiennej przypisania.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
