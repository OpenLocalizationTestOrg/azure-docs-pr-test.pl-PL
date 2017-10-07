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
# <a name="batch-analytics"></a>Analizach wsadowych
Tematy Hello w analizach wsadowych zawierają informacje dotyczące hello zdarzenia i alerty dostępne dla zasobów usługi partii.

Zobacz [rejestrowania diagnostycznego partii zadań Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) Aby uzyskać więcej informacji o włączaniu i korzystanie z dzienników diagnostycznych partii.

## <a name="diagnostic-logs"></a>Dzienniki diagnostyczne

Witaj usługi partia zadań Azure emituje hello następujące zdarzenia dziennika diagnostycznego okres istnienia hello niektórych zasobów partii.

**Usługa dziennika zdarzeń**
* [Tworzenie puli](batch-pool-create-event.md)
* [Start usuwania puli](batch-pool-delete-start-event.md)
* [Usuwanie puli ukończone](batch-pool-delete-complete-event.md)
* [Początkowy rozmiar puli](batch-pool-resize-start-event.md)
* [Zmiana rozmiaru puli ukończone](batch-pool-resize-complete-event.md)
* [Rozpoczęcia zadania](batch-task-start-event.md)
* [Zadania ukończone](batch-task-complete-event.md)
* [Niepowodzenie zadania](batch-task-fail-event.md)