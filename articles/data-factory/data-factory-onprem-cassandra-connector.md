---
title: "dane aaaMove z Cassandra przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z Cassandra lokalnej bazy danych przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Przenoszenia danych z Cassandra lokalną bazą danych przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych Cassandra. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z lokalnego Cassandra magazynu tooany obsługiwane ujścia danych magazynu danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przeniesienie magazynu danych z danych Cassandra tooother magazyny danych, ale nie do przenoszenia danych z magazynu magazynów danych Cassandra tooa innych danych. 

## <a name="supported-versions"></a>Obsługiwane wersje
Łącznik Cassandra Hello obsługuje następujące wersje Cassandra hello: 2.X.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj fabryki danych Azure toobe stanie tooconnect tooyour lokalnymi Cassandra bazy danych usługi, należy zainstalować bramę zarządzania danymi na powitania sam komputera bazy danych hostów hello lub tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello Baza danych. Brama zarządzania danymi jest składnikiem, który łączy usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi. Zobacz [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello toomove potoku danych.

Należy użyć bazy danych hello bramy tooconnect tooa Cassandra, nawet jeśli hello baza danych znajduje się w chmurze hello, na przykład na maszynie Wirtualnej platformy Azure IaaS. Y, do których masz hello bramy na hello tej bazy danych hello hostów w tej samej maszyny Wirtualnej lub na oddzielnym maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.  

Po zainstalowaniu bramy hello automatycznie instaluje bazę tooCassandra tooconnect sterownik ODBC Cassandra firmy Microsoft. W związku z tym nie ma potrzeby toomanually zainstalowania sterownika na komputerze bramy hello podczas kopiowania danych z bazy danych Cassandra hello. 

> [!NOTE]
> Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API. 

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello. 
- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego magazynu danych Cassandra [przykład JSON: kopiowanie danych z tooAzure Cassandra obiektu Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych Cassandra tooa określonych jednostek fabryki danych używanych toodefine:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooCassandra połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **OnPremisesCassandra** |Tak |
| Host |Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.<br/><br/>Określ rozdzielaną przecinkami listę adresów IP lub serwerów tooall tooconnect nazwy hosta jednocześnie. |Tak |
| port |Hello port TCP, którego hello Cassandra serwer używa toolisten dla połączeń klienta. |Nie, wartość domyślna: 9042 |
| Typ authenticationType |Podstawowa lub anonimowe |Tak |
| nazwa użytkownika |Określ nazwę użytkownika dla konta użytkownika hello. |Tak, jeśli authenticationType ustawiono tooBasic. |
| hasło |Określ hasło dla konta użytkownika hello. |Tak, jeśli authenticationType ustawiono tooBasic. |
| gatewayName |Nazwa Hello hello bramy, która jest używana tooconnect toohello lokalnymi Cassandra w bazie danych. |Tak |
| encryptedCredential |Poświadczenie szyfrowane przez bramę hello. |Nie |

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **CassandraTable** ma następujące właściwości hello

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| przestrzeni kluczy |Nazwa schematu bazy danych Cassandra lub hello przestrzeni kluczy. |Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana). |
| tableName |Nazwa tabeli hello Cassandra bazy danych. |Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana). |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Jeśli źródło jest typu **CassandraSource**, hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Zapytania SQL 92 lub CQL zapytania. Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Korzystając z zapytania SQL, określ **nazwa name.table przestrzeni kluczy** toorepresent hello tabelę, która ma tooquery. |Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych). |
| consistencyLevel |poziomu spójności Hello Określa, ile replik musi odpowiadać żądanie odczytu tooa przed zwróceniem aplikacji klienckiej toohello danych. Sprawdzanie Cassandra hello określonej liczby replik dla żądania odczytu hello toosatisfy danych. |JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje. |Nie. Domyślna wartość to jeden. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Przykład JSON: kopiowanie danych z tooAzure Cassandra obiektów Blob
W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Pokazuje, jak dane toocopy z Cassandra lokalnej bazy danych tooan magazynu obiektów Blob Azure. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

> [!IMPORTANT]
> W tym przykładzie przedstawiono fragmenty kodu JSON. Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.

przykład Witaj ma hello następujące obiekty fabryki danych:

