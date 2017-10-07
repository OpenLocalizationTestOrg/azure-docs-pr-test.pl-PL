---
title: aaaMove danych do/z tabel Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomove danych do/z magazynem tabel Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Przenieś tooand danych z tabel Azure przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z magazynu tabel platformy Azure. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania. 

Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure magazynu tabel lub z magazynu tabel Azure tooany obsługiwane ujścia danych. Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. 

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu tabel Azure przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z magazynu tabel Azure, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure magazynu tabel: 

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Istnieją dwa typy połączonych usług można użyć toolink fabryki danych Azure tooan magazynu obiektów blob platformy Azure. Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi. Witaj połączoną usługą magazynu Azure zapewnia usłudze fabryka danych hello z toohello dostępu globalny usługi Azure Storage. Związana hello Azure magazyn SAS (Shared Access Signature) usługa zapewnia usłudze fabryka danych hello z toohello dostęp ograniczony/czas-powiązane z usługi Azure Storage. Nie istnieją inne różnice między tych dwóch połączonych usług. Wybierz usługę hello połączony, który odpowiada Twoim potrzebom. Hello poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureTable** ma hello następujące właściwości.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w wystąpieniu bazy danych tabeli Azure hello, która jest połączona usługa odnosi się do. |Tak. TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego. Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego. |

### <a name="schema-by-data-factory"></a>Schemat fabryka danych
Dla magazynów danych bez schematu, takie jak tabel Azure hello usługi fabryka danych wnioskuje schemat hello w jednym z hello następujące sposoby:

1. Jeśli określisz hello struktury danych za pomocą hello **struktury** tej struktury Schema hello honoruje właściwości w definicji zestawu danych hello, hello usługi fabryka danych. W tym przypadku jeśli wiersza nie zawiera wartości dla kolumny, wartość null podano dla niego.
2. Jeśli nie określisz hello struktury danych za pomocą hello **struktury** właściwości w definicji zestawu danych hello, fabryki danych wnioskuje schemat hello przy użyciu danych hello hello pierwszego wiersza. W takim przypadku jeśli pierwszy wiersz hello nie zawiera pełnej schematu hello, niektóre kolumny zostaną pominięte w hello wynik operacji kopiowania.

W związku z tym dla źródeł danych bez schematu hello najlepszym rozwiązaniem jest toospecify hello struktury danych za pomocą hello **struktury** właściwości.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w sekcji typeProperties hello aktywności hello na powitania drugiej zależą od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

**AzureTableSource** obsługuje następujące właściwości w sekcji typeProperties hello:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| azureTableSourceQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania tabeli platformy Azure. Przykłady w następnej sekcji hello. |Nie. TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego. Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego. |
| azureTableSourceIgnoreTableNotFound |Wskazuje, czy wyjątek hello swallow tabeli nie istnieją. |WARTOŚĆ TRUE<br/>WARTOŚĆ FALSE |Nie |

### <a name="azuretablesourcequery-examples"></a>Przykłady azureTableSourceQuery
W przypadku tabel Azure kolumny typu string:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

W przypadku tabel Azure kolumny typu Data/Godzina:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** obsługuje następujące właściwości w sekcji typeProperties hello:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink hello. |Wartość ciągu. |Nie |
| azureTablePartitionKeyName |Określ nazwę kolumny hello, których wartości są używane jako klucze partycji. Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji hello. |Nazwa kolumny. |Nie |
| azureTableRowKeyName |Określ nazwę kolumny hello, w których wartości kolumn używanych jako klucz wiersza. Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza. |Nazwa kolumny. |Nie |
| azureTableInsertType |Tryb Hello tooinsert dane w tabeli platformy Azure.<br/><br/>Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników hello ze zgodnymi kluczami partycji i wiersza. <br/><br/>toolearn informacji na temat tych ustawień (scalania i Zastąp) działania, zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów. <br/><br> To ustawienie jest stosowane na poziomie wiersza hello, nie poziomu tabeli hello i żadna z tych opcji usuwa wiersze w tabeli wyników hello, które nie istnieją w danych wejściowych hello. |Merge (ustawienie domyślne)<br/>Zamień |Nie |
| writeBatchSize |Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| writeBatchTimeout |Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout |Zakres czasu<br/><br/>Przykład: "00:20:00" (20 minut) |Nie (domyślna toostorage klienta domyślny limit czasu operacji wartość 90 s) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Mapowanie kolumny docelowej tooa kolumny źródła przy użyciu właściwości JSON translator hello, zanim będzie możliwe użycie kolumna docelowa hello jako hello azureTablePartitionKeyName.

