---
title: "AAA \"partii zadań Azure obliczeniowe zmiennych środowiskowych węzła | Dokumentacja firmy Microsoft\""
description: "Obliczenia bazy danych odwołanie do zmiennej środowiskowej węzła dla analizach wsadowych Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Zmienne środowiskowe węzła obliczeń platformy Azure partii
Witaj [usługi partia zadań Azure](https://azure.microsoft.com/services/batch/) ustawia hello następujące zmienne środowiskowe w węzłach obliczeniowych. Możesz odwoływać się do tych zmiennych środowiskowych w wiersze polecenia zadań i programy hello i skrypty uruchamiane przez hello wiersze polecenia.

Aby uzyskać dodatkowe informacje dotyczące używania zmiennych środowiskowych z partii, zobacz [ustawienia środowiska dla zadań](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Widoczność zmiennej środowiskowej

Te zmienne środowiskowe są widoczne tylko w kontekście hello hello **użytkownika zadań**, hello konta użytkownika w węźle hello, w którym jest wykonywane zadania. Będzie *nie* one wyświetlane, jeśli użytkownik [połączyć się zdalnie](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa obliczeniowe węzła za pośrednictwem protokołu RDP (Remote Desktop) lub protokołu Secure Shell (SSH) i listy zmiennych środowiskowych hello. Jest to spowodowane hello konta użytkownika, które służy do połączenia zdalnego nie jest hello taki sam jak hello konto używane przez zadanie hello.

## <a name="command-line-expansion-of-environment-variables"></a>Rozszerzanie zmiennych środowiskowych wiersza polecenia

wiersze poleceń Hello wykonać zadania na obliczeniowe węzłów nie uruchamiaj w powłoce. W związku z tym te wiersze polecenia nie można natywnie skorzystać z funkcji powłoki, takich jak rozszerzanie zmiennych środowiskowych (dotyczy to również hello `PATH`). tootake korzystać z takich funkcji, należy najpierw **wywołania powłoki hello** w wierszu polecenia hello. Na przykład uruchom `cmd.exe` w systemie Windows węzły obliczeniowe lub `/bin/sh` w węzłach Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Zmienne środowiskowe

| Nazwa zmiennej                     | Opis                                                              | Dostępność | Przykład |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | należy Hello nazwę konta wsadowego hello hello zadań.                  | Wszystkie zadania.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Katalogu w ramach hello [katalog roboczy zadania] [ files_dirs] węzły obliczeniowe, w którym certyfikaty są przechowywane w systemie Linux. Należy pamiętać, że tej zmiennej środowiskowej dotyczy tooWindows węzłów obliczeniowych.                                                  | Wszystkie zadania.   |  /mnt/Batch/Tasks/workitems/batchjob001/Job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Identyfikator Hello hello zadania, które hello zadań należy. | Wszystkie zadania z wyjątkiem uruchomienia zadania. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | Pełna ścieżka Hello hello zadanie przygotowanie [katalogu zadania] [ files_dirs] w węźle hello. | Wszystkie zadania z wyjątkiem uruchamiania zadań i zadania przygotowanie zadania. Dostępne tylko, gdy zadanie hello skonfigurowano zadanie przygotowanie zadania. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | Pełna ścieżka Hello hello zadanie przygotowanie [katalog roboczy zadania] [ files_dirs] w węźle hello. | Wszystkie zadania z wyjątkiem uruchamiania zadań i zadania przygotowanie zadania. Dostępne tylko, gdy zadanie hello skonfigurowano zadanie przygotowanie zadania. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Identyfikator Hello hello węzła, który hello zadań jest przypisany do. | Wszystkie zadania. | TVM-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | Pełna ścieżka Hello głównego hello wszystkich [partii katalogów] [ files_dirs] w węźle hello. | Wszystkie zadania. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | Pełna ścieżka hello Hello [udostępnionego katalogu] [ files_dirs] w węźle hello. Wszystkie zadania, które są wykonywane w węźle ma katalogu toothis dostęp do odczytu/zapisu. Zadania, które są wykonywane na innych węzłach nie mają dostępu zdalnego toothis katalogu (nie jest on katalogu sieciowym "udostępniony"). | Wszystkie zadania. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | Pełna ścieżka hello Hello [uruchomić zadania katalogu] [ files_dirs] w węźle hello. | Wszystkie zadania. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Identyfikator Hello hello puli, która hello zadań jest uruchomiona na. | Wszystkie zadania. | batchpool001 |
| AZ_BATCH_TASK_DIR               | Pełna ścieżka hello Hello [katalogu zadania] [ files_dirs] w węźle hello. Ten katalog zawiera hello `stdout.txt` i `stderr.txt` hello zadań i hello AZ_BATCH_TASK_WORKING_DIR. | Wszystkie zadania. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Identyfikator Hello hello bieżącego zadania. | Wszystkie zadania z wyjątkiem uruchomienia zadania. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | Pełna ścieżka hello Hello [katalog roboczy zadania] [ files_dirs] w węźle hello. Witaj aktualnie uruchomione zadanie ma katalogu toothis dostęp do odczytu/zapisu. | Wszystkie zadania. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | Lista Hello węzły i liczba rdzeni przypadająca na węzeł przydzielonych tooa [zadań wielu wystąpieniach][multi_instance]. Węzły i rdzeni są wyświetlane w formacie hello`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, gdzie hello liczba węzłów następuje co najmniej jeden węzeł adresów IP i hello liczba rdzeni dla każdego. |  Mająca wiele wystąpień podstawowym i podzadania. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Witaj listy węzłów, które są przydzielane tooa [zadań wielu wystąpień] [ multi_instance] w formacie hello `nodeIP;nodeIP`. | Mająca wiele wystąpień podstawowym i podzadania. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Witaj listy węzłów, które są przydzielane tooa [zadań wielu wystąpień] [ multi_instance] w formacie hello `nodeIP,nodeIP`. | Mająca wiele wystąpień podstawowym i podzadania. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Witaj adres IP i port hello węzła obliczeniowego na które hello głównym zadaniem [zadań wielu wystąpień] [ multi_instance] działa. | Mająca wiele wystąpień podstawowym i podzadania. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Ścieżka do katalogu jest taka sama dla hello zadanie głównej i każdy podzadaniem [zadań wielu wystąpieniach][multi_instance]. Witaj ścieżka istnieje w każdym węźle, w której działa program hello wielu wystąpień zadań i odczytu/zapisu toohello dostępne polecenia zadania uruchomione w tym węźle (zarówno hello [polecenia koordynacji] [ coord_cmd] i hello [polecenia aplikacji][app_cmd]). Podzadań lub podstawowe zadania, które wykonania na innych węzłach nie mają dostępu zdalnego toothis katalogu (nie jest on katalogu sieciowym "udostępniony"). | Mająca wiele wystąpień podstawowym i podzadania. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Określa, czy bieżący węzeł hello jest węzeł główny hello [zadań wielowystąpieniowy][multi_instance]. Możliwe wartości to `true` i `false`.| Mająca wiele wystąpień podstawowym i podzadania. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Jeśli `true`, hello bieżący węzeł jest węzłem dedykowanych. Jeśli `false`, jest [węzła niskiego priorytetu](batch-low-pri-vms.md). | Wszystkie zadania. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
