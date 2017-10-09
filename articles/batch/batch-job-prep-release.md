---
title: "aaaCreate zadań tooprepare zadania i zakończenie zadania na węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj poziom zadania przygotowanie zadania toominimize danych przenieść węzłów obliczeniowych partii tooAzure i zwolnij zadania oczyszczania węzła po zakończeniu zadania."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Uruchom zadanie przygotowanie i wersji zadania w partii węzły obliczeniowe

 Zadanie usługi partia zadań Azure często wymaga pewnej formy instalacji, przed jego zadania są wykonywane, a po zadania konserwacji, po zakończeniu jego zadań podrzędnych. Może być konieczne toodownload typowych zadań danych wejściowych tooyour węzły obliczeniowe lub Przekaż tooAzure danych wyjściowych zadania magazynu po zakończeniu zadania hello. Można użyć **zadania przygotowanie** i **zadania wersji** zadań tooperform te operacje.

## <a name="what-are-job-preparation-and-release-tasks"></a>Co to są zadanie przygotowanie i zwolnij zadania?
Przed uruchomieniem zadania, hello zadanie przygotowanie zadania działa na wszystkich toorun zaplanowane węzły obliczeniowe co najmniej jedno zadanie. Po zakończeniu zadania hello hello zadania Zwolnienie zadania działa na każdym węźle puli hello wykonywane co najmniej jedno zadanie. Podobnie jak w przypadku normalnych partii zadań, możesz określić toobe wiersza polecenia, wywoływana, gdy zadanie przygotowanie lub wersji zadanie zostanie uruchomione.

Zadania przygotowania i wersji oferują znanych partii zadań funkcje, takie jak pobieranie pliku ([pliki zasobów][net_job_prep_resourcefiles]), z podwyższonym poziomem uprawnień wykonywania, zmienne środowiskowe niestandardowych wykonywania maksymalny czas trwania, liczbę ponownych prób i czas przechowywania pliku.

W następujące sekcje hello, dowiesz się, jak toouse hello [JobPreparationTask] [ net_job_prep] i [JobReleaseTask] [ net_job_release] w hello znaleziono klas [Partiami platformy .NET] [ api_net] biblioteki.

> [!TIP]
> Przygotowanie i wersji zadania są szczególnie przydatne w środowiskach "udostępniania puli", w którym puli węzłów obliczeniowych będzie się powtarzał między uruchomionych zadań i jest używany przez wiele zadań.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Gdy toouse zadania przygotowanie i zwolnić zadania
Przygotowanie zadania i wersji zadania są dobrze dla hello następujące sytuacje:

**Pobierz dane typowe zadania**

Zadania wsadowe często wymagają ze wspólnego zestawu danych jako dane wejściowe dla hello zadania. Na przykład codziennie obliczenia analizy ryzyka, danych rynkowych jest określonych zadań jeszcze typowych zadań tooall w zadaniu hello. Tych danych rynkowych, rozmiar, często kilku gigabajtów należy węzeł obliczeniowy tooeach pobrane tylko raz, aby wszystkie zadania w węźle hello może być używany. Użyj **zadanie przygotowanie zadania** toodownload tego węzła tooeach danych przed hello wykonanie zadania hello innych zadań.

**Usuń dane wyjściowe poleceń i zadań**

W środowisku "udostępniania puli", gdzie węzły obliczeniowe puli nie są wycofany z eksploatacji między zadaniami, może być konieczne danych zadania toodelete między działa. Może być konieczne tooconserve miejsce na węzłach hello lub spełnia zasady zabezpieczeń w organizacji. Użyj **zadania Zwolnienie zadania** toodelete danych, które zostało pobrane przez zadanie przygotowanie zadania lub wygenerowanych podczas wykonanie zadania.

**Przechowywanie dziennika**

Możesz tookeep kopię plików dziennika, które generują zadań lub być może pliki zrzutu awaryjnego, które mogą być generowane przez aplikacje nie powiodło się. Użyj **zadania Zwolnienie zadania** w takich przypadkach toocompress i przekazać ten tooan danych [usługi Azure Storage] [ azure_storage] konta.

