---
title: "aaaMove danych z PostgreSQL przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z bazy danych PostgreSQL przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>Przenoszenia danych z PostgreSQL przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych PostgreSQL. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z lokalnego PostgreSQL magazynu tooany obsługiwane ujścia danych magazynu danych. Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania hello, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Fabryki danych obecnie obsługuje przenoszenia danych z PostgreSQL bazy danych tooother magazyny danych, ale nie do przenoszenia danych z innych danych przechowuje tooan bazą danych PostgreSQL. 

## <a name="prerequisites"></a>Wymagania wstępne

Usługi fabryka danych obsługuje łączenia źródeł PostgreSQL tooon lokalnych przy użyciu hello brama zarządzania danymi. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.

Wymagana jest brama, nawet wtedy, gdy baza danych PostgreSQL hello znajduje się w maszynie Wirtualnej platformy Azure IaaS. Możesz zainstalować bramę na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.

> [!NOTE]
> Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.

## <a name="supported-versions-and-installation"></a>Obsługiwane wersje i instalacji
Brama zarządzania danymi tooconnect toohello PostgreSQL bazy danych, można zainstalować w hello [Ngpsql dostawcy danych PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 lub powyżej na hello sam system jako hello brama zarządzania danymi. PostgreSQL wersji 7.4 i nowszej jest obsługiwana.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych PostgreSQL lokalnymi przy użyciu różnych narzędzi/interfejsów API. 

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello. 
- Można także użyć hello następujące narzędzia toocreate potoku: 
    - Azure Portal
    - Visual Studio
    - Azure PowerShell
    - Szablon usługi Azure Resource Manager
    - Interfejs API .NET
    - Interfejs API REST

     Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego magazynu danych PostgreSQL [przykład JSON: kopiowanie danych z tooAzure PostgreSQL obiektu Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych PostgreSQL tooa określonych jednostek fabryki danych używanych toodefine:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooPostgreSQL połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **OnPremisesPostgreSql** |Tak |
| serwer |Nazwa serwera PostgreSQL hello. |Tak |
| Bazy danych |Nazwa bazy danych PostgreSQL hello. |Tak |
| Schemat |Nazwa schematu hello hello bazy danych. Nazwa schematu Hello jest rozróżniana wielkość liter. |Nie |
| Typ authenticationType |Typ uwierzytelniania używany tooconnect toohello PostgreSQL w bazie danych. Możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych PostgreSQL. |Tak |

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych PostgreSQL) ma następujące właściwości hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w hello wystąpienie bazy danych PostgreSQL, odnoszący się do połączonej usługi. Witaj tableName jest rozróżniana wielkość liter. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Jeśli źródło jest typu **RelationalSource** (która obejmuje PostgreSQL), hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: "zapytania": "Wybierz * z \"MySchema\".\" MyTable\"". |Nie (Jeśli **tableName** z **dataset** jest określona) |

> [!NOTE]
> Nazwy schematu i tabeli jest rozróżniana wielkość liter. Umieść je w `""` (podwójne cudzysłowy) w zapytaniu hello.  

**Przykład:**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>Przykład JSON: kopiowanie danych z tooAzure PostgreSQL obiektów Blob
W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy danych PostgreSQL bazy danych tooAzure magazynu obiektów Blob. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.   

> [!IMPORTANT]
> W tym przykładzie przedstawiono fragmenty kodu JSON. Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych PostgreSQL co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem konfiguracji bramy zarządzania danymi hello. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**PostgreSQL połączonej usługi:**

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
**Magazyn obiektów Blob Azure połączonej usługi:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**Wejściowy zestaw danych PostgreSQL:**

przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" PostgreSQL i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.

Ustawienie `"external": true` informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**W potoku z działania kopiowania:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello danych z tabeli public.usstates hello w bazie danych PostgreSQL hello.

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>Mapowanie typu dla PostgreSQL
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych tooPostgreSQL, hello następujące mapowania są używane z PostgreSQL too.NET typu.

| Typ bazy danych PostgreSQL | Aliasy PostgresSQL | Typ programu .NET framework |
| --- | --- | --- |
| abstime | |Data i godzina | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| bitowe [(n)] | |Byte [], ciąg | &nbsp;
| bit zróżnicowanie [(n)] |varbit |Byte [], ciąg |
| Wartość logiczna |wartość logiczna |Wartość logiczna |
| Pole | |Byte [], ciąg |&nbsp;
| bytea | |Byte [], ciąg |&nbsp;
| znak [(n)] |char [(n)] |Ciąg |
| znak zróżnicowanie [(n)] |varchar [(n)] |Ciąg |
| CID | |Ciąg |&nbsp;
| CIDR | |Ciąg |&nbsp;
| koło | |Byte [], ciąg |&nbsp;
| Data | |Data i godzina |&nbsp;
| DateRange | |Ciąg |&nbsp;
| podwójnej precyzji |FLOAT8 |O podwójnej precyzji |
| inet | |Byte [], ciąg |&nbsp;
| intarry | |Ciąg |&nbsp;
| int4range | |Ciąg |&nbsp;
| int8range | |Ciąg |&nbsp;
| Liczba całkowita |int, int4 |Int32 |
| Interwał [pola] [(p)] | |Zakres czasu |&nbsp;
| JSON | |Ciąg |&nbsp;
| jsonb | |Byte] |&nbsp;
| wiersz | |Byte [], ciąg |&nbsp;
| lseg | |Byte [], ciąg |&nbsp;
| macaddr | |Byte [], ciąg |&nbsp;
| oszczędność pieniędzy | |Decimal |&nbsp;
| numeryczne [(p, s)] |decimal [(p, s)] |Decimal |
| numrange | |Ciąg |&nbsp;
| Identyfikator OID | |Int32 |&nbsp;
| Ścieżka | |Byte [], ciąg |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| punkt | |Byte [], ciąg |&nbsp;
| wielokąta | |Byte [], ciąg |&nbsp;
| rzeczywiste |FLOAT4 |Pojedynczy |
| smallint |int2 |Int16 |
| smallserial |serial2 |Int16 |
| Szeregowe |serial4 |Int32 |
| Tekst | |Ciąg |&nbsp;

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
