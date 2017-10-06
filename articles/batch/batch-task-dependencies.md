---
title: "Po zakończeniu hello innych zadań — partii zadań Azure na podstawie aaaUse zadanie zależności toorun zadania | Dokumentacja firmy Microsoft"
description: "Utwórz zadania, które są zależne od ukończenia hello innych zadań przetwarzania stylu MapReduce i podobnych danych big data obciążeń w partii zadań Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Tworzenie zadań zależności toorun zadania, które są zależne od innych zadań

Toorun zależności zadań można zdefiniować zadania lub zestawu zadań dopiero po zakończeniu zadania nadrzędnego. Sytuacje, w którym zależności zadań są przydatne obejmują:

* Styl MapReduce obciążeń w chmurze hello.
* Zadania, których zadania przetwarzania danych może zostać wyrażona jako ukierunkowanego wykresu acyklicznego (DAG).
* Procesy renderowania wstępnego i renderowania po, gdzie każde zadanie należy wykonać przed rozpoczęciem powitalne następne zadanie.
* Inne zadanie w którym zadania podrzędne są zależne od hello dane wyjściowe zadania nadrzędnego.

Zależności zadań wsadowych umożliwia tworzenie zadań, które są zaplanowane do uruchomienia na węzły obliczeniowe po zakończeniu hello jednego lub więcej zadań nadrzędnej. Na przykład można utworzyć zadania, który renderuje każdej ramce 3D film z oddzielnych zadań równoległych. ostatnim zadaniem Hello — Witaj "scalania zadania"--scaleń hello renderowane ramek na powitania tylko cały film po wszystkich ramki pomyślnie nadano.

Dopiero po pomyślnym zakończeniu zadania nadrzędnego hello zadania zależne są domyślnie zaplanowane do uruchomienia. Można określić zachowanie domyślne hello toooverride akcji zależności i uruchamianie zadań, gdy zadanie nadrzędne hello nie powiedzie się. Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.  

Można tworzyć zadania, które są zależne od innych zadań w relacji jeden do jednego lub jeden do wielu. Można również utworzyć zależność zakresu, gdzie zadania zależy od ukończenia hello grupy zadań w ramach określonego zakresu identyfikatorów zadań. Można połączyć te trzy relacje wiele do wielu toocreate scenariuszy podstawowych.

