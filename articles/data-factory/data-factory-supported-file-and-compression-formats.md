---
title: formaty aaaFile i kompresji w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello formatów plików obsługiwanych przez usługi fabryka danych Azure."
keywords: "dane obiektów blob, kopiowania obiektów blob platformy azure"
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Formaty plików i kompresji obsługiwane przez usługi fabryka danych Azure
*Ten temat dotyczy toohello następujące łączniki: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [systemu plików](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), i [SFTP](data-factory-sftp-connector.md).*

Fabryka danych Azure obsługuje następujące typy format pliku hello:

* [Format tekstu](#text-format)
* [JSON format](#json-format)
* [Avro format](#avro-format)
* [ORC format](#orc-format)
* [Parquet format](#parquet-format)

## <a name="text-format"></a>Format tekstu
Tooread z pliku tekstowego lub zapisać plik tekstowy tooa, ustaw hello `type` właściwości w hello `format` części zestawu danych hello zbyt**TextFormat**. Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji. Zobacz [przykład TextFormat](#textformat-example) sekcję na temat tooconfigure.

| Właściwość | Opis | Dozwolone wartości | Wymagany |
| --- | --- | --- | --- |
| columnDelimiter |znak Hello używać tooseparate kolumn w pliku. Należy rozważyć toouse istnieje rzadkich char nie do drukowania, który prawdopodobnie nie może w Twoich danych. Na przykład określić "\u0001", reprezentujący Start z pozycji (raportu o kondycji). |Dozwolony jest tylko jeden znak. Witaj **domyślne** wartość jest **przecinkiem (',')**. <br/><br/>toouse znaku Unicode, można znaleźć zbyt[znaków Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello odpowiedni kod dla niego. |Nie |
| rowDelimiter |znak Hello używać tooseparate wierszy w pliku. |Dozwolony jest tylko jeden znak. Witaj **domyślne** wartość jest dowolne hello następujące wartości na odczyt: **["\r\n", "\r", "\n"]** i **"\r\n"** podczas zapisu. |Nie |
| escapeChar |znaki specjalne Hello używane tooescape ogranicznik kolumny w hello zawartość pliku wejściowego. <br/><br/>W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar. |Dozwolony jest tylko jeden znak. Brak wartości domyślnej. <br/><br/>Przykład: Jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave hello przecinkami znaków w tekście hello (przykład: "tekst Hello, world"), można zdefiniować '$' jako znak ucieczki hello i użyj ciągu "Hello$, world" w źródle hello. |Nie |
| quoteChar |znak Hello używany tooquote wartość ciągu. ograniczniki kolumn i wierszy wewnątrz znaków cudzysłowu hello Hello będzie traktowane jako część hello wartość ciągu. Ta właściwość ma zastosowanie tooboth danych wejściowych i wyjściowych zestawów danych.<br/><br/>W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar. |Dozwolony jest tylko jeden znak. Brak wartości domyślnej. <br/><br/>Na przykład, jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave przecinkami znaków w tekście hello (przykład: < Hello, world >), można zdefiniować "(podwójnego cudzysłowu) jako hello znaku cudzysłowu i używać ciąg hello"Hello, world"w źródle hello. |Nie |
| nullValue |Co najmniej jeden znak używany toorepresent wartość null. |Co najmniej jeden znak. Witaj **domyślne** wartości są **"\N" i "NULL"** na odczyt i **"\N"** podczas zapisu. |Nie |
| encodingName |Określ nazwę kodowania hello. |Prawidłowa nazwa kodowania. Zobacz [właściwość Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Przykład: windows-1250 lub shift_jis. Witaj **domyślne** wartość jest **UTF-8**. |Nie |
| firstRowAsHeader |Określa, czy tooconsider hello pierwszego wiersza jako nagłówka. W przypadku zestawu danych wejściowych usługa Data Factory odczytuje pierwszy wiersz jako nagłówek. W przypadku zestawu danych wyjściowych usługa Data Factory zapisuje pierwszy wiersz jako nagłówek. <br/><br/>Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |True<br/><b>False (domyślnie)</b> |Nie |
| skipLineCount |Wskazuje liczbę hello tooskip wierszy podczas odczytywania danych z plików wejściowych. Jeśli został określony zarówno skipLineCount i firstRowAsHeader, wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello. <br/><br/>Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Liczba całkowita |Nie |
| treatEmptyAsNull |Określa, czy wartość tootreat null lub pusty ciąg jako wartość null, podczas odczytywania danych z pliku wejściowego. |**True (domyślnie)**<br/>False |Nie |

### <a name="textformat-example"></a>Przykład formatu TextFormat
W hello po definicji JSON dla zestawu danych niektóre właściwości opcjonalne hello określony.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse `escapeChar` zamiast `quoteChar`, Zastąp wiersza hello `quoteChar` z następujących elementów escapeChar hello:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scenariusze użycia właściwości firstRowAsHeader oraz skipLineCount
* Są kopiowane z pliku źródłowego z systemem innym niż plik tooa tekstu i chcesz tooadd wiersz nagłówka, zawierający metadane schematu hello (na przykład: schematu SQL). Określ `firstRowAsHeader` jako wartości true w hello wyjściowy zestaw danych dla tego scenariusza.
* Kopiowania z pliku tekstowego zawierającego zbiorniku plików z systemem innym niż tooa wiersz nagłówka i chcesz toodrop, który wiersz. Określ `firstRowAsHeader` jako wartość true w zestawie danych wejściowych hello.
* Kopiowania z pliku tekstowego i mają tooskip kilka wierszy na początku hello, które nie zawierają żadnych informacji danych lub nagłówek. Określ `skipLineCount` tooindicate hello liczba wierszy toobe pominięte. Jeśli hello pozostałej części pliku hello zawiera wiersz nagłówka, można również określić `firstRowAsHeader`. Jeśli oba `skipLineCount` i `firstRowAsHeader` są określone wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello

## <a name="json-format"></a>JSON format
zbyt**importu/eksportu pliku JSON jako — jest do/z bazy danych Azure rozwiązania Cosmos**, zobacz hello [dokumentów JSON importu/eksportu](data-factory-azure-documentdb-connector.md#importexport-json-documents) sekcji [przenoszenie danych do/z bazy danych Azure rozwiązania Cosmos](data-factory-azure-documentdb-connector.md) artykułu.

Pliki w formacie JSON hello tooparse lub zapisać danych hello w formacie JSON, ustaw hello `type` właściwości w hello `format` sekcji zbyt**JsonFormat**. Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji. Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure.

| Właściwość | Opis | Wymagany |
| --- | --- | --- |
| filePattern |Wskazuje wzorzec hello danych przechowywanych w każdym pliku JSON. Dozwolone wartości to: **setOfObjects** i **arrayOfObjects**. Witaj **domyślne** wartość jest **setOfObjects**. Aby uzyskać szczegółowe informacje o tych wzorcach, zobacz sekcję [Wzorce plików JSON](#json-file-patterns). |Nie |
| jsonNodeReference | Tooiterate i wyodrębniania danych z obiektów hello wewnątrz tablicy pola z hello sam wzorzec, określ ścieżkę JSON hello tablicy. Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON. | Nie |
| jsonPathDefinition | Określ wyrażenie ścieżki JSON powitania dla każdego mapowania kolumn z nazwą dostosowanego kolumna (start małymi literami). Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON; dane możesz wyodrębnić z obiektu lub tablicy. <br/><br/> W przypadku pól w obszarze katalogu głównego obiektu zaczynać się od $ głównego; dla pola w tablicy hello wybierany przez `jsonNodeReference` właściwości, początkową hello elementu tablicy. Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure. | Nie |
| encodingName |Określ nazwę kodowania hello. Aby hello listę prawidłowych nazw kodowania, zobacz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) właściwości. Na przykład: windows-1250 lub shift_jis. Witaj **domyślne** wartość to: **UTF-8**. |Nie |
| nestingSeparator |Znak, który jest używany tooseparate poziomów zagnieżdżenia. Witaj, wartością domyślną jest "." (kropką). |Nie |

### <a name="json-file-patterns"></a>Wzorce plików JSON

Działanie kopiowania może przeanalizować składni powitania po wzorce pliki w formacie JSON:

- **Typ I: setOfObjects**

    Każdy plik zawiera pojedynczy obiekt lub wiele obiektów rozdzielonych wierszami bądź połączonych. W przypadku wybrania tej opcji w zestawie danych wyjściowych działanie kopiowania tworzy pojedynczy plik JSON z każdym obiektem w osobnym wierszu (rozdzielanie wierszami).

    * **przykład kodu JSON z pojedynczym obiektem**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **przykład kodu JSON z obiektami rozdzielonymi wierszami**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **przykład kodu JSON z obiektami połączonymi**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Typ II: arrayOfObjects**

    Każdy plik zawiera tablicę obiektów.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>Przykład formatu JsonFormat

**Przypadek 1. Kopiowanie danych z plików JSON**

Zobacz powitania po dwóch próbek podczas kopiowania danych z plików JSON. Witaj toonote punktów ogólne:

**Przykład 1. Wyodrębnianie danych z obiektu i tablicy**

W tym przykładzie spodziewasz się, co główny obiekt JSON mapy toosingle rekordu w wyniku tabelarycznych. Jeśli masz plik JSON z hello następującej zawartości:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
i mają toocopy sformatować go do tabeli Azure SQL w następujących hello przez wyodrębniania danych z obiektów i tablicy:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części). Więcej szczegółów:

- `structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular. Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn. Zobacz [mapy kolumnach dataset toodestination kolumny zestawu danych źródła](data-factory-map-columns.md) sekcji, aby uzyskać więcej informacji.
- `jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane. toocopy danych z tablicy, można użyć **.property tablicy [x]** tooextract wartość hello podanej właściwości z obiektu x hello, lub można użyć  **tablicy [*] .property** toofind wartość Hello z dowolnych obiektów zawierających takie właściwości.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Przykład 2: cross zastosować wiele obiektów o hello sam wzorca z tablicy**

W tym przykładzie oczekujesz tootransform jeden główny obiekt JSON do wielu rekordów w wyniku tabelarycznych. Jeśli masz plik JSON z hello następującej zawartości:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
i chcesz sformatować go do tabeli Azure SQL w następujących hello przez spłaszczanie hello danych wewnątrz tablicy hello toocopy i krzyżowe z użyciem informacji hello wspólnej głównej:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części). Więcej szczegółów:

- `structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular. Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn. Zobacz [mapy kolumnach dataset toodestination kolumny zestawu danych źródła](data-factory-map-columns.md) sekcji, aby uzyskać więcej informacji.
- `jsonNodeReference`Wskazuje tooiterate i wyodrębniania danych z obiektów hello hello sam wzorca w obszarze **tablicy** orderlines.
- `jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane. W tym przykładzie "ordernumber", "orderdate" i "Miasto" podlegają główny obiekt ze ścieżką JSON, począwszy od "$.", podczas gdy "order_pd" i "order_price" są zdefiniowane z pochodzi od elementu tablicy hello bez "$". ścieżka.

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Należy zwrócić uwagę hello następujące punkty:**

* Jeśli hello `structure` i `jsonPathDefinition` nie są zdefiniowane w zestawie danych usługi fabryka danych hello, hello działanie kopiowania wykrywa hello schematu z pierwszego obiektu hello i spłaszczanie hello całym obiektem.
* Jeśli w danych wejściowych JSON hello tablicy, domyślnie hello działanie kopiowania konwertuje hello cała tablica wartości na ciąg. Można wybrać tooextract danych za pomocą `jsonNodeReference` i/lub `jsonPathDefinition`, lub ją pominąć, nie określając je w `jsonPathDefinition`.
* Jeśli istnieją zduplikowane nazwy w hello tym samym poziomie, hello działanie kopiowania wybiera hello ostatnią.
* W przypadku nazw właściwości wielkość liter ma znaczenie. Dwie właściwości o takiej samej nazwie, ale zapisanej przy użyciu różnej wielkości liter, są traktowane jako dwie osobne właściwości.

**Przypadek 2: Zapisywanie danych tooJSON pliku**

Jeśli masz hello w poniższej tabeli w bazie danych SQL:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

i dla każdego rekordu oczekujesz obiekt JSON tooa toowrite w hello następującego formatu:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

Witaj wyjściowy zestaw danych z **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części). W szczególności `structure` sekcja definiuje hello dostosować nazwy właściwości w pliku docelowym `nestingSeparator` (domyślna to ".") są używane tooidentify hello zagnieżdżania warstwy z hello nazwy. Ta sekcja ma **opcjonalne** chyba, że nazwa właściwości hello toochange porównanie z nazwą kolumny źródła lub zagnieździć niektóre właściwości hello.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>AVRO format
Tooparse hello Avro plików lub zapis danych hello format Avro, ustaw hello `format` `type` właściwości zbyt**AvroFormat**. Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello. Przykład:

```json
"format":
{
    "type": "AvroFormat",
}
```

format Avro toouse w tabeli programu Hive, można odwoływać się za[Apache Hive samouczek](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Należy zwrócić uwagę hello następujące punkty:  

* [Złożone typy danych](http://avro.apache.org/docs/current/spec.html#schema_complex) nie są obsługiwane (rejestruje, wyliczeń, tablic, map, Unii i usunięciu).

## <a name="orc-format"></a>ORC format
Plików ORC hello tooparse lub zapisać danych hello w formacie ORC, ustaw hello `format` `type` właściwości zbyt**OrcFormat**. Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello. Przykład:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Jeśli nie kopiowania plików ORC **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy. Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE. Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605). Wybierz odpowiednie hello.
>
>

Należy zwrócić uwagę hello następujące punkty:

* Złożone typy danych nie są obsługiwane (struktura, mapa, lista, unia)
* Plik ORC ma trzy [opcje związane z kompresją](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów. Używa kompresji hello kodera-dekodera jest hello metadanych tooread hello danych. Jednak podczas zapisywania plików ORC tooan, fabryki danych wybiera ZLIB, który jest domyślnym hello ORC. Obecnie nie są toooverride nie opcji to zachowanie.

## <a name="parquet-format"></a>Parquet format
Tooparse hello Parquet plików lub zapis danych hello w formacie Parquet, ustaw hello `format` `type` właściwości zbyt**ParquetFormat**. Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello. Przykład:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Jeśli nie są kopiowane pliki Parquet **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy. Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE. Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605). Wybierz odpowiednie hello.
>
>

Należy zwrócić uwagę hello następujące punkty:

* Złożone typy danych nie są obsługiwane (mapa, lista)
* Plik parquet ma następujące opcje związane z kompresji hello: NONE, SNAPPY GZIP i LZO. Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów. Koder-dekoder kompresji hello używa hello metadanych tooread hello danych. Jednak podczas zapisywania pliku Parquet tooa, fabryki danych wybiera SNAPPY, jest domyślna hello Parquet formatu. Obecnie nie są toooverride nie opcji to zachowanie.

## <a name="compression-support"></a>Obsługa kompresji
Przetwarzania dużych zestawów danych może spowodować błąd We/Wy i sieci wąskich gardeł. W związku z tym skompresowane dane w magazynach można nie tylko przyspieszenie działania transferu danych przez sieć hello i zaoszczędzić miejsce na dysku, ale również przełączyć istotne ulepszenia wydajności przetwarzania danych big data. Obecnie kompresja jest obsługiwana dla magazynów danych opartych na plikach, takich jak obiektów Blob platformy Azure lub lokalnego systemu plików.  

Kompresja toospecify dla zestawu danych, użyj hello **kompresji** właściwości w elemencie dataset hello JSON jak hello poniższy przykład:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Załóżmy, że hello przykładowego zestawu danych jest używany jako dane wyjściowe hello działanie kopiowania, hello kompresuje działania kopiowania hello dane wyjściowe z kodera-dekodera GZIP przy użyciu optymalny stosunek, a następnie wpisz hello skompresowane dane do pliku o nazwie pagecounts.csv.gz w hello magazynu obiektów Blob Azure.

> [!NOTE]
> Ustawienia kompresji nie są obsługiwane dla danych w hello **AvroFormat**, **OrcFormat**, lub **ParquetFormat**. Podczas odczytywania plików w tych formatach, fabryki danych wykrywa i używa koder-dekoder kompresji hello w hello metadanych. Podczas zapisywania toofiles w tych formatach, fabryki danych wybiera hello domyślne koder-dekoder kompresji w tym formacie. Na przykład ZLIB OrcFormat i SNAPPY dla ParquetFormat.   

Witaj **kompresji** sekcji ma dwie właściwości:  

* **Typ:** hello koder-dekoder kompresji, które mogą być **GZIP**, **Deflate**, **BZIP2**, lub **ZipDeflate**.  
* **Poziom:** hello kompresji, które mogą być **optymalna** lub **najszybciej**.

  * **Najszybszym:** hello kompresji operacji powinno zakończyć się tak szybko jak to możliwe, nawet jeśli nie jest optymalnie skompresowany plik wynikowy hello.
  * **Optymalne**: hello kompresji operacja powinna być optymalnie kompresowana, nawet jeśli hello operacja trwa dłużej toocomplete czasu.

    Aby uzyskać więcej informacji, zobacz [poziom kompresji](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) tematu.

Po określeniu `compression` właściwość w zestawie danych wejściowych JSON, hello potoku można odczytać skompresowane dane ze źródła hello; i po określeniu właściwości hello w zestawie danych wyjściowych JSON aktywności kopiowania hello może zapisywać docelowego toohello skompresowane dane. Poniżej przedstawiono kilka przykładowych scenariuszy:

* Odczytywać skompresowane GZIP danych obiektów blob platformy Azure, zdekompresować i zapisać wynik danych tooan — bazy danych Azure SQL. Zdefiniuj hello wejściowych obiektu Blob Azure zestaw danych o hello `compression` `type` właściwość JSON jako GZIP.
* Odczyt danych z pliku tekstowego z lokalnego systemu plików, skompresować je w formacie GZip i zapisać hello skompresowane dane tooan obiektów blob platformy Azure. Zdefiniuj wyjściowy zestaw danych obiektów Blob platformy Azure z hello `compression` `type` właściwość JSON jako GZip.
* Plik zip odczytu z serwera FTP zdekompresować plików hello tooget wewnątrz i trafić tych plików do usługi Azure Data Lake Store. Zdefiniuj zestaw danych wejściowych FTP z hello `compression` `type` właściwość JSON jako ZipDeflate.
* Odczytywać skompresowane GZIP danych obiektów blob platformy Azure, zdekompresować skompresować je przy użyciu BZIP2 i zapisać wynik tooan danych obiektów blob platformy Azure. Zdefiniuj hello wejściowych obiektu Blob Azure zestaw danych o `compression` `type` ustawić tooGZIP i hello wyjściowy zestaw danych z `compression` `type` ustawiony w tym przypadku tooBZIP2.   


## <a name="next-steps"></a>Następne kroki
Zobacz powitania po artykułach magazynów opartych na plikach danych obsługiwane przez usługi fabryka danych Azure:

- [Azure Blob Storage](data-factory-azure-blob-connector.md)
- [Azure Data Lake Store](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [System plików](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
