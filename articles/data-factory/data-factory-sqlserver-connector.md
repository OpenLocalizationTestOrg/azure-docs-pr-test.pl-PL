---
title: aaaMove tooand danych z programu SQL Server | Dokumentacja firmy Microsoft
description: "Więcej informacji dotyczących sposobu toomove danych do/z programu SQL Server bazy danych to znaczy lokalnej lub w maszynie Wirtualnej platformy Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Przenieś tooand danych z programu SQL Server — lokalnie lub na IaaS (Azure VM) przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych programu SQL Server. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania. 

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z bazy danych programu SQL Server** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **bazy danych programu SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Obsługiwane wersje programu SQL Server
Ta obsługa łącznika programu SQL Server kopiowania danych z / toohello po wersji wystąpienia obsługiwana lokalnie lub w IaaS platformy Azure przy użyciu zarówno uwierzytelnianie SQL i uwierzytelnianie systemu Windows: SQL Server 2016, programu SQL Server 2014, programu SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Włączenie łączności
są tego samego hello Hello pojęcia i kroki niezbędne do łączenia z programu SQL Server obsługiwana lokalnie lub w usłudze Azure IaaS (infrastruktury jako — usługa), maszynach wirtualnych. W obu przypadkach należy toouse brama zarządzania danymi dla połączenia.

Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello. Konfigurowanie wystąpienia bramy jest jako warunek wstępny dla łączenia z programem SQL Server.

