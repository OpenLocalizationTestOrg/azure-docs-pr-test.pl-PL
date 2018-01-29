---
title: "Kopiowanie danych do/z bazy danych SQL Azure przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z obsługiwanej źródłowej baz danych do usługi Azure SQL Database (lub) z bazy danych SQL do zbiornika obsługiwanych magazynów danych przy użyciu fabryki danych."
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
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: a0074bd68dc9714eed9064e42c6e1c6d708d1100
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-to-or-from-azure-sql-database-by-using-azure-data-factory"></a>Kopiowanie danych do lub z bazą danych SQL Azure przy użyciu fabryki danych Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-azure-sql-connector.md)
> * [Wersja 2 — wersja zapoznawcza](connector-azure-sql-database.md)

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane z i do bazy danych SQL Azure. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [łącznika usługi Azure SQL Database w wersji 1](v1/data-factory-azure-sql-connector.md).

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Kopiowanie danych z/do bazy danych SQL Azure żadnych obsługiwanych ujścia magazynu danych lub skopiować dane z dowolnego źródła obsługiwanych magazynu danych do bazy danych SQL Azure. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

W szczególności ten łącznik bazy danych SQL Azure obsługuje:

- Kopiowanie danych przy użyciu uwierzytelniania SQL.
- Jako źródło pobierania danych przy użyciu zapytania SQL lub procedurę składowaną.
- Jako obiekt sink dodanie danych do tabeli docelowej lub wywoływania procedury składowanej z niestandardowej logiki podczas kopiowania.

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do łącznika usługi Azure SQL Database.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Obsługiwane są następujące właściwości dla bazy danych SQL Azure połączone usługi:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **AzureSqlDatabase** | Yes |
| Parametry połączenia |Podaj informacje wymagane do połączenia z wystąpieniem bazy danych SQL Azure dla właściwości connectionString. Obsługiwane jest tylko uwierzytelnianie podstawowe. Zaznacz to pole jako SecureString. |Yes |
| connectVia | [Integrację środowiska uruchomieniowego](concepts-integration-runtime.md) ma być używany do nawiązania połączenia z magazynem danych. (Jeśli w magazynie danych znajduje się w sieci prywatnej), można użyć środowiska uruchomieniowego integracji Azure lub Self-hosted integracji w czasie wykonywania. Jeśli nie zostanie określony, używa domyślnej środowiska uruchomieniowego integracji Azure. |Nie |

