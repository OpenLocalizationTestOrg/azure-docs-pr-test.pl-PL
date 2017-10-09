---
title: "aaaRun zadań równoległych toouse zasoby obliczeniowe wydajnie - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Zwiększenie wydajności i zredukowania kosztów przy użyciu mniejszej liczby węzłów obliczeniowych i uruchamianie równoczesnych zadań w każdym węźle w puli partii zadań Azure"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Równoczesne uruchamianie zadań toomaximize użycia węzłów obliczeniowych partii 

Uruchamiając więcej niż jedno zadanie równocześnie w każdym węźle obliczeń w puli partii zadań Azure, można zmaksymalizować użycia zasobów na mniejszą liczbę węzłów w puli hello. W przypadku niektórych obciążeń może to spowodować krótszych czasów zadań i tańsze.

Gdy niektóre scenariusze korzystania z dedykowanym wszystkie zasoby węzła tooa pojedyncze zadanie, kilku sytuacjach korzystać z stosowanie wielu zadań tooshare tych zasobów:

* **Minimalizowanie transferu danych** podczas zadania są możliwe tooshare danych. W tym scenariuszu może znacznie zmniejszyć koszty transferu danych przez skopiowanie danych udostępnionych tooa mniejszej liczby węzłów i wykonywanie zadań równolegle na każdym węźle. Dotyczy to zwłaszcza, jeśli węzeł skopiowanych tooeach toobe danych hello muszą być przekazywane między regionów geograficznych.
* **Maksymalizacja użycie pamięci** podczas zadania wymagają dużej ilości pamięci, ale tylko w krótkich okresach czasu i w czasie zmiennej podczas wykonywania. Można stosować mniej, ale większy, wyliczenia węzłów mających więcej pamięci tooefficiently obsługi tych wartości szczytowe. Te węzły byłyby wielu zadań uruchomione równolegle w każdym węźle, ale każde zadanie będzie korzystać węzłów hello dużej ilości pamięci w różnym czasie.
* **Zmniejszenia limity numer węzła** podczas komunikacji między węzłami jest wymagana w puli. Obecnie pule skonfigurowane do komunikacji między węzłami są ograniczone too50 węzłów obliczeniowych. Jeśli każdy węzeł w takich puli jest tooexecute stanie zadania równolegle, większa liczba zadań mogą być wykonywane jednocześnie.
* **Replikowanie lokalnych klastra obliczeniowego**, takie jak kiedy najpierw przenieść tooAzure środowiska obliczeniowego. Jeśli bieżącego rozwiązania lokalnego wykonuje wiele zadań na węzeł obliczeń, można zwiększyć maksymalną liczbę hello zadań węzła toomore ściśle duplikatów tej konfiguracji.

## <a name="example-scenario"></a>Przykładowy scenariusz
Jako przykład tooillustrate hello zalet wykonywanie zadań równoległych, załóżmy, że aplikacja zadanie ma wymagania dotyczące procesora CPU i pamięci tak, aby [standardowe\_D1](../cloud-services/cloud-services-sizes-specs.md) węzły są wystarczające. Jednak w kolejności toofinish hello zadania w czasie hello wymagane 1000 te węzły są potrzebne.

Zamiast standardowego\_D1 węzły, które mają 1 rdzeń procesora CPU, można użyć [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) węzłów, które ma 16 rdzeni i włącz wykonywanie zadań równoległych. W związku z tym *16 razy mniej węzłów* można użyć — zamiast 1000 węzłów tylko 63 będą wymagane. Ponadto jeśli pliki dużych aplikacji lub dane referencyjne są wymagane dla każdego węzła, czas trwania zadania i wydajności ponownie lepsza od hello dane są kopiowane tooonly 16 węzłów.

## <a name="enable-parallel-task-execution"></a>Włącz wykonywanie zadań równoległych
Węzłami obliczeniowymi w celu wykonania zadań równoległych można skonfigurować na poziomie puli hello. Z biblioteki .NET partii hello, ustaw hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwość podczas tworzenia puli. Jeśli używasz hello interfejsu API REST partii ustawić hello [maxTasksPerNode] [ rest_addpool] elementu w treści żądania hello podczas tworzenia puli.

Partia zadań Azure umożliwia tooset maksymalną zadań na węzeł toofour razy (4 x) hello liczby rdzeni węzła. Na przykład jeśli hello pula jest skonfigurowana z węzłami rozmiar "Duże" (4 rdzenie), następnie `maxTasksPerNode` too16 może być ustawiony. Aby uzyskać szczegółowe informacje na powitania liczba rdzeni dla każdego rozmiary węzła hello, zobacz [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md). Aby uzyskać więcej informacji na ograniczenia usługi, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).

> [!TIP]
> Można tootake się do konta hello `maxTasksPerNode` wartość utworzenia [formułą automatycznego skalowania] [ enable_autoscaling] dla użytkownika. Na przykład formuła, której wynikiem `$RunningTasks` może mieć znaczący wpływ wzrost zadań na węzeł. Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](batch-automatic-scaling.md) Aby uzyskać więcej informacji.
>
>

