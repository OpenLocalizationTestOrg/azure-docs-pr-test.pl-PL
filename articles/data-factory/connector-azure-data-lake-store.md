---
title: "Kopiowanie danych do/z usługi Azure Data Lake Store przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z obsługiwanej źródłowej magazyny danych do usługi Azure Data Lake Store (lub) z usługi Data Lake Store sklepów zbiornika obsługiwane przy użyciu fabryki danych."
services: data-factory
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 12/07/2017
ms.author: jingwang
ms.openlocfilehash: c388fe0cfe85ec2bf2b752f74d39eb2ebe38ceb1
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/17/2018
---
# <a name="copy-data-to-or-from-azure-data-lake-store-by-using-azure-data-factory"></a>Kopiowanie danych do i z usługi Azure Data Lake Store przy użyciu fabryki danych Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-azure-datalake-connector.md)
> * [Wersja 2 — wersja zapoznawcza](connector-azure-data-lake-store.md)

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane do i z usługi Azure Data Lake Store. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [łącznika usługi Azure Data Lake Store w wersji 1](v1/data-factory-azure-datalake-connector.md).

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Kopiowanie danych z dowolnego źródła obsługiwanych magazynu danych do usługi Azure Data Lake Store lub skopiować dane z usługi Azure Data Lake Store żadnych obsługiwanych ujścia magazynu danych. Lista magazynów danych, które są obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

W szczególności ten łącznik usługi Azure Data Lake Store obsługuje:

- Kopiowanie plików za pomocą **nazwy głównej usługi** lub **tożsamość usługi (MSI) zarządzanej** uwierzytelniania.
- Kopiowanie plików jako — jest lub analizowania/Generowanie plików z [obsługiwane formaty plików i kodery-dekodery kompresji](supported-file-formats-and-compression-codecs.md).

