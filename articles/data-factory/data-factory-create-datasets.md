---
title: zestawy danych aaaCreate w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zestawy danych toocreate w fabryce danych Azure, wraz z przykładami, które używają właściwości, takie jak przesunięcie i anchorDateTime."
keywords: "Tworzenie zestawu danych, przykładowe zestawu danych, przesunięcie przykład"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Zestawy danych w fabryce danych Azure
W tym artykule opisano, jakie zestawy danych są, jak są definiowane w formacie JSON i w jaki sposób są one używane w fabryce danych Azure potoków. Dostarcza szczegółowe informacje na temat każdej sekcji (na przykład struktury, dostępności i zasad) w definicji JSON hello zestawu danych. Witaj podano także przykłady dotyczące używania hello **przesunięcie**, **anchorDateTime**, i **styl** właściwości w definicji zestawu danych JSON.

> [!NOTE]
> Jeśli nowy tooData fabryki, zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) omówienie. Jeśli nie ma praktyczne doświadczenie w tworzeniu fabryki danych, można uzyskać lepsze zrozumienie za odczytywanie hello [samouczek przekształcania danych](data-factory-build-your-first-pipeline.md) i hello [samouczek przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Omówienie
Fabryka danych może obejmować jeden lub wiele potoków. A **potoku** to logiczne grupowanie **działania** który razem wykonania zadania. Hello działań w potoku zdefiniuj akcje tooperform na podstawie danych. Na przykład można użyć danych toocopy działania kopiowania z lokalnego programu SQL Server tooAzure magazynu obiektów Blob. Następnie należy użyć działania Hive, które uruchamia skrypt Hive w usłudze Azure HDInsight klastra tooprocess danych z danych wyjściowych tooproduce magazynu obiektów Blob. Ponadto można użyć drugiego kopiowania działania toocopy hello danych wyjściowych danych tooAzure SQL Data Warehouse, na które raportowania są wbudowane rozwiązania analizy biznesowej (BI). Aby uzyskać więcej informacji na temat potoków i działania, zobacz [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md).

Działanie może zająć zero lub więcej danych wejściowych **zestawów danych**i utworzyć co najmniej jeden wyjściowy zestaw danych. Zestaw danych wejściowych reprezentuje dane wejściowe hello działania w potoku hello, a wyjściowy zestaw danych reprezentuje hello wyjściowy dla działania hello. Zestawy danych identyfikują dane w różnych magazynach danych, takich jak tabele, pliki, foldery i dokumenty. Na przykład zestaw danych obiektów Blob platformy Azure określa hello kontenera obiektów blob i folder w magazynie obiektów Blob, z których hello potoku odczytywane dane hello. 

Przed utworzeniem zestawu danych, należy utworzyć **połączona usługa** toolink toohello fabryki danych magazynu danych. Połączone usługi są podobne do parametrów połączenia, które definiują informacje o połączeniu hello wymagane dla fabryki danych tooconnect tooexternal zasobów. Zestawy danych identyfikowanie danych w ramach hello połączonych magazynów danych, takich jak tabele SQL, pliki, foldery i dokumenty. Na przykład usługi Azure Storage połączone usługi łączy fabryki danych toohello konta magazynu. Zestaw danych obiektów Blob platformy Azure reprezentuje hello kontenera obiektów blob i hello folderu, który zawiera toobe wejściowych obiekty BLOB hello przetworzone. 

Oto przykładowy scenariusz. toocopy danych z obiektu Blob magazynu tooa SQL database, Utwórz dwie połączonej usługi: Magazyn Azure i bazy danych SQL Azure. Następnie utwórz dwa zestawy danych: zestaw danych obiektów Blob platformy Azure, (do którego odwołuje się toohello połączoną usługą magazynu Azure), a tabeli SQL Azure zestawu danych (odwołuje się toohello bazy danych SQL Azure połączone usługi). Witaj usługi Azure Storage i połączone usługi zawiera parametry połączeń, które fabryka danych używa odpowiednio tooyour tooconnect środowiska uruchomieniowego usługi Azure Storage i Azure SQL Database, baza danych SQL Azure. zestaw danych obiektów Blob platformy Azure Hello określa hello kontenera obiektów blob i folderu obiektów blob, który zawiera hello wejściowych obiekty BLOB w magazynie obiektów Blob. zestaw danych z tabeli SQL Azure Hello Określa, że hello tabeli SQL w danych hello toowhich bazy danych SQL jest toobe skopiowane.

Witaj Poniższy diagram przedstawia relacje hello potoku, działania, zestawu danych i połączonej usługi fabryki danych: 

![Relacja między potoku, działania, zestaw danych, połączone usługi](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>JSON dla zestawu danych
Zestaw danych z fabryki danych jest zdefiniowany w formacie JSON w następujący sposób:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Witaj w poniższej tabeli opisano właściwości w hello powyżej JSON:   

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| name |Nazwa zestawu danych hello. Zobacz [fabryki danych Azure - reguły nazewnictwa](data-factory-naming-rules.md) dla reguły nazewnictwa. |Tak |Nie dotyczy |
| type |Typ hello zestawu danych. Określ jeden z typów hello obsługiwane przez fabrykę danych (na przykład: AzureBlob, AzureSqlTable). <br/><br/>Aby uzyskać więcej informacji, zobacz [typ zestawu](#Type). |Tak |Nie dotyczy |
| Struktura |Schemat hello zestawu danych.<br/><br/>Aby uzyskać więcej informacji, zobacz [struktury zestawu danych](#Structure). |Nie |Nie dotyczy |
| typeProperties | właściwości typu Hello są różne dla każdego typu (na przykład: obiektów Blob platformy Azure, tabeli Azure SQL). Aby uzyskać szczegółowe informacje na ich właściwości i typów hello obsługiwane, zobacz [typ zestawu](#Type). |Tak |Nie dotyczy |
| external | Wartość logiczna Flaga toospecify, czy zestaw danych jawnie jest generowany przez potok fabryki danych lub nie. Jeśli hello wejściowy zestaw danych działania nie jest generowany przez potok bieżącego hello, należy ustawić tej flagi tootrue. Ustaw tootrue tej flagi dla hello wejściowego zestawu danych hello pierwsze działanie w potoku hello.  |Nie |wartość false |
| availability | Definiuje hello okno przetwarzania (na przykład co godzinę lub codziennie) lub hello fragmentowania modelu hello zestawu danych produkcyjnych. Każda jednostka danych używane i produkowane przez uruchomienia działania nosi nazwę wycinka danych. Jeśli zestaw toodaily (częstotliwość - Day, interwał - 1) jest dostępność hello wyjściowy zestaw danych, wycinek jest tworzony codziennie. <br/><br/>Aby uzyskać więcej informacji, zobacz [dostępności zestawu danych](#Availability). <br/><br/>Szczegółowe informacje na temat zestawu danych hello fragmentowania modelu, zobacz hello [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu. |Tak |Nie dotyczy |
| policy |Definiuje kryteria hello lub hello warunek, który należy spełnić hello wycinków zestaw danych. <br/><br/>Aby uzyskać więcej informacji, zobacz hello [zestawie danych zasad](#Policy) sekcji. |Nie |Nie dotyczy |

## <a name="dataset-example"></a>Przykład zestawu danych
W hello poniższy przykład, zestaw danych hello reprezentuje tabela o nazwie **MyTable** w bazie danych SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Należy zwrócić uwagę hello następujące punkty:

* **Typ** ustawiono tooAzureSqlTable.
* **tableName** właściwość type (typ określonych tooAzureSqlTable) ma wartość tooMyTable.
* **linkedServiceName** odwołuje się tooa połączone usługi typu AzureSqlDatabase, zdefiniowanego w hello dalej fragment JSON. 
* **częstotliwość dostępności** ustawiono tooDay, i **interwał** ustawiono too1. Oznacza to, że hello wycinek zestawu danych jest tworzony codziennie.  

**AzureSqlLinkedService** jest zdefiniowane w następujący sposób:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

W hello poprzedzających fragment kodu JSON:

* **Typ** ustawiono tooAzureSqlDatabase.
* **connectionString** właściwość type określa informacje tooconnect tooa SQL w bazie danych.  

Jak widać, hello połączonej usługi definiuje sposób tooconnect tooa SQL w bazie danych. Hello dataset definiuje, jakie tabela jest używane jako dane wejściowe i wyjściowe dla hello działania w potoku.   

> [!IMPORTANT]
> Jeśli zestaw danych jest tworzonym przez potok hello, powinien być oznaczony jako **zewnętrznych**. To ustawienie dotyczy tooinputs pierwsze działanie w potoku.   


## <a name="Type"></a>Typ zestawu danych
Typ Hello hello zestawu danych jest zależny od hello magazynu danych, którego używasz. Zobacz hello w poniższej tabeli listę magazynów danych obsługiwane przez fabryki danych. Kliknij przycisk toolearn magazynu danych jak toocreate połączonej usługi i zestawu danych dla tych danych magazynu.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Przechowuje dane z * można lokalnie lub na Azure infrastruktura jako usługa (IaaS). Te magazyny danych wymagają tooinstall [brama zarządzania danymi](data-factory-data-management-gateway.md).

W przykładzie hello w poprzedniej sekcji hello hello DataSet hello ustawiono zbyt**AzureSqlTable**. Podobnie dla zestawu danych obiektów Blob platformy Azure, hello typ zestawu danych hello jest ustawiona zbyt**AzureBlob**, jak pokazano w powitania po JSON:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>Struktura zestawu danych
Witaj **struktury** sekcja jest opcjonalna. Definiuje hello schemat zestawu danych hello przez zawierający kolekcję nazwy i typy danych kolumn. Możesz użyć hello struktura sekcji tooprovide typ informacji o tooconvert używane typy i mapy kolumny z hello źródłowego toohello docelowego. W hello poniższy przykład, hello dataset zawiera trzy kolumny: `slicetimestamp`, `projectname`, i `pageviews`. Są one typu String, typ String i dziesiętnych, odpowiednio.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Każda kolumna w strukturze hello zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa kolumny hello. |Tak |
| type |Typ danych kolumny hello.  |Nie |
| Kultury |. Toobe kulturę opartą na sieci używany, gdy typ hello jest typ architektury .NET: `Datetime` lub `Datetimeoffset`. Domyślnie Hello `en-us`. |Nie |
| Format |Format ciągu toobe używany, gdy typ hello jest typ architektury .NET: `Datetime` lub `Datetimeoffset`. |Nie |

Witaj poniższe wskazówki pomocne w określeniu po tooinclude struktury informacji i jakie tooinclude w hello **struktury** sekcji.

* **Dla źródeł danych strukturalnych**, określ hello struktura sekcji tylko wtedy, gdy ma mapowanie kolumn toosink kolumny źródłowej, a ich nazwy nie są hello takie same. Tego rodzaju źródła danych strukturalnych przechowuje informacje schematu i typu danych wraz z danymi hello. Przykładami źródeł danych strukturalnych programu SQL Server, Oracle i tabeli platformy Azure. 
  
    Ponieważ informacje o typie jest już dostępne dla źródeł danych strukturalnych, nie może zawierać informacje o typie zawierają hello struktura sekcji.
* **Do schematu w źródłach danych odczytu (w szczególności magazynu obiektów Blob)**, można wybrać toostore danych bez żadnych informacji schematu i typu danych hello przechowywania. W przypadku tych typów źródeł danych mają strukturę należy toomap źródła kolumny toosink kolumny. Gdy hello zestawu danych jest wartością wejściową dla działania kopiowania i typy danych zestawu źródła danych powinny być przekonwertowana toonative typy dla obiekt sink hello także struktury. 
    
    Fabryka danych obsługuje następujące wartości udostępnienie informacji o typie w strukturze hello: **Int16, Int32, Int64, pojedynczego, Double, Decimal bajtów [], wartość logiczna, ciąg, Guid, Datetime, Datetimeoffset i Timespan**. Te wartości są specyfikacja języka wspólnego (CLS)-zgodne,. Wartości typu opartej na sieci.

Fabryka danych automatycznie wykonuje konwersje typów przemieszczając się, że magazyn danych ze źródła danych magazynu danych tooa ujścia. 
  

## <a name="dataset-availability"></a>Dostępność zestawu danych
Witaj **dostępności** hello okna przetwarzania (na przykład co godzinę, codziennie lub co tydzień) dla zestawu danych hello definiuje sekcję w zestawie danych. Aby uzyskać więcej informacji na temat działania systemu windows, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md).

powitania po sekcji dostępności Określa, że hello wyjściowy zestaw danych jest albo tworzone co godzinę lub co godzinę hello wejściowy zestaw danych jest dostępne:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Jeśli potoku hello ma powitania od godziny rozpoczęcia i zakończenia:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Witaj wyjściowy zestaw danych jest tworzony co godzinę w potoku hello godziny rozpoczęcia i zakończenia. W związku z tym ma pięć wycinków zestaw danych utworzonych w ramach tego potoku, po jednej dla każdego działania okna (00: 00 - 1 AM, 1: 00 - 2 AM, 2 AM - 3 AM, 3 AM — 4 AM, 4: 00 - 5: 00). 

Witaj poniższej tabeli opisano właściwości, które można użyć w sekcji dostępności hello:

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| frequency |Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.<br/><br/><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca |Tak |Nie dotyczy |
| interval |Określa mnożnik częstotliwości.<br/><br/>"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany. Na przykład, jeśli konieczne hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.<br/><br/>Należy pamiętać, że jeśli określisz **częstotliwość** jako **minutę**, należy ustawić hello interwał toono mniej niż 15. |Tak |Nie dotyczy |
| Styl |Określa, czy wycinek hello powinien zostać utworzony w hello początek lub koniec interwału powitania.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Jeśli **częstotliwość** ustawiono zbyt**miesiąca**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany na powitania ostatni dzień miesiąca. Jeśli **styl** ustawiono zbyt**StartOfInterval**, wycinek hello jest generowany na powitania pierwszego dnia miesiąca.<br/><br/>Jeśli **częstotliwość** ustawiono zbyt**dzień**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany w hello ostatniej godziny hello dnia.<br/><br/>Jeśli **częstotliwość** ustawiono zbyt**godzina**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany na końcu hello hello godzinę. Na przykład dla wycinek hello okres 13: 00 - 14: 00, wycinek hello jest generowany na 14: 00. |Nie |EndOfInterval |
| anchorDateTime |Definiuje położenie bezwzględne hello w czasie używane przez hello harmonogramu toocompute dataset wycinek granic. <br/><br/>Należy pamiętać, że jeśli ta propoerty ma części daty, które są bardziej szczegółowego niż hello określa częstotliwość hello części bardziej szczegółowego są ignorowane. Na przykład, jeśli hello **interwał** jest **co godzinę** (częstotliwość: godzinę i interwał: 1), a hello **anchorDateTime** zawiera **minut i sekund**, następnie hello części minut i sekund **anchorDateTime** są ignorowane. |Nie |01/01/0001 |
| Przesunięcie |Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych. <br/><br/>Należy pamiętać, że jeśli obie **anchorDateTime** i **przesunięcie** są określone, wynik hello jest shift hello połączone. |Nie |Nie dotyczy |

### <a name="offset-example"></a>przykład przesunięcia
Domyślnie codziennie (`"frequency": "Day", "interval": 1`) wycinków Rozpocznij od 00: 00 (północ) uniwersalny czas koordynowany (UTC). Czas UTC 6: 00 toobe czas rozpoczęcia hello zamiast tego, ustawić hello przesunięcie pokazane na powitania po fragment kodu: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>przykład anchorDateTime
W hello poniższy przykład hello dataset jest tworzony co 23 godz. Witaj pierwszego wycinka rozpoczyna się od czasu hello określonego przez **anchorDateTime**, która wartość jest zbyt`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>przykład przesunięcie i stylu
Witaj następujący zestaw danych jest co miesiąc i jest generowany na powitania 3rd każdego miesiąca o godzinie 8:00 AM (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Zestaw danych zasad
Witaj **zasad** sekcja w definicji zestawu danych hello definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych.

### <a name="validation-policies"></a>Zasady sprawdzania poprawności
| Nazwa zasad | Opis | Stosowane za| Wymagane | Domyślne |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Sprawdza poprawność danych hello w **magazynu obiektów Blob Azure** spełnia hello wymagań minimalny rozmiar (w MB). |Azure Blob Storage |Nie |Nie dotyczy |
| minimumRows |Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy. |<ul><li>Baza danych SQL Azure</li><li>Tabeli platformy Azure</li></ul> |Nie |Nie dotyczy |

#### <a name="examples"></a>Przykłady
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Zewnętrznych zestawów danych
Zewnętrznych zestawów danych są hello te, które nie są produkowane przez uruchomione potok w fabryce danych hello. Jeśli hello zestawu danych jest oznaczona jako **zewnętrznych**, hello **ExternalData** zasad może być tooinfluence zdefiniowanego zachowania hello hello dataset wycinek dostępności.

Jeśli zestaw danych jest tworzonym przez fabrykę danych, powinien być oznaczony jako **zewnętrznych**. To ustawienie dotyczy wejść toohello pierwszy aktywności w potoku, chyba że działania lub łańcucha potoku jest używany.

| Nazwa | Opis | Wymagane | Wartość domyślna |
| --- | --- | --- | --- |
| dataDelay |czas Hello toodelay hello sprawdzanie dostępności hello hello danych zewnętrznych dla hello podany wycinka. Na przykład za pomocą tego ustawienia można opóźnić wyboru co godzinę.<br/><br/>Witaj ustawienie dotyczy tylko toohello obecny czas.  Na przykład jeśli 1:00 PM od razu i ta wartość to 10 minut, weryfikacji hello rozpoczyna się od 1:22:00.<br/><br/>Należy zwrócić uwagę, to ustawienie nie wpływa na wycinki hello ostatnich. Wycinków z **czas zakończenia wycinek** + **dataDelay** < **teraz** są przetwarzane bez opóźnień.<br/><br/>Godzinach większą niż 23:59 godziny należy określić przy użyciu hello `day.hours:minutes:seconds` format. Na przykład toospecify 24 godziny, nie używaj 24:00:00. Zamiast tego należy użyć 1.00:00:00. Jeśli używasz 24:00:00, będzie traktowane jako 24 dni (24.00:00:00). 1 dzień i 4 godziny Określ 1:04:00:00. |Nie |0 |
| retryInterval |czas oczekiwania Hello między błędu i hello ponowieniem próby. To ustawienie dotyczy toopresent czasu. Jeśli poprzednie spróbuj hello zakończyło się niepowodzeniem, po hello jest hello następnej próbie **retryInterval** okresu. <br/><br/>Jeśli jest 1:00 PM od razu, możemy rozpocząć hello pierwszej próby. W przypadku 1 minutę i nie można wykonać operacji hello hello czas trwania toocomplete hello pierwsze sprawdzanie poprawności hello Następna ponowna próba nastąpi na 1:00 1 min (czas trwania) + 1min (interwał ponawiania) = 13:02:00. <br/><br/>Wycinki w przeszłości hello nie ma żadnego opóźnienia. Ponów próbę Hello odbywa się natychmiast. |Nie |00:01:00 (1 minuta) |
| retryTimeout |Witaj limitu czasu dla każdego ponowienia próby.<br/><br/>Jeśli ta właściwość jest ustawiona minut too10 weryfikacji hello powinna zostać ukończona w ciągu 10 minut. Jeśli trwa dłużej niż 10 minut tooperform hello weryfikacji, hello ponów limit.<br/><br/>Jeśli wszystkie próby dla limitu czasu sprawdzania poprawności hello, hello wycinek jest oznaczony jako **upłynął limit czasu**. |Nie |00:10:00 (10 minut) |
| maximumRetry |Witaj liczba toocheck dostępności hello hello danych zewnętrznych. Witaj maksymalna dozwolona wartość to 10. |Nie |3 |


## <a name="create-datasets"></a>Tworzenie zestawów danych
Zestawy danych można utworzyć za pomocą jednej z tych narzędzi i zestawy SDK: 

- Kreator kopiowania 
- Azure Portal
- Visual Studio
- PowerShell
- Szablon usługi Azure Resource Manager
- Interfejs API REST
- Interfejs API .NET

Zobacz hello następujące samouczki instrukcje krok po kroku dotyczące tworzenia potoki i zestawów danych przy użyciu jednej z tych narzędzi i zestawy SDK:
 
- [Tworzenie potoku z działaniem przekształcania danych](data-factory-build-your-first-pipeline.md)
- [Tworzenie potoku z działaniem przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Po utworzeniu i wdrożeniu potoku można zarządzać i monitorować Twoje potoki przy użyciu hello Azure bloki portalu lub aplikacji hello monitorowanie i zarządzanie. Zobacz następujące tematy, aby uzyskać instrukcje krok po kroku hello: 

- [Monitorowanie i zarządzanie nimi potoki przy użyciu bloków portalu Azure](data-factory-monitor-manage-pipelines.md)
- [Monitorowanie i zarządzanie nimi potoki przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Zestawy danych w zakresie
Możesz utworzyć zestawy danych, które są potoku o zakresie tooa przy użyciu hello **zestawów danych** właściwości. Te zestawy danych można używać tylko przez działania w ramach tego potoku, a nie przez działania w innych potoków. Poniższy przykład Hello definiuje potoku z dwóch zestawów danych (InputDataset rdc i kompresji rdc OutputDataset) toobe używane w ramach hello potoku.  

> [!IMPORTANT]
> Zestawy danych w zakresie są obsługiwane tylko w przypadku jednorazowego potoki (gdzie **pipelineMode** ustawiono zbyt**OneTime**). Zobacz [potoku Onetime](data-factory-create-pipelines.md#onetime-pipeline) szczegółowe informacje.
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat potoków, zobacz [tworzenie potoków](data-factory-create-pipelines.md). 
- Aby uzyskać więcej informacji o sposobie planowania i wykonywania potoków, zobacz [planowania i wykonywania w fabryce danych Azure](data-factory-scheduling-and-execution.md). 
