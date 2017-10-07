---
title: "aaaPersist i zadań tooAzure magazynu z biblioteką konwencje plików hello danych wyjściowych dla platformy .NET — partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse biblioteki konwencje plików usługi partia zadań Azure dla platformy .NET toopersist partii zadań i tooAzure dane wyjściowe zadania magazynu i widoku hello utrwalone w danych wyjściowych w hello portalu Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Utrwalanie zadań i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Dane zadania jednokierunkowej toopersist jest toouse hello [biblioteki konwencje plików usługi partia zadań Azure dla platformy .NET][nuget_package]. Witaj biblioteki konwencje plików upraszcza proces hello przechowywania danych wyjściowych zadania tooAzure danych przechowywania i pobierania jej. Witaj konwencje plików biblioteki w kodzie zarówno zadania, jak i klienta można używać &mdash; w kodzie zadań utrwalanie plików, a w kliencie code toolist i pobrać je. Kod zadań można również użyć hello biblioteki tooretrieve hello dane wyjściowe zadania nadrzędnego, takich jak w [zadań zależności](batch-task-dependencies.md) scenariusza. 

pliki z biblioteki konwencje plików hello wyjściowe tooretrieve, wystawiając według Identyfikatora i celem można zlokalizować hello plików dla danego zadania lub zadania. Nie trzeba tooknow hello nazwy i lokalizacje plików hello. Na przykład można użyć wszystkich plików pośrednich hello konwencje plików biblioteki toolist dla danego zadania lub Pobierz plik podglądu dla danego zadania.