> [!TIP]
> Inny sposób toopersist dzienniki i innych poleceń i zadań danych jest wyjściowy toouse hello [konwencje pliku wsadowego Azure](batch-task-output.md) biblioteki.
> 
> 

## <a name="job-preparation-task"></a>Zadanie przygotowanie zadania
Przed wykonaniem zadania wsadowego wykonuje hello zadanie przygotowanie zadania w każdym węźle obliczeń, który jest toorun zaplanowanego zadania. Domyślnie hello usługa partia zadań czeka na powitania zadanie przygotowanie zadania toobe wykonany przed uruchomieniem tooexecute zaplanowanego zadania hello w węźle hello. Można jednak skonfigurować usługi hello nie toowait. Jeśli ponowne uruchomienie węzła hello, hello zadanie przygotowanie zadania zostanie ponownie uruchomione, ale można również wyłączyć to zachowanie.

Witaj zadanie przygotowanie zadania jest wykonywany tylko na węzłach, które są toorun zaplanowanego zadania. Zapobiega to hello niepotrzebnych wykonywanie przygotowanie zadania, w przypadku, gdy węzeł nie jest przypisany zadania. Taka sytuacja może wystąpić, gdy hello liczba zadań dla zadania jest mniejsza niż hello liczby węzłów w puli. Ma również zastosowanie podczas [wykonywanie zadań jednoczesnych](batch-parallel-node-tasks.md) jest włączone, jeśli liczba zadań hello jest niższa niż hello całkowita liczba zadań jednoczesnych możliwe niektóre węzły dlatego bezczynności. Uruchamiając nie hello zadanie przygotowanie zadania w węzłach bezczynności, możesz można kupować mniej opłat za transfer danych.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] różni się od [CloudPool.StartTask] [ pool_starttask] w tym JobPreparationTask wykonuje na powitania na początku każdego zadania, natomiast StartTask wykonuje, tylko gdy węzeł obliczeniowy najpierw dołącza puli lub ponownego uruchomienia.
> 
> 

## <a name="job-release-task"></a>Zadanie zwolnienie zadania
Gdy zadanie zostanie oznaczone jako wykonane, hello zadania Zwolnienie zadania jest wykonywany w każdym węźle puli hello wykonywane co najmniej jedno zadanie. Zadania są oznaczone jako ukończone, wysyłając żądanie przerwania. Witaj usługa partia zadań, a następnie ustawia hello stanu zadania za*przerywanie*kończy żadnych zadań aktywnych lub nie działają, skojarzone z zadaniem hello i uruchamia hello zadania Zwolnienie zadania. zadanie Hello przenosi toohello *ukończone* stanu.

> [!NOTE]
> Usuwanie zadania wykonuje również hello zadania Zwolnienie zadania. Jednak jeśli zadanie zostało zakończone, hello zwolnienie zadania nie jest uruchamiane po raz drugi Jeśli zadanie hello później zostanie usunięty.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Zadania w środowisku przedprodukcyjnym i zwolnij zadania związane z partiami platformy .NET
Przypisz toouse zadanie przygotowanie zadania, [JobPreparationTask] [ net_job_prep] zadania tooyour obiektów [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] właściwości . Podobnie, zainicjować [JobReleaseTask] [ net_job_release] i przypisz mu zadania tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset właściwości zadanie zwolnienie zadania.

W poniższym przykładzie `myBatchClient` jest wystąpieniem [BatchClient][net_batch_client], i `myPool` jest istniejącej puli w ramach hello konta usługi partia zadań.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Jak wspomniano wcześniej, hello zwolnienie zadania jest wykonywany, gdy zadanie zostanie przerwane lub usunięty. Zakończ zadanie z [JobOperations.TerminateJobAsync][net_job_terminate]. Usuń zadanie o [JobOperations.DeleteJobAsync][net_job_delete]. Zwykle przerwanie lub usunąć zadania po zakończeniu jego zadań podrzędnych lub gdy został osiągnięty limit czasu, który został zdefiniowany.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Przykładowy kod w witrynie GitHub
toosee przygotowania i wersji zadania akcji, zapoznaj się z hello [JobPrepRelease] [ job_prep_release_sample] przykładowy projekt w witrynie GitHub. Ta aplikacja konsoli hello następujące:

