---
title: "aaaUse niestandardowych działań w potoku fabryki danych Azure"
description: "Dowiedz się, jak toocreate niestandardowych działań i używać ich w potoku fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Korzystanie z działań niestandardowych w potoku usługi Azure Data Factory

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

Istnieją dwa typy działań, które można używać w potoku fabryki danych Azure.

- [Działania przepływu danych](data-factory-data-movement-activities.md) toomove danych między [obsługiwane magazyny danych źródłowy i odbiorczy](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Działania przekształcania danych](data-factory-data-transformation-activities.md) tootransform danych przy użyciu obliczeniowe usług, takich jak Azure HDInsight, partii zadań Azure i usługi Azure Machine Learning. 

Utwórz toomove danych do/z magazynem danych, który fabryki danych nie obsługuje, **działania niestandardowego** z własnych danych przepływu logiki i użyj hello działania w potoku. Podobnie tootransform/przetwarzania danych w taki sposób, który nie jest obsługiwany przez fabrykę danych tworzenia działań niestandardowych z własną logikę przekształcania danych i użyj hello działania w potoku. 

Toorun działania niestandardowego można skonfigurować na **partii zadań Azure** puli maszyn wirtualnych lub z systemem Windows **Azure HDInsight** klastra. Korzystając z partii zadań Azure, można użyć tylko istniejącej puli partii zadań Azure. Natomiast podczas korzystania z usługi HDInsight, można użyć istniejącego klastra usługi HDInsight lub w klastrze, który jest automatycznie tworzony należy na żądanie w czasie wykonywania.  

