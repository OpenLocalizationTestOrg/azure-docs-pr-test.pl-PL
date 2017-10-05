---
title: "Zdarzenie ukończenia usuwania Azure puli partii | Dokumentacja firmy Microsoft"
description: "Dokumentacja dotycząca puli partii usunąć zdarzenie ukończenia."
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="4fcf2-103">Zdarzenie ukończenia usuwania puli</span><span class="sxs-lookup"><span data-stu-id="4fcf2-103">Pool delete complete event</span></span>

 <span data-ttu-id="4fcf2-104">To zdarzenie jest emitowany po ukończeniu operacji usuwania puli.</span><span class="sxs-lookup"><span data-stu-id="4fcf2-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="4fcf2-105">W poniższym przykładzie przedstawiono treści puli zdarzenie ukończenia usuwania.</span><span class="sxs-lookup"><span data-stu-id="4fcf2-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="4fcf2-106">Element</span><span class="sxs-lookup"><span data-stu-id="4fcf2-106">Element</span></span>|<span data-ttu-id="4fcf2-107">Typ</span><span class="sxs-lookup"><span data-stu-id="4fcf2-107">Type</span></span>|<span data-ttu-id="4fcf2-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4fcf2-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="4fcf2-109">id</span><span class="sxs-lookup"><span data-stu-id="4fcf2-109">id</span></span>|<span data-ttu-id="4fcf2-110">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4fcf2-110">String</span></span>|<span data-ttu-id="4fcf2-111">Identyfikator puli.</span><span class="sxs-lookup"><span data-stu-id="4fcf2-111">The id of the pool.</span></span>|
|<span data-ttu-id="4fcf2-112">startTime</span><span class="sxs-lookup"><span data-stu-id="4fcf2-112">startTime</span></span>|<span data-ttu-id="4fcf2-113">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="4fcf2-113">DateTime</span></span>|<span data-ttu-id="4fcf2-114">Czas, usuń pulę uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4fcf2-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="4fcf2-115">wartość endTime</span><span class="sxs-lookup"><span data-stu-id="4fcf2-115">endTime</span></span>|<span data-ttu-id="4fcf2-116">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="4fcf2-116">DateTime</span></span>|<span data-ttu-id="4fcf2-117">Czas usunąć pulę ukończone.</span><span class="sxs-lookup"><span data-stu-id="4fcf2-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="4fcf2-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4fcf2-118">Remarks</span></span>
<span data-ttu-id="4fcf2-119">Aby uzyskać więcej informacji na temat stanów i kody błędów dla operacji zmiany rozmiaru puli, zobacz [usunąć pulę z konta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="4fcf2-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>