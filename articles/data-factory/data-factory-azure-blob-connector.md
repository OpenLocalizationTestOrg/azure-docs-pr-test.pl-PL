---
title: "aaaCopy danych do/z magazynu obiektów Blob Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy obiektu blob danych w fabryce danych Azure. Użyj naszej próbki: jak toocopy tooand danych z magazynu obiektów Blob Azure i bazy danych SQL Azure."
keywords: "dane obiektów blob, kopiowania obiektów blob platformy azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Skopiuj tooor danych z magazynu obiektów Blob platformy Azure przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toocopy danych tooand z magazynu obiektów Blob Azure. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

## <a name="overview"></a>Omówienie
Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure magazynu obiektów Blob lub z magazynu obiektów Blob Azure tooany obsługiwane ujścia danych. Witaj Poniższa tabela zawiera listę magazynów danych są obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello. Na przykład można przenieść dane **z** bazy danych programu SQL Server lub bazy danych Azure SQL **do** magazynu obiektów blob platformy Azure. I dane należy skopiować **z** magazynu obiektów blob Azure **do** magazyn danych SQL Azure lub kolekcji usługi Azure DB rozwiązania Cosmos. 

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z magazynu obiektów Blob Azure** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **tooAzure magazynu obiektów Blob**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Działanie kopiowania obsługuje kopiowania danych z / tooboth kont magazynu ogólnego przeznaczenia Azure i Hot/Cool magazynu obiektów Blob. działanie Hello obsługuje **czytania z bloku, Dołącz lub stronicowe**, ale obsługuje **zapisywania tooonly blokowych obiektów blob**. Usługa Azure Premium Storage nie jest obsługiwany jako zbiorniku, ponieważ nie jest obsługiwana przez stronicowych obiektów blob.
> 
> Aktywność kopiowania nie powoduje usunięcia danych ze źródła hello, po hello, którego dane są pomyślnie skopiowane toohello docelowego. Jeśli potrzebujesz toodelete źródła danych po pomyślnym kopiowania utworzyć [działania niestandardowego](data-factory-use-custom-activities.md) toodelete hello danych i użyj hello działania w potoku hello. Na przykład zobacz hello [usuwania obiektów blob lub folderu przykładem w witrynie GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Rozpoczęcie pracy
Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu obiektów Blob Azure przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Ten artykuł zawiera [wskazówki](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) tworzenia danych toocopy potoku z tooanother lokalizacji magazynu obiektów Blob Azure lokalizacji magazynu obiektów Blob Azure. Samouczek dotyczący tworzenia potoku toocopy danych z magazynu obiektów Blob Azure tooAzure bazy danych SQL, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. Dla właściwości połączonej usługi, które są określone tooAzure magazynu obiektów Blob, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych. I utwórz inny zestaw danych toospecify hello tabeli SQL w bazie danych Azure SQL hello przechowujący dane hello skopiowane z magazynu obiektów blob hello. Dla właściwości zestawu danych, które są określone tooAzure magazynu obiektów Blob, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z bazy danych SQL Azure tooAzure magazynu obiektów Blob, należy użyć SqlSource i BlobSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooAzure magazynu obiektów Blob, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.  

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z magazynu obiektów Blob Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure magazynu obiektów Blob.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Istnieją dwa typy połączonych usług można użyć toolink fabryki danych Azure tooan usługi Azure Storage. Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi. Witaj połączoną usługą magazynu Azure zapewnia usłudze fabryka danych hello z toohello dostępu globalny usługi Azure Storage. Związana hello Azure magazyn SAS (Shared Access Signature) usługa zapewnia usłudze fabryka danych hello z toohello dostęp ograniczony/czas-powiązane z usługi Azure Storage. Nie istnieją inne różnice między tych dwóch połączonych usług. Wybierz usługę hello połączony, który odpowiada Twoim potrzebom. Hello poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Właściwości zestawu danych
toospecify toorepresent zestawu danych wejściowych lub wyjściowych danych w magazynie obiektów Blob Azure, właściwość hello typu DataSet hello do: **AzureBlob**. Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Azure Storage lub SAS magazynu Azure połączonej usługi.  właściwości typu Hello DataSet hello Określ hello **kontenera obiektów blob** i hello **folderu** w magazynie obiektów blob hello.

Pełną listę sekcje JSON & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Fabryka danych obsługuje powitania po zgodne ze specyfikacją CLS .NET na podstawie wartości typu udostępnienie informacji o typie w "strukturę" dla źródeł danych schematu na odczytu obiektów blob platformy Azure: Int16, Int32, Int64, jeden, Double, Decimal, Byte [], Bool, String, Guid, Datetime, Datetimeoffset, Timespan. Fabryka danych automatycznie wykonuje konwersje typów przemieszczając się, że magazyn danych ze źródła danych magazynu danych tooa ujścia.

Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello itp., format hello danych w magazynie danych hello. Witaj typeProperties sekcja dla zestawu danych typu **AzureBlob** dataset zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Ścieżka toohello kontenera i folderu w magazynie obiektów blob hello. Przykład: myblobcontainer\myblobfolder\ |Tak |
| fileName |Nazwa obiektu blob hello. Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.<br/><br/>Jeśli określono nazwę pliku, hello działania (takie jak kopiowanie) działa na hello konkretnego obiektu Blob.<br/><br/>Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w hello folderPath dla zestawu danych wejściowych.<br/><br/>Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello nazwą hello wygenerowany plik będzie w powitania po ten format: dane.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| partitionedBy |partitionedBy jest opcjonalna właściwość. Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych. Na przykład folderPath mogą nadać parametry dla każdej godziny danych. Zobacz hello [przy użyciu sekcji właściwości partitionedBy](#using-partitionedBy-property) szczegółowe informacje i przykłady. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

### <a name="using-partitionedby-property"></a>Za pomocą właściwości partitionedBy
Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).

Aby uzyskać więcej informacji na zestawy danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md) i [planowanie i wykonanie](data-factory-scheduling-and-execution.md) artykułów.

