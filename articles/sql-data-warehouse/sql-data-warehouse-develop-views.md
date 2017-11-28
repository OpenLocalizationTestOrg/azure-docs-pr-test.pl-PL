---
title: "Korzystanie z widoków T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="d0a6c-103">Widoki w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0a6c-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="d0a6c-104">Widoki są szczególnie przydatne w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="d0a6c-105">Służy na kilka różnych sposobów poprawy jakości rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="d0a6c-106">W tym artykule omówiono sposób wzbogacić rozwiązania z widoków, a także ograniczenia, które należy wziąć pod uwagę kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a6c-107">Składnia `CREATE VIEW` nie została szczegółowo opisana w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="d0a6c-108">Zapoznaj się z [CREATE VIEW] [ CREATE VIEW] artykuł w witrynie MSDN, aby uzyskać informacje na ten.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="d0a6c-109">Abstrakcja architektury</span><span class="sxs-lookup"><span data-stu-id="d0a6c-109">Architectural abstraction</span></span>
<span data-ttu-id="d0a6c-110">Jest bardzo typowy wzorzec aplikacji do ponownego tworzenia tabel za pomocą tworzenia tabeli jako wybierz (CTAS) następuje zmiana nazwy wzorzec podczas ładowania danych obiektu.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="d0a6c-111">W poniższym przykładzie dodaje Data nowych rekordów do wymiaru daty.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="d0a6c-112">Należy zauważyć, jak nowy tabela, DimDate_New, jest najpierw utworzyć i następnie zmieniona na zastępowanie wersji oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

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

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="d0a6c-113">Jednak ta metoda może spowodować tabel znajdujących się i znika z punktu widzenia użytkownika, a także "Tabela nie istnieje" komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="d0a6c-114">Widoków może służyć do zapewnienia użytkowników z warstwą prezentacji spójne, przy jednoczesnym obiektów zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="d0a6c-115">Zapewniając użytkownikom dostęp do danych za pośrednictwem widoków, oznacza, że użytkownicy nie muszą mieć wgląd w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="d0a6c-116">Zapewnia to spójny interfejs użytkownika podczas sprawdzeniu, czy projektanci magazyn danych można rozwijać modelu danych i zmaksymalizować wydajność przy użyciu CTAS podczas procesu ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="d0a6c-117">Optymalizacja wydajności</span><span class="sxs-lookup"><span data-stu-id="d0a6c-117">Performance optimization</span></span>
<span data-ttu-id="d0a6c-118">Widoki można również używać do wymuszania zoptymalizowanych pod kątem wydajności sprzężenia między tabelami.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="d0a6c-119">Na przykład widoku można zastosować klucza dystrybucji nadmiarowe jako część łącząca kryteriów, aby zminimalizować przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="d0a6c-120">Inną zaletą widoku można wymusić określonej kwerendy lub łącząca wskazówki.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="d0a6c-121">Korzystanie z widoków w ten sposób gwarantuje, że sprzężenia zawsze są realizowane w sposób optymalny uniknięcie do zapamiętania prawidłowa konstrukcja dla ich sprzężeń przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="d0a6c-122">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d0a6c-122">Limitations</span></span>
<span data-ttu-id="d0a6c-123">Widoki w usłudze SQL Data Warehouse są tylko metadane.</span><span class="sxs-lookup"><span data-stu-id="d0a6c-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="d0a6c-124">W związku z tym nie dostępne są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="d0a6c-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="d0a6c-125">Nie jest dostępna opcja powiązanie schematu</span><span class="sxs-lookup"><span data-stu-id="d0a6c-125">There is no schema binding option</span></span>
* <span data-ttu-id="d0a6c-126">Nie można aktualizować tabel podstawowych za pośrednictwem widoku</span><span class="sxs-lookup"><span data-stu-id="d0a6c-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="d0a6c-127">Nie można tworzyć widoki w tabelach tymczasowych</span><span class="sxs-lookup"><span data-stu-id="d0a6c-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="d0a6c-128">Nie jest obsługiwane dla ROZWIJANIA / wskazówki NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="d0a6c-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="d0a6c-129">Brak widoków indeksowanych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0a6c-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0a6c-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0a6c-130">Next steps</span></span>
<span data-ttu-id="d0a6c-131">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="d0a6c-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="d0a6c-132">Aby uzyskać `CREATE VIEW` składni, zapoznaj się [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="d0a6c-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
