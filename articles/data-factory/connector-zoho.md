---
title: "Kopiowanie danych z Zoho przy użyciu fabryki danych Azure (wersja Beta) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z Zoho do zbiornika obsługiwane magazyny danych za pomocą działania kopiowania w potoku fabryki danych Azure."
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
ms.date: 11/30/2017
ms.author: jingwang
ms.openlocfilehash: 507e7b237c1ddc765af92cd53574e08c6655bd1e
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-zoho-using-azure-data-factory-beta"></a>Kopiowanie danych z Zoho przy użyciu fabryki danych Azure (wersja Beta)

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane z Zoho. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [działanie kopiowania w wersji 1](v1/data-factory-data-movement-activities.md).

> [!IMPORTANT]
> Ten łącznik jest obecnie w wersji Beta. Możesz wypróbować jej możliwości i przekaż nam swoją opinię. Nie należy używać go w środowisku produkcyjnym.

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Możesz skopiować dane z Zoho żadnych obsługiwanych ujścia magazynu danych. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

Fabryka danych Azure oferuje wbudowane sterowników, aby umożliwić łączność, w związku z tym nie trzeba ręcznie zainstalowania sterownika korzystania z tego łącznika.

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do Zoho łącznika.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Zoho połączone usługi, obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **Zoho** | Yes |
| endpoint | Punkt końcowy serwera Zoho. (to znaczy crm.zoho.com/crm/private)  | Yes |
| accessToken | Token dostępu Zoho uwierzytelniania. Można wybrać opcję Oznacz to pole jako SecureString Zapisz w bezpiecznej lokalizacji w ADF lub przechowywania haseł w usłudze Azure Key Vault i umożliwić działanie kopiowania ściągnięcia stamtąd podczas wykonywania kopii danych — Dowiedz się więcej o [przechowywania poświadczeń w magazynie kluczy](store-credentials-in-key-vault.md). | Yes |
| useEncryptedEndpoints | Określa, czy punkty końcowe źródła danych są szyfrowane przy użyciu protokołu HTTPS. Wartość domyślna to true.  | Nie |
| useHostVerification | Określa, czy nazwa hosta w certyfikacie serwera, aby dopasować nazwę hosta serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Wartość domyślna to true.  | Nie |
| usePeerVerification | Określa, czy można zweryfikować tożsamości serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Wartość domyślna to true.  | Nie |

**Przykład:**

```json
{
    "name": "ZohoLinkedService",
    "properties": {
        "type": "Zoho",
        "typeProperties": {
            "endpoint" : "crm.zoho.com/crm/private",
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [zestawów danych](concepts-datasets-linked-services.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez zestaw danych Zoho właściwości.

Aby skopiować dane z Zoho, ustaw właściwość Typ zestawu danych do **ZohoObject**. Nie ma dodatkowych właściwości określonego typu w tego typu dataset.

**Przykład**

```json
{
    "name": "ZohoDataset",
    "properties": {
        "type": "ZohoObject",
        "linkedServiceName": {
            "referenceName": "<Zoho linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę obsługiwanych przez źródło Zoho właściwości.

### <a name="zohosource-as-source"></a>ZohoSource jako źródło

Aby skopiować dane z Zoho, należy ustawić typ źródła w przypadku działania kopiowania do **ZohoSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **ZohoSource** | Yes |
| query | Użyj niestandardowych zapytania SQL można odczytać danych. Na przykład: `"SELECT * FROM Accounts"`. | Yes |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyFromZoho",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Zoho input dataset name>",
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
                "type": "ZohoSource",
                "query": "SELECT * FROM Accounts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>Kolejne kroki
Lista magazynów danych obsługiwane jako źródła i wychwytywanie przez działanie kopiowania w fabryce danych Azure, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats).
