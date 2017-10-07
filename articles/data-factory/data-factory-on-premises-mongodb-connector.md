---
title: "aaaMove dane z bazy danych MongoDB przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove dane z bazy danych MongoDB bazy danych przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Przenoszenie danych z bazy danych MongoDB przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych MongoDB. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Możesz skopiować dane z lokalnej bazy danych MongoDB magazynu tooany obsługiwane ujścia danych magazynu danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych z danych MongoDB, ale nie do przenoszenia danych z magazynu danych innych danych magazynów tooan bazy danych MongoDB. 

## <a name="prerequisites"></a>Wymagania wstępne
Hello fabryki danych Azure toobe stanie tooconnect tooyour lokalnej bazy danych MongoDB bazy danych usługi należy zainstalować hello następujące składniki:

- Obsługiwane wersje bazy danych MongoDB: 2.4, 2.6 3.0 i 3.2.
- Brama zarządzania danymi na hello tej samej maszynie tej bazy danych hello hostów lub na tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello bazy danych. Brama zarządzania danymi to oprogramowanie, które nawiązuje połączenie usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi. Zobacz [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello toomove potoku danych.

    Po zainstalowaniu bramy hello automatycznie instaluje tooMongoDB tooconnect sterownik Microsoft MongoDB ODBC.

    > [!NOTE]
    > Należy toouse hello bramy tooconnect tooMongoDB, nawet jeśli jest obsługiwany na maszynach wirtualnych Azure IaaS. Jeśli próbujesz tooconnect tooan wystąpienie bazy danych MongoDB hostowanych w chmurze, można także zainstalować wystąpienie bramy hello w hello maszyn wirtualnych IaaS.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych bazy danych MongoDB lokalnymi przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych bazy danych MongoDB lokalnych, zobacz [przykład JSON: kopiowanie danych z bazy danych MongoDB tooAzure obiektu Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek tooMongoDB określonego źródła:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj Poniższa tabela zawiera opis elementów JSON określonych zbyt**OnPremisesMongoDB** połączonej usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **OnPremisesMongoDb** |Tak |
| serwer |Adres IP lub hosta nazwę serwera bazy danych MongoDB hello. |Tak |
| port |Port TCP, którego hello serwera bazy danych MongoDB używa toolisten dla połączeń klienta. |Opcjonalne, wartość domyślna: 27017 |
| Typ authenticationType |Podstawowy, lub anonimowe. |Tak |
| nazwa użytkownika |Tooaccess konta użytkownika bazy danych MongoDB. |Tak (jeśli jest używane uwierzytelnianie podstawowe). |
| hasło |Hasło dla użytkownika hello. |Tak (jeśli jest używane uwierzytelnianie podstawowe). |
| authSource |Nazwa bazy danych MongoDB hello czy chcesz toouse toocheck swoje poświadczenia dla uwierzytelniania. |Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe). domyślne: używa konta administratora hello i hello bazy danych określona za pomocą właściwości databaseName. |
| DatabaseName |Nazwa bazy danych MongoDB hello, które mają tooaccess. |Tak |
| gatewayName |Nazwa bramy hello, który uzyskuje dostęp do magazynu danych hello. |Tak |
| encryptedCredential |Poświadczenie szyfrowane przez bramę. |Optional (Opcjonalność) |

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **MongoDbCollection** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| CollectionName |Nazwa kolekcji hello w bazie danych MongoDB. |Tak |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Gdy źródło hello jest typu **MongoDbSource** hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL 92. Na przykład: Wybierz * z MyTable. |Nie (Jeśli **collectionName** z **dataset** jest określona) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Przykład JSON: kopiowanie danych z bazy danych MongoDB tooAzure obiektów Blob
W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Widoczny jest sposób toocopy dane z lokalnej bazy danych MongoDB tooan magazynu obiektów Blob Azure. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [OnPremisesMongoDb](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [MongoDbCollection](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [MongoDbSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych MongoDB, co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem instalacji bramy zarządzania danymi hello zgodnie z instrukcjami hello hello [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu.

**Bazy danych MongoDB połączonej usługi:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**Wejściowy zestaw danych MongoDB:** ustawienie "external": "prawda" informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Azure Blob wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Aktywność kopiowania w potoku z bazy danych MongoDB źródłowy i odbiorczy obiektów Blob:**

potok Hello zawiera działanie kopiowania, który hello toouse skonfigurowanych powyżej wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**MongoDbSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Schemat fabryka danych
Usługi fabryka danych Azure wnioskuje schemat z kolekcji bazy danych MongoDB przy użyciu hello najnowsze 100 dokumentów w kolekcji hello. Jeśli te dokumenty 100 nie zawierają pełny schemat, można zignorować podczas operacji kopiowania hello niektóre kolumny.

## <a name="type-mapping-for-mongodb"></a>Mapowanie typu dla bazy danych MongoDB
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych tooMongoDB hello następującego mapowania są używane z typów too.NET typy bazy danych MongoDB.

| Typ bazy danych MongoDB | Typ programu .NET framework |
| --- | --- |
| Binarne |Byte] |
| Wartość logiczna |Wartość logiczna |
| Date |Data i godzina |
| NumberDouble |O podwójnej precyzji |
| NumberInt |Int32 |
| NumberLong |Int64 |
| Identyfikator obiektu |Ciąg |
| Ciąg |Ciąg |
| IDENTYFIKATOR UUID |Identyfikator GUID |
| Obiekt |Renormalized do spłaszczenia kolumn z "_" jako separatora zagnieżdżonych |

> [!NOTE]
> toolearn o obsługę tablic za pomocą tabele wirtualne można znaleźć zbyt[obsługę złożonych typów przy użyciu tabele wirtualne](#support-for-complex-types-using-virtual-tables) poniższej sekcji.

Obecnie nie są obsługiwane następujące typy danych MongoDB hello: DBPointer, JavaScript, maksymalna liczba na minutę klucza, wyrażenie regularne, Symbol, Timestamp, niezdefiniowane

## <a name="support-for-complex-types-using-virtual-tables"></a>Obsługę złożonych typów przy użyciu tabele wirtualne
Fabryka danych Azure korzysta z wbudowanej ODBC sterownika tooconnect tooand kopiowania danych z bazy danych MongoDB. Typów złożonych takich jak macierze lub obiektów z różnymi typami wszystkich dokumentów hello sterownik hello ponownie normalizuje danych do odpowiednich tabel wirtualnego. W szczególności jeśli tabela zawiera takich kolumn, sterownik hello generuje hello następujące tabele wirtualne:

* A **tabeli podstawowej**, który zawiera hello tych samych danych co hello rzeczywistych tabeli, z wyjątkiem hello kolumny typu złożonego. tabeli podstawowej Hello używa hello takie same nazwy jako hello rzeczywistych tabeli, która reprezentuje.
* A **tabeli wirtualnej** dla każdej kolumny typu złożonego, która rozszerza hello zagnieżdżone dane. tabele wirtualne Hello są nazywane przy użyciu hello Nazwa tabeli rzeczywistych hello, separator "_" i nazwą hello hello tablicy lub obiektu.

Tabele wirtualne odnoszą się toohello dane w tabeli rzeczywistych hello, włączanie tooaccess sterownika hello hello nieznormalizowany danych. Zobacz przykład sekcję poniżej szczegółowe informacje. Dostęp z zawartości hello tablic bazy danych MongoDB, zapytań i przyłączanie tabel wirtualnego hello.

Można użyć hello [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) widoku toointuitively hello listy tabel w bazie danych MongoDB, łącznie z tabelami wirtualnego hello i wyświetlić podgląd danych hello wewnątrz. Można również utworzyć zapytanie w hello kreatora kopiowania i sprawdź poprawność toosee hello wyniku.

### <a name="example"></a>Przykład
Na przykład "ExampleTable" poniżej znajduje się tabela bazy danych MongoDB o jedną kolumnę z tablicę obiektów w każdej komórce — faktury i jedną kolumnę z tablicą typów skalarnych — klasyfikacji.

| _id | Nazwa klienta | Faktury | Poziom usług | Klasyfikacje |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id: elementu "123",: "tostera", cena: Rabat "456",: "0,2"}, {invoice_id: "124", element: "piec", cena: Zniżka "1235": "0,2"}] |Srebrny |[5,6] |
| 2222 |XYZ |[{invoice_id: element "135": "lodówko", cena: Rabat "12543": "0,0"}] |Gold |[1,2] |

Sterownik Hello powoduje wygenerowanie wielu toorepresent tabele wirtualne to pojedynczej tabeli. pierwszy tabeli wirtualnej Hello jest hello tabeli podstawowej o nazwie "ExampleTable", pokazano poniżej. Tabela podstawowa Hello zawiera wszystkie dane hello hello oryginalnej tabeli, ale hello danych z tablic hello została pominięta i jest rozwinięta w tabelach wirtualnych hello.

| _id | Nazwa klienta | Poziom usług |
| --- | --- | --- |
| 1111 |ABC |Srebrny |
| 2222 |XYZ |Gold |

Witaj w poniższych tabelach hello wirtualnego tabel, które reprezentują hello oryginalnego tablic, na przykład Witaj. Te tabele zawierają hello następujące czynności:

* Odwołanie kopii toohello oryginalnego kolumna klucza podstawowego odpowiedni toohello wiersz tablicy oryginalnej hello (za pomocą kolumny _id hello)
* Wskazanie pozycji hello danych hello w tablicy oryginalnej hello
* dane dla każdego elementu w tablicy hello rozwinięty Hello

Tabela "ExampleTable_Invoices":

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | Element | price | Rabat |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |tostera |456 |0.2 |
| 1111 |1 |124 |Piec |1235 |0.2 |
| 2222 |0 |135 |lodówko |12543 |0.0 |

Tabela "ExampleTable_Ratings":

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.

## <a name="next-steps"></a>Następne kroki
Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykuł instrukcje krok po kroku dla tworzenie potoku danych, które przenosi dane z lokalnymi danymi przechowywania tooan magazynu danych Azure.
