---
title: "aaaMove danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a>Przenoszenie danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi SAP Business magazynu (BW). Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z lokalnego SAP Business Warehouse magazynu tooany obsługiwane ujścia danych magazynu danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother SAP Business Warehouse przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SAP Business Warehouse. 

## <a name="supported-versions-and-installation"></a>Obsługiwane wersje i instalacji
Ten łącznik obsługuje wersję SAP Business Warehouse 7.x. Obsługuje ona kopiowania danych z InfoCubes i QueryCubes (takie jak zapytania BEx) przy użyciu zapytania MDX.

tooenable hello łączności toohello wystąpienia programu SAP BW zainstalować hello następujące składniki:
- **Brama zarządzania danymi**: połączenie lokalne tooon danych obsługuje usługi fabryka danych magazynów (w tym SAP Business Warehouse) przy użyciu składnika o nazwie brama zarządzania danymi. Zobacz toolearn o brama zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy hello [przenoszenie danych między danymi lokalnymi przechowywany magazyn danych toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu. Nawet jeśli hello SAP Business Warehouse znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama. Możesz zainstalować bramę hello na powitania tej samej maszyny Wirtualnej jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.
- **SAP NetWeaver biblioteki** na komputerze bramy hello. Hello SAP Netweaver biblioteki można uzyskać od administratora SAP, lub bezpośrednio z hello [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc). Wyszukaj hello **&#1025361; Uwaga SAP** lokalizację pobierania hello tooget hello najnowszej wersji. Upewnij się, że architektura hello hello SAP NetWeaver biblioteki (32-bitowy lub 64-bitowy) odpowiada instalacji bramy. Następnie zainstaluj wszystkie pliki zawarte w hello SAP NetWeaver RFC SDK zgodnie z toohello Uwaga SAP. Witaj SAP NetWeaver biblioteki dołączony jest również hello instalacji narzędzi klienta SAP.

> [!TIP]
> Umieść biblioteki DLL hello wyodrębniony z hello NetWeaver RFC SDK w folderze system32.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API. 

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello. 
- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego SAP Business Warehouse, zobacz [przykład JSON: kopiowanie danych z programu SAP Business Warehouse tooAzure obiektu Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych programu SAP BW tooan określonych jednostek fabryki danych używanych toodefine:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj w poniższej tabeli przedstawiono opis dla określonych tooSAP elementów JSON usługi biznesowe magazynu (BW) połączony.

Właściwość | Opis | Dozwolone wartości | Wymagane
-------- | ----------- | -------------- | --------
serwer | Nazwa serwera hello, na które hello programu SAP BW znajduje się wystąpienie. | Ciąg | Tak
systemNumber | Numer systemu hello systemu SAP BW. | Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg. | Tak
clientId | Identyfikator klienta na powitania klienta w hello systemu SAP W. | Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg. | Tak
nazwa użytkownika | Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera | Ciąg | Tak
hasło | Hasło dla użytkownika hello. | Ciąg | Tak
gatewayName | Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego programu SAP BW wystąpienia. | Ciąg | Tak
encryptedCredential | Witaj zaszyfrowanego ciągu poświadczeń. | Ciąg | Nie

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych z programu SAP BW hello typu **RelationalTable**. 


## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje programu SAP BW), hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query | Określa dane tooread zapytania MDX hello z wystąpienia programu SAP BW hello. | Zapytania MDX. | Tak |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a>Przykład JSON: kopiowanie danych z programu SAP Business Warehouse tooAzure obiektów Blob
Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). W tym przykładzie pokazano sposób toocopy danych z lokalnego SAP Business Warehouse tooan magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.  

> [!IMPORTANT]
> W tym przykładzie przedstawiono fragmenty kodu JSON. Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [SapBw](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Przykładowe Hello co godzinę kopiuje dane z programu SAP Business Warehouse tooan wystąpienia obiektów blob platformy Azure. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem konfiguracji bramy zarządzania danymi hello. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

### <a name="sap-business-warehouse-linked-service"></a>SAP Business Warehouse połączona usługa
To połączone usługi łączy fabrykę danych toohello wystąpienia programu SAP BW. Właściwość type Hello ustawiono zbyt**SapBw**. Witaj typeProperties sekcja zawiera informacje o połączeniu dla wystąpienia programu SAP BW hello. 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
To połączone usługi łączy fabrykę danych toohello konta magazynu Azure. Właściwość type Hello ustawiono zbyt**AzureStorage**. Witaj typeProperties sekcja zawiera informacje o połączeniu dla hello konta magazynu Azure.

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="sap-bw-input-dataset"></a>Wejściowy zestaw danych SAP BW
Ten zestaw danych definiuje zestaw danych SAP Business Warehouse hello. Zbyt Ustaw typ hello DataSet fabryki danych hello**RelationalTable**. Obecnie nie określisz żadnych właściwości określonego typu dla programu SAP BW zestawu danych. zapytania Hello w definicji działania kopiowania hello Określa, jakie tooread danych z wystąpienia programu SAP BW hello. 

Ustawienie właściwości external tootrue informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

Częstotliwość i interwał właściwości definiuje hello harmonogramu. W takim przypadku hello dane są odczytywane z wystąpienia programu SAP BW hello co godzinę. 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure
Ten zestaw danych definiuje hello wyjściowego obiektu Blob systemu Azure zestawu danych. ustawiono tooAzureBlob Hello typu właściwości. sekcja typeProperties Hello zawiera, którym są przechowywane dane hello skopiowane z wystąpienia programu SAP BW hello. Hello są zapisywane dane nowego obiektu blob tooa co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
        }
    }
}
```


### <a name="pipeline-with-copy-activity"></a>W potoku z działanie kopiowania
Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** (dla programu SAP BW źródła) i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a>Mapowanie typu dla programu SAP BW
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych z programu SAP BW, następujące mapowania hello są używane z programu SAP BW typy too.NET typów.

Typ danych w hello ABAP słownik | Typ danych .net
-------------------------------- | --------------
ACCP |  int
CHAR | Ciąg
CLNT | Ciąg
BI | Decimal
CUKY | Ciąg
DEC | Decimal
FLTP | O podwójnej precyzji
INT1 | Bajtów
INT2 | Int16
INT4 | int
JĘZYK | Ciąg
LCHR | Ciąg
LRAW | Byte]
PREC | Int16
QUAN | Decimal
NIEPRZETWORZONE | Byte]
RAWSTRING | Byte]
CIĄG | Ciąg
JEDNOSTKI | Ciąg
DATS | Ciąg
NUMC | Ciąg
TIMS | Ciąg

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).


## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
