---
title: "AAA \"zdarzenie ukończenia zadania partii zadań Azure | Dokumentacja firmy Microsoft\""
description: "Dokumentacja dotycząca zdarzenie ukończenia zadania wsadowego."
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
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a>Zdarzenie ukończenia zadania

 To zdarzenie jest emitowany po zakończeniu zadania, niezależnie od kodu zakończenia hello. To zdarzenie może być używane toodetermine hello czas trwania zadania, których są uruchomione zadanie hello i czy został on ponowione.


 Witaj poniższy przykład przedstawia hello treści zdarzenie ukończenia zadania.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|Identyfikator zadania|Ciąg|Identyfikator Hello hello zadania zawierające hello zadań.|
|id|Ciąg|Identyfikator Hello hello zadań.|
|taskType|Ciąg|Typ Hello hello zadań. Może to być "JobManager" i wskazujący, że jest to zadanie Menedżer zadania lub "User" i wskazujący, że nie jest zadanie Menedżer zadania. To zdarzenie nie jest emitowany zadanie przygotowanie zadania, zadania wersji lub uruchomienia zadania.|
|systemTaskVersion|Int32|Jest to licznik wewnętrzny ponownych prób hello zadania. Wewnętrznie hello usługa partia zadań. Spróbuj ponownie tooaccount zadania, dla przejściowych problemów. Te problemy mogą obejmować wewnętrzny planowania toorecover błędy lub prób z węzłami obliczeniowymi w złym stanie.|
|[nodeInfo](#nodeInfo)|Typ złożony|Zawiera informacje o węźle obliczeń hello, na które hello zadanie zostało wykonane.|
|[multiInstanceSettings](#multiInstanceSettings)|Typ złożony|Określa, że to zadanie hello jest zadaniem wielu wystąpieniach wymagające wielu węzłów obliczeniowych.  Zobacz [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) szczegółowe informacje.|
|[ograniczenia](#constraints)|Typ złożony|ograniczenia wykonywania Hello stosowane toothis zadań.|
|[executionInfo](#executionInfo)|Typ złożony|Zawiera informacje dotyczące wykonywania hello hello zadania.|

###  <a name="nodeInfo"></a>nodeInfo

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|poolId|Ciąg|Identyfikator Hello hello puli, na które hello zadanie zostało wykonane.|
|ID. węzła|Ciąg|Identyfikator Hello hello węzła, na którym hello zadanie zostało wykonane.|

###  <a name="multiInstanceSettings"></a>multiInstanceSettings

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|numberOfInstances|Int32|Liczba Hello wymagane przez zadanie hello węzłów obliczeniowych.|

###  <a name="constraints"></a>ograniczenia

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Witaj maksymalną liczbę razy hello zadanie może zostać podjęta ponowna próba wykonania. Hello usługa partia zadań ponawia zadanie, jeśli jego kod zakończenia jest różna od zera.<br /><br /> Należy pamiętać, że ta wartość określa, w szczególności hello liczby ponownych prób. Usługa partia zadań Hello ponowi zadania hello raz, a następnie może ponów się toothis limit. Na przykład hello maksymalnej liczby ponownych prób to 3, partii próbuje zadanie w górę too4 razy (jedna próba początkowej i 3 ponowne próby).<br /><br /> Jeśli hello maksymalna liczba ponowień to 0, hello usługa partia zadań nie ponów próbę wykonania zadania.<br /><br /> Jeśli hello maksymalna liczba ponowień to -1, usługa partia zadań hello ponowi próbę zadania bez ograniczeń.<br /><br /> Witaj, wartość domyślna to 0 (brak ponownych prób).|

###  <a name="executionInfo"></a>executionInfo

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|startTime|Data i godzina|czas uruchomienia zadania hello Hello. "Uruchomiona" odpowiada toohello **systemem** stanu, więc jeśli zadanie hello Określa pliki zasobów lub pakiety aplikacji, następnie czas rozpoczęcia hello odzwierciedla hello czas, w które zadanie hello Rozpoczęto pobieranie lub ich wdrażania.  Jeśli zadanie hello został ponownie uruchomiony lub ponowione, to hello ostatni czas, w którym zadanie hello rozpoczęcia działania.|
|endTime|Data i godzina|Witaj czas, w którym wykonano zadanie hello.|
|exitCode|Int32|Kod zakończenia Hello hello zadania.|
|retryCount|Int32|Witaj liczba zadań hello było ponawiane przez hello usługa partia zadań. Próba zostanie ponowiona Hello zadań, jeśli kończy działanie z kodem zakończenia różną od zera, zapasowej toohello określony MaxTaskRetryCount.|
|requeueCount|Int32|Witaj liczba zadań hello ma został umieszczony w kolejce przez usługi partia zadań hello hello wyniku żądania użytkownika.<br /><br /> Gdy usuwa użytkownika hello węzłów z pulę (przy zmianie rozmiaru lub zmniejszanie hello puli) lub gdy zadanie hello jest wyłączone, hello użytkownika można określić, czy uruchomienie zadań na węzłach hello jest umieszczony w kolejce do wykonania. Licznik ten uwzględnia śledzi, ile razy hello zadań ma zostać umieszczony w kolejce z tego względu.|
