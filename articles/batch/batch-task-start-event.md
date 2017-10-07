---
title: "AAA \"zdarzenia uruchamiania zadań partii zadań Azure | Dokumentacja firmy Microsoft\""
description: "Odwołanie do zadania wsadowego rozpoczęcia zdarzenia."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Zdarzenia uruchamiania zadań

 To zdarzenie jest emitowany po zadania zaplanowane toostart w węźle obliczeń przez hello harmonogram. Należy pamiętać, że jeśli zadanie hello jest ponowione lub umieszczony w kolejce to zdarzenie będzie obliczanie ponownie hello tego samego zadania, ale hello liczba ponownych prób i zadań w systemie będą odpowiednio aktualizowane.


 Witaj poniższy przykład przedstawia hello treści zdarzenia uruchamiania zadań.

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
        "retryCount": 0
    }
}
```

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|Identyfikator zadania|Ciąg|Identyfikator Hello hello zadania zawierające hello zadań.|
|id|Ciąg|Identyfikator Hello hello zadań.|
|taskType|Ciąg|Typ Hello hello zadań. Może to być "JobManager" i wskazujący, że jest to zadanie Menedżer zadania lub "User" i wskazujący, że nie jest zadanie Menedżer zadania.|
|systemTaskVersion|Int32|Jest to licznik wewnętrzny ponownych prób hello zadania. Wewnętrznie hello usługa partia zadań. Spróbuj ponownie tooaccount zadania, dla przejściowych problemów. Te problemy mogą obejmować wewnętrzny planowania toorecover błędy lub prób z węzłami obliczeniowymi w złym stanie.|
|[nodeInfo](#nodeInfo)|Typ złożony|Zawiera informacje o węźle obliczeń hello, na które hello zadanie zostało wykonane.|
|[multiInstanceSettings](#multiInstanceSettings)|Typ złożony|Określa, że to zadanie hello jest wiele wystąpień zadań wymagających wielu węzłów obliczeniowych.  Zobacz [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) szczegółowe informacje.|
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
|numberOfInstances|int|Liczba Hello wymagane przez zadanie hello węzłów obliczeniowych.|

###  <a name="constraints"></a>ograniczenia

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Witaj maksymalną liczbę razy hello zadanie może zostać podjęta ponowna próba wykonania. Hello usługa partia zadań ponawia zadanie, jeśli jego kod zakończenia jest różna od zera.<br /><br /> Należy pamiętać, że ta wartość określa, w szczególności hello liczby ponownych prób. Usługa partia zadań Hello ponowi zadania hello raz, a następnie może ponów się toothis limit. Na przykład hello maksymalnej liczby ponownych prób to 3, partii próbuje zadanie w górę too4 razy (jedna próba początkowej i 3 ponowne próby).<br /><br /> Jeśli hello maksymalna liczba ponowień to 0, hello usługa partia zadań nie ponów próbę wykonania zadania.<br /><br /> Jeśli hello maksymalna liczba ponowień to -1, usługa partia zadań hello ponowi próbę zadania bez ograniczeń.<br /><br /> Witaj, wartość domyślna to 0 (brak ponownych prób).|

###  <a name="executionInfo"></a>executionInfo

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|retryCount|Int32|Witaj liczba zadań hello było ponawiane przez hello usługa partia zadań. zadanie Hello jest podjęta, jeśli kończy działanie z kodem zakończenia różną od zera, zapasowej toohello określony MaxTaskRetryCount|
