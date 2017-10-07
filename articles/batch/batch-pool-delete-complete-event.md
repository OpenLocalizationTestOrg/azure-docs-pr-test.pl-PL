---
title: "AAA \"zdarzenie ukończenia usuwania puli partii zadań Azure | Dokumentacja firmy Microsoft\""
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="59fef-103">Zdarzenie ukończenia usuwania puli</span><span class="sxs-lookup"><span data-stu-id="59fef-103">Pool delete complete event</span></span>

 <span data-ttu-id="59fef-104">To zdarzenie jest emitowany po ukończeniu operacji usuwania puli.</span><span class="sxs-lookup"><span data-stu-id="59fef-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="59fef-105">Witaj poniższy przykład przedstawia hello treści puli zdarzenie ukończenia usuwania.</span><span class="sxs-lookup"><span data-stu-id="59fef-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="59fef-106">Element</span><span class="sxs-lookup"><span data-stu-id="59fef-106">Element</span></span>|<span data-ttu-id="59fef-107">Typ</span><span class="sxs-lookup"><span data-stu-id="59fef-107">Type</span></span>|<span data-ttu-id="59fef-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="59fef-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="59fef-109">id</span><span class="sxs-lookup"><span data-stu-id="59fef-109">id</span></span>|<span data-ttu-id="59fef-110">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59fef-110">String</span></span>|<span data-ttu-id="59fef-111">Identyfikator Hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="59fef-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="59fef-112">startTime</span><span class="sxs-lookup"><span data-stu-id="59fef-112">startTime</span></span>|<span data-ttu-id="59fef-113">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="59fef-113">DateTime</span></span>|<span data-ttu-id="59fef-114">czas Hello, usuń pulę hello uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="59fef-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="59fef-115">endTime</span><span class="sxs-lookup"><span data-stu-id="59fef-115">endTime</span></span>|<span data-ttu-id="59fef-116">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="59fef-116">DateTime</span></span>|<span data-ttu-id="59fef-117">Hello czasu puli hello Usuwanie zakończone.</span><span class="sxs-lookup"><span data-stu-id="59fef-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="59fef-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="59fef-118">Remarks</span></span>
<span data-ttu-id="59fef-119">Aby uzyskać więcej informacji na temat stanów i kody błędów dla operacji zmiany rozmiaru puli, zobacz [usunąć pulę z konta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="59fef-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>