## <a name="distribution-of-tasks"></a>Podział zadań
W przypadku hello węzłów obliczeniowych w puli mogą jednocześnie wykonywać zadania, jest ważne toospecify sposób toobe zadania hello rozproszone na węzłach hello hello puli.

Za pomocą hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] właściwości, można określić czy zadania powinien być przypisany równomiernie we wszystkich węzłach w puli hello ("rozpraszania"). Lub możesz określić, że jako wiele zadań, jak to możliwe należy przypisać węzła tooeach przed zadania są przydzielone tooanother węzła w puli hello ("pakowania").

Jako przykład sposobu ta funkcja jest przydatna, należy wziąć pod uwagę puli hello [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) węzłów (w powyższym przykładzie hello), które skonfigurowano [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] wartość 16. Jeśli hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] skonfigurowano [ComputeNodeFillType] [ fill_type] z *pakietu*, czy zmaksymalizować użycie wszystkich rdzeni 16 każdego węzła i umożliwia [puli Skalowanie automatyczne](batch-automatic-scaling.md) tooprune nieużywanych węzłów z puli hello (węzłów bez żadnych zadań przypisane). Ten sposób można zmniejszyć obciążenie zasobów i zapisuje pieniędzy.

## <a name="batch-net-example"></a>Przykład .NET partii
To [partiami platformy .NET] [ api_net] interfejsu API fragment kodu przedstawia toocreate żądania puli, która zawiera cztery węzły dużych maksymalnie cztery zadania w każdym węźle. Określa zadanie planowania zasad, które spowoduje wypełnienie każdego węzła za węzeł tooanother zadania tooassigning wcześniejszych zadań w puli hello. Aby uzyskać więcej informacji o dodawaniu pule przy użyciu hello interfejs API .NET partii zobacz [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Przykład REST partii
To [REST partii] [ api_rest] interfejsu API fragment kodu przedstawia toocreate żądania puli, która zawiera dwa węzły dużych maksymalnie cztery zadania w każdym węźle. Aby uzyskać więcej informacji o dodawaniu pule przy użyciu interfejsu API REST hello, zobacz [dodać konto puli tooan][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Można ustawić hello `maxTasksPerNode` elementu i [MaxTasksPerComputeNode] [ maxtasks_net] właściwość tylko w czasie tworzenia puli. Nie można zmodyfikować po puli został już utworzony.
>
>

## <a name="code-sample"></a>Przykład kodu
Witaj [ParallelNodeTasks] [ parallel_tasks_sample] projektu w witrynie GitHub przedstawiono użycie hello hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwości.

Witaj korzysta z tej aplikacji konsolowej C# [partiami platformy .NET] [ api_net] toocreate biblioteki puli z co najmniej jednym węzły obliczeniowe. Można skonfigurować wiele zadań jest wykonywana na tych węzłach toosimulate zmiennej obciążenia. Dane wyjściowe aplikacji hello Określa węzły, które wykonywane każdego zadania. Aplikacja Hello także podsumowanie hello parametrów zadania i czas trwania. Podsumowanie część hello dane wyjściowe dwa przebiegi różnych hello przykładowej aplikacji Hello pojawia się poniżej.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

pierwszy wykonywanie hello przykładowej aplikacji Hello wskazuje, że z jednego węzła w puli hello i hello domyślne ustawienie jedno zadanie na węźle, czas trwania zadania hello jest ponad 30 minut.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Witaj, drugi uruchomienie przedstawiono przykładowe hello znaczny spadek czas trwania zadania. Jest to spowodowane puli hello został skonfigurowany z czterech zadań na węzeł, dzięki czemu zadanie równoległe wykonywanie toocomplete hello zadania w niemal kwartału hello czasu.

> [!NOTE]
> czas trwania zadania Hello w powyższych podsumowania hello nie dołączaj czas utworzenia puli. Każdego z powyższych zadań hello został przesłany toopreviously utworzone pule którego węzły obliczeniowe były hello *bezczynny* stanu w czasie przesyłania.
>
>

## <a name="next-steps"></a>Następne kroki
### <a name="batch-explorer-heat-map"></a>Mapa cieplna Explorer partii
Witaj [Eksploratora usługi partia zadań Azure][batch_explorer], jeden hello partii zadań Azure [przykładowe aplikacje][github_samples], zawiera *Mapa cieplna* funkcja, która umożliwia wizualizację wykonywania zadania. Jeśli w przypadku wykonywania hello [ParallelTasks] [ parallel_tasks_sample] przykładowej aplikacji, można użyć hello Mapa cieplna funkcji tooeasily wizualizacji hello wykonywanie zadań równoległych w każdym węźle.

![Mapa cieplna Explorer partii][1]

*Mapa cieplna Explorer partii przedstawiający puli czterech węzłów z każdego węzła aktualnie wykonywanych zadań cztery*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