#### <a name="sample-1"></a>Przykład 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona. Witaj SliceStart odwołuje się czas toostart hello wycinka. Witaj folderPath jest różne dla każdego wycinka. Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104

#### <a name="sample-2"></a>Przykład 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań. Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink. Chcesz przenieść dane z magazynu obiektów Blob platformy Azure, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**BlobSource**. Podobnie jeśli przenosisz dane tooan magazynu obiektów Blob Azure ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**BlobSink**. Ta sekcja zawiera listę obsługiwanych przez BlobSource i BlobSink właściwości.

**BlobSource** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |TRUE, False (wartość domyślna) |Nie |

**BlobSink** obsługuje następujące właściwości hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| copyBehavior |Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików. |<b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello. Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.<br/><br/><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello znajdują się w hello najpierw poziomu folderu docelowego. pliki docelowe Hello ma automatycznie wygeneruje nazwę. <br/><br/><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello. Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie. |Nie |

**BlobSource** obsługuje także te dwie właściwości dla zgodności z poprzednimi wersjami.

* **treatEmptyAsNull**: Określa, czy tootreat null lub pusty ciąg jako wartość null.
* **skipHeaderLineCount** — określa liczbę wierszy muszą pominięte. Dotyczy tylko gdy wejściowy zestaw danych używa TextFormat.

Podobnie **BlobSink** obsługuje hello następujące właściwości dla zgodności z poprzednimi wersjami.

* **blobWriterAddHeader**: Określa, czy nagłówek kolumny definicji podczas zapisywania tooan tooadd wyjściowy zestaw danych.

Obsługa hello teraz zestawów danych, następujące właściwości, które implementują hello tę samą funkcjonalność: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Witaj poniższej tabeli znajdują się wskazówki dotyczące przy użyciu hello nowych właściwości zestawu danych, zamiast tych właściwości źródło/ujście obiektu blob.

| Właściwości działania kopiowania | Właściwości zestawu danych |
|:--- |:--- |
| skipHeaderLineCount na BlobSource |skipLineCount i firstRowAsHeader. Wiersze są pomijane najpierw i Odczytaj hello pierwszego wiersza jako nagłówka. |
| treatEmptyAsNull na BlobSource |treatEmptyAsNull w zestawie danych wejściowych |
| blobWriterAddHeader na BlobSink |firstRowAsHeader w zestawie danych wyjściowych |

