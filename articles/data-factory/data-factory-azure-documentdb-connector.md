---
title: "aaaMove danych do/z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przenieść dane do/z bazy danych Azure rozwiązania Cosmos kolekcji przy użyciu fabryki danych Azure"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Przenieś tooand danych z bazy danych rozwiązania Cosmos Azure przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z bazy danych Azure rozwiązania Cosmos (interfejsu API usługi DocumentDB). Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania. 

Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure rozwiązania Cosmos bazy danych lub z bazy danych Azure rozwiązania Cosmos tooany obsługiwane ujścia danych. Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. 

> [!IMPORTANT]
> Łącznik usługi Azure DB rozwiązania Cosmos obsługują tylko interfejsu API usługi DocumentDB.

dane toocopy jako — jest do/z pliki w formacie JSON lub innej kolekcji rozwiązania Cosmos bazy danych, zobacz [dokumentów JSON importu/eksportu](#importexport-json-documents).

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych rozwiązania Cosmos Azure przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z rozwiązania Cosmos bazy danych, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooCosmos bazy danych: 

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj w poniższej tabeli przedstawiono opis dla określonych tooAzure elementów JSON DB rozwiązania Cosmos połączone usługi.

| **Właściwość** | **Opis** | **Wymagane** |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **usługi DocumentDb** |Tak |
| Parametry połączenia |Określ informacje niezbędne tooconnect tooAzure DB rozwiązania Cosmos w bazie danych. |Tak |

Przykład:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Pełną listę sekcje & właściwości dostępne do definiowania zestawów danych można znaleźć toohello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Jak struktura, dostępności i zasad zestawu danych JSON jest podobna dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj typeProperties sekcja dla zestawu danych hello typu **DocumentDbCollection** ma hello następujące właściwości.

| **Właściwość** | **Opis** | **Wymagane** |
| --- | --- | --- |
| CollectionName |Nazwa hello kolekcji dokumentów DB rozwiązania Cosmos. |Tak |

Przykład:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Schemat fabryka danych
Dla magazynów danych bez schematu, takie jak bazy danych Azure rozwiązania Cosmos hello usługi fabryka danych wnioskuje schemat hello w jednym z hello następujące sposoby:  

1. Jeśli określisz hello struktury danych za pomocą hello **struktury** tej struktury Schema hello honoruje właściwości w definicji zestawu danych hello, hello usługi fabryka danych. W takim przypadku wiersza nie zawiera wartości dla kolumny, będzie należy podać dla niego wartość null.
2. Jeśli nie określisz hello struktury danych za pomocą hello **struktury** właściwości w definicji zestawu danych hello, hello usługi fabryka danych wnioskuje schemat hello przy użyciu danych hello hello pierwszego wiersza. W takim przypadku jeśli pierwszy wiersz hello nie zawiera pełnej schematu hello, niektóre kolumny będą niedostępne w hello wynik operacji kopiowania.

W związku z tym dla źródeł danych bez schematu hello najlepszym rozwiązaniem jest toospecify hello struktury danych za pomocą hello **struktury** właściwości.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań można znaleźć toohello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

> [!NOTE]
> Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.

Właściwości dostępne w sekcji typeProperties hello aktywności hello na powitania drugiej różnią się każdy typ działania, a w przypadku działania kopiowania różnią się w zależności od typów hello źródeł i sink.

W przypadku działania kopiowania, gdy źródłem jest typu **DocumentDbCollectionSource** hello następujące właściwości są dostępne w **typeProperties** sekcji:

| **Właściwość** | **Opis** | **Dozwolone wartości** | **Wymagane** |
| --- | --- | --- | --- |
| query |Określ hello zapytania tooread dane. |Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos. <br/><br/>Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Nie <br/><br/>Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate znak specjalny, który hello dokumentu jest zagnieżdżony. |Dowolny znak. <br/><br/>Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone. Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem nestingSeparator, czyli "." w hello powyżej przykłady. Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli. |Nie |

**DocumentDbCollectionSink** obsługuje hello następujące właściwości:

| **Właściwość** | **Opis** | **Dozwolone wartości** | **Wymagane** |
| --- | --- | --- | --- |
| nestingSeparator |Wymagany jest znak specjalny w tooindicate nazwa kolumny źródła hello, który zagnieżdżone dokumentu. <br/><br/>Na przykład powyżej: `Name.First` w danych wyjściowych hello tabeli tworzy hello następującej strukturze JSON w dokumencie DB rozwiązania Cosmos hello:<br/><br/>"Nazwa": {<br/>    "Pierwszy": "Jan"<br/>}, |Znak, który jest używany tooseparate poziomów zagnieżdżenia.<br/><br/>Wartość domyślna to `.` (kropką). |Znak, który jest używany tooseparate poziomów zagnieżdżenia. <br/><br/>Wartość domyślna to `.` (kropką). |
| writeBatchSize |Liczba równoległe żądań tooAzure DB rozwiązania Cosmos usługi toocreate dokumentów.<br/><br/>Aby precyzyjnie zdefiniować hello wydajności podczas kopiowania danych z bazy danych usługi rozwiązania Cosmos przy użyciu tej właściwości. Wraz ze zwiększeniem writeBatchSize, ponieważ więcej tooCosmos równoległych żądań bazy danych są wysyłane, może spodziewać się lepszą wydajność. Jednak potrzebny tooavoid ograniczania przepustowości, który może zgłaszać komunikat o błędzie hello: "jest duża szybkość żądania".<br/><br/>Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Operacje kopiowania, można użyć lepsze hello toohave kolekcji (np. S3) większości dostępna przepustowość (2500 żądań jednostek na sekundę). |Liczba całkowita |Nie (domyślne: 5) |
| writeBatchTimeout |Czas toocomplete operacji hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |

## <a name="importexport-json-documents"></a>Dokumentów JSON Import/Eksport
Korzystając z tego łącznika DB rozwiązania Cosmos, można łatwo

* Zaimportuj dokumentów JSON z różnych źródeł do rozwiązania Cosmos bazy danych, w tym obiektów Blob platformy Azure, usługa Azure Data Lake, lokalnego systemu plików lub innych magazynów opartych na plikach obsługiwane przez usługi fabryka danych Azure.
* Wyeksportuj dokumentów JSON z collecton rozwiązania Cosmos bazy danych do różnych magazynów opartych na plikach.
* Migrowanie danych między dwoma kolekcje DB rozwiązania Cosmos w postaci — jest.

Skopiuj takiego schematu niezależny od tooachieve 
* Korzystając z Kreatora kopiowania, sprawdź hello **"wyeksportować w postaci — jest tooJSON plików lub rozwiązania Cosmos bazy danych kolekcji"** opcji.
* Gdy edycję JSON, nie należy określać sekcji "structure" hello w opublikowanych DB rozwiązania Cosmos ani właściwości "nestingSeparator" dla bazy danych rozwiązania Cosmos źródło/ujście w przypadku działania kopiowania. tooimport z / tooJSON pliki eksportu, hello pliku magazynu danych należy określić typ formatu jako "JsonFormat", "filePattern" config i Pomiń hello rest format ustawień, zobacz [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format) sekcji Szczegóły.

## <a name="json-examples"></a>Przykłady JSON
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z bazy danych Azure rozwiązania Cosmos i magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** za pomocą dowolnego hello tooany źródeł z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Przykład: Kopiowanie danych z bazy danych Azure rozwiązania Cosmos tooAzure obiektów Blob
Poniższy przykład Hello zawiera:

1. Połączonej usługi typu [DocumentDb](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [DocumentDbCollectionSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane w tooAzure bazy danych rozwiązania Cosmos Azure Blob. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Azure DB rozwiązania Cosmos połączonej usługi:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Magazyn obiektów Blob Azure połączonej usługi:**

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
**Azure DB dokument wejściowy zestaw danych:**

Przykładowe Hello zakłada istnieje kolekcja o nazwie **osoby** w bazie danych bazy danych Azure rozwiązania Cosmos.

Ustawienie "external": "true" i określenie externalData informacje o zasadach hello fabryki danych Azure Usługa tabeli hello zewnętrznych toohello fabryki danych i nie są produkowane przez działanie w fabryce danych hello.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Azure Blob wyjściowy zestaw danych:**

Dane są skopiowanych tooa nowego obiektu blob co godzinę o ścieżce hello obiektu blob hello odzwierciedlające hello określonej daty/godziny z szczegółowości godzinę.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Przykładowy dokument JSON w hello osoby kolekcji w bazie danych DB rozwiązania Cosmos:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Rozwiązania cosmos bazy danych obsługuje tworzenie zapytań dla dokumentów przy użyciu składni SQL przez hierarchiczna dokumentów JSON.

Przykład: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

następujące Hello potoku kopie danych z hello kolekcji osoby w hello Azure DB rozwiązania Cosmos tooan bazy danych obiektów blob platformy Azure. W ramach hello działania kopiowania hello określono wejściowych i wyjściowych zestawów danych.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure DB rozwiązania Cosmos 
Poniższy przykład Hello zawiera:

1. Połączonej usługi typu [DocumentDb](#azure-documentdb-linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

przykład Witaj kopiuje dane z tooAzure obiektów blob platformy Azure DB rozwiązania Cosmos. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Magazyn obiektów Blob Azure połączonej usługi:**

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
**Azure DB rozwiązania Cosmos połączonej usługi:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure wejściowego zestawu danych obiektów Blob:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Azure DB rozwiązania Cosmos wyjściowy zestaw danych:**

przykład Witaj kopiuje kolekcję tooa danych o nazwie "Osoba".

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
następujące Hello potoku kopie danych z obiektu Blob Azure toohello kolekcji osoby w hello DB rozwiązania Cosmos. W ramach hello działania kopiowania hello określono wejściowych i wyjściowych zestawów danych.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Jeśli hello przykładowe dane wejściowe obiektu blob jest jako

```
1,John,,Doe
```
Następnie będzie hello dane wyjściowe JSON do rozwiązania Cosmos bazy danych jako:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone. Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem **nestingSeparator**, czyli "." w tym przykładzie. Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli.

## <a name="appendix"></a>Dodatek
1. **Pytanie:** hello aktualizacja obsługi działania kopiowania istniejących rekordów?

    **Odpowiedź:** nie.
2. **Pytanie:** jak ponowną próbę kopiowania tooAzure DB rozwiązania Cosmos dotyczą już skopiowane rekordy?

    **Odpowiedź:** Jeśli rekordy ma pole "ID" i operacji kopiowania hello próbuje tooinsert rekord z hello sam identyfikator operacji kopiowania hello zgłasza błąd.  
3. **Pytanie:** fabryki danych obsługuje [zakres lub partycjonowanie danych opartych na skrót](../documentdb/documentdb-partition-data.md)?

    **Odpowiedź:** nie.
4. **Pytanie:** można określić więcej niż jednej bazy danych Azure rozwiązania Cosmos kolekcji dla tabeli?

    **Odpowiedź:** nie. W tym momencie można określić tylko jedną kolekcję.

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
