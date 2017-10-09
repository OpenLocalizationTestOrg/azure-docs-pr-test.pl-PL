---
title: "AAA \"zdarzenia rozpoczęcia delete puli partii zadań Azure | Dokumentacja firmy Microsoft\""
description: "Odwołanie do usunięcia puli partii rozpoczęcia zdarzenia."
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="38623-103">Zdarzenia rozpoczęcia delete puli</span><span class="sxs-lookup"><span data-stu-id="38623-103">Pool delete start event</span></span>

 <span data-ttu-id="38623-104">To zdarzenie jest emitowany, gdy rozpoczęto operację usuwania puli.</span><span class="sxs-lookup"><span data-stu-id="38623-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="38623-105">Usuń pulę hello jest zdarzenie asynchroniczne, może spodziewać się zakończeniu toobe zdarzenie ukończenia usuwania puli wysyłanego, gdy operacja usuwania hello.</span><span class="sxs-lookup"><span data-stu-id="38623-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="38623-106">Witaj poniższy przykład przedstawia hello treści zdarzenia rozpoczęcia delete puli.</span><span class="sxs-lookup"><span data-stu-id="38623-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="38623-107">Element</span><span class="sxs-lookup"><span data-stu-id="38623-107">Element</span></span>|<span data-ttu-id="38623-108">Typ</span><span class="sxs-lookup"><span data-stu-id="38623-108">Type</span></span>|<span data-ttu-id="38623-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="38623-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="38623-110">id</span><span class="sxs-lookup"><span data-stu-id="38623-110">id</span></span>|<span data-ttu-id="38623-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38623-111">String</span></span>|<span data-ttu-id="38623-112">Identyfikator Hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="38623-112">hello id of hello pool.</span></span>|