W hello poniższy przykład, kolumna źródłowa DivisionID jest kolumna docelowa zamapowanych toohello: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Witaj DivisionID jest określony jako klucza partycji hello.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Przykłady JSON
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z magazynu tabel platformy Azure i bazy danych obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** za pomocą dowolnego hello tooany źródeł z wychwytywanie hello obsługiwane. Aby uzyskać więcej informacji, zobacz sekcję hello, "obsługiwane magazyny danych i formaty" w [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Przykład: Kopiowanie danych z tabel Azure tooAzure obiektów Blob
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli).
2. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).
3. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [AzureTableSource](#activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane należące toohello domyślnej partycji w obiekcie blob tooa tabel Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Połączonej usługi magazynu Azure:**

```JSON
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

**Azure tabeli wejściowy zestaw danych:**

przykład Witaj przyjęto założenie, że utworzono tabelę "MyTable" w tabeli platformy Azure.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

```JSON
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

**Działanie kopiowania w potoku z AzureTableSource i BlobSink:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**AzureTableSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określony za pomocą **AzureTableSourceQuery** właściwości wybiera hello danych z partycji domyślnej hello toocopy co godzinę.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure tabeli
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli)
2. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).
4. Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [AzureTableSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tooan obiektów blob platformy Azure tabeli platformy Azure. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Usługa Azure storage (dla tabeli platformy Azure i obiektów Blob) połączonej usługi:**

```JSON
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

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": "prawda" ustawienie informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Tabeli platformy Azure wyjściowy zestaw danych:**

przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w tabeli platformy Azure. Tworzenie tabeli platformy Azure z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Działanie kopiowania w potoku z BlobSource i AzureTableSink:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a>Mapowanie typu dla tabeli platformy Azure
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie.

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych za & z tabel Azure, hello po [mapowania zdefiniowane przez usługę Azure tabeli](https://msdn.microsoft.com/library/azure/dd179338.aspx) są używane z typu too.NET typy OData tabeli platformy Azure i na odwrót.

| Typ danych OData | Typ architektury .NET | Szczegóły |
| --- | --- | --- |
| Edm.Binary |Byte] |Tablica bajtów się too64 KB. |
| Edm.Boolean |wartość logiczna |Wartość logiczna. |
| Edm.DateTime |Data i godzina |Wartość 64-bitowa, wyrażone jako uniwersalny czas koordynowany (UTC). Witaj obsługiwany zakres zaczyna się od 12:00, a 1 stycznia, 1601 r. N.E. daty/godziny (R), CZAS UTC. zakres Hello kończy się na 31 grudnia 9999 r. |
| Edm.Double |O podwójnej precyzji |64-bitowej zmiennej punktu wartości. |
| Edm.Guid |Identyfikator GUID |Globalnie unikatowy identyfikator 128-bitowego. |
| Edm.Int32 |Int32 |32-bitową liczbę całkowitą. |
| Edm.Int64 |Int64 |64-bitową liczbę całkowitą. |
| Edm.String |Ciąg |Wartość algorytmem UTF-16. Wartości parametrów może być aktywne too64 KB. |

### <a name="type-conversion-sample"></a>Przykładowe konwersji typu
następujące przykładowe Hello jest kopiowania danych z tabeli tooAzure obiektów Blob platformy Azure z konwersji typu.

Załóżmy, że hello zestawu danych obiektów Blob jest w formacie CSV zawiera trzy kolumny. Jeden z nich jest kolumną daty/godziny w formacie datetime niestandardowych za pomocą nazwy skróconej francuskim dzień tygodnia hello.

Definiowanie zestawu danych obiektów Blob źródła hello następujący wraz z definicji typu dla kolumny hello.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Biorąc pod uwagę mapowanie typu hello z too.NET typu OData tabeli platformy Azure, czy definiuje hello tabeli w tabeli platformy Azure z hello następującego schematu.

**Schemat tabeli platformy Azure:**

| Nazwa kolumny | Typ |
| --- | --- |
| Nazwa użytkownika |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

Następnie określ następujący hello Azure tabeli dataset. Nie trzeba toospecify "structure" sekcji informacji o typach powitania od informacji o typie hello został już określony w hello bazowy magazynu danych.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

W takim przypadku fabryka danych automatycznie konwersje typów tym hello pola daty/godziny w formacie datetime niestandardowych hello przy użyciu kultury "fr-fr" hello, podczas przenoszenia danych z obiektu Blob tooAzure tabeli.

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize, zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md).