## <a name="task-dependencies-with-batch-net"></a>Zależności zadań z partiami platformy .NET
W tym artykule omówiono sposób hello tooconfigure zależności zadań za pomocą [partiami platformy .NET] [ net_msdn] biblioteki. Firma Microsoft najpierw dowiesz się, jak za[włączyć współzależności](#enable-task-dependencies) na zadaniach i pokazują, jak za[skonfigurować zadania z zależnościami](#create-dependent-tasks). Również opisać jak toospecify zależności akcji toorun zadań zależnych Jeśli hello nadrzędnego nie powiedzie się. Ponadto omówiono hello [scenariusze zależności](#dependency-scenarios) obsługującego partii.

## <a name="enable-task-dependencies"></a>Włącz zależności zadań
zależności zadań toouse w partii aplikacji, należy najpierw skonfigurować hello zadania toouse zadań zależności. W partiami platformy .NET, należy włączyć ją w Twojej [CloudJob] [ net_cloudjob] przez ustawienie jej [UsesTaskDependencies] [ net_usestaskdependencies] właściwości zbyt`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

W hello poprzedzających fragment kodu, "batchClient" jest wystąpieniem hello [BatchClient] [ net_batchclient] klasy.

## <a name="create-dependent-tasks"></a>Utwórz zadania zależne
toocreate zadanie, które jest zależna od zakończenia hello jednego lub więcej zadań nadrzędnej, można określić które hello zadania "zależy od" hello innych zadań. W partiami platformy .NET, należy skonfigurować hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] właściwości z wystąpieniem hello [TaskDependencies] [ net_taskdependencies] klasy:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Następujący fragment kodu tworzy zależnego zadania o identyfikatorze zadania "Kwiaty". Witaj "Kwiaty" zadań zależy od zadania "Ustaniu" i "Sun". Zadanie "Kwiaty" będzie zaplanowane toorun w węźle obliczeń tylko po zadań, które "Ustaniu" i "Sun" została ukończona pomyślnie.

> [!NOTE]
> Zadanie jest uznawany za toobe ukończona pomyślnie, gdy będzie hello **ukończone** stanu i jego **kod zakończenia** jest `0`. W partiami platformy .NET, oznacza to [CloudTask][net_cloudtask].[ Stan] [ net_taskstate] wartość właściwości `Completed` i hello w CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] wartość właściwości jest `0`.
> 
> 

## <a name="dependency-scenarios"></a>Scenariusze zależności
Istnieją trzy scenariusze zależności podstawowe zadania, których można używać w partii zadań Azure: jeden do jednego, jeden do wielu, a zadania o identyfikatorze zakresu zależności. Mogą to być połączone tooprovide czwarty scenariuszu wiele do wielu.

| Scenariusz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Przykład |  |
|:---:| --- | --- |
|  [Jeden do jednego](#one-to-one) |*taskB* zależy od *taskA* <p/> *taskB* nie będzie można zaplanować wykonywanie do momentu *taskA* zostało ukończone pomyślnie |![Diagram: jeden do jednego zadania zależności][1] |
|  [Jeden do wielu](#one-to-many) |*zadanieC* zależy od *zadaniaA* i *zadaniaB* <p/> *taskC* nie zostanie zaplanowane do wykonania przed zakończeniem *taskA* i *taskB* zostały ukończone pomyślnie |![Diagram: jeden do wielu zadań zależności][2] |
|  [Zakres identyfikator zadania](#task-id-range) |*taskD* zależy od zakresu zadań <p/> *taskD* nie zostanie zaplanowane wykonywanie do momentu hello zadania z identyfikatorami *1* za pośrednictwem *10* zostały ukończone pomyślnie |![Diagram: Zadanie identyfikator zakresu zależności][3] |

> [!TIP]
> Można utworzyć **wiele do wielu** relacje, np. gdy zadania C, D E i F każdego zależą od zadania, A i B. Jest to przydatne, na przykład w zrównoleglone przetwarzania wstępnego scenariuszy, w którym zadania podrzędne są zależne od danych wyjściowych hello wielu zadań nadrzędnego.
> 
> W przykładach hello w tej sekcji zależne zadanie jest uruchamiane tylko wtedy, gdy zadania nadrzędnego hello pomyślnie ukończona. To zachowanie jest hello domyślne zachowanie dla zadania zależne. Możesz uruchomić zadanie zależne po niepowodzeniu zadaniem nadrzędnym, określając zachowanie domyślne hello toooverride akcji zależności. Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.

### <a name="one-to-one"></a>Jeden do jednego
W relacji jeden do jednego zadania zależy od hello pomyślne zakończenie zadania jednego zdarzenia nadrzędnego. toocreate hello zależności, podaj toohello identyfikator pojedyncze zadanie [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Jeden do wielu
W relacji jeden do wielu zadania zależy od ukończenia hello wielu zadań nadrzędnej. toocreate hello zależności, przedstawiają kolekcję zadań identyfikatorów toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [ net_cloudtask].

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a>Zakres identyfikator zadania
W zależności w zakresie nadrzędnej zadania zadania zależy od hello hello zakończenia zadania, których identyfikatory znajdują się w zakresie.
zależności hello toocreate, najpierw Podaj hello i ostatnio identyfikatorów zadań w hello zakresu toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Gdy używasz zakresy identyfikatorów zadań dla zależności hello identyfikatorów zadań w zakresie hello *musi* być liczbami w postaci ciągu wartości będące liczbami całkowitymi.
> 
> Każde zadanie w zakresie hello muszą spełniać zależności hello pomyślne zakończenie działania albo wykonując z błąd, który jest akcja zależności zamapowanych tooa ustawić także**Satisfy**. Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a>Akcje zależności

Domyślnie zadanie zależne lub zestawu zadań działa tylko po pomyślnym zakończeniu zadania nadrzędnego. W niektórych scenariuszach może być toorun zadania zależne, nawet w przypadku awarii hello zadaniem nadrzędnym. Hello domyślne zachowanie można przesłonić, określając akcji zależności. Akcja zależności Określa, czy zadanie zależne kwalifikujących się toorun, oparte na powitania powodzenie lub niepowodzenie hello zadaniem nadrzędnym. 

Na przykład załóżmy, że zadanie zależne oczekuje na dane z hello ukończenia zadania nadrzędnego hello. Zadanie nadrzędne hello nie powiedzie się, zadania zależne hello może nadal być stanie toorun przy użyciu starszych danych. W takim przypadku akcji zależności można określić zadania zależne hello jest toorun kwalifikujących się niezależnie od awarii hello hello zadaniem nadrzędnym.

Akcja zależności jest oparta na warunku wyjścia dla zadania nadrzędnego hello. Można określić akcję zależności dla każdego hello następujących warunków zakończenia. dla platformy .NET, zobacz hello [ExitConditions] [ net_exitconditions] klasy, aby uzyskać szczegółowe informacje:

- Po wystąpieniu błędu przetwarzania wstępnego.
- Po wystąpieniu błędu przekazywania plików. Jeśli zadanie hello kończy działanie z kodem zakończenia, która została określona za pomocą **exitCodes** lub **exitCodeRanges**, a następnie napotka błąd podczas przekazywania pliku, hello akcji określonej przez hello zakończenia kod ma pierwszeństwo.
- Gdy zadanie hello kończy działanie z kodem zakończenia zdefiniowanych przez hello **ExitCodes** właściwości.
- Gdy zadanie hello kończy działanie z kodem zakończenia, która wykracza poza zakres określony przez hello **ExitCodeRanges** właściwości.
- Witaj domyślne działanie case, jeśli zadanie hello kończy działanie z kodem zakończenia nie jest zdefiniowany przez **ExitCodes** lub **ExitCodeRanges**, lub czy istnieje hello zadań przetwarzania wstępnego błąd i hello **PreProcessingError**  nie ustawiono właściwości lub jeśli hello zadań kończy się niepowodzeniem z plikiem przekazywanie błędów i hello **FileUploadError** nie ustawiono właściwości. 

toospecify akcją zależności w programie .NET, zestaw hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] właściwości warunku exit hello. Witaj **DependencyAction** właściwość przyjmuje jeden z dwóch wartości:

- Ustawienie hello **DependencyAction** właściwości zbyt**Satisfy** wskazuje, że zadania zależne są toorun kwalifikujących się, jeśli zadaniem nadrzędnym hello kończy działanie z powodu określonego błędu.
- Ustawienie hello **DependencyAction** właściwości zbyt**bloku** wskazuje, że zadania zależne nie są toorun kwalifikujących się.

Domyślnym ustawieniem hello Hello **DependencyAction** właściwość jest **Satisfy** dla kod zakończenia 0, i **bloku** dla wszystkich innych warunków zakończenia.

Witaj poniższy fragment kodu ustawia hello **DependencyAction** właściwości dla zadania nadrzędnego. Jeśli zadaniem nadrzędnym hello kończy działanie z błędem przetwarzania wstępnego lub z hello hello zależnych kody błędów określona, zadanie zostanie zablokowany. Jeśli zadaniem nadrzędnym hello kończy działanie z inny błąd zera, zadania zależne hello jest toorun kwalifikujących się.

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a>Przykład kodu
Witaj [TaskDependencies] [ github_taskdependencies] przykładowy projekt jest jednym z hello [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub. Przedstawiono to rozwiązanie Visual Studio:

- Jak tooenable zadań zależności w zadaniu
- Jak toocreate zadań, które są zależne od innych zadań
- Jak tooexecute tych zadań w puli węzłów obliczeniowych.

## <a name="next-steps"></a>Następne kroki
### <a name="application-deployment"></a>Wdrażanie aplikacji
Witaj [pakietów aplikacji](batch-application-packages.md) funkcja partii zapewnia łatwy sposób wdrożyć tooboth i wersji aplikacji hello, wykonywanych zadań na węzłach obliczeniowych.

### <a name="installing-applications-and-staging-data"></a>Instalowanie aplikacji i danych na potrzeby przemieszczania
Zobacz [instalowania aplikacji i danych na partii przemieszczania węzły obliczeniowe] [ forum_post] forum partii zadań Azure hello Omówienie metody przygotowania węzły toorun zadania. Zapisane przez jeden z członków zespołu partii zadań Azure hello, ten wpis jest dobrym Elementarz na powitania różne sposoby toocopy aplikacje, dane wejściowe zadania i inne pliki tooyour obliczeniowe węzłów.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: jeden do jednego zależności"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: jeden do wielu zależności"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: zadanie identyfikator zakresu zależności"
