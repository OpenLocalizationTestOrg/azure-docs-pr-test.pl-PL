---
title: "aaaMove danych z lokalnego systemu plików HDFS | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Przenoszenia danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalnego systemu plików HDFS. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z magazynu danych zbiornika tooany obsługiwany system plików HDFS. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przenoszenia danych z lokalnego systemu plików HDFS tooother następującą liczbę magazynów danych, ale nie przenoszenia danych z innych danych tooan magazyny lokalny system plików HDFS.

> [!NOTE]
> Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego. Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello. 

## <a name="enabling-connectivity"></a>Włączenie łączności
Usługi fabryka danych obsługuje łączenia HDFS tooon lokalnych przy użyciu hello brama zarządzania danymi. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello. Użyj hello bramy tooconnect tooHDFS nawet wtedy, gdy jest ona hostowana w maszynie Wirtualnej platformy Azure IaaS.

> [!NOTE]
> Marka hello się zbyt dostęp brama zarządzania danymi**wszystkie** hello [nazwa węzła serwera]: [nazwa węzła portu] i [serwery węzła danych]: [port węzeł danych] hello klastra usługi Hadoop. Domyślne [nazwa węzła port] jest 50070, a domyślna [port węzeł danych] jest 50075.

Podczas instalowania bramy na powitania sam lokalnymi maszyny lub hello Azure VM hello systemu plików HDFS, zalecamy zainstalowanie bramy hello na oddzielnych maszyny/Azure IaaS maszyny Wirtualnej. Wystąpienia bramy na osobnym komputerze ogranicza rywalizację zasobów, poprawia wydajność. Po zainstalowaniu bramy hello na osobnym komputerze hello maszyny powinny być stanie tooaccess hello maszyny z hello systemu plików HDFS.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła systemu plików HDFS przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych systemu plików HDFS, zobacz [przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS tooAzure obiektu Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sekcji tego artykułu.

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooHDFS:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Połączona usługa łączy fabryki danych tooa magazynu danych. Tworzenie połączonej usługi typu **Hdfs** toolink lokalnego systemu plików HDFS tooyour usługi fabryka danych. Hello w poniższej tabeli przedstawiono opis usługi określonego tooHDFS połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **Hdfs** |Tak |
| Url |Adres URL toohello systemu plików HDFS |Tak |
| Typ authenticationType |Anonimowe lub Windows. <br><br> toouse **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć zbyt[w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) tooset się w lokalnym środowisku odpowiednio. |Tak |
| Nazwa użytkownika |Uwierzytelnianie nazwy użytkownika dla systemu Windows. |Tak (w przypadku uwierzytelniania systemu Windows) |
| hasło |Hasło dla uwierzytelniania systemu Windows. |Tak (w przypadku uwierzytelniania systemu Windows) |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać toohello tooconnect systemu plików HDFS. |Tak |
| encryptedCredential |[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello poświadczeń dostępu do danych wyjściowych. |Nie |

### <a name="using-anonymous-authentication"></a>Przy użyciu uwierzytelniania anonimowego

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Przy użyciu uwierzytelniania systemu Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **FileShare** (w tym system plików HDFS w zestawie danych) ma następujące właściwości hello

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Ścieżka folderu toohello. Przykład:`myfolder`<br/><br/>Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: <br/><br/>Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| partitionedBy |partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych. Przykład: folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

> [!NOTE]
> Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.

### <a name="using-partionedby-property"></a>Za pomocą właściwości partionedBy
Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).

toolearn więcej informacji na temat zestawów danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md), [planowanie i wykonanie](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md) artykułów.

#### <a name="sample-1"></a>Przykład 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona. Witaj SliceStart odwołuje się czas toostart hello wycinka. Witaj folderPath jest różne dla każdego wycinka. Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Przykład 2:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Dla działania kopiowania, gdy źródłem jest typu **FileSystemSource** hello następujące właściwości są dostępne w sekcji typeProperties:

**FileSystemSource** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

## <a name="supported-file-and-compression-formats"></a>Obsługiwane formaty plików i kompresji
Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS tooAzure obiektów Blob
W tym przykładzie pokazano sposób toocopy danych z lokalnego systemu plików HDFS tooAzure magazynu obiektów Blob. Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.  

