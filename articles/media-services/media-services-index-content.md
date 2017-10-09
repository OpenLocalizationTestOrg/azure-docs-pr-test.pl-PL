---
title: "aaaIndexing plikach multimedialnych za pomocą usługi Azure Media indeksatora"
description: "Indeksator usługi Azure Media pozwala toomake zawartości z możliwością wyszukiwania plików multimedialnych i toogenerate wykaz pełnotekstowy dla i słów kluczowych. W tym temacie przedstawiono sposób toouse indeksatora nośnika."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Indeksowanie plików multimedialnych na pliki z indeksatora multimediów Azure
Indeksator usługi Azure Media pozwala toomake zawartości z możliwością wyszukiwania plików multimedialnych i toogenerate wykaz pełnotekstowy dla i słów kluczowych. Możesz przetwarzać jeden plik multimediów lub wiele plików multimediów w partii.  

> [!IMPORTANT]
> Podczas indeksowania zawartości, upewnij się, że toouse plików multimedialnych, które mają bardzo jasne mowy (bez muzyką w tle, szumu, efekty lub szumów mikrofonu). Oto kilka przykładów odpowiedniej zawartości: rejestrowane spotkań, wykładów lub prezentacji. Witaj następującej zawartości może nie nadawać się do indeksowania: filmy, programy telewizyjne, wszystko z mieszanym audio i efekty, nieprawidłowo zarejestrowana zawartości za pomocą szumu tła (szumów).
> 
> 

Zadania indeksowania można wygenerować hello następujące dane wyjściowe:

* Zamknięte pliki podpisu w hello następujących formatów: **SAMI**, **TTML**, i **WebVTT**.
  
    Pliki napisów obejmują tag o nazwie Recognizability, których wyniki zadania indeksowania oparte na jak rozpoznać mowy hello hello źródła wideo jest.  Możesz użyć wartości hello plików wyjściowych tooscreen Recognizability dla użyteczność. Niski wynik będzie oznaczać słabych wyników indeksowania powodu tooaudio jakości.