## <a name="get-started"></a>Rozpoczęcie pracy

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do usługi Azure Data lake Store.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Następujące właściwości są obsługiwane przez usługi Azure Data Lake Store połączonej usługi:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną **AzureDataLakeStore**. | Yes |
| dataLakeStoreUri | Informacje o koncie usługi Azure Data Lake Store. Informacja ta ma jeden z następujących formatów: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`. | Yes |
| dzierżawa | Określ informacje dzierżawy (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja. Można go pobrać, ustawiając kursor myszy w prawym górnym rogu portalu Azure. | Yes |
| subscriptionId | Identyfikator subskrypcji platformy Azure, do której należy konto usługi Data Lake Store. | Wymagany dla odbiorcy |
| resourceGroupName | Nazwa grupy zasobów platformy Azure, do której należy konto usługi Data Lake Store. | Wymagany dla odbiorcy |
| connectVia | [Integrację środowiska uruchomieniowego](concepts-integration-runtime.md) ma być używany do nawiązania połączenia z magazynem danych. (Jeśli w magazynie danych znajduje się w sieci prywatnej), można użyć środowiska uruchomieniowego integracji Azure lub Self-hosted integracji w czasie wykonywania. Jeśli nie zostanie określony, używa domyślnej środowiska uruchomieniowego integracji Azure. |Nie |

Odpowiednio można znaleźć w poniższych sekcjach więcej właściwości i JSON próbek różnymi typami uwierzytelniania:

- [Przy użyciu uwierzytelniania głównej usługi](#using-service-principal-authentication)
- [Uwierzytelnianie tożsamości zarządzanych usług](#using-managed-service-identity-authentication)

### <a name="using-service-principal-authentication"></a>Przy użyciu uwierzytelniania głównej usługi

Aby używać uwierzytelniania głównej usługi, Zarejestruj podmiot aplikacji w usłudze Azure Active Directory (Azure AD) i przyznać jej dostęp do usługi Data Lake Store. Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Zwróć uwagę na następujące wartości, które służą do definiowania połączonej usługi:

- Identyfikator aplikacji
- Klucz aplikacji
- Identyfikator dzierżawy

>[!IMPORTANT]
> Upewnij się, że można przydzielić usługi głównej odpowiednie uprawnienia w usłudze Azure Data Lake Store:
>- **Jako źródło**, przyznaj co najmniej **Odczyt i wykonywanie** uprawnienia do listy, a następnie skopiuj zawartość folderu, dostępu do danych lub **odczytu** uprawnień do kopiowania pojedynczy plik. Nie jest wymagany na kontroli dostępu na poziomie konta (IAM).
>- **Jako obiekt sink**, przyznaj co najmniej **zapisu i wykonywania** uprawnienia do tworzenia elementów podrzędnych w folderze dostępu do danych. I jeśli Azure IR służy do kopiowania (źródłowy i odbiorczy znajdują się w chmurze), aby umożliwić wykryć Data Lake Store regionu fabryki danych, co najmniej przyznać **czytnika** roli w kontroli dostępu do konta (IAM). Aby uniknąć tej roli IAM jawnie [utworzyć IR Azure](create-azure-integration-runtime.md#create-azure-ir) z lokalizacją Twojej usługi Data Lake Store i skojarz w usłudze Data Lake Store połączonej usługi, jak w poniższym przykładzie:

Obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| servicePrincipalId | Określ identyfikator aplikacji klienta. | Yes |
| servicePrincipalKey | Określ klucz aplikacji. Zaznacz to pole jako SecureString. | Yes |

**Przykład:**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": {
                "type": "SecureString",
                "value": "<service principal key>"
            },
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="using-managed-service-identity-authentication"></a>Uwierzytelnianie tożsamości zarządzanych usług

Fabryka danych może być skojarzony z [tożsamość usługi zarządzanej](data-factory-service-identity.md), reprezentuje tej fabryki danych. Ta tożsamość usługi można korzystać bezpośrednio do uwierzytelniania usługi Data Lake Store, podobnie jak przy użyciu własnego nazwy głównej usługi. Umożliwia tej fabryki wyznaczonych do dostępu i skopiować dane z/do usługi Data Lake Store.

Aby używać uwierzytelniania tożsamości (MSI) zarządzanych usług:

1. [Pobieranie tożsamości usługi fabryka danych](data-factory-service-identity.md#retrieve-service-identity) przez skopiowanie wartości "Usługa tożsamości aplikacji Identyfikatora" generowane wraz z fabryką.
2. Udziel dostępu do tożsamości usługi Data Lake Store w taki sam sposób jak w przypadku nazwy głównej usługi. Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania, aplikacji Przypisz usługi Azure AD do usługi Azure Data Lake Store konta pliku lub folderu](../data-lake-store/data-lake-store-service-to-service-authenticate-using-active-directory.md#step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder).

>[!IMPORTANT]
> Upewnij się, że można przydzielić danych fabryki usługi tożsamości odpowiednie uprawnienia w usłudze Azure Data Lake Store:
>- **Jako źródło**, przyznaj co najmniej **Odczyt i wykonywanie** uprawnienia do listy, a następnie skopiuj zawartość folderu, dostępu do danych lub **odczytu** uprawnień do kopiowania pojedynczy plik. Nie jest wymagany na kontroli dostępu na poziomie konta (IAM).
>- **Jako obiekt sink**, przyznaj co najmniej **zapisu i wykonywania** uprawnienia do tworzenia elementów podrzędnych w folderze dostępu do danych. I jeśli Azure IR służy do kopiowania (źródłowy i odbiorczy znajdują się w chmurze), aby umożliwić wykryć Data Lake Store regionu fabryki danych, co najmniej przyznać **czytnika** roli w kontroli dostępu do konta (IAM). Aby uniknąć tej roli IAM jawnie [utworzyć IR Azure](create-azure-integration-runtime.md#create-azure-ir) z lokalizacją Twojej usługi Data Lake Store i skojarz w usłudze Data Lake Store połączonej usługi, jak w poniższym przykładzie:

W fabryce danych Azure nie trzeba określić wszelkie właściwości poza ogólne informacje o usłudze Data Lake Store w połączonej usłudze.

**Przykład:**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje zobacz artykuł zestawów danych. Ta sekcja zawiera listę właściwości obsługiwanych przez zestaw danych usługi Azure Data Lake Store.

Aby skopiować dane do/z usługi Azure Data Lake Store, ustaw właściwość Typ zestawu danych do **AzureDataLakeStoreFile**. Obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type zestawu danych: **AzureDataLakeStoreFile** |Yes |
| folderPath | Ścieżka do kontenera i folderu w magazynie plików. Przykład: rootfolder/podfolder / |Yes |
| fileName | Określ nazwę pliku w **folderPath** Jeśli chcesz skopiować do/z określonego pliku. Jeśli nie określono żadnej wartości dla tej właściwości zestawu danych wskazuje wszystkie pliki w folderze.<br/><br/>Jeśli nazwa pliku nie jest określony dla wyjściowego zestawu danych i **preserveHierarchy** nie została określona w zbiornika działania działanie kopiowania automatycznie generuje nazwę pliku o następującym formacie: `Data.[activity run id GUID].[GUID if FlattenHierarchy].[format if configured].[compression if configured]`. Na przykład: `Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.gz`. |Nie |
| Format | Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.<br/><br/>Jeśli chcesz przeanalizować lub wygenerować pliki w określonym formacie, obsługiwane są następujące typy plików w formacie: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Ustaw **typu** właściwości w formacie do jednej z tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](supported-file-formats-and-compression-codecs.md#text-format), [formatu Json](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), i [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sekcje. |Nie (tylko w przypadku scenariusza kopiowania binarny) |
| Kompresja | Określ typ i poziom kompresji danych. Aby uzyskać więcej informacji, zobacz [obsługiwane formaty plików i kodery-dekodery kompresji](supported-file-formats-and-compression-codecs.md#compression-support).<br/>Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.<br/>Obsługiwane poziomy: **optymalna** i **najszybciej**. |Nie |

**Przykład:**

```json
{
    "name": "ADLSDataset",
    "properties": {
        "type": "AzureDataLakeStoreFile",
        "linkedServiceName":{
            "referenceName": "<ADLS linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "datalake/myfolder/",
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

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez usługi Azure Data Lake źródłowy i odbiorczy właściwości.

### <a name="azure-data-lake-store-as-source"></a>Azure Data Lake Store jako źródło

Aby skopiować dane z usługi Azure Data Lake Store, należy ustawić typ źródła w przypadku działania kopiowania do **AzureDataLakeStoreSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **AzureDataLakeStoreSource** |Yes |
| Cykliczne | Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu. Uwaga: po cykliczne ma ustawioną wartość PRAWDA, a obiekt sink jest magazynu opartych na plikach, pusty folder/podrzędne-folder nie będą kopiowane utworzone w ujścia.<br/>Dozwolone wartości to: **true** (ustawienie domyślne), **false** | Nie |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyFromADLS",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<ADLS input dataset name>",
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
                "type": "AzureDataLakeStoreSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="azure-data-lake-store-as-sink"></a>Azure Data Lake Store jako odbioru

Aby skopiować dane do usługi Azure Data Lake Store, należy ustawić typ ujścia w działaniu kopiowania do **AzureDataLakeStoreSink**. Następujące właściwości są obsługiwane w **zbiornika** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość typu sink działania kopiowania: **AzureDataLakeStoreSink** |Yes |
| copyBehavior | Określa zachowanie kopiowania, gdy źródłem jest pliki z magazynu danych opartych na plikach.<br/><br/>Dozwolone wartości to:<br/><b>-PreserveHierarchy (ustawienie domyślne)</b>: zachowuje hierarchię plików w folderze docelowym. Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.<br/><b>-FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego znajdują się w pierwszym poziomem folderu docelowego. Pliki docelowe mają automatycznie wygeneruje nazwę. <br/><b>-MergeFiles</b>: scala wszystkie pliki z folderu źródłowego do jednego pliku. Jeśli zostanie określona nazwa pliku/obiektów Blob, nazwa scalony plik jest określona nazwa; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie. | Nie |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyToADLS",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<ADLS output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "AzureDataLakeStoreSink",
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
