---
title: "Indeks tooSearch danych aaaPush przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toopush danych tooAzure indeksu wyszukiwania przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Wypychanie indeksu usługi Azure Search tooan danych przy użyciu fabryki danych Azure
W tym artykule opisano, jak indeks wyszukiwania tooAzure magazynu toouse hello działanie kopiowania toopush danych z obsługiwanych źródła danych. Magazyny danych obsługiwanych źródłowych są wymienione w kolumnie źródła hello hello [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z kombinacji magazynu obsługiwane dane i działanie kopiowania.

## <a name="enabling-connectivity"></a>Włączenie łączności
tooallow usługi fabryka danych połączenia tooan z lokalnym magazynem danych, zainstalować bramę zarządzania danymi w środowisku lokalnym. Możesz zainstalować bramę na hello na tym samym komputerze obsługującym hello źródła danych magazynu lub na tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello danych.

Brama zarządzania danymi nawiązuje połączenie usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi. Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o działanie kopiowania, który wypycha dane z indeksem wyszukiwania tooAzure źródła danych magazynu przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych tooAzure indeks, zobacz [przykład JSON: kopiowanie danych z lokalnego programu SQL Server tooAzure indeks](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure indeksu wyszukiwania:

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Witaj w poniższej tabeli zawiera opisy elementów JSON usługi Azure Search połączone toohello określone.

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| type | musi mieć ustawioną właściwość type Hello: **AzureSearch**. | Tak |
| adres URL | Adres URL hello usługi Azure Search. | Tak |
| key | Klucz administratora dla hello usługi Azure Search. | Tak |

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych. Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu hello **AzureSearchIndex** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| type | zbyt należy ustawić właściwość typu Hello**AzureSearchIndex**.| Tak |
| indexName | Nazwa indeksu usługi Azure Search hello. Fabryki danych nie powoduje utworzenia hello indeksu. Indeks Hello musi istnieć w usłudze Azure Search. | Tak |


## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i tabele wyjściowe i różnych zasad są dostępne dla wszystkich typów działań. Właściwości, które są dostępne w sekcji typeProperties hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Dla działania kopiowania, gdy zbiornika hello jest typu hello **AzureSearchIndexSink**, hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Określa, czy toomerge lub Zastąp, gdy dokument już istnieje w indeksie hello. Zobacz hello [WriteBehavior właściwości](#writebehavior-property).| Merge (ustawienie domyślne)<br/>Upload| Nie |
| writeBatchSize | Przekazywanie danych do indeksu usługi Azure Search hello, gdy osiągnie rozmiar buforu hello writeBatchSize. Zobacz hello [właściwości WriteBatchSize](#writebatchsize-property) szczegółowe informacje. | 1 too1 000. Wartość domyślna to 1000. | Nie |

### <a name="writebehavior-property"></a>Właściwość WriteBehavior
Upserts AzureSearchSink podczas zapisywania danych. Innymi słowy podczas zapisywania dokumentu, jeśli klucz dokumentu hello już istnieje w indeksie usługi Azure Search hello, usługi Azure Search aktualizuje hello istniejącego dokumentu, zamiast zgłaszanie wyjątków konflikt.

Witaj AzureSearchSink zapewnia hello następujące dwa zachowania upsert (przy użyciu zestawu SDK AzureSearch):

- **Scal**: łączenie wszystkich kolumn hello hello nowy dokument z hello jedną istniejącą. Dla kolumn o wartości null w hello nowy dokument wartość hello w hello jedną istniejącą zostanie zachowana.
- **Przekaż**: hello nowy dokument zastępuje hello istniejący. Dla kolumn nie jest określona w hello nowy dokument hello wartość jest ustawiana toonull, czy istnieje wartość inną niż null w hello istniejącego dokumentu lub nie.

Witaj domyślne zachowanie to **scalania**.

### <a name="writebatchsize-property"></a>Właściwość WriteBatchSize
Usługa Azure Search obsługuje dokumenty Zapisywanie jako zadanie wsadowe. Plik wsadowy może zawierać too1 1, 000 akcje. Akcja obsługuje jednej operacji przekazywania/merge hello tooperform dokumentu.

### <a name="data-type-support"></a>Obsługa typu danych
Witaj Poniższa tabela określa, czy lub nie obsługuje typu danych usługi Azure Search.

| Typ danych w usłudze Azure wyszukiwania | Obsługiwane w ujściu usługi Azure Search |
| ---------------------- | ------------------------------ |
| Ciąg | Tak |
| Int32 | Tak |
| Int64 | Tak |
| O podwójnej precyzji | Tak |
| Wartość logiczna | Tak |
| DataTimeOffset | Tak |
| Tablica ciągów | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Przykład JSON: kopiowanie danych z lokalnego programu SQL Server tooAzure wyszukiwania indeksu

następujące przykładowe pokazuje Hello:

1.  Połączonej usługi typu [AzureSearch](#linked-service-properties).
2.  Połączonej usługi typu [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Dane wejściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSearchIndex](#dataset-properties).
4.  A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) i [AzureSearchIndexSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z lokalnymi indeksu usługi Azure Search tooan bazy danych programu SQL Server. właściwości JSON Hello używane w tym przykładzie są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem konfiguracji bramy zarządzania danymi hello na komputerze lokalnym. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**Usługa Azure Search połączone:**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Usługi SQL Server połączone**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**Wejściowy zestaw danych programu SQL Server**

przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w programie SQL Server i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych. Umożliwia wysyłanie zapytań przez wiele tabel w ramach tej samej bazy danych za pomocą jednego zestawu danych, ale pojedynczej tabeli muszą być używane do hello dataset tableName typeProperty powitalne.

Ustawienie "external": "prawda" informuje usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

**Usługa Azure Search wyjściowy zestaw danych:**

Hello próbki kopii danych tooan indeksu usługi Azure Search o nazwie **produkty**. Fabryki danych nie powoduje utworzenia hello indeksu. Witaj tootest przykładowe, Utwórz indeks o tej nazwie. Tworzenie indeksu usługi Azure Search hello z hello taką samą liczbę kolumn, tak jak hello wejściowy zestaw danych. Nowe wpisy są dodawane indeksu usługi Azure Search toohello co godzinę.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy indeksu usługi Azure Search:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**AzureSearchIndexSink**. Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

Jeśli kopiujesz danych z magazynu danych chmury do usługi Azure Search `executionLocation` właściwość jest wymagana. Witaj następujący fragment kodu JSON zawiera hello zmiany wymagane w obszarze działania kopiowania `typeProperties` jako przykład. Sprawdź [kopiowanie danych między magazyny danych w chmurze](data-factory-data-movement-activities.md#global) sekcji obsługiwane wartości i więcej szczegółów.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Skopiuj ze źródłowej chmurze
Jeśli kopiujesz danych z magazynu danych chmury do usługi Azure Search `executionLocation` właściwość jest wymagana. Witaj następujący fragment kodu JSON zawiera hello zmiany wymagane w obszarze działania kopiowania `typeProperties` jako przykład. Sprawdź [kopiowanie danych między magazyny danych w chmurze](data-factory-data-movement-activities.md#global) sekcji obsługiwane wartości i więcej szczegółów.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello. Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie  
Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) oraz różne sposoby toooptimize go.

## <a name="next-steps"></a>Następne kroki
Zobacz następujące artykuły hello:

* [Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.
