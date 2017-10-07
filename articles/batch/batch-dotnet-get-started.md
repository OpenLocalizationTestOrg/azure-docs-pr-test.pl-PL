---
title: "aaaTutorial — Biblioteka klienta użyj hello partii zadań Azure dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu platformy .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Rozpoczynanie pracy kompilowanie rozwiązań za pomocą biblioteki klienta hello partii dla platformy .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Dowiedz się podstawy hello [partii zadań Azure] [ azure_batch] i hello [partiami platformy .NET] [ net_api] biblioteki w tym artykule jako omówimy C# przykładowej aplikacji krok przez krok. Przyjrzymy się jak hello Przykładowa aplikacja korzysta z tooprocess usługi partii hello równoległych obciążenia w chmurze hello i sposób interakcji z [usługi Azure Storage](../storage/common/storage-introduction.md) potrzeby przemieszczania plików i odzyskiwania. Będzie informacje wspólnego przepływu pracy aplikacji partii i Uzyskaj podstawową wiedzę na temat hello głównych składników usługi partia zadań takich jak zadania, zadania, pul i węzły obliczeniowe.

![Przepływ pracy rozwiązania w usłudze Batch (podstawowy)][11]<br/>

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że masz praktyczną wiedzę na temat języka C# i programu Visual Studio. Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello partii i usługi magazynu.

### <a name="accounts"></a>Konta
* **Konto platformy Azure**: jeśli nie masz jeszcze subskrypcji platformy Azure, [utwórz bezpłatne konto platformy Azure][azure_free_account].
* **Konto usługi Batch**: po uzyskaniu subskrypcji platformy Azure [utwórz konto usługi Azure Batch](batch-account-create-portal.md).
* **Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Obecnie partii obsługuje *tylko* hello **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku #5 [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w [o Azure konta magazynu](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Musi mieć **programu Visual Studio 2015 lub nowsza** toobuild hello przykładowy projekt. Bezpłatne i wersji próbnej wersji programu Visual Studio można znaleźć w hello [omówienie produktów Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>Przykład kodu *DotNetTutorial*
Witaj [DotNetTutorial] [ github_dotnettutorial] próbki jest jednym z hello wiele przykładów kodu partii znaleziony w hello [azure partii próbek] [ github_samples] repozytorium na GitHub. Wszystkie próbki hello można pobrać po kliknięciu **klonowania lub pobierania > Pobierz ZIP** na stronie głównej repozytorium hello lub przez kliknięcie przycisku hello [azure partii — przykłady master.zip] [ github_samples_zip]łącze bezpośrednie. Po zostały wyodrębnione hello zawartość pliku ZIP hello, można znaleźć rozwiązania hello w hello następującego folderu:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch Explorer (opcjonalnie)
Witaj [Eksploratora usługi partia zadań Azure] [ github_batchexplorer] to bezpłatne narzędzie, które znajduje się w hello [azure partii próbek] [ github_samples] repozytorium w witrynie GitHub. Podczas toocomplete nie wymaga tego samouczka, może być przydatne podczas opracowywania i debugowania rozwiązań partii.

## <a name="dotnettutorial-sample-project-overview"></a>Omówienie przykładowego projektu DotNetTutorial
Witaj *DotNetTutorial* przykładowy kod jest rozwiązaniem Visual Studio, która zawiera dwa projekty: **DotNetTutorial** i **TaskApplication**.

* **DotNetTutorial** jest aplikacją kliencką hello, która współdziała z tooexecute hello partii i magazynu usług równoległych obciążenie obliczeniowe węzłach (maszynach wirtualnych). Aplikacja DotNetTutorial jest uruchamiana na lokalnej stacji roboczej.
* **TaskApplication** to program hello, który jest uruchamiany na węzłach obliczeniowych Azure tooperform hello rzeczywistą pracę. W przykładowym hello `TaskApplication.exe` analizuje hello tekst w pliku, który został pobrany z usługi Azure Storage (plik wejściowy hello). Następnie tworzy plik tekstowy (plik wyjściowy hello) zawierający listę hello trzy najważniejsze wyrazy, które pojawiają się w pliku wejściowym hello. Po utworzeniu pliku wyjściowego hello, TaskApplication przekazuje hello tooAzure pliku magazynu. Dzięki temu aplikacja kliencka toohello dostępne do pobrania. TaskApplication uruchamia się równolegle na wielu węzłach obliczeniowych w hello usługa partia zadań.

