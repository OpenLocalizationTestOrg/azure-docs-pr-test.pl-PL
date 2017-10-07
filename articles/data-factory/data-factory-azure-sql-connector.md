---
title: aaaCopy danych do/z bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocopy danych do/z bazy danych SQL Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Skopiuj tooand danych z bazy danych SQL Azure przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych tooand z bazy danych SQL Azure. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.  

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z bazy danych SQL Azure** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **tooAzure bazy danych SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Obsługiwany typ uwierzytelniania
Łącznik bazy danych SQL Azure obsługuje uwierzytelnianie podstawowe.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych SQL Azure za pomocą różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. Dla właściwości połączonej usługi, które są określone tooAzure bazy danych SQL, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 
3. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych. I utwórz inny zestaw danych toospecify hello tabeli SQL w bazie danych Azure SQL hello przechowujący dane hello skopiowane z magazynu obiektów blob hello. Dla właściwości zestawu danych, które są określone tooAzure usługi Data Lake Store, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
4. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z bazy danych SQL Azure tooAzure magazynu obiektów Blob, należy użyć SqlSource i BlobSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooAzure bazy danych SQL, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z bazy danych SQL Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-database) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure bazy danych SQL: 

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Azure SQL połączone łącza usługi fabryka danych tooyour bazy danych Azure SQL. Witaj w poniższej tabeli zawiera opis JSON elementy określonych tooAzure SQL połączonej usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **AzureSqlDatabase** |Tak |
| Parametry połączenia |Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString. Obsługiwane jest tylko uwierzytelnianie podstawowe. |Tak |

