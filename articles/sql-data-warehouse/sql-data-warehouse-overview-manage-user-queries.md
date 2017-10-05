---
title: "Monitorowanie użytkownika zapytania w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Omówienie zagadnienia dotyczące najlepszych rozwiązań i zadania monitorowania kwerend użytkowników w usłudze Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="eae84-103">Monitor kwerend użytkowników w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="eae84-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="eae84-104">Omówienie zagadnienia dotyczące najlepszych rozwiązań i zadania monitorowania kwerend użytkowników w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="eae84-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="eae84-105">Kategoria</span><span class="sxs-lookup"><span data-stu-id="eae84-105">Category</span></span> | <span data-ttu-id="eae84-106">Zadania lub brany pod uwagę</span><span class="sxs-lookup"><span data-stu-id="eae84-106">Task or consideration</span></span> | <span data-ttu-id="eae84-107">Opis</span><span class="sxs-lookup"><span data-stu-id="eae84-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="eae84-108">Niska wydajność</span><span class="sxs-lookup"><span data-stu-id="eae84-108">Slow performance</span></span> |<span data-ttu-id="eae84-109">Znajdź zapytania długotrwałe użytkownika</span><span class="sxs-lookup"><span data-stu-id="eae84-109">Find a long-running user query</span></span> |<span data-ttu-id="eae84-110">[Znajdź kwerend][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="eae84-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="eae84-111">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="eae84-111">Concurrency</span></span> |<span data-ttu-id="eae84-112">Przydzielanie zasobów równoczesnych do zapytań użytkownika</span><span class="sxs-lookup"><span data-stu-id="eae84-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="eae84-113">[Zarządzanie współbieżności i obciążenia][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="eae84-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eae84-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eae84-114">Next steps</span></span>
<span data-ttu-id="eae84-115">Aby uzyskać więcej porad zarządzania, przejdź do [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="eae84-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
