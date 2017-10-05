---
title: "Azure zdarzenia rozpoczęcia delete puli partii | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="6cad0-103">Zdarzenia rozpoczęcia delete puli</span><span class="sxs-lookup"><span data-stu-id="6cad0-103">Pool delete start event</span></span>

 <span data-ttu-id="6cad0-104">To zdarzenie jest emitowany, gdy rozpoczęto operację usuwania puli.</span><span class="sxs-lookup"><span data-stu-id="6cad0-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="6cad0-105">Usuwanie puli jest zdarzenie asynchroniczne, można oczekiwać, że zdarzenie ukończenia usuwania puli być emitowane po ukończeniu operacji usuwania.</span><span class="sxs-lookup"><span data-stu-id="6cad0-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="6cad0-106">W poniższym przykładzie przedstawiono treści zdarzenia rozpoczęcia delete puli.</span><span class="sxs-lookup"><span data-stu-id="6cad0-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="6cad0-107">Element</span><span class="sxs-lookup"><span data-stu-id="6cad0-107">Element</span></span>|<span data-ttu-id="6cad0-108">Typ</span><span class="sxs-lookup"><span data-stu-id="6cad0-108">Type</span></span>|<span data-ttu-id="6cad0-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6cad0-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="6cad0-110">id</span><span class="sxs-lookup"><span data-stu-id="6cad0-110">id</span></span>|<span data-ttu-id="6cad0-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6cad0-111">String</span></span>|<span data-ttu-id="6cad0-112">Identyfikator puli.</span><span class="sxs-lookup"><span data-stu-id="6cad0-112">The id of the pool.</span></span>|