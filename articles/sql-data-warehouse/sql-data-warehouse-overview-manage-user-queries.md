---
title: "aaaMonitor kwerend użytkowników w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Omówienie zagadnień hello, najlepszych rozwiązań i zadania monitorowania kwerend użytkowników w usłudze Azure SQL Data Warehouse"
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
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="81dbb-103">Monitor kwerend użytkowników w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="81dbb-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="81dbb-104">Omówienie zagadnień hello, najlepszych rozwiązań i zadania monitorowania kwerend użytkowników w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81dbb-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="81dbb-105">Kategoria</span><span class="sxs-lookup"><span data-stu-id="81dbb-105">Category</span></span> | <span data-ttu-id="81dbb-106">Zadania lub brany pod uwagę</span><span class="sxs-lookup"><span data-stu-id="81dbb-106">Task or consideration</span></span> | <span data-ttu-id="81dbb-107">Opis</span><span class="sxs-lookup"><span data-stu-id="81dbb-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="81dbb-108">Niska wydajność</span><span class="sxs-lookup"><span data-stu-id="81dbb-108">Slow performance</span></span> |<span data-ttu-id="81dbb-109">Znajdź zapytania długotrwałe użytkownika</span><span class="sxs-lookup"><span data-stu-id="81dbb-109">Find a long-running user query</span></span> |<span data-ttu-id="81dbb-110">[Znajdź kwerend][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="81dbb-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="81dbb-111">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="81dbb-111">Concurrency</span></span> |<span data-ttu-id="81dbb-112">Przydzielanie zasobów równoczesnych zapytań toouser</span><span class="sxs-lookup"><span data-stu-id="81dbb-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="81dbb-113">[Zarządzanie współbieżności i obciążenia][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="81dbb-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="81dbb-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81dbb-114">Next steps</span></span>
<span data-ttu-id="81dbb-115">Aby uzyskać więcej porad zarządzania, odwiedź toohello [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="81dbb-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
