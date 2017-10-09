---
title: "przy użyciu fabryki danych i wsadowego zestawów danych na dużą skalę aaaProcess | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak potoku tooprocess dużych ilości danych w fabryce danych Azure przy użyciu możliwości przetwarzania równoległego partii zadań Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Przetwarzanie dużych ilości danych za pomocą usług Data Factory i Batch
W tym artykule opisano architekturę rozwiązania próbki, które przenosi i przetwarzania dużych zestawów danych w sposób automatycznego i zaplanowane. Umożliwia także wskazówki end-to-end tooimplement hello rozwiązania przy użyciu fabryki danych Azure i partii zadań Azure.

W tym artykule jest dłuższa niż artykułem typowe, ponieważ zawiera ona wskazówki przykładowe całego rozwiązania. W przypadku nowych tooBatch i fabryki danych, informacje na temat tych usług i jak one współdziałają ze sobą. Jeśli znasz coś o usługach hello i są projektowanie/zaprojektowanie rozwiązania, może skupić się tylko na powitania [sekcji architektura](#architecture-of-sample-solution) hello artykułu i jeśli tworzysz prototypu lub rozwiązania, można również tootry out instrukcje krok po kroku w hello [wskazówki](#implementation-of-sample-solution). Zapraszamy komentarze dotyczące tej zawartości i sposobie używania jej.

Po pierwsze Zobaczmy, jak może pomóc fabryki danych i instancji usługi przy użyciu przetwarzania dużych zestawów danych w chmurze hello.     

## <a name="why-azure-batch"></a>Dlaczego usługa partia zadań Azure?
Partia zadań Azure pozwala aplikacji na dużą skalę równoległych i wysokiej wydajności obliczeniowej (HPC) toorun wydajnie w chmurze hello. Jest usługą platformy, która planuje toorun pracy obliczeniowych w zarządzanej kolekcji maszyn wirtualnych, a można automatycznie skali obliczeniowe zasobów toomeet hello potrzeb zadań.

Za pomocą hello usługa partia zadań można definiować tooexecute zasobów obliczeniowych Azure aplikacji równolegle i na dużą skalę. Mogą być uruchamiane na żądanie lub według harmonogramu zadań, a nie ma potrzeby toomanually tworzenie, konfigurowanie i zarządzanie klastra HPC, poszczególnych maszyn wirtualnych, sieci wirtualnych lub złożonych zadań i zadań planowania infrastruktury.

Zobacz następujące artykuły, jeśli nie masz doświadczenia z partii zadań Azure jako ułatwia zrozumienie architektury hello/implementacja opisanego w tym artykule rozwiązania hello hello.   

* [Podstawowe informacje o partii zadań Azure](../batch/batch-technical-overview.md)
* [Przegląd funkcji partii](../batch/batch-api-basics.md)

(opcjonalnie) toolearn więcej informacji na temat partii zadań Azure, zobacz hello [ścieżka szkoleniowa dotycząca partii zadań Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Dlaczego fabryki danych Azure?
Fabryka danych jest usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych. Przy użyciu usługi fabryka danych hello, można utworzyć potoki zarządzanych danych, które przenoszenia danych z lokalnego i w chmurze, magazynu danych scentralizowane tooa magazynów danych (na przykład: magazyn obiektów Blob Azure), a procesu/Przekształcanie danych za pomocą usług, takich jak Azure HDInsight i Azure Uczenie maszynowe. Można również zaplanować toorun potoki danych w zaplanowanym czasie (co godzinę, codziennie, co tydzień, itp.) i monitorowanie i zarządzanie nimi na problemy tooidentify oka i podejmij akcję.

Zobacz następujące artykuły, jeśli nie masz doświadczenia z fabryką danych Azure jako ułatwia zrozumienie architektury hello/implementacja opisanego w tym artykule rozwiązania hello hello.  

* [Wprowadzenie do fabryki danych Azure](data-factory-introduction.md)
* [Tworzenie swój pierwszy potok danych](data-factory-build-your-first-pipeline.md)   

(opcjonalnie) toolearn więcej informacji na temat fabryki danych Azure, zobacz hello [ścieżka szkoleniowa dotycząca fabryki danych Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Fabryki danych i partii razem
Fabryka danych zawiera wbudowane działania, takie jak działanie kopiowania toocopy/przeniesienia danych z źródła danych magazynu magazyn danych docelowy tooa i Hive działania tooprocess danych na platformie Azure przy użyciu klastrów platformy Hadoop (HDInsight). Zobacz [działań przekształcania danych](data-factory-data-transformation-activities.md) listę obsługiwanych transformacji działania.

Również umożliwia możesz toocreate .NET działań niestandardowych danych toomove lub inny proces na własną logikę i Uruchom te działania na klaster Azure HDInsight lub w puli partii zadań Azure maszyn wirtualnych. Korzystając z partii zadań Azure, można skonfigurować skali tooauto hello puli (Dodawanie lub usuwanie maszyn wirtualnych na podstawie obciążenia hello) na podstawie formuły, musisz podać.     

## <a name="architecture-of-sample-solution"></a>Architektura przykładowe rozwiązanie
Mimo że architektura hello opisane w tym artykule jest prostym rozwiązaniem, jest odpowiednie toocomplex scenariuszy, takich jak modelowania branży usług finansowych, przetwarzania obrazów i renderowania i genomiczne analizy ryzyka.

Hello diagramie 1) jak fabryki danych organizuje przenoszenia danych i przetwarzania i 2) sposobu przetwarzania partii zadań Azure hello danych w sposób równoległy. Pobieranie i diagram hello wydruku dla ułatwienia (11 x 17 cali. lub rozmiaru A3): [aranżacji HPC i danych przy użyciu partii zadań Azure i fabryki danych](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagram przetwarzania danych na dużą skalę](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Witaj Poniższa lista zawiera podstawowe kroki hello hello procesu. rozwiązanie Hello zawiera rozwiązania end-to-end hello toobuild kodu i wyjaśnienia.

1. **Skonfiguruj partii zadań Azure z pulą węzłów obliczeniowych (VM)**. Można określić hello liczba węzłów, a rozmiar każdego węzła.
2. **Tworzy wystąpienie fabryki danych Azure** skonfigurowanego jednostek, które reprezentują magazynu obiektów blob platformy Azure, usługa obliczeniowych partii zadań Azure danych wejścia/wyjścia i przepływu pracy/potoku z działaniami, które Przenieś i przekształcania danych.
3. **Tworzenie niestandardowego działania .NET w potoku fabryki danych hello**. działanie Hello jest uruchamiany na powitania puli partii zadań Azure kodu użytkownika.
4. **Przechowywania dużych ilości danych wejściowych jako obiekty BLOB w magazynie Azure**. Danych jest podzielona na wycinków logiczne (zazwyczaj za czas).
5. **Fabryka danych kopiuje dane są przetwarzane równolegle** toohello lokalizacji dodatkowej.
6. **Fabryka danych uruchamia hello działań niestandardowych przy użyciu puli hello przydzielone przez partię**. Fabryka danych można uruchomić jednocześnie działań. Każde działanie przetwarza wycinka danych. wyniki Hello są przechowywane w magazynie Azure.
7. **Fabryka danych przenosi hello wyniki końcowe tooa trzeci lokalizacji**, w celu dystrybucji za pośrednictwem aplikacji lub dla dalszego przetwarzania przez inne narzędzia.

## <a name="implementation-of-sample-solution"></a>Implementacja przykładowe rozwiązanie
Hello przykładowe rozwiązanie jest celowo proste i tooshow należy jak toouse fabryki danych i partii razem tooprocess zestawów danych. rozwiązanie powitania po prostu zlicza hello wystąpienia terminu wyszukiwania ("Microsoft") w organizacji w szeregów czasowych plików wejściowych. Generuje on hello liczby toooutput plików.

**Czas**: Jeśli znasz podstawowe informacje o Azure, fabryki danych i partii i zostały ukończone hello wymagania wstępne wymienione poniżej, firma Microsoft oszacować to rozwiązanie ma toocomplete 1 – 2 godz.

### <a name="prerequisites"></a>Wymagania wstępne
#### <a name="azure-subscription"></a>Subskrypcja platformy Azure
Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Konto magazynu Azure
Używasz konta magazynu Azure do przechowywania danych hello w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account). Witaj przykładowe rozwiązanie korzysta z magazynu obiektów blob.

#### <a name="azure-batch-account"></a>Konto usługi partia zadań Azure
Tworzenie konta usługi partia zadań Azure za pomocą hello [portalu Azure](http://manage.windowsazure.com/). Zobacz [tworzenie i zarządzanie nimi konto partii zadań Azure](../batch/batch-account-create-portal.md). Należy zwrócić uwagę hello partii zadań Azure konta nazwy i klucza konta. Można również użyć [AzureRmBatchAccount nowy](https://msdn.microsoft.com/library/mt603749.aspx) toocreate polecenia cmdlet konto partii zadań Azure. Zobacz [wprowadzenie do poleceń cmdlet programu PowerShell usługi partia zadań Azure](../batch/batch-powershell-cmdlets-get-started.md) szczegółowe instrukcje na temat używania tego polecenia cmdlet.

Witaj przykładowe rozwiązanie używa danych tooprocess partii zadań Azure (pośrednio przez potok fabryki danych Azure) w sposób równoległy w puli węzłów obliczeniowych (zarządzanej kolekcji maszyn wirtualnych).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Azure puli partii maszyn wirtualnych (VM)
Utwórz **puli partii zadań Azure** z co najmniej 2 węzły obliczeniowe.

1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **Przeglądaj** w hello menu po lewej stronie i kliknij przycisk **konta usługi partia zadań**.
2. Wybierz użytkownika hello tooopen konto partii zadań Azure **konta usługi partia zadań** bloku.
3. Kliknij przycisk **pule** kafelka.
4. W hello **pule** bloku, kliknij przycisk Dodaj na powitania narzędzi tooadd puli.
   1. Wpisz identyfikator puli hello (**identyfikator puli**). Uwaga hello **identyfikator puli hello**; potrzebne podczas tworzenia hello rozwiązania fabryki danych.
   2. Określ **systemu Windows Server 2012 R2** hello ustawienia rodziny systemów operacyjnych.
   3. Wybierz **warstwę cenową węzła**.
   4. Wprowadź **2** jako wartość hello **docelowego w wersji dedykowanej** ustawienie.
   5. Wprowadź **2** jako wartość hello **maksymalna liczba zadań na węzeł** ustawienie.
   6. Kliknij przycisk **OK** toocreate hello puli.

#### <a name="azure-storage-explorer"></a>Eksplorator usługi Azure Storage
[Azure magazynu Explorer 6 (Narzędzia)](https://azurestorageexplorer.codeplex.com/) lub [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (z oprogramowania ClumsyLeaf). Zapoznanie się i zmieniając hello danych w projektach usługi Azure Storage, w tym dzienniki hello aplikacji hostowanych w chmurze za pomocą tych narzędzi.

1. Utworzyć kontener o nazwie **mojkontener** prywatny dostęp (Brak dostępu anonimowego)
2. Jeśli używasz **CloudXplorer**, tworzyć foldery i podfoldery z hello następujące struktury:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`i `outputfolder` są folderów najwyższego poziomu w `mycontainer`. Witaj `inputfolder` ma podfoldery z sygnaturami daty i godziny (RRRR-MM-DD-HH).

   Jeśli używasz **Eksploratora usługi Storage Azure**, w następnym kroku hello potrzebne pliki tooupload o nazwach: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` i tak dalej. Ten krok automatycznie tworzy foldery hello.
3. Utwórz plik tekstowy **plik.txt** na komputerze z zawartością, która ma hello — słowo kluczowe **Microsoft**. Na przykład: "test niestandardowe aktywności testów Microsoft działania niestandardowego Microsoft".
4. Przekaż toohello pliku hello następujące foldery wejściowego w magazynie obiektów blob platformy Azure.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Jeśli używasz **Eksploratora usługi Storage Azure**, Przekaż plik hello **plik.txt** za**mojkontener**. Kliknij przycisk **kopiowania** na powitania narzędzi toocreate kopię hello obiektów blob. W hello **kopiowania obiektu Blob** okno dialogowe, zmień hello **Nazwa docelowego obiektu blob** zbyt`inputfolder/2015-11-16-00/file.txt`. Powtórz ten krok toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` i tak dalej. Ta akcja powoduje automatyczne utworzenie hello folderów.
5. Tworzenie kontenera o nazwie: `customactivitycontainer`. Możesz przekazać hello działania niestandardowego zip pliku toothis kontenera.

#### <a name="visual-studio"></a>Visual Studio
Zainstaluj program Microsoft Visual Studio 2012 lub nowszym toocreate hello niestandardowych partii działania toobe używane w hello rozwiązania fabryki danych.

### <a name="high-level-steps-toocreate-hello-solution"></a>Ogólne kroki toocreate hello rozwiązania
1. Utwórz niestandardowe działanie, które zawiera hello logikę przetwarzania danych.
2. Tworzenie fabryki danych Azure, która używa niestandardowego działania hello:

### <a name="create-hello-custom-activity"></a>Tworzenie niestandardowego działania hello
Hello działania niestandardowego fabryki danych jest Puls hello tego rozwiązania próbki. Witaj przykładowe rozwiązanie używa niestandardowego działania hello toorun partii zadań Azure. Zobacz [skorzystać z działań niestandardowych w potoku fabryki danych Azure](data-factory-use-custom-activities.md) hello podstawowe informacje toodevelop niestandardowych działań i używania ich w fabryce danych Azure potoków.

toocreate działania niestandardowego .NET używanego w potoku fabryki danych Azure, należy toocreate **Biblioteka klas programu .NET** projektu z klasy, która implementuje który **IDotNetActivity** interfejsu. Ten interfejs jest tylko jedna metoda: **Execute**. Oto hello podpis metody hello:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

Metoda Hello ma kilka kluczowych składników należy toounderstand.

* Metoda Hello przyjmuje cztery parametry:

  1. **linkedServices**. Wyliczalny lista połączonych usług połączonych źródeł danych wejścia/wyjścia (na przykład: magazyn obiektów Blob Azure) toohello fabryki danych. W tym przykładzie istnieje tylko jeden połączonej usługi typu usługi Azure Storage używane dla danych wejściowych i wyjściowych.
  2. **zestawy danych**. Jest to lista wyliczalny zestawów danych. Można użyć tego parametru tooget hello lokalizacji i schematów wynika z zestawów danych wejściowych i wyjściowych.
  3. **działanie**. Tego parametru reprezentuje hello bieżącego obliczeniowe — w takim przypadku usługa partia zadań Azure.
  4. **Rejestrator**. Umożliwia rejestratora Hello komentarze debugowania tej powierzchni jako hello, poszukaj w dzienniku "Użytkownika" hello potoku.
* Witaj, metoda zwraca słownik, który może być działań niestandardowych toochain używane razem w przyszłości hello. Ta funkcja nie jest jeszcze zaimplementowana, więc Zwróć pusty słownik z metody hello.

#### <a name="procedure-create-hello-custom-activity"></a>Procedura: Tworzenie niestandardowego działania hello
1. Utwórz projekt Biblioteka klas programu .NET w programie Visual Studio.

   1. Uruchom **programu Visual Studio 2012**/**2013/2015**.
   2. Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.
   3. Rozwiń węzeł **szablony**i wybierz **Visual C\#**. W tym przewodniku, należy użyć serwera C\#, ale można użyć dowolnego .NET języka toodevelop hello działania niestandardowego.
   4. Wybierz **biblioteki klas** z hello listy typów projektu na powitania prawo.
   5. Wprowadź **MyDotNetActivity** dla hello **nazwa**.
   6. Wybierz **C:\\ADF** dla hello **lokalizacji**. Utwórz hello folder **ADF** Jeśli nie istnieje.
   7. Kliknij przycisk **OK** toocreate hello projektu.
2. Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.
3. W hello **Konsola Menedżera pakietów**, wykonaj następujące polecenie tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Importuj hello **usługi Azure Storage** pakietu NuGet w projekcie toohello. Ten pakiet jest potrzebna, ponieważ używasz hello interfejsu API z magazynu obiektów Blob w tym przykładzie.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Dodaj następujące hello **przy użyciu** plik źródłowy toohello dyrektywy w projekcie hello.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Zmień nazwę hello hello **przestrzeni nazw** za**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Zmień nazwę hello klasy hello zbyt**MyDotNetActivity** i pochodną hello **IDotNetActivity** interfejsu, jak pokazano poniżej.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Witaj wdrożenie (Dodaj) **Execute** metody hello **IDotNetActivity** interfejsu toohello **MyDotNetActivity** hello klasy i skopiuj następujące metody toohello kodu przykładowej. Zobacz hello [wykonywanie metody](#execute-method) sekcji wyjaśnienie logiki hello używane w ramach tej metody.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. Dodaj następujące klasy toohello metody pomocnika hello. Te metody są wywoływane przez hello **Execute** metody. Przede wszystkim hello **Calculate** metody izoluje hello kodu, który iteruje po każdy obiekt blob.

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    Witaj **GetFolderPath** metoda zwraca folder toohello ścieżki hello hello tooand tego hello zestawu danych punktów **GetFileName** metoda zwraca nazwę hello hello obiekt blob/pliku, który hello wskazuje zestawu danych.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Witaj **Calculate** metody oblicza hello liczbę wystąpień — słowo kluczowe **Microsoft** w hello plików wejściowych (obiekty BLOB w folderze hello). Witaj terminu wyszukiwania ("Microsoft") jest ustalony w kodzie hello.

1. Skompiluj projekt hello. Kliknij przycisk **kompilacji** hello menu i kliknij przycisk **Kompiluj rozwiązanie**.
2. Uruchom **Eksploratora Windows**i przejdź zbyt**bin\\debugowania** lub **bin\\wersji** folder, w zależności od typu hello kompilacji.
3. Utwórz plik zip **MyDotNetActivity.zip** zawierający wszystkie hello pliki binarne w hello  **\\bin\\debugowania** folderu. Możesz tooinclude hello MyDotNetActivity. **pdb** pliku, tak aby uzyskać dodatkowe szczegóły, takie jak numer wiersza w kodzie źródłowym hello, który spowodował problem hello, gdy wystąpi błąd.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Przekaż **MyDotNetActivity.zip** jako kontener obiektów blob toohello obiektu blob: `customactivitycontainer` w hello Azure magazynu obiektów blob tego hello **StorageLinkedService** połączonej usługi w hello  **ADFTutorialDataFactory** używa. Tworzenie kontenera obiektów blob hello `customactivitycontainer` Jeśli jeszcze nie istnieje.

#### <a name="execute-method"></a>Execute — Metoda
Ta sekcja zawiera bardziej szczegółowe informacje i notatki dotyczące kodu hello w hello metody Execute.

1. elementy członkowskie Hello iteracji w kolekcji wejściowych hello znajdują się w hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) przestrzeni nazw. Iteracji w kolekcji obiektów blob hello wymaga użycia hello **BlobContinuationToken** klasy. W zasadzie, należy użyć-pętli z tokenem hello jako mechanizm hello wyjścia hello pętli while. Aby uzyskać więcej informacji, zobacz [jak toouse magazynu obiektów Blob z .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Podstawowe pętli jest następujący:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Zapoznaj się dokumentacją hello hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) metody, aby uzyskać szczegółowe informacje.
2. Hello kodu pracuje nad hello zestawu obiektów blob logicznie znajdzie się w obrębie hello czy-pętli while. W hello **Execute** metoda, czy hello — gdy pętli przekazuje hello listę obiektów blob tooa metodę o nazwie **Calculate**. Witaj, metoda zwraca ciąg zmiennej o nazwie **dane wyjściowe** czyli hello wyniku o iterowane za pośrednictwem wszystkich hello obiektów blob w segmencie hello.

   Zwraca hello liczbę wystąpień hello wyszukiwany termin (**Microsoft**) w obiekcie blob hello przekazany toohello **Calculate** metody.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Raz hello **Calculate** metody przeprowadził hello pracy, jego musi być napisana tooa nowego obiektu blob. Aby dla każdego zestawu obiektów blob przetwarzane z wynikami hello można pisać nowego obiektu blob. Nowy obiekt blob toowrite tooa, pierwsze Znajdź hello wyjściowego zestawu danych.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. Kod Hello również wywołuje metodę pomocnika: **GetFolderPath** ścieżka folderu hello tooretrieve (nazwa kontenera magazynu hello).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Witaj **GetFolderPath** tooan obiektu DataSet AzureBlobDataSet, który ma właściwość o nazwie FolderPath hello rzutowania.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. Witaj Witaj wywołań kodu **GetFileName** metody tooretrieve hello nazwę pliku (obiektów blob). Kod Hello jest podobne toohello powyżej ścieżka folderu hello tooget kodu.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. Witaj nazwę pliku hello są zapisywane przez utworzenie obiekt URI. Konstruktor URI Hello używa hello **BlobEndpoint** nazwa kontenera hello tooreturn właściwości. Witaj folderu ścieżka i nazwa pliku są dodawane tooconstruct hello dane wyjściowe identyfikator URI obiektu blob.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. Hello nazwę pliku hello został zapisany i teraz można zapisać ciągu wyjściowego hello ze hello **Calculate** nowego obiektu blob tooa metody:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Tworzenie fabryki danych hello
W hello [tworzenia działań niestandardowych hello](#create-the-custom-activity) sekcji utworzone niestandardowe działania i hello przekazanego pliku zip z plików binarnych i hello PDB plików tooan kontenera obiektów blob platformy Azure. W tej sekcji utworzysz Azure **fabryki danych** z **potoku** używającą hello **działania niestandardowego**.

Witaj zestawu danych wejściowych dla działań niestandardowych hello reprezentuje hello obiektów blob (pliki) w folderze wejściowych hello (`mycontainer\\inputfolder`) w magazynie obiektów blob. Witaj wyjściowy zestaw danych dla działania hello reprezentuje obiekty BLOB danych wyjściowych hello w folderze wyjściowym hello (`mycontainer\\outputfolder`) w magazynie obiektów blob.

Upuść jeden lub więcej plików w folderach wejściowych hello:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Na przykład usunąć jeden plik (plik.txt) z powitania po zawartości do poszczególnych folderów hello.

```
test custom activity Microsoft test custom activity Microsoft
```

Każdego folderu wejściowych odpowiada wycinek tooa w fabryce danych Azure, nawet wtedy, gdy hello znajduje się w nim pliki 2 lub większą. Każdy wycinek jest przetwarzany przez potok hello, działania niestandardowego hello iterację wszystkich hello obiektów blob w folderze wejściowych powitania dla tego wycinka.

Widać pięć pliki wyjściowe z hello sam zawartości. Na przykład plik wyjściowy hello przetwarzanie hello plik w folderze hello 2015-11-16-00 ma hello następującej zawartości:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Jeśli musisz porzucić wiele plików (plik.txt, Plik2.txt file3.txt) z hello folder wejściowy toohello tej samej zawartości, zobacz powitania po zawartości w pliku wyjściowym hello. Każdego folderu (2015-11-16-00 itp.) odpowiada wycinek tooa w tym przykładzie, mimo że hello znajduje się w nim wiele plików wejściowych.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

Plik wyjściowy Hello ma trzy wiersze teraz, po jednej dla każdego pliku wejściowego (blob) w folderze hello skojarzone z hello slice (2015-11-16-00).

Zadanie jest tworzone dla każdej uruchamiania działania. W tym przykładzie istnieje tylko jedno działanie w potoku hello. Gdy wycinek jest przetwarzany przez potok hello, hello działania niestandardowego działa w partii zadań Azure tooprocess hello wycinka. Ponieważ pięć wycinków (każdy wycinek może mieć wielu obiektów blob lub pliku), jest pięć zadań utworzona w partii zadań Azure. Po uruchomieniu zadania w partii, jest rzeczywiście hello działań niestandardowych z systemem.

Witaj następujące wskazówki zawiera dodatkowe szczegóły.

#### <a name="step-1-create-hello-data-factory"></a>Krok 1: Tworzenie fabryki danych hello
1. Po zalogowaniu toohello [portalu Azure](https://portal.azure.com/), hello następujące kroki:

   1. Kliknij przycisk **nowy** w menu po lewej stronie powitania.
   2. Kliknij przycisk **dane i analiza** w hello **nowy** bloku.
   3. Kliknij przycisk **fabryki danych** na powitania **analizy danych** bloku.
2. W hello **nowa fabryka danych** bloku, wprowadź **CustomActivityFactory** dla hello nazwy. Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: **nazwa fabryki danych "CustomActivityFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład **yournameCustomActivityFactory**) i spróbuj utworzyć ponownie.
3. Kliknij przycisk **Nazwa grupy zasobów**i wybierz istniejącą grupę zasobów lub Utwórz grupę zasobów.
4. Sprawdź, czy używasz hello poprawne subskrypcji i regionu, w którym ma toobe fabryki danych hello utworzone.
5. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.
6. Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure.
7. Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Krok 2: Tworzenie usługi połączonej
Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług. W tym kroku zostanie połączony z **usługi Azure Storage** konta i **partii zadań Azure** tooyour konta usługi fabryka danych.

#### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
1. Kliknij hello **tworzenie i wdrażanie** Kafelek na powitania **FABRYKI danych** bloku **CustomActivityFactory**. Zostanie wyświetlony hello Edytor fabryki danych.
2. Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **magazynu Azure.** Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure. toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Tworzenie usługi partia zadań Azure połączone
W tym kroku możesz utworzyć połączonej usługi dla Twojego **partii zadań Azure** konta, które jest używane toorun hello fabryki danych niestandardowego działania.

1. Kliknij przycisk **nowych obliczeń** hello pasek poleceń i wybierz **partii zadań Azure.** Powinny pojawić się hello skryptu JSON do tworzenia partii zadań Azure połączonej usługi w edytorze hello.
2. W hello skryptu JSON:

   1. Zastąp **nazwa konta** o nazwie hello konta partii zadań Azure.
   2. Zastąp **klucz dostępu** z klucz dostępu hello hello konto partii zadań Azure.
   3. Wprowadź identyfikator hello puli hello hello **poolName** właściwości**.** Dla tej właściwości można określić albo nazwę puli lub puli identyfikatora.
   4. Wprowadź hello partii identyfikatora URI dla hello **batchUri** właściwości JSON.

      > [!IMPORTANT]
      > Witaj **adres URL** z hello **bloku konta usługi partia zadań Azure** jest zgodny z formatem hello: \<accountname\>.\< region\>. batch.azure.com. Dla hello **batchUri** właściwości w hello JSON, należy za**Usuń "accountname."** z hello adresu URL. Przykład: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Dla hello **poolName** właściwości, można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.

      > [!NOTE]
      > Hello usługi fabryka danych nie obsługuje opcji na żądanie dla partii zadań Azure, w przeciwieństwie do usługi HDInsight. Pulę partii zadań Azure można używać tylko w fabryce danych Azure.
      >
      >
   5. Określ **StorageLinkedService** dla hello **linkedServiceName** właściwości. Tej połączonej usługi utworzony w poprzednim kroku hello. Ten magazyn jest używany jako obszaru przemieszczania dla plików i dzienników.
3. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

#### <a name="step-3-create-datasets"></a>Krok 3: Tworzenie zestawów danych
W tym kroku możesz utworzyć zestawy danych toorepresent w danych wejściowych i dane wyjściowe.

#### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **nowy zestaw danych** przycisk na powitania narzędzi i kliknij przycisk **magazynu obiektów Blob Azure** z menu rozwijanego hello.
2. Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    Utworzyć potok w dalszej części tego przewodnika, czas rozpoczęcia: 2015-11-16T00:00:00Z i na końcu czasu: 2015-11-16T05:00:00Z. Są to dane zaplanowane tooproduce **co godzinę**, więc istnieje 5 wycinków wejścia/wyjścia (między **00**: 00:00 -\> **05**: 00:00).

    Witaj **częstotliwość** i **interwał** dla zestawu danych wejściowych hello jest ustawiony za**godzina** i **1**, co oznacza, że hello danych wejściowych jest dostępny co godzinę.

    Poniżej przedstawiono hello godzin rozpoczęcia każdy wycinek, które jest reprezentowana przez **SliceStart** zmiennej systemowej w hello powyżej fragment kodu JSON.

    | **Wycinek** | **Godzina rozpoczęcia**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**: 00:00 |
    | 2         | 2015-11-16T**01**: 00:00 |
    | 3         | 2015-11-16T**02**: 00:00 |
    | 4         | 2015-11-16T**03**: 00:00 |
    | 5         | 2015-11-16T**04**: 00:00 |

    Witaj **folderPath** jest obliczana przy użyciu hello rok, miesiąc, dzień i godzinę część czas rozpoczęcia wycinek hello (**SliceStart**). W związku z tym Oto jak folder wejściowy jest mapowane tooa wycinka.

    | **Wycinek** | **Godzina rozpoczęcia**          | **Folder wejściowy**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16-**04** |

1. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **InputDataset** tabeli.

#### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
W tym kroku utworzysz innego elementu dataset typu AzureBlob toorepresent hello wyjście danych.

1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **nowy zestaw danych** przycisk na powitania narzędzi i kliknij przycisk **magazynu obiektów Blob Azure** z menu rozwijanego hello.
2. Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    Obiekt blob/plik wyjściowy jest generowany dla każdego wejściowego wycinka. Oto, jak dla każdego wycinka nosi nazwę pliku wyjściowego. Wszystkie pliki wyjściowe hello są generowane w jednym folderze wyjściowym: `mycontainer\\outputfolder`.

    | **Wycinek** | **Godzina rozpoczęcia**          | **Plik wyjściowy**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16 -**00. txt** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16 -**01. txt** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16 -**02. txt** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16 -**03. txt** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16 -**04. txt** |

    Należy pamiętać, że hello wszystkie pliki w folderze wejściowych (na przykład: 2015-11-16-00) są częścią wycinek hello czas rozpoczęcia: 2015-11-16-00. Podczas przetwarzania tego wycinka działania niestandardowego hello skanowania za pomocą każdego pliku i tworzy wiersz w pliku wyjściowym hello hello liczby wystąpień terminu wyszukiwania ("Microsoft"). Jeśli istnieją trzy pliki w folderze hello 2015-11-16-00, istnieją trzy wiersze w pliku wyjściowym hello: 2015-11-16-00.txt.

1. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Krok 4: Tworzenie i uruchamianie potoku hello z działań niestandardowych
W tym kroku możesz utworzyć potok z jednego działania, hello działania niestandardowego utworzonego wcześniej.

> [!IMPORTANT]
> Jeśli nie zostały jeszcze przekazane hello **plik.txt** tooinput folderów w kontenerze obiektów blob hello zrobić przed utworzeniem hello potoku. Witaj **isPaused** właściwość jest ustawiona toofalse w potoku hello JSON, więc potoku hello uruchamia natychmiast jako hello **start** przypada w przeszłości hello.
>
>

1. W hello Edytor fabryki danych, kliknij przycisk **nowy potok** na powitania paska poleceń. Jeśli polecenie hello nie jest widoczne, kliknij **... (Wielokropek)**  toosee go.
2. Zastąp hello JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Należy zwrócić uwagę hello następujące punkty:

   * Istnieje tylko jedno działanie w potoku hello i jest typu: **DotNetActivity**.
   * **AssemblyName** jest ustawiona na nazwę toohello hello biblioteki DLL: **MyDotNetActivity.dll**.
   * **Punkt wejścia** ustawiono zbyt**MyDotNetActivityNS.MyDotNetActivity**. Zasadniczo jest \<przestrzeni nazw\>.\< ClassName\> w kodzie.
   * **PackageLinkedService** ustawiono zbyt**StorageLinkedService** wskazującego toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego. Jeśli używasz różnych kont usługi Azure Storage dla wejścia/wyjścia plików i plik zip hello działań niestandardowych, masz toocreate innej usługi Azure Storage połączonej usługi. W tym artykule przyjęto założenie, że używasz hello tego samego konta magazynu Azure.
   * **PackageFile** ustawiono zbyt**customactivitycontainer/MyDotNetActivity.zip**. Jest w formacie hello: \<containerforthezip\>/\<nameofthezip.zip\>.
   * przyjmuje działania niestandardowego Hello **InputDataset** jako dane wejściowe i **OutputDataset** jako dane wyjściowe.
   * Witaj **linkedServiceName** właściwości niestandardowe działania hello punktów toohello **AzureBatchLinkedService**, który informuje usługi fabryka danych Azure tego działania niestandardowego hello musi toorun w partii zadań Azure.
   * Witaj **współbieżności** ustawienie jest ważne. Jeśli używasz hello domyślną wartość, która ma wartość 1, nawet jeśli masz 2 lub obliczeniowe więcej węzłów w puli partii zadań Azure hello, wycinków hello są przetwarzane po kolei. W związku z tym nie korzystasz z możliwości przetwarzania równoległego hello partii zadań Azure. Jeśli ustawisz **współbieżności** tooa wyższa wartość, powiedz 2, oznacza to dwa wycinków (odpowiada tootwo zadań w partii zadań Azure) mogą być przetwarzane w hello sam czas, w którym to przypadku obie maszyny wirtualne hello w hello są używane w puli partii zadań Azure. W związku z tym odpowiednio ustawione hello właściwości współbieżności.
   * Tylko jedno zadanie (wycinek) jest wykonywana na maszynie Wirtualnej w dowolnym momencie domyślnie. Witaj przyczyna jest fakt, że domyślnie hello **maksymalna zadania dla maszyny Wirtualnej** ustawiono too1 puli partii zadań Azure. W ramach wymagań wstępnych, pula jest utworzona z tym too2 zestaw właściwości, więc dwa wycinków fabryki danych może być uruchomiony na maszynie Wirtualnej na powitania tym samym czasie.

    -   **isPaused** właściwość jest ustawieniem domyślnym toofalse. potok Hello uruchamia natychmiast w tym przykładzie, ponieważ wycinków hello uruchomić w przeszłości hello. Można ustawić tej właściwości tootrue toopause hello potoku i ustaw ją toorestart toofalse Wstecz.

    -   Witaj **start** czasu i **zakończenia** czasy są od siebie pięć godzin i wycinki są tworzone co godzinę, więc pięć wycinków są produkowane przez potok hello.

1. Kliknij przycisk **Wdróż** na pasku toodeploy hello potoku poleceń hello.

#### <a name="step-5-test-hello-pipeline"></a>Krok 5: Testowanie hello potoku
W tym kroku należy przetestować potoku hello upuszczanie plików w folderach wejściowych hello. Zacznijmy testowania potoku hello z jednego pliku na jeden folder wejściowy.

1. W bloku fabryki danych hello w hello portalu Azure, kliknij przycisk **Diagram**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. W widoku diagramu hello, kliknij dwukrotnie plik wejściowy zestaw danych: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Powinny pojawić się hello **InputDataset** blok z wszystkich pięciu wycinków gotowe. Powiadomienie hello **czas rozpoczęcia WYCINEK** i **czas zakończenia WYCINEK** dla każdego wycinka.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. W hello **widoku diagramu**, kliknij przycisk **OutputDataset**.
5. Powinny być widoczne czy hello pięć wycinki danych wyjściowych znajdują się w stanie gotowe hello już został utworzony.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Użyj tooview portalu Azure hello **zadania** skojarzone z hello **wycinków** i sprawdzić, jakie maszyny Wirtualnej, każdy wycinek uruchomionego na. Zobacz [integracji fabryki danych i partii](#data-factory-and-batch-integration) sekcji, aby uzyskać szczegółowe informacje.
7. Powinny pojawić się pliki wyjściowe hello w hello `outputfolder` z `mycontainer` w Azure magazynu obiektów blob.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Powinny pojawić się pięć plików wyjściowych, po jednej dla każdego wejściowego wycinka. Każdy z hello output się, że plik powinien mieć zawartości toohello podobne następujące dane wyjściowe:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Witaj poniższym diagramie przedstawiono sposób wycinków fabryki danych hello mapowania tootasks w partii zadań Azure. W tym przykładzie wycinek ma tylko jeden przebieg.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Teraz spróbujmy z wieloma plikami w folderze. Tworzenie plików: **Plik2.txt**, **file3.txt**, **file4.txt**, i **file5.txt** z hello tej samej zawartości, tak jak plik.txt w folderze hello: **2015-11-06-01**.
9. W folderze wyjściowym hello **usunąć** hello pliku wyjściowego: **2015-11-16-01.txt**.
10. Teraz, w hello **OutputDataset** bloku, kliknij prawym przyciskiem myszy hello wycinek z **czas rozpoczęcia WYCINEK** ustawić także**2015-11-16 01:00:00 AM**i kliknij przycisk **Uruchom**toorerun/ponownie-process hello wycinka. Teraz wycinek hello ma pięć plików zamiast jeden plik.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Po uruchomieniu hello wycinka i jego stan jest **gotowe**, sprawdź zawartość hello w pliku wyjściowym powitania dla tego wycinka (**2015-11-16-01.txt**) w hello `outputfolder` z `mycontainer` w magazynie obiektów blob. Należy wiersz dla każdego pliku hello wycinka.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Jeśli nie została usunięta 2015 pliku wyjściowego hello-11-16-01.txt przed podjęciem próby z pięć plików wejściowych, zobacz jeden wiersz z hello wycinek poprzedniego uruchomienia i pięciu wierszach z hello wycinek bieżącego uruchomienia. Domyślnie zawartość hello jest plik dołączany toooutput, jeśli już istnieje.
>
>

#### <a name="data-factory-and-batch-integration"></a>Integracja z fabryki danych i usługi partia zadań
Witaj usługi fabryka danych tworzy zadanie w partii zadań Azure o nazwie hello: `adf-poolname:job-xxx`.

![Fabryka danych Azure - zadań wsadowych](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Zadania w zadaniu hello jest tworzony przy każdym uruchomieniu działania wycinek. W przypadku 10 toobe gotowy wycinków przetwarzane 10 zadań są tworzone w hello zadania. Może mieć więcej niż jeden wycinek typu uruchamiania równolegle, jeśli masz wiele węzłów obliczeniowych w puli hello. Jeśli maksymalna zadań hello na obliczeniowe zbyt zestawu węzłów > 1, może istnieć więcej niż jedną slice uruchomionych na powitania obliczeniowych tej samej.

W tym przykładzie istnieje pięć wycinków, więc pięć zadań w partii zadań Azure. Z hello **współbieżności** ustawić także**5** hello w potoku JSON w fabryce danych Azure i **maksymalna zadania dla maszyny Wirtualnej** ustawić także**2** w partii zadań Azure Pula z **2** maszyn wirtualnych, hello zadań uruchamia szybkie (Sprawdź godziny rozpoczęcia i zakończenia zadania).

Użyj zadania wsadowego hello portalu tooview hello i jego zadań, które są skojarzone z hello **wycinków** i sprawdzić, jakie maszyny Wirtualnej, każdy wycinek uruchomionego na.

![Fabryka danych Azure - zadań zadania wsadowego](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Debugowanie hello potoku
Debugowanie obejmuje kilka podstawowych technik:

1. Jeśli hello wycinek wejściowy nie jest ustawiona zbyt**gotowe**, potwierdź, że struktura folderów wejściowych hello jest poprawna i plik.txt istnieje w folderach wejściowych hello.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. W hello **Execute** metody działania niestandardowego, użyj hello **IActivityLogger** toolog informacji o obiekcie, ułatwiające rozwiązywanie problemów. wiadomości powitania rejestrowane widoczne w użytkownika hello\_plików dziennika 0.

   W hello **OutputDataset** bloku, kliknij przycisk hello wycinek toosee hello **WYCINKA danych** bloku dla tego wycinka. Zostanie wyświetlony **uruchomień działania** dla tego wycinka. Powinny pojawić się jeden uruchamiania dla wycinka hello działania. Jeśli klikniesz przycisk **Uruchom** na pasku poleceń hello, można uruchomić inne działanie Uruchom hello tego samego wycinka.

   Po kliknięciu przycisku uruchamiania działania hello Zobacz hello **szczegóły uruchomienia działania** bloku zawierającego listę plików dziennika. Zobacz zarejestrowane komunikaty w hello **użytkownika\_dziennika 0** pliku. Po wystąpieniu błędu, zobacz trzech uruchomień działania ponieważ liczby ponownych prób hello ustawiono too3 w potoku hello/aktywność JSON. Po kliknięciu przycisku uruchamiania działania hello możesz Zobacz pliki dziennika hello możesz przejrzeć tootroubleshoot hello błędu.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   W hello listę plików dziennika, kliknij przycisk hello **0.log użytkownika**. W prawym panelu hello są wyniki hello przy użyciu hello **IActivityLogger.Write** metody.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Sprawdź system-0.log za wszelkie komunikaty o błędach systemu i wyjątki.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Zawierają hello **PDB** plików w pliku zip hello w celu hello szczegóły błędu mają informacje takie jak **stosu wywołań** po wystąpieniu błędu.
4. Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z bez podfolderów.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Upewnij się, że hello **assemblyName** (MyDotNetActivity.dll), **punktu wejścia** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) i **packageLinkedService** (powinien Azure toohello punktu magazynu obiektów blob zawierający plik zip hello) są ustawione wartości toocorrect.
6. Stałe błędu i chcesz wycinek hello tooreprocess, kliknij prawym przyciskiem myszy hello wycinek hello **OutputDataset** bloku i kliknij przycisk **Uruchom**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Zostanie wyświetlony **kontenera** w magazynie obiektów Blob Azure o nazwie: `adfjobs`. Ten kontener nie jest automatycznie usuwana, ale można je bezpiecznie usunąć po zakończeniu testowania hello rozwiązania. Podobnie, hello rozwiązania fabryki danych tworzy partii zadań Azure **zadania** o nazwie: `adf-\<pool ID/name\>:job-0000000001`. Po Jeśli chcesz przetestować hello rozwiązania, można usunąć tego zadania.
   >
   >
7. działania niestandardowego Hello nie używa hello **app.config** plików z pakietu. W związku z tym jeśli kod odczytuje wszelkie parametry połączenia z pliku konfiguracji hello, działa w czasie wykonywania. Witaj najlepsze rozwiązanie przy użyciu partii zadań Azure jest toohold żadnych kluczy tajnych w **Azure KeyVault**, keyvault hello tooprotect główną usługi na podstawie certyfikatu, a dystrybucję hello certyfikatu tooAzure partii puli. Witaj działania niestandardowego .NET, a następnie mogą uzyskiwać dostęp do kluczy tajnych z hello KeyVault w czasie wykonywania. To rozwiązanie jest rodzajowy i mogą być skalowane tooany typu klucza tajnego, nie tylko w parametrach połączenia.

    Istnieje obejście łatwiejsze (ale nie najlepiej): można utworzyć **Azure SQL połączona usługa** ustawień parametrów połączenia, tworzenie połączonej usługi i dataset hello łańcucha jako fikcyjny wejściowy zestaw danych tekst hello używa zestawu danych toohello niestandardowego działania .NET. Mogą być następnie hello dostępu połączone usługi parametry połączenia w kodzie działania niestandardowego hello, powinny działać prawidłowo w czasie wykonywania.  

#### <a name="extend-hello-sample"></a>Rozszerzanie hello próbki
Można rozszerzyć toolearn tej próbki więcej informacji na temat funkcji usługi fabryka danych Azure i partii zadań Azure. Na przykład tooprocess wycinki inny zakres czasu, hello następujące kroki:

1. Dodaj następujące podfoldery hello hello `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 i miejscu plików wejściowych zawierających w tych folderach. Zmień hello godziny zakończenia dla potoku hello z `2015-11-16T05:00:00Z` zbyt`2015-11-16T10:00:00Z`. W hello **widoku diagramu**, kliknij dwukrotnie hello **InputDataset**i Potwierdź, że wejściowy wycinków hello są gotowe. Kliknij dwukrotnie **OuptutDataset** toosee hello stanu wycinków danych wyjściowych. Jeśli są w stanie gotowe, sprawdź folder wyjściowy hello hello plików wyjściowych.
2. Zwiększanie lub zmniejszanie hello **współbieżności** toounderstand ustawienie jak ma to wpływ na wydajność hello rozwiązania, szczególnie hello przetwarzania zachodzących w partii zadań Azure. (Zobacz krok 4: tworzenie i uruchamianie potoku hello, aby uzyskać więcej informacji na temat hello **współbieżności** ustawienie.)
3. Tworzenie puli za pomocą/małe **maksymalna zadania dla maszyny Wirtualnej**. toouse hello nowej puli, utworzoną przez siebie w hello aktualizacji usługi partia zadań Azure, połączone w rozwiązaniu do hello fabryki danych. (Zobacz krok 4: tworzenie i uruchamianie potoku hello, aby uzyskać więcej informacji na temat hello **maksymalna zadania dla maszyny Wirtualnej** ustawienie.)
4. Tworzenie puli partii zadań Azure z **skalowania automatycznego** funkcji. Automatyczne skalowanie węzłów obliczeniowych w puli partii zadań Azure to dynamiczne Dostosowywanie hello przetwarzania zasilania używanych przez aplikację. 

    tutaj Hello przykładowa formuła osiąga hello następujące zachowanie: podczas tworzenia puli hello, rozpoczyna się od 1 maszyny Wirtualnej. Metryka $PendingTasks definiuje hello liczbę zadań uruchomiona + aktywny (w kolejce) stanu.  Formuła Hello znajduje hello średnią liczbę zadań oczekujących w hello ostatnich 180 sekund i odpowiednio ustawia TargetDedicated. Gwarantuje, że TargetDedicated nigdy nie wykracza poza 25 maszyn wirtualnych. Tak, jak nowe zadania są przesyłane, automatycznie zwiększa rozmiar puli i jako zakończenie zadania, maszyn wirtualnych stają się wolnego jeden po drugim i skalowanie automatyczne hello zmniejsza tych maszyn wirtualnych. startingNumberOfVMs i maxNumberofVMs mogą być dostosowane tooyour potrzeb.
 
    Formuła skalowania automatycznego:

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](../batch/batch-automatic-scaling.md) szczegółowe informacje.

   Jeśli puli hello używa domyślnej hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello usługa partia zadań może zająć 15 do 30 minut tooprepare hello maszyny Wirtualnej przed uruchomieniem hello działania niestandardowego.  Jeśli pula hello jest przy użyciu różnych autoScaleEvaluationInterval, hello usługa partia zadań może zająć autoScaleEvaluationInterval + 10 minut.
5. W rozwiązaniu próbki hello hello **Execute** metoda wywołuje hello **Calculate** metody, która przetwarza dane wejściowe wycinek tooproduce wycinka danych wyjściowych. Można napisać własny tooprocess — metoda dane wejściowe i Zastąp wywołanie metody Calculate hello w metody Execute hello metody tooyour połączeń.

### <a name="next-steps-consume-hello-data"></a>Następne kroki: wykorzystują dane hello
Po przetwarzania danych, można pobrać go online narzędzia, takie jak **Microsoft Power BI**. Oto łącza toohelp zrozumienie usługi Power BI i w jaki sposób toouse go na platformie Azure:

* [Eksploruj zestawu danych w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Wprowadzenie do korzystania z hello Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Odświeżanie danych w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure i usługi Power BI — omówienie](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Dokumentacja
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Wprowadzenie tooAzure usługi fabryka danych](data-factory-introduction.md)
  * [Rozpoczynanie pracy z fabryką danych Azure](data-factory-build-your-first-pipeline.md)
  * [Korzystanie z działań niestandardowych w potoku usługi Azure Data Factory](data-factory-use-custom-activities.md)
* [Partia zadań Azure](https://azure.microsoft.com/documentation/services/batch/)

  * [Podstawowe informacje o partii zadań Azure](../batch/batch-technical-overview.md)
  * [Przegląd funkcji partii zadań Azure](../batch/batch-api-basics.md)
  * [Tworzenie i zarządzanie nimi konto partii zadań Azure w portalu Azure hello](../batch/batch-account-create-portal.md)
  * [Rozpoczynanie pracy z platformą .NET biblioteki usługi partia zadań Azure](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
