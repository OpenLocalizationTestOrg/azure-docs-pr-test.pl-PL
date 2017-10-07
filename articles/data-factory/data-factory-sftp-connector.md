---
title: "aaaMove danych z serwera SFTP przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z lokalnymi lub serwer SFTP chmury przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Przenoszenie danych z serwera SFTP przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tooa serwera SFTP na lokalnej/w chmurze obsługiwana ujścia magazynu danych. W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.

Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother serwera SFTP przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SFTP serwera. Obsługuje ona zarówno lokalnie i w chmurze. serwery SFTP.

> [!NOTE]
> Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego. Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello. 

## <a name="supported-scenarios-and-authentication-types"></a>Obsługiwane scenariusze i typy uwierzytelniania
Można użyć tych danych toocopy łącznika SFTP z **zarówno w chmurze SFTP serwerów i serwerów lokalnych SFTP**. **Podstawowe** i **parametry SshPublicKey** podczas łączenia serwera SFTP toohello są obsługiwane typy uwierzytelniania.

Podczas kopiowania danych z lokalnego serwera SFTP, należy zainstalować bramę zarządzania danymi w środowisku lokalnymi hello/Azure maszyny Wirtualnej. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) szczegółowe informacje na temat hello bramy. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykuł, aby uzyskać szczegółowe instrukcje dotyczące konfigurowania bramy hello i przy jego użyciu.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła SFTP przy użyciu różnych narzędzi/interfejsów API.

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. Dla formatu JSON przykłady toocopy danych z tooAzure serwera SFTP magazynu obiektów Blob, zobacz [przykład JSON: kopiowanie danych z obiektu blob tooAzure serwera SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) sekcji tego artykułu.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooFTP połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| type | zbyt należy ustawić właściwość typu Hello`Sftp`. |Tak |
| Host | Nazwa lub adres IP serwera SFTP hello. |Tak |
| port |Port, na którym hello SFTP serwer nasłuchuje. Witaj, wartość domyślna to: 21 |Nie |
| Typ authenticationType |Określ typ uwierzytelniania. Dozwolone wartości: **podstawowe**, **parametry SshPublicKey**. <br><br> Odwołuje się zbyt[używanie uwierzytelniania podstawowego](#using-basic-authentication) i [przy użyciu publicznego klucza uwierzytelniania SSH](#using-ssh-public-key-authentication) odpowiednio sekcje więcej właściwości i przykłady JSON. |Tak |
| skipHostKeyValidation | Określ, czy tooskip hosta klucza weryfikacji. | Nie. Witaj wartość domyślna: false |
| hostKeyFingerprint | Podaj odcisk palca hello hello klucza hosta. | Tak, jeśli hello `skipHostKeyValidation` ustawiono toofalse.  |
| gatewayName |Nazwa tooan tooconnect brama zarządzania danymi hello SFTP serwerem lokalnym. | Tak, jeśli kopiowanie danych z lokalnego serwera SFTP. |
| encryptedCredential | Serwer protokołu SFTP hello tooaccess zaszyfrowane poświadczenia. Wygenerowany automatycznie po określeniu opcji Uwierzytelnianie podstawowe (nazwy użytkownika i hasła) lub uwierzytelniania parametry SshPublicKey (nazwy użytkownika i ścieżki do klucza prywatnego lub zawartości) kopiowania kreatora lub hello ClickOnce podręcznego okna dialogowego. | Nie. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP. |

### <a name="using-basic-authentication"></a>Przy użyciu uwierzytelniania podstawowego

Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `Basic`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| nazwa użytkownika | Użytkownik, który ma dostęp toohello SFTP serwera. |Tak |
| hasło | Hasło dla użytkownika hello (nazwa_użytkownika). | Tak |

#### <a name="example-basic-authentication"></a>Przykład: Uwierzytelnianie podstawowe
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Przykład: Uwierzytelnianie podstawowe z zaszyfrowanych poświadczeniach

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Przy użyciu uwierzytelniania klucza publicznego SSH

Ustaw toouse SSH uwierzytelniania klucza publicznego, `authenticationType` jako `SshPublicKey`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| nazwa użytkownika |Użytkownik, który ma dostęp toohello SFTP serwera |Tak |
| privateKeyPath | Określ ścieżkę bezwzględną toohello pliku klucza prywatnego może dostęp do tej bramy. | Określ albo hello `privateKeyPath` lub `privateKeyContent`. <br><br> Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP. |
| privateKeyContent | Zserializowany ciąg hello prywatnego klucza zawartości. Witaj kreatora kopiowania może odczytywać hello pliku klucza prywatnego i Wyodrębnij zawartość klucza prywatnego hello automatycznie. Jeśli używane są wszystkie inne narzędzie/pakiet SDK, należy użyć właściwości privateKeyPath hello. | Określ albo hello `privateKeyPath` lub `privateKeyContent`. |
| Hasło | Określ hello przebiegu frazy/hasło toodecrypt hello prywatny klucz, jeśli plik klucza hello jest chroniony przez hasło. | Tak, czy plik klucza prywatnego hello jest chroniony przez hasło. |

> [!NOTE]
> Łącznik SFTP obsługują tylko klucz OpenSSH. Upewnij się, że plik klucza jest w nieprawidłowym formacie hello. Możesz użyć narzędzia Putty tooconvert z formatu tooOpenSSH ppk.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Przykład: Parametry SshPublicKey uwierzytelnianie przy użyciu filePath klucza prywatnego

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Przykład: Parametry SshPublicKey uwierzytelniania za pomocą prywatnego klucza zawartości

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.

Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych. Zawiera informacje, które jest toohello określonego typu dataset. Hello typeProperties sekcja dla zestawu danych typu **FileShare** dataset zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Folder toohello ścieżki Sub. Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: <br/><br/>Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| obiektu fileFilter |Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.<br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1:`"fileFilter": "*.log"`<br/>Przykład 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików. Ta właściwość nie jest obsługiwana z systemu plików HDFS. |Nie |
| partitionedBy |partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych. Na przykład folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |
| useBinaryTransfer |Określ, czy używany tryb transferu binarnego. Wartość true dla trybie binarnym i wartość false ASCII. Wartość domyślna: wartość True. Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP. |Nie |

> [!NOTE]
> Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.

### <a name="using-partionedby-property"></a>Za pomocą właściwości partionedBy
Jak wspomniano w poprzedniej sekcji hello, można określić dynamiczne folderPath, nazwę pliku dla danych szeregów czasowych ze partitionedBy. Możesz to zrobić z hello makra fabryki danych i zmiennej systemowej hello SliceStart, SliceEnd sygnalizujące hello logicznej okresu wycinek podanych danych.

toolearn dotyczące zestawów danych serii czasu, planowania i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md), [planowanie i wykonanie](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md) artykułów.

