---
title: "aaaMove danych z serwera FTP przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z serwera FTP przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Przenoszenie danych z serwera FTP przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello aktywności kopiowania w fabryce danych Azure toomove danych z serwera FTP. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z magazynu FTP serwera tooany obsługiwane ujścia danych. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przechowuje przenoszenia danych z danych tooother serwera FTP, ale nie przenoszenia danych z innych danych są przechowywane na serwerze tooan FTP. Obsługuje ona zarówno lokalnie i w chmurze, serwerami FTP.

> [!NOTE]
> działanie kopiowania Hello nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego. Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, należy utworzyć plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello. 

## <a name="enable-connectivity"></a>Włącz połączenie
Jeśli przenosisz dane z **lokalnymi** magazynu danych chmury tooa serwera FTP (na przykład tooAzure magazynu obiektów Blob), zainstalować i używać bramy zarządzania danymi. Witaj brama zarządzania danymi jest agent klienta, który jest zainstalowany na komputerze lokalnym i umożliwia chmury usługi tooconnect tooan lokalnych zasobów. Aby uzyskać więcej informacji, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md). Aby uzyskać instrukcje krok po kroku na temat ustawiania hello bramy i przy jego użyciu, zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md). Używasz powitania serwera tooan FTP tooconnect bramy, nawet jeśli serwer hello znajduje się na infrastrukturę platformy Azure jako usługa (IaaS) maszynę wirtualną (VM).

Jest możliwe tooinstall hello bramy na powitania sam lokalnymi maszyny lub maszyn wirtualnych IaaS hello serwera FTP. Jednak zaleca się zainstalowanie bramy hello na osobnym komputerze fizycznym lub maszyn wirtualnych IaaS tooavoid rywalizacji i w celu zapewnienia lepszej wydajności. Po zainstalowaniu bramy hello na osobnym komputerze maszyny hello powinien być serwer FTP hello tooaccess stanie.

## <a name="get-started"></a>Rozpoczęcie pracy
Można utworzyć potoku o działanie kopiowania, który przenosi dane ze źródła FTP przy użyciu różnych narzędzi lub interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania fabryki danych**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) Przewodnik Szybki.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **PowerShell**, **szablonu usługi Azure Resource Manager**, **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.

Czy za pomocą narzędzia hello lub interfejsów API, wykonaj następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych. Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych FTP, zobacz hello [przykład JSON: kopiowanie danych z obiektu blob tooAzure serwera FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) sekcji tego artykułu.

> [!NOTE]
> Aby uzyskać szczegółowe informacje o obsługiwanych toouse formaty plików i ich kompresji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md).

Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooFTP.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Witaj w poniższej tabeli opisano usługi FTP połączone tooan określone elementy JSON.

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| type |Ustaw ten tooFtpServer. |Tak |&nbsp; |
| Host |Określ nazwę hello lub adres IP powitania serwera FTP. |Tak |&nbsp; |
| Typ authenticationType |Określ typ uwierzytelniania hello. |Tak |Basic anonimowe |
| nazwa użytkownika |Określ hello użytkownik, który ma serwer FTP toohello dostępu. |Nie |&nbsp; |
| hasło |Określ hasło hello hello użytkownika (username). |Nie |&nbsp; |
| encryptedCredential |Określ serwer hello FTP tooaccess poświadczeń hello szyfrowane. |Nie |&nbsp; |
| gatewayName |Określ nazwę hello hello bramy w serwer FTP lokalnymi tooan tooconnect brama zarządzania danymi. |Nie |&nbsp; |
| port |Określ port hello, na które hello FTP nasłuchuje serwer. |Nie |21 |
| enableSsl |Określ, czy toouse FTP za pośrednictwem kanału SSL/TLS. |Nie |Wartość true |
| enableServerCertificateValidation |Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli używasz FTP za pośrednictwem kanału SSL/TLS. |Nie |Wartość true |