* Połączonej usługi typu [OnPremisesCassandra](#linked-service-properties).
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [CassandraTable](#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [CassandraSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Cassandra połączonej usługi:**

W tym przykładzie użyto hello **Cassandra** połączonej usługi. Zobacz [Cassandra połączona usługa](#linked-service-properties) sekcji właściwości hello obsługiwane przez tej połączonej usługi.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Połączonej usługi magazynu Azure:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

**Zestaw danych wejściowych Cassandra:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
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

Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

**Azure Blob wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Aktywność kopiowania w potoku z Cassandra źródłowy i odbiorczy obiektów Blob:**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**CassandraSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.

Zobacz [właściwości typu RelationalSource](#copy-activity-properties) hello listę obsługiwanych przez hello RelationalSource właściwości.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Mapowanie typu dla Cassandra
| Typ Cassandra | Typ na podstawie .net |
| --- | --- |
| ASCII |Ciąg |
| BIGINT |Int64 |
| OBIEKT BLOB |Byte] |
| WARTOŚĆ LOGICZNA |Wartość logiczna |
| DECIMAL |Decimal |
| O PODWÓJNEJ PRECYZJI |O podwójnej precyzji |
| FLOAT |Pojedynczy |
| INET |Ciąg |
| INT |Int32 |
| TEKST |Ciąg |
| ZNACZNIK CZASU |Data i godzina |
| TIMEUUID |Identyfikator GUID |
| IDENTYFIKATOR UUID |Identyfikator GUID |
| VARCHAR |Ciąg |
| VARINT |Decimal |

> [!NOTE]
> Kolekcja typów (mapy, zestaw, listy itp.), można znaleźć zbyt[współpracy z typami kolekcji Cassandra za pomocą tabeli wirtualnej](#work-with-collections-using-virtual-table) sekcji.
>
> Typy definiowane przez użytkownika nie są obsługiwane.
>
> Długość Hello długości kolumny typu Binary i kolumny typu String nie może być większa niż 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Praca z kolekcji za pomocą tabeli wirtualnej
Fabryka danych Azure korzysta z wbudowanej ODBC sterownika tooconnect tooand kopiowania danych z bazy danych Cassandra. Dla typów kolekcji, w tym mapy, zestaw i listy sterownik hello renormalizes hello danych do odpowiednich tabel wirtualnego. W szczególności jeśli tabela zawiera wszystkie kolumny w kolekcji, sterownik hello generuje hello następujące tabele wirtualne:

* A **tabeli podstawowej**, który zawiera hello tych samych danych co hello rzeczywistych tabeli, z wyjątkiem hello kolekcji kolumn. tabeli podstawowej Hello używa hello takie same nazwy jako hello rzeczywistych tabeli, która reprezentuje.
* A **tabeli wirtualnej** dla każdej kolekcji kolumny, która rozszerza hello zagnieżdżone dane. tabele wirtualne Hello reprezentujących kolekcje są nazywane przy użyciu nazwy hello hello rzeczywistych tabeli separator "*vt*" i nazwę hello hello kolumny.

Tabele wirtualne odnoszą się toohello dane w tabeli rzeczywistych hello, włączanie tooaccess sterownika hello hello nieznormalizowany danych. Zobacz sekcję przykład, aby uzyskać szczegółowe informacje. Dostęp z zawartości hello Cassandra kolekcji, zapytań i przyłączanie tabel wirtualnego hello.

Można użyć hello [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) widoku toointuitively hello listy tabel w bazie danych Cassandra tym tabele wirtualne hello i wyświetlić podgląd danych hello wewnątrz. Można również utworzyć zapytanie w hello kreatora kopiowania i sprawdź poprawność toosee hello wyniku.

### <a name="example"></a>Przykład
Na przykład hello następujące "ExampleTable" jest Cassandra tabeli bazy danych, która zawiera całkowitą kolumna klucza podstawowego o nazwie "pk_int", kolumna tekst o nazwie wartość kolumny listy, kolumny mapy i zestawu kolumn (o nazwie "StringSet").

| pk_int | Wartość | List | mapy | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"Przykładowa wartość 1" |["1", "2", "3"] |{"S1": "", "S2": "b"} |{"", "B", "C"} |
| 3 |"przykład value 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"", "E"} |

Sterownik Hello powoduje wygenerowanie wielu toorepresent tabele wirtualne to pojedynczej tabeli. Witaj kolumny klucza obcego w tabelach wirtualnych hello odwoływania się do hello kolumn klucza podstawowego w tabeli rzeczywistych hello i wskazywać rzeczywistych, które odpowiada wiersza tabeli wirtualnej hello wiersza tabeli.

pierwszy tabeli wirtualnej Hello jest hello tabeli podstawowej o nazwie "ExampleTable" jest wyświetlany w obszarze hello w poniższej tabeli. Tabela bazowa Hello zawiera hello tych samych danych co hello oryginalnej tabeli bazy danych, z wyjątkiem hello kolekcje, które są pominięte w tej tabeli i rozwinięty w innych tabelach wirtualnych.

| pk_int | Wartość |
| --- | --- |
| 1 |"Przykładowa wartość 1" |
| 3 |"przykład value 3" |

Witaj w poniższych tabelach hello tabel wirtualnych, które renormalize hello dane z kolumny listy, mapy i StringSet hello. Witaj kolumny o nazwach kończyć "_index" lub "_klucza" wskazać pozycję hello hello danych w oryginalnej listy hello lub mapy. Witaj kolumny o nazwach kończących się znakiem "_value" zawierają dane hello rozwinięty z kolekcji hello.

#### <a name="table-exampletablevtlist"></a>Tabela "ExampleTable_vt_List":
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tabela "ExampleTable_vt_Map":
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |A |
| 1 |S2 |B |
| 3 |S1 |T |

#### <a name="table-exampletablevtstringset"></a>Tabela "ExampleTable_vt_StringSet":
| pk_int | StringSet_value |
| --- | --- |
| 1 |A |
| 1 |B |
| 1 |C |
| 3 |A |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