> [!TIP]
> Począwszy od wersji 2017-05-01, hello interfejsu API partii usługi obsługuje trwałych tooAzure danych wyjściowych magazynu dla zadań i zadania Menedżer zadania, które będą uruchamiane w pulach utworzone za pomocą hello konfiguracji maszyny wirtualnej. Witaj interfejsu API partii usługi zawiera toopersist mówiąc w uproszczeniu, dane wyjściowe z kodem hello, tworzy zadanie, który służy jako alternatywne toohello konwencje plików biblioteki. Dane wyjściowe toopersist partii klienta aplikacji można modyfikować, bez konieczności aplikacji hello tooupdate, która działa zadania. Aby uzyskać więcej informacji, zobacz [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Kiedy używać danych wyjściowych zadania toopersist hello konwencje plik biblioteki?

Partia zadań Azure zawiera więcej niż jednym ze sposobów toopersist dane wyjściowe zadania. Witaj konwencje plików jest najlepiej nadaje się toothese scenariusze:

- Można łatwo zmodyfikować hello kod aplikacji hello, że zadanie działa toopersist plików za pomocą hello konwencje plików biblioteki.
- Podczas zadania hello jest nadal uruchomiona, które mają toostream tooAzure danych magazynu.
- Chcesz, aby dane toopersist z zestawów utworzonych za pomocą konfiguracji usługi w chmurze hello lub hello konfiguracji maszyny wirtualnej.
- Aplikacja kliencka lub innych zadań w hello zadania toolocate potrzeb, a pliki wyjściowe zadań za pomocą Identyfikatora lub w celu pobrania. 
- Ma tooview dane wyjściowe zadania w hello portalu Azure.

Jeśli scenariusz różni się od wymienione powyżej, może być konieczne tooconsider inny sposób. Aby uzyskać więcej informacji dotyczących innych opcji trwałych danych wyjściowych zadania, zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Co to jest hello standardowych konwencji pliku wsadowego?

Witaj [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) zawiera schemat nazewnictwa dla hello docelowego kontenerów i obiektów blob ścieżki toowhich zapisu plików wyjściowych. TooAzure utrwalonego plików magazynu, który odpowiednia toohello standardowej konwencji pliku są automatycznie dostępne do wyświetlenia w hello portalu Azure. Hello portal zna hello konwencji nazewnictwa i dlatego można wyświetlać pliki zgodnymi tooit.

Hello konwencje plików biblioteki dla platformy .NET automatycznie nazwy kontenery magazynu, a pliki wyjściowe zadań zgodnie z toohello konwencje plików standardowych. Hello konwencje plików biblioteki są także pliki wyjściowe tooquery metod w usłudze Azure Storage według Identyfikatora toojob, identyfikator zadania lub cel.   

Jeśli tworzysz języka innego niż .NET, można zaimplementować standard konwencje plików hello samodzielnie w aplikacji. Aby uzyskać więcej informacji, zobacz [temat standardowych konwencji pliku wsadowego hello](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Łącze tooyour konta usługi Azure Storage konta usługi partia zadań

toopersist magazynu przy użyciu hello konwencje plik biblioteki, należy najpierw połączyć tooyour konta usługi Azure Storage konta usługi partia zadań tooAzure danych wyjściowych. Jeśli jeszcze tego nie zrobiono tego wcześniej, łączenie tooyour konta magazynu konta usługi partia zadań za pomocą hello [portalu Azure](https://portal.azure.com):

1. Przejdź tooyour konta usługi partia zadań w hello portalu Azure. 
2. W obszarze **ustawienia**, wybierz pozycję **konta magazynu**.
3. Jeśli nie masz już konto magazynu skojarzonych z Twoim kontem usługi partia zadań, kliknij przycisk **konta magazynu, (Brak)**.
4. Wybierz konto magazynu z listy powitania dla Twojej subskrypcji. Aby uzyskać najlepszą wydajność, należy użyć konta usługi Azure Storage, który znajduje się w hello tym samym regionie co hello konta usługi partia zadań, na którym są uruchomione zadania.

## <a name="persist-output-data"></a>Utrwalić danych wyjściowych

toopersist i zadań wysyłania danych z biblioteką konwencje plików hello, utworzyć kontener w usłudze Azure Storage, a następnie zapisz hello dane wyjściowe toohello kontenera. Użyj hello [biblioteki klienta usługi Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage) w Twojej zadań kodu tooupload hello zadań dane wyjściowe toohello kontenerze. 

Aby uzyskać więcej informacji na temat pracy z kontenerów i obiektów blob w magazynie Azure, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Wszystkie dane wyjściowe poleceń i zadań utrwalone z konwencjami pliku hello biblioteki są przechowywane w samym kontenerze hello. Duża liczba zadań toopersist plików na powitania sam czas [magazynu ograniczenie](../storage/common/storage-performance-checklist.md#blobs) może wtedy zostać wymuszone.
> 
> 

### <a name="create-storage-container"></a>Tworzenie kontenera magazynu

tooAzure dane wyjściowe zadania toopersist magazynowania, najpierw utworzyć kontener wywołując [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Ta metoda rozszerzenia przyjmuje [CloudStorageAccount] [ net_cloudstorageaccount] obiektu jako parametr. Tworzy kontener o nazwie zgodnie z toohello konwencje plików standard, tak aby jego zawartość jest wykrywalny przez hello Azure portal i hello metod pobierania omówione w dalszej części artykułu hello.

Zwykle umieścić toocreate kodu hello kontener w aplikacji klienta &mdash; hello aplikacji do tworzenia z puli, zadań i zadań.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Zadanie magazynu danych wyjściowych

Teraz, gdy zostały przygotowane kontenera w magazynie Azure, zadania można zapisać danych wyjściowych toohello kontenera przy użyciu hello [TaskOutputStorage] [ net_taskoutputstorage] w bibliotece konwencje plików hello znaleziono klasy.

W kodzie zadań, należy najpierw utworzyć [TaskOutputStorage] [ net_taskoutputstorage] obiekt, a następnie po ukończeniu zadania hello pracy Wywołaj hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave metody tooAzure jego dane wyjściowe magazynu.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Witaj `kind` parametru hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) metody kategoryzuje hello utrwalone plików. Istnieją cztery wstępnie zdefiniowane [TaskOutputKind] [ net_taskoutputkind] typów: `TaskOutput`, `TaskPreview`, `TaskLog`, i `TaskIntermediate.` można również definiować niestandardowe kategorie danych wyjściowych.

Te typy danych wyjściowych pozwala toospecify, jakiego typu dane wyjściowe toolist później kwerendy partii dla hello utrwalone dane wyjściowe z danego zadania. Innymi słowy wśród wyjść hello zadania można filtrować listy hello na jeden z typów danych wyjściowych hello. Na przykład "Udostępnij hello *Podgląd* dane wyjściowe zadania *109*." Więcej informacji na temat wyświetlania i pobierania danych wyjściowych jest wyświetlana w [pobrać dane wyjściowe](#retrieve-output) dalszej części artykułu hello.

> [!TIP]
> Witaj rodzaj wyjścia decyduje również o którym w hello Azure portal określonego pliku pojawi się: *TaskOutput*-skategoryzowane pliki są wyświetlane w obszarze **pliki wyjściowe zadania**, i *TaskLog*pliki są wyświetlane w obszarze **zadań dzienniki**.
> 
> 

### <a name="store-job-outputs"></a>Dane wyjściowe zadania magazynu

Ponadto wyniki zadań toostoring, można przechowywać dane wyjściowe hello skojarzone z zadaniem całego. Na przykład w zadaniu scalania hello zadania renderowania movie, można utrwalić filmu hello pełni renderowane jako dane wyjściowe zadania. Po zakończeniu zadania aplikacji klienta, można wyświetlić listę i pobrać dane wyjściowe hello hello zadania, a jest nie wymagają tooquery hello poszczególne zadania.

Przechowywanie danych wyjściowych zadania przez wywołanie hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] metody, a następnie określ hello [JobOutputKind] [ net_joboutputkind] i nazwa pliku:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Jak hello **TaskOutputKind** typu dla danych wyjściowych zadania, możesz użyć hello [JobOutputKind] [ net_joboutputkind] toocategorize typ zadania elementu utrwalone plików. Ten parametr umożliwia toolater zapytanie dla określonego typu danych wyjściowych (lista). Witaj **JobOutputKind** typu kategoriami zarówno dane wyjściowe, jak i w wersji zapoznawczej i obsługuje tworzenie niestandardowych kategorii.

### <a name="store-task-logs"></a>Dzienniki zadania magazynu

Ponadto toopersisting magazynu toodurable plików podczas zadania lub zadania wykonuje, może być konieczne toopersist pliki, które są aktualizowane podczas wykonywania zadania hello &mdash; pliki dziennika lub `stdout.txt` i `stderr.txt`, na przykład. W tym celu hello biblioteki konwencje plików usługi partia zadań Azure udostępnia hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] metody. Z [SaveTrackedAsync][net_savetrackedasync], można śledzić pliku tooa aktualizacje w węźle hello (interwałem określonym przez użytkownika) i utrwalić tooAzure tych aktualizacji magazynu.

W hello następującego fragmentu kodu, używamy [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` w usłudze Azure Storage co 15 s podczas wykonywania zadań hello hello:

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

Witaj oznaczone jako sekcji `Code tooprocess data and produce output file(s)` to symbol zastępczy hello kod, który przeprowadza się zwykle zadania. Na przykład może być kodu, który pobiera dane z usługi Azure Storage i wykonuje przekształcenie lub obliczeń na nim. ważnym elementem Hello ta Wstawka kodu jest prezentacja jak może zawijać się taki kod w `using` tooperiodically bloku zaktualizować plik z [SaveTrackedAsync][net_savetrackedasync].

agent węzła Hello jest program, który jest uruchamiany na każdym węźle w puli hello i udostępnia interfejs polecenia i kontroli hello między węzłem hello a hello usługa partia zadań. Witaj `Task.Delay` wywołanie jest wymagane na końcu hello to `using` tooensure bloku, który hello agenta węzła ma zawartość hello tooflush czas standardowy plik stdout.txt toohello w węźle hello. Bez tego opóźnienia jest możliwe toomiss hello ostatniego kilka sekund w danych wyjściowych. Tego opóźnienia nie może być wymagane dla wszystkich plików.

> [!NOTE]
> Po włączeniu pliku śledzenia z **SaveTrackedAsync**, tylko *dołącza* pliku śledzonych toohello są tooAzure utrwalonego magazynu. Ta metoda służy tylko do śledzenia-obracanie pliki dziennika lub innych plików, które zostały napisane toowith Dołącz toohello operacje na końcu pliku hello.
> 
> 

## <a name="retrieve-output-data"></a>Pobieranie danych wyjściowych

Podczas pobierania danych wyjściowych utrwalonego za pomocą biblioteki konwencje pliku wsadowego Azure hello, w tym zadań i zadania skoncentrowane na sposób. Użytkownik może prosić o hello wyjściowe dla danego zadania lub zadania bez konieczności tooknow ścieżki w usłudze Azure Storage lub nawet jego nazwa pliku. Zamiast tego można zażądać plików wyjściowych przez zadanie lub zadania identyfikatora.

Hello poniższy fragment kodu iteruje zadania, niektóre informacje na temat plików wyjściowych hello hello zadania drukowania i pobiera pliki z magazynu.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Pliki wyjściowe widoku w hello portalu Azure

Witaj portalu Azure Wyświetla pliki wyjściowe zadań i dzienników, które są trwałe tooa połączone konta magazynu platformy Azure przy użyciu hello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Można zaimplementować te konwencje samodzielnie hello preferowanego języka lub hello konwencje plików biblioteki można używać w aplikacji platformy .NET.

tooenable hello wyświetlania plików wyjściowych w portalu hello, musi spełniać następujące wymagania hello:

1. [Łączenie konta usługi Azure Storage](#requirement-linked-storage-account) tooyour konta usługi partia zadań.
2. Odpowiednia toohello wstępnie zdefiniowane konwencje nazewnictwa dla plików i kontenery magazynu podczas przechowywanie danych wyjściowych. Można znaleźć definicji hello tych konwencji w hello konwencje plików biblioteki [README][github_file_conventions_readme]. Jeśli używasz hello [konwencje plików usługi partia zadań Azure] [ nuget_package] toopersist biblioteki z danych wyjściowych, pliki są zachowywane zgodnie z toohello standardowej konwencji pliku.

dane wyjściowe zadania tooview pliki i loguje hello portalu Azure, przejdź toohello zadań, której wyjście myślisz, następnie kliknij opcję **zapisane pliki wyjściowe** lub **zapisane dzienniki**. Ten obraz zawiera hello **zapisane pliki wyjściowe** hello zadania o identyfikatorze "007":

![Wyniki zadań bloku w hello portalu Azure][2]

## <a name="code-sample"></a>Przykład kodu

Witaj [PersistOutputs] [ github_persistoutputs] przykładowy projekt jest jednym z hello [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub. To rozwiązanie Visual Studio pokazano, jak toouse hello Azure partii pliku konwencje biblioteki toopersist zadań output toodurable magazynu. Witaj toorun przykładowe, wykonaj następujące kroki:

1. Witaj Otwórz projekt w **programu Visual Studio 2015 lub nowsza**.
2. Dodaj wsadowego i magazynowania **poświadczenia konta** za**AccountSettings.settings** w projekcie Microsoft.Azure.Batch.Samples.Common hello.
3. **Tworzenie** (ale nie jest uruchomiony) hello rozwiązania. Jeśli zostanie wyświetlony monit, należy przywrócić wszystkie pakiety NuGet.
4. Użyj hello Azure portalu tooupload [pakiet aplikacji](batch-application-packages.md) dla **PersistOutputsTask**. Zawierają hello `PersistOutputsTask.exe` i jego zestawów zależnych hello zip pakietu, identyfikator aplikacji hello zestawu zbyt wersja pakietu "PersistOutputsTask" i aplikacji hello zbyt "1.0".
5. **Uruchom** (Uruchom) hello **PersistOutputs** projektu.
6. Gdy zostanie wyświetlony monit o toochoose hello trwałości technologii toouse dla uruchomionego hello próbki, wprowadź **1** próbki hello toorun przy użyciu danych wyjściowych zadania toopersist hello konwencje plików biblioteki. 

## <a name="next-steps"></a>Następne kroki

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Pobierz hello konwencje pliku wsadowego biblioteki dla platformy .NET

Biblioteka konwencje pliku wsadowego powitania dla platformy .NET jest dostępna na [NuGet][nuget_package]. Biblioteka Hello rozszerza hello [CloudJob] [ net_cloudjob] i [CloudTask] [ net_cloudtask] klas z nowych metod. Zobacz też hello [odwołania dokumentacji](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello konwencje plików biblioteki.

Witaj [kod źródłowy] [ github_file_conventions] hello konwencje plików biblioteki są dostępne w serwisie GitHub w hello Microsoft Azure SDK dla platformy .NET repozytorium. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Eksploruj inne podejścia trwałych danych wyjściowych

- Zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md) omówienie trwałych danych zadań i zadania.
- Zobacz [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md) toolearn jak toopersist hello interfejsu API usługi partii toouse dane wyjściowe.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Pliki wyjściowe zapisane i zapisane dzienniki selektory w portalu"
[2]: ./media/batch-task-output/task-output-02.png "Wyniki zadań bloku w hello portalu Azure"
