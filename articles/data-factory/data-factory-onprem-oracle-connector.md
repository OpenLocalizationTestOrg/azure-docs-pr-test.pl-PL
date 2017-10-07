---
title: "aaaCopy danych do/z programem Oracle przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy danych z bazy danych Oracle, który jest lokalnie przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Kopiowanie danych z bazy danych Oracle lokalnymi przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych Oracle. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z bazy danych Oracle** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **bazą danych Oracle tooan**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Fabryka danych obsługuje łączącego źródeł Oracle tooon lokalnych przy użyciu hello brama zarządzania danymi. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) toolearn artykuł na temat bramy zarządzania danymi i [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello potoku danych toomove danych.

Wymagana jest brama, nawet jeśli hello Oracle znajduje się w maszynie Wirtualnej platformy Azure IaaS. Możesz zainstalować bramę hello na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.

> [!NOTE]
> Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.

## <a name="supported-versions-and-installation"></a>Obsługiwane wersje i instalacji
Ten łącznik Oracle obsługuje dwie wersje sterowników:

- **Sterownik firmy Microsoft dla programu Oracle (zalecane)**: począwszy od brama zarządzania danymi w wersji 2.7, sterownik firmy Microsoft dla programu Oracle jest instalowany automatycznie wraz z bramy hello, więc nie trzeba tooadditionally dojście hello sterowników w kolejności tooestablish tooOracle łączność, a także mogą wystąpić lepszą wydajność kopiowania za pomocą tego sterownika. Poniżej wersji Oracle bazy danych są obsługiwane:
    - R1 Oracle 12c (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Sterownik firmy Microsoft dla programu Oracle aktualnie obsługuje tylko kopiowanie danych z programem Oracle, ale bez zapisywania tooOracle. I możliwości połączenia Uwaga hello testów na karcie diagnostyki bramy zarządzania danych nie obsługuje tego sterownika. Alternatywnie można użyć hello kopiowania kreatora toovalidate hello łączności.
>

- **Dostawca danych programu Oracle dla platformy .NET:** można także toouse dostawca danych programu Oracle toocopy danych z / tooOracle. Ten składnik jest uwzględniona w [Oracle danych dostęp do składników dla systemu Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Na maszynie hello, w której zainstalowano bramę hello, należy zainstalować odpowiednią wersję hello (32/64-bitowe). [Dostawca danych programu Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) mogą uzyskiwać dostęp do tooOracle Database 10 g wersji 2 lub nowszej.

    Jeśli zostanie wybrana opcja "Instalacja XCopy", wykonaj kroki w pliku readme.htm hello. Zaleca się wybrać hello Instalatora przy użyciu interfejsu użytkownika (z systemem innym niż — XCopy jeden).

    Po zainstalowaniu dostawcy hello **ponowne uruchomienie** hello usługa hosta bramy zarządzania danymi na tym komputerze za pomocą usługi w aplecie (lub) Menedżera konfiguracji bramy zarządzania danymi.  

Użycie kopii Kreatora tooauthor hello kopiowania potoku hello sterownik typu będzie ustalona automatycznie. Sterownik Microsoft zostanie użyty domyślnie, chyba że używana wersja bramy jest niższa niż 2.7 lub wybierz Oracle jako obiekt sink.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych Oracle przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z Oralce tooan bazy danych magazynu obiektów blob platformy Azure, utworzysz dwa toolink połączonej usługi bazy danych Oracle i fabryki danych tooyour konta magazynu platformy Azure. Dla właściwości połączonej usługi, które są określone tooOracle, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.
3. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. W przykładzie hello wymienionych w ostatnim kroku hello utworzysz tabelę hello toospecify zestawu danych w bazie danych programu Oracle zawiera hello danych wejściowych. Utwórz innego kontenera obiektów blob hello toospecify zestawu danych i folderu hello, która przechowuje dane hello skopiowanych z hello baz danych programu Oracle. Dla właściwości zestawu danych, które są określone tooOracle [właściwości zestawu danych](#dataset-properties) sekcji.
4. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa OracleSource jako źródło i BlobSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z magazynu obiektów Blob Azure tooOracle bazy danych, należy użyć BlobSource i OracleSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooOracle bazy danych, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z lokalną bazą danych Oracle, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine jednostek fabryki danych:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooOracle połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **OnPremisesOracle** |Tak |
| driverType | Określ, które sterownik toouse toocopy dane z / tooOracle bazy danych. Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne). Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika. | Nie |
| Parametry połączenia | Określ informacje niezbędne wystąpienie bazy danych Oracle toohello tooconnect hello właściwości connectionString. | Tak |
| gatewayName | Nazwa bramy hello, że jest używana tooconnect toohello lokalnego serwera Oracle |Tak |

**Przykład: za pomocą sterownika Microsoft:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Przykład: za pomocą sterownika ODP**

Odwołuje się zbyt[tej lokacji](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) dla hello dozwolone formaty.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Oracle, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj typeProperties sekcja dla zestawu danych hello typu OracleTable ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Oznacza nazwę tabeli hello na powitania hello połączonej usługi bazy danych programu Oracle. |Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona) |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

> [!NOTE]
> Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

### <a name="oraclesource"></a>OracleSource
W przypadku działania kopiowania, gdy źródłem hello jest typu **OracleSource** hello następujące właściwości są dostępne w **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| oracleReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: Wybierz * z MyTable <br/><br/>Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz * z MyTable |Nie (Jeśli **tableName** z **dataset** jest określona) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: 00:30:00 (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 100) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Przykłady JSON do kopiowania tooand danych z bazy danych Oracle
Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy danych z / tooan Oracle bazy danych do/z magazynu obiektów Blob Azure. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Przykład: Kopiowanie danych z programu Oracle tooAzure obiektów Blob

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako źródło i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) jako obiekt sink.

