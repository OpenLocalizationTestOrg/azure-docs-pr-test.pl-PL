---
title: "aaaIndexing magazynu obiektów Blob Azure z usługi Azure Search"
description: "Dowiedz się, jak tooindex obiektów Blob platformy Azure magazynu i Wyodrębnij tekst z dokumentów z usługi Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Indeksowanie dokumentów w magazynie obiektów Blob Azure o usłudze Azure Search
W tym artykule przedstawiono sposób toouse usługi Azure Search tooindex dokumentów (takich jak PDF, dokumentów Microsoft Office i kilka innych typowych formatach) przechowywanych w magazynie obiektów Blob platformy Azure. Najpierw wyjaśniono podstawy hello instalowania i konfigurowania indeksatora obiektu blob. Następnie zapewnia lepszą eksploracji zachowania i scenariusze są prawdopodobnie tooencounter.

## <a name="supported-document-formats"></a>Obsługiwane formaty dokumentu
indeksator blob Hello można wyodrębnić tekst z następujące formaty dokumentu hello:

* PLIK PDF
* Microsoft Office formaty: DOCX/DOC, XLSX/XLS, PPTX/PPT MSG (wiadomości e-mail programu Outlook)  
* HTML
* XML
* ZIP
* EML
* RTF
* Pliki w formacie zwykłego tekstu (Zobacz też [Indeksowanie Zwykły tekst](#IndexingPlainText))
* JSON (zobacz [obiektów blob JSON indeksowania](search-howto-index-json-blobs.md))
* CSV (zobacz [CSV indeksowanie obiektów blob](search-howto-index-csv-blobs.md) funkcja w wersji zapoznawczej)

> [!IMPORTANT]
> Obsługa tablice CSV i JSON jest obecnie w wersji zapoznawczej. Te formaty są dostępne wyłącznie przy użyciu wersji **2016-09-01-Preview** z hello interfejsu API REST lub wersja preview 2.x hello zestawu .NET SDK. Należy pamiętać, Podgląd interfejsy API są przeznaczone do testowania i ocenie, a nie powinna być używana w środowisku produkcyjnym.
>
>

## <a name="setting-up-blob-indexing"></a>Konfigurowanie indeksowanie obiektów blob
Można skonfigurować indeksator usługi Azure Blob Storage za pomocą:

* [Witryna Azure Portal](https://ms.portal.azure.com)
* Usługa Azure Search [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Usługa Azure Search [zestawu .NET SDK](https://aka.ms/search-sdk)

> [!NOTE]
> Niektóre funkcje (na przykład mapowania pola) nie są jeszcze dostępne w portalu hello i mieć toobe używana programowo.
>
>

W tym miejscu przedstawiony przepływu hello przy użyciu hello interfejsu API REST.

### <a name="step-1-create-a-data-source"></a>Krok 1: Tworzenie źródła danych
Źródło danych określa, które tooindex danych, poświadczenia potrzebne tooaccess hello danych i zasady tooefficiently zidentyfikować zmiany danych hello (nowych, zmodyfikowanych lub usuniętych wierszy). Źródło danych może być używane przez wiele indeksatorów w hello same usługi wyszukiwania.

W przypadku indeksowanie obiektów blob, hello źródło danych musi mieć hello następujących wymaganych właściwości:

* **Nazwa** jest unikatowa nazwa hello hello źródła danych w ramach usługi wyszukiwania.
* **Typ** musi być `azureblob`.
* **poświadczenia** zawiera parametry połączenia konta magazynu hello jako hello `credentials.connectionString` parametru. Zobacz [jak poświadczenia toospecify](#Credentials) poniżej szczegółowe informacje.
* **kontener** Określa kontener na koncie magazynu. Domyślnie wszystkie obiekty BLOB w kontenerze hello są pobieranie. Jeśli chcesz tylko obiekty BLOB tooindex z określonego katalogu wirtualnego, można określić tego katalogu przy użyciu hello opcjonalne **zapytania** parametru.

toocreate źródła danych:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Aby uzyskać więcej informacji na temat hello Utwórz źródło danych interfejsu API, zobacz [utworzyć źródło danych](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Jak toospecify poświadczeń ####

Można podać poświadczenia hello hello kontenera obiektów blob w jeden z następujących sposobów:

- **Parametry połączenia konta magazynu pełny dostęp**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Parametry połączenia hello możesz pobrać ze strony hello portalu Azure, przechodząc bloku konto magazynu toohello > Ustawienia > klucze (dla kont magazynu Classic) lub Ustawienia > uzyskać dostęp do kluczy (dla kont magazynu usługi Azure Resource Manager).
- **Sygnatury dostępu współdzielonego konta magazynu** ciąg połączenia (SAS): `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS powinny mieć hello listę i uprawnienia do odczytu z kontenerów i obiektów (obiekty BLOB w tym przypadku).
-  **Sygnatury dostępu współdzielonego kontenera**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS powinny mieć hello listę i uprawnienia do odczytu z hello kontenera.

Aby uzyskać więcej informacji w magazynie udostępnionym sygnatur dostępu, zobacz [za pomocą sygnatur dostępu udostępnionego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Korzystając z poświadczeń sygnatury dostępu Współdzielonego, konieczne będzie poświadczenia źródła danych hello tooupdate okresowo z tooprevent odnowionego podpisów ich wygaśnięciem. Po wygaśnięciu poświadczeń sygnatury dostępu Współdzielonego, indeksatora hello niepowodzenie komunikat o błędzie podobny zbyt`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Krok 2: Tworzenie indeksu
Indeks Hello określa hello pola w dokumencie atrybuty, oraz innych konstrukcji środowiska wyszukiwania hello kształtu.

Oto jak toocreate indeks z możliwością wyszukiwania `content` pole tekstowe hello toostore wyodrębniony z obiektów blob:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Aby uzyskać więcej informacji na temat Tworzenie indeksów, zobacz [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>Krok 3: Utwórz indeksator
Indeksator łączy źródła danych z indeksem wyszukiwania docelowego, a zawiera harmonogram tooautomate hello odświeżania.

Po utworzeniu hello indeks i źródło danych jest gotowy toocreate hello indeksatora:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Ten indeksator będzie uruchamiany co dwie godziny (interwał harmonogramu jest ustawiona zbyt "PT2H"). toorun indeksatora co 30 minut, ustawić interwał powitania także "PT30M". Witaj najkrótszy obsługiwany interwał wynosi 5 minut. Hello harmonogram jest opcjonalny — w przypadku jego pominięcia, indeksatora działa tylko wtedy, gdy po utworzeniu. Jednak w dowolnym momencie można uruchomić indeksatora na żądanie.   

Aby uzyskać więcej informacji na temat hello Tworzenie interfejsu API indeksatora, zapoznaj się z [Utwórz indeksator](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Jak usługa Azure Search indeksy obiektów blob

W zależności od hello [konfiguracji indeksatora](#PartsOfBlobToIndex), hello indeksatora obiektu blob może indeksować tylko metadane magazynu (przydatne, gdy tylko najważniejsze informacje hello metadanych i nie wymagają tooindex hello zawartości obiektów blob), magazynu i zawartości metadanych i/lub metadane i zawartość tekstową. Domyślnie indeksatora hello wyodrębnia metadane i zawartość.

> [!NOTE]
> Domyślnie obiekty BLOB z zawartością strukturalnych, takich jak JSON lub CSV są indeksowane jako pojedynczy fragmentów tekstu. Jeśli obiekty BLOB JSON i CSV tooindex struktury, zobacz [obiektów blob JSON indeksowania](search-howto-index-json-blobs.md) i [CSV indeksowanie obiektów blob](search-howto-index-csv-blobs.md) funkcji w wersji zapoznawczej.
>
> Osadzone lub złożonego dokumentu (na przykład archiwum ZIP lub dokument programu Word z osadzonym e-mail programu Outlook zawierające załączniki) są również indeksowane jako pojedynczego dokumentu.

* zawartość tekstową Hello dokumentu hello jest wyodrębniany do pola ciągu o nazwie `content`.

> [!NOTE]
> Usługa wyszukiwanie Azure ogranicza ilość tekstu wyodrębniane w zależności od warstwy cenowej hello: 32 000 znaków za darmo w warstwie, 64 000 Basic i 4 milionów do warstwy standardowa, standardowe S2 i standardowa S3. Ostrzeżenie jest dołączany hello indeksatora stanu odpowiedzi dla dokumentów obcięte.  

* Właściwości określone przez użytkownika metadanych dla obiektu blob hello, jeśli są wyodrębniane verbatim.
* Standardowa obiektów blob metadane właściwości są wyodrębniane do hello następujące pola:

  * **metadane\_magazynu\_nazwa** (typem Edm.String) — Nazwa pliku hello hello obiektu blob. Na przykład, jeśli masz /my-container/my-folder/subfolder/resume.pdf obiektów blob hello wartość tego pola jest `resume.pdf`.
  * **metadane\_magazynu\_ścieżki** (typem Edm.String) — Witaj pełny identyfikator URI obiektu blob hello, w tym hello konta magazynu. Na przykład: `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **metadane\_magazynu\_zawartości\_typu** (typem Edm.String) — typ zawartości, określone przez kod hello używane tooupload hello blob. Na przykład `application/octet-stream`.
  * **metadane\_magazynu\_ostatniego\_zmodyfikować** (Edm.DateTimeOffset) - Ostatnia modyfikacja sygnatury czasowej hello obiektu blob. Usługa Azure Search korzysta z tego sygnatury czasowej tooidentify zmienione obiekty BLOB, tooavoid indeksowanie wszystko po początkowej indeksowania hello.
  * **metadane\_magazynu\_rozmiar** (Edm.Int64) - wyrażony w bajtach rozmiar obiektu blob.
  * **metadane\_magazynu\_zawartości\_md5** (typem Edm.String) - skrótu MD5 hello zawartości obiektu blob, jeśli jest dostępna.
* Format dokumentu tooeach określonych właściwości metadanych są wyodrębniane do pól hello wymienionych [tutaj](#ContentSpecificMetadata).

Nie ma potrzeby toodefine pól dla wszystkich hello powyżej właściwości w indeksie wyszukiwania — tylko przechwytywania właściwości hello, potrzebnych aplikacji.

> [!NOTE]
> Często hello nazwy pól w indeksie istniejących będzie się różnił od nazw pól hello generowane podczas wyodrębniania dokumentu. Można użyć **mapowań pól** nazwy właściwości hello toomap udostępniane przez usługi Azure Search nazwy pól toohello w indeksie wyszukiwania. Przykład pola używanego mapowania poniżej zostanie wyświetlone.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Definiowanie kluczy dokumentu i mapowania pól
W usłudze Azure Search klucz dokumentu hello unikatowo identyfikuje dokumentu. Każdy indeks musi mieć dokładnie jedno pole klucza typu typem Edm.String. pole klucza Hello jest wymagane dla każdego dokumentu, który jest dodawany indeksu toohello (jest rzeczywiście hello tylko pole wymagane).  

Należy rozważyć wyodrębnionego pole, które powinny być mapowane toohello pola klucza indeksu. Kandydaci Hello:

* **metadane\_magazynu\_nazwa** — to może być wygodną kandydata, ale należy pamiętać, że nazwy hello 1) nie muszą być unikatowe, jak mogą mieć obiektów blob z hello takie same nazwy w różnych folderach i 2) hello nazwa może zawierać znaków który są nieprawidłowe w dokumencie kluczy, takich jak łączniki. Za pomocą hello mogą dotyczyć nieprawidłowe znaki `base64Encode` [funkcja mapowania pól](search-indexer-field-mappings.md#base64EncodeFunction) — Jeśli to zrobisz, podczas przekazując interfejsu API wywołuje takie jak wyszukiwanie, należy pamiętać tooencode dokumentu kluczy. (Na przykład, .NET można hello [metody UrlTokenEncode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) w tym celu).
* **metadane\_magazynu\_ścieżki** — przy użyciu pełnej ścieżki hello zapewnia unikatowość, ale ostatecznie zawiera ścieżkę hello `/` znaki, które są [nieprawidłowe w kluczu dokumentu](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Jak powyżej, jest dostępna opcja hello kodowanie kluczy hello przy użyciu hello `base64Encode` [funkcja](search-indexer-field-mappings.md#base64EncodeFunction).
* Jeśli żaden z powyższych opcji hello działa, możesz dodać obiekty BLOB toohello właściwości niestandardowych metadanych. Ta opcja jednak wymaga tooadd procesu przekazywania z obiektu blob obiekty BLOB tooall tego metadane właściwości. Ponieważ klucz hello jest wymagana właściwość, wszystkie obiekty BLOB, które nie mają tej właściwości nie powiedzie się toobe indeksowane.

> [!IMPORTANT]
> Jeśli nie ma jawnego mapowania hello pola klucza w indeksie hello, usługi Azure Search automatycznie używa `metadata_storage_path` jako wartości kluczy (hello druga opcja powyżej) koduje hello klucza i base-64.
>
>

Na przykład umożliwia pobranie hello `metadata_storage_name` pole jako klucz dokumentu hello. Załóżmy również, że indeks ma pole klucza o nazwie `key` i pole `fileSize` do przechowywania hello rozmiar dokumentu. elementy toowire się zgodnie z potrzebami, określ następujące mapowania pól, podczas tworzenia lub aktualizowania indeksator hello:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring to wszystko w jednym, Oto jak można dodać mapowania pól i Włącz kodowanie base-64 kluczy dla istniejącego indeksatora:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn więcej informacji na temat mapowania pól, zobacz [w tym artykule](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Kontrolowanie, które obiekty BLOB są indeksowane.
Można kontrolować, które obiekty BLOB są indeksowane i które są pomijane.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Indeksuj tylko hello blob z określonych rozszerzeń plików
Może indeksować tylko hello obiekty BLOB z rozszerzeniami nazwy pliku hello przy użyciu hello `indexedFileNameExtensions` parametru konfiguracji indeksatora. wartość Hello jest ciąg zawierający rozdzielaną przecinkami listę rozszerzeń nazw plików (z początku kropką). Na przykład tooindex tylko hello. PDF i. Obiekty BLOB DOCX, wykonaj następujące czynności:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Wyklucz obiekty BLOB z określonych rozszerzeń plików
Obiekty BLOB z określonych rozszerzeń nazw plików można wykluczyć z indeksowania przy użyciu hello `excludedFileNameExtensions` parametru konfiguracji. wartość Hello jest ciąg zawierający rozdzielaną przecinkami listę rozszerzeń nazw plików (z początku kropką). Na przykład tooindex wszystkie obiekty BLOB z wyjątkiem tych z hello. PNG, a. Rozszerzenia JPEG, wykonaj następujące czynności:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Jeśli oba `indexedFileNameExtensions` i `excludedFileNameExtensions` parametrów, usługi Azure Search najpierw sprawdza `indexedFileNameExtensions`, następnie w `excludedFileNameExtensions`. Oznacza to, że jeśli hello samo rozszerzenie pliku znajduje się w obu list, zostanie on wykluczony z indeksowania.

### <a name="dealing-with-unsupported-content-types"></a>Zajmujących się nieobsługiwane typy zawartości

Domyślnie program hello blob indeksatora zatrzymuje zaraz po napotkaniu obiektu blob o nieobsługiwanym typie zawartości (na przykład obraz). Oczywiście można użyć hello `excludedFileNameExtensions` parametru tooskip niektórych typów zawartości. Jednak może być konieczne obiekty BLOB tooindex bez wiedzy o wszystkich hello możliwych typów zawartości z wyprzedzeniem. toocontinue indeksowania po napotkaniu nieobsługiwany typ zawartości, ustaw hello `failOnUnsupportedContentType` parametru konfiguracji zbyt`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Ignorowanie błędy analizy

Azure logiki wyodrębniania dokumentu wyszukiwania nie jest doskonała i czasami nie powiedzie się dokumenty tooparse obsługiwanego typu zawartości, takich jak. DOCX lub. PDF. Jeśli nie chcesz, aby hello toointerrupt indeksowania w takich przypadkach, ustaw hello `maxFailedItems` i `maxFailedItemsPerBatch` rozsądne wartości toosome parametry konfiguracji. Na przykład:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Kontrolowanie, które części obiektu blob hello są indeksowane

Można kontrolować, które części hello obiekty BLOB są indeksowane przy użyciu hello `dataToExtract` parametru konfiguracji. Może upłynąć hello następujące wartości:

* `storageMetadata`— Określa, że tylko hello [właściwości standardowych obiektów blob i metadanych określonych przez użytkownika](../storage/blobs/storage-properties-metadata.md) są indeksowane.
* `allMetadata`— Określa, że metadane magazynu i hello [metadane specyficzne dla typu zawartości](#ContentSpecificMetadata) wyodrębniony z obiektu blob hello są indeksowane zawartości.
* `contentAndMetadata`-Określa wszystkie metadane i zawartość tekstową wyodrębniony z obiektu blob hello są indeksowane. Jest to wartość domyślna hello.

Na przykład tooindex tylko hello magazynu metadanych, należy użyć:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Przy użyciu jak obiekty BLOB są indeksowane toocontrol metadane obiektu blob

opisane powyżej parametry konfiguracji Hello zastosować tooall obiektów blob. Czasami, jak można toocontrol *poszczególne obiekty BLOB* są indeksowane. Można to zrobić, dodając następujące hello obiektów blob metadane właściwości i wartości:

| Nazwa właściwości | Wartość właściwości | Wyjaśnienie |
| --- | --- | --- |
| AzureSearch_Skip |wartość "prawda" |Powoduje, że blob hello indeksatora Pomiń toocompletely hello obiektu blob. Nastąpiła wyodrębniania metadanych ani zawartości. Jest to przydatne, gdy konkretnego obiektu blob nie powiedzie się wielokrotnie i przerywa proces indeksowania hello. |
| AzureSearch_SkipContent |wartość "prawda" |Jest to równoważne z `"dataToExtract" : "allMetadata"` ustawienia opisane [powyżej](#PartsOfBlobToIndex) tooa zakresie konkretnego obiektu blob. |

## <a name="incremental-indexing-and-deletion-detection"></a>Przyrostowe wykrywania indeksowanie i usuwaniem.
Po skonfigurowaniu toorun indeksatora obiektów blob, zgodnie z harmonogramem jego ponowna indeksacja tylko hello zmienionych obiektów blob, zgodnie z ustaleniami hello blob `LastModified` sygnatury czasowej.

> [!NOTE]
> Nie masz toospecify zasady wykrywania zmian — przyrostowe indeksowania jest włączona automatycznie.

Trwa usuwanie dokumentów toosupport, użyj podejście "usuwania nietrwałego". Po usunięciu obiektów blob hello ostatecznego odpowiednie dokumenty nie zostaną usunięte z indeksu wyszukiwania hello. Zamiast tego należy użyć hello następujące kroki:  

1. Dodawanie niestandardowych metadanych właściwości toohello obiektu blob tooindicate tooAzure wyszukiwania logicznie usunięty
2. Skonfiguruj zasady usuwania nietrwałego wykrywania na powitania źródła danych
3. Po przetworzeniu indeksatora hello blob hello (jak to przedstawiono stan indeksatora hello interfejsu API) fizycznie można usunąć obiektu blob hello

Na przykład następujące zasady hello uwzględnia toobe obiektów blob, usunąć, jeśli ma ona właściwości metadanych `IsDeleted` z wartością hello `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indeksowanie dużych zestawów danych

Indeksowanie obiektów blob może być czasochłonne. W przypadkach, gdy mają miliony tooindex obiektów blob można przyspieszyć indeksowania partycjonowanie danych i używając wiele indeksatorów tooprocess hello danych równolegle. Oto, jak należy wybrać tę opcję:

- Dzielenia danych na wielu kontenerów obiektów blob lub foldery wirtualne
- Skonfiguruj kilka źródeł danych usługi Azure Search, po jednym dla każdego kontenera lub folderu. folder obiektu blob tooa toopoint, użyj hello `query` parametru:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Tworzenie odpowiedniego indeksatora dla każdego źródła danych. Wszystkie hello indeksatory mogą punktu toohello tego samego indeksu wyszukiwania docelowego.  

- Jednostki wyszukiwania w usłudze można uruchomić jeden indeksator w danym momencie. Tworzenie wiele indeksatorów, zgodnie z powyższym opisem tylko jest przydatne, jeśli są one uruchamiane równolegle. toorun wiele indeksatorów równolegle, skalowanie usługi wyszukiwania przez utworzenie odpowiedniej liczby partycji i replik. Na przykład jeśli usługi wyszukiwania 6 jednostek wyszukiwania (na przykład 2 partycjach x 3 repliki), następnie 6 indeksatory może działać jednocześnie, co six-fold wzrost hello przepływność indeksowania. toolearn więcej informacji na temat skalowania i planowania pojemności, zobacz [skalować poziomy zasobów dla zapytania i obciążeń w usłudze Azure Search indeksowanie](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indeksowanie dokumentów oraz powiązane dane

Może być zbyt "złóż" dokumenty z wielu źródeł w indeksie. Na przykład można toomerge tekst z obiektów blob z inne metadane przechowywane w bazie danych rozwiązania Cosmos. Można nawet hello wypychania indeksowania interfejsu API wraz z różnych indeksatory za tworzenie dokumentów wyszukiwania z wielu części. 

Dla tego toowork tooagree na powitania klucz dokumentu należy wszystkich indeksatorów i inne składniki. Aby uzyskać szczegółowy przewodnik, zobacz ten artykuł, zewnętrznych: [łączenie dokumentów z innymi danymi w usłudze Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indeksowania zwykłego tekstu 

Jeśli hello wszystkich obiektów blob zawiera zwykły tekst w tej samej kodowania, może znacznie poprawić wydajność indeksowania, przy użyciu **tekstu podczas analizowania trybu**. tekst toouse analizowania trybie hello zestaw `parsingMode` właściwości konfiguracji zbyt`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Domyślnie program hello `UTF-8` zakłada, że kodowania. toospecify inne kodowanie, użyj hello `encoding` właściwości konfiguracji: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Właściwości metadanych specyficznych dla typu zawartości
Hello Poniższa tabela zawiera podsumowanie przetwarzania wykonywane dla każdego formatu dokumentu oraz opis właściwości metadanych hello wyodrębnione przez usługę Azure Search.

| Format dokumentu / typ zawartości | Właściwości typu zawartości określonych metadanych. | Szczegóły przetwarzania |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Usuwanie kod znaczników HTML i wyodrębnianie tekstu |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Wyodrębnienie tekstu, w tym dokumenty osadzonych (z wyjątkiem obrazy) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| DOKUMENT (programu application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| PPT (aplikacji vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Wyodrębnienie tekstu, w tym osadzonych dokumentów |
| MSG (aplikacji vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Wyodrębnienie tekstu, w tym załączniki |
| ZIP (aplikacja/zip) |`metadata_content_type` |Wyodrębnienie tekstu z wszystkie dokumenty na powitania archiwum |
| XML (aplikacja/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Usuwanie znaczników XML i wyodrębnianie tekstu |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Wyodrębnienie tekstu<br/>Uwaga: Jeśli potrzebujesz tooextract pola wielu dokumentów z obiektu blob JSON, zobacz [obiektów blob JSON indeksowania](search-howto-index-json-blobs.md) Aby uzyskać więcej informacji |
| EML (komunikat/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Wyodrębnienie tekstu, w tym załączniki |
| RTF (aplikacja/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Wyodrębnienie tekstu|
| Zwykłego tekstu (zwykły tekst) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Wyodrębnienie tekstu|


## <a name="help-us-make-azure-search-better"></a>Pomóż nam udoskonalić usługę Azure Search
Daj nam znać, jeśli masz żądania funkcji lub pomysły dotyczące ulepszeń w naszym [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
