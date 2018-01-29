---
title: "Kopiowanie danych z i do przechowywania plików Azure przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z Azure File Storage do zbiornika obsługiwanych magazynów danych (lub) obsługiwanej źródłowej magazyny danych do magazynu plików Azure przy użyciu fabryki danych Azure."
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
ms.date: 11/09/2017
ms.author: jingwang
ms.openlocfilehash: b3f093f84758fe8622f09212b6a11a2c5f3795aa
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-or-to-azure-file-storage-by-using-azure-data-factory"></a>Kopiowanie danych z lub do magazynu plików Azure przy użyciu fabryki danych Azure

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane z i do przechowywania plików Azure (pliki Azure). Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [działanie kopiowania w wersji 1](v1/data-factory-data-movement-activities.md).

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Możesz skopiować dane z usługi Magazyn plików Azure żadnych obsługiwanych ujścia magazynu danych lub skopiować dane z dowolnego źródła obsługiwanych magazynu danych do magazynu plików Azure. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

W szczególności ten łącznik Azure File Storage obsługuje kopiowanie plików jako — jest lub analizowania/Generowanie plików z [obsługiwane formaty plików i kodery-dekodery kompresji](supported-file-formats-and-compression-codecs.md).

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonych do przechowywania plików Azure.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Obsługiwane są następujące właściwości dla pliku połączoną usługą magazynu Azure:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **plików**. | Yes |
| host | Określa punkt końcowy magazyn plików Azure jako `"host": "\\\\<storage name>.file.core.windows.net\\<file service name>"`. | Yes |
| Nazwa użytkownika | Określ użytkownika, dostęp do magazynu plików Azure jako `"userid": "AZURE\\<storage name>"`. | Yes |
| hasło | Określ klucz dostępu do magazynu. Zaznacz to pole jako SecureString.<br/> | Yes |
| connectVia | [Integrację środowiska uruchomieniowego](concepts-integration-runtime.md) ma być używany do nawiązania połączenia z magazynem danych. (Jeśli w magazynie danych znajduje się w sieci prywatnej), można użyć środowiska uruchomieniowego integracji Azure lub Self-hosted integracji w czasie wykonywania. Jeśli nie zostanie określony, używa domyślnej środowiska uruchomieniowego integracji Azure. |Brak źródła tak dla obiekt sink |

