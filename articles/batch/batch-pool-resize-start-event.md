---
title: "AAA \"zmiany rozmiaru puli partii zadań Azure rozpoczęcia zdarzenia | Dokumentacja firmy Microsoft\""
description: "Informacje dotyczące zmiany rozmiaru puli partii rozpoczęcia zdarzenia."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Zdarzenie rozpoczęcia zmiany rozmiaru puli

 To zdarzenie jest emitowany rozpoczęcie rozmiaru puli. Ponieważ zmiany rozmiaru puli hello jest zdarzenie asynchroniczne, może spodziewać się zakończeniu toobe zdarzenie ukończenia zmiany rozmiaru puli wysyłanego po hello operacja zmiany rozmiaru.

 Zmień rozmiar Hello poniższy przykład, że pokazuje hello treści zdarzenia rozpoczęcia zmiany rozmiaru puli do zmiany rozmiaru puli z 0 węzłów too2 ręcznego.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Element|Typ|Uwagi|
|-------------|----------|-----------|
|poolId|Ciąg|Identyfikator Hello hello puli.|
|nodeDeallocationOption|Ciąg|Określa, kiedy węzły mogą zostać usunięte z puli hello, jeśli hello rozmiar puli będzie zmniejszany.<br /><br /> Możliwe wartości:<br /><br /> **requeue** — Przerwij wykonywane zadania i requeue je. Witaj zadania zostaną ponownie uruchomione, gdy zadanie hello jest włączone. Usuń węzły zaraz po zakończeniu zadania.<br /><br /> **przerwanie** — przerwania uruchomionych zadań. Witaj zadania nie zostaną ponownie uruchomione. Usuń węzły zaraz po zakończeniu zadania.<br /><br /> **taskcompletion** — Zezwalaj na aktualnie uruchomione zadania toocomplete. Nie planuj nowych zadań czasu oczekiwania. Usuń węzły, po zakończeniu wykonywania wszystkich zadań.<br /><br /> **Retaineddata** — Zezwalaj na aktualnie uruchomione zadania toocomplete, a następnie zaczekaj na zakończenie wszystkich zadań tooexpire okresów przechowywania danych. Nie planuj nowych zadań czasu oczekiwania. Usuń węzły, gdy wygasły wszystkich okresów przechowywania zadań.<br /><br /> Wartość domyślna Hello jest requeue.<br /><br /> Jeśli rozmiar puli hello jest zwiększenie, hello wartość zbyt**nieprawidłowy**.|
|currentDedicated|Int32|Witaj liczba węzłów obliczeniowych aktualnie przypisane toohello puli.|
|targetDedicated|Int32|Witaj liczba węzłów obliczeniowych, które są żądane hello puli.|
|enableAutoScale|wartość logiczna|Określa, czy rozmiar puli hello automatycznie dostosowuje się wraz z upływem czasu.|
|isAutoPool|wartość logiczna|Speficies czy puli hello został utworzony za pomocą mechanizmu AutoPool zadania.|
