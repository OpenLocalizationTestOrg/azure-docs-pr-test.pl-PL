---
title: "dane aaaExplore usługi Hadoop klastra i tworzenia modeli w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Za pomocą hello proces nauki danych zespołu scenariusz end-to-end wykorzystujących usługi HDInsight Hadoop klastra toobuild i wdrożenia modelu za pomocą publicznie dostępnych zestawu danych."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Hello proces nauki danych zespołu w działaniu: klastrów użycia usługi Azure HDInsight Hadoop
W tym przewodniku używamy hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md) w scenariuszu end-to-end przy użyciu [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj i funkcji danych odtwarzania z hello publicznie dostępne [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych i toodown przykładowe dane hello. Modele danych hello są tworzone z usługi Azure Machine Learning toohandle binarnej i wieloklasowej klasyfikacji i regresji predykcyjnej zadania.

Aby uzyskać wskazówki, który pokazuje, jak toohandle większy zestaw danych (1 terabajt) podobny scenariusz za pomocą usługi HDInsight Hadoop clusters do przetwarzania danych, zobacz [zespołu danych nauki proces — za pomocą usługi Azure HDInsight klastrów platformy Hadoop w zestawie danych 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Jest również możliwe toouse hello tooaccomplish notesu IPython zadań wskazówki przedstawioną hello przy użyciu zestawu hello 1 TB danych. Użytkownicy, którzy będą jak tootry takie podejście powinni skontaktować hello [wskazówki Criteo za pomocą połączenia ODBC programu Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tematu.

## <a name="dataset"></a>Opis elementu Dataset rund taksówki NYC
Hello danych podróży taksówki NYC około 20GB skompresowanego wartości rozdzielanych przecinkami (CSV) plików (~ 48GB nieskompresowane), składającej się z więcej niż 173 milionów poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży. Każdy rekord podróży obejmuje hello odbiór i przyjmowania lokalizacji i czasu, numer licencji hack anonimowe (sterownik) i numer Medalionu (taksówki jego unikatowy identyfikator). Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:

1. pliki CSV "trip_data" Hello zawierają szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. pliki CSV "trip_fare" Hello zawierają szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z pola hello: Medalionu, hack\_licencji i pobrania\_daty/godziny.

tooget wszystkie hello szczegóły odpowiednich tooa określonego podróży, jest wystarczające toojoin z trzech kluczy: "Medalionu" hello "hack\_licencji" i "podnoszenia\_datetime".

Firma Microsoft opisano niektóre szczegółowe dane hello, gdy są przechowywane ich do tabele programu Hive wkrótce.

## <a name="mltasks"></a>Przykłady prognozowania zadań
Gdy zbliża się data, określania hello rodzaj prognoz, które chcesz toomake oparte na analizie jego pomaga wyjaśnienia hello zadań w procesie należy tooinclude.
Poniżej przedstawiono trzy przykłady problemów prognozowania, które można rozwiązać w ramach tego przewodnika, w której skład opiera się na powitania *Porada\_kwota*:

1. **Klasyfikacji binarnej**: prognozowania, czy etykietki został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 jest ujemny przykład.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Wieloklasowej klasyfikacji**: zakres hello toopredict kwot Porada uregulowaniu płatności hello podróży. Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Zadanie regresji**: toopredict hello ilość Porada hello płatnej w podróży.  

## <a name="setup"></a>Konfigurowanie klastra usługi HDInsight Hadoop zaawansowana analityka
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

Można skonfigurować środowiska platformy Azure zaawansowana analityka używającego klastra usługi HDInsight w trzy kroki:

1. [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md): to konto magazynu jest używany do przechowywania danych w magazynie obiektów Blob Azure. dane Hello używane w klastrach HDInsight również znajdują się tutaj.
2. [Dostosowywanie Azure HDInsight Hadoop clusters dla hello zaawansowane procesu analizy i technologii](machine-learning-data-science-customize-hadoop-cluster.md). Spowoduje to utworzenie Azure HDInsight Hadoop, klaster z 64-bitowych Anaconda Python 2.7 zainstalowane we wszystkich węzłach. Istnieją dwa tooremember ważne czynności podczas dostosowywania z klastrem usługi HDInsight.
   
   * Należy pamiętać, konta magazynu hello toolink utworzonego w kroku 1 z klastrem usługi HDInsight, podczas jej tworzenia. To konto magazynu jest tooaccess używane dane, które są przetwarzane w ramach klastra hello.
   * Po utworzeniu klastra hello włączyć dostęp zdalny toohello węzła głównego klastra hello. Przejdź toohello **konfiguracji** i kliknij polecenie **Włącz zdalne**. Ten krok określa hello poświadczenia użytkownika używane do logowania zdalnego.
3. [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md): modeli uczenia maszynowego toobuild używane jest to Azure Machine Learning obszaru roboczego. To zadanie zostanie rozwiązana po zakończeniu Eksploracja danych początkowych i w dół próbkowania przy użyciu hello klastra usługi HDInsight.

## <a name="getdata"></a>Pobierz dane hello ze źródła publiczny
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

tooget hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych z lokalizacji publicznej, możesz użyć dowolnej z metod hello opisanego w [tooand przenoszenia danych z magazynu obiektów Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello danych tooyour maszyny.

Opisano sposób użycia narzędzia AzCopy tootransfer hello pliki zawierający dane. toodownload i zainstaluj narzędzie AzCopy postępuj zgodnie z instrukcjami hello w [wprowadzenie hello wiersza polecenia Azcopy](../storage/common/storage-use-azcopy.md).

1. Z poziomu okna wiersza polecenia wystawiać hello następujące polecenia narzędzia AzCopy, zastępując *< path_to_data_folder >* z hello docelowej lokalizacji:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Po zakończeniu kopiowania hello łącznie 24 plików zip znajdują się w folderze danych hello wybrany. Rozpakuj hello pobrane pliki toohello tym samym katalogu na komputerze lokalnym. Zanotuj folder hello, w którym znajdują się pliki hello nieskompresowane. Ten folder będzie hello określonego tooas *< ścieżka\_do\_unzipped_data\_pliki\>*  jest poniżej.

## <a name="upload"></a>Przekaż hello toohello domyślny kontener danych klastra usługi Azure HDInsight Hadoop
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

W hello następujące polecenia narzędzia AzCopy, Zastąp hello następujące parametry hello rzeczywiste wartości, które określono podczas tworzenia klastra usługi Hadoop hello i rozpakować hello plików danych.

* ***&#60; path_to_data_folder >*** katalogu hello (wraz ze ścieżką) na komputerze zawierają hello rozpakowane pliki danych  
* ***&#60; nazwa konta magazynu z klastra usługi Hadoop >*** hello konta magazynu skojarzone z klastrem usługi HDInsight
* ***&#60; domyślny kontener klastra usługi Hadoop >*** hello domyślny kontener używane przez klaster. Zanotuj nazwę tego hello domyślnych hello kontenera jest zwykle hello takie same nazwy jako hello samego klastra. Na przykład jeśli hello klastra jest nazywany "abc123.azurehdinsight.net", hello domyślny kontener jest abc123.
* ***&#60; klucz konta magazynu >*** hello klucza dla konta magazynu hello używane przez klaster

Z wiersza polecenia lub okno programu Windows PowerShell na tym komputerze uruchom hello następujące dwa polecenia AzCopy.

To polecenie przekazuje dane podróży hello zbyt***nyctaxitripraw*** katalogu w kontenerze domyślna hello hello klastra usługi Hadoop.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

To polecenie przekazuje dane taryfy hello zbyt***nyctaxifareraw*** katalogu w kontenerze domyślna hello hello klastra usługi Hadoop.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

Hello danych powinna się teraz w magazynie obiektów Blob Azure i gotowe toobe używane w ramach klastra usługi HDInsight hello.

## <a name="#download-hql-files"></a>Zaloguj się do hello węzła głównego klastra usługi Hadoop i i przygotować do analizy danych poznawcze
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

tooaccess hello węzła głównego klastra hello do analizy danych poznawcze i w dół próbkowania hello danych, wykonaj procedurę hello opisane w temacie [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

W tym przewodniku używamy głównie zapytań w [Hive](https://hive.apache.org/), język zapytań SQL przypominającej, tooperform eksploracji wstępne dane. zapytań programu Hive Hello są przechowywane w plikach .hql. Firma Microsoft następnie wyłącza przykładowe to toobe danych używana w usłudze Azure Machine Learning przeznaczone do budowania modeli.

tooprepare hello klastra do analizy danych poznawcze, możemy Pobierz hello .hql pliki zawierające hello odpowiednie skrypty Hive z [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa lokalnego katalogu (C:\temp) na powitania węzła głównego. toodo, otwórz hello **wiersza polecenia** z poziomu hello węzłem głównym hello klastra i problem hello następujące dwa polecenia:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Te dwa polecenia pobierze wszystkie pliki .hql potrzebne w tym katalogu lokalnego toohello wskazówki ***C:\temp &#92;*** w hello węzła głównego.

## <a name="#hive-db-tables"></a>Utwórz gałąź bazy danych i tabele partycjonowane według miesięcy
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

Firma Microsoft są teraz gotowe toocreate tabele programu Hive dla naszego zestawu danych taksówki NYC.
Witaj węzła głównego klastra usługi Hadoop hello, otwórz hello ***wiersza polecenia platformy Hadoop*** na hello pulpitu hello węzła głównego, a następnie wprowadź katalog Hive hello wprowadzając polecenie hello

    cd %hive_home%\bin

> [!NOTE]
> **Uruchom wszystkie polecenia gałęzi w tym przewodniku z hello powyżej Hive bin / directory wiersza. To zajmie się wszelkie problemy, ścieżka automatycznie. Używane hello pojęcia "Hive katalogu wiersza", "bin gałęzi / wiersza katalogu" i "wiersza polecenia usługi Hadoop" zamiennie w tym przewodniku.**
> 
> 

Hello gałęzi katalogu w wierszu polecenia programu wprowadź następujące polecenie w wierszu polecenia Hadoop hello węzła głównego toosubmit hello Hive zapytania toocreate gałąź bazy danych i tabele hello:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Oto hello zawartość hello ***C:\temp\sample\_hive\_utworzyć\_db\_i\_tables.hql*** pliku, który tworzy gałąź bazy danych ***nyctaxidb *** i tabele ***podróży*** i ***taryfy***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Ten skrypt Hive tworzy dwie tabele:

* Tabela "podróży" Hello zawiera szczegóły podróży każdego jazdy (Szczegóły sterownika, czasu odbioru, odległość podróży i razy)
* Tabela "opłata" Hello zawiera szczegóły taryfy (kwota taryfy, kwota poradę, przejazd i opłaty).

Jeśli konieczne uzyskania dodatkowej pomocy w tych procedurach lub mają tooinvestigate tych alternatywnych, zobacz sekcję hello [zapytań Hive przesłać bezpośrednio z hello wiersza polecenia usługi Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Załaduj dane tooHive tabel, partycji
> [!NOTE]
> Jest to zazwyczaj **Admin** zadań.
> 
> 

dataset taksówki Hello NYC ma fizycznych partycjonowania według miesięcy, której używamy tooenable krótszy czas przetwarzania i zapytania. Witaj poniższe polecenia programu PowerShell (wystawiony na podstawie hello gałęzi katalogu przy użyciu hello **wiersza polecenia platformy Hadoop**) załadować danych toohello "podróży" i "opłata" tabele programu Hive podzielona na partycje według miesięcy.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hello *próbki\_hive\_załadować\_danych\_przez\_partitions.hql* plik zawiera następujące hello **ZAŁADOWAĆ** poleceń.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Należy pamiętać, że liczba zapytań programu Hive używanej w tym miejscu w procesu eksploracji hello są związane z jednej partycji lub tylko kilka partycji. Jednak te zapytania może zostać uruchomione przez cały danych hello.

### <a name="#show-db"></a>Pokaż baz danych w hello klastra usługi HDInsight Hadoop
tooshow baz hello danych utworzonych w klastrze usługi HDInsight Hadoop w oknie wiersza polecenia platformy Hadoop hello, uruchom następujące polecenie w wierszu polecenia Hadoop hello:

    hive -e "show databases;"

### <a name="#show-tables"></a>Pokaż tabele programu Hive hello w bazie danych nyctaxidb hello
tabele hello tooshow hello nyctaxidb bazy danych, uruchom następujące polecenie w wierszu polecenia Hadoop hello:

    hive -e "show tables in nyctaxidb;"

Możemy potwierdzić, że tabele hello są dzielone wydając polecenie hello poniżej:

    hive -e "show partitions nyctaxidb.trip;"

Witaj oczekuje się, że dane wyjściowe są wyświetlane poniżej:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Podobnie możemy upewnij się, że ta tabela taryfy hello jest podzielona na partycje wydając polecenie hello poniżej:

    hive -e "show partitions nyctaxidb.fare;"

Witaj oczekuje się, że dane wyjściowe są wyświetlane poniżej:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Eksploracja danych i funkcji inżynieryjne w gałęzi
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Witaj Eksploracja danych i funkcji engineering zadania hello dane ładowane do hello tabele programu Hive można osiągnąć za pomocą zapytań Hive. Poniżej przedstawiono przykłady takich zadań, że firma Microsoft przeprowadzi użytkownika przez proces w tej sekcji:

* Wyświetl hello top 10 rekordów w obu tabel.
* Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.
* Zbadaj jakości danych hello pól długości i szerokości geograficznej.
* Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.
* Generowanie funkcji przez obliczeniowych hello bezpośredniego podróży odległości.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Eksploracja: Wyświetlanie hello top 10 rekordów w podróży tabeli
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

jakie dane hello wygląda toosee, omówione 10 rekordy z każdej tabeli. Uruchom hello oddzielnie następujące dwa zapytania z wiersza katalogu Hive hello hello Hadoop wiersza polecenia konsoli tooinspect hello rekordów.

tooget hello top 10 rekordów w tabeli hello "podróży" z hello pierwszy miesiąc:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello top 10 rekordów w tabeli hello "opłata" z hello miesiąca:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Często jest przydatne toosave hello rekordów tooa pliku w celu wyświetlenia wygodne. Niewielkie zmiany toohello powyżej zapytania rozwiązanie to:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Eksploracja: Wyświetl hello liczby rekordów w każdej partycji 12 hello
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Odsetek jest hello jak hello liczby rund różni się w roku kalendarzowym hello. Grupowanie według miesięcy pozwala nam toosee wygląda tej dystrybucji rund.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Daje hello danych wyjściowych:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

W tym miejscu hello pierwszej kolumny hello miesiąc a hello jest drugi hello liczby rund w danym miesiącu.

Firma Microsoft zliczanie hello całkowita liczba rekordów w naszym zestawie danych podróży wysyłając hello następujące polecenie w wierszu hello gałęzi katalogu.

    hive -e "select count(*) from nyctaxidb.trip;"

Daje to:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Za pomocą polecenia toothose podobne wyświetlane dla zestawu danych w podróży hello, firma Microsoft może wystawiać zapytań programu Hive z wiersza katalogu Hive hello hello taryfy zestawu danych toovalidate hello liczby rekordów.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Daje hello danych wyjściowych:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Należy pamiętać, że hello dokładnie takie same numery rund miesięcznie jest zwracany w obu zestawach danych. Zapewnia to pierwsze sprawdzenie hello tego powitalne danych został załadowany poprawnie.

Zliczanie hello całkowita liczba rekordów w zestawie danych taryfy hello może odbywać się przy użyciu polecenia hello poniżej w wierszu katalogu Hive hello:

    hive -e "select count(*) from nyctaxidb.fare;"

Daje to:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

Całkowita liczba rekordów z obu tabel Hello jest również hello tego samego. Zapewnia to drugi sprawdzania poprawności tego powitalne danych został załadowany poprawnie.

### <a name="exploration-trip-distribution-by-medallion"></a>Eksploracja: Podróży dystrybucji przez Medalionu
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

W tym przykładzie identyfikuje hello Medalionu (taksówki numery) z więcej niż 100 rund w danym okresie. Hello zapytania korzyści z hello na partycje dostępu do tabel, ponieważ należy przygotować przez zmienną partycji hello **miesiąca**. Witaj wyniki zapytania są zapisywane queryoutput.tsv pliku lokalnego tooa `C:\temp` na powitania węzła głównego.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Oto zawartość hello *próbki\_hive\_podróży\_liczba\_przez\_medallion.hql* pliku inspekcji.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Medalionu Hello w zestawie danych taksówki NYC hello identyfikuje unikatowy pliku cab. Firma Microsoft można określić, które pliki cab są "zajęte" pytając, które z nich wprowadzone więcej niż określoną liczbę rund w określonym przedziale czasu. Witaj poniższy przykład identyfikuje pliki cab, wprowadzone w więcej niż stu rund w hello pierwszych trzech miesięcy i zapisuje hello zapytania tooa lokalnego pliku wyników C:\temp\queryoutput.tsv.

Oto zawartość hello *próbki\_hive\_podróży\_liczba\_przez\_medallion.hql* pliku inspekcji.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Z hello gałęzi katalogu wierszu poniższego polecenia hello problemu:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Eksploracja: Podróży dystrybucji Medalionu i hack_license
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Podczas eksplorowania zestawu danych, chcemy często tooexamine hello liczbę wystąpień co grupy wartości. W tej sekcji przedstawiono przykładową jak toodo dla plików cab i sterowników.

Witaj *próbki\_hive\_podróży\_liczba\_przez\_Medalionu\_license.hql* grup plików danych taryfy hello "Medalionu" i "hack_license" i zwraca liczbę każdej kombinacji. Poniżej przedstawiono jego zawartość.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Ta kwerenda zwraca kombinacji określony sterownik, uporządkowanych malejąco liczby rund i cab.

Z hello Hive wiersza katalogu, uruchom:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

wyniki zapytania Hello są zapisywane w pliku lokalnego tooa C:\temp\queryoutput.tsv.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Eksploracja: Oceny jakości danych przez wyszukiwanie rekordów nieprawidłowa długość i szerokość geograficzna
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Typowe celem analizy danych poznawcze jest tooweed się rekordy nieprawidłowe lub uszkodzone. Witaj przykładzie w tej sekcji określa, czy albo hello pola współrzędnych geograficznych zawierać wartości do tej pory spoza hello NYC obszaru. Ponieważ istnieje prawdopodobieństwo, że takie rekordów mają wartości błędne współrzędne geograficzne, chcemy tooeliminate je z żadnych danych toobe używany do modelowania.

Oto zawartość hello *próbki\_hive\_jakości\_assessment.hql* pliku inspekcji.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Z hello Hive wiersza katalogu, uruchom:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Witaj *-S* hello wydruk ekranu stan zadania Hive mapy/Zmniejsz hello pomija argument zawarte w tym poleceniu. Jest to przydatne, ponieważ sprawia, że hello ekranu drukowanie hello Hive wyników zapytania bardziej czytelne.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Eksploracja: Binarny klasy dystrybucje podróży porad
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Opisane w hello problemu klasyfikacji binarnej hello [przykłady zadań prognozowania](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sekcji, czy etykietki został podany lub nie jest przydatne tooknow. Tej dystrybucji porady jest plikiem binarnym:

* Porada podane (klasy 1, porada\_ilość > $0)  
* Brak porady (klasa 0, porada\_kwota = $0).

Witaj *próbki\_hive\_Przechylony\_frequencies.hql* pliku pokazano poniżej robi to.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Z hello Hive wiersza katalogu, uruchom:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Eksploracja: Klasa dystrybucje w ustawieniu wieloklasowej hello
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Witaj wieloklasowej klasyfikacji problemu opisane w hello [przykłady zadań prognozowania](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sekcji ten zestaw danych również jest przydatna tooa klasyfikacji fizycznych gdzie chcielibyśmy toopredict hello ilość porady hello podane. Możemy użyć bins toodefine Porada zakresów w zapytaniu hello. tooget hello dystrybucji klasy dla hello różnych zakresów poradę, używamy hello *próbki\_hive\_Porada\_zakres\_frequencies.hql* pliku. Poniżej przedstawiono jego zawartość.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Uruchom następujące polecenie z wiersza polecenia platformy Hadoop konsoli hello:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Eksploracji: Bezpośrednie odległość między dwiema lokalizacjami współrzędne geograficzne obliczeniowe
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

O miary odległości bezpośredniego hello pozwala nam toofind limit hello rozbieżność między nim a hello rzeczywiste rzeczy przed wyjazdem odległości. Ta funkcja możemy Motywuj przez wskazujące, że osób może być mniejsza prawdopodobnie tootip, jeśli ich dowiedzieć się, że sterownik hello celowo trwało ich drogą znacznie dłużej.

toosee hello porównanie odległość rzeczywiste podróży i hello [odległość Haversine](http://en.wikipedia.org/wiki/Haversine_formula) między dwoma punktami współrzędne geograficzne (hello "koła" wielkiego) używamy funkcje trygonometryczne hello dostępne w gałęzi, w związku z tym:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

W powyższym zapytaniu hello R jest hello promień hello Earth w milach i pi jest tooradians przekonwertowany. Należy zauważyć, że punkty współrzędne geograficzne hello wartości "filtrowane" tooremove daleko od hello NYC obszaru.

W takim przypadku możemy zapisać naszych wyników tooa katalog o nazwie "queryoutputdir". Witaj sekwencji poleceń pokazano poniżej najpierw tworzy ten katalog wyjściowy, a następnie uruchamia polecenie gałęzi hello.

Z hello Hive wiersza katalogu, uruchom:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Witaj wyniki zapytania są zapisywane obiektów blob too9 Azure ***queryoutputdir/000000\_0*** za ***queryoutputdir/000008\_0*** w kontenerze domyślna hello hello klastra usługi Hadoop.

rozmiar hello toosee hello poszczególne obiekty BLOB, przeprowadzana hello następujące polecenie w wierszu katalogu Hive hello:

    hdfs dfs -ls wasb:///queryoutputdir

toosee hello zawartość określonego pliku, powiedz 000000\_0, używamy jego Hadoop `copyToLocal` poleceń, w związku z tym.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal`może być bardzo wolno dla dużych plików, a nie jest zalecane używanie z nimi.  
> 
> 

Zaletą tych danych znajdują się w obiekcie blob Azure jest, że firma Microsoft może Eksplorowanie danych hello w ramach usługi Azure Machine Learning przy użyciu hello [i zaimportuj dane] [ import-data] modułu.

## <a name="#downsample"></a>Przykładowe modele danych i kompilacji w usłudze Azure Machine Learning w dół
> [!NOTE]
> Jest to zazwyczaj **naukowca danych** zadań.
> 
> 

Po faza analizy danych poznawcze hello możemy teraz gotowy toodown przykładowe hello dane przeznaczone do budowania modeli w usłudze Azure Machine Learning. W tej sekcji zostanie przedstawiony sposób toouse gałąź zapytania toodown przykładowych hello danych, który następnie jest dostępny z hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.

### <a name="down-sampling-hello-data"></a>Próbkowanie danych hello w dół
Istnieją dwa kroki tej procedury. Najpierw dołączyć firma Microsoft hello **nyctaxidb.trip** i **nyctaxidb.fare** tabel w trzech kluczy, które znajdują się we wszystkich rekordach: "Medalionu", "hack\_licencji", i "podnoszenia\_datetime". Następnie możemy wygenerować etykiety klasyfikacji binarnej **Przechylony** i etykiety klasyfikacji wielu klasy **Porada\_klasy**.

toobe toouse stanie hello dół próbki danych bezpośrednio z hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning jest konieczne toostore wyniki hello hello powyżej wewnętrznej tabeli Hive tooan zapytania. W poniżej możemy utworzyć wewnętrznej tabeli Hive i wypełnić zawartością z hello przyłączone i w dół próbki danych.

Witaj zapytania stosuje standardowe funkcje Hive bezpośrednio toogenerate hello godzinę dnia, tygodnia w roku, dzień tygodnia (1 zawiera poniedziałek i 7 zawiera niedziela) z hello "podnoszenia\_datetime" pola i hello bezpośredniego odległość między hello odbiór i dropoff lokalizacje. Użytkownicy mogą odwoływać się za[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) pełną listę funkcji.

Witaj zapytania, a następnie danych hello próbek w dół, aby hello wyniki zapytania można umieścić w hello Azure Machine Learning Studio. Tylko około 1% hello oryginalnego zestawu danych jest importowany do hello Studio.

Poniżej przedstawiono zawartość hello *próbki\_hive\_przygotowanie\_dla\_aml\_full.hql* pliku, który przygotowuje danych do tworzenia w usłudze Azure Machine Learning model.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

Monituj toorun tego zapytania z katalogu Hive hello:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Teraz mamy wewnętrznej tabeli "nyctaxidb.nyctaxi_downsampled_dataset", który można uzyskać dostęp za pomocą hello [i zaimportuj dane] [ import-data] modułu na podstawie usługi Azure Machine Learning. Ponadto firma Microsoft może używać tego elementu dataset do budowania modeli uczenia maszynowego.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Używaj modułu i zaimportuj dane hello w hello tooaccess uczenie maszynowe Azure w dół próbki danych
Jako wymagania wstępne dotyczące wysyłania zapytań Hive w hello [i zaimportuj dane] [ import-data] moduł usługi Azure Machine Learning, potrzebujemy dostęp do obszaru roboczego uczenia maszynowego Azure tooan i dostęp do poświadczeń toohello hello klaster i jego skojarzone konto magazynu.

Niektóre szczegóły na powitania [i zaimportuj dane] [ import-data] modułu i hello tooinput parametry:

**Identyfikator URI serwera HCatalog**: Jeśli nazwa klastra hello jest abc123, to po prostu: https://abc123.azurehdinsight.net

**Nazwa konta użytkownika Hadoop** : nazwa użytkownika hello wybrany dla klastra hello (**nie** nazwa użytkownika dostępu zdalnego hello)

**Hasło konta ser Hadoop** : hasło hello wybrany dla klastra hello (**nie** hello hasła dostępu zdalnego)

**Lokalizacja danych wyjściowych** : to jest wybierany toobe Azure.

**Nazwa konta magazynu Azure** : Nazwa hello domyślnego konta magazynu skojarzone z klastrem hello.

**Nazwa kontenera Azure** : to jest nazwa kontenera domyślnego hello hello klastra i jest zwykle hello takie same jak nazwa klastra hello. W przypadku klastra o nazwie "abc123" jest po prostu abc123.

> [!IMPORTANT]
> **Tabeli Życzymy tooquery przy użyciu hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning musi być wewnętrznej tabeli.** Porada na określenie, czy tabela T w bazie danych D.db wewnętrznej tabeli ma następującą składnię.
> 
> 

Z hello gałęzi katalogu wierszu polecenia hello problemu:

    hdfs dfs -ls wasb:///D.db/T

Jeśli zostanie wprowadzony hello jest wewnętrzna tabela, jego zawartość musi wskazywać tutaj. Inny sposób toodetermine czy tabeli wewnętrznej tabeli jest hello toouse Eksploratora usługi Storage platformy Azure. Użyj jej nazwa kontenera domyślnego toohello toonavigate hello klastra, a następnie Filtruj według nazwy tabeli hello. Jeśli tabela hello i jego zawartość występuje, to potwierdzenie jest wewnętrznej tabeli.

W tym miejscu jest migawką hello zapytań Hive i hello [i zaimportuj dane] [ import-data] modułu:

![Zapytanie hive dla modułu importowanie danych](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Od naszej próbki danych znajduje się w kontenerze domyślna hello dół, hello wynikowe zapytanie Hive z usługi Azure Machine Learning jest bardzo prosty i jest tylko "Wybierz * z nyctaxidb.nyctaxi\_próbkowane w dół\_danych".

zestaw danych Hello teraz może być używany jako punkt początkowy dla budowania modeli uczenia maszynowego hello.

### <a name="mlmodel"></a>Tworzenie modeli w usłudze Azure Machine Learning
Możemy teraz stanie tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net). dane Hello jest gotowy do nas toouse w rozwiązywaniu problemów prognozowania hello określonych powyżej:

**1. Klasyfikacji binarnej**: toopredict czy poradę został płatnej w podróży.

**Uczeń używane:** Regresja logistyczna Two-class

a. W przypadku tego problemu naszą etykietę docelowego (lub klasy) jest "Przechylony". Nasze oryginalnego zestawu danych próbkowania w dół ma kilka kolumn, które są przecieki docelowych do tego eksperymentu klasyfikacji. W szczególności: Porada\_klasy, porada\_kwota i całkowitej\_ilość ujawniania informacji na temat hello etykiety docelowej, która nie jest dostępny na czas testowania. Firma Microsoft Usuń te kolumny z brany pod uwagę przy użyciu hello [Select Columns in Dataset] [ select-columns] modułu.

migawki Hello poniżej zawiera naszych toopredict eksperymentu czy poradę został płatnej dla danego podróży.

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. W tym eksperymencie naszych dystrybucje etykiety docelowego zostały około 1:1.

migawki Hello poniżej przedstawia dystrybucji hello etykiet klasy Porada hello problemu klasyfikacji binarnej.

![Dystrybucji Porada etykiet — klasa](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

W związku z tym możemy uzyskać AUC 0.987, jak pokazano na poniższej ilustracji hello.

![Wartość AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Wieloklasowej klasyfikacji**: zakres hello toopredict kwot Porada uregulowaniu płatności hello podróży, za pomocą hello wcześniej zdefiniowany klasy.

**Uczeń używane:** Wieloklasowej Regresja logistyczna

a. W przypadku tego problemu jest naszą etykietę docelowego (lub klasy) "Porada\_klasy" może to zająć jednej z pięciu wartości (0,1,2,3,4). Jak w przypadku klasyfikacji binarnej hello mamy kilka kolumn, które są przecieki docelowych do tego eksperymentu. W szczególności: Przechylony, porada\_łączna kwota\_ilość ujawniania informacji na temat hello etykiety docelowej, która nie jest dostępny na czas testowania. Firma Microsoft Usuń te kolumny za pomocą hello [Select Columns in Dataset] [ select-columns] modułu.

Hello migawki poniżej przedstawia naszych toopredict eksperymentu, w których bin Porada jest prawdopodobnie toofall (klasa 0: Porada = $0, 1 — klasa: Porada > $0 i Porada < = $5, klasy 2: Porada > $5 i Porada < = $10 klasy 3: Porada > $10 i Porada < = $20 Klasa 4: Porada > $20)

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Teraz Pokaż się wygląd naszego dystrybucji klasy rzeczywiste testu. Widzimy, że klasa 0 i 1 klasy są powszechnie znane, hello innych klas są rzadko.

![Testowanie dystrybucji — klasa](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. W tym eksperymencie używamy toolook macierzy pomyłek w naszym dokładności przewidywania. Jest to pokazane poniżej.

![Macierz pomyłek](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Należy pamiętać, że naszych dokładności klasy w klasach powszechnie hello jest bardzo dobre, hello modelu, które nie są dobrym zadanie "learning" w klasach rzadkich hello.

**3. Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.

**Uczeń używane:** Boosted drzewa decyzyjnego

a. W przypadku tego problemu jest naszą etykietę docelowego (lub klasy) "Porada\_kwota". Nasze przecieki docelowego w tym przypadku są: Przechylony, porada\_klasy całkowita\_kwota; te zmienne ujawnienie informacji na temat kwota Porada hello jest zazwyczaj niedostępna na czas testowania. Firma Microsoft Usuń te kolumny za pomocą hello [Select Columns in Dataset] [ select-columns] modułu.

belows migawki Hello przedstawiający kwotę hello toopredict eksperymentu naszych hello podane poradę.

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. W przypadku problemów regresji mierzymy hello dokładności przewidywania naszych analizując hello kwadrat błąd prognoz hello, hello współczynnik determinacji i Witaj, takich jak. Zostanie przedstawiony je poniżej.

![Statystyki prognozowania](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Widzimy o hello współczynnik determinacji jest 0.709, podejrzeń około 71% wariancję hello tłumaczy naszych współczynników modelu.

> [!IMPORTANT]
> więcej informacji na temat usługi Azure Machine Learning toolearn i w jaki sposób tooaccess i użyj go, zobacz zbyt[co to jest Machine Learning?](machine-learning-what-is-machine-learning.md). Zasób przydatne do odtwarzania z licznych eksperymenty uczenia maszynowego w usłudze Azure Machine Learning to hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/). Galeria Hello obejmuje gamy eksperymenty i zapewnia kompleksowy wprowadzenia hello zakres możliwości usługi Azure Machine Learning.
> 
> 

## <a name="license-information"></a>Informacje o licencji
Ten przewodnik próbki i jego towarzyszący skrypty są udostępniane przez firmę Microsoft hello MIT licencji. Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.

## <a name="references"></a>Dokumentacja
• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
