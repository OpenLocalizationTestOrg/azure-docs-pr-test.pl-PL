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
# <a name="pool-delete-start-event"></a>Zdarzenia rozpoczęcia delete puli

 To zdarzenie jest emitowany, gdy rozpoczęto operację usuwania puli. Usuń pulę hello jest zdarzenie asynchroniczne, może spodziewać się zakończeniu toobe zdarzenie ukończenia usuwania puli wysyłanego, gdy operacja usuwania hello.

 Witaj poniższy przykład przedstawia hello treści zdarzenia rozpoczęcia delete puli.

```
{
    "id": "myPool1"
}
```

|Element|Typ|Uwagi|
|-------------|----------|-----------|
|id|Ciąg|Identyfikator Hello hello puli.|
