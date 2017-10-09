---
title: "aaaMove danych z tabeli sieci Web przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z tabeli w sieci Web stronę przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Przenoszenie danych ze źródła tabeli sieci Web przy użyciu fabryki danych Azure
W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tabeli w tooa strony sieci Web obsługiwane ujścia magazynu danych. W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.

Fabryka danych aktualnie obsługuje tylko przechowuje przenoszenia danych z danych tooother tabeli sieci Web, ale nie przenoszenia danych z innych danych przechowuje tooa Web tabeli docelowej.

> [!IMPORTANT]
> Ten łącznik sieci Web obsługuje obecnie tylko wyodrębnianie zawartości tabeli ze strony HTML. Użyj tooretrieve danych z punktu końcowego protokołu HTTP/s [łącznika HTTP](data-factory-http-connector.md) zamiast tego.

## <a name="getting-started"></a>Wprowadzenie
Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API. 

- Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**. Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello. 
- Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**. Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania. 

Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:

1. Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.
2. Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania. 
3. Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe. 

Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie. Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.  Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z tabeli sieci web, zobacz [przykład JSON: kopiowanie danych z sieci Web tooAzure tabeli obiektów Blob](#json-example-copy-data-from-web-table-to-azure-blob) sekcji tego artykułu. 

Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek tooa określonej sieci Web tabeli:

## <a name="linked-service-properties"></a>Połączona usługa właściwości
Hello w poniższej tabeli przedstawiono opis usługi określonego tooWeb połączone elementy JSON.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **sieci Web** |Tak |
| Url |Adres URL źródła toohello w sieci Web |Tak |
| Typ authenticationType |Anonimowe. |Tak |

### <a name="using-anonymous-authentication"></a>Przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Właściwości zestawu danych
Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu. Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).

Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych. Witaj typeProperties sekcja dla zestawu danych typu **tabeli WebTable** ma następujące właściwości hello

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |Typ hello zestawu danych. musi być ustawiona zbyt**tabeli WebTable** |Tak |
| Ścieżka |Względny adres URL toohello zasób zawiera tabelę hello. |Nie. Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany. |
| Indeks |Indeks Hello hello tabeli w zasobie hello. Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML. |Tak |

**Przykład:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Właściwości działania kopiowania
Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu. Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.

Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania. Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.

Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Przykład JSON: kopiowanie danych z sieci Web tooAzure tabeli obiektów Blob
następujące przykładowe pokazuje Hello:

1. Połączonej usługi typu [Web](#linked-service-properties).
2. Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Dane wejściowe [dataset](data-factory-create-datasets.md) typu [tabeli WebTable](#dataset-properties).
4. Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [WebSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

przykład Witaj kopiuje dane z sieci Web tooan tabeli obiektów blob platformy Azure co godzinę. właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.

następujące przykładowe Hello pokazuje, jak obiekt blob danych toocopy z tooan tabeli sieci Web Azure. Jednak dane mogą być kopiowane bezpośrednio tooany hello wychwytywanie hello podane w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu przy użyciu hello działanie kopiowania w fabryce danych Azure.

**Sieci Web połączonej usługi** w tym przykładzie używa hello sieci Web połączonej usługi przy użyciu uwierzytelniania anonimowego. Zobacz [sieci Web połączonej usługi](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

**Wejściowy zestaw danych tabeli WebTable** ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w hello Fabryka danych.

> [!NOTE]
> Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Azure Blob wyjściowy zestaw danych**

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
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**W potoku z działanie kopiowania**

Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**WebSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.

Zobacz [właściwości typu WebSource](#copy-activity-type-properties) hello listę obsługiwanych przez hello WebSource właściwości.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>Pobierz indeksu tabeli na stronie HTML
1. Uruchom **Excel 2016** i przełączanie toohello **danych** kartę.  
2. Kliknij przycisk **nowe zapytanie** na powitania narzędzi za punkt**z innych źródeł** i kliknij przycisk **z sieci Web**.

    ![Power Query menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. W hello **z sieci Web** okna dialogowego wprowadź **adres URL** można skorzystać w połączonej usłudze JSON (na przykład: https://en.wikipedia.org/wiki/) oraz ścieżkę należy określić dla zestawu danych hello (na przykład: AFI % 27s_100_Years... 100_Movies) i kliknij przycisk **OK**.

    ![Z okna dialogowego sieci Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    Adres URL używany w tym przykładzie: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Jeśli widzisz **zawartości sieci Web Access** okno dialogowe, wybierz hello prawo **adres URL**, **uwierzytelniania**i kliknij przycisk **Connect**.

   ![Okno dialogowe zawartości sieci Web Access](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Kliknij przycisk **tabeli** elementu hello drzewa widoku toosee zawartości z hello tabeli, a następnie kliknij przycisk **Edytuj** u dołu hello.  

   ![Nawigator okna dialogowego](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. W hello **edytora zapytań** okna, kliknij przycisk **Zaawansowany edytor** przycisk na powitania narzędzi.

    ![Przycisk Zaawansowane Edytora](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Okno dialogowe Zaawansowany edytor hello, hello numer obok "Source" jest za hello indeksu.

    ![Zaawansowany edytor - indeksu](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Jeśli korzystasz z programu Excel 2013, użyj [Microsoft Power Query dla programu Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello indeksu. Zobacz [strony sieci web tooa Połącz](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artykułu, aby uzyskać szczegółowe informacje. Witaj kroki są podobne, jeśli używasz [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Wydajność i dostrajania
Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.