Podczas instalowania bramy na powitania sam lokalnymi wystąpienia maszyny Wirtualnej maszynie lub w chmurze hello programu SQL Server w celu zapewnienia lepszej wydajności, zaleca się, zainstaluj je na oddzielnych komputerach. Taki hello bramy i serwera SQL na oddzielnych komputerach zmniejsza rywalizacji.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych programu SQL Server przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z tooan bazy danych programu SQL Server magazynu obiektów blob platformy Azure, utworzysz dwa toolink połączonej usługi bazy danych programu SQL Server i fabryki danych tooyour konta magazynu Azure. Dla właściwości połączonej usługi, które są określone tooSQL bazy danych serwera, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 
3. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. W przykładzie hello wymienionych w ostatnim kroku hello utworzeniu tabeli SQL hello toospecify zestawu danych w bazie danych programu SQL Server zawiera hello danych wejściowych. Utwórz innego kontenera obiektów blob hello toospecify zestawu danych i folderu hello, która przechowuje dane hello skopiowanych z hello bazy danych programu SQL Server. Dla właściwości zestawu danych, które są określone tooSQL bazy danych serwera, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
4. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa SqlSource jako źródło i BlobSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z magazynu obiektów Blob Azure tooSQL bazy danych serwera, należy użyć BlobSource i SqlSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooSQL bazy danych serwera, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z lokalną bazą danych programu SQL Server, zobacz [przykłady JSON](#json-examples-for-copying-data-from-and-to-sql-server) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooSQL serwera: 

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne. Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.

Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**. |Tak |
| Parametry połączenia |Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows. |Tak |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows. Przykład: **domainname\\username**. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |

Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Przykłady
**JSON dla przy użyciu uwierzytelniania programu SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON dla przy użyciu uwierzytelniania systemu Windows**

Brama zarządzania danymi zostanie personifikacji hello określony tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
W próbkach hello użyto zestawu danych typu **SqlServerTable** toorepresent tabeli w bazie danych programu SQL Server.  

Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów zestawu danych (SQL Server, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj **typeProperties** sekcja dla zestawu danych hello typu **SqlServerTable** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Server hello, która jest połączona usługa odnosi się do. |Tak |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Chcesz przenieść dane z bazy danych programu SQL Server, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**SqlSource**. Podobnie jeśli przenosisz bazę danych programu SQL Server tooa danych ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**SqlSink**. Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.

Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

> [!NOTE]
> Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

### <a name="sqlsource"></a>SqlSource
Gdy źródło w działaniu kopiowania jest typu **SqlSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: Wybierz * z MyTable. Może odwoływać się wiele tabel z bazy danych hello odwołuje się hello wejściowy zestaw danych. Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz z MyTable. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania hello bazy danych SQL Server źródła tooget hello danych.

Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

> [!NOTE]
> Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON. Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.

### <a name="sqlsink"></a>SqlSink
**SqlSink** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji. |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji. |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |
| sqlWriterStoredProcedureName |Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |
| sqlWriterTableType |Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane. Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli. Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi. |Nazwa typu tabeli. |Nie |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Przykłady JSON do kopiowania danych z tooSQL serwera
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Witaj, jak następujące przykłady Pokaż toocopy tooand danych z programu SQL Server i magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Przykład: Kopiowanie danych z programu SQL Server tooAzure obiektów Blob
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych, z programu SQL Server tooan tabeli obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem konfiguracji bramy zarządzania danymi hello. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**Usługi SQL Server połączone**
```json
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
**Azure Blob połączoną usługą magazynu**

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
**Wejściowy zestaw danych programu SQL Server**

przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w programie SQL Server i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych. Umożliwia wysyłanie zapytań przez wiele tabel w ramach tej samej bazy danych za pomocą jednego zestawu danych, ale pojedynczej tabeli muszą być używane do hello dataset tableName typeProperty powitalne.

Ustawienie "external": "prawda" informuje usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
  "name": "SqlServerInput",
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
**Azure Blob wyjściowy zestaw danych**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

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
**W potoku z działanie kopiowania**

potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
W tym przykładzie **sqlReaderQuery** dla hello SqlSource został określony. Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello danych hello tooget źródła danych programu SQL Server. Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry). Hello sqlReaderQuery można odwoływać się wiele tabel w bazie danych hello odwołuje się hello wejściowy zestaw danych. Nie jest tabelą hello ograniczone tooonly ustawione jako hello typeProperty tableName zestawu danych.

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

Zobacz hello [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSource i BlobSink właściwości.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Przykład: Kopiowanie danych z obiektu Blob Azure tooSQL serwera
następujące przykładowe pokazuje Hello:

1. Witaj połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).
2. Witaj połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#sql-server-copy-activity-type-properties).

Przykładowe Hello kopiuje dane szeregów czasowych, z tabeli programu SQL Server tooa obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Usługi SQL Server połączone**

```json
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
**Azure Blob połączoną usługą magazynu**

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
**Azure wejściowego zestawu danych obiektów Blob**

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": "prawda" ustawienie informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
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
**Zestaw danych wyjściowych programu SQL Server**

przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w programie SQL Server. Utwórz tabelę hello w programie SQL Server z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**W potoku z działanie kopiowania**

potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.

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
            "name": " SqlServerOutput "
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

## <a name="troubleshooting-connection-issues"></a>Rozwiązywanie problemów z połączeniem
1. Konfigurowanie połączeń zdalnych tooaccept programu SQL Server. Uruchom **programu SQL Server Management Studio**, kliknij prawym przyciskiem myszy **serwera**i kliknij przycisk **właściwości**. Wybierz **połączeń** z listy hello i wyboru **Zezwalaj na połączenia zdalne toohello serwera**.

    ![Włącz połączenia zdalne](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Zobacz [konfigurowania dostępu zdalnego hello opcji konfiguracji serwera](https://msdn.microsoft.com/library/ms191464.aspx) szczegółowy opis kroków.
2. Uruchom **programu SQL Server Configuration Manager**. Rozwiń węzeł **konfigurację sieci programu SQL Server** dla hello wystąpienia możesz chcieć, a następnie wybierz **protokoły dla elementu MSSQLSERVER**. Protokoły w prawym okienku hello powinna zostać wyświetlona. Włącz protokół TCP/IP, klikając prawym przyciskiem myszy **TCP/IP** i klikając **włączyć**.

    ![Włącz protokół TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Zobacz [włączyć lub wyłączyć protokół sieciowy serwera](https://msdn.microsoft.com/library/ms191294.aspx) szczegółowe informacje i alternatywny sposób włączania protokołu TCP/IP.
3. W tym samym oknie Witaj, kliknij dwukrotnie **TCP/IP** toolaunch **właściwości protokołu TCP/IP** okna.
4. Przełącz toohello **adresów IP** kartę. Przewiń w dół toosee **IPWszystkie** sekcji. Zanotuj hello ** TCP Port ** (domyślnie jest **1433**).
5. Utwórz **regułę zapory systemu Windows hello** na ruch przychodzący tooallow maszyny hello za pośrednictwem tego portu.  
6. **Sprawdź połączenie**: tooconnect toohello SQL Server przy użyciu w pełni kwalifikowana nazwa, użyj programu SQL Server Management Studio z innego komputera. Na przykład: "<machine>.<domain>. Corp.<company>.com, 1433. "

   > [!IMPORTANT]

   > Zobacz [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) Aby uzyskać szczegółowe informacje.
   >
   > Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Kolumny tożsamości w hello docelowej bazy danych
Ta sekcja zawiera przykład, w którym kopiuje dane z tabeli źródłowej z nie tożsamości tooa docelowej tabeli z kolumny tożsamości.

**Tabela źródłowa:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabela docelowa:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Należy zauważyć, że tabela docelowa hello ma kolumny tożsamości.

**Źródło zestawu danych JSON definicji**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
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

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
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
Zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykule przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku.

## <a name="type-mapping-for-sql-server"></a>Mapowanie typu dla programu SQL server
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, hello działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych za & z programu SQL server hello następujące mapowania są używane z too.NET typu SQL i odwrotnie.

Mapowanie Hello jest taki sam jak hello mapowanie typu danych serwera SQL dla ADO.NET.

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

## <a name="mapping-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Kopiuj powtarzalne
Podczas kopiowania danych tooSQL bazy danych serwera, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie. Zamiast tego zobacz tooperform UPSERT [tooSqlSink powtarzalne zapisu](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu. 

Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
