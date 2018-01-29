---
title: "Kopiowanie danych do/z usługi Azure SQL Data Warehouse przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z magazynów obsługiwanych źródłowych do usługi Azure SQL Data Warehouse (lub) z magazynu danych SQL sklepów zbiornika obsługiwane przy użyciu fabryki danych."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: jingwang
ms.openlocfilehash: 9360c0ee90f9a4ffdffd7649505699f656833bbe
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-to-or-from-azure-sql-data-warehouse-by-using-azure-data-factory"></a>Kopiowanie danych do i z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-azure-sql-data-warehouse-connector.md)
> * [Wersja 2 — wersja zapoznawcza](connector-azure-sql-data-warehouse.md)

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane do i z usługi Azure SQL Data Warehouse. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [łącznika usługi Azure SQL Data Warehouse w wersji 1](v1/data-factory-azure-sql-data-warehouse-connector.md).

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Kopiowanie danych z/do usługi Azure SQL Data Warehouse żadnych obsługiwanych ujścia magazynu danych lub skopiować dane z dowolnego źródła obsługiwanych magazynu danych do usługi Azure SQL Data Warehouse. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

W szczególności ten łącznik usługi Azure SQL Data Warehouse obsługuje:

- Kopiowanie danych przy użyciu uwierzytelniania SQL.
- Jako źródło pobierania danych przy użyciu zapytania SQL lub procedurę składowaną.
- Jako zbiornika, ładowanie danych przy użyciu **PolyBase** lub wstawiania zbiorczego. Jest **zalecane** w celu poprawy wydajności kopii.

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do łącznika usługi Azure SQL Data Warehouse.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Obsługiwane są następujące właściwości dla usługi Azure SQL Data Warehouse połączone:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **AzureSqlDW** | Yes |
| Parametry połączenia |Podaj informacje wymagane do połączenia z wystąpieniem usługi Azure SQL Data Warehouse właściwości connectionString. Obsługiwane jest tylko uwierzytelnianie podstawowe. Zaznacz to pole jako SecureString. |Yes |
| connectVia | [Integrację środowiska uruchomieniowego](concepts-integration-runtime.md) ma być używany do nawiązania połączenia z magazynem danych. (Jeśli w magazynie danych znajduje się w sieci prywatnej), można użyć środowiska uruchomieniowego integracji Azure lub Self-hosted integracji w czasie wykonywania. Jeśli nie zostanie określony, używa domyślnej środowiska uruchomieniowego integracji Azure. |Nie |


