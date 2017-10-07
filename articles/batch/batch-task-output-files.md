---
title: "aaaPersist i zadań output tooAzure magazynu z hello interfejsu API usługi partia zadań Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooAzure magazynu wyjściowe toouse interfejsu API usługi partii toopersist partii zadań i zadania."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Utrwalanie tooAzure danych zadań magazynu z hello interfejsu API usługi partii

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Począwszy od wersji 2017-05-01, hello interfejsu API partii usługi obsługuje trwałych tooAzure danych wyjściowych magazynu dla zadań i zadania Menedżer zadania, które będą uruchamiane w pulach hello konfiguracji maszyny wirtualnej. Podczas dodawania zadania jako miejsce docelowe danych wyjściowych zadania hello hello można określić kontener w usłudze Azure Storage. Witaj, usługa partia zadań, a następnie zapisuje kontenera toothat żadnych danych wyjściowych danych po zakończeniu zadania hello.

Zaletą toousing hello wyjście zadań toopersist interfejsu API usługi jest niepotrzebne aplikacji hello toomodify hello zadania wsadowego jest uruchomiona. Zamiast tego z aplikacji klienckiej tooyour kilka prostych zmian, można ją utrwalić dane wyjściowe zadania hello z kodem hello, która tworzy zadanie hello.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Kiedy używać danych wyjściowych zadania toopersist hello interfejsu API usługi partii?

Partia zadań Azure zawiera więcej niż jednym ze sposobów toopersist dane wyjściowe zadania. Używanie hello interfejsu API usługi partii jest to wygodny podejście, które są najlepiej nadaje się toothese scenariusze:

- Dane wyjściowe zadania toopersist kodu toowrite z mają w aplikacji klienta, bez modyfikowania aplikacji hello zadań jest uruchomiona.
- Chcesz, aby dane wyjściowe toopersist partii zadań i zadania Menedżer zadania w pulach utworzone za pomocą hello konfiguracji maszyny wirtualnej.
- Ma toopersist dane wyjściowe tooan usługi Azure Storage kontenera o nazwie dowolnego.
- Ma toopersist dane wyjściowe tooan kontenera magazynu Azure o nazwie zgodnie z toohello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Jeśli scenariusz różni się od wymienione powyżej, może być konieczne tooconsider inny sposób. Na przykład interfejsu API usługi partii hello aktualnie nie obsługuje przesyłania strumieniowego tooAzure dane wyjściowe magazynu podczas wykonywania zadania hello. dane wyjściowe toostream, należy rozważyć użycie biblioteki konwencje pliku wsadowego hello, dostępna dla platformy .NET. W przypadku języków musisz tooimplement własne rozwiązania. Aby uzyskać więcej informacji dotyczących innych opcji trwałych danych wyjściowych zadania, zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Tworzenie kontenera w usłudze Azure Storage

