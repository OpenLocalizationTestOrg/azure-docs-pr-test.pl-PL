---
title: "Widoki aaaUsing T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z widoków języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="e9bf9-103">Widoki w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e9bf9-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="e9bf9-104">Widoki są szczególnie przydatne w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="e9bf9-105">Służy na kilka różnych sposobów tooimprove hello jakości rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="e9bf9-106">W tym artykule omówiono kilka przykładów sposobu tooenrich rozwiązania z widoków, a także ograniczenia hello, które wymagają toobe traktowane jako.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="e9bf9-107">Składnia `CREATE VIEW` nie została szczegółowo opisana w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="e9bf9-108">Zobacz toohello [CREATE VIEW] [ CREATE VIEW] artykuł w witrynie MSDN, aby uzyskać informacje na ten.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="e9bf9-109">Abstrakcja architektury</span><span class="sxs-lookup"><span data-stu-id="e9bf9-109">Architectural abstraction</span></span>
<span data-ttu-id="e9bf9-110">Bardzo typowy wzorzec aplikacji jest toore — Tworzenie tabel za pomocą tworzenia tabeli jako wybierz (CTAS) następuje zmiana nazwy wzorzec podczas ładowania danych obiektu.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="e9bf9-111">w poniższym przykładzie Hello dodaje wymiaru daty tooa rekordów nową datą.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="e9bf9-112">Należy zwrócić uwagę, jak nowy tabela, DimDate_New, utworzenia i zmienić nazwy oryginalnej wersji hello tooreplace hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="e9bf9-113">Jednak ta metoda może spowodować tabel znajdujących się i znika z punktu widzenia użytkownika, a także "Tabela nie istnieje" komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="e9bf9-114">Widoki może być używane tooprovide użytkowników z warstwą prezentacji spójne przy jednoczesnym obiektów hello zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="e9bf9-115">Zapewniając użytkownikom dostęp do danych toohello za pośrednictwem widoków, oznacza, że użytkownicy nie muszą toohave widoczność hello tabel.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="e9bf9-116">Zapewnia to spójny interfejs użytkownika przy jednoczesnym zapewnieniu projektanci magazynu danych hello może rozwijać hello modelu danych i zmaksymalizować wydajność przy użyciu CTAS podczas procesu ładowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="e9bf9-117">Optymalizacja wydajności</span><span class="sxs-lookup"><span data-stu-id="e9bf9-117">Performance optimization</span></span>
<span data-ttu-id="e9bf9-118">Widoki mogą być również wykorzystywane tooenforce zoptymalizowanych pod kątem wydajności sprzężenia między tabelami.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="e9bf9-119">Na przykład widoku można zastosować klucza dystrybucji nadmiarowe jako część hello dołączenie przenoszenia danych toominimize kryteriów.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="e9bf9-120">Inną zaletą widok może być tooforce określonej kwerendy lub łącząca wskazówki.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="e9bf9-121">Korzystanie z widoków w ten sposób gwarantuje, że sprzężenia zawsze są realizowane w sposób optymalny unikanie hello potrzebę prawidłowa konstrukcja hello tooremember użytkowników dla ich sprzężeń.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="e9bf9-122">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="e9bf9-122">Limitations</span></span>
<span data-ttu-id="e9bf9-123">Widoki w usłudze SQL Data Warehouse są tylko metadane.</span><span class="sxs-lookup"><span data-stu-id="e9bf9-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="e9bf9-124">W związku z tym hello następujące opcje nie są dostępne:</span><span class="sxs-lookup"><span data-stu-id="e9bf9-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="e9bf9-125">Nie jest dostępna opcja powiązanie schematu</span><span class="sxs-lookup"><span data-stu-id="e9bf9-125">There is no schema binding option</span></span>
* <span data-ttu-id="e9bf9-126">Nie można aktualizować tabel podstawowych za pośrednictwem widoku hello</span><span class="sxs-lookup"><span data-stu-id="e9bf9-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="e9bf9-127">Nie można tworzyć widoki w tabelach tymczasowych</span><span class="sxs-lookup"><span data-stu-id="e9bf9-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="e9bf9-128">Nie jest obsługiwane dla hello ROZWIJANIA / wskazówki NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="e9bf9-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="e9bf9-129">Brak widoków indeksowanych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e9bf9-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9bf9-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9bf9-130">Next steps</span></span>
<span data-ttu-id="e9bf9-131">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e9bf9-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="e9bf9-132">Aby uzyskać `CREATE VIEW` składni można znaleźć zbyt[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="e9bf9-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