### <a name="use-anonymous-authentication"></a>Uwierzytelnianie anonimowe

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Użyj nazwy użytkownika i hasła w postaci zwykłego tekstu dla uwierzytelniania podstawowego

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Użyj portu, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>EncryptedCredential używany do uwierzytelniania i bramy

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md). Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.

Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych. Zawiera informacje, które jest toohello określonego typu dataset. Witaj **typeProperties** sekcja dla zestawu danych typu **FileShare** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Folder toohello podrzędną. Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** ścieżki folderu toohave oparte na wycinku rozpoczęcia i zakończenia daty i godziny. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Gdy **fileName** nie jest określony dla wyjściowego zestawu danych, nazwa hello hello wygenerowany plik jest zgodny z formatem hello: <br/><br/>Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nie |
| obiektu fileFilter |Określ filtr tooselect toobe używane podzbiór plików w hello **folderPath**, a nie wszystkich plików.<br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1:`"fileFilter": "*.log"`<br/>Przykład 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> **obiektu fileFilter** dotyczy wejściowy zestaw danych z udziału plików. Ta właściwość nie jest obsługiwana z Hadoop Distributed pliku System (HDFS). |Nie |
| partitionedBy |Używane toospecify dynamicznym **folderPath** i **fileName** czasu serii danych. Na przykład można określić **folderPath** który jest sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz toocopy pliki, są one między magazynów opartych na plikach (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**, i są obsługiwane poziomy **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |
| useBinaryTransfer |Określ, czy dane binarne hello toouse tryb transferu. Witaj wartości to PRAWDA dla trybu binarnego (jest to wartość domyślna hello), a wartość false dla ASCII. Ta właściwość jest używana tylko w przypadku hello typu skojarzonej połączonej usługi typu: SerwerFTP. |Nie |

> [!NOTE]
> **Nazwa pliku** i **obiektu fileFilter** nie mogą być używane jednocześnie.

### <a name="use-hello-partionedby-property"></a>Użyj właściwości partionedBy hello
Jak wspomniano w poprzedniej sekcji hello, można określić dynamicznym **folderPath** i **fileName** czasu serii danych z hello **partitionedBy** właściwości.

toolearn dotyczące zestawów danych serii czasu, planowania i wycinków, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md), [planowania i wykonywania](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Przykład 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart, w hello z formatem określonym (YYYYMMDDHH). Witaj SliceStart odwołuje się czas toostart hello wycinka. Ścieżka folderu Hello jest różne dla każdego wycinka. (Na przykład wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104).

#### <a name="sample-2"></a>Przykład 2

```json
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
W tym przykładzie hello rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez hello **folderPath** i **fileName** właściwości.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md). Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości dostępne w hello **typeProperties** sekcji hello działania na powitania drugiej strony, zależą od każdego typu działania. Dla działania kopiowania hello właściwości typu hello zależy od typów hello źródeł i sink.

W przypadku działania kopiowania, gdy źródłem hello jest typu **FileSystemSource**, hello następujące właściwości są dostępne w **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Przykład JSON: kopiowanie danych z tooAzure serwera FTP obiektów Blob
W tym przykładzie pokazano sposób toocopy danych z tooAzure serwera FTP magazynu obiektów Blob. Jednak dane mogą być kopiowane bezpośrednio tooany hello wychwytywanie hello podane w [obsługiwane formaty i magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats), za pomocą działania kopiowania hello w fabryce danych.  

Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Połączonej usługi typu [SerwerFTP](#linked-service-properties)
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [udziału plików](#dataset-properties)
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

przykład Witaj kopiuje dane z tooan serwera FTP obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

### <a name="ftp-linked-service"></a>Połączona usługa FTP

W tym przykładzie używane uwierzytelnianie podstawowe, hello nazwy użytkownika i hasła w postaci zwykłego tekstu. Można także użyć jednej z hello następujące sposoby:

* Uwierzytelnianie anonimowe
* Uwierzytelnianie podstawowe z zaszyfrowane poświadczenia
* FTP over SSL/TLS (FTPS)

Zobacz hello [FTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage

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
### <a name="ftp-input-dataset"></a>Zestaw danych wejściowych FTP

Ten zestaw danych odwołuje się folder toohello FTP `mysharedfolder` i plik `test.csv`. Witaj potoku kopie hello toohello docelowej lokalizacji plików.

Ustawienie **zewnętrznych** za**true** informuje usługi fabryka danych hello tego zestawu danych hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello obiektu blob hello dynamicznie jest obliczane, na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Działanie kopiowania w potoku z zbiornika źródła i obiektów blob systemu plików

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**i hello **zbiornika** typu ustawiono zbyt**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="next-steps"></a>Następne kroki
Zobacz następujące artykuły hello:

* toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) w fabryce danych i różne sposoby toooptimize, zobacz hello [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).

* Aby uzyskać instrukcje tworzenia potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