> [!IMPORTANT]
> Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) serwera bazy danych do [Zezwalaj usługom Azure na dostęp do serwera](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ponadto jeśli dane są kopiowane do bazy danych SQL Azure z zewnętrznej platformy Azure, łącznie z lokalnych źródeł danych z fabryką danych siebie integrację środowiska uruchomieniowego, skonfigurować odpowiedni zakres adresów IP dla komputera, który wysyła dane do bazy danych SQL Azure Baza danych.

**Przykład:**

```json
{
    "name": "AzureSqlDbLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
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

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje zobacz artykuł zestawów danych. Ta sekcja zawiera listę właściwości obsługiwanych przez zestaw danych z bazy danych SQL Azure.

Aby skopiować dane z i do bazy danych SQL Azure, ustaw właściwość Typ zestawu danych do **AzureSqlTable**. Obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type zestawu danych: **AzureSqlTable** | Yes |
| tableName |Nazwa tabeli lub widoku w wystąpieniu bazy danych SQL Azure, odnoszący się do połączonej usługi. | Yes |

**Przykład:**

```json
{
    "name": "AzureSQLDbDataset",
    "properties":
    {
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Database linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez usługi Azure SQL Database źródłowy i odbiorczy właściwości.

### <a name="azure-sql-database-as-source"></a>Baza danych SQL Azure jako źródła

Aby skopiować dane z bazy danych SQL Azure, należy ustawić typ źródła w przypadku działania kopiowania do **SqlSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **SqlSource** | Yes |
| sqlReaderQuery |Użyj niestandardowych zapytania SQL można odczytać danych. Przykład: `select * from MyTable`. |Nie |
| sqlReaderStoredProcedureName |Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej. Ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze składowanej. |Nie |
| storedProcedureParameters |Parametry dla procedury składowanej.<br/>Dozwolone wartości to: par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej. |Nie |

**Informacje, które należy zwrócić uwagę:**

- Jeśli **sqlReaderQuery** określono dla SqlSource, odbywa się działanie kopii tego zapytania względem źródła bazy danych SQL Azure umożliwiają pobieranie danych. Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).
- Jeśli nie określisz "sqlReaderQuery" lub "sqlReaderStoredProcedureName" kolumn określona w sekcji "structure" zestawu danych JSON służą do utworzenia kwerendy (`select column1, column2 from mytable`) w celu uruchomienia bazy danych SQL Azure. Jeśli definicji zestawu danych nie ma "structure", wszystkie kolumny są wybierane w tabeli.
- Jeśli używasz **sqlReaderStoredProcedureName**, nadal należy określić manekina **tableName** właściwość w zestawie danych JSON.

**Przykład: przy użyciu zapytania SQL**

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL Database input dataset name>",
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
                "type": "SqlSource",
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
        "name": "CopyFromAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL Database input dataset name>",
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
                "type": "SqlSource",
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

### <a name="azure-sql-database-as-sink"></a>Baza danych SQL Azure jako odbioru

Aby skopiować dane do bazy danych SQL Azure, należy ustawić typ ujścia w działaniu kopiowania do **SqlSink**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **zbiornika** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość typu sink działania kopiowania: **SqlSink** | Yes |
| writeBatchSize |Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.<br/>Dozwolone wartości to: liczba całkowita (liczba wierszy). |Nie (domyślna to 10 000) |
| writeBatchTimeout |Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.<br/>Dozwolone wartości to: timespan. Przykład: "00: 30:00" (30 minut). |Nie |
| preCopyScript |Określ zapytanie SQL dla aktywności kopiowania do wykonania przed zapisaniem danych do bazy danych SQL Azure. Go będzie można wywołać tylko raz na kopii Uruchom. Ta właściwość służy do oczyszczania danych wstępnie załadowane. |Nie |
| sqlWriterStoredProcedureName |Nazwa procedury przechowywanej, która definiuje sposób dotyczą źródła danych do tabeli docelowej, np. czy upserts lub Przekształcanie przy użyciu logiki biznesowej. <br/><br/>Należy pamiętać, będzie tej procedury składowanej **wywoływane na partię**. Jeśli chcesz wykonać operację, która tylko jest uruchamiane jeden raz i nie ma nic do wykonania z źródło danych, np. Usuń/obcięcia należy użyć `preCopyScript` właściwości. |Nie |
| storedProcedureParameters |Parametry dla procedury składowanej.<br/>Dozwolone wartości to: par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej. |Nie |
| sqlWriterTableType |Określ nazwę typu tabeli do użycia w procedurze składowanej. Działanie kopiowania udostępnia dane jest przenoszony w tabeli tymczasowej o tym typie tabeli. Kod procedury składowanej można następnie scalić dane są kopiowane z istniejącymi danymi. |Nie |

> [!TIP]
> Podczas kopiowania danych do bazy danych SQL Azure, działanie kopiowania dołącza dane do tabeli ujścia domyślnie. Aby przeprowadzić UPSERT lub dodatkowe reguły biznesowe, użyj procedury składowanej w SqlSink. Dowiedz się więcej szczegółów z [wywoływania procedury składowanej dla obiekt Sink SQL](#invoking-stored-procedure-for-sql-sink).

**Przykład 1: dołączanie danych**

```json
"activities":[
    {
        "name": "CopyToAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure SQL Database output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "writeBatchSize": 100000
            }
        }
    }
]
```

**Przykład 2: wywoływanie procedury składowanej podczas kopiowania dla upsert**

Dowiedz się więcej szczegółów z [wywoływania procedury składowanej dla obiekt Sink SQL](#invoking-stored-procedure-for-sql-sink).

```json
"activities":[
    {
        "name": "CopyToAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure SQL Database output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
                "sqlWriterTableType": "CopyTestTableType",
                "storedProcedureParameters": {
                    "identifier": { "value": "1", "type": "Int" },
                    "stringData": { "value": "str1" }
                }
            }
        }
    }
]
```

## <a name="identity-columns-in-the-target-database"></a>Kolumny tożsamości w docelowej bazie danych

Ta sekcja zawiera przykład kopiowanie danych z tabeli źródłowej bez kolumny tożsamości do tabeli docelowej z kolumny tożsamości.

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

Zwróć uwagę, że tabela docelowa ma kolumny tożsamości.

**Źródło zestawu danych JSON definicji**

```json
{
    "name": "SampleSource",
    "properties": {
        "type": " AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "SourceTbl"
        }
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
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "TargetTbl"
        }
    }
}
```

Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością). W tym scenariuszu, należy określić **struktury** właściwości w definicji zestawu danych docelowego, który nie zawiera kolumny tożsamości.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Wywołaj procedurę składowaną z zbiornika SQL

Podczas kopiowania danych do usługi Azure SQL Database, określonego przez użytkownika, przechowywane procedury można można konfigurować i wywoływane z dodatkowymi parametrami.

Podczas kopiowania wbudowane mechanizmy nie służą można procedury składowanej. Zazwyczaj jest używany podczas upsert (insert i update) lub dodatkowego przetwarzania (Scalanie kolumn wyszukiwania dodatkowe wartości, wstawiania do wielu tabel, itp.) musi odbywać się przed ostatnim wstawiania źródła danych w tabeli docelowej.

Poniższy przykład przedstawia sposób użycia procedury składowanej celu upsert do tabeli w bazie danych SQL Azure. Zakładając, że dane wejściowe, jak i w tabeli "Marketingowych" sink zawiera trzy kolumny: identyfikator profilu, stan i kategorii. Wykonaj upsert na podstawie kolumny "ProfileID" i stosowane tylko dla określonej kategorii.

**Wyjściowy zestaw danych**

```json
{
    "name": "AzureSQLDbDataset",
    "properties":
    {
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Database linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "Marketing"
        }
    }
}
```

Zdefiniuj w sekcji "SqlSink" w przypadku działania kopiowania w następujący sposób.

```json
"sink": {
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing",
    "storedProcedureParameters": {
        "category": {
            "value": "ProductA"
        }
    }
}
```

W bazie danych należy zdefiniować procedury składowanej z taką samą nazwę jak "SqlWriterStoredProcedureName". Obsługuje on dane wejściowe z określonego źródła i merge w tabeli wyników. Zwróć uwagę, nazwa parametru procedury składowanej powinna być taka sama jak "Nazwa_tabeli" zdefiniowany w zestawie danych.

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @category varchar(256)
AS
BEGIN
  MERGE [dbo].[Marketing] AS target
  USING @Marketing AS source
  ON (target.ProfileID = source.ProfileID and target.Category = @category)
  WHEN MATCHED THEN
      UPDATE SET State = source.State
  WHEN NOT MATCHED THEN
      INSERT (ProfileID, State, Category)
      VALUES (source.ProfileID, source.State, source.Category)
END
```

W bazie danych należy zdefiniować typu tabeli o takiej samej nazwie jako sqlWriterTableType. Należy zauważyć, że schemat tabeli powinna być taka sama jak schemat zwrócony przez dane wejściowe.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL，
    [Category] [varchar](256) NOT NULL，
)
```

Funkcja procedury składowanej korzysta z [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb675163.aspx).

## <a name="data-type-mapping-for-azure-sql-database"></a>Mapowanie typu danych dla bazy danych SQL Azure

Podczas kopiowania danych z/do bazy danych SQL Azure, następujące mapowania są używane z bazą danych SQL Azure typów danych do typów danych tymczasowych fabryki danych Azure. Zobacz [schemat i dane typu mapowania](copy-activity-schema-and-type-mapping.md) Aby poznać sposób działania kopiowania mapowania typu źródłowego: schemat i dane sink.

| Typ danych bazy danych SQL Azure | Typ danych tymczasowych fabryki danych |
|:--- |:--- |
| bigint |Int64 |
| Binarne |Byte[] |
| bitowe |Wartość logiczna |
| char |Ciąg, Char] |
| data |Data/godzina |
| Data/godzina |Data/godzina |
| datetime2 |Data/godzina |
| Datetimeoffset |DateTimeOffset |
| Decimal |Decimal |
| Atrybut FILESTREAM (varbinary(max)) |Byte[] |
| Liczba zmiennoprzecinkowa |Podwójnej precyzji |
| Obraz |Byte[] |
| int |Int32 |
| oszczędność pieniędzy |Decimal |
| nchar |Ciąg, Char] |
| ntext |Ciąg, Char] |
| numeryczne |Decimal |
| nvarchar |Ciąg, Char] |
| rzeczywiste |Kawaler/panna |
| ROWVERSION |Byte[] |
| smalldatetime |Data/godzina |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Obiekt * |
| Tekst |Ciąg, Char] |
| time |TimeSpan |
| sygnatura czasowa |Byte[] |
| tinyint |Bajtów |
| uniqueidentifier |Identyfikator GUID |
| varbinary |Byte[] |
| varchar |Ciąg, Char] |
| xml |Xml |

## <a name="next-steps"></a>Kolejne kroki
Lista magazynów danych obsługiwane jako źródła i wychwytywanie przez działanie kopiowania w fabryce danych Azure, zobacz [obsługiwane magazyny danych](copy-activity-overview.md##supported-data-stores-and-formats).