>[!IMPORTANT]
> - Aby skopiować dane do usługi Magazyn plików Azure przy użyciu środowiska uruchomieniowego integracji Azure, jawnie [utworzyć IR Azure](create-azure-integration-runtime.md#create-azure-ir) z lokalizacją przechowywania plików i kojarzenie w połączonej usłudze jako poniższym przykładzie.
> - Aby skopiować dane z/na magazyn plików Azure przy użyciu środowiska uruchomieniowego integracji Self-hosted poza platformą Azure, pamiętaj, aby otworzyć port wychodzący TCP 445 w sieci lokalnej.

**Przykład:**

```json
{
    "name": "AzureFileStorageLinkedService",
    "properties": {
        "type": "FileServer",
        "typeProperties": {
            "host": "\\\\<storage name>.file.core.windows.net\\<file service name>",
            "userid": "AZURE\\<storage name>",
            "password": {
                "type": "SecureString",
                "value": "<storage access key>"
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

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje zobacz artykuł zestawów danych. Ta sekcja zawiera listę właściwości obsługiwane przez Magazyn plików Azure zestawu danych.

Aby skopiować dane z i do przechowywania plików Azure, ustaw właściwość Typ zestawu danych do **FileShare**. Obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type zestawu danych: **udziału plików** |Yes |
| folderPath | Ścieżka do folderu. |Yes |
| fileName | Określ nazwę pliku w **folderPath** Jeśli chcesz skopiować do/z określonego pliku. Nie określaj żadnej wartości dla tej właściwości, zestaw danych wskazuje wszystkie pliki w folderze jako źródło i automatycznie generuje nazwę pliku.<br/><br/>**Nazwa pliku automatycznego generowania dla obiekt sink:** gdy nie określono nazwy pliku dla wyjściowego zestawu danych i **preserveHierarchy** nie została określona w zbiornika działania działanie kopiowania generuje nazwę pliku z następującego wzorca: <br/>- `Data_[activity run id]_[GUID].[format].[compression if configured]`. Na przykład: `Data_0a405f8a-93ff-4c6f-b3be-f69616f1df7a_0d143eda-d5b8-44df-82ec-95c50895ff80.txt.gz` <br/>- lub `[Table name].[format].[compression if configured]` dla relacyjnego źródła, gdy zapytanie nie jest określona. Na przykład: MySourceTable.orc. |Nie |
| obiektu fileFilter | Określ filtr służący do wybierania podzbioru pliki w ścieżce folderu, a nie wszystkie pliki. Ma zastosowanie tylko wtedy, gdy nie jest określona nazwa pliku. <br/><br/>Dozwolone symbole wieloznaczne są: `*` (wielu znaków) i `?` (pojedynczy znak).<br/>— Przykład 1:`"fileFilter": "*.log"`<br/>— Przykład 2:`"fileFilter": 2017-09-??.txt"` |Nie |
| Format | Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.<br/><br/>Jeśli chcesz przeanalizować lub wygenerować pliki w określonym formacie, obsługiwane są następujące typy plików w formacie: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Ustaw **typu** właściwości w formacie do jednej z tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](supported-file-formats-and-compression-codecs.md#text-format), [formatu Json](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), i [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sekcje. |Nie (tylko w przypadku scenariusza kopiowania binarny) |
| Kompresja | Określ typ i poziom kompresji danych. Aby uzyskać więcej informacji, zobacz [obsługiwane formaty plików i kodery-dekodery kompresji](supported-file-formats-and-compression-codecs.md#compression-support).<br/>Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.<br/>Obsługiwane poziomy: **optymalna** i **najszybciej**. |Nie |

**Przykład:**

```json
{
    "name": "AzureFileStorageDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName":{
            "referenceName": "<Azure File Storage linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "folder/subfolder/",
            "fileName": "myfile.csv.gz",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez Magazyn plików Azure źródłowy i odbiorczy właściwości.

### <a name="azure-file-storage-as-source"></a>Magazyn plików Azure jako źródła

Aby skopiować dane z usługi Magazyn plików Azure, należy ustawić typ źródła w przypadku działania kopiowania do **FileSystemSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **FileSystemSource** |Yes |
| Cykliczne | Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu. Uwaga: po cykliczne ma ustawioną wartość PRAWDA, a obiekt sink jest magazynu opartych na plikach, pusty folder/podrzędne-folder nie będą kopiowane utworzone w ujścia.<br/>Dozwolone wartości to: **true** (ustawienie domyślne), **false** | Nie |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyFromAzureFileStorage",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure File Storage input dataset name>",
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
                "type": "FileSystemSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="azure-file-storage-as-sink"></a>Magazyn plików Azure jako odbioru

Aby skopiować dane do magazynu plików Azure, należy ustawić typ ujścia w działaniu kopiowania do **FileSystemSink**. Następujące właściwości są obsługiwane w **zbiornika** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość typu sink działania kopiowania: **FileSystemSink** |Yes |
| copyBehavior | Określa zachowanie kopiowania, gdy źródłem jest pliki z magazynu danych opartych na plikach.<br/><br/>Dozwolone wartości to:<br/><b>-PreserveHierarchy (ustawienie domyślne)</b>: zachowuje hierarchię plików w folderze docelowym. Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.<br/><b>-FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego znajdują się w pierwszym poziomem folderu docelowego. Pliki docelowe mają automatycznie wygeneruje nazwę. <br/><b>-MergeFiles</b>: scala wszystkie pliki z folderu źródłowego do jednego pliku. Jeśli zostanie określona nazwa pliku/obiektów Blob, nazwa scalony plik jest określona nazwa; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie. | Nie |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyToAzureFileStorage",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure File Storage output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "FileSystemSink",
                "copyBehavior": "PreserveHierarchy"
            }
        }
    }
]
```

### <a name="recursive-and-copybehavior-examples"></a>Przykłady cyklicznego i copyBehavior

W tej sekcji opisano efekty operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.

| Cykliczne | copyBehavior | Struktura folderów źródła | Wynikowa docelowego |
|:--- |:--- |:--- |:--- |
| prawda |preserveHierarchy | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | folder docelowy Folder1 jest tworzony z tej samej struktury jako źródło:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| prawda |flattenHierarchy | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | element docelowy Folder1, utworzono o następującej strukturze: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5 |
| prawda |mergeFiles | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | element docelowy Folder1, utworzono o następującej strukturze: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie |
| fałsz |preserveHierarchy | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | folder docelowy Folder1 jest tworzony o następującej strukturze<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| fałsz |flattenHierarchy | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | folder docelowy Folder1 jest tworzony o następującej strukturze<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2<br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |
| fałsz |mergeFiles | Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | folder docelowy Folder1 jest tworzony o następującej strukturze<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie. Nazwa wygenerowana automatycznie Plik1<br/><br/>Subfolder1 plik3, File4 i File5 nie są odczytywane. |

## <a name="next-steps"></a>Kolejne kroki
Lista magazynów danych obsługiwane jako źródła i wychwytywanie przez działanie kopiowania w fabryce danych Azure, zobacz [obsługiwane magazyny danych](copy-activity-overview.md##supported-data-stores-and-formats).