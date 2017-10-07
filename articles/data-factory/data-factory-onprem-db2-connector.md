---
title: "aaaMove danych z bazy danych DB2 przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomove dane z bazy danych DB2 lokalnej bazy danych przy użyciu działania kopiowania fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Przenieść dane z bazy danych DB2 za pomocą działania kopiowania fabryki danych Azure
W tym artykule opisano używania działania kopiowania fabryki danych Azure toocopy danych z magazynu danych tooa lokalnej bazy danych DB2 bazy danych. Możesz skopiować magazynu tooany danych, który jest wymieniony jako obsługiwany zbiornika w hello [działań przepływu danych fabryki danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artykułu. W tym temacie opiera się na powitania artykułu fabryki danych, które zawiera omówienie przepływu danych za pomocą działania kopiowania i wyświetla kombinacje magazynu danych hello obsługiwane. 

Fabryka danych aktualnie obsługuje tylko przenoszenia danych z tooa bazy danych DB2 [obsługiwanych ujścia magazynu danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Przenoszenie danych z innych danych przechowuje tooa bazy danych DB2 bazy danych nie jest obsługiwana.

## <a name="prerequisites"></a>Wymagania wstępne
Fabryka danych obsługuje połączenia bazy danych DB2 lokalnie tooan przy użyciu hello [brama zarządzania danymi](data-factory-data-management-gateway.md). Aby uzyskać instrukcje krok po kroku tooset zapasową hello bramy danych w potoku toomove danych, zobacz hello [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

Wymagana jest brama, nawet jeśli hello bazy danych DB2 znajduje się na maszynie Wirtualnej Azure IaaS. Możesz zainstalować bramę hello na powitania tej samej IaaS maszyny Wirtualnej jako hello magazynu danych. Jeśli brama hello można połączyć z usługą toohello bazy danych, możesz zainstalować hello bramę na innej maszynie Wirtualnej.

Brama zarządzania danymi Hello oferuje wbudowane sterownik bazy danych DB2, więc nie zostanie toomanually zainstalować sterownik toocopy danych z bazy danych DB2.

> [!NOTE]
> Aby uzyskać wskazówki dotyczące rozwiązywania problemów dotyczących połączenia i problemy bramy, zobacz hello [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artykułu.


## <a name="supported-versions"></a>Obsługiwane wersje
Łącznik Hello DB2 fabryki danych obsługuje hello IBM DB2 platform i wersje Menedżera dostępu programu SQL Distributed relacyjnej bazy danych architektury DRDA () w wersji 9, 10 lub 11:

* IBM DB2 w wersji 11.1 z/OS
* IBM DB2 w wersji 10.1 z/OS
* IBM DB2 (AS400) i wersji 7.2
* IBM DB2 i (AS400) w wersji 7.1
* IBM DB2 dla systemu Linux, UNIX i systemu Windows (LUW) w wersji 11
* IBM DB2 dla LUW wersji 10.5
* IBM DB2 dla LUW wersji 10.1

> [!TIP]
> Jeśli zostanie wyświetlony komunikat o błędzie powitania "hello pakietu odpowiedniego tooan SQL instrukcji żądania wykonania nie został znaleziony. SQLSTATE 51002 SQLCODE =-805, = "hello przyczyna jest potrzebny pakiet nie został utworzony dla zwykłego użytkownika hello na powitania systemu operacyjnego. tooresolve ten problem, wykonaj te instrukcje dla danego typu serwera bazy danych DB2:
> - Bazy danych DB2 dla i (AS400): umożliwia użytkownikowi zasilania utworzyć kolekcję hello na powitania zwykłego użytkownika przed uruchomieniem działanie kopiowania. toocreate hello kolekcji, użyj polecenia hello:`create collection <username>`
> - Bazy danych DB2 z/OS lub LUW: Użyj konta wysokiego poziomu uprawnień — użytkownik zaawansowany lub administrator urzędów pakietu i powiązania, BINDADD, uprawnienia EXECUTE tooPUBLIC — toorun hello raz kopiowania. Witaj potrzebny pakiet jest tworzony automatycznie podczas kopiowania hello. Potem można przełączać wstecz toohello zwykłego użytkownika dla sekwencji kolejnych kopii.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o toomove działania kopiowania danych z magazynu danych programu DB2 lokalnie przy użyciu różnych narzędzi i interfejsów API: 

- Witaj Najprostszym sposobem toocreate potoku jest hello toouse kreatora kopiowania fabryki danych Azure. Szybkie przewodnik dotyczący tworzenia za pomocą Kreatora kopiowania hello potoku, zobacz hello [samouczek: tworzenie potoku za pomocą Kreatora kopiowania hello](data-factory-copy-data-wizard-tutorial.md). 
- Można również użyć narzędzia toocreate potoku, w tym hello portalu Azure, programu Visual Studio, programu Azure PowerShell, usługi Azure Resource Manager szablonu, hello interfejs API .NET i hello interfejsu API REST. Aby uzyskać instrukcje krok po kroku toocreate potoku z działaniem kopiowania, zobacz hello [samouczek działanie kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Tworzenie fabryki danych tooyour magazynów danych wejściowych i wyjściowych toolink połączonych usług.
2. Tworzenie zestawów danych toorepresent w danych wejściowych i wyjściowych danych dla operacji kopiowania hello. 
3. Utworzyć potok aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Używania hello kreatora kopiowania, definicje JSON hello fabryki danych połączone usługi, zestawy danych i jednostek potoku są tworzone automatycznie dla Ciebie. Użycie narzędzia lub interfejsów API (z wyjątkiem hello interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello hello jednostek fabryki danych. Witaj [przykład JSON: kopiowanie danych z bazy danych DB2 tooAzure magazynu obiektów Blob](#json-example-copy-data-from-db2-to-azure-blob) zawiera definicje JSON hello hello jednostek fabryki danych, które są używane toocopy danych z magazynu danych programu DB2 lokalnie.

Witaj następujące sekcje zawierają szczegółowe informacje o hello właściwości JSON, które są używane toodefine hello fabryki danych podmiotów, które są określone tooa bazy danych DB2 magazynu danych.

## <a name="db2-linked-service-properties"></a>Właściwości usługi połączone bazy danych DB2
Witaj w poniższej tabeli wymieniono właściwości JSON hello, które są określone tooa bazy danych DB2 połączone usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| **Typ** |Ta właściwość musi być ustawiona zbyt**OnPremisesDB2**. |Tak |
| **Serwer** |Nazwa powitania serwera hello bazy danych DB2. |Tak |
| **bazy danych** |Nazwa Hello hello bazy danych DB2 bazy danych. |Tak |
| **Schemat** |Nazwa Hello hello schematu w bazie danych hello bazy danych DB2. Ta właściwość jest rozróżniana wielkość liter. |Nie |
| **Typ authenticationType** |Hello typ uwierzytelniania, który jest używany tooconnect toohello bazy danych DB2 w bazie danych. Witaj możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| **Nazwa użytkownika** |Nazwa Hello hello konta użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| **hasło** |Hello hasło dla konta użytkownika hello. |Nie |
| **gatewayName** |Nazwa Hello hello bramy, która hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych DB2. |Tak |

## <a name="dataset-properties"></a>Właściwości zestawu danych
Listę hello sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje, takich jak **struktury**, **dostępności**i hello **zasad** dla zestawu danych JSON, są podobne dla wszystkich typów obiektów dataset (Azure SQL, magazynem Azure Blob, tabel Azure Magazyn i tak dalej).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj **typeProperties** sekcja dla zestawu danych typu **RelationalTable**, które dotyczą hello bazy danych DB2 zestawu danych, hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| **tableName** |Nazwa Hello hello tabeli w wystąpieniu bazy danych hello DB2, który hello połączonej usługi odwołuje się do. Ta właściwość jest rozróżniana wielkość liter. |Nie (jeśli hello **zapytania** właściwości działania kopiowania typu **RelationalSource** jest określona) |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Listę hello sekcje i właściwości, które są dostępne do definiowania działania kopiowania, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Kopiuj właściwości działania, takie jak **nazwa**, **opis**, **dane wejściowe** tabeli, **generuje** tabeli, i **zasad**, są dostępne dla wszystkich typów działań. Witaj właściwości, które są dostępne w hello **typeProperties** sekcji hello działanie dla każdego typu działania. Dla działania kopiowania właściwości hello zależy od hello typy źródeł danych i sink.

Dla działania kopiowania, gdy źródłem hello jest typu **RelationalSource** (która obejmuje bazy danych DB2), hello następujące właściwości są dostępne w hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| **zapytania** |Użyj hello zapytanie niestandardowe tooread hello danych. |Ciąg zapytania SQL. Na przykład: `"query": "select * from "MySchema"."MyTable""` |Nie (jeśli hello **tableName** określono właściwości zestawu danych) |

> [!NOTE]
> Nazwy schematu i tabeli jest rozróżniana wielkość liter. W instrukcji zapytania hello, ujmij nazw właściwości, za pomocą "" (podwójne cudzysłowy). Na przykład:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Przykład JSON: kopiowanie danych z bazy danych DB2 tooAzure magazynu obiektów Blob
W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). przykład Witaj pokazuje, jak toocopy dane z bazy danych DB2 bazy danych magazynu tooBlob. Jednak możesz skopiować dane zbyt[wszystkie obsługiwane dane przechowywane typ ujścia](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania fabryki danych Azure.

przykład Witaj ma powitania po jednostek fabryki danych:

- Bazy danych DB2 połączonej usługi typu [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Połączonej usługi typu magazynu obiektów Blob platformy Azure [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- A [potoku](data-factory-create-pipelines.md) z działania kopiowania, który używa hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) właściwości

przykład Witaj co godzinę kopiuje dane z wyniku kwerendy w tooan bazy danych DB2 obiektów blob platformy Azure. Witaj JSON właściwości, które są używane w przykładowym hello są opisane w hello sekcjach hello jednostki definicje.

Pierwszym krokiem Zainstaluj i skonfiguruj bramę danych. Instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**Bazy danych DB2 połączone usługi**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

**Azure Blob połączoną usługą magazynu**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Wejściowy zestaw danych DB2**

przykład Witaj przyjęto założenie, że utworzono tabelę w bazie danych DB2 o nazwie "MyTable", która zawiera kolumnę z etykietą "timestamp" hello czasu serii danych.

Witaj **zewnętrznych** właściwość jest ustawiona zbyt "wartość true." Usługi fabryka danych hello to ustawienie informuje o tym, że ten zestaw danych jest zewnętrzne toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello. Zwróć uwagę, że hello **typu** właściwość jest ustawiona zbyt**RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

**Azure Blob wyjściowy zestaw danych**

Dane są zapisywane nowego obiektu blob tooa co godzinę przez ustawienie hello **częstotliwość** właściwości zbyt "Hour" i hello **interwał** too1 właściwości. Witaj **folderPath** właściwości dla obiektu blob hello dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godzinę części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Potoku dla aktywności kopiowania hello**

potok Hello zawiera działanie kopiowania, który jest skonfigurowany toouse określony wejściowych i wyjściowych zestawów danych i która jest toorun zaplanowane co godzinę. W definicji JSON dla potoku hello hello, hello **źródła** typu ustawiono zbyt**RelationalSource** i hello **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello danych z tabeli "Zamówienia" hello.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Mapowanie typu dla bazy danych DB2
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, działanie kopiowania wykonuje automatyczne konwersje typu toosink typu źródłowego za pomocą następującego rozwinięcie hello:

1. Konwertować z typu .NET tooa typu natywnego źródła
2. Konwertować z typu natywnego zbiornika tooa typu .NET

Hello następujące mapowania są używane, gdy działanie kopiowania konwertuje hello dane z bazy danych DB2 .NET tooa typu:

| Typ bazy danych DB2 | Typ programu .NET framework |
| --- | --- |
| SmallInt |Int16 |
| Liczba całkowita |Int32 |
| BigInt |Int64 |
| Real |Pojedynczy |
| O podwójnej precyzji |O podwójnej precyzji |
| Float |O podwójnej precyzji |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| numeryczne |Decimal |
| Date |Data i godzina |
| Time |Zakres czasu |
| Znacznik czasu |Data i godzina |
| XML |Byte] |
| char |Ciąg |
| VarChar |Ciąg |
| LongVarChar |Ciąg |
| DB2DynArray |Ciąg |
| Binarne |Byte] |
| VarBinary |Byte] |
| LongVarBinary |Byte] |
| Grafika |Ciąg |
| VarGraphic |Ciąg |
| LongVarGraphic |Ciąg |
| CLOB |Ciąg |
| Obiekt blob |Byte] |
| DbClob |Ciąg |
| SmallInt |Int16 |
| Liczba całkowita |Int32 |
| BigInt |Int64 |
| Real |Pojedynczy |
| O podwójnej precyzji |O podwójnej precyzji |
| Float |O podwójnej precyzji |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| numeryczne |Decimal |
| Date |Data i godzina |
| Time |Zakres czasu |
| Znacznik czasu |Data i godzina |
| XML |Byte] |
| char |Ciąg |

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn toomap kolumn w powitania źródło zestawu danych toocolumns w zestawie danych zbiornika hello, zobacz temat [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Odczyty powtarzalne źródłami relacyjnymi
Po skopiowaniu danych z magazynu danych relacyjnych zachować powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować ponawiania hello **zasad** właściwości zestawu danych toorerun wycinka, gdy wystąpi błąd. Upewnij się, że hello te same dane jest do odczytu niezależnie od tego, jak wiele razy hello wycinek jest Uruchom ponownie i niezależnie od tego, jak ponownie uruchomić hello wycinka. Aby uzyskać więcej informacji, zobacz [Repeatable odczytuje z źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie
Więcej informacji na temat kluczowych czynników wpływających na wydajność hello działanie kopiowania i sposoby wydajności toooptimize w hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).
