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
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="cadb4-103">Przypisz zmiennych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cadb4-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="cadb4-104">Zmienne w usłudze SQL Data Warehouse są ustawiane przy użyciu hello `DECLARE` instrukcji lub hello `SET` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="cadb4-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="cadb4-105">Wszystkie z następujących hello są doskonale prawidłowe metody tooset wartość zmiennej:</span><span class="sxs-lookup"><span data-stu-id="cadb4-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="cadb4-106">Ustawienia zmiennych z DECLARE</span><span class="sxs-lookup"><span data-stu-id="cadb4-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="cadb4-107">Inicjowanie zmiennych z DECLARE jest jednym z najbardziej elastycznym hello tooset sposoby wartość zmiennej w magazynie danych programu SQL.</span><span class="sxs-lookup"><span data-stu-id="cadb4-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="cadb4-108">Umożliwia także DECLARE tooset więcej niż jedną zmienną w czasie.</span><span class="sxs-lookup"><span data-stu-id="cadb4-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="cadb4-109">Nie można użyć `SELECT` lub `UPDATE` toodo to:</span><span class="sxs-lookup"><span data-stu-id="cadb4-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="cadb4-110">Nie można zainicjować i użyć zmiennej w hello tej samej instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="cadb4-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="cadb4-111">Poniższy przykład hello punktu hello tooillustrate jest **nie** jako @p1 jest zainicjowany i używane w hello tej samej instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="cadb4-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="cadb4-112">To spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="cadb4-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="cadb4-113">Ustawienie wartości z zestawu</span><span class="sxs-lookup"><span data-stu-id="cadb4-113">Setting values with SET</span></span>
<span data-ttu-id="cadb4-114">Zestaw to częsta metoda do ustawiania zmiennej.</span><span class="sxs-lookup"><span data-stu-id="cadb4-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="cadb4-115">Poniższe przykłady hello są prawidłowe metody ustawienia zmiennej z ZESTAWEM:</span><span class="sxs-lookup"><span data-stu-id="cadb4-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="cadb4-116">Z zestawu jednej zmiennej można ustawić tylko w czasie.</span><span class="sxs-lookup"><span data-stu-id="cadb4-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="cadb4-117">Jednak jak podano powyżej złożone operatory jest dopuszczalna.</span><span class="sxs-lookup"><span data-stu-id="cadb4-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="cadb4-118">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="cadb4-118">Limitations</span></span>
<span data-ttu-id="cadb4-119">Wybierz lub aktualizacji nie można użyć zmiennej przypisania.</span><span class="sxs-lookup"><span data-stu-id="cadb4-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cadb4-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cadb4-120">Next steps</span></span>
<span data-ttu-id="cadb4-121">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="cadb4-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
