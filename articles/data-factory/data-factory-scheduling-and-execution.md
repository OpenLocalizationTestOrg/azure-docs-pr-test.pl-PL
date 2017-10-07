---
title: "aaaScheduling i wykonywania z fabryką danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, planowania i wykonywania aspektów modelu aplikacji fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Planowanie fabryki danych i wykonywania
W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji hello fabryki danych Azure. W tym artykule przyjęto założenie, że rozumiesz podstawowe pojęcia modelu aplikacji fabryki danych, w tym działania, potoki połączonych usług i zestawów danych. Dla podstawowych pojęciach dotyczących usługi fabryka danych Azure Zobacz hello następujące artykuły:

* [Wprowadzenie tooData fabryki](data-factory-introduction.md)
* [Potoki](data-factory-create-pipelines.md)
* [Zestawy danych](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Czas rozpoczęcia i zakończenia potoku
Potok jest aktywna tylko między jego **start** czasu i **zakończenia** czasu. Nie jest wykonywany przed godziną rozpoczęcia hello lub po godzinie zakończenia hello. Jeśli potoku hello jest wstrzymana, nie została wykonana niezależnie od jego czas rozpoczęcia i zakończenia. Dla toorun potoku jego powinien nie można wstrzymać. Te ustawienia (start, koniec wstrzymana) można znaleźć w definicji potoku hello: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Aby uzyskać więcej informacji zobacz te właściwości [tworzenie potoków](data-factory-create-pipelines.md) artykułu. 


## <a name="specify-schedule-for-an-activity"></a>Określ harmonogram dla działania
Nie jest hello potok, który jest wykonywany. Działania hello w potoku hello, które są wykonywane w hello jest ogólnym kontekście hello potoku. Można określić harmonogramu cyklicznego dla działania za pomocą hello **harmonogramu** sekcji aktywność JSON. Na przykład można zaplanować działania toorun co godzinę w następujący sposób:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Jak pokazano na powitania po diagramu, określanie harmonogramu dla działania tworzy serię windows wirowania z w hello potoku rozpoczęcia i zakończenia razy. Windows wirowania są szereg przedziały czasu nienakładający, ciągły stałym rozmiarze. Te okna wirowania logiczne dla działania są nazywane **okien działania**.

![Przykład harmonogram działania](media/data-factory-scheduling-and-execution/scheduler-example.png)

Witaj **harmonogramu** właściwość dla działania jest opcjonalna. Jeśli określisz tej właściwości musi być zgodna hello okresach, które określisz w definicji zestawu danych wyjściowych dla działania hello hello. Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. Dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. 

## <a name="specify-schedule-for-a-dataset"></a>Określ harmonogram dla zestawu danych
Działania w potoku fabryki danych może zająć zero lub więcej danych wejściowych **zestawów danych** i tworzące co najmniej jeden wyjściowy zestaw danych. Dla działania można określić hello okresach, w których hello danych wejściowych jest dostępna lub dane wyjściowe hello jest generowany przy użyciu hello **dostępności** części hello definicji zestawu danych. 

**Częstotliwość** w hello **dostępności** sekcja określa jednostkę czasu hello. Witaj dozwolone są wartości częstotliwości: minuty, godziny, dnia, tygodnia i miesiąca. Witaj **interwał** właściwości w sekcji dostępności hello Określa mnożnik częstotliwości. Na przykład: Jeśli częstotliwość hello ustawiono tooDay i interwał jest ustawiany too1 dla wyjściowego zestawu danych, danych wyjściowych hello jest tworzony codziennie. Można określić częstotliwość hello jako minutę, zaleca się ustawienie hello interwał toono mniej niż 15. 

Poniższy przykład hello, hello danych wejściowych jest dostępne co godzinę i danych wyjściowych hello jest tworzone co godzinę (`"frequency": "Hour", "interval": 1`). 

**Wejściowy zestaw danych:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Wyjściowy zestaw danych**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Obecnie **wyjściowego zestawu danych dysków hello harmonogram**. Innymi słowy harmonogram hello określony dla zestawu danych wyjściowych hello jest używany toorun działania w czasie wykonywania. Dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello. 

W następujących hello potoku definicji, hello **harmonogramu** właściwość jest używane toospecify harmonogram działania hello. Ta właściwość jest opcjonalna. Obecnie hello harmonogram hello działania muszą być zgodne harmonogram hello określony dla hello wyjściowego zestawu danych.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

W tym przykładzie co godzinę uruchomień działania hello między hello godziny rozpoczęcia i zakończenia hello potoku. dane wyjściowe Hello jest tworzone co godzinę dla windows trzech godzin (8 AM - 9 AM, 9 AM - 10, a 10 AM - 11: 00). 

Nosi nazwę każdej jednostki danych używane lub generowane przez działanie Uruchom **wycinka danych**. powitania po diagramie przedstawiono przykład działania o jeden wejściowy zestaw danych i jeden wyjściowy zestaw danych: 

![Harmonogram dostępności](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

Hello diagram pokazuje hello co godzinę wycinków danych dla hello argument wejściowy i wyjściowy zestaw danych. Witaj diagram przedstawia trzy wycinków wejściowych, które są gotowe do przetworzenia. działanie AM 10-11 Hello jest w toku, tworzenie wycinek danych wyjściowych AM 10-11 hello. 

Dostęp można uzyskać interwał czasu hello skojarzone z hello wycinek bieżący w zestawie danych hello JSON przy użyciu zmiennych: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) i [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Podobnie można uzyskać dostępu do interwał czasu hello skojarzone z okna działania za pomocą hello WindowStart i WindowEnd. Harmonogram Hello działania muszą być zgodne hello harmonogram hello wyjściowego zestawu danych działania hello. W związku z tym hello SliceStart i SliceEnd wartości są hello takie same jak wartości WindowStart i WindowEnd odpowiednio. Aby uzyskać więcej informacji o tych zmiennych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md#data-factory-system-variables) artykułów.  

Te zmienne można użyć do różnych celów w Twoich działaniach w formacie JSON. Na przykład można ich tooselect dane wejściowe i wyjściowe zestawy danych reprezentujący dane serii czas (na przykład: 8 AM too9 MAM). W tym przykładzie również używane **WindowStart** i **WindowEnd** tooselect odpowiednie dane dla działania uruchamiania i skopiuj go blob tooa z odpowiednią hello **folderPath**. Witaj **folderPath** jest toohave sparametryzowane oddzielny folder dla każdej godziny.  

W hello poprzedzających przykład określony dla zestawów danych wejściowych i wyjściowych harmonogram hello jest hello takie same (co godzinę). Jeśli hello wejściowy zestaw danych dla działania hello jest dostępny w innej częstotliwości, powiedz co 15 minut, hello tworzącego tego zestawu danych wyjściowych nadal odbywa się działanie godzinę jako hello wyjściowy zestaw danych jest jakie dysków hello harmonogram działania. Aby uzyskać więcej informacji, zobacz [modelu zestawów danych z różnych częstotliwości](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Dostępność zestawu danych i zasady
Jak już wspomniano użycia hello częstotliwość i interwał właściwości w sekcji dostępności hello definicji zestawu danych. Istnieje kilka właściwości, które mają wpływ na powitania planowania i wykonywania działania. 

### <a name="dataset-availability"></a>Dostępność zestawu danych 
Witaj poniższej tabeli opisano właściwości można używać w hello **dostępności** sekcji:

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| frequency |Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.<br/><br/><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca |Tak |Nie dotyczy |
| interval |Określa mnożnik częstotliwości<br/><br/>"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany.<br/><br/>Należy hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.<br/><br/><b>Uwaga</b>: Jeśli określisz częstotliwość co minutę, firma Microsoft zaleca ustawienie hello interwał toono mniej niż 15 |Tak |Nie dotyczy |
| Styl |Określa, czy wycinek hello powinien zostać utworzony w hello rozpoczęcia/zakończenia hello interwału.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Jeśli częstotliwość ustawiono tooMonth i styl jest ustawiony tooEndOfInterval, wycinek hello jest realizowane na powitania ostatni dzień miesiąca. Jeśli hello styl jest ustawiony tooStartOfInterval, wycinek hello jest realizowane na powitania pierwszego dnia miesiąca.<br/><br/>Jeśli częstotliwość ustawiono tooDay i styl jest ustawiony tooEndOfInterval, wycinek hello jest tworzona w hello ostatniej godziny hello dnia.<br/><br/>Jeśli częstotliwość ustawiono tooHour i styl jest ustawiony tooEndOfInterval, wycinek hello jest generowany na końcu hello hello godzinę. Na przykład dla wycinka okres 13: 00 – 14: 00, wycinek hello jest generowany na 14: 00. |Nie |EndOfInterval |
| anchorDateTime |Definiuje położenie bezwzględne hello w czasie używana przez granice wycinek dataset toocompute harmonogramu. <br/><br/><b>Uwaga</b>: hello AnchorDateTime ma części daty, które są bardziej szczegółowego niż częstotliwość hello następnie hello części bardziej szczegółowego są ignorowane. <br/><br/>Na przykład, jeśli hello <b>interwał</b> jest <b>co godzinę</b> (częstotliwość: godzinę i interwał: 1) i hello <b>AnchorDateTime</b> zawiera <b>minut i sekund</b>, następnie hello <b>minut i sekund</b> części hello AnchorDateTime są ignorowane. |Nie |01/01/0001 |
| Przesunięcie |Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych. <br/><br/><b>Uwaga</b>: Jeśli jest określony zarówno anchorDateTime, jak i przesunięcie wynik hello jest shift hello połączone. |Nie |Nie dotyczy |

### <a name="offset-example"></a>przykład przesunięcia
Domyślnie codziennie (`"frequency": "Day", "interval": 1`) wycinków uruchomione w czasie UTC 00: 00 (północ). Czas UTC 6: 00 toobe czas rozpoczęcia hello zamiast tego, ustawić hello przesunięcie pokazane na powitania po fragment kodu: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>przykład anchorDateTime
W hello poniższy przykład hello dataset jest tworzony co 23 godz. Witaj pierwszego wycinka rozpoczyna się od czasu hello określonego przez anchorDateTime hello, która jest ustawiona zbyt`2017-04-19T08:00:00` (czas UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Przesunięcie i stylu przykład
Witaj następujący zestaw danych jest miesięczne zestawu danych i jest generowany na 3rd każdego miesiąca o godzinie 8:00 AM (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Zestaw danych zasad
Zestaw danych może mieć zdefiniowane zasady sprawdzania poprawności określający, jak mogą być sprawdzone hello dane generowane przez wykonanie wycinek przed jest gotowy do użycia. W takich przypadkach po zakończeniu wykonywania, wycinek hello hello dane wyjściowe wycinek stan zmienia się zbyt**oczekiwania** z podstanu z **weryfikacji**. Po zweryfikowaniu wycinków hello zmiany stanu wycinka hello zbyt**gotowe**. Jeśli wycinek danych został utworzony, ale nie przeszedł sprawdzania poprawności hello, uruchomień działania podrzędne wycinki, które są zależne od tego wycinka nie są przetwarzane. [Monitorowanie i zarządzanie nimi potoki](data-factory-monitor-manage-pipelines.md) obejmuje hello różnych stanów wycinków danych z fabryki danych.

Witaj **zasad** sekcja w definicji zestawu danych definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych. Witaj poniższej tabeli opisano właściwości można używać w hello **zasad** sekcji:

| Nazwa zasad | Opis | Stosowane za| Wymagane | Domyślne |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Sprawdza poprawność danych hello w **obiektów blob platformy Azure** spełnia hello wymagań minimalny rozmiar (w MB). |Obiekt bob Azure |Nie |Nie dotyczy |
| minimumRows | Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy. |<ul><li>Usługa Azure SQL Database</li><li>Tabeli platformy Azure</li></ul> |Nie |Nie dotyczy |

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

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Aby uzyskać więcej informacji na temat tych właściwości i przykłady, zobacz [utworzyć zestawy danych](data-factory-create-datasets.md) artykułu. 

## <a name="activity-policies"></a>Zasady dotyczące działań
Zasady wpływają na zachowanie środowiska wykonawczego hello działania, w szczególności, podczas przetwarzania wycinka hello tabeli. w poniższej tabeli Hello zawiera szczegóły hello.

| Właściwość | Dozwolone wartości | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| Współbieżność |Liczba całkowita <br/><br/>Wartość maksymalna: 10 |1 |Liczba równoczesnych wykonaniami hello działania.<br/><br/>Określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków. Na przykład jeśli działanie wymaga toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Określa kolejność hello wycinki danych, które są przetwarzane.<br/><br/>Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie. Jeśli ustawisz hello executionPriorityOrder toobe NewestFirst wycinka hello godzinie 5 jest przetwarzana najpierw. Podobnie jeśli ustawisz hello executionPriorityORder toobe OldestFIrst wycinka hello godzinie 4 jest przetwarzany. |
| retry |Liczba całkowita<br/><br/>Maksymalna wartość może być 10 |0 |Liczba ponownych prób przed hello przetwarzania danych dla wycinka hello jest oznaczona jako niepowodzenie. Wykonania działania dla wycinka danych próba zostanie ponowiona się toohello określona liczba ponownych prób. Ponów próbę Hello odbywa się jak najszybciej po awarii hello. |
| timeout |Zakres czasu |00:00:00 |Limit czasu dla działania hello. Przykład: 00:10:00 (oznacza limitu 10 minut)<br/><br/>Jeśli wartość nie została określona lub jest równa 0, limit czasu hello jest nieograniczony.<br/><br/>Jeśli czas przetwarzania danych hello na wycinek przekracza wartość limitu czasu hello, anulowaniu i hello system próbuje tooretry hello przetwarzania. Witaj liczby ponownych prób zależy od hello ponawiania właściwości. W przypadku przekroczenia limitu czasu hello stan jest ustawiany tooTimedOut. |
| Opóźnienie |Zakres czasu |00:00:00 |Określ opóźnienie hello przed rozpoczęciem przetwarzania danych powoduje uruchomienie wycinek hello.<br/><br/>Hello wykonywania działań dotyczących wycinek danych jest uruchamiany po hello opóźnienie jest hello oczekiwany czas wykonywania.<br/><br/>Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut) |
| Parametr longRetry |Liczba całkowita<br/><br/>Wartość maksymalna: 10 |1 |Witaj liczbę długi ponownych prób przed hello wycinek wykonanie nie powiodło się.<br/><br/>Parametr longRetry prób uzyskają przez longRetryInterval. Dlatego toospecify czas między ponownymi próbami, należy użyć longRetry. Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i hello maksymalną liczbę prób ponawiania * longRetry.<br/><br/>Na przykład, jeśli mamy hello następujące ustawienia zasad działania hello:<br/>Spróbuj ponownie: 3<br/>Parametr longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Załóżmy istnieje tylko jeden wycinek tooexecute (oczekiwanie stanu) i wykonania działania hello zawsze kończy się niepowodzeniem. Początkowo może być 3 wykonywanie kolejnych prób. Po każdej próbie stanu wycinka hello byłoby ponów próbę. Po pierwsze 3 prób się za pośrednictwem stanu wycinka hello będą LongRetry.<br/><br/>Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób. Po utworzeniu tego stanu wycinka hello będzie można i będą podejmowane próby. Dlatego całkowity 6 podejmowano.<br/><br/>Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek hello będzie gotowy i są podjęto próby.<br/><br/>Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub hello ogólnej środowiska jest niestabilnym, w których przetwarzania danych. W takich przypadkach podczas ponownych prób po kolei nie mogą pomóc w i w ten sposób po upływie interwału czasu powoduje hello potrzebne dane wyjściowe.<br/><br/>Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval. Zazwyczaj wyższej wartości oznacza innych kwestii systemowych. |
| longRetryInterval |Zakres czasu |00:00:00 |Witaj opóźnienie między próbami czas ponów |

Aby uzyskać więcej informacji, zobacz [potoki](data-factory-create-pipelines.md) artykułu. 

## <a name="parallel-processing-of-data-slices"></a>Równoległe przetwarzanie wycinków danych
W przeszłości hello można ustawić hello datę rozpoczęcia dla potoku hello. Po wykonaniu tej fabryki danych automatycznie oblicza wszystkie fragmenty danych w przeszłości hello (wypełnienia tyłu) i rozpoczyna przetwarzanie je. Na przykład: Jeśli utworzyć potok z datą rozpoczęcia 2017-04-01 i hello jest data bieżąca 2017-04-10. Jeśli okresach hello z hello produkt wyjściowy zestaw danych jest codziennie, a następnie uruchamia fabryki danych przetwarzania wszystkie fragmenty hello z 2017-04-01 too2017-04-09 natychmiast, ponieważ data rozpoczęcia hello jest w przeszłości hello. wycinek Hello 2017-04-10 nie został przetworzony jeszcze ponieważ hello wartość właściwości stylu w sekcji dostępności hello jest EndOfInterval domyślnie. Witaj najstarsze wycinek jest przetwarzany najpierw jako domyślny hello wartość executionPriorityOrder jest OldestFirst. Opis właściwości stylu hello, zobacz [dostępności zestawu danych](#dataset-availability) sekcji. Opis sekcji executionPriorityOrder hello, zobacz hello [zasady dotyczące działań](#activity-policies) sekcji. 

Można skonfigurować toobe wycinki danych wypełnione wstecz przetwarzane równolegle przez ustawienie hello **współbieżności** właściwości w hello **zasad** sekcji hello działania w formacie JSON. Ta właściwość określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków. Wartość domyślna Hello hello współbieżności właściwości to 1. W związku z tym jeden wycinek jest przetwarzany w czasie domyślnie. Witaj, wartość maksymalna wynosi 10. Gdy potoku potrzebuje toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych. 

## <a name="rerun-a-failed-data-slice"></a>Uruchom ponownie wycinek danych nie powiodło się
Gdy wystąpi błąd podczas przetwarzania wycinka danych, można ustalić przyczyny niepowodzenia przetwarzania hello wycinek przy użyciu bloków portalu Azure lub monitora i zarządzania aplikacji. Zobacz [monitorowania i zarządzania nimi przy użyciu bloków portalu Azure potoki](data-factory-monitor-manage-pipelines.md) lub [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md) szczegółowe informacje.

Należy wziąć pod uwagę hello poniższy przykład, który zawiera dwa działania. Działania Activity1 i działania 2. Działania Activity1 zużywa fragment Dataset1 i tworzy wycinek Dataset2, które jest używane jako dane wejściowe przez tooproduce Activity2 wycinek hello ostatecznego zestawu danych.

![Wycinek nie powiodło się](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hello diagram wskazuje, że poza trzech ostatnich wycinków, wystąpił wycinek 9 10 AM hello produkujących awarii dla Dataset2. Fabryka danych automatycznie śledzi zależności zestawu hello czasu serii danych. W związku z tym nie rozpoczyna działania hello uruchamiania dla wycinka niższego rzędu 9 10 AM hello.

Narzędzia zarządzania i monitorowania fabryki danych pozwala toodrill do dzienników diagnostycznych hello hello wycinka nie powiodło się tooeasily Znajdź hello głównego spowodować hello problemu i rozwiąż problem. Po hello problem został rozwiązany, można łatwo uruchomić uruchamiania nie powiodło się wycinek hello tooproduce hello działania. Aby uzyskać więcej informacji na temat toorerun i zrozumienie stanu przejścia wycinki danych, zobacz [monitorowania i zarządzania nimi przy użyciu bloków portalu Azure potoki](data-factory-monitor-manage-pipelines.md) lub [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md).

Po ponownym uruchomieniu hello 9 10 AM slice dla **Dataset2**, fabryki danych uruchamia hello uruchamiania dla wycinka zależnych 9 10 AM hello na powitania ostatecznego zestawu danych.

![Uruchom ponownie wycinka nie powiodło się](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Wiele działań w potoku
Potok może obejmować więcej niż jedno działanie. Jeśli masz wiele działań w potoku i hello dane wyjściowe działania nie jest wejściem innego działania, hello działania mogą działać równolegle, jeśli wycinki danych wejściowych dla działań hello jest gotowe.

Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. działania Hello może znajdować się w hello potoku tego samego lub w innej potoków. działanie drugi Hello wykonuje tylko wtedy, gdy hello najpierw jeden zakończy działanie pomyślnie.

Rozważmy na przykład hello następującego przypadku, gdy potoku ma dwa działania:

1. A1 działania, który wymaga zewnętrzny zestaw danych wejściowych D1 i tworzy wyjściowy zestaw danych D2.
2. A2 działania, która wymaga danych wejściowych z zestawu danych D2 i tworzy wyjściowy zestaw danych D3.

W tym scenariuszu działania A1 i A2 są w hello sam potoku. Witaj działanie, które A1 jest uruchamiany, gdy dane zewnętrzne hello jest dostępny i częstotliwość dostępności hello zaplanowane zostanie osiągnięty. Witaj działania A2 uruchamiane po hello zaplanowane wycinków z D2 staną się dostępne i hello częstotliwość zaplanowana dostępność zostanie osiągnięty. W przypadku błędu w jednym z wycinków hello w zestawie danych D2, A2 nie działa dla tego wycinka, dopóki nie będzie dostępny.

Witaj widoku diagramu z obu działaniami w hello się, że tego samego potoku będzie wyglądała powitania po diagramu:

![Tworzenie łańcuchów działań w hello sam potoku](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Jak wspomniano wcześniej, hello działania może być w różnych potoków. W takiej sytuacji widoku diagramu hello będzie wyglądać powitania po diagramu:

![Tworzenie łańcuchów działań w dwóch potoki](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Zobacz hello [skopiuj sekwencyjnie](#copy-sequentially) sekcji w dodatku hello przykład.

## <a name="model-datasets-with-different-frequencies"></a>Zestawy danych modelu z różnych częstotliwości
W próbkach hello zostały hello tej samej częstotliwości hello wejściowych i wyjściowych zestawów danych i hello działania harmonogram okna. W niektórych scenariuszach wymagane hello możliwości tooproduce wyjście z częstotliwością od częstotliwości hello jeden lub więcej składników. Fabryka danych obsługuje modelowania tych scenariuszy.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Przykład 1: Tworzy codzienne raportu wyjściowego dla danych wejściowych, który jest dostępny co godzinę
Rozważmy scenariusz, w którym możesz mieć pomiaru dane wejściowe z czujników dostępne co godzinę w magazynie obiektów Blob Azure. Chcesz tooproduce codzienne agregacji raport o statystyk, takich jak średnią, minimalną i maksymalną dla dzień hello przy [działania hive fabryki danych](data-factory-hive-activity.md).

Oto, jak można model ten scenariusz przy użyciu fabryki danych:

**Wejściowy zestaw danych**

Witaj wejściowej co godzinę pliki są usuwane w folderze hello hello danego dnia. Dostępność dla danych wejściowych jest ustawiona na **godzina** (częstotliwość: godziny, interwał: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Wyjściowy zestaw danych**

Jeden plik wyjściowy jest tworzony codziennie w folderze hello dnia. Dostępność danych wyjściowych jest ustawiona na **dzień** (częstotliwość: dzień i interwał: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Działania: działania w potoku hive**

skryptu hive Hello odbiera hello odpowiednie *DateTime* informacji jako parametry, które używają hello **WindowStart** zmiennej, jak pokazano w hello następującego fragmentu. skryptu hive Hello używa tych danych hello tooload zmiennej z hello poprawnego folderu dzień hello i uruchom hello agregacji toogenerate hello w danych wyjściowych.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Witaj Poniższy diagram przedstawia hello scenariusza z punktu widzenia zależności danych.

![Zależności danych](./media/data-factory-scheduling-and-execution/data-dependency.png)

Witaj wycinek danych wyjściowych dla każdego dnia zależy od 24 wycinków co godzinę z zestawem danych wejściowych. Te zależności automatycznie z nazwami hello wycinki danych wejściowych, które wchodzą w hello oblicza fabryki danych sam okres czasu jako hello wyprodukowanych toobe wycinek danych wyjściowych. Jeśli żadnego hello 24 wycinków wejściowych nie jest dostępna, fabryki danych oczekuje na toobe wejściowych wycinek hello gotowe przed rozpoczęciem hello codziennego uruchamiania działania.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Przykład 2: Określ zależności z wyrażeń i funkcji usługi fabryka danych
Teraz Rozważmy scenariusz, w innym. Załóżmy, że masz działania hive, która przetwarza dwóch zestawów danych wejściowych. Jeden z nich ma codziennie nowe dane, ale jeden z nich pobiera nowe dane co tydzień. Załóżmy, że żądana toodo sprzężenia między hello dwóch parametrów wejściowych i utworzenie danych wyjściowych każdego dnia.

podejście proste Hello, w którym fabryka danych automatycznie danych liczbowych limit hello dane wejściowe wycinków tooprocess ustawiając wyjściowych toohello okresu nie działa czasowym wycinka danych.

Należy określić, że każde działanie Uruchom hello fabryki danych należy używać wycinek danych ostatniego tygodnia dla zestawu danych wejściowych co tydzień hello. Korzystania z funkcji usługi fabryka danych Azure, jak pokazano w powitania po tooimplement fragment to zachowanie.

**Input1: Obiektów blob platformy Azure**

Witaj pierwsze dane wejściowe, jest hello obiektów blob platformy Azure są aktualizowane codziennie.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2: Obiektów blob platformy Azure**

Input2 jest hello Azure blob aktualizowana co tydzień.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Dane wyjściowe: Obiektów blob platformy Azure**

Jeden plik wyjściowy jest tworzony codziennie w folderze hello hello dzień. Dostępność danych wyjściowych jest ustawiona zbyt**dzień** (częstotliwość: dzień, interwał: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Działania: działania w potoku hive**

działanie hive Hello przyjmuje hello dwóch parametrów wejściowych i tworzy wycinek danych wyjściowych każdego dnia. Można określić toodepend wycinka dane wyjściowe każdego dnia na hello wycinek wejściowych poprzedniego tygodnia dla danych wejściowych co tydzień w następujący sposób.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md) listę funkcje i zmienne systemu, które obsługuje fabryki danych.

## <a name="appendix"></a>Dodatek

### <a name="example-copy-sequentially"></a>Przykład: kopiowanie sekwencyjnie
Jego jest możliwe toorun wiele operacji kopiowania po kolei w sposób sekwencyjnych/uporządkowane. Na przykład może mieć dwóch kopii działań w potoku (CopyActivity1 i CopyActivity2) z hello następujące dane wejściowe dane wyjściowe zestawy danych:   

CopyActivity1

Dane wejściowe: zestawu danych. Dane wyjściowe: Dataset2.

CopyActivity2

Dane wejściowe: Dataset2.  Dane wyjściowe: Dataset3.

CopyActivity2 może działać tylko wtedy, gdy hello CopyActivity1 zostało uruchomione pomyślnie i Dataset2 jest dostępny.

Oto kod JSON potoku próbki hello:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Zwróć uwagę, że w przykładzie hello hello wyjściowego zestawu danych hello pierwsze działanie kopiowania (Dataset2) został określony jako danych wejściowych dla drugiego działania hello. W związku z tym hello działania drugi działa tylko wtedy, gdy hello wyjściowy zestaw danych z pierwsze działanie hello jest gotowy.  

Przykład Witaj CopyActivity2 może mieć inne dane, takie jak Dataset3, ale Dataset2 można określić jako tooCopyActivity2 wejściowych, więc nie można uruchomić działanie hello zakończenie CopyActivity1. Na przykład:

CopyActivity1

Dane wejściowe: Dataset1. Dane wyjściowe: Dataset2.

CopyActivity2

Dane wejściowe: Dataset3, Dataset2. Dane wyjściowe: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Zwróć uwagę, że w przykładzie hello dwóch zestawów danych wejściowych są określone dla aktywności kopiowania drugi hello. Jeśli określono wielu danych wejściowych, tylko hello pierwszego wejściowego zestawu danych służy do kopiowania danych, ale inne zestawy danych są używane jako zależności. CopyActivity2 zaczyna się dopiero po hello są spełnione następujące warunki:

* Pomyślnie ukończono CopyActivity1 i Dataset2 jest dostępny. Ten zestaw danych nie jest używany podczas kopiowania tooDataset4 danych. Tylko działa jako zależność planowania dla CopyActivity2.   
* Dataset3 jest dostępna. Ten zestaw danych reprezentuje dane hello, który jest skopiowany toohello docelowym. 