> [!IMPORTANT]
> Skonfiguruj [zapory magazynu danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) i serwer bazy danych do [Zezwalaj usługom Azure na dostęp do serwera](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ponadto jeśli kopiujesz danych Azure SQL Data Warehouse z poza tym Azure z lokalnych źródeł danych ze środowiskiem uruchomieniowym integracji Self-hosted skonfigurować odpowiedni zakres adresów IP dla komputera, który wysyła dane do danych SQL Azure Magazyn.

**Przykład:**

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje zobacz artykuł zestawów danych. Ta sekcja zawiera listę właściwości obsługiwanych przez zestaw danych Azure SQL Data Warehouse.

Aby skopiować dane z i do usługi Azure SQL Data Warehouse, ustaw właściwość Typ zestawu danych do **AzureSqlDWTable**. Obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type zestawu danych: **AzureSqlDWTable** | Yes |
| tableName |Nazwa tabeli lub widoku w wystąpieniu usługi Azure SQL Data Warehouse, odnoszący się do połączonej usługi. | Yes |

**Przykład:**

```json
{
    "name": "AzureSQLDWDataset",
    "properties":
    {
        "type": "AzureSqlDWTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Data Warehouse linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez Magazyn danych SQL Azure źródłowy i odbiorczy właściwości.

### <a name="azure-sql-data-warehouse-as-source"></a>Usługa Azure SQL Data Warehouse jako źródło

Aby skopiować dane z usługi Azure SQL Data Warehouse, należy ustawić typ źródła w przypadku działania kopiowania do **SqlDWSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **SqlDWSource** | Yes |
| sqlReaderQuery |Użyj niestandardowych zapytania SQL można odczytać danych. Przykład: `select * from MyTable`. |Nie |
| sqlReaderStoredProcedureName |Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej. Ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze składowanej. |Nie |
| storedProcedureParameters |Parametry dla procedury składowanej.<br/>Dozwolone wartości to: par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej. |Nie |

**Informacje, które należy zwrócić uwagę:**

- Jeśli **sqlReaderQuery** określono dla SqlSource, odbywa się działanie kopii tego zapytania względem źródła magazynu danych SQL Azure umożliwiają pobieranie danych. Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).
- Jeśli nie określisz "sqlReaderQuery" lub "sqlReaderStoredProcedureName" kolumn określona w sekcji "structure" zestawu danych JSON służą do utworzenia kwerendy (`select column1, column2 from mytable`) w celu uruchomienia usługi Azure SQL Data Warehouse. Jeśli definicji zestawu danych nie ma "structure", wszystkie kolumny są wybierane w tabeli.
- Jeśli używasz **sqlReaderStoredProcedureName**, nadal należy określić manekina **tableName** właściwość w zestawie danych JSON.

**Przykład: przy użyciu zapytania SQL**

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL DW input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlDWSource",
                "sqlReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

**Przykład: przy użyciu procedury składowanej**

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL DW input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlDWSource",
                "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
                "storedProcedureParameters": {
                    "stringData": { "value": "str3" },
                    "identifier": { "value": "$$Text.Format('{0:yyyy}', <datetime parameter>)", "type": "Int"}
                }
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

**Definicja procedury składowanej:**

```sql
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

### <a name="azure-sql-data-warehouse-as-sink"></a>Usługa Azure SQL Data Warehouse jako obiekt sink

Aby skopiować dane do usługi Azure SQL Data Warehouse, należy ustawić typ ujścia w działaniu kopiowania do **SqlDWSink**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **zbiornika** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość typu sink działania kopiowania: **SqlDWSink** | Yes |
| allowPolyBase |Wskazuje, czy do użycia zamiast mechanizmu BULKINSERT PolyBase (jeśli jest to wymagane). <br/><br/> **Przy użyciu programu PolyBase jest zalecanym sposobem ładowanie danych do usługi SQL Data Warehouse.** Zobacz [Użyj programu PolyBase, aby załadować dane do usługi Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcji dla ograniczenia i szczegółów.<br/><br/>Dozwolone wartości to: **True** (ustawienie domyślne) i **False**.  |Nie |
| Usługi |Grupy właściwości, które można określić, kiedy **allowPolybase** właściwość jest ustawiona na **true**. |Nie |
| rejectValue |Określa liczbę lub odsetek wierszy, które można odrzucić przed zapytanie nie powiedzie się.<br/><br/>Dowiedz się więcej o opcjach Odrzuć PolyBase **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu. <br/><br/>Dozwolone wartości to: 0 (domyślnie), 1, 2,... |Nie |
| dla właściwości rejectType |Określa, czy opcja rejectValue jest określona jako wartość literału lub wartość procentowa.<br/><br/>Dozwolone wartości to: **wartość** (ustawienie domyślne) i **procent**. |Nie |
| rejectSampleValue |Określa liczbę wierszy do pobrania przed PolyBase ponownie oblicza procent odrzuconych wierszy.<br/><br/>Dozwolone wartości to: 1, 2,... |Tak, jeśli **dla właściwości rejectType** jest **procent** |
| useTypeDefault |Określa sposób obsługi brakujących wartości w rozdzielane pliki tekstowe, jeśli PolyBase pobiera dane z pliku tekstowego.<br/><br/>Dowiedz się więcej o tej właściwości z sekcji argumenty w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).<br/><br/>Dozwolone wartości to: **True**, **False** (ustawienie domyślne). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu. Ma zastosowanie tylko wtedy, gdy aparat PolyBase nie jest używany.<br/><br/>Dozwolone wartości to: liczba całkowita (liczba wierszy). |Nie (domyślna to 10 000) |
| writeBatchTimeout |Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania. Ma zastosowanie tylko wtedy, gdy aparat PolyBase nie jest używany.<br/><br/>Dozwolone wartości to: timespan. Przykład: "00: 30:00" (30 minut). |Nie |
| preCopyScript |Określ zapytanie SQL dla aktywności kopiowania do wykonania przed zapisaniem danych do usługi Azure SQL Data Warehouse w każdym przebiegu. Ta właściwość służy do oczyszczania danych wstępnie załadowane. |Nie |(#repeatability podczas kopiowania). |Instrukcja zapytania. |Nie |

**Przykład:**

```json
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

Dowiedz się więcej na temat korzystania z programu PolyBase do załadowania do usługi SQL Data Warehouse wydajnie z następnej sekcji.

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a>Użyj programu PolyBase, aby załadować dane do magazynu danych SQL Azure

Przy użyciu  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  jest wydajny sposób ładowania dużych ilości danych do magazynu danych SQL Azure z wysokiej przepływności. Przy użyciu programu PolyBase zamiast domyślnego mechanizmu BULKINSERT widać duże korzyści w przepływności. Zobacz [skopiuj numer odwołania wydajności](copy-activity-performance.md#performance-reference) z szczegółowe porównanie. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](connector-azure-sql-data-warehouse.md).

* Jeśli źródło danych jest w **obiektów Blob platformy Azure lub usługi Azure Data Lake Store**i format jest zgodny z PolyBase, można skopiować bezpośrednio do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase. Zobacz  **[bezpośrednich kopii przy użyciu programu PolyBase](#direct-copy-using-polybase)**  ze szczegółami.
* Jeśli Twoje źródła magazynu danych i format nie jest początkowo obsługiwana przez aparat PolyBase, możesz użyć  **[przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase)**  funkcji zamiast tego. Udostępnia również możesz lepszą przepustowość automatycznie konwersji danych do formatu zgodnego PolyBase i przechowywanie danych w magazynie obiektów Blob platformy Azure. Następnie ładuje dane do usługi SQL Data Warehouse.

### <a name="direct-copy-using-polybase"></a>Bezpośrednie kopiowania przy użyciu programu PolyBase

Aparat PolyBase magazynu danych SQL obsługuje bezpośrednio obiektów Blob platformy Azure i usługi Azure Data Lake Store (przy użyciu nazwy głównej usługi) jako źródło i wymagania format określonego pliku. Jeśli źródło danych spełnia kryteria opisane w tej sekcji, możesz bezpośrednio skopiować z magazynu danych źródła do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase. W przeciwnym razie można użyć [przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase).

> [!TIP]
> Aby skopiować dane z usługi Data Lake Store SQL Data Warehouse wydajnie, Dowiedz się więcej o [fabryki danych Azure ułatwia nawet wygodny do ujawniania wgląd w dane dotyczące danych podczas korzystania z usługi Data Lake Store z usługi SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Jeśli nie zostały spełnione wymagania, fabryki danych Azure sprawdza ustawienia i automatycznie powraca do mechanizmu BULKINSERT przenoszenia danych.

1. **Źródło połączona usługa** jest typu: **AzureStorage** lub **AzureDataLakeStore**.
2. **Wejściowy zestaw danych** jest typu: **AzureBlob** lub **AzureDataLakeStoreFile**i wpisz w formacie `type` właściwości **OrcFormat** , **ParquetFormat**, lub **TextFormat** z następujących konfiguracji:

   1. `rowDelimiter`musi być  **\n** .
   2. `nullValue`ustawiono **pusty ciąg** (""), lub `treatEmptyAsNull` ustawiono **true**.
   3. `encodingName`ustawiono **utf-8**, która jest **domyślne** wartość.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader`, i `skipLineCount` nie zostały określone.
   5. `compression`może być **bez kompresji**, **GZip**, lub **Deflate**.

    ```json
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

3. Brak nie `skipHeaderLineCount` w obszarze **BlobSource** lub **AzureDataLakeStore** dla działania kopiowania w potoku.
4. Brak nie `sliceIdentifierColumnName` w obszarze **SqlDWSink** dla działania kopiowania w potoku. (PolyBase gwarantuje, że wszystkie dane są aktualizowane lub nic nie jest aktualizowana w jednym przebiegu. Aby osiągnąć **powtarzalności**, można użyć `sqlWriterCleanupScript`).

```json
"activities":[
    {
        "name": "CopyFromAzureBlobToSQLDataWarehouseViaPolyBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "BlobDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "AzureSQLDWDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "SqlDWSink",
                "allowPolyBase": true
            }
        }
    }
]
```

### <a name="staged-copy-using-polybase"></a>Kopiuj przygotowanego przy użyciu programu PolyBase

Źródło danych nie spełnia kryteriów wprowadzone w poprzedniej sekcji, umożliwia kopiowanie danych za pośrednictwem tymczasowego przemieszczania magazynu obiektów Blob Azure (nie może być magazyn w warstwie Premium). W takim przypadku fabryki danych Azure automatycznie wykonuje przekształcenia danych spełnia wymagania dotyczące formatu danych PolyBase, a następnie użyj programu PolyBase, aby załadować dane do usługi SQL Data Warehouse i następnie wyczyść tymczasowego danych z magazynu obiektów Blob. Zobacz [przemieszczane kopiowania](copy-activity-performance.md#staged-copy) szczegółowe informacje na temat jak kopiowanie danych za pośrednictwem tymczasowych obiektów Blob platformy Azure działa na ogół.

Aby użyć tej funkcji, należy utworzyć [połączonej usługi magazynu Azure](connector-azure-blob-storage.md#linked-service-properties) odwołujący się do konta magazynu Azure, które ma magazynu tymczasowego obiektu blob, następnie określ `enableStaging` i `stagingSettings` właściwości dla działania kopiowania, jak pokazano w poniższym kodzie:

```json
"activities":[
    {
        "name": "CopyFromSQLServerToSQLDataWarehouseViaPolyBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "SQLServerDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "AzureSQLDWDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
            },
            "sink": {
                "type": "SqlDWSink",
                "allowPolyBase": true
            },
            "enableStaging": true,
            "stagingSettings": {
                "linkedServiceName": {
                    "referenceName": "MyStagingBlob",
                    "type": "LinkedServiceReference"
                }
            }
        }
    }
]
```

## <a name="best-practices-when-using-polybase"></a>Najlepsze rozwiązania w sytuacji, gdy przy użyciu programu PolyBase

Poniższe sekcje zawierają dodatkowe wskazówki te, które są wymienione w [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Uprawnienia wymagane bazy danych

Aby użyć programu PolyBase, wymaga użytkownika używane do ładowania danych do usługi SQL Data Warehouse [uprawnienia "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) w docelowej bazie danych. Jest jednym ze sposobów osiągnięcia, które można dodać tego użytkownika jako członka roli "db_owner". Dowiedz się, jak to zrobić, postępując [w tej sekcji](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Rozmiar wiersza i danych typu ograniczenia

Program Polybase obciążenia są ograniczone do ładowania wierszy, zarówno mniejszy niż **1 MB** i nie można załadować VARCHR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX). Zapoznaj się [tutaj](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Jeśli masz dane źródłowe z wierszami o rozmiarze większym niż 1 MB, można podzielić tabel źródłowych w pionie na kilka małych sieci, gdy największy rozmiar wiersza dla każdego z nich nie przekracza limit. Mniejsze tabele następnie można załadować przy użyciu programu PolyBase i scalane w usłudze Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>Klasa zasobów magazynu danych SQL

Aby uzyskać najlepsze możliwe przepływności, należy wziąć pod uwagę można przypisać większą klasa zasobów do użytkownika używane do ładowania danych do usługi SQL Data Warehouse przy użyciu programu PolyBase. Dowiedz się, jak to zrobić, postępując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName w magazynie danych SQL Azure

Poniższa tabela zawiera przykłady dotyczące sposobu określania **tableName** właściwość w zestawie danych JSON dla różnych kombinacji nazwy schematu i tabeli.

| Schemat bazy danych | Nazwa tabeli | Właściwość tableName JSON |
| --- | --- | --- |
| właściciel bazy danych |MyTable |MyTable lub dbo. MyTable lub [dbo]. [MyTable] |
| dbo1 |MyTable |dbo1. MyTable lub [dbo1]. [MyTable] |
| właściciel bazy danych |My.Table |[My.Table] lub [dbo]. [My.Table] |
| dbo1 |My.Table |[dbo1]. [My.Table] |

Jeśli zostanie wyświetlony następujący błąd, może to być problem z wartość określona dla właściwości tableName. Poniższa tabela dla poprawne sposobu na określenie wartości dla właściwości tableName JSON.

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Kolumn z wartościami domyślnymi

Obecnie funkcja PolyBase w fabryce danych akceptuje tylko taką samą liczbę kolumn w tabeli docelowej. Przykład tabeli z kolumnami cztery i jeden z nich jest zdefiniowana z wartością domyślną. Dane wejściowe nadal powinien zawierać cztery kolumny. Udostępnia zestaw danych wejściowych 3 kolumny spowoduje uzyskanie błąd podobny do następującego:

```
All columns of the table must be specified in the INSERT BULK statement.
```

Wartość NULL jest specjalny rodzaj wartości domyślnej. W przypadku wartości Null kolumny danych wejściowych (w obiekcie blob) dla tej kolumny może być pusta (nie może być brakuje wejściowy zestaw danych). Program PolyBase wstawia wartość NULL w przypadku ich w magazynie danych SQL Azure.

## <a name="data-type-mapping-for-azure-sql-data-warehouse"></a>Mapowanie typu danych dla usługi Azure SQL Data Warehouse

Podczas kopiowania danych z/na magazyn danych SQL Azure, z typów danych Azure SQL Data Warehouse są używane następujące mapowania do typów danych tymczasowych fabryki danych Azure. Zobacz [schemat i dane typu mapowania](copy-activity-schema-and-type-mapping.md) Aby poznać sposób działania kopiowania mapowania typu źródłowego: schemat i dane sink.

| Typ danych w usłudze Azure SQL Data Warehouse | Typ danych tymczasowych fabryki danych |
|:--- |:--- |
| bigint |Int64 |
| Binarne |Byte] |
| bitowe |Wartość logiczna |
| char |Ciąg, Char] |
| data |Data/godzina |
| Data/godzina |Data/godzina |
| datetime2 |Data/godzina |
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
| rzeczywiste |Kawaler/panna |
| ROWVERSION |Byte] |
| smalldatetime |Data/godzina |
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

## <a name="next-steps"></a>Kolejne kroki
Lista magazynów danych obsługiwane jako źródła i wychwytywanie przez działanie kopiowania w fabryce danych Azure, zobacz [obsługiwane magazyny danych](copy-activity-overview.md##supported-data-stores-and-formats).