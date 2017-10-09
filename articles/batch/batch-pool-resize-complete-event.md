---
title: "AAA \"zdarzenie ukończenia zmiany rozmiaru puli partii zadań Azure | Dokumentacja firmy Microsoft\""
description: "Dokumentacja dotycząca puli partii resize zdarzenie ukończenia."
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Zdarzenie ukończenia zmiany rozmiaru puli

 To zdarzenie jest emitowany podczas zmiany rozmiaru puli zakończone lub nie powiodło się.

 Witaj poniższy przykład przedstawia hello treści zdarzenie ukończenia zmiany rozmiaru puli dla puli, zwiększyć rozmiar, która została ukończona pomyślnie.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Element|Typ|Uwagi|
|-------------|----------|-----------|
|id|Ciąg|Identyfikator Hello hello puli.|
|nodeDeallocationOption|Ciąg|Określa, kiedy węzły mogą zostać usunięte z puli hello, jeśli hello rozmiar puli będzie zmniejszany.<br /><br /> Możliwe wartości:<br /><br /> **requeue** — Przerwij wykonywane zadania i requeue je. Witaj zadania zostaną ponownie uruchomione, gdy zadanie hello jest włączone. Usuń węzły zaraz po zakończeniu zadania.<br /><br /> **przerwanie** — przerwania uruchomionych zadań. Witaj zadania nie zostaną ponownie uruchomione. Usuń węzły zaraz po zakończeniu zadania.<br /><br /> **taskcompletion** — Zezwalaj na aktualnie uruchomione zadania toocomplete. Nie planuj nowych zadań czasu oczekiwania. Usuń węzły, po zakończeniu wykonywania wszystkich zadań.<br /><br /> **Retaineddata** — Zezwalaj na aktualnie uruchomione zadania toocomplete, a następnie zaczekaj na zakończenie wszystkich zadań tooexpire okresów przechowywania danych. Nie planuj nowych zadań czasu oczekiwania. Usuń węzły, gdy wygasły wszystkich okresów przechowywania zadań.<br /><br /> Wartość domyślna Hello jest requeue.<br /><br /> Jeśli rozmiar puli hello jest zwiększenie, hello wartość zbyt**nieprawidłowy**.|
|currentDedicated|Int32|Witaj liczba węzłów obliczeniowych aktualnie przypisane toohello puli.|
|targetDedicated|Int32|Witaj liczba węzłów obliczeniowych, które są żądane hello puli.|
|enableAutoScale|wartość logiczna|Określa, czy rozmiar puli hello automatycznie dostosowuje się wraz z upływem czasu.|
|isAutoPool|wartość logiczna|Określa, czy pula hello został utworzony za pomocą mechanizmu AutoPool zadania.|
|startTime|Data i godzina|czas Hello zmiany rozmiaru puli hello jest uruchomiona.|
|endTime|Data i godzina|Witaj czasu zmiany rozmiaru puli hello ukończona.|
|resultCode|Ciąg|Zmień rozmiar Hello wynik hello.|
|resultMessage|Ciąg|Błąd podczas zmiany rozmiaru Hello zawiera szczegóły hello hello wyniku.<br /><br /> Jeśli rozmiar hello zakończone pomyślnie go stanów, które hello operacja powiodła się.|
