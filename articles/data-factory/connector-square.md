---
title: "Kopiowanie danych z przy użyciu fabryki danych Azure (wersja Beta) kwadratu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z kwadratowe do zbiornika obsługiwane magazyny danych za pomocą działania kopiowania w potoku fabryki danych Azure."
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
ms.openlocfilehash: 1988d293c78e7fb51f08d040ab96a6d7a3abbb87
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-square-using-azure-data-factory-beta"></a>Kopiowanie danych z kwadratowe przy użyciu fabryki danych Azure (wersja Beta)

Ten artykuł przedstawia sposób użycia działanie kopiowania w fabryce danych Azure można skopiować danych z kwadratowe. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [działanie kopiowania w wersji 1](v1/data-factory-data-movement-activities.md).

> [!IMPORTANT]
> Ten łącznik jest obecnie w wersji Beta. Możesz wypróbować jej możliwości i przekaż nam swoją opinię. Nie należy używać go w środowisku produkcyjnym.

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Możesz skopiować dane z kwadratowe żadnych obsługiwanych ujścia magazynu danych. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

Fabryka danych Azure oferuje wbudowane sterowników, aby umożliwić łączność, w związku z tym nie trzeba ręcznie zainstalowania sterownika korzystania z tego łącznika.

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do łącznika.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

Następujące właściwości są obsługiwane dla kwadratowego połączonej usługi:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **kwadratowe** | Yes |
| host | Adres URL wystąpienia kwadratowych. (i.e. mystore.mysquare.com)  | Yes |
| clientId | Identyfikator klienta skojarzony z aplikacją kwadratowych.  | Yes |
| clientSecret | Klucz tajny klienta skojarzone z aplikacją kwadratowych. Można wybrać opcję Oznacz to pole jako SecureString Zapisz w bezpiecznej lokalizacji w ADF lub przechowywania haseł w usłudze Azure Key Vault i umożliwić działanie kopiowania ściągnięcia stamtąd podczas wykonywania kopii danych — Dowiedz się więcej o [przechowywania poświadczeń w magazynie kluczy](store-credentials-in-key-vault.md). | Yes |
| redirectUri | Adres URL przekierowania przypisane na pulpicie nawigacyjnym aplikacji kwadratowych. (tj. http://localhost:2500)  | Yes |
| useEncryptedEndpoints | Określa, czy punkty końcowe źródła danych są szyfrowane przy użyciu protokołu HTTPS. Wartość domyślna to true.  | Nie |
| useHostVerification | Określa, czy nazwa hosta w certyfikacie serwera, aby dopasować nazwę hosta serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Wartość domyślna to true.  | Nie |
| usePeerVerification | Określa, czy można zweryfikować tożsamości serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Wartość domyślna to true.  | Nie |

**Przykład:**

```json
{
    "name": "SquareLinkedService",
    "properties": {
        "type": "Square",
        "typeProperties": {
            "host" : "mystore.mysquare.com",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            },
            "redirectUri" : "http://localhost:2500"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [zestawów danych](concepts-datasets-linked-services.md) artykułu. Ta sekcja zawiera listę właściwości obsługiwanych przez kwadratowa zestawu danych.

Aby skopiować dane z kwadratowy, ustaw właściwość Typ zestawu danych do **SquareObject**. Nie ma dodatkowych właściwości określonego typu w tego typu dataset.

**Przykład**

```json
{
    "name": "SquareDataset",
    "properties": {
        "type": "SquareObject",
        "linkedServiceName": {
            "referenceName": "<Square linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę właściwości obsługiwane przez źródło kwadratowych.

### <a name="squaresource-as-source"></a>SquareSource jako źródło

Aby skopiować dane z kwadratowy, Ustaw typ źródła w przypadku działania kopiowania do **SquareSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **SquareSource** | Yes |
| query | Użyj niestandardowych zapytania SQL można odczytać danych. Na przykład: `"SELECT * FROM Business"`. | Yes |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyFromSquare",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Square input dataset name>",
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
                "type": "SquareSource",
                "query": "SELECT * FROM Business"
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