zadanie toopersist output tooAzure magazynu, musisz toocreate kontener, który służy jako docelowy hello plików wyjściowych. Tworzenie kontenera hello, najlepiej uruchomienia zadania, aby przesłać zadanie. kontener hello toocreate, użyj hello odpowiedniej biblioteki klienta magazynu Azure lub zestawu SDK. Aby uzyskać więcej informacji na temat interfejsy API usługi Azure Storage, zobacz hello [dokumentację usługi Azure Storage](https://docs.microsoft.com/azure/storage/).

Na przykład podczas pisania aplikacji w języku C#, użyj hello [biblioteki klienta usługi Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). powitania po przykładzie pokazano, jak toocreate kontener:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Uzyskiwanie sygnatury dostępu współdzielonego dla kontenera hello

Po utworzeniu kontenera hello uzyskiwanie sygnatury dostępu współdzielonego (SAS), z kontenerem toohello dostęp do zapisu. Sygnatury dostępu Współdzielonego zapewnia dostęp delegowany toohello kontener. Witaj SAS udziela dostępu z określonego zestawu uprawnień i w określonym przedziale czasu. Usługa partia zadań Hello musi SAS z kontenerem toohello dane wyjściowe zadania. toowrite uprawnień zapisu. Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego, zobacz [używanie sygnatury dostępu współdzielonego \(SAS\) w usłudze Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Po wyświetleniu okna sygnatury dostępu Współdzielonego przy użyciu hello interfejsy API usługi Azure Storage, hello interfejsu API zwraca ciąg tokenu sygnatury dostępu Współdzielonego. Ten ciąg tokenu zawiera wszystkie parametry hello SAS, w tym uprawnienia hello i interwał powitania za pośrednictwem których hello SAS jest prawidłowy. toouse hello SAS tooaccess kontenera w magazynie Azure, należy tooappend hello SAS ciąg tokenu toohello identyfikator URI zasobu. zasób Hello identyfikatora URI, wraz z hello dołączany tokenu sygnatury dostępu Współdzielonego, zapewnia uwierzytelniony dostęp tooAzure magazynu.

Witaj poniższy przykład pokazuje, jak ciąg hello kontenera tokenu tooget SAS tylko do zapisu, a następnie dołącza hello SAS toohello kontenera identyfikatora URI:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Określ plików wyjściowych dla danych wyjściowych zadania

pliki wyjściowe toospecify zadania, utworzyć kolekcję [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) obiekty i przypisać je toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) właściwości po utworzeniu zadania hello. 

Witaj poniższy przykład kodu .NET tworzy zadanie, które zapisuje liczb losowych tooa plik o nazwie `output.txt`. przykład Witaj tworzy plik wyjściowy do `output.txt` toobe zapisywane toohello kontenera. przykład Witaj tworzy także plików wyjściowych dla wszystkie pliki dziennika, które jest zgodny z wzorcem pliku hello `std*.txt` (_np._, `stdout.txt` i `stderr.txt`). adresu URL kontenera Hello wymaga hello sygnatury dostępu Współdzielonego, który został utworzony wcześniej hello kontenera. Witaj usługa partia zadań używa hello SAS tooauthenticate dostępu toohello kontenera: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Określ wzorzec pliku do dopasowania

Po określeniu pliku wyjściowego, można użyć hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) toospecify właściwości wzorzec pliku do dopasowania. wzorzec pliku Hello zgadzają zero pliki, pojedynczego pliku lub zestawu plików, które są tworzone przez zadanie hello.

Hello **FilePattern** właściwość obsługuje standardowe plików symboli wieloznacznych `*` (dla innych niż cykliczne zgodna) i `**` (dla cyklicznego zgodna). Na przykład w powyższym przykładowym kodzie hello określa toomatch wzorzec pliku hello `std*.txt` lokalizacji: 

`filePattern: @"..\std*.txt"`

tooupload jednego pliku, określ wzorzec pliku bez symboli wieloznacznych. Na przykład powyższym przykładowym kodzie hello określa hello pliku wzorca toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Określ warunek przekazywania

Witaj [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) właściwości zezwala na przekazywanie warunkowego plików wyjściowych. Typowy scenariusz obejmuje tooupload jeden zestaw plików w przypadku pomyślnego zakończenia zadania hello i inny zestaw plików, jeśli działanie nie powiodło się. Na przykład możesz plików pełnego dziennika tooupload tylko wtedy, gdy hello zadań kończy się niepowodzeniem i kończy działanie z kodem zakończenia różną od zera. Podobnie można plików wyników tooupload tylko wtedy, gdy zadanie hello powiedzie się, jak te pliki mogą być brakujące lub niekompletne, jeśli zadanie hello nie powiedzie się.

Witaj powyższy kod przykładowy ustawia hello **UploadCondition** właściwości zbyt**TaskCompletion**. To ustawienie określa, czy plik hello jest toobe przekazany po zakończeniu zadania hello, niezależnie od wartości hello hello kodu zakończenia. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

W przypadku innych ustawień, zobacz hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) wyliczenia.

