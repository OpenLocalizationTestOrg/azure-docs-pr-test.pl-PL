---
title: "aaaCopy działania wydajności i dostrajania przewodnik | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat kluczowych czynników wpływających na wydajność hello przepływu danych w fabryce danych Azure, korzystając z działanie kopiowania."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Skopiuj wydajności działania i dostrajania przewodnik
Działanie kopiowania fabryki danych Azure oferuje najwyższej jakości danych bezpieczne, niezawodne i wysoko wydajnych ładowania rozwiązania. On pozwala toocopy dziesiątki terabajtów danych codziennie przez szeroki zakres chmury i lokalnych magazynów danych. Ładowanie wydajności danych ogromną fast jest tooensure klucza można skoncentrować się na problem "danych big data" core hello: kompilowanie rozwiązań zaawansowane analizy i uzyskiwanie szczegółowych informacji z wszystkie te dane.

Platforma Azure oferuje zestaw korporacyjnej rozwiązania dotyczące danych magazynu i danych magazynu i działanie kopiowania oferuje zoptymalizowanego ładowania środowisko, które jest łatwe tooconfigure i konfigurowanie danych. Z po prostu działanie pojedynczej kopii można uzyskać:

* Ładowanie danych do **magazyn danych SQL Azure** w **1,2 GB/s**. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).
* Ładowanie danych do **magazynu obiektów Blob Azure** na **1.0 GB/s**
* Ładowanie danych do **Azure Data Lake Store** na **1.0 GB/s**

W tym artykule opisano:

* [Numery wydajności](#performance-reference) dla obsługiwanych źródłowy i odbiorczy toohelp dane w magazynach plan projektu.
* Funkcje, które mogą zwiększyć hello przepływność kopiowania w różnych scenariuszy, w tym [jednostki przepływu danych w chmurze](#cloud-data-movement-units), [równoległych kopii](#parallel-copy), i [przemieszczane kopiowania](#staged-copy);
* [Wskazówki dotyczące dostrajania wydajności](#performance-tuning-steps) na jak tootune hello wydajności i hello kluczowych czynników wpływających można skopiować wydajności.

> [!NOTE]
> Jeśli nie masz doświadczenia w obsłudze działania kopiowania ogólnie rzecz biorąc, zobacz [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md) przed przeczytaniem tego artykułu.
>

## <a name="performance-reference"></a>Informacje dotyczące wydajności

Jako odwołanie pod tabelą pokazuje liczbę przepływności kopiowania hello w MB/s dla hello podane pary źródłowy i odbiorczy testów wewnętrznych. Porównanie można go również pokazano, jak różne ustawienia [jednostki przepływu danych w chmurze](#cloud-data-movement-units) lub [skalowalność brama zarządzania danymi](data-factory-data-management-gateway-high-availability-scalability.md) (wiele węzłów bramy) pozwalają na wydajność kopiowania.

![Macierz wydajności](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Toonote punktów:**
* Przepływność jest obliczana przy użyciu następującej formuły hello: [read rozmiar danych ze źródła] / [czas trwania działania kopiowania].
* Witaj wydajności numery w tabeli hello zostały mierzone przy użyciu [TPC-H](http://www.tpc.org/tpch/) zestawu danych w działaniu pojedynczej kopii Uruchom.
* W magazynie danych Azure hello źródło i ujście są w hello tego samego regionu systemu Azure.
* Dla kopii hybrydowej między lokalnymi i w chmurze magazyny danych każdy węzeł bramy była uruchomiona na komputerze, który został oddzielony od hello magazyn danych lokalnych z poniżej specyfikacji. Pojedyncze działanie była uruchomiona na bramy, operacji kopiowania hello używane tylko niewielką część hello testowej maszyny procesora CPU, pamięć lub przepustowości sieci. Dowiedz się więcej o [brany pod uwagę dla bramy zarządzania danymi](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>Procesor CPU</td>
        <td>32 rdzenie 2,20 GHz Intel Xeon E5-2660 v2</td>
    </tr>
    <tr>
        <td>Memory (Pamięć)</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Sieć</td>
        <td>Interfejs internetowy: 10 GB/s; interfejsu intranetowego: 40 GB/s</td>
    </tr>
    </table>


> [!TIP]
> Wyższej przepustowości można osiągnąć dzięki wykorzystaniu jednostki przepływu więcej danych (DMUs) niż hello Domyślna maksymalna DMUs, który wynosi 32 dla działania kopiowania w chmurze na chmurze, uruchom. Na przykład z 100 DMUs, możesz osiągnąć kopiowanie danych z obiektu Blob Azure do usługi Azure Data Lake Store **1.0GBps**. Zobacz hello [jednostki przepływu danych w chmurze](#cloud-data-movement-units) sekcji, aby uzyskać szczegółowe informacje o tej funkcji i hello obsługiwany scenariusz. Skontaktuj się z [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/) toorequest DMUs więcej.

## <a name="parallel-copy"></a>Kopiuj równoległych
Może odczytywać źródła danych z hello lub zapisać miejsce docelowe danych toohello **równolegle w ramach działania kopiowania, uruchom**. Ta funkcja zwiększa przepływność hello operacji kopiowania i zmniejsza hello czas toomove danych.

To ustawienie jest inny niż hello **współbieżności** właściwości w definicji działania hello. Hello **współbieżności** właściwość określa liczbę hello **uruchamia równoczesne działanie kopiowania** tooprocess danych z innego działania systemu windows (1 AM too2 AM, m 2 AM too3, czy 3 AM too4 i tak dalej). Ta możliwość jest przydatne podczas wykonywania historycznych obciążenia. możliwość kopiowania równoległych Hello stosuje tooa **pojedynczy uruchamiania działania**.

Oto przykładowy scenariusz. W hello poniższy przykład wiele wycinków z ostatnich hello konieczne toobe przetworzone. Fabryka danych uruchamia wystąpienia działania kopiowania (Uruchom działania) dla każdego wycinka:

* wycinek danych Hello z pierwszym oknie działanie hello (1 AM too2 m) == > działania Uruchom 1
* wycinek danych Hello z drugiego okna działania hello (2 AM too3 AM) == > działania Uruchom 2
* wycinek danych Hello z drugiego okna działania hello (3 AM too4 AM) == > działania Uruchom 3

I tak dalej.

W tym przykładzie, gdy hello **współbieżności** wartość too2, **działania Uruchom 1** i **działania Uruchom 2** skopiować dane z dwóch okien działania **jednocześnie**  wydajność przepływu danych tooimprove. Jednak jeśli wiele plików są skojarzone z działania Uruchom 1, usługa przenoszenia danych hello kopiuje pliki z hello źródła toohello docelowego jeden plik w czasie.

### <a name="cloud-data-movement-units"></a>Jednostki przepływu danych w chmurze
A **jednostki przepływu danych w chmurze (DMU)** jest miary, która reprezentuje hello zasilania (kombinacja Procesora, pamięci i alokacji zasobów sieciowych) z pojedynczą jednostkę w fabryce danych. DMU może być używany w operacji kopiowania w chmurze do chmury, ale nie w kopii hybrydowej.

Domyślnie fabryki danych używa jednej chmurze DMU tooperform uruchamiania pojedynczego działania kopiowania. toooverride to ustawienie domyślne, określ wartość hello **cloudDataMovementUnits** właściwości w następujący sposób. Informacje o poziomie hello są bardziej wydajne może spowodować, że po skonfigurowaniu więcej jednostek dla konkretnej kopii źródłowy i odbiorczy, zobacz hello [dotyczące wydajności](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Witaj **dozwolone wartości** dla hello **cloudDataMovementUnits** właściwości są 1 (domyślna), 2, 4, 8, 16, 32. Witaj **rzeczywistą liczbę chmury DMUs** używany w czasie wykonywania operacji kopiowania hello jest równa tooor mniejsza niż wartość hello skonfigurowane, w zależności od Twojego wzorca danych.

> [!NOTE]
> Jeśli potrzebujesz więcej chmury DMUs umożliwiających uzyskanie większej produktywności, skontaktuj się z [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/). Obecnie działa tylko wtedy, gdy ustawienie 8 i nowszych możesz **skopiować wielu plików z obiektu Blob magazynu/Data Lake Store/Amazon S3/w chmurze SFTP FTP/w chmurze tooBlob magazynu/Data Lake Store/usługi Azure SQL Database**.
>

### <a name="parallelcopies"></a>parallelCopies
Można użyć hello **parallelCopies** równoległości hello tooindicate właściwości, które mają toouse działanie kopiowania. Tej właściwości można traktować jako hello maksymalną liczbę wątków w ramach działania kopiowania, który może odczytywać źródła lub zapisać magazyny danych zbiornika tooyour równolegle.

Dla każdego działania kopiowania Uruchom fabryki danych określa hello liczbę równolegle kopiuje toouse toocopy dane z magazynu danych źródła hello i magazyn danych docelowy toohello. Witaj domyślną liczbę równoległych kopii, których używa zależy od typu hello źródłowy i odbiorczy, którego używasz.  

| Źródłowy i odbiorczy | Liczba równoległych kopii domyślne określone przez usługę |
| --- | --- |
| Kopiowanie danych między magazynów opartych na plikach (magazynu obiektów Blob; Data Lake Store; Amazon S3; lokalnego systemu plików; lokalny system plików HDFS) |Od 1 do 32. Zależy od rozmiaru hello hello plików oraz hello numer jednostki przepływu danych w chmurze (DMUs), toocopy używanych danych między dwa magazyny danych w chmurze lub hello fizyczną konfigurację hello maszyna bramy używana do kopii hybrydowej (toocopy danych tooor z lokalnego magazynu danych ). |
| Kopiowanie danych z **magazynu tabel tooAzure przechowywania wszystkie źródła danych** |4 |
| Wszystkie inne źródłowy i odbiorczy pary |1 |

Zazwyczaj hello domyślne zachowanie powinien zapewnić hello najlepsze przepływności. Jednak toocontrol hello obciążenia na maszynach hostujących magazyny danych lub tootune wydajności kopii, mogą wybrać wartość domyślną hello toooverride, określ wartość hello **parallelCopies** właściwości. Witaj, wartość musi być od 1 do 32 (zarówno z wartościami granicznymi). W czasie wykonywania, aby uzyskać najlepszą wydajność hello, działanie kopiowania używa wartość, która jest mniejsza lub równa toohello wartość ustawiona.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Toonote punktów:

* Po skopiowaniu danych między magazynów opartych na plikach hello **parallelCopies** określić równoległości hello na poziomie pliku hello. Witaj podziału w jednym pliku sytuacja może mieć miejsce pod automatycznie i w przezroczysty sposób i jest przeznaczona toouse hello najlepsze odpowiedni rozmiar fragmentu danego źródła magazynu danych wpisz dane tooload tooparallelCopies równoległych i prostopadły. Witaj rzeczywista liczba równoległych kopii hello danych przepływu usługi używa dla operacji kopiowania hello w czasie wykonywania jest nie więcej niż hello liczbę plików. Jeśli jest zachowanie kopii hello **mergeFile**, aktywność kopiowania nie może korzystać z równoległości poziomie plików.
* Po określeniu wartość hello **parallelCopies** właściwość, należy wziąć pod uwagę wzrost obciążenia hello na źródłowy i odbiorczy magazynów danych i toogateway, jest kopią hybrydowego. Dzieje się to szczególnie jeśli masz wiele działań lub równoczesnych uruchomień hello tego samego działania, które wykonywane hello tego samego magazynu danych. Jeśli zauważysz jest przeciążony hello magazynu danych lub bramy z hello obciążenia, Zmniejsz hello **parallelCopies** wartość toorelieve hello obciążenia.
* Po skopiowaniu danych z magazynów, które nie są toostores opartych na plikach, które są oparte na pliku usługi przenoszenia danych hello ignoruje hello **parallelCopies** właściwości. Nawet wtedy, gdy określono równoległości, nie zostanie zastosowane w tym przypadku.

> [!NOTE]
> Należy użyć hello toouse 1.11 lub nowszej wersji bramy zarządzania danymi **parallelCopies** funkcji po wykonaniu kopii hybrydowej.
>
>

toobetter te dwie właściwości i tooenhance Twojego przepływność przepływu danych, zobacz hello [przykładowe przypadki użycia](#case-study-use-parallel-copy). Nie ma potrzeby tooconfigure **parallelCopies** tootake zaletą hello domyślne zachowanie. Jeśli skonfigurujesz i **parallelCopies** jest za mały, chmury wielu DMUs może nie być w pełni wykorzystywane.  

### <a name="billing-impact"></a>Wpływ rozliczeń
Ma ona **ważne** tooremember, które są naliczane na podstawie hello całkowita czasu hello operacji kopiowania. Jeśli zadanie kopiowania używane tootake godzinę z jednostką jednej chmury i obecnie trwa 15 minut z czterech jednostki chmury, hello ogólną pozostaje rachunku prawie hello takie same. Na przykład używasz cztery jednostki chmury. pierwszy jednostki chmury Hello spędza na 10 minut, hello drugi 10 minut, hello trzeci z nich 5 minut i hello czwarty jeden, 5 minut, wszystko w jednym uruchamiania działania kopiowania. Naliczane są opłaty za hello całkowita kopiowania (przenoszenie danych) czas, który jest 10 + 10 + 5 + 5 = 30 minut. Przy użyciu **parallelCopies** nie ma wpływu na rozliczenia.

## <a name="staged-copy"></a>Kopiuj przemieszczanego
Po skopiowaniu danych z magazynu danych źródła danych magazynu tooa odbioru można toouse magazynu obiektów Blob jako magazyn tymczasowy tymczasowej. Przemieszczania jest szczególnie przydatna w hello w następujących przypadkach:

1. **Chcesz tooingest dane z różnych baz danych do usługi SQL Data Warehouse przy użyciu programu PolyBase**. Usługi SQL Data Warehouse używa PolyBase jako mechanizm wysokiej przepustowości tooload dużej ilości danych do usługi SQL Data Warehouse. Jednak hello źródło danych musi być w magazynie obiektów Blob i musi spełniać kryteria. Podczas ładowania danych z magazynu danych innego niż magazynu obiektów Blob, możesz przeprowadzić aktywację dane kopiowanie za pośrednictwem tymczasowego przemieszczania magazynu obiektów Blob. W takim przypadku fabryki danych wykonuje tooensure przekształcenia danych hello wymagane spełnia wymagania hello PolyBase. Następnie używa PolyBase tooload danych do usługi SQL Data Warehouse. Aby uzyskać więcej informacji, zobacz [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).
2. **Czasami zajmie trochę czasu tooperform przenoszenia danych hybrydowych (to znaczy toocopy między z lokalnym magazynem danych i magazynu danych w chmurze) przez powolne połączenie sieciowe**. wydajność tooimprove można skompresować hello danych w sieci lokalnej, aby przyspieszyć mniej czasu przechowywania danych tymczasowych toohello toomove danych w chmurze hello. Następnie można zdekompresować danych hello w hello przemieszczania magazynu, przed załadowaniem do magazynu danych docelowy hello.
3. **Nie chcesz tooopen porty inne niż port 80 i portu 443 w zaporze, z powodu zasad firmowych IT**. Na przykład podczas kopiowania danych z ujścia danych bazy danych SQL Azure tooan magazynu lokalnego lub ujścia magazynu danych SQL Azure, należy tooactivate wychodzącego komunikacji TCP na porcie 1433 dla zapory systemu Windows hello i firmowej zapory. W tym scenariuszu skorzystaj z hello toofirst kopiowania danych tooa obiektu Blob magazynu przemieszczania wystąpienie bramy za pośrednictwem protokołu HTTP lub HTTPS na porcie 443. Następnie ładowanie danych hello do bazy danych SQL lub SQL Data Warehouse z obszaru przemieszczania magazynu obiektów Blob. W tym przepływie nie trzeba tooenable portu 1433.

### <a name="how-staged-copy-works"></a>Jak przemieszczanego działania kopiowania
Po uaktywnieniu hello przemieszczania funkcji pierwszy dane hello zostaną skopiowane z magazynu danych na potrzeby przemieszczania hello źródła danych magazynu toohello (użycie własnego). Następnie hello dane są kopiowane z hello przemieszczania magazynu danych zbiornika toohello magazynu danych. Fabryka danych automatycznie zarządza hello dwuetapowa przepływu dla Ciebie. Fabryka danych także czyści dane tymczasowe z hello przemieszczania magazynu po zakończeniu przenoszenia danych hello.

W scenariuszu kopiowania chmury hello (źródłowy i odbiorczy dane magazynów znajdują się w chmurze hello) bramy nie jest używany. Witaj usługi fabryka danych wykonuje operacje kopiowania hello.

![Przemieszczane kopiowania: Scenariusz chmury](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

W scenariuszu kopiowania hybrydowego hello (źródło jest lokalnie i sink znajduje się w chmurze hello), bramy hello przenosi tooa przemieszczania magazynu danych magazynu danych z hello źródła danych. Magazyn danych z hello przemieszczania danych magazynu danych zbiornika toohello przenosić usługi fabryka danych. Kopiowanie danych z tooan magazynu danych chmury lokalnego magazynu danych za pośrednictwem trybu przejściowego także jest obsługiwany z przepływem hello wycofane.

![Przemieszczane kopiowania: scenariusza hybrydowego](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Po uaktywnieniu przepływu danych przy użyciu tymczasowego magazynu można określić, czy mają hello toobe dane skompresowane przed przeniesieniem danych ze źródła hello danych przechowywać przejściowej tooan lub magazynu danych na potrzeby przemieszczania, a następnie dekompresowane przed przenoszenia danych z przejściowej lub przemieszczania magazynu toohello ujście danych magazynu danych.

Obecnie nie można skopiować danych między dwa lokalnych magazynów danych przy użyciu magazynu tymczasowego. Oczekujemy, ta opcja toobe dostępne wkrótce.

### <a name="configuration"></a>Konfiguracja
Skonfiguruj hello **enableStaging** ustawienie w toospecify działanie kopiowania czy hello toobe dane umieszczane w magazynie obiektów Blob, przed załadowaniem do magazynu danych docelowym. Podczas ustawiania **enableStaging** tooTRUE, określić dodatkowe właściwości hello na liście hello następnej tabeli. Jeśli nie masz, należy również toocreate magazynu Azure lub magazynu udostępnionego usługi połączone podpisu dostępu dla przemieszczania.

| Właściwość | Opis | Wartość domyślna | Wymagane |
| --- | --- | --- | --- |
| **enableStaging** |Określ, czy dane toocopy za pośrednictwem przejściowej przemieszczania magazynu. |False |Nie |
| **linkedServiceName** |Określ nazwę hello [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [element AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) połączonej usługi, która odwołuje się toohello wystąpienie magazynu, który jest używany jako magazyn tymczasowy tymczasowej. <br/><br/> Nie można używać magazynu danych tooload sygnatury dostępu współdzielonego do usługi SQL Data Warehouse przy użyciu programu PolyBase. Można go użyć w innych scenariuszach. |Nie dotyczy |Tak, gdy **enableStaging** ustawiono tooTRUE |
| **Ścieżka** |Określ ścieżki do magazynu obiektów Blob hello czy chcesz toocontain hello umieszczone dane. Jeśli ścieżka nie zostanie określona, usługa hello tworzy dane tymczasowe toostore kontenera. <br/><br/> Określ ścieżkę tylko w przypadku używania magazynu z sygnatury dostępu współdzielonego lub wymagają toobe dane tymczasowe w określonej lokalizacji. |Nie dotyczy |Nie |
| **enableCompression** |Określa, czy dane powinny kompresowane, zanim zostanie skopiowany toohello docelowego. To ustawienie ogranicza hello ilość transferowanych danych. |False |Nie |

Oto przykładowe definicji działania kopiowania z właściwościami hello, które zostały opisane w powyższej tabeli hello:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Wpływ rozliczeń
Są naliczane na podstawie dwa kroki: kopiowanie czas trwania i skopiować typu.

* Gdy używasz przemieszczania podczas kopiowania chmury (kopiowanie danych z magazynu danych chmury tooanother chmury danych magazynu), naliczane są opłaty hello [łączny czas trwania kopiowania kroki 1 i 2] x [cenie jednostkowej kopiowania chmury].
* Gdy używasz przemieszczania podczas kopiowania hybrydowych (kopiowanie danych z magazynu danych chmury tooa magazynu lokalnego danych), naliczane są opłaty [hybrydowego kopiowania czas] x [cenie jednostkowej kopiowania hybrydowego] + [czas trwania kopiowania w chmurze] x [cenie jednostkowej kopiowania chmury].

## <a name="performance-tuning-steps"></a>Kroki dostrajania wydajności
Zalecamy tootune hello wydajności usługi fabryka danych z działania kopiowania należy wykonać następujące czynności:

1. **Ustalanie linii bazowej**. W fazie programowanie hello przetestować potoku sieci za pomocą działania kopiowania przed przykładowych danych reprezentatywnych. Można użyć hello fabryki danych [fragmentowania modelu](data-factory-scheduling-and-execution.md) toolimit hello ilość danych z.

   Zbieranie czasu wykonywania i charakterystyki wydajności przy użyciu hello **monitorowanie i zarządzanie aplikacjami**. Wybierz **Monitor & Zarządzaj** na stronie głównej fabryki danych. W widoku drzewa hello wybierz hello **wyjściowy zestaw danych**. W hello **okien działania** wybierz hello uruchamiania działania kopiowania. **Okien działania** Wyświetla czas trwania działania kopiowania hello i hello rozmiar danych hello, który jest skopiowany. Przepływność Hello jest wymieniony w **działania okna Eksploratora**. Zobacz toolearn więcej informacji na temat aplikacji hello [monitora i zarządzanie nimi potoki fabryki danych Azure przy użyciu hello monitorowanie i zarządzanie aplikacjami](data-factory-monitor-manage-app.md).

   ![Szczegóły uruchamiania działania](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   W dalszej części artykułu hello możesz porównać hello wydajności i konfiguracji Twojego scenariusza tooCopy działania w [dotyczące wydajności](#performance-reference) z naszych testów.
2. **Diagnozowanie i zoptymalizować wydajność**. Hello wydajności, które należy obserwować nie spełnia Twoich oczekiwań, należy najpierw tooidentify wąskich gardeł wydajności. Następnie optymalizacji wydajności tooremove lub zmniejszyć wpływ hello wąskich gardeł. Pełny opis wydajności diagnostyki wykracza poza zakres tego artykułu hello, ale poniżej przedstawiono niektóre typowe kwestie wymagające rozważenia:

   * Funkcje wydajności:
     * [Kopiuj równoległych](#parallel-copy)
     * [Jednostki przepływu danych w chmurze](#cloud-data-movement-units)
     * [Kopiuj przemieszczanego](#staged-copy)
     * [Skalowalność zarządzania bramy danych](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Brama zarządzania danymi](#considerations-for-data-management-gateway)
   * [Źródło](#considerations-for-the-source)
   * [Obiekt sink](#considerations-for-the-sink)
   * [Serializacja i deserializacja](#considerations-for-serialization-and-deserialization)
   * [Kompresja](#considerations-for-compression)
   * [Mapowanie kolumny](#considerations-for-column-mapping)
   * [Inne zagadnienia](#other-considerations)
3. **Rozwiń węzeł hello konfiguracji tooyour cały zestaw danych**. Po zakończeniu wyniki wykonania hello i wydajności, można rozwinąć hello definicji i potoku aktywnego okresu toocover cały zestaw danych.

## <a name="considerations-for-data-management-gateway"></a>Zagadnienia dotyczące bramy zarządzania danymi
**Instalator bramy**: zalecane jest użycie dedykowanych maszyny toohost brama zarządzania danymi. Zobacz [zagadnienia dotyczące korzystania z bramy zarządzania danymi](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Monitorowanie bramy i w górę/skalowalnych w poziomie**: pojedyncza brama logicznych z co najmniej jeden węzeł bramy może obsługiwać wiele działanie kopiowania działa na powitania w sam czas jednocześnie. Można wyświetlić migawki czasie niemal rzeczywistym wykorzystania zasobów (CPU, pamięci, network(in/out), itp.) na komputerze bramy, a także hello liczbę współbieżnych zadań uruchomiona, a limit w hello portalu Azure, zobacz [Monitor bramy w portalu hello](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Duże konieczność na hybrydowego przenoszenia danych z dużą liczbą jednoczesnych kopii uruchomień działania lub z dużą ilością danych toocopy, rozważ zbyt[skalowanie w górę i skalowania w poziomie bramy](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) tak toobetter wykorzystywać zasobu lub Skopiuj tooprovision więcej tooempower zasobów. 

## <a name="considerations-for-hello-source"></a>Zagadnienia dotyczące hello źródła
### <a name="general"></a>Ogólne
Upewnij się, że ten hello podstawowy magazyn danych nie jest przeciążony przez innych obciążeń uruchomionych na nim.

Dla magazynów danych firmy Microsoft, zobacz [monitorowania i dostrajania tematy](#performance-reference) które są określone toodata magazynów i ułatwiające zrozumienie, jakie dane przechowywania charakterystyki wydajności, zminimalizować czas reakcji i zmaksymalizować przepustowość.

Po skopiowaniu danych z obiektu Blob magazynu tooSQL hurtowni danych, należy rozważyć użycie **PolyBase** tooboost wydajności. Zobacz [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) szczegółowe informacje. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Magazyny danych opartych na plikach
*(W tym magazynu obiektów Blob, Data Lake Store, Amazon S3, systemów lokalnych plików i lokalnego systemu plików HDFS)*

* **Średni rozmiar pliku i liczba plików**: działanie kopiowania transfery danych jeden plik w czasie. Z samą ilość danych toobe przenieść hello hello ogólną przepustowość jest niższe, jeśli dane hello zawiera wiele małych plików zamiast kilka dużych plików powodu toohello faza inicjowania dla każdego pliku. W związku z tym jeśli to możliwe, połączenie małych plików do większych plików toogain wyższej przepustowości.
* **Plik formatu i kompresji**: więcej sposobów tooimprove wydajności, zobacz hello [uwagi do serializacji i deserializacji](#considerations-for-serialization-and-deserialization) i [zagadnienia dotyczące kompresji](#considerations-for-compression) sekcje.
* Dla hello **lokalnego systemu plików** scenariusz, w którym **brama zarządzania danymi** jest wymagane, zobacz hello [zagadnienia dotyczące bramy zarządzania danymi](#considerations-for-data-management-gateway) sekcji.

### <a name="relational-data-stores"></a>Magazyny danych relacyjnych
*(W tym bazy danych SQL. Magazyn danych SQL; Amazon Redshift; Bazy danych programu SQL Server; i Oracle, MySQL, DB2 Teradata, Sybase i PostgreSQL bazy danych itp.)*

* **Wzorzec danych**: schemat tabeli ma wpływ na przepustowość kopiowania. Rozmiar wiersza dużych zapewnia lepszą wydajność niż rozmiar wiersza małych, toocopy hello samą ilość danych. Przyczyna Hello jest tej bazy danych hello wydajniej mogą pobierać partie mniej danych, które zawierają mniej wierszy.
* **Zapytanie lub procedura składowana**: Optymalizacja logiki hello hello zapytań lub procedurze składowanej Określ hello działanie kopiowania źródła toofetch danych wydajniej.
* Dla **lokalnych relacyjnych baz danych**, takie jak SQL Server i Oracle, które wymagają stosowania hello **brama zarządzania danymi**, zobacz hello [zagadnienia dotyczące bramy zarządzania danymi](#considerations-on-data-management-gateway) sekcji.

## <a name="considerations-for-hello-sink"></a>Zagadnienia dotyczące hello odbioru
### <a name="general"></a>Ogólne
Upewnij się, że ten hello podstawowy magazyn danych nie jest przeciążony przez innych obciążeń uruchomionych na nim.

Magazyny danych firmy Microsoft, można znaleźć zbyt[monitorowania i dostrajania tematy](#performance-reference) , które są określone toodata magazynów. Te tematy mogą ułatwić zrozumienie charakterystyki wydajności magazynu danych i jak czas odpowiedzi toominimize i zmaksymalizować przepustowość.

Jeśli kopiujesz dane z **magazynu obiektów Blob** zbyt**SQL Data Warehouse**, należy rozważyć użycie **PolyBase** tooboost wydajności. Zobacz [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) szczegółowe informacje. Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Magazyny danych opartych na plikach
*(W tym magazynu obiektów Blob, Data Lake Store, Amazon S3, systemów lokalnych plików i lokalnego systemu plików HDFS)*

* **Skopiuj zachowanie**: po skopiowaniu danych z magazynu danych opartych na plikach różne działania kopiowania zawiera trzy pozycje za pośrednictwem hello **copyBehavior** właściwości. Ją zachowuje hierarchię, spłaszcza hierarchii lub scala plików. Zachowywanie albo zmniejszenie liczby poziomów hierarchii ma niewielkiego lub żadnego zmniejszenie wydajności, ale scalanie plików powoduje tooincrease zmniejszenie wydajności.
* **Plik formatu i kompresji**: hello zobacz [uwagi do serializacji i deserializacji](#considerations-for-serialization-and-deserialization) i [zagadnienia dotyczące kompresji](#considerations-for-compression) sekcje na więcej sposobów tooimprove wydajności .
* **Magazyn obiektów blob**: obecnie obsługuje magazynu obiektów Blob tylko blokowe obiekty BLOB do transferu danych zoptymalizowanych i przepływności.
* Dla **lokalnych systemów plików** scenariusze, które wymagają stosowania hello **brama zarządzania danymi**, zobacz hello [zagadnienia dotyczące bramy zarządzania danymi](#considerations-for-data-management-gateway) sekcji.

### <a name="relational-data-stores"></a>Magazyny danych relacyjnych
*(W tym bazy danych SQL, SQL Data Warehouse, baz danych programu SQL Server i Oracle — bazy danych)*

* **Skopiuj zachowanie**: w zależności od ustawionych dla właściwości hello **sqlSink**, działanie kopiowania zapisuje dane toohello docelowej bazy danych na różne sposoby.
  * Domyślnie program hello danych przepływu danych tooinsert API kopiowania zbiorczego hello w Dołącz tryb, który zawiera usługi używa hello najlepszą wydajność.
  * Jeśli skonfigurujesz procedury składowanej w ujściu hello hello bazy danych ma zastosowanie jeden wiersz danych hello w momencie zamiast jako ładowania zbiorczego. Wydajność porzuca znacznie. Jeśli zestaw danych jest duży, jeśli ma to zastosowanie, rozważ przejście toousing hello **sqlWriterCleanupScript** właściwości.
  * Jeśli skonfigurujesz hello **sqlWriterCleanupScript** Uruchom właściwości dla każdego działania kopiowania, hello usługi wyzwalaczy hello skryptu, a następnie można użyć hello API kopiowania zbiorczego tooinsert hello danych. Na przykład toooverwrite hello całą tabelę z hello najnowsze dane, można określić toofirst skryptu Usuń wszystkie rekordy przed ładowanie zbiorcze hello nowe dane ze źródła hello.
* **Rozmiar danych wzorca i partii**:
  * Schemat tabeli ma wpływ na przepustowość kopiowania. toocopy hello samą ilość danych, rozmiar wiersza dużych zapewnia lepszą wydajność niż rozmiar wiersza małych ponieważ hello bazy danych można zatwierdzić wydajniej mniej partie danych.
  * Działanie kopiowania wstawia danych w serii partii. Należy określić hello liczbę wierszy w partii, przy użyciu hello **writeBatchSize** właściwości. Jeśli dane mają małe wiersze, można ustawić hello **writeBatchSize** właściwość o wyższych toobenefit wartość mniejszy narzut partii i wyższej przepustowości. Jeśli rozmiar wiersza hello danych jest duży, należy zachować ostrożność, wraz ze zwiększeniem **writeBatchSize**. Wysokiej wartości może prowadzić tooa kopiowania niepowodzenia spowodowane przeciążeniem hello bazy danych.
* Dla **lokalnych relacyjnych baz danych** , takich jak SQL Server i Oracle, które wymagają stosowania hello **brama zarządzania danymi**, zobacz hello [zagadnienia dotyczące bramy zarządzania danymi](#considerations-for-data-management-gateway) sekcji.

### <a name="nosql-stores"></a>Magazynów NoSQL
*(W tym magazynu tabel i bazy danych rozwiązania Cosmos Azure)*

* Aby uzyskać **tabeli magazynu**:
  * **Partycja**: znacznie zapisu danych partycji toointerleaved powoduje spadek wydajności. Sortuj źródło danych przez klucz partycji, tak aby hello dane są wstawiane wydajnie do jednej partycji po drugim lub Dostosuj hello logiki toowrite hello danych tooa jednej partycji.
* Aby uzyskać **rozwiązania Cosmos Azure DB**:
  * **Rozmiar partii**: hello **writeBatchSize** właściwość ustawia hello liczba równoległych żądań toohello bazy danych Azure rozwiązania Cosmos usługi toocreate dokumentów. Lepszą wydajność można oczekiwać, wraz ze zwiększeniem **writeBatchSize** ponieważ więcej żądań równoległe są wysyłane tooAzure DB rozwiązania Cosmos. Jednak obserwować ograniczania przepustowości podczas pisania tooAzure DB rozwiązania Cosmos (hello jest komunikat o błędzie "Żądania jest duża szybkość"). Różne czynniki mogą spowodować ograniczanie rozmiar dokumentu, w tym liczbę hello w dokumentach hello i hello zasady indeksowania w kolekcji docelowej. tooachieve wyższej przepustowości kopiowania, rozważ użycie lepsze kolekcji, na przykład S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Zagadnienia dotyczące serializacja i deserializacja
Serializacja i deserializacja może wystąpić, gdy Twoje wejściowy zestaw danych lub zestawu danych wyjściowych jest plikiem. Zobacz [obsługiwane formaty plików i kompresji](data-factory-supported-file-and-compression-formats.md) ze szczegółami obsługiwane formaty plików przez działanie kopiowania.

**Skopiuj zachowanie**:

* Kopiowanie plików między magazynami danych opartych na plikach:
  * Gdy wejściowych i wyjściowych zestawów danych, które mają hello takie same lub nie ustawienia formatu pliku, usługa przenoszenia danych hello wykonuje kopię binarne bez serializacji lub deserializacji. Zostanie wyświetlony wyższej przepustowości w porównaniu toohello scenariusza, w którym hello źródłowy i odbiorczy ustawienia formatu pliku różnią się od siebie nawzajem.
  * Podczas wprowadzania i dane wyjściowe zestawy danych zarówno w formacie tekstowym i kodowanie hello tylko typ jest inny, usługa przenoszenia danych hello jest wyłącznie Konwersja kodowania. Nie wszystkie serializacji i deserializacji, co powoduje, że pewnego zapasu wydajności porównywane tooa binarne kopiowania.
  * Gdy wejściowych i wyjściowych zestawów danych zarówno ma różnych formatach plików lub różne konfiguracje, takie jak ograniczników hello usługi przenoszenia danych deserializuje źródła danych toostream, przekształcania i serializować go na format danych wyjściowych hello wskazana. Ten wyniki operacji narzut ważniejsze wydajność w porównaniu tooother scenariuszy.
* Podczas kopiowania plików z magazynem danych, który nie jest opartych na plikach (na przykład z magazynu opartego na pliku tooa relacyjnego magazynu) hello serializacji lub deserializacji krok jest wymagany. Ten krok powoduje znaczne obciążenie.

**Format pliku**: format pliku hello wybierzesz może wpłynąć na wydajność kopiowania. Na przykład Avro jest compact format binarny, który przechowuje metadane z danymi. Ma ona szeroki zakres obsługi w ekosystemie Hadoop hello przetwarzania i zapytań. Jednak Avro jest droższe do serializacji i deserializacji niższe przepływności kopiowania, którego wynikiem porównaniu tootext format. Należy wybrać format plików w całej hello całościowo przetwarzania przepływu. Uruchom z danych hello formularza są przechowywane w, źródła danych lub toobe wyodrębniane z systemów zewnętrznych; format najlepszy Hello przechowywania, przetwarzania analitycznego i badania; i w jaki format hello danych powinny być eksportowane do składnic danych programów dla narzędzi do raportowania i wizualizacji. Czasami formacie, który jest nieoptymalne do odczytu i zapisu, wydajność może być dobrym rozwiązaniem, gdy należy wziąć pod uwagę hello ogólne analitycznych procesu.

## <a name="considerations-for-compression"></a>Zagadnienia dotyczące kompresji
Gdy zestaw danych wejściowych lub wyjściowych jest plikiem, można ustawić działanie kopiowania tooperform kompresja lub dekompresja jako miejsce docelowe danych toohello jest zapisywany. Po wybraniu kompresji wprowadzeniu zależności między operacjami wejścia/wyjścia (We/Wy) i procesora CPU. Kompresowanie danych hello koszty dodatkowe w zasoby obliczeniowe. Ale w zamian zmniejsza we/wy sieci i magazynu. W zależności od danych mogą pojawić się zwiększenie wydajności w ogólną przepustowość kopiowania.

**Koder-dekoder**: działanie kopiowania obsługuje typy kompresję Deflate, bzip2 i gzip. Usługa Azure HDInsight mogą używać wszystkich trzech typów przetwarzania. Każdy koder-dekoder kompresji ma zalety. Na przykład bzip2 ma hello najniższy kopiowania przepływności, ale uzyskać hello najlepszą Hive wydajność zapytań z bzip2, ponieważ podziel go do przetwarzania. Gzip jest opcja hello najbardziej zrównoważonym i jest używany hello najczęściej. Wybierz hello koder-dekoder, najlepiej pasującą do Twojego scenariusza end-to-end.

**Poziom**: są dostępne dwie opcje dla każdego koder-dekoder kompresji: najszybciej skompresowane i optymalnie skompresowane. Hello najszybciej skompresowany opcja kompresuje hello dane tak szybko jak to możliwe, nawet jeśli nie jest optymalnie skompresowany plik wynikowy hello. Witaj optymalnie skompresowany opcja zużywa więcej czasu na kompresji i daje minimalnej ilości danych. Można przetestować toosee obie opcje, które zapewnia lepszą wydajność ogólną w Twoim przypadku.

**Wchodzi w grę**: toocopy dużej ilości danych między magazynem lokalnych i chmurze hello, należy wziąć pod uwagę przy użyciu magazynu obiektów blob tymczasowe kompresji. Przy użyciu tymczasowego magazynu jest przydatne, gdy hello przepustowości sieci firmowej i usługami Azure jest czynnikiem ograniczającym hello, i chcesz hello wejściowy zestaw danych i danych wyjściowych ustawione oba toobe w skompresowanej. W szczególności można podzielić działania pojedynczej kopii kopii dwóch działań. Witaj pierwszego kopiowania działania kopie z przejściowej tooan źródła hello lub tymczasowych obiektów blob w postaci skompresowanej. Hello drugi działanie kopiowania kopiuje hello skompresowane dane z obszaru przemieszczania, a następnie dekompresuje podczas zapisuje toohello ujścia.

## <a name="considerations-for-column-mapping"></a>Zagadnienia dotyczące mapowania kolumn
Można ustawić hello **columnMappings** właściwości w działanie kopiowania toomap wszystkie lub podzbiór hello wejściowych kolumn wyjściowych toohello kolumn. Po usługi przenoszenia danych hello odczytuje hello dane ze źródła hello, musi tooperform mapowanie kolumn na powitania danych przed ujścia toohello danych hello jest zapisywany. To dodatkowe przetwarzanie ogranicza przepływność kopiowania.

W przypadku zapytań sklepu źródła danych, na przykład, czy jest relacyjnego magazynu, takich jak SQL Database lub SQL Server, czy jest magazynu NoSQL, takie jak magazyn tabel lub bazy danych rozwiązania Cosmos platformy Azure, należy wziąć pod uwagę wypychanie hello filtrowanie kolumn i zmianę kolejności toohello logiki **zapytania**  właściwości zamiast mapowania kolumn. W ten sposób projekcji hello jest przeprowadzana usługi przenoszenia danych hello odczytuje magazyn danych z hello źródła danych, gdzie jest znacznie większą wydajność.

## <a name="other-considerations"></a>Inne zagadnienia
Gdy hello rozmiar danych ma toocopy jest duży, można dostosować logiki toofurther partycji hello danych biznesowych przy użyciu hello fragmentowania mechanizmu w fabryce danych. Następnie Zaplanuj działanie kopiowania o tej toorun częściej Uruchom rozmiar danych hello tooreduce dla każdego działania kopiowania.

Można ostrożność hello liczbę zestawów danych i działania kopiowania wymagające toohello tooconnector fabryki danych tego samego magazynu danych na powitania sam czas. Wielu zadań jednoczesnych kopii może ograniczyć magazynu danych i prowadzić toodegraded wydajności, skopiuj zadania wewnętrzny ponownych prób, a w niektórych przypadkach niepowodzenia wykonywania.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Przykładowy scenariusz: kopiowanie danych z magazynu lokalnego programu SQL Server tooBlob
**Scenariusz**: potoku jest wbudowana toocopy danych z lokalnego magazynu tooBlob programu SQL Server w formacie CSV. toomake szybciej hello zadanie kopiowania, powinna być kompresowana hello plików CSV do formatu bzip2.

**Badanie i analiza**: hello przepływność działanie kopiowania jest mniej niż 2 MB/s, czyli znacznie mniejsza niż testów porównawczych wydajności hello.

**Analiza wydajności i dostrajania**: tootroubleshoot hello problem z wydajnością, Przyjrzyjmy się jak danych hello jest przetwarzany i przenieść.

1. **Odczytanie danych**: Brama otwiera tooSQL połączenia serwera i wysyła hello zapytania. SQL Server odpowiada, wysyłając tooGateway strumienia danych hello za pośrednictwem sieci intranet hello.
2. **Serializować i kompresji danych**: format tooCSV strumienia danych hello serializuje bramy i kompresuje hello strumienia bzip2 tooa danych.
3. **Zapisu danych**: hello bzip2 strumienia tooBlob magazynu za pośrednictwem Internetu hello przekazuje bramy.

Jak widać, dane hello są przetwarzane i przenoszone przesyłania strumieniowego sekwencyjnie: SQL Server > LAN > bramy > WAN > magazynu obiektów Blob. **Witaj ogólną wydajność jest uzyskiwany za hello minimalnej przepustowości w potoku hello**.

![Przepływ danych](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Co najmniej jednego z następujących czynników hello może spowodować hello wąskie gardło:

* **Źródło**: sam serwer SQL ma niskiej przepustowości z powodu dużymi obciążeniami.
* **Brama zarządzania danymi**:
  * **LAN**: bramy znajduje się daleko od hello komputera programu SQL Server i ma połączenie o niskiej przepustowości.
  * **Brama**: bramy osiągnęła jego hello tooperform ograniczenia obciążenia następujące operacje:
    * **Serializacja**: serializacja tooCSV strumienia danych hello format ma powolne przepływności.
    * **Kompresja**: wybrano koder-dekoder kompresji powolne (na przykład, bzip2, czyli Core i7 2,8 MB/s).
  * **WAN**: brakuje hello przepustowość między siecią firmową hello i usługami Azure (na przykład T1 = 1,544 KB/s; T2 = 6,312 KB/s).
* **Obiekt sink**: magazyn obiektów Blob ma niskiej przepustowości. (W tym scenariuszu jest mało prawdopodobne, ponieważ jego umowy dotyczącej poziomu usług gwarantuje co najmniej 60 MB/s).

W takim przypadku kompresji danych bzip2 może być spowolnieniem hello całego procesu. Przełączanie koder-dekoder kompresji gzip tooa może ułatwić to "wąskie gardło".

## <a name="sample-scenarios-use-parallel-copy"></a>Przykładowe scenariusze: Użyj równoległych kopii
**Scenariusz I:** skopiuj pliki 1 MB 1000 z hello lokalnego pliku system tooBlob magazynu.

**Analiza i dostrajania wydajności**: na przykład jeśli jest zainstalowana brama na komputerze czterordzeniowe fabryki danych używa 16 równoległych kopii toomove plików z magazynu tooBlob system plików hello jednocześnie. To wykonywanie równoległe powinno spowodować wysokiej przepływności. Można również jawnie określić liczbę równoległych kopii hello. Podczas kopiowania wiele małych plików, równoległe kopie znacznie pomocy przepływność przy użyciu zasobów bardziej efektywnie.

![Scenariusz 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Scenariusz II**: Skopiuj 20 obiekty BLOB 500 MB z obiektu Blob magazynu tooData takie magazynu, a następnie dostrajania wydajności.

**Analiza i dostrajania wydajności**: W tym scenariuszu fabryki danych kopiuje hello dane z magazynu obiektów Blob tooData Lake — magazyn przy użyciu pojedynczej kopii (**parallelCopies** ustawić too1) i danych w chmurze pojedynczej jednostki przepływu. Witaj przepływności widoczny będzie Zamknij toothat opisanego w hello [wydajności odwołanie sekcji](#performance-reference).   

![Scenariusz 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Scenariusz III**: rozmiar pliku jest większy niż dziesiątki MB i całkowitej ilości jest duży.

**Analiza i włączanie wydajności**: zwiększenie **parallelCopies** nie zapewnia lepszą wydajność kopiowania z powodu ograniczenia zasobów hello DMU jednym chmury. Zamiast tego należy określić chmury więcej DMUs tooget więcej zasobów tooperform hello przenoszenia danych. Nie określaj wartości dla hello **parallelCopies** właściwości. Fabryka danych obsługuje hello równoległości dla Ciebie. W tym przypadku jeśli ustawisz **cloudDataMovementUnits** too4, przepływności około cztery razy występuje.

![Scenariusz 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Dokumentacja
Poniżej przedstawiono monitorowania wydajności i dostrajania odwołań dla niektórych hello obsługiwane magazyny danych:

* Magazyn Azure (w tym magazynie obiektów Blob i Magazyn tabel): [wartości docelowe skalowalności magazynu Azure](../storage/common/storage-scalability-targets.md) i [Lista kontrolna wydajności i skalowalności magazynu Azure](../storage/common/storage-performance-checklist.md)
* Azure SQL Database: Można [monitorować wydajność hello](../sql-database/sql-database-single-database-monitor.md) i sprawdź hello bazy danych transakcji jednostki (bazy danych DTU) procent
* Usługa Azure SQL Data Warehouse: Zdolność jest mierzony w jednostki magazynu danych (dwu); zobacz [Zarządzaj obliczeniowe zasilania w usłudze Azure SQL Data Warehouse (omówienie)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure DB rozwiązania Cosmos: [poziomy wydajności w usłudze Azure DB rozwiązania Cosmos](../documentdb/documentdb-performance-levels.md)
* Lokalny program SQL Server: [monitora i dostrajanie wydajności](https://msdn.microsoft.com/library/ms189081.aspx)
* Lokalny serwer plików: [dostrajania wydajności dla serwerów plików](https://msdn.microsoft.com/library/dn567661.aspx)