Witaj poniższym diagramie przedstawiono hello głównej operacje, które są wykonywane przez aplikację kliencką hello, *DotNetTutorial*i aplikacji hello, która jest wykonywana przez zadania hello *TaskApplication*. Ten podstawowy przepływ pracy jest typowy dla wielu rozwiązań obliczeniowych utworzonych za pomocą usługi Batch. Gdy nie wykazują wszystkich funkcji dostępnych w hello usługa partia zadań, niemal każdego scenariusza partii zawiera części ten przepływ pracy.

![Przykładowy przepływ pracy w usłudze Batch][8]<br/>

[**Krok 1.**](#step-1-create-storage-containers) Utwórz **kontenery** w usłudze Azure Blob Storage.<br/>
[**Krok 2.**](#step-2-upload-task-application-and-data-files) Pliki aplikacji zadania przekazywania i toocontainers plików wejściowych.<br/>
[**Krok 3.**](#step-3-create-batch-pool) Utwórz **pulę** w usłudze Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Witaj puli **StartTask** pliki do pobrania hello toonodes pliki binarne (TaskApplication) zadań zgodnie z ich przyłączyć hello puli.<br/>
[**Krok 4.**](#step-4-create-batch-job) Utwórz **zadanie** w usłudze Batch.<br/>
[**Krok 5.**](#step-5-add-tasks-to-job) Dodaj **zadania** toohello zadania.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** zadania Hello są zaplanowane tooexecute na węzłach.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Każde zadanie pobiera dane wejściowe z usługi Azure Storage, a następnie rozpoczyna się wykonywanie.<br/>
[**Krok 6.**](#step-6-monitor-tasks) Monitoruj podzadania.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Jak czynności zostały wykonane, ich przekazywanie ich tooAzure danych wyjściowych magazynu.<br/>
[**Krok 7.**](#step-7-download-task-output) Pobierz dane wyjściowe podzadań z usługi Storage.

Jak wspomniano, nie każde rozwiązanie z partii wykonuje te kroki szczegółowe może obejmować wiele innych, ale hello *DotNetTutorial* aplikacja przykładowa prezentuje często używanych procesów, które można odnaleźć w rozwiązaniu partii.

## <a name="build-hello-dotnettutorial-sample-project"></a>Tworzenie hello *DotNetTutorial* przykładowy projekt
Można było pomyślnie uruchomić hello próbki, należy określić poświadczenia konta zarówno wsadowego i magazynowania w hello *DotNetTutorial* projektu `Program.cs` pliku. Jeśli jeszcze tego nie zrobiono, otwórz rozwiązanie hello w programie Visual Studio, klikając hello `DotNetTutorial.sln` pliku rozwiązania. Lub otworzyć z poziomu programu Visual Studio za pomocą hello **Plik > Otwórz > Projekt/rozwiązanie** menu.

Otwórz `Program.cs` w hello *DotNetTutorial* projektu. Następnie dodaj poświadczeń określonych hello górze pliku hello:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Jak wspomniano powyżej, obecnie należy określić poświadczenia hello **ogólnego przeznaczenia** konta magazynu w usłudze Azure Storage. Aplikacje partii używać magazynu obiektów blob w ramach hello **ogólnego przeznaczenia** konta magazynu. Nie określaj hello poświadczenia dla konta magazynu, który został utworzony przez wybranie hello *magazynu obiektów Blob* typ konta.
>
>

Poświadczenia konta wsadowego i magazynowania w bloku konta hello każdej usługi można znaleźć w hello [portalu Azure][azure_portal]:

![Partii poświadczeń w portalu hello][9]
![magazynu poświadczeń w portalu hello][10]<br/>

Po zaktualizowaniu hello projektu przy użyciu poświadczeń, kliknij prawym przyciskiem myszy rozwiązanie hello w Eksploratorze rozwiązań i kliknij przycisk **Kompiluj rozwiązanie**. Witaj przywracania pakietów NuGet, upewnij się, jeśli zostanie wyświetlony monit.

> [!TIP]
> Jeśli nie przywrócono automatycznie pakietów NuGet hello lub zobacz błędy dotyczące pakietów hello toorestore błąd, upewnij się, że masz hello [Menedżera pakietów NuGet] [ nuget_packagemgr] zainstalowane. Włącz pobieranie brakujących pakietów hello. Zobacz [włączenie pakietu przywrócić podczas kompilacji] [ nuget_restore] tooenable Pobieranie pakietu.
>
>

W hello następujące sekcje możemy podzielić hello przykładowej aplikacji na powitania kroki wykonuje tooprocess obciążenia w hello usługa partia zadań i te kroki szczegółowo omówiono w nim. Firma Microsoft zachęca toorefer toohello Otwórz rozwiązanie w programie Visual Studio podczas pracy swojemu za pośrednictwem hello dalszej części tego artykułu, ponieważ nie każdy wiersz kodu w przykładowym hello jest omówiona.

Przejdź do góry toohello hello `MainAsync` metoda hello *DotNetTutorial* projektu `Program.cs` pliku toostart z kroku 1. Każdy krok poniżej, a następnie około odwołuje się postępu hello następujące metody `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Krok 1: tworzenie kontenerów w usłudze Storage
![Tworzenie kontenerów w usłudze Azure Storage][1]
<br/>

Usługa Batch ma wbudowaną funkcję obsługi interakcji z usługą Azure Storage. Kontenery na koncie magazynu będzie udostępniać hello pliki wymagane przez hello zadania, które są uruchamiane na koncie usługi partia zadań. kontenery Hello udostępniają danych wyjściowych hello toostore miejsce, który tworzy hello zadania. Po pierwsze Hello hello *DotNetTutorial* jest aplikacja kliencka jest utworzyć trzy kontenery w [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md):

* **Aplikacja**: ten kontener zapisze aplikacji hello uruchamiając hello zadania, jak również żadnego z jego zależności, takich jak biblioteki dll.
* **wejściowy**: zadań pobierze tooprocess pliki danych hello z hello *wejściowych* kontenera.
* **dane wyjściowe**: gdy zadania ukończyć przetwarzania pliku wejściowego, przekaże one hello wyniki toohello *dane wyjściowe* kontenera.

W kolejności toointeract z magazynu kont i Utwórz kontenerów, używamy hello [biblioteki klienta magazynu Azure dla platformy .NET][net_api_storage]. Możemy utworzyć konto toohello odwołanie z [CloudStorageAccount][net_cloudstorageaccount]i na którym utworzyć [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Używamy hello `blobClient` odwołania w całej aplikacji hello i przekaż go jako parametru metody tooseveral. Na przykład znajduje się w bloku kodu hello poniższą hello powyżej, w którym nazywa się `CreateContainerIfNotExistAsync` tooactually utworzyć hello kontenerów.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Po utworzeniu hello kontenery aplikacji hello teraz przekazać hello pliki, które będą używane przez zadania hello.

> [!TIP]
> [Jak toouse magazynu obiektów Blob z .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) zawiera omówienie pracy z usługą Azure Storage kontenerów i obiektów blob. Po rozpoczęciu pracy z instancją powinno być hello górze listy odczytu.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Krok 2: przekazanie aplikacji podzadań i plików danych
![Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers][2]
<br/>

W pliku hello Przekaż operacji *DotNetTutorial* najpierw definiuje kolekcji **aplikacji** i **wejściowych** pliku ścieżki istniejących na komputerze lokalnym hello. Następnie przekazanie tych kontenerach toohello pliki, które zostały utworzone w poprzednim kroku hello.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Istnieją dwie metody w `Program.cs` który są zaangażowane w procesu przekazywania hello:

* `UploadFilesToContainerAsync`: Ta metoda zwraca kolekcję [ResourceFile] [ net_resourcefile] obiektów (opisanych poniżej) i wewnętrznie wywołania `UploadFileToContainerAsync` tooupload każdego pliku przekazano hello *filePaths* parametru.
* `UploadFileToContainerAsync`: Ta metoda hello faktycznie wykonuje hello przekazywania pliku i tworzy hello jest [ResourceFile] [ net_resourcefile] obiektów. Po przekazaniu pliku hello, uzyskuje sygnatury dostępu współdzielonego (SAS) dla pliku hello i zwraca obiekt ResourceFile, który reprezentuje go. Sygnatury dostępu współdzielonego zostały również omówione poniżej.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ net_resourcefile] zawiera zadania w partii hello adresu URL tooa plik z magazynu Azure, który jest pobrany tooa węźle obliczeń przed uruchomieniem tego zadania. Witaj [ResourceFile.BlobSource] [ net_resourcefile_blobsource] właściwość określa hello pełny adres URL pliku hello, ponieważ znajduje się ona w magazynie Azure. adres URL Hello mogą również obejmować sygnatury dostępu współdzielonego (SAS) zawiera plik toohello bezpiecznego dostępu. Większość typów podzadań w usłudze Batch dla platformy .NET obejmuje właściwość *ResourceFiles*, w tym następujące elementy:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

DotNetTutorial Przykładowa aplikacja Hello używają hello JobPreparationTask lub JobReleaseTask typy zadań, lecz więcej o nich w [węzły obliczeniowe uruchamianie działań przygotowania i kończenia zadania w partii zadań Azure](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Sygnatura dostępu współdzielonego (SAS)
Ciągi są sygnatury dostępu współdzielonego, który — gdy dołączone jako część adresu URL — Podaj toocontainers bezpiecznego dostępu i obiekty BLOB w usłudze Azure Storage. Hello DotNetTutorial aplikacja korzysta z obu obiektów blob i kontener udostępnionych adresów URL sygnatury dostępu i pokazano, jak tooobtain te udostępniane dostęp ciągi podpisu z hello usługi magazynu.

* **Obiekt blob sygnatur dostępu współdzielonego**: hello puli StartTask w DotNetTutorial korzysta z sygnatur dostępu do udostępnionego obiektu blob podczas pobierania plików binarnych aplikacji hello i pliki danych wejściowych z magazynu (zobacz krok nr 3 poniżej). Witaj `UploadFileToContainerAsync` metody w jego DotNetTutorial `Program.cs` zawiera hello kod, który uzyskuje sygnatury dostępu współdzielonego każdy obiekt blob. Odbywa się to przez wywołanie metody [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Kontener sygnatury dostępu współdzielonego**: zgodnie z każdego zadania zakończy pracę w węźle obliczeń hello, zostanie przesłany jego dane wyjściowe pliku toohello *dane wyjściowe* kontenera w magazynie Azure. toodo, TaskApplication używa kontenera sygnatury dostępu współdzielonego, która zapewnia kontener toohello dostęp do zapisu jako część ścieżki hello, gdy jego przekazuje plik hello. Uzyskiwanie sygnatury dostępu współdzielonego kontenera hello odbywa się w podobny sposób jak podczas uzyskiwania blob hello udostępnionych sygnatury dostępu. W DotNetTutorial, możesz znaleźć tego hello `GetContainerSasUrl` wywołania metody pomocnika [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo tak. Będzie przeczytać więcej informacji o używaniu kontenera hello TaskApplication udostępnionych sygnatury dostępu w "krok 6: zadań monitorowania."

> [!TIP]
> Wyewidencjonowanie hello dwuczęściową serii na sygnatur dostępu współdzielonego [część 1: hello Opis udostępnionych model sygnatury dostępu Współdzielonego dostępu](../storage/common/storage-dotnet-shared-access-signature-part-1.md) i [część 2: tworzenie i używanie sygnatury dostępu współdzielonego (SAS) z magazynu obiektów Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn więcej informacji na temat zapewnianie bezpiecznego dostępu toodata na koncie magazynu.
>
>

## <a name="step-3-create-batch-pool"></a>Krok 3: tworzenie puli usługi Batch
![Tworzenie puli usługi Batch][3]
<br/>

**Pula** usługi Batch jest kolekcją węzłów obliczeniowych (maszyn wirtualnych), w których usługa Batch wykonuje podzadania danego zadania.

Po przekazaniu aplikacji hello i toohello pliki danych konta magazynu z interfejsami API magazynu Azure, *DotNetTutorial* rozpoczyna wprowadzanie usługa partia zadań toohello wywołania z interfejsów API dostarczonych przez hello biblioteki partiami platformy .NET. Witaj kod najpierw tworzy [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Następnie próbki hello tworzona jest pula węzłów obliczeniowych w hello konta usługi partia zadań przy użyciu wywołania zbyt`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`używa hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] toocreate metody nowej puli w hello usługa partia zadań:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Po utworzeniu puli z [CreatePool][net_pool_create], można określić kilka parametrów, takich jak hello liczba węzłów obliczeniowych hello [rozmiar węzłów hello](../cloud-services/cloud-services-sizes-specs.md), i hello operacyjnego węzłów System. W *DotNetTutorial*, używamy [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify systemu Windows Server 2012 R2 z [usługi w chmurze](../cloud-services/cloud-services-guestos-update-matrix.md). 

Można również tworzyć pule węzły obliczeniowe, które są maszynach wirtualnych Azure (VM), określając hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] dla użytkownika. Pulę węzłów obliczeniowych maszyn wirtualnych można utworzyć na podstawie [obrazów systemu Linux](batch-linux-nodes.md) lub Windows. Źródło Hello obrazów maszyny Wirtualnej można:

- Hello [Marketplace maszyny wirtualne Azure][vm_marketplace], co umożliwia obrazów systemów Windows i Linux, które są gotowe do użycia. 
- Obraz niestandardowy przygotowywany i udostępniany przez użytkownika. Aby uzyskać szczegółowe informacje o obrazach niestandardowych, zobacz [Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch](batch-api-basics.md#pool).

> [!IMPORTANT]
> W usłudze Batch opłaty są naliczane za zasoby obliczeniowe. koszty toominimize można obniżyć `targetDedicatedComputeNodes` too1 przed uruchomieniem hello próbki.
>
>

Wraz z tych właściwości węzła fizycznego, można również określić [StartTask] [ net_pool_starttask] hello puli. Hello StartTask wykonywane na każdym węźle, ponieważ ten węzeł dołącza hello puli i każdym uruchomieniu węzła. Witaj StartTask jest szczególnie przydatna w przypadku instalowania aplikacji na węzły obliczeniowe wcześniejsze toohello wykonywanie zadań. Na przykład zadań przetwarzania danych przy użyciu skryptów języka Python, można użyć tooinstall StartTask Python na powitania węzłów obliczeniowych.

W tej przykładowej aplikacji hello StartTask kopiuje hello pliki, które pobiera z magazynu (które są określane przy użyciu hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] właściwości) z hello StartTask pracy katalogu toohello udostępnionego katalogu który *wszystkie* zadań uruchomionych w węźle hello może uzyskać dostęp. Zasadniczo spowoduje to skopiowanie `TaskApplication.exe` i jego zależności toohello udostępniony katalog w każdym węźle jako węzeł hello dołącza pulę hello tak, aby wszystkie zadania, które będą uruchamiane w węźle hello do niego dostęp.

> [!TIP]
> Witaj **pakietów aplikacji** funkcji partii zadań Azure zapewnia inny sposób tooget na powitania węzłów obliczeniowych w puli aplikacji. Zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md) szczegółowe informacje.
>
>

Godny uwagi we fragmencie kodu hello powyżej jest również użycie Witaj dwie zmienne środowiskowe w hello *CommandLine* właściwości hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` i `%AZ_BATCH_NODE_SHARED_DIR%`. Każdy węzeł obliczeniowy w puli partii jest automatycznie konfigurowany z kilku zmiennych środowiskowych, które są określone tooBatch. Żaden proces, która jest wykonywana przez zadanie ma zmienne środowiskowe toothese dostępu.

> [!TIP]
> toofind więcej informacji na temat hello zmiennych środowiskowych, które są dostępne w węzłach obliczeń w puli partii i informacji na temat zadań katalogów roboczych, zobacz hello [ustawienia środowiska dla zadań](batch-api-basics.md#environment-settings-for-tasks) i [plików i katalogów ](batch-api-basics.md#files-and-directories) części hello [Przegląd funkcji partii dla deweloperów](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Krok 4: tworzenie zadania w usłudze Batch
![Tworzenie zadania w usłudze Batch][4]<br/>

**Zadanie** usługi Batch jest kolekcją podzadań i jest skojarzone z pulą węzłów obliczeniowych. wykonanie Hello zadań w ramach zadania w węzłach obliczeń puli hello skojarzone.

Można użyć zadania nie tylko do organizowaniu i śledzenia zadań w powiązanych obciążeń pracą, ale nakładaniu pewne ograniczenia — takie jak hello maksymalną czasu wykonywania zadania hello (i przez rozszerzenie, jego zadań podrzędnych), a także priorytet zadania w zadaniach tooother relacji hello partii konto. W tym przykładzie jednak hello zadanie jest skojarzone tylko z pulą hello, który został utworzony w kroku #3. Żadne dodatkowe właściwości nie są konfigurowane.

Wszystkie zadania usługi Batch są skojarzone z określoną pulą. To skojarzenie wskazuje węzły, które hello zadania będą wykonywane na. Określ to przy użyciu hello [CloudJob.PoolInformation] [ net_job_poolinfo] właściwości, jak pokazano w hello poniższy fragment kodu.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Teraz, kiedy zadania został utworzony, zadania są dodawane tooperform hello pracy.

## <a name="step-5-add-tasks-toojob"></a>Krok 5: Dodawanie toojob zadań
![Dodaj toojob zadań][5]<br/>
*(1) zadania są dodawane toohello zadania, zadania (2) hello są zaplanowane toorun w węzłach i (3) hello zadania Pobierz tooprocess pliki danych hello*

Wsadowe **zadania** są hello poszczególnych jednostek pracy wykonywanych na powitania węzły obliczeniowe. Zadanie ma wiersza polecenia i uruchamia hello skrypty lub pliki wykonywalne, w tym wierszu polecenia.

tooactually wykonywania pracy, zadań, należy dodać tooa zadania. Każdy [CloudTask] [ net_task] jest konfigurowana przy użyciu właściwości wiersza polecenia i [ResourceFiles] [ net_task_resourcefiles] (tak jak StartTask hello puli) który zadanie Hello pobiera węzła toohello przed jego wiersza polecenia jest wykonywane automatycznie. W hello *DotNetTutorial* przykładowy projekt, każde zadanie przetwarza tylko jeden plik. W związku z tym jego kolekcja ResourceFiles zawiera jeden element.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Podczas uzyskiwania dostępu do zmiennych środowiskowych takich jak `%AZ_BATCH_NODE_SHARED_DIR%` lub wykonywanie aplikacji nie można odnaleźć w węźle hello `PATH`, wiersze poleceń zadań musi być poprzedzona znakiem `cmd /c`. Zostanie jawnie wykonania hello interpreter poleceń i poinstruować go tooterminate po przeprowadzeniu polecenia. To wymaganie nie jest konieczne, jeśli zadania wykonywania aplikacji w węźle hello `PATH` (takich jak *robocopy.exe* lub *powershell.exe*) i są używane nie zmiennych środowiskowych.
>
>

W ramach hello `foreach` pętli we fragmencie kodu hello powyżej, zobaczysz, że hello wiersz polecenia dla zadania hello jest tworzony w taki sposób, że trzech argumentów wiersza polecenia są przekazywane za*TaskApplication.exe*:

1. Witaj **pierwszy argument** to ścieżka hello hello tooprocess pliku. To jest plik toohello ścieżka lokalna hello, ponieważ znajduje się w węźle hello. Gdy hello obiektu ResourceFile w `UploadFileToContainerAsync` została pierwotnie utworzona powyżej, nazwa pliku hello została użyta dla tej właściwości (jako parametru konstruktora ResourceFile toohello). Wskazuje, czy plik hello znajdują się w hello takie same katalogu jako *TaskApplication.exe*.
2. Witaj **drugi argument** Określa, że top hello *N* wyrazy mają być zapisywane toohello pliku wyjściowego. W przykładowym hello to jest ustalony, aby top trzy słowa hello są zapisywane toohello pliku wyjściowego.
3. Witaj **trzeci argument** jest sygnatury dostępu współdzielonego hello (SAS), która zapewnia dostęp do zapisu toohello **dane wyjściowe** kontenera w magazynie Azure. *TaskApplication.exe* używa tego wspólnego dostępu podpisu adresu URL, gdy przekazuje on tooAzure pliku wyjściowego hello magazynu. Witaj kodu dla tego można znaleźć w hello `UploadFileToContainer` metody w projekcie TaskApplication hello `Program.cs` pliku:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Krok 6: monitorowanie podzadań
![Monitorowanie podzadań][6]<br/>
*powitania klienta aplikacji (1) monitory hello zadań związanych uzupełniania i stan sukcesu i (2) hello zadania przekazywania wynik danych tooAzure magazynu*

Jeśli zadania zostaną dodane zadania tooa, są automatycznie w kolejce i zaplanowane do uruchomienia w węzłach obliczeń w puli hello skojarzone z zadaniem hello. Na podstawie hello ustawień przez użytkownika, partii obsługuje wszystkich zadań usługi kolejkowania, planowania, ponawianie próby i obowiązków administracyjnych innych zadań za Ciebie.

Istnieje wiele metod toomonitoring wykonywania zadania. Aplikacja DotNetTutorial stanowi prosty przykład zgłaszania tylko w przypadku ukończenia oraz stanów powodzenia lub niepowodzenia. W ramach hello `MonitorTasks` metody w jego DotNetTutorial `Program.cs`, istnieją trzy pojęcia partiami platformy .NET, które gwarantuje dyskusji. Są one wymienione poniżej w kolejności ich występowania:

1. **ODATADetailLevel**: określenie funkcji [ODATADetailLevel][net_odatadetaillevel] na liście operacji (takich jak uzyskanie listy podzadań zadania) jest niezbędne do zapewnienia wydajności aplikacji usługi Batch. Dodaj [wydajnie zapytania usługi partia zadań Azure hello](batch-efficient-list-queries.md) tooyour odczytywania listy, jeśli planujesz wykonanie dowolny rodzaj monitorowanie stanu w aplikacjach partii.
2. **TaskStateMonitor**: funkcja [TaskStateMonitor][net_taskstatemonitor] zapewnia aplikacjom usługi Batch dla platformy .NET narzędzia pomocy do monitorowania stanów podzadań. W `MonitorTasks`, *DotNetTutorial* czeka na wszystkich zadań tooreach [TaskState.Completed] [ net_taskstate] przed upływem limitu czasu. Następnie kończy zadanie hello.
3. **TerminateJobAsync**: przerywanie zadania o [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (lub hello blokuje JobOperations.TerminateJob) oznacza to zadanie jako zakończone. Jest ważne toodo tak więc jeśli rozwiązanie partii używa [JobReleaseTask][net_jobreltask]. Jest to szczególny typ podzadania, który opisano w temacie [Job preparation and completion tasks](batch-job-prep-release.md) (Przygotowanie zadania i podzadania związane z ukończeniem).

Witaj `MonitorTasks` metody z *DotNetTutorial*w `Program.cs` pojawia się poniżej:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Krok 7: pobranie danych wyjściowych podzadań
![Pobieranie danych wyjściowych zadań podrzędnych z usługi Storage][7]<br/>

Teraz, hello ukończenia zadania, dane wyjściowe zadania hello hello można pobrać z magazynu Azure. Odbywa się przy użyciu wywołania zbyt`DownloadBlobsFromContainerAsync` w *DotNetTutorial*w `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Witaj wywołanie za`DownloadBlobsFromContainerAsync` w hello *DotNetTutorial* aplikacji określa, że pliki hello powinny być pobrany tooyour `%TEMP%` folderu. Możesz wolnego toomodify to lokalizacji wyjściowej.
>
>

## <a name="step-8-delete-containers"></a>Krok 8: usuwanie kontenerów
Naliczane są opłaty za dane przechowywane w usłudze Azure Storage, dlatego jest zawsze blob tooremove dobrym rozwiązaniem, które nie są już potrzebne dla zadań wsadowych. W jego DotNetTutorial `Program.cs`, jest to zrobić za pomocą metody pomocniczej toohello trzy wywołania `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

metody Hello jedynie uzyskuje kontenera toohello odwołania, a następnie wywołuje [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Krok 9: Usuwanie hello zadania i hello puli
W ostatnim kroku hello jest monitem toodelete hello zadania i hello puli utworzone przez aplikację DotNetTutorial hello. Mimo że nie są naliczane opłaty za same zadania i podzadania, *są* naliczane opłaty za węzły obliczeniowe. W związku z tym zaleca się przydzielanie węzłów tylko zależnie do potrzeb. Usuwanie nieużywanych pul może odbywać się podczas konserwacji.

Witaj BatchClient [JobOperations] [ net_joboperations] i [PoolOperations] [ net_pooloperations] mają odpowiednie metody usunięcia, które są nazywane, jeśli Hello użytkownika stanowi potwierdzenie usunięcia:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Należy pamiętać, że opłaty są naliczane za zasoby obliczeniowe — usunięcie nieużywanych pul zminimalizuje koszty. Ponadto należy pamiętać, że usunięcie puli spowoduje usunięcie wszystkich węzłów obliczeniowych w tej puli, a wszystkie dane na powitania węzły będą nieodwracalny po usunięciu hello puli.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Uruchom hello *DotNetTutorial* próbki
Po uruchomieniu hello przykładowej aplikacji, dane wyjściowe konsoli hello będzie podobne następujące toohello. W czasie wykonywania wystąpią wstrzymany w `Awaiting task completion, timeout in 00:30:00...` podczas puli hello węzły obliczeniowe są uruchamiane. Użyj hello [portalu Azure] [ azure_portal] toomonitor puli, węzły obliczeniowe, zadań i zadań podczas i po zakończeniu wykonywania. Użyj hello [portalu Azure] [ azure_portal] lub hello [Eksploratora usługi Storage Azure] [ storage_explorers] zasobów magazynu hello tooview (kontenerów i obiektów blob) znajdujących się utworzone przez aplikację hello.

Typowy czas wykonywania jest **około 5 minut** po uruchomieniu aplikacji hello w konfiguracji domyślnej.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Następne kroki
Uznać za zmiany wolnego toomake*DotNetTutorial* i *TaskApplication* tooexperiment innej obliczania scenariuszy. Na przykład, spróbuj opóźnienie wykonywania zbyt*TaskApplication*, takich jak [Thread.Sleep][net_thread_sleep], toosimulate długotrwałych zadań i monitorować je w portalu hello. Spróbuj dodać więcej zadań lub dostosowanie hello liczba węzłów obliczeniowych. Dodaj logikę toocheck dla i Zezwalaj na użycie hello istniejących czas wykonywania toospeed puli (*wskazówka*: Zapoznaj się z `ArticleHelpers.cs` w hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] projektu w [azure partii próbek][github_samples]).

Teraz, kiedy znasz hello podstawowy przepływ pracy rozwiązania partii, jest toodig czasu w toohello dodatkowe funkcje hello usługa partia zadań.

* Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.
* Uruchomienie hello inne artykuły programowanie partii w obszarze **programowanie szczegółowe** w hello [ścieżka szkoleniowa dotycząca partii][batch_learning_path].
* Zapoznaj się z inną implementację przetwarzania obciążenia hello "pierwszych N słów" za pomocą partii w hello [TopNWords] [ github_topnwords] próbki.
* Przejrzyj hello partiami platformy .NET [informacje o wersji](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) hello najnowszych zmian w bibliotece hello.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Tworzenie kontenerów w usłudze Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Tworzenie puli usługi Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Tworzenie zadania w usłudze Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Dodaj toojob zadań"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorowanie podzadań"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Pobieranie danych wyjściowych podzadań z usługi Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Przepływ pracy w rozwiązaniu usługi Batch (pełny diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Poświadczenia usługi Batch w portalu"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Poświadczenia usługi Storage w portalu"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Przepływ pracy rozwiązania w usłudze Batch (diagram minimalny)"