#### <a name="sample-1"></a>Przykład 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona. Witaj SliceStart odwołuje się czas toostart hello wycinka. Witaj folderPath jest różne dla każdego wycinka. Przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Przykład 2:

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
W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości hello dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania właściwości typu hello zależy od typów hello źródeł i sink.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Obsługiwane formaty plików i kompresji
Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Przykład JSON: Kopiowanie danych z obiektu blob tooAzure serwera SFTP
Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy danych z użyciem protokołu SFTP źródła tooAzure magazynu obiektów Blob. Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.

> [!IMPORTANT]
> W tym przykładzie przedstawiono fragmenty kodu JSON. Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych. Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.

przykład Witaj ma hello następujące obiekty fabryki danych:

* Połączonej usługi typu [sftp](#linked-service-properties).
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z tooan serwera SFTP obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

**Usługa SFTP połączone**

W tym przykładzie używane uwierzytelnianie podstawowe hello z nazwy użytkownika i hasła w postaci zwykłego tekstu. Można także użyć jednej z hello następujące sposoby:

* Uwierzytelnianie podstawowe z zaszyfrowane poświadczenia
* Uwierzytelnianie klucza publicznego SSH

Zobacz [FTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Połączona usługa Azure Storage**

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
**Zestaw danych wejściowych SFTP**

Ten zestaw danych odwołuje się toohello SFTP folder `mysharedfolder` i plik `test.csv`. Witaj potoku kopie hello toohello docelowej lokalizacji plików.

Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Blob wyjściowy zestaw danych**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**W potoku z działanie kopiowania**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.

## <a name="next-steps"></a>Następne kroki
Zobacz następujące artykuły hello:

* [Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.