1. Tworzona jest pula z dwoma węzłami "małe".
2. Tworzy zadanie przygotowanie zadania, wersji i zadań standardowych.
3. Uruchamia hello zadanie przygotowanie zadania, który najpierw zapisuje plik tekstowy tooa identyfikator węzła hello w katalogu "udostępniony" węzła.
4. Uruchomienie zadania na każdym węźle, który zapisuje jego toohello identyfikator zadania tego samego pliku tekstowego.
5. Po wykonaniu wszystkich zadań (lub osiągnięciu limitu czasu hello), drukuje zawartość hello każdego węzła tekstowego pliku toohello konsoli.
6. Po zakończeniu zadania hello jest uruchamiane hello zadania zlecenia zadań toodelete hello pliku hello węzła.
7. Drukuje hello kody hello zadanie przygotowanie zakończenia i zwolnij zadań dla każdego węzła, na którym są wykonywane.
8. Wstrzymuje wykonanie tooallow potwierdzenie usunięcia zadania i/lub puli.

Dane wyjściowe z aplikacji przykładowej hello jest podobne toohello następujące czynności:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Powodu toohello zmiennej tworzenia i czasu rozpoczęcia węzłów w nowej puli (niektóre węzły są gotowe do zadań przed innymi) mogą pojawić się różne wyniki. W szczególności ponieważ zadania hello zakończył się szybko, jednym z węzłów hello puli może wykonywać wszystkie zadania hello zadania. W takim przypadku można zauważyć tego hello zadania przedprodukcyjnym i zwolnij zadania nie istnieją dla węzła hello, wykonywania żadnych zadań.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Przejrzyj zadanie przygotowanie i zadania wersji w hello portalu Azure
Po uruchomieniu hello przykładowej aplikacji, można użyć hello [portalu Azure] [ portal] tooview hello właściwości hello zadania i jego zadań, a nawet pobierać plik tekstowy udostępnionego hello jest modyfikowany przez hello zadania.

Witaj Poniższy zrzut ekranu przedstawia hello **przygotowanie zadania bloku** w portalu Azure po uruchomieniu hello przykładowej aplikacji hello. Przejdź toohello *JobPrepReleaseSampleJob* właściwości po zakończeniu zadania (ale przed usunięciem zadania, a pula) i kliknij przycisk **zadań przygotowawczych** lub **wersji zadania** tooview ich właściwości.

![Właściwości przygotowanie zadania w portalu Azure][1]

## <a name="next-steps"></a>Następne kroki
### <a name="application-packages"></a>Pakiety aplikacji
W dodatku toohello zadanie przygotowanie zadania umożliwia także hello [pakietów aplikacji](batch-application-packages.md) funkcji partii tooprepare obliczeniowe węzłów do wykonania zadania. Ta funkcja jest szczególnie przydatna w przypadku wdrażania aplikacji, które nie wymagają uruchomiony Instalator, aplikacje, które zawierają wiele plików (100 +) lub aplikacji, które wymagają kontroli wersji strict.

### <a name="installing-applications-and-staging-data"></a>Instalowanie aplikacji i danych na potrzeby przemieszczania
Ten wpis na forum MSDN zawiera omówienie kilka metod przygotowywania węzły do uruchamiania zadań:

[Instalowanie aplikacji i danych na partii przemieszczania węzły obliczeniowe][forum_post]

Napisane przez jeden z członków zespołu partii zadań Azure hello, omówiono kilka technik służy węzłów toocompute toodeploy aplikacji i danych.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
