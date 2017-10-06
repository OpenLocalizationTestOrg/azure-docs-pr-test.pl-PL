---
title: "aaaCopy danych do/z usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy danych do/z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Skopiuj tooand danych z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z usługą Magazyn danych SQL Azure. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.  

> [!TIP]
> tooachieve najlepszych wydajności, użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse. Witaj [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcja zawiera szczegółowe informacje. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Dane należy skopiować **z usługi Azure SQL Data Warehouse** toohello po magazynów danych:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Można skopiować danych z powitania po magazyny danych **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Podczas kopiowania danych z tooAzure serwera SQL lub bazy danych SQL Azure SQL Data Warehouse, jeśli tabela hello nie istnieje w magazynie docelowym hello, fabryki danych może automatycznie tworzyć hello tabeli w usłudze SQL Data Warehouse za pomocą schematu hello hello tabeli w źródle hello Magazyn danych. Zobacz [automatycznego tworzenia tabel](#auto-table-creation) szczegółowe informacje.

## <a name="supported-authentication-type"></a>Obsługiwany typ uwierzytelniania
Azure SQL Data Warehouse łącznika Obsługa uwierzytelniania podstawowego.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z usługi Azure SQL Data Warehouse przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potok, który kopiuje dane z usługi Azure SQL Data Warehouse jest toouse hello kopiowania danych kreatora. Zobacz [samouczek: ładowanie danych do usługi SQL Data Warehouse z fabryką danych](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać co najmniej jeden potoków. 
2. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych. Na przykład jeśli dane są kopiowane z magazynu danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour magazynu danych Azure SQL. Dla właściwości połączonej usługi, które są określone tooAzure SQL Data Warehouse, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji. 
3. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych. I utwórz inny zestaw danych toospecify hello tabeli w hello Azure SQL data warehouse przechowuje dane hello skopiowane z magazynu obiektów blob hello. Dla właściwości zestawu danych, które są określone tooAzure SQL Data Warehouse, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.
4. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlDWSink jako zbiorniku dla aktywności kopiowania hello. Podobnie są kopiowane z usługi Azure SQL Data Warehouse tooAzure magazynu obiektów Blob, należy użyć SqlDWSource i BlobSink w przypadku działania kopiowania hello. Dla właściwości działania kopiowania, które są określone tooAzure SQL Data Warehouse, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji. Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z usługi Azure SQL Data Warehouse, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure SQL Data Warehouse:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj w poniższej tabeli przedstawiono opis dla określonych tooAzure elementów JSON usługi SQL Data Warehouse połączone.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **AzureSqlDW** |Tak |
| Parametry połączenia |Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString. Obsługiwane jest tylko uwierzytelnianie podstawowe. |Tak |

> [!IMPORTANT]
> Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) i hello serwera bazy danych za[Zezwól serwerowi hello tooaccess usług Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ponadto jeśli kopiujesz tooAzure danych magazynu danych SQL z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla maszyny hello, który wysyła dane tooAzure SQL Data Warehouse.

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureSqlDWTable** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w bazie danych Azure SQL Data Warehouse hello, który hello połączonej usługi odwołuje się do. |Tak |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

> [!NOTE]
> Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

### <a name="sqldwsource"></a>SqlDWSource
Jeśli źródło jest typu **SqlDWSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: Wybierz * z MyTable. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

Jeśli hello **sqlReaderQuery** określono hello SqlDWSource, hello odbywa się działanie kopii tego zapytania względem hello Azure SQL Data Warehouse źródła tooget hello danych.

Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild toorun zapytania względem hello Azure SQL Data Warehouse. Przykład: `select column1, column2 from mytable`. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

#### <a name="sqldwsource-example"></a>Przykład SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
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

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. Aby uzyskać więcej informacji, zobacz [sekcji powtarzalności](#repeatability-during-copy). |Instrukcja zapytania. |Nie |
| allowPolyBase |Wskazuje, czy toouse PolyBase (jeśli jest to wymagane) zamiast BULKINSERT mechanizmu. <br/><br/> **Przy użyciu programu PolyBase jest hello zalecany sposób tooload danych do usługi SQL Data Warehouse.** Zobacz [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcji dla ograniczenia i szczegółów. |True <br/>Wartość FAŁSZ (ustawienie domyślne) |Nie |
| Usługi |Grupa właściwości, które można określić podczas hello **allowPolybase** właściwość jest ustawiona zbyt**true**. |&nbsp; |Nie |
| rejectValue |Określa numer hello lub procent wierszy, które można odrzucić przed hello działanie nie powiodło się. <br/><br/>Dowiedz się więcej na temat hello PolyBase Odrzuć opcje w hello **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu. |0 (domyślnie), 1, 2... |Nie |
| dla właściwości rejectType |Określa, czy opcja rejectValue hello jest określona jako wartość literału lub wartość procentowa. |Wartość (ustawienie domyślne), wartość procentowa |Nie |
| rejectSampleValue |Określa liczbę hello tooretrieve wierszy przed hello PolyBase ponownie oblicza hello procent odrzuconych wierszy. |1, 2, … |Tak, jeśli **dla właściwości rejectType** jest **procent** |
| useTypeDefault |Określa, jak toohandle brakujących wartości w rozdzielane pliki tekstowe po programie PolyBase pobiera dane z pliku tekstowego hello.<br/><br/>Dowiedz się więcej o tej właściwości z sekcji argumenty hello w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |Wartość true, False (ustawienie domyślne) |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |

#### <a name="sqldwsink-example"></a>Przykład SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Użyj programu PolyBase tooload danych do magazynu danych SQL Azure
Przy użyciu  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  jest wydajny sposób ładowania dużych ilości danych do magazynu danych SQL Azure z wysokiej przepływności. Widać duże korzyści hello przepływność przy użyciu programu PolyBase zamiast hello domyślnego mechanizmu BULKINSERT. Zobacz [skopiuj numer odwołania wydajności](data-factory-copy-activity-performance.md#performance-reference) z szczegółowe porównanie. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).

* Jeśli źródło danych jest w **obiektów Blob platformy Azure lub usługi Azure Data Lake Store**i hello format jest zgodny z PolyBase, możesz bezpośrednio skopiować tooAzure SQL Data Warehouse przy użyciu programu PolyBase. Zobacz  **[bezpośrednich kopii przy użyciu programu PolyBase](#direct-copy-using-polybase)**  ze szczegółami.
* Jeśli Twoje źródła magazynu danych i format nie jest początkowo obsługiwana przez aparat PolyBase, możesz użyć hello  **[przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase)**  funkcji zamiast tego. Udostępnia również możesz lepszą przepustowość automatycznie konwersji danych hello na format zgodny PolyBase i przechowywanie danych hello w magazynie obiektów Blob platformy Azure. Następnie ładuje dane do usługi SQL Data Warehouse.

Zestaw hello `allowPolyBase` właściwości zbyt**true** pokazane na powitania poniższy przykład dla fabryki danych Azure toouse PolyBase toocopy danych do usługi Azure SQL Data Warehouse. Po ustawieniu allowPolyBase tootrue można określić właściwości specyficzne dla programu PolyBase przy użyciu hello `polyBaseSettings` grupy właściwości. Zobacz hello [SqlDWSink](#SqlDWSink) sekcji, aby uzyskać więcej informacji o właściwościach, które mogą korzystać z usługi.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Bezpośrednie kopiowania przy użyciu programu PolyBase
Aparat PolyBase magazynu danych SQL obsługuje bezpośrednio obiektów Blob platformy Azure i usługi Azure Data Lake Store (przy użyciu nazwy głównej usługi) jako źródło i wymagania format określonego pliku. Jeśli źródło danych spełnia kryteria hello opisane w tej sekcji, możesz skopiować bezpośrednio ze źródła danych magazynu tooAzure, który SQL Data Warehouse przy użyciu programu PolyBase. W przeciwnym razie można użyć [przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase).

> [!TIP]
> toocopy dane z usługi Data Lake Store tooSQL hurtowni danych, Dowiedz się więcej o [fabryki danych Azure ułatwia nawet łatwiejsze i wygodne toouncover wgląd w dane dotyczące danych podczas korzystania z usługi Data Lake Store z usługi SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Jeśli nie są spełnione wymagania hello, fabryki danych Azure sprawdza ustawienia hello i automatycznie powraca mechanizm BULKINSERT toohello hello przenoszenia danych.

1. **Źródło połączona usługa** jest typu: **AzureStorage** lub **AzureDataLakeStore z uwierzytelnianiem główna usługi**.  
2. Witaj **wejściowy zestaw danych** jest typu: **AzureBlob** lub **AzureDataLakeStore**, i hello typ formatu w obszarze `type` właściwości **OrcFormat** , lub **TextFormat** z hello następujące konfiguracje:

   1. `rowDelimiter`musi być  **\n** .
   2. `nullValue`ustawiono zbyt**pusty ciąg** (""), lub `treatEmptyAsNull` ustawiono zbyt**true**.
   3. `encodingName`ustawiono zbyt**utf-8**, która jest **domyślne** wartość.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader`, i `skipLineCount` nie zostały określone.
   5. `compression`może być **bez kompresji**, **GZip**, lub **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Brak nie `skipHeaderLineCount` w obszarze **BlobSource** lub **AzureDataLakeStore** dla hello działanie kopiowania w potoku hello.
4. Brak nie `sliceIdentifierColumnName` w obszarze **SqlDWSink** dla hello działanie kopiowania w potoku hello. (PolyBase gwarantuje, że wszystkie dane są aktualizowane lub nic nie jest aktualizowana w jednym przebiegu. tooachieve **powtarzalności**, można użyć `sqlWriterCleanupScript`).
5. Brak nie `columnMapping` używany w hello skojarzony w przypadku działania kopiowania.

### <a name="staged-copy-using-polybase"></a>Kopiuj przygotowanego przy użyciu programu PolyBase
Źródło danych nie spełnia kryteriów hello wprowadzone w poprzedniej sekcji hello, umożliwia kopiowanie danych za pośrednictwem tymczasowego przemieszczania magazynu obiektów Blob Azure (nie może być magazyn w warstwie Premium). W takim przypadku fabryki danych Azure automatycznie wykonuje przekształcenia na powitania toomeet dane formatu wymagania dotyczące danych PolyBase, a następnie użyj programu PolyBase tooload danych do usługi SQL Data Warehouse i ostatnio oczyszczania tymczasowego danych z magazynu obiektów Blob hello. Zobacz [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) szczegółowe informacje na temat jak kopiowanie danych za pośrednictwem tymczasowych obiektów Blob platformy Azure działa na ogół.

> [!NOTE]
> Podczas kopiowania danych z danych z lokalnego magazynu do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase i przemieszczania, jeśli wersja bramy zarządzania danymi znajduje się poniżej 2.4 środowiska JRE (Java Runtime Environment) jest wymagane dla bramy komputera, który jest używany tootransform źródło danych do prawidłowego formatu. Sugerują, że uaktualnienie najnowszej bramy tooavoid w toohello tych zależności.
>

toouse tej funkcji, Utwórz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) przywołujący toohello konta magazynu Azure, które ma hello tymczasowego obiektu blob magazynu, następnie określ hello `enableStaging` i `stagingSettings` właściwości hello działanie kopiowania jak pokazano w hello następującego kodu:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Najlepsze rozwiązania w sytuacji, gdy przy użyciu programu PolyBase
Witaj poniższe sekcje zawierają dodatkowe toohello najlepsze praktyki te, które są wymienione w [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Uprawnienia wymagane bazy danych
toouse PolyBase wymaga hello użytkownika jest tooload używane dane do usługi SQL Data Warehouse ma hello [uprawnienia "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) na powitania docelowej bazy danych. Jednym ze sposobów tooachieve, który jest tooadd ten użytkownik jest członkiem roli "db_owner". Dowiedz się, jak toodo który wykonując [w tej sekcji](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Rozmiar wiersza i danych typu ograniczenia
Program Polybase obciążenia są ograniczone tooloading wierszy zarówno mniejszy niż **1 MB** i nie można załadować tooVARCHR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX). Odwołuje się zbyt[tutaj](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Jeśli masz dane źródłowe z wierszami o rozmiarze większym niż 1 MB, można tabel źródłowych hello toosplit w pionie do kilku małych sieci, gdy największy rozmiar wiersza hello każdego z nich nie przekracza hello limit. następnie można załadować tabel mniejszych Hello, przy użyciu programu PolyBase i scalane w usłudze Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>Klasa zasobów magazynu danych SQL
tooachieve najlepsze możliwe przepływności, należy wziąć pod uwagę tooassign większych zasobów klasy toohello użytkownika są używane tooload danych do usługi SQL Data Warehouse przy użyciu programu PolyBase. Dowiedz się, jak toodo który wykonując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName w magazynie danych SQL Azure
Witaj poniższej tabeli przedstawiono przykłady dotyczące toospecify hello **tableName** właściwość w zestawie danych JSON dla różnych kombinacji nazwy schematu i tabeli.

| Schemat bazy danych | Nazwa tabeli | Właściwość tableName JSON |
| --- | --- | --- |
| właściciel bazy danych |MyTable |MyTable lub dbo. MyTable lub [dbo]. [MyTable] |
| dbo1 |MyTable |dbo1. MyTable lub [dbo1]. [MyTable] |
| właściciel bazy danych |My.Table |[My.Table] lub [dbo]. [My.Table] |
| dbo1 |My.Table |[dbo1]. [My.Table] |

Jeśli zostanie wyświetlony następujący błąd hello, może to być problem z wartością hello, który został określony jako właściwość tableName hello. Zobacz tabelę hello hello prawidłowy sposób toospecify wartości dla właściwości JSON tableName hello.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Kolumn z wartościami domyślnymi
Obecnie PolyBase akceptuje tylko funkcji w fabryce danych hello taką samą liczbę kolumn w tabeli docelowej hello. Przykład tabeli z kolumnami cztery i jeden z nich jest zdefiniowana z wartością domyślną. dane wejściowe Hello nadal powinien zawierać cztery kolumny. Zapewnianie 3 kolumny zestawu danych wejściowych ważnością toohello podobne błąd następującego komunikatu:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
Wartość NULL jest specjalny rodzaj wartości domyślnej. W przypadku wartości Null kolumny hello danych wejściowych hello (w obiekcie blob) dla tej kolumny może być pusta (nie może być brakuje hello wejściowy zestaw danych). Program PolyBase wstawia wartości NULL dla nich hello Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Automatyczne tworzenie tabeli
Jeśli używasz kreatora kopiowania toocopy danych z programu SQL Server lub bazy danych SQL Azure tooAzure SQL Data Warehouse i hello tabeli, która odpowiada toohello tabela źródłowa nie istnieje w magazynie docelowym hello, fabryki danych może automatycznie tworzyć hello tabeli w hello Magazyn danych przy użyciu schematu tabeli źródłowej hello.

Fabryka danych tworzy hello tabeli w magazynie docelowym hello z hello sama nazwa w magazynie danych źródła hello tabeli. Hello typy danych kolumn są wybierane oparte na powitania po mapowania typu. W razie potrzeby wykonuje toofix konwersje typu wszelkie niezgodności między magazynami źródłowym i docelowym. Używa okrężnego tabeli dystrybucji.

| Typ kolumny źródłowej bazy danych SQL | Typ kolumny docelowej magazynu danych SQL (limit rozmiaru) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| bitowe | bitowe |
| Decimal | Decimal |
| numeryczne | Decimal |
| Float | Float |
| oszczędność pieniędzy | oszczędność pieniędzy |
| Real | Real |
| SmallMoney | SmallMoney |
| Binarne | Binarne |
| varbinary | Varbinary (up too8000) |
| Date | Date |
| Data i godzina | Data i godzina |
| DateTime2 | DateTime2 |
| Time | Time |
| DateTimeOffset | DateTimeOffset |
| SmallDateTime | SmallDateTime |
| Tekst | Varchar (up too8000) |
| NText | NVarChar (up too4000) |
| Image (Obraz) | VarBinary (up too8000) |
| Unikatowy identyfikator | Unikatowy identyfikator |
| char | char |
| NChar | NChar |
| VarChar | VarChar (up too8000) |
| NVarChar | NVarChar (up too4000) |
| XML | Varchar (up too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Mapowanie typu dla usługi Azure SQL Data Warehouse
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych za & z usługi Azure SQL Data Warehouse, hello następujące mapowania są używane z too.NET typu SQL i odwrotnie.

Mapowanie Hello jest taki sam jak hello [mapowanie typu danych serwera SQL dla ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

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

Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello. Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Przykłady JSON do kopiowania tooand danych z magazynu danych SQL
Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy tooand danych z magazynu danych SQL Azure i magazynu obiektów Blob Azure. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Przykład: Kopiowanie danych z usługi Azure SQL Data Warehouse tooAzure obiektów Blob
przykład Witaj definiuje powitania po jednostek fabryki danych:

1. Połączonej usługi typu [AzureSqlDW](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlDWSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane (co godzinę, codziennie, itp.) szeregów czasowych, z tabeli w obiekcie blob tooa bazy danych magazynu danych SQL Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Usługa Azure SQL Data Warehouse połączonej usługi:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
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
**Usługa Azure SQL Data Warehouse wejściowy zestaw danych:**

przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w magazynie danych SQL Azure i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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

**Działanie kopiowania w potoku z SqlDWSource i BlobSink:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlDWSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> Przykład Witaj **sqlReaderQuery** dla hello SqlDWSource został określony. Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello Azure SQL Data Warehouse źródła tooget hello danych.
>
> Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).
>
> Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild kwerendy (Wybierz Kolumna1, Kolumna2 z mytable) toorun przed hello Azure SQL Data Warehouse. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Przykład: Kopiowanie danych z tooAzure obiektów Blob platformy Azure SQL Data Warehouse
przykład Witaj definiuje powitania po jednostek fabryki danych:

1. Połączonej usługi typu [AzureSqlDW](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlDWSink](#copy-activity-properties).

Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli tooa obiektów blob platformy Azure w bazie danych magazynu danych SQL Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Usługa Azure SQL Data Warehouse połączonej usługi:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
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
**Azure wejściowego zestawu danych obiektów Blob:**

Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1). Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia. "external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

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
**Usługa Azure SQL Data Warehouse wyjściowy zestaw danych:**

przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w usłudze Azure SQL Data Warehouse. Utwórz tabelę hello w usłudze Azure SQL Data Warehouse przy użyciu hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello. Dodawaniu nowych wierszy tabeli toohello co godzinę.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**Działanie kopiowania w potoku z BlobSource i SqlDWSink:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
Aby uzyskać wskazówki, zobacz Zobacz hello [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md) i [ładowanie danych z fabryką danych Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artykułu w hello Azure SQL Data Warehouse dokumentacja.

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