* Plik ze słowami kluczowymi (XML).
* Audio indeksowania plików obiektów blob (AIB) do użytku z programem SQL server.
  
    Aby uzyskać więcej informacji, zobacz [przy użyciu plików AIB z indeksatora multimediów Azure i SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

W tym temacie pokazano, jak indeksowania toocreate zadania zbyt**indeksu zasobów** i **indeksu wiele plików**.

Aby hello najnowsze aktualizacje usługi Azure Media indeksatora, zobacz [blogi Media Services](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Za pomocą plików konfiguracji i manifestu dla zadania indeksowania
Więcej szczegółów można określić dla zadań indeksowania przy użyciu konfiguracji zadania. Na przykład można określić które toouse metadanych dla pliku nośnika. Metadane używane przez tooexpand aparat języka hello jego słownictwa i znacznie zwiększa dokładność rozpoznawania mowy hello.  Możesz są również stanie toospecify plików żądanego wyniku.

Wiele plików multimedialnych może także przetwarzać jednocześnie przy użyciu pliku manifestu.

Aby uzyskać więcej informacji, zobacz [dla usługi Azure Media indeksatora ustawień wstępnych zadań](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Indeksu zasobów
Witaj następująca metoda przekazuje plik nośnika jako zasób i tworzy zasób hello tooindex zadania.

Należy pamiętać, że jeśli nie określono żadnych pliku konfiguracji, pliku multimedialnego hello będzie indeksowany przy użyciu wszystkich ustawień domyślnych.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Pliki wyjściowe
Domyślnie zadania indeksowania generuje hello następujące pliki wyjściowe. w pierwszym zawartości wyjściowej hello będą przechowywane pliki Hello.

W przypadku więcej niż jeden plik wejściowy nośnika indeksatora spowoduje wygenerowanie pliku manifestu dla danych wyjściowych zadania hello, o nazwie "JobResult.txt". Dla każdego pliku wejściowego nośnika hello AIB wynikowy, SAMI, TTML, WebVTT pliki — słowo kluczowe sekwencyjnie numerowane i o nazwie przy użyciu hello "Alias".

| Nazwa pliku | Opis |
| --- | --- |
| **InputFileName.aib** |Plik obiektu blob indeksowania audio. <br/><br/> Plik dźwiękowy indeksowanie obiektów Blob (AIB) jest plikiem binarnym, które można przeszukiwać w Microsoft SQL server przy użyciu wyszukiwania pełnotekstowego.  Plik AIB Hello jest większe możliwości niż pliki podpis prostego powitania, ponieważ zawiera alternatywy dla każdego wyrazu, co pozwala znacznie więcej możliwości wyszukiwania. <br/> <br/>Wymaga instalacji hello hello dodatek indeksatora SQL na maszynie uruchomionych usług Microsoft SQL server 2008 lub nowszym. Wyszukiwanie hello AIB przy użyciu programu Microsoft SQL server wyszukiwanie pełnotekstowe zapewnia dokładniejsze wyniki wyszukiwania niż wyszukiwanie hello zamknięte pliki podpisów generowanych przez WAMI. Jest to spowodowane hello AIB zawiera słowa zastępcze dźwięk, które podobne, natomiast hello zamknięty podpis pliki zawierają hello najwyższy word zaufania dla każdego segmentu hello audio. Jeśli wyszukiwanie rozmowy wyrazów ma znaczenie upmost, następnie zaleca toouse hello AIB w połączeniu z programem Microsoft SQL Server.<br/><br/> toodownload hello dodatek, kliknij przycisk <a href="http://aka.ms/indexersql">Azure Media indeksatora SQL dodatek</a>. <br/><br/>Jego jest również możliwe tooutilize innych aparatów wyszukiwania takich jak Apache Lucene/Solr toosimply indeksu hello wideo na podstawie podpisu hello zamknięte i słowo kluczowe pliki XML, ale spowoduje to mniej dokładne wyniki wyszukiwania. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Podpis (DW) zamkniętych plikach w formatach SAMI TTML i WebVTT.<br/><br/>Mogą być używane toomake audio i wideo plików dostępny toopeople niepełnosprawne przesłuchanie.<br/><br/>Zamknięte pliki podpis zawierać tag o nazwie <b>Recognizability</b> który wyników zadania indeksowania oparte na jak rozpoznać mowy hello hello źródła wideo jest.  Można użyć wartości hello <b>Recognizability</b> tooscreen dane wyjściowe pliki użyteczność. Niski wynik będzie oznaczać słabych wyników indeksowania powodu tooaudio jakości. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Pliki — słowo kluczowe i informacje. <br/><br/>Plik — słowo kluczowe jest plik XML, który zawiera słowa kluczowe wyodrębnione z zawartości mowy hello, częstotliwości i przesunięcia informacje. <br/><br/>Plik informacji o to plik tekstowy, który zawiera szczegółowe informacje dotyczące każdego terminu rozpoznany. pierwszy wiersz Hello specjalne i zawiera hello Recognizability wynik. Każdej kolejny wiersz znajduje się lista tabulatorem hello następujące dane: start czasu, czas zakończenia, word/frazy, zaufania. Witaj czas jest podany w sekundach i zaufania hello jest podawana jako liczbę z zakresu od 0-1. <br/><br/>Przykład wiersza: "word 1,20 wysokości 1,45 0,67" <br/><br/>Te pliki mogą być używane dla wielu celów, takich jak analiza mowy tooperform, lub toosearch narażonych silników takich jak Bing, Google lub Microsoft SharePoint toomake hello plików multimedialnych mogą szybciej odnajdywać lub nawet używane toodeliver więcej odpowiednich reklam. |
| **JobResult.txt** |Dane wyjściowe manifestu, tylko wtedy, gdy indeksowanie wiele plików zawierających hello następujących informacji:<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Błąd</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Jeśli nie wszystkie pliki multimedialne wejściowe są indeksowane pomyślnie, zadania indeksowania hello zakończy się niepowodzeniem z kodem błędu 4000. Aby uzyskać więcej informacji, zobacz [kody błędów](#error_codes).

## <a name="index-multiple-files"></a>Indeks wielu plików
Hello następujące metody przekazywania wielu plików multimedialnych jako zasób i tworzy tooindex zadania te pliki w partii.

Plik manifestu z rozszerzeniem .lst hello został utworzony i przekazywanie do hello zawartości. Plik manifestu Hello zawiera hello listę wszystkich plików zasobów hello. Aby uzyskać więcej informacji, zobacz [dla usługi Azure Media indeksatora ustawień wstępnych zadań](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Częściowo udanej zadania
Jeśli nie wszystkie pliki multimedialne wejściowe są indeksowane pomyślnie, zadania indeksowania hello zakończy się niepowodzeniem z kodem błędu 4000. Aby uzyskać więcej informacji, zobacz [kody błędów](#error_codes).

Witaj tego samego danych wyjściowych (jako pomyślnie zadań) są generowane. Może się odwoływać toohello wyjściowego pliku manifestu toofind wychodzących, które nie są pliki wejściowe, zgodnie z toohello błąd wartości w kolumnie. Dla plików wejściowych, których nie powiodła się hello AIB wynikowy, SAMI, TTML, WebVTT i pliki — słowo kluczowe nie zostanie wygenerowany.

### <a id="preset"></a>Zadanie wstępne ustawienie indeksatora multimediów Azure
Hello przetwarzania przez indeksator multimediów Azure można dostosować, podając zadaniem opcjonalnym ustawienia wstępnego obok hello zadań.  Witaj poniżej opisano hello format tego pliku konfiguracyjnego xml.

| Nazwa | Wymagane | Opis |
| --- | --- | --- |
| **dane wejściowe** |wartość false |Pliki zasobów, które mają tooindex.</p><p>Indeksator multimediów Azure obsługuje następujące formaty plików nośnika hello: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>Można określić nazwę pliku hello (s) w hello **nazwa** lub **listy** atrybutu hello **wejściowych** elementu (jak pokazano poniżej). Jeśli nie określisz, które tooindex pliku zasobów, jest pobierany plik podstawowy hello. Jeśli plik podstawowy zasobów nie jest ustawiona, pierwszy plik zasobów wejściowych hello hello jest indeksowany.</p><p>tooexplicitly Określ nazwę pliku zasobów hello, czy:<br/>`<input name="TestFile.wmv">`<br/><br/>Można również indeksu wielu plików zasobów jednocześnie (zapasowej too10). toodo to:<br/><br/><ol class="ordered"><li><p>Utwórz plik tekstowy (plik manifestu) i nadaj mu rozszerzenie .lst. </p></li><li><p>Dodaj listę wszystkich nazw plików zasobów hello w pliku manifestu toothis zasobów wejściowych. </p></li><li><p>Dodawanie zasobów toohello pliku thanifest (przekazywanie).  </p></li><li><p>Określ nazwę hello hello pliku manifestu w atrybucie listy hello danych wejściowych.<br/>`<input list="input.lst">`</li></ol><br/><br/>Uwaga: Jeśli dodasz więcej niż 10 pliku manifestu toohello pliki hello indeksowania zadanie zakończy się niepowodzeniem z kodem błędu 2006 hello. |
| **metadane** |wartość false |Metadane dla hello określone pliki zasobów używany do dostosowania słownika.  Przydatne tooprepare indeksatora toorecognize słownictwa niestandardowych słów, takich jak nazwy własne.<br/>`<metadata key="..." value="..."/>` <br/><br/>Możesz podać **wartości** dla wstępnie zdefiniowane **klucze**. Obecnie obsługiwane są następujące klucze hello:<br/><br/>"title" i "opis" - używane dla języka hello tootweak dostosowanie słownictwa modelu dla zadania i zwiększyć dokładność rozpoznawania mowy.  wartości Hello inicjatora Internet wyszukiwania toofind kontekstowej tekst dokumentów, za pomocą słownik wewnętrzny hello tooaugment zawartość hello hello czas trwania zadania indeksowania.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **Funkcje** <br/><br/> Dodany w wersji 1.2. Hello obsługiwana tylko funkcja jest obecnie rozpoznawania mowy ("ASR"). |wartość false |Funkcja rozpoznawania mowy Hello ma hello następujące klucze ustawień:<table><tr><th><p>Klucz</p></th>        <th><p>Opis</p></th><th><p>Przykładowa wartość</p></th></tr><tr><td><p>Język</p></td><td><p>Witaj w pliku multimedialnym hello toobe języka naturalnego.</p></td><td><p>Angielski, hiszpański</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>Rozdzielana średnikami lista hello potrzeby formatów podpisu danych wyjściowych (jeśli istnieje)</p></td><td><p>ttml sami; webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Flaga wartości logicznej określenie, czy plik AIB jest wymagany (na potrzeby używania z programu SQL Server i powitania klienta IFilter indeksatora).  Aby uzyskać więcej informacji, zobacz <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">przy użyciu plików AIB z indeksatora multimediów Azure i SQL Server</a>.</p></td><td><p>Wartość PRAWDA; Wartość false</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Flaga wartości logicznej określenie, czy plik XML — słowo kluczowe jest wymagana.</p></td><td><p>Wartość PRAWDA; Wartość false. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Flaga wartości logicznej określenie, czy tooforce pełne etykiety (niezależnie od poziomu zaufania).  </p><p>Domyślna to false, w takim przypadku słów i wyrażeń, które mają mniej niż 50% ufności są pominięte wyniki końcowe podpis hello i zastępuje wielokropek ("...").  Wielokropek Hello są przydatne do kontroli jakości podpisu i inspekcji.</p></td><td><p>Wartość PRAWDA; Wartość false. </p></td></tr></table> |

### <a id="error_codes"></a>Kody błędów
W przypadku hello błąd, zgłoś Azure Media indeksatora ponownie hello następujące kody błędów:

| Kod | Nazwa | Możliwe przyczyny |
| --- | --- | --- |
| 2000 |Nieprawidłowa konfiguracja |Nieprawidłowa konfiguracja |
| 2001 |Nieprawidłowy zasobów wejściowych |Brak zasobów wejściowych lub pusty zasobów. |
| 2002 |Nieprawidłowy manifest |Manifest jest pusta lub manifestu zawiera nieprawidłowe elementy. |
| 2003 |Plik nośnika toodownload nie powiodło się |Nieprawidłowy adres URL w pliku manifestu. |
| 2004 |Nieobsługiwany protokół |Protokół adresu URL nośnika nie jest obsługiwany. |
| 2005 |Nieobsługiwany typ pliku |Typ pliku wejściowego nośnika nie jest obsługiwany. |
| 2006 |Zbyt wiele plików wejściowych |W manifeście wejściowych hello jest więcej niż 10 plików. |
| 3000 |Plik nośnika toodecode nie powiodło się |Koder-dekoder nieobsługiwany nośnik <br/>lub<br/> Uszkodzony plik <br/>lub<br/> Nie strumieniem audio na nośniku wejściowego. |
| 4000 |Indeksowanie partii częściowo powiodła się |Niektóre z hello nośników wejściowych, które pliki są nie toobe indeksowane. Aby uzyskać więcej informacji, zobacz <a href="#output_files">pliki wyjściowe</a>. |
| inne |Błędy wewnętrzne |Skontaktuj się z zespołem pomocy technicznej. indexer@microsoft.com |

## <a id="supported_languages"></a>Obsługiwane języki
Obecnie są obsługiwane hello językach angielskim i hiszpańskim. Aby uzyskać więcej informacji, zobacz [hello wersji 1.2 wpis w blogu](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[Przy użyciu plików AIB z indeksatora multimediów Azure i SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indeksowanie plików multimedialnych na pliki z podglądem indeksatora 2 multimediów Azure](media-services-process-content-with-indexer2.md)

