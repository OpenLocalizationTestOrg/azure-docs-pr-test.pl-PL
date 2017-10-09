---
title: "toohello aaaUpgrading zestawu .NET SDK w wersji 1.1 dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Uaktualnianie toohello zestawu SDK usługi Azure Search .NET w wersji 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Uaktualnianie toohello zestawu SDK usługi Azure Search .NET w wersji 3
Jeśli używasz wersji 2.0 — wersja zapoznawcza lub starszej programu hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk), ten artykuł pomoże Ci uaktualnienie wersji toouse aplikacji 3.

Aby uzyskać bardziej ogólne wskazówki hello SDK tym przykłady, zobacz [jak toouse Azure wyszukiwanie od aplikacji .NET](search-howto-dotnet-sdk.md).

Wersja 3 hello zestawu .NET SDK usługi Azure Search zawiera pewne zmiany z wcześniejszych wersji. Są to przede wszystkim niewielkie, tak więc zmiana kodu powinny wymagać tylko minimalnym wysiłku. Zobacz [tooupgrade kroki](#UpgradeSteps) instrukcje na temat toochange Twojego nowej wersji zestawu SDK kodu toouse hello.

> [!NOTE]
> Jeśli używasz wersji 1.0.2-preview lub starsze, należy najpierw uaktualnić tooversion 1.1, a następnie Uaktualnij tooversion 3. Zobacz [dodatku: kroki tooupgrade tooversion 1.1](#UpgradeStepsV1) instrukcje.
>
> Wystąpienia usługi Azure Search obsługuje kilka wersji interfejsu API REST, w tym hello najnowszy numer. Można kontynuować toouse wersji, gdy nie jest już hello najnowszego, ale zaleca się przeprowadzenie migracji kodu toouse hello najnowszej wersji. Korzystając z hello interfejsu API REST, należy określić wersję interfejsu API hello w każde żądanie za pośrednictwem parametru api-version hello. Używając hello zestawu .NET SDK, wersja hello hello używasz zestawu SDK określa hello odpowiedniej wersji hello interfejsu API REST. Jeśli używasz starszej zestawu SDK można kontynuować toorun kodu bez zmian, nawet jeśli usługa hello jest wersja uaktualniona toosupport nowszej interfejsu API.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Nowości w wersji 3
Wersja 3 hello elementów docelowych zestawu .NET SDK usługi Azure Search hello najnowszej wersji ogólnie dostępna hello interfejsu API REST wyszukiwanie Azure, w szczególności 2016-09-01. Dzięki temu możliwe toouse wiele nowych funkcji usługi Azure Search z aplikacji .NET, w tym następujące hello:

* [Analizatory niestandardowe](https://aka.ms/customanalyzers)
* [Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md) i [Azure Table Storage](search-howto-indexing-azure-tables.md) indeksatorze obsługi
* Dostosowywanie indeksatora za pośrednictwem [mapowań pól](search-indexer-field-mappings.md)
* Elementy etag obsługuje tooenable bezpieczne równoczesnych aktualizowania indeksu definicje, indeksatorów i źródeł danych
* Obsługę tworzenia indeksu definicje pól deklaratywnie dekoracji klasy modelu, a następnie użyć nowego hello `FieldBuilder` klasy.
* Obsługa platformy .NET Core i przenośnych profilu platformy .NET 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Kroki tooupgrade
Najpierw należy zaktualizować odwołania programu NuGet dla `Microsoft.Azure.Search` używając albo hello Konsola Menedżera pakietów NuGet lub przez kliknięcie prawym przyciskiem myszy odwołania projektu i wybierając pozycję "Zarządzaj NuGet pakietów..." w programie Visual Studio.

Po NuGet pobrała nowe pakiety hello oraz ich zależności, ponownie skompiluj projekt. W zależności od struktury kodu jego może odbudować pomyślnie. Jeśli tak, wszystko jest gotowe toogo!

W przypadku niepowodzenia kompilacji powinien zostać wyświetlony błąd kompilacji, takie jak następujące hello:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

Witaj, następnym krokiem jest toofix ten błąd kompilacji. Zobacz [fundamentalne zmiany w wersji 3](#ListOfChanges) szczegółowe informacje na temat co powoduje błąd hello i w jaki sposób toofix go.

Dodatkowe kompilacji może zostać wyświetlony ostrzeżenia dotyczące tooobsolete metody lub właściwości. ostrzeżenia Hello zawiera instrukcje dotyczące jakie toouse zamiast z hello przestarzałe funkcji. Na przykład, jeśli aplikacja używa hello `IndexingParameters.Base64EncodeKeys` właściwość, należy pobrać ostrzeżenie informujące,`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Gdy problem został rozwiązany błędy kompilacji, możesz wprowadzić zmiany tooyour aplikacji tootake korzystać z nowych funkcji w razie potrzeby. Nowe funkcje w hello SDK wyszczególnione w [nowości w wersji 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Fundamentalne zmiany w wersji 3
Brak niewielkiej liczby zmian podziału w wersji 3, które mogą wymagać kod zmienia dodatkowo toorebuilding aplikacji.

### <a name="indexesgetclient-return-type"></a>Zwracany typ Indexes.GetClient
Witaj `Indexes.GetClient` metoda ma nowy typ zwracany. Wcześniej, zwracana `SearchIndexClient`, ale ta zmiana została wprowadzona zbyt`ISearchIndexClient` w wersji 2.0-preview, a zmiany są przenoszone tooversion 3. Jest to toosupport klientów, którzy mają toomock hello `GetClient` metodę dla testów jednostkowych przez zwrócenie implementację testową z `ISearchIndexClient`.

#### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Można zmienić toothis toofix wszelkie błędy kompilacji:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, typ danych i inne osoby nie są już toostrings umożliwiają niejawnej konwersji
Istnieje wiele typów w hello Azure Search .NET SDK, który pochodzi z `ExtensibleEnum`. Wcześniej te typy zostały wszystkie niejawnego tootype `string`. Jednak usterki zostało odnalezione hello `Object.Equals` implementacji dla tych klas i ustalające usterki hello wymagane wyłączenie niejawnej konwersji. Jawna konwersja zbyt`string` jest nadal dozwolone.

#### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Można zmienić toothis toofix wszelkie błędy kompilacji:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Usunięte przestarzali członkowie

Może pojawić się właściwości, które zostały oznaczone jako przestarzałe w wersji 2.0-preview, a później usunięte w wersji 3 lub toomethods powiązane błędy kompilacji. Jeśli wystąpią błędy takie, Oto jak tooresolve je:

- W przypadku używania tego konstruktora: `ScoringParameter(string name, string value)`, zamiast tego użyj tego:`ScoringParameter(string name, IEnumerable<string> values)`
- W przypadku używania hello `ScoringParameter.Value` właściwość, użyj hello `ScoringParameter.Values` właściwości lub hello `ToString` metody zamiast tego.
- W przypadku używania hello `SearchRequestOptions.RequestId` właściwość, użyj hello `ClientRequestId` właściwości zamiast tego.

### <a name="removed-preview-features"></a>Funkcje usunięte w wersji zapoznawczej

Jeśli uaktualniasz tooversion Podgląd 2.0 w wersji 3 należy pamiętać, że JSON i analizowania pomocy technicznej dla obiekt Blob indeksatorów CSV została usunięta, ponieważ te funkcje są nadal w wersji zapoznawczej. W szczególności hello następujące metody hello `IndexingParametersExtensions` klasy zostały usunięte:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Jeśli aplikacja ma twardych zależność od tych funkcji, nie będzie możliwe tooupgrade tooversion 3 z hello zestawu .NET SDK usługi Azure Search. Można kontynuować toouse wersji 2.0-preview. Jednak należy należy pamiętać, że **zaleca się używania Podgląd zestawów SDK w aplikacji produkcyjnych**. Funkcje w wersji zapoznawczej są tylko do oceny i może ulec zmianie.

## <a name="conclusion"></a>Podsumowanie
Aby uzyskać więcej informacji na temat używania hello zestawu .NET SDK usługi Azure Search, zobacz nasze niedawno zaktualizowanego [porad](search-howto-dotnet-sdk.md).

Chętnie poznamy Twoją opinię na powitania zestawu SDK. Jeśli wystąpią problemy, możesz wolnego tooask nam Aby uzyskać pomoc dotyczącą hello [forum usługi Azure Search w witrynie MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Jeśli napotkasz błąd, możesz pliku problemu w hello [repozytorium GitHub zestawu SDK .NET usługi Azure](https://github.com/Azure/azure-sdk-for-net/issues). Upewnij się, że tooprefix tytuł problemu z "wyszukiwania zestawu SDK:".

Dziękujemy za skorzystanie z usługi Azure Search!

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Dodatek: Kroki tooupgrade tooversion 1.1
> [!NOTE]
> Ta sekcja dotyczy tylko toousers 1.0.2-preview wersji zestawu .NET SDK usługi Azure Search hello i starszych.
> 
> 

Najpierw należy zaktualizować odwołania programu NuGet dla `Microsoft.Azure.Search` używając albo hello Konsola Menedżera pakietów NuGet lub przez kliknięcie prawym przyciskiem myszy odwołania projektu i wybierając pozycję "Zarządzaj NuGet pakietów..." w programie Visual Studio.

Po NuGet pobrała nowe pakiety hello oraz ich zależności, ponownie skompiluj projekt.

Jeśli wcześniej przy użyciu wersji 1.0.0-preview, 1.0.1-preview lub 1.0.2-preview, hello ma być pomyślnie wykonane i wszystko jest gotowe toogo!

Jeśli zostały wcześniej przy użyciu wersji 0.13.0-preview lub starsze, powinny pojawić się błędy, takie jak następujące hello kompilacji:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

Witaj następnym krokiem jest błędy kompilacji hello toofix jeden po drugim. Większość wymaga zmiana niektóre nazwy klasy i metody, których nazwy zostały zmienione w hello zestawu SDK. [Lista fundamentalne zmiany w wersji 1.1](#ListOfChangesV1) zawiera listę tych zmian nazw.

Jeśli używasz niestandardowej klasy toomodel dokumentów, a te klasy mają właściwości typów pierwotnych wartości null (na przykład `int` lub `bool` w języku C#), jest w wersji hello 1.1 hello zestawu SDK, które należy zwrócić uwagę poprawkę. Zobacz [poprawki błędów w wersji 1.1](#BugFixesV1) więcej szczegółów.

Ponadto po problem został rozwiązany błędy kompilacji, możesz wprowadzić zmiany tooyour aplikacji tootake korzystać z nowych funkcji w razie potrzeby.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Lista fundamentalne zmiany w wersji 1.1
Witaj poniżej jest określona przez prawdopodobieństwo hello czy hello zmiany będzie miało wpływ na kod aplikacji.

#### <a name="indexbatch-and-indexaction-changes"></a>IndexBatch i IndexAction zmian
`IndexBatch.Create`Zmieniono zbyt`IndexBatch.New` i nie ma już `params` argumentu. Można użyć `IndexBatch.New` partii, które mieszać różnego rodzaju akcje (scalenia, usuwa itp.). Ponadto istnieją nowe metody statyczne do tworzenia instancji gdzie wszystkie akcje hello są takie same hello: `Delete`, `Merge`, `MergeOrUpload`, i `Upload`.

`IndexAction`nie ma konstruktorów publicznych i jego właściwości są niezmienne. Należy użyć nowych metod statycznych hello tworzenia akcje do różnych celów: `Delete`, `Merge`, `MergeOrUpload`, i `Upload`. `IndexAction.Create`została usunięta. Jeśli używane jest przeciążenie hello, który przyjmuje tylko dokumenty, upewnij się, że toouse `Upload` zamiast tego.

##### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Można zmienić toothis toofix wszelkie błędy kompilacji:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Jeśli chcesz, możesz dodatkowo upraszcza go toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>IndexBatchException zmiany
Witaj `IndexBatchException.IndexResponse` właściwości została zmieniona za`IndexingResults`, a jej typ jest teraz `IList<IndexingResult>`.

##### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Można zmienić toothis toofix wszelkie błędy kompilacji:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Operacja zmiany — metoda
Każdej operacji w hello zestawu .NET SDK usługi Azure Search jest ujawniona jako zbiór przeciążenia metody dla wywoływania synchroniczne i asynchroniczne. Witaj podpisów i factoring z tych przeciążenia metody została zmieniona w wersji 1.1.

Na przykład Witaj "Uzyskać statystyki indeksu" operacji w starszych wersjach hello SDK widoczne te podpisy:

W `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

W `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

Sygnatury metody Hello hello tej samej operacji w wersji 1.1 wyglądać następująco:

W `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

W `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Począwszy od wersji 1.1, hello zestawu .NET SDK usługi Azure Search porządkuje metody operacji inaczej:

* Parametry opcjonalne są teraz modelowane jako domyślne parametry raczej niż przeciążenia metody dodatkowe. Czasami znacznie zmniejsza liczbę hello przeciążenia metody.
* metody rozszerzenia Hello Ukryj teraz dużo hello nadmiarowe szczegóły HTTP z hello wywołującego. Na przykład starsze wersje zestawu SDK zwrócił obiekt odpowiedzi z kodem stanu HTTP, która będzie często hello nie potrzebuję toocheck, ponieważ throw metody operacji `CloudException` dla dowolnego kodu stanu wskazujący błąd. Witaj nowe obiekty modelu Zwróć metody rozszerzenia, zapisywanie możesz hello problemy o toounwrap je w kodzie.
* Z drugiej strony hello podstawowych interfejsów teraz ujawniać metod, które zapewniają większą kontrolę na poziomie hello HTTP, jeśli zajdzie taka potrzeba. Teraz można przekazać niestandardowe toobe nagłówki HTTP dołączone do żądania i hello nowe `AzureOperationResponse<T>` zwracany typ zapewnia bezpośredni dostęp do toohello `HttpRequestMessage` i `HttpResponseMessage` hello operacji. `AzureOperationResponse`jest zdefiniowany w hello `Microsoft.Rest.Azure` przestrzeni nazw i zastępuje `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>ScoringParameters zmiany
Nową klasę o nazwie `ScoringParameter` zostało dodane w najnowszej toomake SDK hello łatwiejsze profile tooscoring tooprovide parametrów w zapytaniu wyszukiwania. Wcześniej hello `ScoringProfiles` właściwości hello `SearchParameters` klasy została wpisana jako `IList<string>`; Teraz jest wpisana jako `IList<ScoringParameter>`.

##### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Można zmienić toothis toofix wszelkie błędy kompilacji: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Zmiany modelu klasy
Powodu toohello podpisu zmian opisanych w [operację zmiany metody](#OperationMethodChanges), wiele klas w hello `Microsoft.Azure.Search.Models` przestrzeni nazw został przeniesiony lub usunięty. Na przykład:

* `IndexDefinitionResponse`został zastąpiony`AzureOperationResponse<Index>`
* `DocumentSearchResponse`Zmieniono zbyt`DocumentSearchResult`
* `IndexResult`Zmieniono zbyt`IndexingResult`
* `Documents.Count()`obecnie zwraca `long` o liczbie dokumentów hello zamiast`DocumentCountResponse`
* `IndexGetStatisticsResponse`Zmieniono zbyt`IndexGetStatisticsResult`
* `IndexListResponse`Zmieniono zbyt`IndexListResult`

toosummarize, `OperationResponse`-pochodzi z klasy, które były dostępne tylko toowrap obiekt modelu zostały usunięte. Witaj pozostałych klasy miały ich sufiks zmieniła się z `Response` zbyt`Result`.

##### <a name="example"></a>Przykład
Jeśli kod wygląda następująco:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Można zmienić toothis toofix wszelkie błędy kompilacji:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Klasy odpowiedzi i IEnumerable
Dodatkowe zmiany, które mogą mieć wpływ na kod jest klasy odpowiedzi, zawierających kolekcje nie implementuje `IEnumerable<T>`. Zamiast tego można bezpośredni dostęp hello właściwości kolekcji. Na przykład, jeśli kod wygląda następująco:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Można zmienić toothis toofix wszelkie błędy kompilacji:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Szczególnych przypadkach dla aplikacji sieci web
Jeśli masz aplikację sieci web, który serializuje `DocumentSearchResponse` bezpośrednio w przeglądarce toohello wyniki wyszukiwania toosend, konieczne będzie toochange kodu lub hello wyniki nie zostaną poprawnie serializować. Na przykład, jeśli kod wygląda następująco:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Można ją zmienić, pobierając hello `.Results` właściwości hello wyszukiwania odpowiedzi toofix wyszukiwania wynik renderowania:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Konieczne będzie toolook w takich przypadkach w kodzie **hello kompilatora nie ostrzega** ponieważ `JsonResult.Data` jest typu `object`.

#### <a name="cloudexception-changes"></a>CloudException zmiany
Witaj `CloudException` klasy została przeniesiona z hello `Hyak.Common` toohello przestrzeni nazw `Microsoft.Rest.Azure` przestrzeni nazw. Ponadto jego `Error` zbyt zmieniono właściwość`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Zmiany SearchServiceClient i SearchIndexClient
Witaj typu hello `Credentials` właściwość zostanie zmieniona z `SearchCredentials` tooits podstawowa klasa `ServiceClientCredentials`. Jeśli potrzebujesz tooaccess hello `SearchCredentials` z `SearchIndexClient` lub `SearchServiceClient`, użyj nowego hello `SearchCredentials` właściwości.

W starszych wersjach hello zestawu SDK `SearchServiceClient` i `SearchIndexClient` ma konstruktorów, które miały `HttpClient` parametru. Te zostały zastąpione konstruktorów przyjmujących `HttpClientHandler` i tablica `DelegatingHandler` obiektów. Dzięki temu można łatwiej tooinstall niestandardowe programy obsługi procesu toopre żądań HTTP w razie potrzeby.

Na koniec hello konstruktorów, które miały `Uri` i `SearchCredentials` zostały zmienione. Na przykład, jeśli kod, który wygląda następująco:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Można zmienić toothis toofix wszelkie błędy kompilacji:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Ponadto należy pamiętać, że typ hello hello poświadczenia parametru został zmieniony zbyt`ServiceClientCredentials`. Jest to prawdopodobnie nie tooaffect kodu od `SearchCredentials` jest pochodną `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Przekazywanie identyfikator żądania
Identyfikator żądania w starszych wersjach hello zestawu SDK, można ustawić na powitania `SearchServiceClient` lub `SearchIndexClient` i może być uwzględniony w każdym toohello żądania interfejsu API REST. Jest to przydatne podczas rozwiązywania problemów z usługą wyszukiwania, jeśli potrzebujesz pomocy technicznej toocontact. Jednak jest bardziej użyteczne tooset Unikatowy identyfikator dla każdej operacji zamiast toouse hello tym samym identyfikatorze dla wszystkich operacji. Z tego powodu hello `SetClientRequestId` metody `SearchServiceClient` i `SearchIndexClient` zostały usunięte. Zamiast tego można przekazać metodę operacji tooeach identyfikator żądania za pośrednictwem hello opcjonalne `SearchRequestOptions` parametru.

> [!NOTE]
> W przyszłym wydaniu hello zestawu SDK zostanie dodany nowy mechanizm do ustawiania Identyfikatora żądania globalnie na powitania klienta obiektów zgodny z podejścia hello używane przez innych zestawów SDK usługi Azure.
> 
> 

#### <a name="example"></a>Przykład
Jeśli masz kod, który wygląda następująco:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Można zmienić toothis toofix wszelkie błędy kompilacji:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Zmiany nazwy interfejsu
nazwy interfejsu grup operacja Hello są wszystkie zmienione toobe zgodne z odpowiadającymi im nazwami właściwości:

* Witaj typu `ISearchServiceClient.Indexes` została zmieniona z `IIndexOperations` zbyt`IIndexesOperations`.
* Witaj typu `ISearchServiceClient.Indexers` została zmieniona z `IIndexerOperations` zbyt`IIndexersOperations`.
* Witaj typu `ISearchServiceClient.DataSources` została zmieniona z `IDataSourceOperations` zbyt`IDataSourcesOperations`.
* Witaj typu `ISearchIndexClient.Documents` została zmieniona z `IDocumentOperations` zbyt`IDocumentsOperations`.

Ta zmiana jest kod tooaffect mało prawdopodobne, chyba że zostaną utworzone mocks te interfejsy do celów testowych.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Poprawki błędów w wersji 1.1
Wystąpił błąd w starszych wersjach tooserialization dotyczące zestawu .NET SDK usługi Azure Search hello klas niestandardowych modelu. Hello błąd mógł wystąpić, jeśli klasę modelu niestandardowe zostały utworzone z właściwością typu niedopuszczające wartości.

#### <a name="steps-tooreproduce"></a>Kroki tooreproduce
Utwórz klasę modelu niestandardowych z właściwością typ niedopuszczający wartości null. Na przykład, Dodaj publiczną `UnitCount` właściwości typu `int` zamiast `int?`.

Jeśli indeks dokument z wartością domyślną hello tego typu (na przykład 0 dla `int`), pole hello będzie mieć wartość null w usłudze Azure Search. Następnie wyszukiwania dla tego dokumentu, hello `Search` zgłosi wywołania `JsonSerializationException` strona skarżąca, który nie może przekonwertować `null` zbyt`int`.

Ponadto filtry mogą nie działać zgodnie z oczekiwaniami, ponieważ wartość null została napisana indeksu toohello zamiast wartości hello przeznaczone.

#### <a name="fix-details"></a>Usuń szczegóły
Ten problem został rozwiązany w wersji 1.1 hello zestawu SDK. Teraz, jeśli masz klasę modelu w następujący sposób:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

i `IntValue` too0, czy wartość jest teraz prawidłowo zserializowanej 0 umieszczonego hello i przechowywane jako 0 hello indeksu. Również uruchomienie round działa zgodnie z oczekiwaniami.

Jest świadome tego podejścia przy rozwiązywaniu jednego toobe potencjalny problem: Jeśli używasz typu modelu z właściwością wartości null, jest zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello. Hello zestawu SDK ani hello API REST usługi Azure Search nie pomoże tooenforce można to.

To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `Edm.Int32`. Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search). Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Z tego powodu Będziemy nadal zaleca się używanie typów dopuszczających wartości zerowe w klasach modeli najlepszym rozwiązaniem.

Aby uzyskać więcej szczegółów na tej poprawki błędów i hello, zobacz [ten problem w usłudze GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

