---
title: aaaMove danych z baz danych ODBC | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu toomove danych ze źródła danych ODBC są przechowywane przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Przenieś magazyny danych ODBC z danych przy użyciu fabryki danych Azure
W tym artykule opisano, jak przechowywać toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi danymi ODBC. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z magazynu ODBC danych magazynu tooany obsługiwane ujścia danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych ze źródła danych ODBC, ale nie do przenoszenia danych z magazynu magazynów danych ODBC tooan innych danych. 

## <a name="enabling-connectivity"></a>Włączenie łączności
Usługi fabryka danych obsługuje połączenia lokalnego tooon ODBC — źródła przy użyciu hello brama zarządzania danymi. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello. Użyj magazynu danych ODBC tooan hello bramy tooconnect, nawet jeśli jest obsługiwany w maszynie Wirtualnej platformy Azure IaaS.

Możesz zainstalować bramę hello na powitania lokalnego tego samego komputera lub maszyny Wirtualnej platformy Azure jako magazynu danych ODBC hello hello. Jednak zaleca się instalowania bramy hello na oddzielnych maszyny/Azure IaaS maszyny Wirtualnej rywalizacji tooavoid i w celu zapewnienia lepszej wydajności. Po zainstalowaniu bramy hello na osobnym komputerze hello maszyny powinny być możliwe tooaccess hello maszyny z magazynem danych ODBC hello.

Oprócz hello brama zarządzania danymi należy również sterownika ODBC hello tooinstall hello magazynu danych na komputerze bramy hello.

> [!NOTE]
> Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych ODBC, za pomocą różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych ODBC, zobacz [przykład JSON: tooAzure obiektu Blob magazynu kopii danych ze źródła danych ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych określonego tooODBC jednostek fabryki danych używanych toodefine:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooODBC połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **OnPremisesOdbc** |Tak |
| Parametry połączenia |poświadczenie zaszyfrowana Hello poświadczeń innych niż dostępu część hello ciąg połączenia i opcjonalne. Przykłady w hello następujące sekcje. |Tak |
| poświadczenia |Hello dostępu do poświadczeń część hello parametrów połączenia określonego w formacie wartość właściwości sterownika. Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ". |Nie |
| Typ authenticationType |Typ uwierzytelniania używany Magazyn danych ODBC toohello tooconnect. Możliwe wartości to: anonimowych, jak i podstawowych. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać magazynu danych ODBC toohello tooconnect. |Tak |

### <a name="using-basic-authentication"></a>Przy użyciu uwierzytelniania podstawowego

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Przy użyciu poświadczeń zaszyfrowanych przy użyciu uwierzytelniania podstawowego
Można szyfrować poświadczeń hello przy użyciu hello [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji hello Program Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych ODBC) ma następujące właściwości hello

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w magazynie danych ODBC hello. |Tak |

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

W przypadku działania kopiowania, gdy źródłem jest typu **RelationalSource** (która obejmuje ODBC), hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: Wybierz * z MyTable. |Tak |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Przykład JSON: tooAzure obiektu Blob magazynu kopii danych ze źródła danych ODBC
W poniższym przykładzie przedstawiono definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Pokazuje, jak dane toocopy z ODBC źródła tooan magazynu obiektów Blob Azure. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

przykład Witaj ma hello następujące obiekty fabryki danych:

1. Połączonej usługi typu [OnPremisesOdbc](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa magazynu danych ODBC, co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem należy skonfigurować bramę zarządzania danymi hello. Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**ODBC połączona usługa** w tym przykładzie używa hello uwierzytelnianie podstawowe. Zobacz [ODBC połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Połączona usługa Azure Storage**

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

**Wejściowy zestaw danych ODBC**

przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w bazie danych ODBC i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Działanie kopiowania w potoku ze źródłem ODBC (RelationalSource) i ujście obiektów Blob (BlobSink)**

potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Mapowanie typu dla ODBC
Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:

1. Konwertować z typu too.NET typów natywnych źródła
2. Konwertować z typu sink toonative typu .NET

Podczas przenoszenia danych z baz danych ODBC, typy danych ODBC są typami too.NET zamapowane, jak wspomniano w hello [mapowanie typu danych ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tematu.

## <a name="map-source-toosink-columns"></a>Mapowanie kolumny toosink źródłowe
toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany. Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>GE historyk magazynu
Utwórz ODBC połączone usługi toolink [historyk Proficy GE (teraz GE historyk)](http://www.geautomation.com/products/proficy-historian) fabryki danych Azure tooan magazynu danych, jak pokazano w hello poniższy przykład:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Instalowanie bramy zarządzania danymi na maszynie lokalnej i zarejestruj bramę hello hello Portal. bramy Hello zainstalowanej na komputerze lokalnym używa sterownika ODBC hello GE historyk tooconnect toohello historyk GE magazynu danych. W związku z tym należy zainstalować sterownik hello, jeśli nie jest już zainstalowany na komputerze bramy hello. Zobacz [włączenie łączności](#enabling-connectivity) sekcji, aby uzyskać szczegółowe informacje.

Przed użyciem hello historyk GE przechowywania w rozwiązaniu fabryki danych, należy sprawdzić, czy brama hello łączy toohello magazynu danych przy użyciu instrukcji w następnej sekcji hello.

Przeczytaj artykuł powitania od początku hello szczegółowe omówienie używania danych ODBC są przechowywane jako źródło danych magazynów w operacji kopiowania.  

## <a name="troubleshoot-connectivity-issues"></a>Rozwiązywanie problemów z połączeniem
problemy z połączeniem tootroubleshoot, użyj hello **diagnostyki** karcie **Menedżera konfiguracji bramy zarządzania danymi**.

1. Uruchom **Menedżera konfiguracji bramy zarządzania danymi**. Możesz uruchomić "C:\Program Files\Microsoft danych zarządzania Gateway\1.0\Shared\ConfigManager.exe" bezpośrednio (lub) wyszukiwania dla **bramy** toofind łącze zbyt**brama zarządzania danymi firmy Microsoft** Aplikacja, jak pokazano w powitania po obrazu.

    ![Brama wyszukiwania](./media/data-factory-odbc-connector/search-gateway.png)
2. Przełącz toohello **diagnostyki** kartę.

    ![Diagnostyki bramy](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Wybierz hello **typu** danych magazynu (połączonej usługi).
4. Określ **uwierzytelniania** , a następnie wprowadź **poświadczenia** (lub) wprowadź **ciąg połączenia** to magazyn danych toohello tooconnect używane.
5. Kliknij przycisk **połączenie testowe** magazynu danych toohello tootest hello połączenia.

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
