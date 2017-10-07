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
# <a name="pool-delete-complete-event"></a>Zdarzenie ukończenia usuwania puli

 To zdarzenie jest emitowany po ukończeniu operacji usuwania puli.

 Witaj poniższy przykład przedstawia hello treści puli zdarzenie ukończenia usuwania.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Element|Typ|Uwagi|
|-------------|----------|-----------|
|id|Ciąg|Identyfikator Hello hello puli.|
|startTime|Data i godzina|czas Hello, usuń pulę hello uruchomienia.|
|endTime|Data i godzina|Hello czasu puli hello Usuwanie zakończone.|

## <a name="remarks"></a>Uwagi
Aby uzyskać więcej informacji na temat stanów i kody błędów dla operacji zmiany rozmiaru puli, zobacz [usunąć pulę z konta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).