przykład Witaj definicje JSON powitania po jednostek fabryki danych. Można użyć tych toocreate definicje danych toocopy potoku z systemu plików HDFS tooAzure magazynu obiektów Blob za pomocą [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Połączonej usługi typu [OnPremisesHdfs](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z lokalnego systemu plików HDFS tooan obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

Pierwszym krokiem należy skonfigurować bramę zarządzania danymi hello. Witaj instrukcjami hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.

**System plików HDFS połączonej usługi:** w tym przykładzie używa hello uwierzytelniania systemu Windows. Zobacz [HDFS połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Połączonej usługi magazynu Azure:**

```JSON
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

**System plików HDFS wejściowy zestaw danych:** ten zestaw danych odwołuje się folderu systemu plików HDFS toohello DataTransfer/UnitTest /. potok Hello kopiuje wszystkie pliki hello do tego miejsca docelowego toohello folderu.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Azure Blob wyjściowy zestaw danych:**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**

potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource** i **zbiornika** typu ustawiono zbyt**BlobSink**. Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Uwierzytelnianie Kerberos dla łącznika systemu plików HDFS
Istnieją dwie opcje tooset środowiska lokalne powitania tak toouse uwierzytelniania Kerberos w systemie plików HDFS łącznika. Możesz wybrać hello, co najlepiej pasuje do sprawę.
* Opcja 1: [maszyna bramy sprzężenia obszaru Kerberos](#kerberos-join-realm)
* Opcja 2: [włączyć wzajemnego zaufania między domeną systemu Windows i protokół Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opcja 1: Dołącz maszynę bramy obszaru Kerberos

#### <a name="requirement"></a>Wymaganie:

* Maszyna bramy Hello musi protokół Kerberos hello toojoin i nie można dołączyć do dowolnej domeny systemu Windows.

#### <a name="how-tooconfigure"></a>Jak tooconfigure:

**Na komputerze bramy:**

1.  Uruchom hello **Ksetup** tooconfigure narzędzie hello Centrum dystrybucji KLUCZY Kerberos serwera i obszar.

    Hello maszyny musi być skonfigurowany jako członek grupy roboczej, ponieważ obszaru Kerberos różni się od domeny systemu Windows. Można to osiągnąć przez ustawienie hello protokół Kerberos i dodanie serwera Centrum dystrybucji KLUCZY w następujący sposób. Zastąp *REALM.COM* z własnych odpowiednich obszaru zgodnie z potrzebami.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Uruchom ponownie** maszyny powitania po wykonaniu tych poleceń 2.

2.  Sprawdź konfigurację hello z **Ksetup** polecenia. dane wyjściowe Hello powinien być podobny do:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**W fabryce danych Azure:**

* Skonfigurować za pomocą łącznika systemu plików HDFS hello **uwierzytelniania systemu Windows** wraz z protokołu Kerberos główną nazwę i hasło tooconnect toohello HDFS źródła danych. Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.

### <a name="kerberos-mutual-trust"></a>Opcja 2: Włączanie wzajemnego zaufania między domeną systemu Windows i protokół Kerberos

#### <a name="requirement"></a>Wymaganie:
*   Maszyna bramy Hello musi zostać dołączony do domeny systemu Windows.
*   Potrzebne ustawienia uprawnień tooupdate hello kontrolera domeny.

#### <a name="how-tooconfigure"></a>Jak tooconfigure:

> [!NOTE]
> Zastąp REALM.COM i AD.COM w hello samouczka z własnych odpowiednich obszaru i kontroler domeny, zgodnie z potrzebami.

**Na serwerze Centrum dystrybucji KLUCZY:**

1.  Edytuje konfigurację Centrum dystrybucji KLUCZY hello w **krb5.conf** toolet pliku Centrum dystrybucji KLUCZY zaufania domeny systemu Windows, odwoływanie toohello następującego szablonu konfiguracji. Domyślnie program hello konfiguracji znajduje się pod adresem **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Uruchom ponownie** hello po konfiguracji Usługa Centrum dystrybucji KLUCZY.

2.  Przygotowanie podmiot zabezpieczeń o nazwie  **krbtgt/REALM.COM@AD.COM**  w Centrum dystrybucji KLUCZY serwera z hello następujące polecenie:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  W **hadoop.security.auth_to_local** konfigurację usługi systemu plików HDFS plików, dodawanie `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Na kontrolerze domeny:**

1.  Uruchom następujące hello **Ksetup** tooadd wpis obszaru polecenia:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Ustanowienie relacji zaufania z domeny systemu Windows tooKerberos obszaru. [hasło] jest hello hasła dla podmiotu hello  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Wybierz algorytm szyfrowania używany w protokole Kerberos.

    1. Przejdź tooServer Manager > Zarządzanie zasadami grupy > domeny > Obiekty zasad grupy > domyślny lub zasad domeny Active i edycji.

    2. W hello **Edytor zarządzania zasadami grupy** oknie podręcznym, przejdź tooComputer konfiguracji > zasady > Ustawienia systemu Windows > Ustawienia zabezpieczeń > Zasady lokalne > Opcje zabezpieczeń i skonfigurować **sieci zabezpieczenia: Konfigurowanie typów szyfrowania dozwolone dla protokołu Kerberos**.

    3. Algorytm szyfrowania wybierz hello ma toouse przy połączeniu tooKDC. Zazwyczaj można po prostu wybierz wszystkie opcje hello.

        ![Typy szyfrowania konfiguracji dla protokołu Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Użyj **Ksetup** polecenia toospecify hello szyfrowania algorytmu toobe używane na powitania określonego obszaru.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Utwórz główną w kolejności toouse głównej protokołu Kerberos w domenie systemu Windows hello mapowanie między hello konta domeny i protokołu Kerberos.

    1. Uruchamianie narzędzi administracyjnych hello > **użytkownicy usługi Active Directory i komputery**.

    2. Skonfiguruj zaawansowane funkcje, klikając **widoku** > **zaawansowanych funkcji**.

    3. Zlokalizuj hello konta toowhich toocreate mapowania, a następnie kliknij prawym przyciskiem myszy tooview **mapowania nazw** > kliknij **nazwy protokołu Kerberos** kartę.

    4. Dodaj podmiot zabezpieczeń z hello obszaru.

        ![Mapowania tożsamości zabezpieczeń](media/data-factory-hdfs-connector/map-security-identity.png)

**Na komputerze bramy:**

* Uruchom następujące hello **Ksetup** polecenia tooadd wpis obszaru.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**W fabryce danych Azure:**

* Skonfigurować za pomocą łącznika systemu plików HDFS hello **uwierzytelniania systemu Windows** wraz z Twojego konta domeny albo źródło danych systemu plików HDFS toohello tooconnect główna protokołu Kerberos. Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
