---
title: "aaaMove danych z usługi magazynowania proste Amazon przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z prostego Amazon usługi Storage (S3) przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Przenoszenia danych z usługi magazynowania proste Amazon przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello aktywności kopiowania w fabryce danych Azure toomove danych z usługi magazynowania proste Amazon (S3). Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.

Można skopiować danych z magazynu danych zbiornika tooany obsługiwane Amazon S3. Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. Fabryka danych aktualnie obsługuje tylko przenoszenia danych z baz danych tooother Amazon S3, ale nie przenoszenia danych z innych danych przechowuje tooAmazon S3.

## <a name="required-permissions"></a>Wymagane uprawnienia
toocopy danych z usługi Amazon S3, upewnij się, że zostały przyznane hello następujących uprawnień:

* `s3:GetObject`i `s3:GetObjectVersion` Amazon S3 obiektu operacji.
* `s3:ListBucket`operacjach Amazon S3 zasobnika. Jeśli używasz hello kreatora kopiowania fabryki danych `s3:ListAllMyBuckets` jest również wymagany.

Aby uzyskać więcej informacji o hello pełną listę uprawnień Amazon S3, zobacz [określanie uprawnień w zasadach](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potoku o działanie kopiowania, który przenosi dane ze źródła Amazon S3 przy użyciu różnych narzędzi lub interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Przewodnik Szybki, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Aby uzyskać instrukcje krok po kroku toocreate potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Czy za pomocą narzędzia lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych. Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych Amazon S3, zobacz hello [przykład JSON: kopiowanie danych z tooAzure Amazon S3 Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sekcji tego artykułu.

> [!NOTE]
> Aby uzyskać więcej informacji o obsługiwanych formatów plików i kompresji dla działania kopiowania, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md).

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAmazon S3.

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Połączona usługa łączy fabryki danych tooa magazynu danych. Tworzenie połączonej usługi typu **AwsAccessKey** toolink danych Amazon S3 przechowywać tooyour fabryki danych. Witaj w poniższej tabeli udostępnia usługę opis dla określonego tooAmazon elementów JSON S3 (AwsAccessKey) połączony.

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| accessKeyID |Identyfikator klucza tajnego dostępu hello. |Ciąg |Tak |
| secretAccessKey |klucz tajny dostępu Hello samej siebie. |Zaszyfrowanego ciągu tajny |Tak |

Oto przykład:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
toospecify toorepresent zestawu danych wejściowych danych w magazynie obiektów Blob platformy Azure, właściwość type hello zestawu DataSet hello zbyt**AmazonS3**. Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Amazon S3 połączonej usługi. Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md). 

Sekcje, takie jak struktury, dostępności i zasady są podobne dla wszystkich typów zestawu danych (takich jak bazy danych SQL, obiektów blob platformy Azure i tabeli platformy Azure). Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello. Witaj **typeProperties** sekcja dla zestawu danych typu **AmazonS3** (w tym dataset hello Amazon S3) ma następujące właściwości hello:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| bucketName |Nazwa pakietu Hello S3. |Ciąg |Tak |
| key |Klucz obiektu Hello S3. |Ciąg |Nie |
| Prefiks |Prefiks hello S3 obiektu klucza. Wybrano obiektów, w której klucze uruchomienia z tym prefiksem. Ma zastosowanie tylko wtedy, gdy klucz jest pusty. |Ciąg |Nie |
| Wersja |Wersja Hello hello S3 obiektu, jeśli włączono S3 przechowywania wersji. |Ciąg |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz, aby pliki toocopy-między opartych na plikach magazynów (kopia binarnego), Pomiń hello format sekcji w obu definicji zestawu danych wejściowych i wyjściowych. |Nie | |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Witaj, obsługiwane typy: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Witaj obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie | |


> [!NOTE]
> **bucketName + klawisz** Określa lokalizację hello hello S3 obiektu, którym zasobnika jest hello nadrzędny kontener dla obiektów S3, a klucz hello pełną ścieżkę toohello S3 obiektu.

### <a name="sample-dataset-with-prefix"></a>Przykładowego zestawu danych z prefiksem

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Przykładowego zestawu danych (z wersją)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Dynamiczne ścieżki S3
Witaj powyższego przykładu użyto stałej wartości dla hello **klucza** i **bucketName** właściwości w elemencie dataset hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Program może obliczyć te właściwości dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Możesz zrobić hello takie same dla hello **prefiks** właściwości Amazon S3 zestawu danych. Aby uzyskać listę obsługiwanych funkcji i zmiennych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md). Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań. Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania. Dla działania kopiowania hello właściwości różnią się w zależności od typów hello źródeł i sink. Gdy źródła w przypadku działania kopiowania hello jest typu **FileSystemSource** (która obejmuje Amazon S3), hello następujące właściwości są dostępne w **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Określa, czy lista toorecursively S3 obiekty w katalogu hello. |wartość true, false |Nie |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Przykład JSON: kopiowanie danych z tooAzure Amazon S3 magazynu obiektów Blob
W tym przykładzie pokazano sposób toocopy danych z tooan Amazon S3 magazynu obiektów Blob platformy Azure. Jednak dane mogą być kopiowane bezpośrednio za[żadnego wychwytywanie hello, które są obsługiwane](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania hello w fabryce danych.

przykład Witaj definicje JSON powitania po jednostek fabryki danych. Te definicje toocreate potoku toocopy danych z magazynu tooBlob Amazon S3, można użyć przy użyciu hello [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Połączonej usługi typu [AwsAccessKey](#linked-service-properties).
* Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AmazonS3](#dataset-properties).
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z tooan Amazon S3 obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

### <a name="amazon-s3-linked-service"></a>Usługi Amazon S3 połączone

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage

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

### <a name="amazon-s3-input-dataset"></a>Zestaw danych wejściowych Amazon S3

Ustawienie **"external": true** informuje usługi fabryka danych hello tego zestawu danych hello jest zewnętrznych toohello fabryki danych. Wejściowy zestaw danych, który nie jest generowany przez działania w potoku hello ustawić tootrue tej właściwości.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1). Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana. Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Działanie kopiowania w potoku ze źródłem Amazon S3 i ujście obiektów blob

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**, i **zbiornika** typu ustawiono zbyt**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).


## <a name="next-steps"></a>Następne kroki
Zobacz następujące artykuły hello:

* toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) w fabryce danych i różne sposoby toooptimize, zobacz hello [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).

* Aby uzyskać instrukcje tworzenia potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
