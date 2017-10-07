---
title: "aaaMove danych SAP HANA przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych SAP HANA przy użyciu fabryki danych Azure."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Przenoszenie danych z SAP HANA przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi SAP HANA. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z lokalnego SAP HANA magazynu tooany obsługiwane ujścia danych magazynu danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother SAP HANA przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SAP HANA.

## <a name="supported-versions-and-installation"></a>Obsługiwane wersje i instalacji
Ten łącznik obsługuje dowolnej wersji bazy danych SAP HANA. Obsługuje ona kopiowanie danych z tabel wierszy i kolumn, za pomocą zapytań SQL i HANA modelach informacji (takich jak widoki analityczne i obliczeń).

tooenable hello łączności toohello wystąpieniem SAP HANA zainstalować hello następujące składniki:
- **Brama zarządzania danymi**: połączenie lokalne tooon danych obsługuje usługi fabryka danych magazynów (w tym SAP HANA) przy użyciu składnika o nazwie brama zarządzania danymi. Zobacz toolearn o brama zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy hello [przenoszenie danych między danymi lokalnymi przechowywany magazyn danych toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu. Nawet jeśli hello SAP HANA znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama. Możesz zainstalować bramę hello na powitania tej samej maszyny Wirtualnej jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.
- **Sterownik SAP HANA ODBC** na komputerze bramy hello. Sterownik SAP HANA ODBC hello można pobrać z hello [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc). Wyszukiwanie przy użyciu słowa kluczowego hello **SAP HANA klienta dla systemu Windows**. 

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API. 

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello. 
- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego SAP HANA [przykład JSON: kopiowanie danych z programu SAP HANA tooAzure obiektu Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych SAP HANA tooan określonych jednostek fabryki danych używanych toodefine:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj w poniższej tabeli zawiera opis JSON elementy określonych tooSAP HANA połączonej usługi.

Właściwość | Opis | Dozwolone wartości | Wymagane
-------- | ----------- | -------------- | --------
serwer | Nazwa serwera hello, na które hello SAP HANA znajduje się wystąpienie. Jeśli serwer używa portu dostosowane, określ `server:port`. | Ciąg | Tak
Typ authenticationType | Typ uwierzytelniania. | Ciąg. "Basic" lub "Windows" | Tak 
nazwa użytkownika | Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera | Ciąg | Tak
hasło | Hasło dla użytkownika hello. | Ciąg | Tak
gatewayName | Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego SAP HANA wystąpienia. | Ciąg | Tak
encryptedCredential | Witaj zaszyfrowanego ciągu poświadczeń. | Ciąg | Nie

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA hello typu **RelationalTable**. 


## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje SAP HANA), hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query | Określa hello SQL tooread dane z wystąpieniem SAP HANA hello. | Zapytanie SQL. | Tak |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>Przykład JSON: kopiowanie danych z programu SAP HANA tooAzure obiektów Blob
Witaj poniższy przykład zawiera definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). W tym przykładzie pokazano sposób toocopy danych z lokalnego SAP HANA tooan magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello wymienione [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.  

> [!IMPORTANT]
> W tym przykładzie przedstawiono fragmenty kodu JSON. Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [SapHana](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj co godzinę kopiuje dane z SAP HANA tooan wystąpienia obiektów blob platformy Azure. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem konfiguracji bramy zarządzania danymi hello. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

### <a name="sap-hana-linked-service"></a>SAP HANA połączone usługi
To połączone usługi łączy fabrykę danych SAP HANA toohello wystąpienia. Właściwość type Hello ustawiono zbyt**SapHana**. Hello typeProperties sekcja zawiera informacje o połączeniu dla hello wystąpienia SAP HANA.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
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

### <a name="sap-hana-input-dataset"></a>Zestaw danych wejściowych SAP HANA

Ten zestaw danych definiuje zestaw danych SAP HANA hello. Zbyt Ustaw typ hello DataSet fabryki danych hello**RelationalTable**. Obecnie nie określisz żadnych właściwości określonego typu dla zestawu danych SAP HANA. Zapytanie Hello w definicji działania kopiowania hello określa jakie tooread danych z hello wystąpienia SAP HANA. 

Ustawienie właściwości external tootrue informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

Częstotliwość i interwał właściwości definiuje hello harmonogramu. W takim przypadku hello dane są odczytywane z wystąpieniem SAP HANA hello co godzinę. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
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
Ten zestaw danych definiuje hello wyjściowego obiektu Blob systemu Azure zestawu danych. ustawiono tooAzureBlob Hello typu właściwości. sekcja typeProperties Hello zawiera, których są przechowywane dane hello skopiowane z hello SAP HANA wystąpienia. Hello są zapisywane dane nowego obiektu blob tooa co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** (dla źródła SAP HANA) i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Mapowanie typu dla SAP HANA
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych z programu SAP HANA, następujące mapowania hello są używane z typów too.NET typy SAP HANA.

SAP HANA typu | Typ na podstawie .NET
------------- | ---------------
TINYINT | Bajtów
SMALLINT | Int16
INT | Int32
BIGINT | Int64
RZECZYWISTE | Pojedynczy
O PODWÓJNEJ PRECYZJI | Pojedynczy
DECIMAL | Decimal
WARTOŚĆ LOGICZNA | Bajtów
VARCHAR | Ciąg
NVARCHAR | Ciąg
CLOB | Byte]
ALPHANUM | Ciąg
OBIEKT BLOB | Byte]
DATA | Data i godzina
CZAS | Zakres czasu
ZNACZNIK CZASU | Data i godzina
SECONDDATE | Data i godzina

## <a name="known-limitations"></a>Znane ograniczenia
Podczas kopiowania danych z programu SAP HANA istnieje kilka znane ograniczenia:

- Ciągi NVARCHAR to toomaximum skróconą długość 4000 znaków Unicode
- SMALLDECIMAL nie jest obsługiwane.
- VARBINARY nie jest obsługiwane.
- Prawidłowe daty należą do zakresu od 30-1899/12, a 9999-12/31

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