### <a name="disambiguate-files-with-hello-same-name"></a>Pliki z hello odróżniania samej nazwie

Witaj zadań w ramach zadania może tworzyć pliki, których hello tej samej nazwy. Na przykład `stdout.txt` i `stderr.txt` są tworzone dla każdego zadania w ramach zadania. Ponieważ każde zadanie jest uruchamiane w kontekście jego własnej, pliki te nie powodują konflikt w systemie plików hello węzła. Jednak podczas przekazywania plików z wielu zadań tooa udostępnionego kontenera należy toodisambiguate pliki z hello tej samej nazwy.

Witaj [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) właściwość określa hello docelowego obiektu blob lub katalog wirtualny dla plików wyjściowych. Można użyć hello **ścieżki** właściwości tooname hello blob lub katalogu wirtualnego w taki sposób, że dane wyjściowe pliki z hello jednoznacznie noszą tej samej nazwy w usłudze Azure Storage. Za pomocą Identyfikatora zadania hello w ścieżce hello jest tooensure dobrze unikatowe nazwy i łatwo zidentyfikować plików.

Jeśli hello **FilePattern** właściwość ma wartość wyrażenia z symbolami wieloznacznymi tooa, a następnie wszystkie pliki, które jest zgodny z wzorcem hello są określony przez hello katalog wirtualny przekazane toohello **ścieżki** właściwości. Na przykład, jeśli hello kontener jest `mycontainer`, zadanie hello jest identyfikator `mytask`, i wzorzec pliku hello jest `..\std*.txt`, następnie hello bezwzględną pliki wyjściowe toohello identyfikatorów URI w usłudze Azure Storage będą wyglądać podobnie do:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Jeśli hello **FilePattern** właściwość toomatch zestaw jedna nazwa pliku, co oznacza nie zawiera żadnych symboli wieloznacznych, następnie hello wartość hello **ścieżki** właściwość określa hello obiektów blob w pełni kwalifikowana nazwa . Jeśli przewidujesz konflikty nazw z jednego pliku z wielu zadań, następnie wprowadzić nazwę katalogu wirtualnego hello hello jako część toodisambiguate nazwę pliku hello tych plików. Na przykład zestaw hello **ścieżki** właściwości tooinclude hello zadania o identyfikatorze, hello znak ogranicznika (zazwyczaj ukośnikiem) i nazwa pliku hello:

`path: taskId + @"/output.txt"`

Hello bezwzględny identyfikator URI toohello plików wyjściowych dla zestawu zadań będą wyglądać podobnie do:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Aby uzyskać więcej informacji na temat katalogów wirtualnych w usłudze Azure Storage, zobacz [listy hello BLOB w kontenerze](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnozowanie błędów przekazywania plików

Jeśli przekazywanie danych wyjściowych pliki tooAzure magazynu kończy się niepowodzeniem, a następnie zadanie hello przenosi toohello **Ukończono** stanu i hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) właściwość jest ustawiona. Sprawdź hello **FailureInformation** toodetermine właściwości jakie błąd. Na przykład w tym miejscu jest błąd występujący podczas przekazywania pliku, jeśli nie można odnaleźć kontenera hello: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

Na każdym przekazywania pliku wsadowego zapisuje dziennika dwa pliki toohello węźle obliczeń, `fileuploadout.txt` i `fileuploaderr.txt`. Możesz przejrzeć te pliki dziennika toolearn więcej informacji na temat określonego błędu. W przypadkach, gdy przekazywania pliku hello nigdy nie podjęto, na przykład ponieważ nie można uruchomić samo zadanie hello następnie te pliki dziennika nie istnieje.

## <a name="diagnose-file-upload-performance"></a>Diagnozowanie wydajność przekazywania pliku