przykład Witaj co godzinę kopiuje dane z tabeli w obiekcie blob tooa bazy danych Oracle lokalnymi. Aby uzyskać więcej informacji na różne właściwości używane w przykładowym hello dokumentacji w sekcjach poniżej hello próbek.

**Oracle połączone usługi:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Magazyn obiektów Blob Azure połączonej usługi:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Wejściowy zestaw danych Oracle:**

przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w oprogramowaniu Oracle i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**W potoku z działania kopiowania:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**OracleSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.  Zapytanie SQL Hello określony za pomocą **oracleReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Przykład: Kopiowanie danych z tooOracle obiektów Blob platformy Azure
W tym przykładzie pokazano sposób toocopy danych z magazynu obiektów Blob Azure tooan lokalnej bazy danych programu Oracle. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.  

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) jako źródło [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako obiekt sink.

przykład Witaj kopiuje dane z tabeli tooa obiektów blob w lokalną bazą danych Oracle co godzinę. Aby uzyskać więcej informacji na różne właściwości używane w przykładowym hello dokumentacji w sekcjach poniżej hello próbek.

**Oracle połączone usługi:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Magazyn obiektów Blob Azure połączonej usługi:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Azure wejściowego zestawu danych obiektów Blob**

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
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

**Oracle wyjściowy zestaw danych:**

przykład Witaj przyjęto założenie, że w Oracle utworzono tabelę "MyTable". Utwórz tabelę hello w oprogramowaniu Oracle z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**W potoku z działania kopiowania:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i hello **zbiornika** typu ustawiono zbyt**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Wskazówki dotyczące rozwiązywania problemów
### <a name="problem-1-net-framework-data-provider"></a>Problem 1: Dostawca danych programu .NET Framework

Zobacz następujące hello **komunikat o błędzie**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Możliwe przyczyny:**

1. Witaj .NET Framework Data Provider for Oracle nie został zainstalowany.
2. .NET Framework Data Provider for Oracle Hello został zainstalowany too.NET Framework 2.0 i nie został znaleziony w folderach hello programu .NET Framework 4.0.

**Rozdzielczość/obejście problemu:**

1. Jeśli nie zainstalowano hello dostawcy .NET dla Oracle, [go zainstalować](http://www.oracle.com/technetwork/topics/dotnet/downloads/) i ponów próbę hello scenariusza.
2. Jeśli otrzymasz komunikat o błędzie hello nawet po zainstalowaniu dostawcy hello hello następujące kroki:
   1. Otwórz konfiguracji komputera programu .NET 2.0 z folderu hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Wyszukaj **dostawca danych programu Oracle dla platformy .NET**, i powinno być możliwe toofind wpis pokazane na powitania po próbki w **system.dane** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Dostawca danych programu oracle dla platformy .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Skopiuj ten plik machine.config toohello wpis w hello następującego folderu v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config i too4.xxx.x.x wersji hello zmiany.
4. Zainstaluj "\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll < ścieżka instalacji ODP.NET >" na powitania globalnej pamięci podręcznej zestawów (GAC), uruchamiając `gacutil /i [provider path]`. ## porady dotyczące rozwiązywania problemów

### <a name="problem-2-datetime-formatting"></a>Problem 2: formatowanie daty/godziny

Zobacz następujące hello **komunikat o błędzie**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Rozdzielczość/obejście problemu:**

Ciąg zapytania hello tooadjust może być konieczne w przypadku Twojego działania kopiowania oparte na konfiguracji daty w bazie danych programu Oracle, jak pokazano poniżej hello próbki (przy użyciu funkcji to_date hello):

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Mapowanie typu dla Oracle
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych z bazy danych Oracle, następujące mapowania hello są używane z too.NET typu danych Oracle i na odwrót.

| Typ danych Oracle | Typ danych .NET framework |
| --- | --- |
| BPLIK |Byte] |
| OBIEKT BLOB |Byte] |
| CHAR |Ciąg |
| CLOB |Ciąg |
| DATA |Data i godzina |
| FLOAT |Decimal, ciąg (jeśli precyzja > 28) |
| LICZBA CAŁKOWITA |Decimal, ciąg (jeśli precyzja > 28) |
| INTERWAŁ tooMONTH roku |Int32 |
| INTERWAŁ tooSECOND dnia |Zakres czasu |
| DŁUGA |Ciąg |
| LONG RAW |Byte] |
| NCHAR |Ciąg |
| NCLOB |Ciąg |
| NUMER |Decimal, ciąg (jeśli precyzja > 28) |
| NVARCHAR2 |Ciąg |
| NIEPRZETWORZONE |Byte] |
| ROWID |Ciąg |
| ZNACZNIK CZASU |Data i godzina |
| SYGNATURA CZASOWA Z LOKALNEJ STREFIE CZASOWEJ |Data i godzina |
| SYGNATURA CZASOWA ZE STREFĄ CZASOWĄ |Data i godzina |
| LICZBA CAŁKOWITA BEZ ZNAKU |Liczba |
| VARCHAR2 |Ciąg |
| XML |Ciąg |

> [!NOTE]
> Typ danych **tooMONTH roku INTERWAŁ** i **tooSECOND dzień INTERWAŁ** nie są obsługiwane, gdy za pomocą sterownika Microsoft.

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
