---
title: "Kopiowanie danych z bazy danych HBase przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z bazy danych HBase do zbiornika obsługiwane magazyny danych za pomocą działania kopiowania w potoku fabryki danych Azure."
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
ms.openlocfilehash: ea2258b953925116f759655583d9601c5a55db7c
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-hbase-using-azure-data-factory"></a>Kopiowanie danych z bazy danych HBase przy użyciu fabryki danych Azure 

W tym artykule omówiono sposób użycia działanie kopiowania w fabryce danych Azure, aby skopiować dane z bazy danych HBase. Opiera się na [skopiuj omówienie działania](copy-activity-overview.md) artykułu, który przedstawia ogólny przegląd działanie kopiowania.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [działanie kopiowania w wersji 1](v1/data-factory-data-movement-activities.md).

## <a name="supported-capabilities"></a>Obsługiwane możliwości

Możesz skopiować dane z bazy danych HBase żadnych obsługiwanych ujścia magazynu danych. Lista magazynów danych, które są obsługiwane jako źródła/wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](copy-activity-overview.md#supported-data-stores-and-formats) tabeli.

Fabryka danych Azure oferuje wbudowane sterowników, aby umożliwić łączność, w związku z tym nie trzeba ręcznie zainstalowania sterownika korzystania z tego łącznika.

## <a name="getting-started"></a>Wprowadzenie

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Poniższe sekcje zawierają szczegółowe informacje o właściwościach, które są używane do definiowania jednostek fabryki danych określonej do bazy danych HBase łącznika.

## <a name="linked-service-properties"></a>Połączona usługa właściwości

HBase połączone usługi, obsługiwane są następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Właściwość type musi mieć ustawioną: **HBase** | Yes |
| host | Adres IP lub hosta nazwę serwera bazy danych HBase. (i.e. 192.168.222.160)  | Yes |
| port | Port TCP używany przez wystąpienie bazy danych HBase do nasłuchiwania dla połączeń klienta. Wartość domyślna to 9090.  | Nie |
| httpPath | Adres URL częściowe odpowiadający serwera bazy danych HBase. (tj. /gateway/sandbox/hbase/version)  | Nie |
| authenticationType | Mechanizm uwierzytelniania na potrzeby łączenia się z serwerem bazy danych HBase. <br/>Dozwolone wartości to: **anonimowe**, **podstawowe** | Yes |
| nazwa użytkownika | Nazwa użytkownika używana do łączenia się z wystąpieniem bazy danych HBase.  | Nie |
| hasło | Hasło odpowiadający nazwie użytkownika. Można wybrać opcję Oznacz to pole jako SecureString Zapisz w bezpiecznej lokalizacji w ADF lub przechowywania haseł w usłudze Azure Key Vault i umożliwić działanie kopiowania ściągnięcia stamtąd podczas wykonywania kopii danych — Dowiedz się więcej o [przechowywania poświadczeń w magazynie kluczy](store-credentials-in-key-vault.md). | Nie |
| enableSsl | Określa, czy połączenia z serwerem są szyfrowane przy użyciu protokołu SSL. Wartość domyślna to false.  | Nie |
| trustedCertPath | Pełna ścieżka pliku PEM, zawierająca zaufane certyfikaty urzędu certyfikacji do weryfikowania serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Tej właściwości można ustawić tylko w przypadku korzystania z protokołu SSL na siebie IR. Wartość domyślna to plik cacerts.pem zainstalowane z IR.  | Nie |
| allowHostNameCNMismatch | Określa, czy wymagają nazwy certyfikat wystawiony przez urząd certyfikacji SSL do dopasowania nazwy hosta serwera podczas nawiązywania połączenia za pośrednictwem protokołu SSL. Wartość domyślna to false.  | Nie |
| allowSelfSignedServerCert | Określa, czy certyfikaty z podpisem własnym z serwera. Wartość domyślna to false.  | Nie |
| connectVia | [Integrację środowiska uruchomieniowego](concepts-integration-runtime.md) ma być używany do nawiązania połączenia z magazynem danych. (Jeśli w magazynie danych jest dostępny publicznie) można użyć środowiska uruchomieniowego integracji Self-hosted lub środowiska uruchomieniowego integracji Azure. Jeśli nie zostanie określony, używa domyślnej środowiska uruchomieniowego integracji Azure. |Nie |

**Przykład:**

```json
{
    "name": "HBaseLinkedService",
    "properties": {
        "type": "HBase",
        "typeProperties": {
            "host" : "<host>",
            "port" : "<port>",
            "httpPath" : "/gateway/sandbox/hbase/version",
            "authenticationType" : "Basic",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "enableSsl" : true,
            "trustedCertPath" : "<trustedCertPath>",
            "allowHostNameCNMismatch" : true,
            "allowSelfSignedServerCert" : true
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych

Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [zestawów danych](concepts-datasets-linked-services.md) artykułu. Ta sekcja zawiera listę właściwości obsługiwanych przez zestaw danych HBase.

Aby skopiować dane z bazy danych HBase, ustaw właściwość Typ zestawu danych do **HBaseObject**. Nie ma dodatkowych właściwości określonego typu w tego typu dataset.

**Przykład**

```json
{
    "name": "HBaseDataset",
    "properties": {
        "type": "HBaseObject",
        "linkedServiceName": {
            "referenceName": "<HBase linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania

Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [potoki](concepts-pipelines-activities.md) artykułu. Ta sekcja zawiera listę właściwości obsługiwane przez źródło HBase.

### <a name="hbasesource-as-source"></a>HBaseSource jako źródło

Aby skopiować dane z bazy danych HBase, należy ustawić typ źródła w przypadku działania kopiowania do **HBaseSource**. Następujące właściwości są obsługiwane w przypadku działania kopiowania **źródła** sekcji:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | Musi mieć ustawioną właściwość type źródła działania kopiowania: **HBaseSource** | Yes |
| query | Użyj niestandardowych zapytania SQL można odczytać danych. Na przykład: `"SELECT * FROM MyTable"`. | Yes |

**Przykład:**

```json
"activities":[
    {
        "name": "CopyFromHBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<HBase input dataset name>",
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
                "type": "HBaseSource",
                "query": "SELECT * FROM MyTable"
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