Witaj `fileuploadout.txt` plików dzienników postępu przekazywania. Można sprawdzić toolearn tego pliku, który trwa więcej informacji na temat czas przekazywania pliku. Należy pamiętać, że istnieje wiele czynników tooupload wydajności, w tym rozmiar hello hello węzła, innych działań w węźle hello w czasie hello przekazywania hello kontenera docelowego hello w hello są liczbę węzłów w tym samym regionie co hello puli partii, przekazywanie toohello konta magazynu na powitania sam czas i tak dalej.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Interfejs API usługi partii hello za pomocą hello standardowych konwencji pliku wsadowego

Można utrwalić danych wyjściowych zadania z hello interfejsu API partii usługi, należy określić nazwę użytkownika docelowy kontener i obiektów blob, jednak chcesz. Możesz również tooname je zgodnie z toohello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). standard konwencje plików Hello określa nazwy hello hello docelowy kontener i obiektów blob w usłudze Azure Storage dla pliku wyjściowego danego na podstawie nazw hello hello zadań i zadań. Jeśli należy używać hello konwencje plików standard nazewnictwa plików wyjściowych, a następnie Twoje pliki wyjściowe są dostępne do wyświetlenia w hello [portalu Azure](https://portal.azure.com).

Jeśli tworzysz w języku C#, można użyć metody hello wbudowane hello [biblioteki konwencje pliku wsadowego dla platformy .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Ta biblioteka tworzy hello poprawnie o nazwie kontenerów i obiektów blob ścieżki dla Ciebie. Na przykład można wywołać hello interfejsu API tooget hello poprawną nazwę kontenera hello, na podstawie nazwy zadania hello:

```csharp
string containerName = job.OutputStorageContainerName();
```

Można użyć hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) tooreturn metody adres URL sygnatury dostępu Współdzielonego dostępu współdzielonego, który jest używany toowrite toohello kontenera. Można następnie przekazać ten toohello SAS [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) konstruktora.

Jeśli tworzysz w języku innym niż C#, konieczne będzie tooimplement hello konwencje plików standard samodzielnie.

## <a name="code-sample"></a>Przykład kodu

Witaj [PersistOutputs] [ github_persistoutputs] przykładowy projekt jest jednym z hello [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub. To rozwiązanie Visual Studio pokazano, jak biblioteki klienta toouse hello partii zadań dla zadania toopersist .NET output toodurable magazynu. Witaj toorun przykładowe, wykonaj następujące kroki:

1. Witaj Otwórz projekt w **programu Visual Studio 2015 lub nowsza**.
2. Dodaj wsadowego i magazynowania **poświadczenia konta** za**AccountSettings.settings** w projekcie Microsoft.Azure.Batch.Samples.Common hello.
3. **Tworzenie** (ale nie jest uruchomiony) hello rozwiązania. Jeśli zostanie wyświetlony monit, należy przywrócić wszystkie pakiety NuGet.
4. Użyj hello Azure portalu tooupload [pakiet aplikacji](batch-application-packages.md) dla **PersistOutputsTask**. Zawierają hello `PersistOutputsTask.exe` i jego zestawów zależnych hello zip pakietu, identyfikator aplikacji hello zestawu zbyt wersja pakietu "PersistOutputsTask" i aplikacji hello zbyt "1.0".
5. **Uruchom** (Uruchom) hello **PersistOutputs** projektu.
6. Gdy zostanie wyświetlony monit o toochoose hello trwałości technologii toouse dla uruchomionego hello próbki, wprowadź **2** toorun hello próbki, przy użyciu danych wyjściowych zadania toopersist hello interfejsu API usługi partii.
7. W razie potrzeby próbki hello ponownie uruchomić, wprowadzania **3** toopersist wyjście z interfejsu API usługi partii hello i tooname hello i kontener obiektów blob ścieżki docelowej zgodnie z toohello konwencje plików standardowych.

## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji na trwałych danych wyjściowych zadania z hello konwencje plików biblioteki dla platformy .NET, zobacz [utrwalić i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist ](batch-task-output-file-conventions.md).
- Aby uzyskać informacje na inne podejścia trwałych danych wyjściowych w partii zadań Azure, zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
