---
title: aaaAzure analizach wsadowych | Dokumentacja firmy Microsoft
description: "Odwołanie do analizy partii zadań Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="e9c5c-103">Analizach wsadowych</span><span class="sxs-lookup"><span data-stu-id="e9c5c-103">Batch Analytics</span></span>
<span data-ttu-id="e9c5c-104">Tematy Hello w analizach wsadowych zawierają informacje dotyczące hello zdarzenia i alerty dostępne dla zasobów usługi partii.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="e9c5c-105">Zobacz [rejestrowania diagnostycznego partii zadań Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) Aby uzyskać więcej informacji o włączaniu i korzystanie z dzienników diagnostycznych partii.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="e9c5c-106">Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="e9c5c-106">Diagnostic logs</span></span>

<span data-ttu-id="e9c5c-107">Witaj usługi partia zadań Azure emituje hello następujące zdarzenia dziennika diagnostycznego okres istnienia hello niektórych zasobów partii.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="e9c5c-108">**Usługa dziennika zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-108">**Service Log events**</span></span>
* [<span data-ttu-id="e9c5c-109">Tworzenie puli</span><span class="sxs-lookup"><span data-stu-id="e9c5c-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="e9c5c-110">Start usuwania puli</span><span class="sxs-lookup"><span data-stu-id="e9c5c-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="e9c5c-111">Usuwanie puli ukończone</span><span class="sxs-lookup"><span data-stu-id="e9c5c-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="e9c5c-112">Początkowy rozmiar puli</span><span class="sxs-lookup"><span data-stu-id="e9c5c-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="e9c5c-113">Zmiana rozmiaru puli ukończone</span><span class="sxs-lookup"><span data-stu-id="e9c5c-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="e9c5c-114">Rozpoczęcia zadania</span><span class="sxs-lookup"><span data-stu-id="e9c5c-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="e9c5c-115">Zadania ukończone</span><span class="sxs-lookup"><span data-stu-id="e9c5c-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="e9c5c-116">Niepowodzenie zadania</span><span class="sxs-lookup"><span data-stu-id="e9c5c-116">Task fail</span></span>](batch-task-fail-event.md)