Zobacz [określenie TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sekcji, aby uzyskać szczegółowe informacje na temat tych właściwości.    

### <a name="recursive-and-copybehavior-examples"></a>Przykłady cyklicznego i copyBehavior
W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.

| Cykliczne | copyBehavior | Efekty |
| --- | --- | --- |
| Wartość true |preserveHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| Wartość true |flattenHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5 |
| Wartość true |mergeFiles |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>docelowy Hello Folder1 jest tworzony z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie |
| wartość false |preserveHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/><br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| wartość false |flattenHierarchy |Dla folderu źródłowego Folder1 z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/><br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| wartość false |mergeFiles |Dla folderu źródłowego Folder1 z następującej struktury hello:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>folder docelowy Hello Folder1 jest tworzony z hello następujące struktury<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie. Nazwa wygenerowana automatycznie Plik1<br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Wskazówki: Użyj Kreatora kopiowania toocopy danych do/z magazynu obiektów Blob
Oto jak magazynu obiektów blob tooquickly kopiowania danych z platformy Azure. W tym przewodniku danych na serwerze źródłowym i docelowym są przechowywane typu: magazyn obiektów Blob Azure. Witaj potoku, w tym przewodniku kopiuje dane z tooanother folderu w hello tego samego kontenera obiektów blob. Ten przewodnik jest celowo proste tooshow ustawienia lub właściwości w przypadku używania magazynu obiektów Blob jako źródło lub ujścia. 

### <a name="prerequisites"></a>Wymagania wstępne
1. Utwórz ogólnego przeznaczenia **konta magazynu Azure** Jeśli nie masz już. Użyj magazynu obiektów blob hello jednocześnie jako **źródła** i **docelowego** magazynu danych, w tym przewodniku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.
2. Tworzenie kontenera obiektów blob o nazwie **adfblobconnector** hello koncie magazynu. 
4. Utwórz folder o nazwie **wejściowych** w hello **adfblobconnector** kontenera.
5. Utwórz plik o nazwie **emp.txt** z powitania po zawartości i przekaż go toohello **wejściowych** folderu za pomocą narzędzi takich jak [Eksploratora usługi Storage platformy Azure](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Tworzenie fabryki danych hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.
3. W hello **nowa fabryka danych** bloku:   
    1. Wprowadź **ADFBlobConnectorDF** dla hello **nazwa**. Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: `*Data factory name “ADFBlobConnectorDF” is not available`, Zmień nazwę hello hello fabryki danych (na przykład yournameADFBlobConnectorDF) i spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
    2. Wybierz swoją **subskrypcję** platformy Azure.
    3. Dla grupy zasobów, wybierz **Użyj istniejącego** tooselect istniejącego zasobu grupy (lub) wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.
    4. Wybierz **lokalizacji** hello fabryki danych.
    5. Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.
    6. Kliknij przycisk **Utwórz**.
3. Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu: ![strony głównej fabryki danych](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Kreator kopiowania
1. Na stronie głównej fabryki danych powitania kliknij hello **kopiowanie danych [Podgląd]** Kafelek toolaunch **kreatora kopiowania danych** w osobnej karcie.    
    
    > [!NOTE]
    >    Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** ustawienie (lub) schowaj włączone i utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić Kreatora hello.
2. W hello **właściwości** strony:
    1. Wprowadź **CopyPipeline** dla **Nazwa zadania**. Nazwa zadania Hello jest nazwa hello hello potok w fabryce danych.
    2. Wprowadź **opis** hello zadania (opcjonalnie).
    3. Dla **okresach zadań lub harmonogram zadań**, Zachowaj hello **regularnego uruchamiania zgodnie z harmonogramem** opcji. Jeśli chcesz toorun to zadanie tylko raz zamiast cyklicznie uruchamiany zgodnie z harmonogramem, wybierz opcję **uruchom raz teraz**. Jeśli zostanie wybrana, **uruchom raz teraz** opcji [potoku jednorazowego](data-factory-create-pipelines.md#onetime-pipeline) jest tworzony. 
    4. Ustawienia hello zachować **wzorzec cykliczny**. To zadanie codziennie działa między hello rozpoczęcia i zakończenia godzin należy określić w hello następnego kroku.
    5. Zmień hello **Data i godzina rozpoczęcia** za**2017-04/21**. 
    6. Zmień hello **Data i godzina zakończenia** za**04/25/2017**. Może być data hello tootype zamiast przeglądania hello kalendarza.     
    8. Kliknij przycisk **Dalej**.
      ![Skopiuj narzędzie — strona właściwości](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Na powitania **magazynu danych źródła** kliknij przycisk **magazyn obiektów Blob Azure** kafelka. Zadanie kopiowania hello są używane magazynu tej strony toospecify hello źródła danych. Możesz użyć istniejącej połączonej usługi magazynu danych lub określić nowy magazyn danych. toouse istniejące połączone usługi, należy wybrać **z ISTNIEJĄCYMI usługami POŁĄCZONEGO** i wybierz hello prawo połączonej usługi. 
    ![Skopiuj narzędzie — strona Sklepu źródła danych](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Na powitania **Określ konto magazynu obiektów Blob platformy Azure hello** strony:
   1. Zachowaj hello automatycznie generowanej nazwę **nazwa połączenia**. Nazwa połączenia Hello jest hello hello połączone usługi typu: Magazyn Azure. 
   2. Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.
   3. Wybierz subskrypcję platformy Azure lub pozostaw **Zaznacz wszystko** dla **subskrypcji platformy Azure**.   
   4. Wybierz **konto magazynu Azure** z hello konta dostępne w ramach subskrypcji hello wybrane listy magazynu Azure. Możesz również tooenter ustawienia konta magazynu ręcznie, wybierając **ręcznie wprowadzić** opcję hello **konta metodę wyboru**.
   5. Kliknij przycisk **Dalej**. 
      ![Skopiuj narzędzie — Określ konto magazynu obiektów Blob platformy Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. Na **wybierz hello wejściowy plik lub folder** strony:
   1. Kliknij dwukrotnie **adfblobcontainer**.
   2. Wybierz **wejściowych**i kliknij przycisk **wybierz**. W tym przewodniku wybierz opcję hello folder wejściowy. Hello emp.txt pliku można również wybrać w folderze hello zamiast tego. 
      ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Na powitania **wybierz hello wejściowy plik lub folder** strony:
    1. Upewnij się, że hello **pliku lub folderu** ustawiono zbyt**adfblobconnector/wprowadzania**. W przypadku plików hello w podfolderach, na przykład 2017/04/01, 2017/04/02 i tak dalej, wprowadź adfblobconnector/danych wejściowych / {year} / {month} / {day} dla pliku lub folderu. Po naciśnięciu klawisza TAB poza pole tekstowe hello, zobaczysz trzech formatów tooselect list rozwijanych roku (rrrr), miesiąc (MM) i dzień (dd). 
    2. Nie ustawiaj **skopiuj plik rekursywnie**. Umożliwia wybranie tej opcji przechodzenia toorecursively za pomocą folderów dla miejsca docelowego skopiowanych toohello toobe plików. 
    3. Nie hello **binarne kopiowania** opcji. Wybierz ten tooperform opcji kopię binarne docelowego toohello pliku źródłowego. Nie należy wybierać w ramach tego przewodnika, dzięki czemu można wyświetlić więcej opcji w kolejnych stronach hello. 
    4. Upewnij się, że hello **typ kompresji** ustawiono zbyt**Brak**. Wybierz wartość dla tej opcji, jeśli plików źródłowych są kompresowane w jednym z formatów hello obsługiwane. 
    5. Kliknij przycisk **Dalej**.
    ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Na powitania **ustawienia formatu pliku** strony, zobacz ograniczniki hello i hello schemat, który jest automatycznie wykrywane przez kreatora hello podczas analizowania pliku hello. 
    1. Potwierdź hello następujące opcje:. Witaj **format pliku** ustawiono zbyt**formacie tekstowym**. Wszystkie formaty hello obsługiwane na liście rozwijanej hello jest widoczny. Na przykład: JSON, Avro, ORC, Parquet.
        b. Witaj **ogranicznik kolumny** ustawiono zbyt`Comma (,)`. Widać hello inne ograniczniki kolumny obsługiwane przez fabrykę danych na liście rozwijanej hello. Można również określić niestandardowe ogranicznika.
        c. Witaj **ogranicznik wiersza** ustawiono zbyt`Carriage Return + Line feed (\r\n)`. Widać hello inne obsługiwane przez fabrykę danych na liście rozwijanej hello ograniczniki wiersza. Można również określić niestandardowe ogranicznika.
        d. Witaj **pominąć licznik wierszy** ustawiono zbyt**0**. Kilka toobe wiersze pominięto u góry hello hello pliku, wprowadź tutaj numer hello.
        e.  Witaj **pierwszy wiersz danych zawiera nazwy kolumn** nie jest ustawiona. Jeśli pliki źródłowe hello zawiera nazwy kolumn w pierwszym wierszu hello, wybierz tę opcję.
        f. Witaj **wartość pusta kolumna jest traktowana jako null** opcja jest ustawiona.
    2. Rozwiń węzeł **Zaawansowane ustawienia** toosee zaawansowane możliwości.
    3. U dołu hello hello strony, zobacz hello **Podgląd** danych z pliku emp.txt hello.
    4. Kliknij przycisk **SCHEMATU** tab na powitania dolnej toosee hello schematu tego kreatora kopiowania hello wykryta przez hello dane w pliku źródłowym hello.
    5. Kliknij przycisk **dalej** po Przejrzyj ograniczniki hello i wyświetlić podgląd danych.
    ![Skopiuj narzędzie — Ustawienia format pliku](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Na powitania **magazyn danych docelowej strony**, wybierz pozycję **magazyn obiektów Blob Azure**i kliknij przycisk **dalej**. Używasz hello magazynu obiektów Blob Azure jako zarówno hello źródłowego i docelowego magazyny danych w ramach tego przewodnika.    
    ![Skopiuj narzędzie — Wybierz miejsce docelowe magazynu danych](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. Na **Określ konto magazynu obiektów Blob platformy Azure hello** strony:
   1. Wprowadź **AzureStorageLinkedService** dla hello **nazwa połączenia** pola.
   2. Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.
   3. Wybierz swoją **subskrypcję** platformy Azure.  
   4. Wybierz konto magazynu platformy Azure. 
   5. Kliknij przycisk **Dalej**.     
10. Na powitania **hello wybierz wyjściowy plik lub folder** strony: 
    6. Określ **ścieżka folderu** jako **adfblobconnector/wyjścia / {year} / {month} / {day}**. Wprowadź **kartę**.
    7. Dla hello **roku**, wybierz pozycję **rrrr**.
    8. Dla hello **miesiąca**, upewnij się, że ustawiono zbyt**MM**.
    9. Dla hello **dzień**, upewnij się, że ustawiono zbyt**dd**.
    10. Upewnij się, że hello **typ kompresji** ustawiono zbyt**Brak**.
    11. Upewnij się, że hello **skopiuj zachowanie** ustawiono zbyt**Scal pliki**. Jeśli hello produkt wyjściowy plik z powitalne tej samej nazwie już istnieje, hello nowej zawartości jest dodany toohello tego samego pliku na końcu hello.
    12. Kliknij przycisk **Dalej**.
    ![Skopiuj narzędzie — Wybierz dane wyjściowe pliku lub folderu](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Na powitania **ustawienia formatu pliku** strony, przejrzyj ustawienia hello, a następnie kliknij przycisk **dalej**. Jednym z hello tutaj dodatkowe opcje jest tooadd pliku wyjściowego toohello nagłówka. Jeśli wybierzesz tę opcję, z nazwami kolumn hello zostanie dodany wiersz nagłówka ze schematu hello hello źródła. Podczas wyświetlania hello schematu źródła hello można zmienić nazwy hello domyślne nazwy kolumn. Na przykład można zmienić hello pierwszej kolumny tooFirst nazwy i drugiej kolumny tooLast nazwy. Następnie plik wyjściowy hello jest generowany przy użyciu nagłówka o tych nazwach jako nazwy kolumn. 
    ![Skopiuj narzędzie — Ustawienia format pliku dla miejsca docelowego](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Na powitania **ustawienia wydajności** strony, upewnij się, że **chmury jednostki** i **równoległe kopie** są ustawiane za**automatycznie**i kliknij przycisk Dalej. Aby uzyskać więcej informacji o tych ustawieniach, zobacz [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md#parallel-copy).
    ![Skopiuj narzędzie — Ustawienia wydajności](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Na powitania **Podsumowanie** strony, przejrzyj wszystkie ustawienia (właściwości zadania, ustawienia źródłowe i docelowe i ustawień kopii), a następnie kliknij przycisk **dalej**.
    ![Skopiuj narzędzie — strona podsumowania](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Przejrzyj informacje w hello **Podsumowanie** , a następnie kliknij przycisk **Zakończ**. Kreator Hello tworzy dwa połączone usługi, dwóch zestawów danych (dane wejściowe i wyjściowe) i jeden potok w fabryce danych hello (z którego uruchamiana jest hello kreatora kopiowania).
    ![Skopiuj narzędzie - stronę wdrożenia](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Monitor hello potoku (zadanie kopiowania)

1. Kliknij łącze hello `Click here toomonitor copy pipeline` na powitania **wdrożenia** strony. 
2. Powinny pojawić się hello **monitorowanie i Zarządzanie aplikacją** w osobnej karcie.  ![Monitorowanie aplikacji i zarządzanie](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Hello zmiany **start** czasu u góry hello zbyt`04/19/2017` i **zakończenia** czasu zbyt`04/27/2017`, a następnie kliknij przycisk **Zastosuj**. 
4. Powinny pojawić się pięć okien działania w hello **okien działania** listy. Witaj **WindowStart** razy powinna obejmować wszystkie dni od czasu zakończenia toopipeline potoku. 
5. Kliknij przycisk **Odśwież** przycisk hello **okien działania** listy kilka razy, aż zostanie wyświetlony stan wszystkich okien działania hello hello ustawiono tooReady. 
6. Teraz Sprawdź, czy pliki wyjściowe hello są generowane w folderze wyjściowym hello adfblobconnector kontenera. Powinny pojawić się następujące struktury folderów w folderze wyjściowym hello hello: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Aby uzyskać szczegółowe informacje o monitorowaniu i zarządzaniu nimi fabryk danych, zobacz [monitora i zarządzanie nimi potoku fabryki danych](data-factory-monitor-manage-app.md) artykułu. 
 
### <a name="data-factory-entities"></a>Obiekty fabryki danych
Teraz Przełącz kartę toohello tylnej strony głównej hello fabryki danych. Zwróć uwagę, że istnieją dwa połączone usługi, dwa zestawy danych i jeden potok w fabryce danych teraz. 

![Strona główna fabryka danych z jednostkami](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Kliknij przycisk **tworzenie i wdrażanie** toolaunch Edytor fabryki danych. 

![Edytor fabryki danych](media/data-factory-azure-blob-connector/data-factory-editor.png)

Powinny pojawić się powitania po jednostek fabryki danych w fabryce danych: 

 - Dwa połączone usługi. Jeden hello źródła i hello innego hello docelowym. Obie te usługi hello połączone można znaleźć toohello tego samego konta magazynu Azure w ramach tego przewodnika. 
 - Dwa zestawy danych. Zestaw wejściowy i wyjściowy zestaw danych. W tym przewodniku, to oba rozwiązania używają hello sam kontenera obiektów blob, ale odwołuje się foldery toodifferent (dane wejściowe i wyjściowe).
 - Potok. potok Hello zawiera działanie kopiowania, który używa źródła obiektów blob i danych obiektów blob zbiornika toocopy z tooanother obiektów blob platformy Azure w lokalizacji lokalizacji obiektu blob systemu Azure. 

Witaj poniższe sekcje zawierają więcej informacji na temat tych jednostek. 

#### <a name="linked-services"></a>Połączone usługi
Powinny pojawić się dwa połączonych usług. Jeden hello źródła i hello innego hello docelowym. W tym przewodniku zarówno wyglądu definicje hello same z wyjątkiem hello nazwy. Witaj **typu** hello połączonej usługi jest ustawiony za**AzureStorage**. Najważniejsze właściwości definicji usługi hello połączony jest hello **connectionString**, który jest używany przez fabryki danych tooconnect tooyour konta magazynu Azure w czasie wykonywania. Ignoruj hello hubName właściwości w definicji hello. 

##### <a name="source-blob-storage-linked-service"></a>Źródła obiektów blob połączoną usługą magazynu
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Docelowy obiekt blob połączoną usługą magazynu

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Aby uzyskać więcej informacji na temat połączoną usługą magazynu Azure, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 

#### <a name="datasets"></a>Zestawy danych
Istnieją dwa zestawy danych: zestaw wejściowy i wyjściowy zestaw danych. Typ Hello hello dataset jest ustawiona zbyt**AzureBlob** dla obu. 

zestaw danych wejściowych Hello punktów toohello **wejściowych** folderu hello **adfblobconnector** kontenera obiektów blob. Witaj **zewnętrznych** właściwość jest ustawiona zbyt**true** dla tego zestawu danych jako hello danych nie został przedstawiony przez potok hello z działanie kopiowania hello, który przyjmuje tego zestawu danych jako dane wejściowe. 

Witaj wyjściowego zestawu danych punktów toohello **dane wyjściowe** folderu hello tego samego kontenera obiektów blob. Witaj wyjściowy zestaw danych używa również hello rok, miesiąc i dzień hello **SliceStart** toodynamically zmiennej systemu obliczyć hello ścieżki do pliku wyjściowego hello. Listę funkcje i zmienne systemu obsługiwane przez fabrykę danych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md). Witaj **zewnętrznych** właściwość jest ustawiona zbyt**false** (wartość domyślna), ponieważ ten zestaw danych jest generowany przez potok hello. 

Aby uzyskać więcej informacji na temat właściwości obsługiwanych przez zestaw danych obiektów Blob platformy Azure, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.

##### <a name="input-dataset"></a>Wejściowy zestaw danych

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Wyjściowy zestaw danych

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Potok
potok Hello jest tylko jedno działanie. Witaj **typu** hello działania jest ustawiony za**kopiowania**.  Właściwości typu hello hello działania istnieją dwie sekcje, jeden dla źródła i hello drugi dla obiekt sink. Typ źródła Hello ustawiono zbyt**BlobSource** jako działania hello jest kopiowanie danych z magazynu obiektów blob. Witaj typ ujścia ustawiono zbyt**BlobSink** jako działania hello kopiowanie magazynu obiektów blob tooa danych. działanie kopiowania Hello przyjmuje InputDataset z4y jako dane wejściowe hello i OutputDataset-z4y jako dane wyjściowe hello. 

Aby uzyskać więcej informacji o obsługiwanych przez BlobSource i BlobSink właściwości, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Przykłady JSON do kopiowania tooand danych z magazynu obiektów Blob  
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z magazynu obiektów Blob Azure i bazy danych SQL Azure. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Przykład JSON: Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [BlobSource](#copy-activity-properties) i [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tabeli Azure SQL tooan obiektów blob platformy Azure. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Azure połączoną usługą SQL:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Połączonej usługi magazynu Azure:**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**. Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego. Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.  

**Azure wejściowego zestawu danych obiektów Blob:**

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": "prawda" ustawienie informuje fabryki danych tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Azure SQL wyjściowy zestaw danych:**

przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w bazie danych Azure SQL. Utwórz tabelę hello w bazie danych Azure SQL z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Przykład JSON: Kopiowanie danych z tooAzure Azure SQL Blob
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) i [BlobSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tooan tabeli Azure SQL obiektów blob platformy Azure. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Azure połączoną usługą SQL:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Połączonej usługi magazynu Azure:**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**. Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego. Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.  

**Azure SQL wejściowy zestaw danych:**

przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Azure SQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.

Ustawienie "external": "prawda" informuje usługi fabryka danych tej tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Azure Blob wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
