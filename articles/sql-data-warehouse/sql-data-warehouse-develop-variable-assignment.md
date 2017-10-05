---
title: "Przypisz zmiennych w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="4dbd3-103">Przypisz zmiennych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4dbd3-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="4dbd3-104">Zmienne w usłudze SQL Data Warehouse są ustawiane przy użyciu `DECLARE` instrukcji lub `SET` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="4dbd3-105">Są spełnione wszystkie poniższe idealnie prawidłowe metody, aby ustawić wartość zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4dbd3-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="4dbd3-106">Ustawienia zmiennych z DECLARE</span><span class="sxs-lookup"><span data-stu-id="4dbd3-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="4dbd3-107">Inicjowanie zmiennych z DECLARE jest jednym z najbardziej elastycznym sposoby ustawiania wartości zmiennej w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="4dbd3-108">Umożliwia także DECLARE można ustawić więcej niż jedną zmienną w czasie.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="4dbd3-109">Nie można użyć `SELECT` lub `UPDATE` w tym celu:</span><span class="sxs-lookup"><span data-stu-id="4dbd3-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="4dbd3-110">Nie można zainicjować i użyć zmiennej w tej samej instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="4dbd3-111">Aby zilustrować punkt, w poniższym przykładzie jest **nie** jako @p1 jest zainicjowany i używany w tej samej instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="4dbd3-112">To spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="4dbd3-113">Ustawienie wartości z zestawu</span><span class="sxs-lookup"><span data-stu-id="4dbd3-113">Setting values with SET</span></span>
<span data-ttu-id="4dbd3-114">Zestaw to częsta metoda do ustawiania zmiennej.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="4dbd3-115">Poniższe przykłady są prawidłowe metody ustawienia zmiennej z zestawu:</span><span class="sxs-lookup"><span data-stu-id="4dbd3-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="4dbd3-116">Z zestawu jednej zmiennej można ustawić tylko w czasie.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="4dbd3-117">Jednak jak podano powyżej złożone operatory jest dopuszczalna.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="4dbd3-118">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="4dbd3-118">Limitations</span></span>
<span data-ttu-id="4dbd3-119">Wybierz lub aktualizacji nie można użyć zmiennej przypisania.</span><span class="sxs-lookup"><span data-stu-id="4dbd3-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbd3-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dbd3-120">Next steps</span></span>
<span data-ttu-id="4dbd3-121">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="4dbd3-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
