---
title: "aaaResources związane z opracowywaniem hurtowni danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Pojęcia dotyczące programowania, decyzji projektowych i zalecenia dotyczące technik programowania dla usługi SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="5685c-103">Decyzje dotyczące projektu i technik programowania dla usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5685c-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="5685c-104">Zapoznaj się z za pośrednictwem tych artykułach programowanie toobetter zrozumienie kluczowych decyzji projektowych, zalecenia i technik programowania dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5685c-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="5685c-105">Kluczowych decyzji projektowych</span><span class="sxs-lookup"><span data-stu-id="5685c-105">Key design decisions</span></span>
<span data-ttu-id="5685c-106">Witaj następujące artykuły omówiono niektóre hello podstawowych pojęć i decyzje dotyczące projektu do tworzenia aplikacji hello magazynu danych rozproszonych za pomocą usługi SQL Data Warehouse będzie toounderstand:</span><span class="sxs-lookup"><span data-stu-id="5685c-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="5685c-107">[połączenia][connections]</span><span class="sxs-lookup"><span data-stu-id="5685c-107">[connections][connections]</span></span>
* <span data-ttu-id="5685c-108">[Współbieżność][concurrency]</span><span class="sxs-lookup"><span data-stu-id="5685c-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="5685c-109">[transakcje][transactions]</span><span class="sxs-lookup"><span data-stu-id="5685c-109">[transactions][transactions]</span></span>
* <span data-ttu-id="5685c-110">[schematy zdefiniowane przez użytkownika][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="5685c-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="5685c-111">[Dystrybucja tabeli][table distribution]</span><span class="sxs-lookup"><span data-stu-id="5685c-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="5685c-112">[indeksy tabel][table indexes]</span><span class="sxs-lookup"><span data-stu-id="5685c-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="5685c-113">[partycje tabeli][table partitions]</span><span class="sxs-lookup"><span data-stu-id="5685c-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="5685c-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="5685c-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="5685c-115">[statystyki][statistics]</span><span class="sxs-lookup"><span data-stu-id="5685c-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="5685c-116">Zalecenia dotyczące tworzenia i technik programowania</span><span class="sxs-lookup"><span data-stu-id="5685c-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="5685c-117">Te artykuły wyróżnianie określonych technik programowania, wskazówki i zalecenia dotyczące Tworzenie magazynu danych SQL:</span><span class="sxs-lookup"><span data-stu-id="5685c-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="5685c-118">[procedury składowane][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="5685c-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="5685c-119">[etykiety][labels]</span><span class="sxs-lookup"><span data-stu-id="5685c-119">[labels][labels]</span></span>
* <span data-ttu-id="5685c-120">[Widoki][views]</span><span class="sxs-lookup"><span data-stu-id="5685c-120">[views][views]</span></span>
* <span data-ttu-id="5685c-121">[tabele tymczasowe][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="5685c-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="5685c-122">[dynamiczne SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="5685c-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="5685c-123">[tworzenie pętli][looping]</span><span class="sxs-lookup"><span data-stu-id="5685c-123">[looping][looping]</span></span>
* <span data-ttu-id="5685c-124">[Grupuj według opcje][group by options]</span><span class="sxs-lookup"><span data-stu-id="5685c-124">[group by options][group by options]</span></span>
* <span data-ttu-id="5685c-125">[Przypisanie zmiennej][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="5685c-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="5685c-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5685c-126">Next steps</span></span>
<span data-ttu-id="5685c-127">Gdy nastąpiło za pośrednictwem artykuły programowanie hello zapoznaj się za pośrednictwem hello [odwołania Transact-SQL] [ Transact-SQL reference] strony, aby uzyskać więcej informacji na powitania obsługiwana składnia SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5685c-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