> [!IMPORTANT]
> Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello serwera bazy danych za[Zezwól serwerowi hello tooaccess usług Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ponadto jeśli kopiujesz tooAzure danych bazy danych SQL z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla maszyny hello, który wysyła dane tooAzure bazy danych SQL.

## <a name="dataset-properties"></a>Właściwości zestawu danych
toospecify toorepresent zestawu danych wejściowych lub wyjściowych danych w bazie danych Azure SQL, ustawić właściwości typu hello hello zestawu danych, aby: **AzureSqlTable**. Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Azure SQL połączonej usługi.  

Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureSqlTable** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Azure hello, która jest połączona usługa odnosi się do. |Tak |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

> [!NOTE]
> Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.

Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Chcesz przenieść dane z bazy danych Azure SQL, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**SqlSource**. Podobnie jeśli przenosisz bazę danych Azure SQL tooan danych ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**SqlSink**. Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.

### <a name="sqlsource"></a>SqlSource
W przypadku działania kopiowania, gdy źródłem hello jest typu **SqlSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Przykład: `select * from MyTable`. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania względem hello bazy danych SQL Azure źródła tooget hello danych. Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild kwerendy (`select column1, column2 from mytable`) toorun przed hello bazy danych SQL Azure. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

> [!NOTE]
> Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON. Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.
>
>

### <a name="sqlsource-example"></a>Przykład SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**Definicja procedury przechowywane Hello:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy). |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny dla działania kopiowania toofill o identyfikatorze wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy). |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |
| sqlWriterStoredProcedureName |Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |
| sqlWriterTableType |Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane. Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli. Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi. |Nazwa typu tabeli. |Nie |

#### <a name="sqlsink-example"></a>Przykład SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Przykłady JSON do kopiowania tooand danych z bazy danych SQL
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z bazy danych SQL Azure i magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Przykład: Kopiowanie danych z bazy danych SQL Azure tooAzure obiektów Blob
Witaj sam definiuje powitania po jednostek fabryki danych:

1. Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli w obiekcie blob tooa bazy danych Azure SQL co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.  

**Baza danych SQL Azure połączonej usługi:**

```JSON
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
Zobacz hello [połączoną usługę SQL Azure](#linked-service) sekcji hello listy właściwości obsługiwanych przez tej połączonej usługi.

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
Zobacz hello [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu hello listy właściwości obsługiwanych przez tej połączonej usługi.


**Azure SQL wejściowy zestaw danych:**

przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Azure SQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.

Ustawienie "external": "prawda" informuje usługi fabryka danych Azure hello tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
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

Zobacz hello [właściwości typu zestawu danych Azure SQL](#dataset) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.  

**Azure Blob wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```JSON
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
Zobacz hello [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.  

**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```JSON
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
Przykład Witaj **sqlReaderQuery** dla hello SqlSource został określony. Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello hello tooget danymi bazy danych SQL Azure. Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild toorun zapytania względem hello bazy danych SQL Azure. Na przykład: `select column1, column2 from mytable`. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

Zobacz hello [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSource i BlobSink właściwości.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure bazy danych SQL
przykład Witaj definiuje powitania po jednostek fabryki danych:  

1. Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli tooa obiektów blob platformy Azure w bazie danych Azure SQL co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Azure połączoną usługą SQL:**

```JSON
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
Zobacz hello [połączoną usługę SQL Azure](#linked-service) sekcji hello listy właściwości obsługiwanych przez tej połączonej usługi.

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
Zobacz hello [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu hello listy właściwości obsługiwanych przez tej połączonej usługi.


**Azure wejściowego zestawu danych obiektów Blob:**

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Zobacz hello [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.

**Baza danych SQL Azure wyjściowy zestaw danych:**

przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w języku SQL Azure. Utwórz tabelę hello SQL Azure z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```JSON
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
Zobacz hello [właściwości typu zestawu danych Azure SQL](#dataset) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.

**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.

```JSON
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
            "type": "BlobSource",
            "blobColumnSeparators": ","
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
Zobacz hello [zbiornika Sql](#sqlsink) sekcji i [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSink i BlobSource właściwości.

## <a name="identity-columns-in-hello-target-database"></a>Kolumny tożsamości w hello docelowej bazy danych
Ta sekcja zawiera przykład kopiowanie danych z tabeli źródłowej bez tożsamości tooa docelowej tabeli z kolumny tożsamości.

**Tabela źródłowa:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabela docelowa:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Należy zauważyć, że tabela docelowa hello ma kolumny tożsamości.

**Źródło zestawu danych JSON definicji**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Docelowy zestaw danych JSON definicji**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością). W tym scenariuszu należy toospecify **struktury** właściwości w definicji zestawu danych docelowego hello, która nie zawiera kolumny tożsamości hello.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Wywołaj procedurę składowaną z zbiornika SQL
Na przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku, zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykułu. 

## <a name="type-mapping-for-azure-sql-database"></a>Mapowanie typu dla bazy danych SQL Azure
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia tooand danych z bazy danych SQL Azure, hello następujące mapowania są używane z too.NET typu SQL i odwrotnie. Mapowanie Hello jest taki sam jak hello mapowanie typu danych serwera SQL dla ADO.NET.

| Typ aparatu bazy danych programu SQL Server | Typ programu .NET framework |
| --- | --- |
| bigint |Int64 |
| Binarne |Byte] |
| bitowe |Wartość logiczna |
| char |Ciąg, Char] |
| Data |Data i godzina |
| Data i godzina |Data i godzina |
| datetime2 |Data i godzina |
| Datetimeoffset |DateTimeOffset |
| Decimal |Decimal |
| Atrybut FILESTREAM (varbinary(max)) |Byte] |
| Float |O podwójnej precyzji |
| Obraz |Byte] |
| int |Int32 |
| oszczędność pieniędzy |Decimal |
| nchar |Ciąg, Char] |
| ntext |Ciąg, Char] |
| numeryczne |Decimal |
| nvarchar |Ciąg, Char] |
| rzeczywiste |Pojedynczy |
| ROWVERSION |Byte] |
| smalldatetime |Data i godzina |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Obiekt * |
| Tekst |Ciąg, Char] |
| time |Zakres czasu |
| sygnatura czasowa |Byte] |
| tinyint |Bajtów |
| Unikatowy identyfikator |Identyfikator GUID |
| varbinary |Byte] |
| varchar |Ciąg, Char] |
| xml |XML |

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Kopiuj powtarzalne
Podczas kopiowania danych tooSQL bazy danych serwera, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie. Zamiast tego zobacz tooperform UPSERT [tooSqlSink powtarzalne zapisu](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu. 

Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
