---
title: "aaaMove dane z witryny Salesforce przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z witryny Salesforce przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Przenieść dane z witryny Salesforce przy użyciu fabryki danych Azure
W tym artykule omówiono używania działania kopiowania danych toocopy fabryki danych Azure z magazynem danych tooany Salesforce, który znajduje się w kolumnie zbiornika hello w hello [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli. W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z kombinacji magazynu obsługiwane dane i działanie kopiowania.

Fabryka danych Azure aktualnie obsługuje tylko do przenoszenia danych z usług Salesforce za[obsługiwane magazyny danych zbiornika](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ale nie obsługuje przenoszenia danych z innych tooSalesforce magazynów danych.

## <a name="supported-versions"></a>Obsługiwane wersje
Ten łącznik obsługuje następujące wersje usług Salesforce hello: Developer Edition w wersji Professional, Enterprise Edition albo nieograniczone Edition. I obsługuje kopiowanie z Salesforce produkcji, piaskownicy i domeny niestandardowej.

## <a name="prerequisites"></a>Wymagania wstępne
* Musi być włączone uprawnienia interfejsu API. Zobacz [jak włączyć dostęp do interfejsu API w usłudze Salesforce przez zestaw uprawnień?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy danych z baz danych lokalnych tooon Salesforce, użytkownik musi mieć co najmniej 2.0 bramy zarządzania danych zainstalowanej w środowisku lokalnym.

## <a name="salesforce-request-limits"></a>Limity żądań usług SalesForce
Usługa SalesForce obejmuje limity dla całkowita liczba żądań interfejsu API i równoczesnych żądań interfejsu API. Należy zwrócić uwagę hello następujące punkty:

- Jeśli hello liczbę jednoczesnych żądań przekracza hello limit, ograniczanie występuje, i zobaczysz losowe awarie.
- Jeśli hello całkowita liczba żądań przekracza hello limit, hello konta usług Salesforce jest blokowana przez 24 godziny.

Może również wyświetlony błąd "REQUEST_LIMIT_EXCEEDED" hello, w obu przypadkach. Sekcja hello "interfejsu API limity żądań" w hello [Salesforce Developer limity](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artykułu, aby uzyskać szczegółowe informacje.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z witryny Salesforce przy użyciu różnych narzędzi/interfejsów API.

Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.

Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager **, **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello: 

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z usług Salesforce, zobacz [przykład JSON: kopiowanie danych z usług Salesforce tooAzure obiektu Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooSalesforce: 

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli opisano elementy JSON, które są określone toohello Salesforce połączone usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **Salesforce**. |Tak |
| environmentUrl | Określ wystąpienie adres URL usługi Salesforce hello. <br><br> -Domyślna to "https://login.salesforce.com". <br> -toocopy danych z piaskownicy, określ "https://test.salesforce.com". <br> -toocopy dane z domeny niestandardowej, określić, na przykład "https://[domain].my.salesforce.com". |Nie |
| nazwa użytkownika |Określ nazwę użytkownika dla konta użytkownika hello. |Tak |
| hasło |Określ hasło dla konta użytkownika hello. |Tak |
| securityToken |Określ tokenu zabezpieczającego dla konta użytkownika hello. Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje na temat tooreset/get tokenu zabezpieczającego. Ogólnie rzecz biorąc, zobacz toolearn o tokeny zabezpieczające [zabezpieczeń i hello interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Tak |

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, tabeli platformy Azure i tak dalej).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu hello **RelationalTable** ma hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w usłudze Salesforce. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

> [!IMPORTANT]
> Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak tabele nazwę, opis, danych wejściowych i wyjściowych i różnych zasad są dostępne dla wszystkich typów działań.

Hello właściwości, które są dostępne w hello drugiej sekcji typeProperties aktywności hello na powitania, zależą od każdego typu działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

W przypadku działania kopiowania, gdy źródłem hello jest typu hello **RelationalSource** (która obejmuje usługi Salesforce), hello następujące właściwości są dostępne w sekcji typeProperties:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania. Przykład: `select * from MyTable__c`. |Nie (jeśli hello **tableName** z hello **dataset** jest określona) |

> [!IMPORTANT]
> Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Wskazówki zapytania
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Podczas pobierania danych przy użyciu where klauzuli według kolumny daty i godziny
Gdy Określ hello SOQL lub SQL zapytanie, płatności uwagi toohello różnica format daty/godziny. Na przykład:

* **Przykładowe SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Przykładowe SQL**:
    * **Stosowanie zapytania hello toospecify kreatora kopiowania:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Przy użyciu edycji toospecify hello kwerendy (prawidłowo ucieczki znaku):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Pobieranie danych z raportu usług Salesforce
Można pobrać dane z raportów usług Salesforce, określając kwerendy w postaci `{call "<report name>"}`, na przykład. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Przywracanie usuniętych rekordów z Kosza usług Salesforce
tooquery hello nietrwałego usunięte rekordy z Kosza usług Salesforce, można określić **"IsDeleted = 1"** w zapytaniu. Na przykład:

* Określ tooquery tylko usunięte hello rekordy "Wybierz * z MyTable__c **gdzie IsDeleted = 1**"
* tooquery hello wszystkich rekordów, łącznie z istniejących hello i hello usunięty, określ "Wybierz * z MyTable__c **gdzie IsDeleted = 0 lub IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Przykład JSON: kopiowanie danych z usług Salesforce tooAzure obiektów Blob
Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Przedstawiają sposób toocopy dane usług Salesforce tooAzure magazynu obiektów Blob. Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.   

Poniżej przedstawiono hello artefakty fabryki danych należy toocreate tooimplement hello scenariusza. sekcje Hello listy hello zawierają szczegółowe informacje na temat tych kroków.

* Połączonej usługi typu hello [Salesforce](#linked-service-properties)
* Połączonej usługi typu hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Dane wejściowe [dataset](data-factory-create-datasets.md) typu hello [RelationalTable](#dataset-properties)
* Dane wyjściowe [dataset](data-factory-create-datasets.md) typu hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Usługa SalesForce połączone**

W tym przykładzie użyto hello **Salesforce** połączonej usługi. Zobacz hello [Salesforce połączona usługa](#linked-service-properties) sekcji hello właściwości, które są obsługiwane przez tej połączonej usługi.  Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje dotyczące sposobu tooreset/get hello tokenu zabezpieczającego.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
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
**Wejściowy zestaw danych usług SalesForce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.

> [!IMPORTANT]
> Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Wyjściowy zestaw danych obiektów blob platformy Azure**

Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Potok wraz z działanie kopiowania**

Witaj potoku zawiera działanie kopiowania, która jest skonfigurowana toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource**i hello **zbiornika** typu ustawiono zbyt**BlobSink**.

Zobacz [właściwości typu RelationalSource](#copy-activity-properties) hello listę właściwości, które są obsługiwane przez hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Mapowanie typu dla usług Salesforce
| Typ usług SalesForce | . Typ opartej na sieci |
| --- | --- |
| Automatyczny numer |Ciąg |
| Pole wyboru |Wartość logiczna |
| Waluta |O podwójnej precyzji |
| Date |Data i godzina |
| Data i godzina |Data i godzina |
| Adres e-mail |Ciąg |
| Identyfikator |Ciąg |
| Relacja wyszukiwania |Ciąg |
| Lista wyboru wielokrotnego wyboru |Ciąg |
| Liczba |O podwójnej precyzji |
| Procent |O podwójnej precyzji |
| Numer telefonu |Ciąg |
| Lista wyboru |Ciąg |
| Tekst |Ciąg |
| Obszar tekstu |Ciąg |
| Obszar tekstu (Liczba długa) |Ciąg |
| Obszar tekstu (zaawansowana) |Ciąg |
| Tekst (zaszyfrowane) |Ciąg |
| ADRES URL |Ciąg |

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Wydajności i dostosowywanie
Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