Witaj następujący przewodnik zawiera instrukcje krok po kroku dotyczące tworzenia działań niestandardowych .NET i używania hello niestandardowego działania w potoku. wskazówki Hello używa **partii zadań Azure** połączonej usługi. połączona usługa Azure HDInsight toouse zamiast tego, tworzenie połączonej usługi typu **HDInsight** (własnego klastra usługi HDInsight) lub **HDInsightOnDemand** (fabryka danych powoduje utworzenie klastra usługi HDInsight na żądanie). Następnie należy skonfigurować hello toouse niestandardowe działanie usługi HDInsight połączone. Zobacz [użycia usługi Azure HDInsight połączone usługi](#use-hdinsight-compute-service) sekcji, aby uzyskać więcej informacji na temat używania usługi Azure HDInsight toorun hello niestandardowego działania.

> [!IMPORTANT]
> - Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows. Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux. Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.
> - Nie jest możliwe toouse bramę zarządzania danymi z działań niestandardowych tooaccess lokalnych źródeł danych. Obecnie [brama zarządzania danymi](data-factory-data-management-gateway.md) obsługuje tylko działania kopiowania hello i działania procedury składowanej w fabryce danych.   

## <a name="walkthrough-create-a-custom-activity"></a>Wskazówki: Tworzenie niestandardowego działania
### <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2012/2013/2015
* Pobierz i zainstaluj zestaw [SDK .NET Azure](https://azure.microsoft.com/downloads/).

### <a name="azure-batch-prerequisites"></a>Wymagania wstępne partii platformy Azure
W przewodniku hello możesz uruchomić własnych działań platformy .NET przy użyciu partii zadań Azure jako zasoby obliczeniowe. **Partia zadań Azure** to platforma usług do uruchomienia równoległego na dużą skalę i wysokiej wydajności aplikacji (HPC) wydajnie w chmurze hello obliczeniowych. Partia zadań Azure planuje toorun pracy obliczeniowych na zarządzanego **kolekcji maszyn wirtualnych**, i może automatycznie skalowania zasobów obliczeniowych zasobów toomeet hello potrzeb zadań. Zobacz [podstawowe informacje o partii zadań Azure] [ batch-technical-overview] artykułu szczegółowe omówienie hello usługi partia zadań Azure.

Samouczek hello należy utworzyć konto partii zadań Azure przy użyciu puli maszyn wirtualnych. Poniżej przedstawiono kroki hello:

1. Utwórz **konto partii zadań Azure** przy użyciu hello [portalu Azure](http://portal.azure.com). Zobacz [tworzenie i zarządzanie nimi konto partii zadań Azure] [ batch-create-account] artykułu, aby uzyskać instrukcje.
2. Zanotuj nazwę konta partii zadań Azure hello, klucz konta identyfikatora URI i nazwa puli. Należy je toocreate usługi partia zadań Azure połączone.
    1. Na stronie głównej hello konto partii zadań Azure, zobacz **adres URL** w hello następującego formatu: `https://myaccount.westus.batch.azure.com`. W tym przykładzie **myaccount** jest nazwą hello hello konto partii zadań Azure. Identyfikator URI używanych w definicji usługi hello połączony jest adresem URL hello bez nazwy hello hello konta. Na przykład: `https://<region>.batch.azure.com`.
    2. Kliknij przycisk **klucze** w menu po lewej stronie powitania i kopiowania hello **podstawowy klucz dostępu**.
    3. toouse istniejącej puli, kliknij przycisk **pule** w hello menu i zanotuj hello **identyfikator** hello puli. Jeśli nie masz istniejącej puli, przenieść toohello następnego kroku.     
2. Utwórz **puli partii zadań Azure**.

   1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **Przeglądaj** w hello menu po lewej stronie i kliknij przycisk **konta usługi partia zadań**.
   2. Wybierz użytkownika hello tooopen konto partii zadań Azure **konta usługi partia zadań** bloku.
   3. Kliknij przycisk **pule** kafelka.
   4. W hello **pule** bloku, kliknij przycisk Dodaj na powitania narzędzi tooadd puli.
      1. Wpisz identyfikator puli hello (identyfikator puli). Uwaga hello **identyfikator puli hello**; potrzebne podczas tworzenia hello rozwiązania fabryki danych.
      2. Określ **systemu Windows Server 2012 R2** hello ustawienia rodziny systemów operacyjnych.
      3. Wybierz **warstwę cenową węzła**.
      4. Wprowadź **2** jako wartość hello **docelowego w wersji dedykowanej** ustawienie.
      5. Wprowadź **2** jako wartość hello **maksymalna liczba zadań na węzeł** ustawienie.
   5. Kliknij przycisk **OK** toocreate hello puli.
   6. Zanotuj hello **identyfikator** hello puli. 



### <a name="high-level-steps"></a>Ogólne kroki
Poniżej przedstawiono hello dwa ogólne kroki, wykonywanych w ramach tego przewodnika: 

1. Tworzenie niestandardowego działania, który zawiera proste danych przekształcania/przetwarzania logiki.
2. Tworzenie fabryki danych Azure z potok, który używa hello działania niestandardowego.

### <a name="create-a-custom-activity"></a>Tworzenie niestandardowego działania
Utwórz toocreate .NET działań niestandardowych **Biblioteka klas programu .NET** projektu z klasy, która implementuje, który **IDotNetActivity** interfejsu. Ten interfejs jest tylko jedna metoda: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) i podpisie:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


Metoda Hello przyjmuje cztery parametry:

- **linkedServices**. Ta właściwość jest wyliczalny listę usług połączonych magazyn danych odwołuje się zestaw danych wejścia/wyjścia dla działania hello.   
- **zestawy danych**. Ta właściwość jest wyliczalny listę zestawów danych wejścia/wyjścia dla działania hello. Można użyć tego parametru tooget hello lokalizacji i schematów wynika z zestawów danych wejściowych i wyjściowych.
- **działanie**. Ta właściwość reprezentuje hello bieżącego działania. Może być używane tooaccess rozszerzone właściwości skojarzone z hello działań niestandardowych. Zobacz [dostępu właściwości rozszerzone](#access-extended-properties) szczegółowe informacje.
- **Rejestrator**. Ten obiekt umożliwia zapisanie komentarze debugowania tej powierzchni w dzienniku użytkownika hello hello potoku.

Witaj, metoda zwraca słownik, który może być działań niestandardowych toochain używane razem w przyszłości hello. Ta funkcja nie jest jeszcze zaimplementowana, więc Zwróć pusty słownik z metody hello.  

### <a name="procedure"></a>Procedura
1. Utwórz **Biblioteka klas programu .NET** projektu.
   <ol type="a">
     <li>Uruchom <b>programu Visual Studio 2017</b> lub <b>programu Visual Studio 2015</b> lub <b>programu Visual Studio 2013</b> lub <b>programu Visual Studio 2012</b>.</li>
     <li>Kliknij przycisk <b>pliku</b>, punktu zbyt<b>nowy</b>i kliknij przycisk <b>projektu</b>.</li>
     <li>Rozwiń węzeł <b>Szablony</b> i wybierz opcję <b>Visual C#</b>. W tym przewodniku Użyj C#, ale można użyć dowolnego .NET języka toodevelop hello działania niestandardowego.</li>
     <li>Wybierz <b>biblioteki klas</b> z hello listy typów projektu na powitania prawo. VS 2017 wybierz <b>biblioteki klas (.NET Framework)</b> </li>
     <li>Wprowadź <b>MyDotNetActivity</b> dla hello <b>nazwa</b>.</li>
     <li>Wybierz <b>C:\ADFGetStarted</b> dla hello <b>lokalizacji</b>.</li>
     <li>Kliknij przycisk <b>OK</b> toocreate hello projektu.</li>
   </ol>
2.Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.
3. W konsoli Menedżera pakietów hello, wykonaj następujące polecenie tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Importuj hello **usługi Azure Storage** pakietu NuGet w projekcie toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Uruchamianie usługi fabryka danych wymaga wersji hello 4.3 WindowsAzure.Storage. Jeśli dodasz tooa odwołanie do nowszej wersji zestawu Azure Storage w projekcie działań niestandardowych, zostanie wyświetlony błąd podczas działania hello. Błąd hello tooresolve, zobacz [izolacji elementu Appdomain](#appdomain-isolation) sekcji. 
5. Dodaj następujące hello **przy użyciu** plik źródłowy toohello instrukcje w projekcie hello.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Zmień nazwę hello hello **przestrzeni nazw** za**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Zmień nazwę hello klasy hello zbyt**MyDotNetActivity** i pochodną hello **IDotNetActivity** interfejsu pokazane na powitania następującego fragmentu kodu:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Witaj wdrożenie (Dodaj) **Execute** metody hello **IDotNetActivity** interfejsu toohello **MyDotNetActivity** hello klasy i skopiuj następujące metody toohello kodu przykładowej.

    Witaj następującym przykładowym zlicza hello wystąpienia terminu wyszukiwania hello ("Microsoft") w każdy obiekt blob skojarzony z wycinka danych.

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. Dodaj następujące metody pomocnicze hello: 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    Hello GetFolderPath metoda zwraca hello ścieżki toohello folderu, który hello zestawu danych punktów tooand hello GetFileName — metoda zwraca hello nazwę hello obiekt blob/pliku hello wskazuje zestawu danych. Jeśli użytkownik havefolderPath definiuje, korzystając ze zmiennych, takich jak {Year}, {Month}, {Day} itd., hello metoda zwraca ciąg hello, jak bez zamianę wartości środowiska uruchomieniowego. Zobacz [dostępu właściwości rozszerzone](#access-extended-properties) sekcji, aby uzyskać szczegółowe informacje dotyczące uzyskiwania dostępu do SliceStart, SliceEnd itp.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Hello metody Calculate oblicza hello liczbę wystąpień słowa kluczowego hello plików wejściowych (obiekty BLOB w folderze hello) firmy Microsoft. Witaj terminu wyszukiwania ("Microsoft") jest ustalony w kodzie hello.
10. Skompiluj projekt hello. Kliknij przycisk **kompilacji** hello menu i kliknij przycisk **Kompiluj rozwiązanie**.

    > [!IMPORTANT]
    > Ustaw 4.5.2 wersję programu .NET Framework jako hello platformy docelowej projektu: kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **właściwości** platformy docelowej hello tooset. Fabryki danych nie obsługuje niestandardowych działań skompilowany .NET Framework w wersji nowszej niż 4.5.2.

11. Uruchom **Eksploratora Windows**i przejdź zbyt**bin\debug** lub **bin\release** folder, w zależności od typu hello kompilacji.
12. Utwórz plik zip **MyDotNetActivity.zip** zawierający wszystkie hello pliki binarne w hello <project folder>\bin\Debug folderu. Zawierają hello **MyDotNetActivity.pdb** pliku, tak aby uzyskać dodatkowe szczegóły, takie jak numer wiersza w kodzie źródłowym hello, który spowodował problem hello, jeśli wystąpił błąd. 

    > [!IMPORTANT]
    > Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z nie podfolderach.

    ![Binarne pliki wyjściowe](./media/data-factory-use-custom-activities/Binaries.png)
14. Tworzenie kontenera obiektów blob o nazwie **customactivitycontainer** Jeśli jeszcze nie istnieje. 
15. Przekaż MyDotNetActivity.zip jako customactivitycontainer toohello obiektów blob w **ogólnego przeznaczenia** magazynu obiektów blob platformy Azure (gorącą nie/chłodnej magazynu obiektów Blob), który odwołuje się do AzureStorageLinkedService.  

> [!IMPORTANT]
> Jeśli dodawanie tego rozwiązania tooa .NET działania projektu w programie Visual Studio, zawierający projekt fabryki danych i dodać projekt działania too.NET odwołanie z projektu aplikacji hello fabryki danych nie ma potrzeby tooperform hello ostatnie dwa kroki tworzenia ręcznie Witaj pliku zip i przekazać go toohello magazynu ogólnego przeznaczenia obiektów blob platformy Azure. Podczas publikowania jednostek fabryki danych przy użyciu programu Visual Studio, te kroki automatycznie są wykonywane przez proces publikowania hello. Aby uzyskać więcej informacji, zobacz [fabryki danych projektu programu Visual Studio](#data-factory-project-in-visual-studio) sekcji.

## <a name="create-a-pipeline-with-custom-activity"></a>Utworzyć potok z działań niestandardowych
Utworzono niestandardowe działania i przekazać plik zip hello z kontenera obiektów blob tooa plików binarnych w **ogólnego przeznaczenia** konta magazynu Azure. W tej sekcji utworzysz fabryki danych Azure z potok, który używa hello działania niestandardowego.

Witaj wejściowego zestawu danych dla działań niestandardowych hello reprezentuje obiektów blob (pliki) w folderze customactivityinput hello adftutorial kontenera w magazynie obiektów blob hello. Witaj wyjściowego zestawu danych działania hello reprezentuje obiekty BLOB danych wyjściowych w folderze customactivityoutput hello adftutorial kontenera w magazynie obiektów blob hello.

Utwórz **plik.txt** pliku z hello poniżej zawartości i przekaż go za**customactivityinput** folderu hello **adftutorial** kontenera. Tworzenie kontenera adftutorial hello, jeśli już istnieje. 

```
test custom activity Microsoft test custom activity Microsoft
```

folder wejściowy Hello odpowiada wycinek tooa w fabryce danych Azure, nawet wtedy, gdy hello folder ma dwa lub więcej plików. Każdy wycinek jest przetwarzany przez potok hello, działania niestandardowego hello iterację wszystkich hello obiektów blob w folderze wejściowych powitania dla tego wycinka.

Zobaczysz, że jeden wyjściowy plik z folderu adftutorial\customactivityoutput hello z jednego lub więcej wierszy (tak samo jak liczbę obiektów blob w folderze wejściowych hello):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Poniżej przedstawiono kroki hello, wykonywanej w tej sekcji:

1. Utwórz **fabryki danych**.
2. Utwórz **połączone usługi** hello partii zadań Azure puli maszyn wirtualnych, na których hello działania niestandardowego uruchamia i hello magazynu Azure, który przechowuje hello obiekty BLOB wejścia/wyjścia.
3. Utwórz dane wejściowe i wyjściowe **zestawów danych** reprezentujące dane wejściowe i wyjściowe hello działania niestandardowego.
4. Utwórz **potoku** używającą hello działania niestandardowego.

> [!NOTE]
> Utwórz hello **plik.txt** i przekaż go tooa kontenera obiektów blob, jeśli jeszcze tego nie zrobiono. Zobacz instrukcje w powyższej sekcji hello.   

### <a name="step-1-create-hello-data-factory"></a>Krok 1: Tworzenie fabryki danych hello
1. Po zalogowaniu toohello w portalu Azure hello następujące kroki:
   1. Kliknij przycisk **nowy** w menu po lewej stronie powitania.
   2. Kliknij przycisk **dane i analiza** w hello **nowy** bloku.
   3. Kliknij przycisk **fabryki danych** na powitania **analizy danych** bloku.
   
    ![Nowe menu fabryki danych Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. W hello **nowa fabryka danych** bloku, wprowadź **CustomActivityFactory** dla hello nazwy. Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: **nazwa fabryki danych "CustomActivityFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład **yournameCustomActivityFactory**) i spróbuj utworzyć ponownie.

    ![Nowy blok fabryki danych Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Kliknij przycisk **Nazwa grupy zasobów**i wybierz istniejącą grupę zasobów lub Utwórz grupę zasobów.
4. Sprawdź, czy są używa hello poprawne **subskrypcji** i **region** miejscu toobe fabryki danych hello utworzony.
5. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.
6. Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure.
7. Po hello fabryki danych został utworzony pomyślnie, zobacz hello fabryki danych bloku, który umożliwia hello zawartość hello fabryki danych.
    
    ![Blok Fabryka danych](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Krok 2: Tworzenie usługi połączonej
Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług. W tym kroku możesz połączyć Twoje konto usługi Azure Storage i fabryki danych tooyour konto partii zadań Azure.

#### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
1. Kliknij hello **tworzenie i wdrażanie** Kafelek na powitania **FABRYKI danych** bloku **CustomActivityFactory**. Zostanie wyświetlony hello Edytor fabryki danych.
2. Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **magazynu Azure**. Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.
    
    ![Nowy magazyn danych - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Zastąp `<accountname>` z nazwą konta magazynu Azure i `<accountkey>` z kluczem dostępu z hello kontem magazynu platformy Azure. toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Usługa Azure Storage zbędne usługi](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

#### <a name="create-azure-batch-linked-service"></a>Tworzenie usługi partia zadań Azure połączone
1. W hello Edytor fabryki danych, kliknij przycisk **... Więcej** na pasku poleceń hello, kliknij przycisk **nowych obliczeń**, a następnie wybierz **partii zadań Azure** hello menu.

    ![Nowe obliczeń - partii zadań Azure](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Wprowadź hello następującego skryptu JSON toohello zmiany:

   1. Określ nazwę konta partii zadań Azure hello **accountName** właściwości. Witaj **adres URL** z hello **bloku konta usługi partia zadań Azure** jest zgodny z formatem hello: `http://accountname.region.batch.azure.com`. Dla hello **batchUri** właściwości w hello JSON, należy tooremove `accountname.` z hello adresu URL i użyj hello `accountname` dla hello `accountName` właściwości JSON.
   2. Określ klucz konta partii zadań Azure hello hello **accessKey** właściwości.
   3. Określ nazwę hello puli hello został utworzony jako część wymagania wstępne dotyczące hello **poolName** właściwości. Można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.
   4. Określ identyfikator URI usługi partia zadań Azure dla hello **batchUri** właściwości. Przykład: `https://westus.batch.azure.com`.  
   5. Określ hello **AzureStorageLinkedService** dla hello **linkedServiceName** właściwości.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Dla hello **poolName** właściwości, można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.

      > [!IMPORTANT]
      > Hello usługi fabryka danych nie obsługuje opcji na żądanie dla partii zadań Azure, w przeciwieństwie do usługi HDInsight. Pulę partii zadań Azure można używać tylko w fabryce danych Azure.   
    

### <a name="step-3-create-datasets"></a>Krok 3: Tworzenie zestawów danych
W tym kroku możesz utworzyć zestawy danych toorepresent w danych wejściowych i dane wyjściowe.

#### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**, a następnie wybierz **magazynu obiektów Blob Azure** z menu rozwijanego hello.
2. Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   Utworzyć potok w dalszej części tego przewodnika, czas rozpoczęcia: 2016-11-16T00:00:00Z i na końcu czasu: 2016-11-16T05:00:00Z. Co godzinę, jest zaplanowane tooproduce danych co pięć wycinków wejścia/wyjścia (między **00**: 00:00 -> **05**: 00:00).

   Witaj **częstotliwość** i **interwał** dla zestawu danych wejściowych hello jest ustawiony za**godzina** i **1**, co oznacza, że hello danych wejściowych jest dostępny co godzinę. W tym przykładzie jest takie same hello hello intputfolder pliku (plik.txt).

   Poniżej przedstawiono hello godziny rozpoczęcia dla każdego wycinka, która jest reprezentowana przez SliceStart zmienna w hello powyżej fragment kodu JSON.
3. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **InputDataset**. Upewnij się, że widoczny hello **tabeli UTWORZONE pomyślnie** wiadomości na pasku tytułu hello hello edytora.

#### <a name="create-an-output-dataset"></a>Tworzenie wyjściowego zestawu danych
1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**, a następnie wybierz **magazynu obiektów Blob Azure**.
2. Zastąp hello skryptu JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     Lokalizacja danych wyjściowych jest **adftutorial/customactivityoutput/** i nazwa pliku wyjściowego jest RRRR MM-dd-HH.txt w przypadku RRRR MM-dd gg hello rok, miesiąc, datę i godzinę wycinek hello tworzonym. Zobacz [dokumentacja dla deweloperów] [ adf-developer-reference] szczegółowe informacje.

    Obiekt blob/plik wyjściowy jest generowany dla każdego wejściowego wycinka. Oto, jak dla każdego wycinka nosi nazwę pliku wyjściowego. Wszystkie pliki wyjściowe hello są generowane w jednym folderze wyjściowym: **adftutorial\customactivityoutput**.

   | Wycinek | Godzina rozpoczęcia | Plik wyjściowy |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Należy pamiętać, że wszystkie pliki hello w folderze wejściowych część wycinek z godziny rozpoczęcia hello wymienionych powyżej. Podczas przetwarzania tego wycinka działania niestandardowego hello skanowania za pomocą każdego pliku i tworzy wiersz w pliku wyjściowym hello hello liczby wystąpień terminu wyszukiwania ("Microsoft"). Jeśli istnieją trzy pliki w hello inputfolder, istnieją trzy wiersze w pliku wyjściowym hello każdego co godzinę wycinka: 2016-11-16-00.txt 2016-11-16:01:00:00.txt itp.
3. Witaj toodeploy **OutputDataset**, kliknij przycisk **Wdróż** na powitania paska poleceń.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Tworzenie i uruchamianie potok, który używa hello niestandardowego działania
1. W hello Edytor fabryki danych, kliknij przycisk **... Więcej**, a następnie wybierz **nowy potok** na powitania paska poleceń. 
2. Zastąp hello JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Należy zwrócić uwagę hello następujące punkty:

   * **Współbieżność** ustawiono zbyt**2** tak, aby dwa wycinków są przetwarzane równolegle przez 2 maszyny wirtualne w puli partii zadań Azure hello.
   * W sekcji działania hello jest jedno działanie i jest typu: **DotNetActivity**.
   * **AssemblyName** jest ustawiona na nazwę toohello hello biblioteki DLL: **MyDotnetActivity.dll**.
   * **Punkt wejścia** ustawiono zbyt**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** ustawiono zbyt**AzureStorageLinkedService** wskazującego toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego. Jeśli korzystasz z innego konta usługi Azure Storage dla wejścia/wyjścia plików i hello działania niestandardowego pliku zip, utworzysz innego połączoną usługą magazynu Azure. W tym artykule przyjęto założenie, że używasz hello tego samego konta magazynu Azure.
   * **PackageFile** ustawiono zbyt**customactivitycontainer/MyDotNetActivity.zip**. Jest w formacie hello: containerforthezip/nameofthezip.zip.
   * przyjmuje działania niestandardowego Hello **InputDataset** jako dane wejściowe i **OutputDataset** jako dane wyjściowe.
   * Hello właściwość linkedServiceName działania niestandardowego hello punktów toohello **AzureBatchLinkedService**, który informuje usługi fabryka danych Azure tego działania niestandardowego hello musi toorun na maszynach wirtualnych Azure partii.
   * **isPaused** właściwość jest ustawiona zbyt**false** domyślnie. potok Hello uruchamia natychmiast w tym przykładzie, ponieważ wycinków hello uruchomić w przeszłości hello. Można ustawić tej właściwości tootrue toopause hello potoku i ustaw ją toorestart toofalse Wstecz.
   * Witaj **start** czasu i **zakończenia** czasy są **pięć** godziny od siebie i wycinki są tworzone co godzinę, więc pięć wycinków są produkowane przez potok hello.
3. toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania paska poleceń.

### <a name="monitor-hello-pipeline"></a>Monitor hello potoku
1. W bloku fabryki danych hello w hello portalu Azure, kliknij przycisk **Diagram**.

    ![Kafelek Diagram](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. W hello widoku diagramu kliknij przycisk hello OutputDataset.

    ![Widok diagramu](./media/data-factory-use-custom-activities/diagram.png)
3. Powinny być widoczne czy hello pięć wycinki danych wyjściowych znajdują się w stanie gotowe hello. Jeśli nie są w stanie gotowe hello, nie została opracowana jeszcze. 

   ![Wycinki danych wyjściowych](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Sprawdź, czy pliki wyjściowe hello są generowane w magazynie obiektów blob hello w hello **adftutorial** kontenera.

   ![dane wyjściowe z działań niestandardowych][image-data-factory-ouput-from-custom-activity]
5. Po otwarciu pliku wyjściowego hello powinien pojawić się hello dane wyjściowe podobne toohello następujące dane wyjściowe:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Użyj hello [portalu Azure] [ azure-preview-portal] lub toomonitor poleceń cmdlet programu Azure PowerShell z fabryki danych, potoki i zestawów danych. Można wyświetlić wiadomości z hello **ActivityLogger** w kodzie hello hello niestandardowego działania w dziennikach hello (w szczególności 0.log użytkownika), które można pobrać z portalu hello lub przy użyciu poleceń cmdlet.

   ![Pobierz dzienniki z działań niestandardowych][image-data-factory-download-logs-from-custom-activity]

Zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md) szczegółowy opis kroków monitorowania zestawy danych i potoki.      

## <a name="data-factory-project-in-visual-studio"></a>Projekt fabryki danych w programie Visual Studio  
Można tworzyć i publikować jednostek fabryki danych przy użyciu programu Visual Studio, a za pomocą portalu Azure. Szczegółowe informacje na temat tworzenia i publikowania jednostek fabryki danych przy użyciu programu Visual Studio, zobacz [kompilacji swój pierwszy potok, za pomocą programu Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) i [kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artykuły.

Witaj, następujące dodatkowe kroki w przypadku tworzenia projektu fabryki danych w programie Visual Studio:
 
1. Dodaj hello fabryki danych projektu toohello rozwiązania Visual Studio, zawierającego hello projektu działania niestandardowego. 
2. Dodać projekt działania .NET toohello odwołanie z hello fabryki danych projektu. Kliknij prawym przyciskiem myszy projekt w fabryce danych, wskaż zbyt**Dodaj**, a następnie kliknij przycisk **odwołania**. 
3. W hello **Dodaj odwołanie** okno dialogowe, wybierz opcję hello **MyDotNetActivity** projektu, a następnie kliknij przycisk **OK**.
4. Tworzenie i publikowanie hello rozwiązania.

    > [!IMPORTANT]
    > Podczas publikowania jednostek fabryki danych pliku zip jest automatycznie tworzony i jest przekazany toohello kontenera obiektów blob: customactivitycontainer. Jeśli hello kontenera obiektów blob nie istnieje, jest on automatycznie tworzony zbyt.  


## <a name="data-factory-and-batch-integration"></a>Integracja z fabryki danych i usługi partia zadań
Witaj usługi fabryka danych tworzy zadanie w partii zadań Azure o nazwie hello: **adf poolname: xxx zadania**. Kliknij przycisk **zadania** z menu po lewej stronie powitania. 

![Fabryka danych Azure - zadań wsadowych](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Zadanie jest tworzone przy każdym uruchomieniu działania wycinek. W przypadku pięć toobe gotowy wycinków przetwarzane pięć zadań są tworzone w ramach tego zadania. Jeśli istnieje wiele węzłów obliczeniowych w puli partii hello, co najmniej dwa wycinków można uruchomić równolegle. Jeśli obliczeniowe hello maksymalną zadań na zestaw węzłów zbyt > 1, może także zawierać więcej niż jeden wycinek uruchomionych na powitania tego samego obliczeń.

![Fabryka danych Azure - zadań zadania wsadowego](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

powitania po diagram ilustruje hello relacji między fabryki danych Azure i partii zadań.

![Fabryka danych & partii](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Rozwiązywanie problemów z błędami
Rozwiązywanie problemów z składa się z kilku podstawowych techniki:

1. Jeśli zostanie wyświetlony następujący błąd hello, używasz magazynu obiektów blob aktywny/chłodnej zamiast przy użyciu magazynu obiektów blob platformy Azure ogólnego przeznaczenia. Przekaż tooa pliku zip hello **ogólnego przeznaczenia konta magazynu Azure**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Jeśli zostanie wyświetlony następujący błąd hello, upewnij się, że hello nazwy klasy hello w hello CS dopasowań hello nazwa pliku podana dla hello **punktu wejścia** właściwości w potoku hello JSON. W przewodniku hello jest nazwa klasy hello: MyDotNetActivity i hello punktu wejścia w hello JSON: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Jeśli hello nazwy są zgodne, potwierdź, że wszystkie pliki binarne hello są w hello **folderu głównego** hello pliku zip. Oznacza to, że podczas otwierania pliku zip hello powinna zostać wyświetlona wszystkie pliki hello w folderze głównym hello, a nie wszystkie podfoldery.   
3. Jeśli hello wycinek wejściowy nie jest ustawiona zbyt**gotowe**, potwierdź poprawność struktury folderów wejściowych hello i **plik.txt** istnieje w folderach wejściowych hello.
3. W hello **Execute** metody działania niestandardowego, użyj hello **IActivityLogger** toolog informacji o obiekcie, ułatwiające rozwiązywanie problemów. wiadomości powitania rejestrowane uwzględniane w plikach dziennika użytkownika hello (co najmniej jeden plik o nazwie: 0.log użytkownika, 1.log użytkownika, użytkownik 2.log itp.).

   W hello **OutputDataset** bloku, kliknij przycisk hello wycinek toosee hello **WYCINKA danych** bloku dla tego wycinka. Zostanie wyświetlony **uruchomień działania** dla tego wycinka. Powinny pojawić się jeden uruchamiania dla wycinka hello działania. Jeśli na pasku poleceń powitania kliknij przycisk Uruchom, możesz uruchomić innego działania Uruchom hello tego samego wycinka.

   Po kliknięciu przycisku uruchamiania działania hello Zobacz hello **szczegóły uruchomienia działania** bloku zawierającego listę plików dziennika. Zobaczysz zarejestrowane komunikaty, w pliku user_0.log hello. Po wystąpieniu błędu, zobacz trzech uruchomień działania ponieważ liczby ponownych prób hello ustawiono too3 w potoku hello/aktywność JSON. Po kliknięciu przycisku uruchamiania działania hello możesz Zobacz pliki dziennika hello możesz przejrzeć tootroubleshoot hello błędu.

   W hello listę plików dziennika, kliknij przycisk hello **0.log użytkownika**. W prawym panelu hello są wyniki hello przy użyciu hello **IActivityLogger.Write** metody. Jeśli nie widzisz wszystkich wiadomości, sprawdź, czy istnieje więcej plików dziennika o nazwie: user_1.log, user_2.log itp. W przeciwnym razie kod hello mogła zakończyć się niepowodzeniem po hello ostatniego logowania wiadomości.

   Ponadto sprawdź **0.log systemu** za wszelkie komunikaty o błędach systemu i wyjątki.
4. Zawierają hello **PDB** plików w pliku zip hello w celu hello szczegóły błędu mają informacje takie jak **stosu wywołań** po wystąpieniu błędu.
5. Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z nie podfolderach.
6. Upewnij się, że hello **assemblyName** (MyDotNetActivity.dll), **punktu wejścia**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) i **packageLinkedService** (powinna wskazywać toohello **ogólnego przeznaczenia**magazynu obiektów blob platformy Azure, który zawiera plik zip hello) są ustawione wartości toocorrect.
7. Stałe błędu i chcesz wycinek hello tooreprocess, kliknij prawym przyciskiem myszy hello wycinek hello **OutputDataset** bloku i kliknij przycisk **Uruchom**.
8. Jeśli zostanie wyświetlony następujący błąd hello, używasz pakietu usługi Azure Storage hello wersji > 4.3.0. Uruchamianie usługi fabryka danych wymaga wersji hello 4.3 WindowsAzure.Storage. Zobacz [izolacji elementu Appdomain](#appdomain-isolation) sekcji Obejście należy używać hello nowszej wersji zestawu Azure Storage. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Jeśli używasz wersji hello 4.3.0 pakietu usługi Azure Storage, Usuń hello istniejące odwołanie tooAzure magazynu pakietu wersji > 4.3.0. Następnie uruchom następujące polecenie w konsoli Menedżera pakietów NuGet hello. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Tworzenie projektu hello. Usuń zespół Azure.Storage wersji > 4.3.0 z folderu bin\Debug hello. Utwórz plik zip zawierający pliki binarne i pliku PDB hello. Stary plik zip hello zamienić na w kontenerze obiektów blob hello (customactivitycontainer). Uruchom ponownie hello wycinków, które zakończyły się niepowodzeniem (kliknij prawym przyciskiem myszy wycinek i kliknij przycisk Uruchom).   
8. działania niestandardowego Hello nie używa hello **app.config** plików z pakietu. W związku z tym jeśli kod odczytuje wszelkie parametry połączenia z pliku konfiguracji hello, działa w czasie wykonywania. Witaj najlepsze rozwiązanie przy użyciu partii zadań Azure jest toohold żadnych kluczy tajnych w **Azure KeyVault**, użyj hello tooprotect główną usługi na podstawie certyfikatu **keyvault**i dystrybuowanie hello certyfikatu tooAzure puli partii. Witaj działania niestandardowego .NET, a następnie mogą uzyskiwać dostęp do kluczy tajnych z hello KeyVault w czasie wykonywania. To rozwiązanie jest ogólnego rozwiązania i mogą być skalowane tooany typu klucza tajnego, nie tylko w parametrach połączenia.

   Istnieje obejście łatwiejsze (ale nie najlepiej): można utworzyć **Azure SQL połączona usługa** ustawień parametrów połączenia, tworzenie połączonej usługi i dataset hello łańcucha jako fikcyjny wejściowy zestaw danych tekst hello używa zestawu danych toohello niestandardowego działania .NET. Mogą być następnie hello dostępu połączone usługi parametry połączenia w hello działania niestandardowego kodu.  

## <a name="update-custom-activity"></a>Aktualizowanie działań niestandardowych
Po zaktualizowaniu hello kodu dla działań niestandardowych hello skompiluj go i przekazać hello plik zip, który zawiera nowego magazynu obiektów blob toohello plików binarnych.

## <a name="appdomain-isolation"></a>Izolacja domeny aplikacji
Zobacz [Cross próbki AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) który pokazuje sposób toocreate działania niestandardowego, który nie jest ograniczone wersji tooassembly używanych przez uruchamianie fabryki danych hello (przykład: WindowsAzure.Storage v4.3.0 Newtonsoft.Json v6.0.x, itp.).

## <a name="access-extended-properties"></a>Dostęp do właściwości rozszerzone
Właściwości rozszerzone można zadeklarować w działaniu hello JSON, jak pokazano w hello następujące przykładowe:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


W przykładzie hello są dwie właściwości rozszerzone: **SliceStart** i **DataFactoryName**. wartość Hello SliceStart opiera się na powitania SliceStart zmienna. Zobacz [zmienne systemowe](data-factory-functions-variables.md) listę zmiennych obsługiwany system. wartość Hello DataFactoryName jest ustalony tooCustomActivityFactory.

tooaccess tych właściwości w hello rozszerzone **Execute** metody toohello podobny kod Użyj następującego kodu:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Automatyczne skalowanie partii zadań Azure
Można również utworzyć puli partii zadań Azure z **skalowania automatycznego** funkcji. Na przykład można utworzyć puli partii zadań azure 0 dedykowanych maszyn wirtualnych i formuły skalowania automatycznego na podstawie hello liczby oczekujących zadań. 

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

## <a name="use-hdinsight-compute-service"></a>Korzystanie z usługi obliczeniowe HDInsight
W przewodniku hello używane są działania niestandardowe hello toorun obliczeniowych partii zadań Azure. Można również użyć klastra usługi HDInsight opartej na systemie Windows lub ma fabryki danych tworzenia klastra usługi HDInsight opartej na systemie Windows na żądanie i ma uruchamiania w klastrze usługi HDInsight hello działania niestandardowe hello. Poniżej przedstawiono ogólne kroki hello przy użyciu klastra usługi HDInsight.

> [!IMPORTANT]
> Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows. Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux. Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.
 

1. Tworzenie usługi Azure HDInsight połączone.   
2. HDInsight Użyj połączonej usługi zamiast **AzureBatchLinkedService** hello w potoku JSON.

Jeśli chcesz, aby tootest go z przewodnikiem hello, zmień **start** i **zakończenia** razy dla potoku hello tak, aby można było testować hello scenariusz hello usługi Azure HDInsight.

#### <a name="create-azure-hdinsight-linked-service"></a>Tworzenie połączonej usługi Azure HDInsight
Hello usługi fabryka danych Azure obsługuje tworzenie klastra na żądanie i korzystać z niego dane wyjściowe tooprocess tooproduce wejściowego. Można również użyć własnego klastra tooperform hello takie same. Korzystając z klastrem usługi HDInsight na żądanie, klaster pobiera utworzone dla każdego wycinka. Korzystając z klastrem usługi HDInsight, klaster hello jest gotowy tooprocess natychmiast hello wycinka. W związku z tym korzystając z klastra na żądanie, nie widać danych wyjściowych hello tak szybko, jak kiedy używać własnego klastra.

> [!NOTE]
> W czasie wykonywania wystąpienia działania .NET działa tylko na jednym węźle procesu roboczego w klastrze HDInsight hello; nie może być skalowana toorun na wielu węzłach. Wiele wystąpień programu .NET działania można uruchomić równolegle w różnych węzłach klastra usługi HDInsight hello.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse klaster usługi HDInsight na żądanie
1. W hello **portalu Azure**, kliknij przycisk **Utwórz i wdróż** stronie głównej hello fabryki danych.
2. W hello Edytor fabryki danych, kliknij przycisk **nowych obliczeń** polecenia hello paska i wybierz pozycję **klastra usługi HDInsight na żądanie** hello menu.
3. Wprowadź hello następującego skryptu JSON toohello zmiany:

   1. Dla hello **wartość clusterSize** właściwości, określ rozmiar hello hello klastra usługi HDInsight.
   2. Dla hello **timeToLive** właściwości, określ, jak długo powitania klienta może być bezczynne, zanim ich usunięcia.
   3. Dla hello **wersji** właściwości, określ wersję HDInsight hello ma toouse. Jeśli należy wykluczyć tę właściwość, najnowsza wersja hello jest używany.  
   4. Dla hello **linkedServiceName**, określ **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows. Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux. Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.

4. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse klastrem usługi HDInsight:
1. W hello **portalu Azure**, kliknij przycisk **Utwórz i wdróż** stronie głównej hello fabryki danych.
2. W hello **Edytor fabryki danych**, kliknij przycisk **nowych obliczeń** polecenia hello paska i wybierz pozycję **klastra usługi HDInsight** hello menu.
3. Wprowadź hello następującego skryptu JSON toohello zmiany:

   1. Dla hello **clusterUri** właściwości, wprowadź adres URL powitania dla Twojej usługi HDInsight. Na przykład: https://<clustername>.azurehdinsight.net/     
   2. Dla hello **UserName** właściwości, wprowadź nazwę użytkownika hello mającego klastra usługi HDInsight toohello dostępu.
   3. Dla hello **hasło** właściwości, wprowadź hasło hello hello użytkownika.
   4. Dla hello **LinkedServiceName** właściwości, wprowadź **AzureStorageLinkedService**.
4. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) szczegółowe informacje.

W hello **potoku JSON**, używanie usługi HDInsight (na żądanie lub własne) połączonej usługi:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Tworzenie niestandardowego działania przy użyciu zestawu .NET SDK
W przewodniku hello w tym artykule Tworzenie fabryki danych z potok, który używa niestandardowego działania hello hello portalu Azure. Witaj następującego kodu pokazuje, jak toocreate hello fabryki danych przy użyciu zestawu .NET SDK zamiast tego. Można znaleźć więcej informacji o korzystaniu z zestawu SDK tooprogrammatically tworzenie potoków w hello [utworzyć potok z działania kopiowania przy użyciu interfejsu API platformy .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artykułu. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Debugowanie działań niestandardowych w programie Visual Studio
Witaj [fabryki danych Azure - lokalnego środowiska](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) przykładem w witrynie GitHub zawiera narzędzie umożliwiający toodebug niestandardowych działań platformy .NET w programie Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Przykład niestandardowych działań w witrynie GitHub
| Przykład | Jakie niestandardowe działanie robi |
| --- | --- |
| [Narzędzie do pobierania danych HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Pobiera dane z tooAzure punkt końcowy HTTP magazynu obiektów Blob przy użyciu działań niestandardowych C# w fabryce danych. |
| [Przykładowe wskaźniki nastrojów klientów analizy w usłudze Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Wywołuje model usługi uczenie Maszynowe Azure i analizy wskaźniki nastrojów klientów oceniania, prognozowania itp. |
| [Uruchom skrypt języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |Wywołuje skrypt języka R, uruchamiając RScript.exe w klastrze usługi HDInsight, na którym jest już zainstalowany R na nim. |
| [Krzyżowe AppDomain .NET działania](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Używa innego zestawu wersji z takich, które jest używane przez hello uruchamiania usługi fabryka danych |
| [Ponowne przetworzenie modelu w usług Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Ponownego przetwarzania modelu w usług Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
