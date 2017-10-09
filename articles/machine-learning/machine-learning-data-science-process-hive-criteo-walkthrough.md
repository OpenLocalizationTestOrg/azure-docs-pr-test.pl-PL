---
title: "Hello proces nauki danych zespołu w akcji — na zestaw 1 TB danych przy użyciu klastra usługi Azure HDInsight Hadoop | Dokumentacja firmy Microsoft"
description: "Scenariusz end-to-end wykorzystujących usługi HDInsight Hadoop przy użyciu hello proces nauki danych zespołu toobuild klastra, a następnie wdrożyć model przy użyciu dużych publicznie dostępnych dataset (1 TB)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Hello proces nauki danych zespołu w akcji — na zestaw 1 TB danych przy użyciu klastra usługi Azure HDInsight Hadoop

W tym przewodniku zostaje przedstawiony przy użyciu hello proces nauki danych zespołu w scenariuszu end-to-end z [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj, funkcję odtwarzania i w dół przykładowych danych z jednego z hello publicznie dostępne [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawów danych. Używamy toobuild usługi Azure Machine Learning model klasyfikacji binarnej na tych danych. Zostanie przedstawiony, jak toopublish te modele jako usługi sieci Web.

Możliwe jest również możliwe toouse IPython notesu tooaccomplish hello zadania przedstawione w tym przewodniku. Użytkownicy, którzy będą jak tootry takie podejście powinni skontaktować hello [wskazówki Criteo za pomocą połączenia ODBC programu Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tematu.

## <a name="dataset"></a>Opis elementu Criteo Dataset
Hello Criteo dane są około 370 GB plików TSV gzip skompresowane (~1.3TB nieskompresowane), zestawu danych prognozowania kliknij składającej się z ponad miliard 4.3 rekordów. Jest ona pobierana z 24 dni kliknij danych udostępnionych przez [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Dla wygody hello analityków danych Firma Microsoft ma rozpakowane dostępne tooexperiment toous danych z.

Każdy rekord w tym elemencie dataset zawiera kolumny 40:

* Pierwsza kolumna Hello jest etykieta kolumny, która wskazuje, czy użytkownik kliknie **Dodaj** (wartość 1) lub w ogóle nie kliknij jedną (wartość 0)
* następnie 13 kolumny są numeryczną, i
* ostatni 26 są podzielone na kategorie kolumn

kolumny Hello są anonimowe i szereg wyliczany nazwy: "Col1" (dla kolumny etykiety hello) zbyt "Col40" (dla ostatniej kolumny podzielone na kategorie hello).            

Poniżej przedstawiono fragment hello najpierw 20 kolumn dwóch uwag (wiersze) z tego zestawu danych:

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Istnieją brakujące wartości w kolumnach liczbowych i podzielone na kategorie hello w tym zestawie danych. Przedstawione prostą metodę obsługi hello brakujące wartości. Dodatkowe szczegóły danych hello są zbadane, gdy będziemy przechowywać w tabele programu Hive.

**Definicja:** *szybkość przeglądowego (kont.):* to hello odsetek kliknięć w hello danych. W tym zestawie danych Criteo hello Ewidencyjne to około 3.3% lub 0.033.

## <a name="mltasks"></a>Przykłady prognozowania zadań
Dwa przykładowe prognozowania problemy zostały rozwiązane w tym przewodniku:

1. **Klasyfikacji binarnej**: wskazuje, czy użytkownik kliknął add:
   
   * Klasa 0: Nie kliknij
   * Klasa 1: kliknij przycisk
2. **Regresja**: prognozuje prawdopodobieństwo powitania kliknij ad z funkcji użytkownika.

## <a name="setup"></a>Ustaw się HDInsight klastra usługi Hadoop do analizy danych
**Uwaga:** jest to zazwyczaj **Admin** zadań.

Konfigurowanie środowiska Azure nauki danych do tworzenia rozwiązań analizy predykcyjnej z klastrami usługi HDInsight w trzy kroki:

1. [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md): to konto magazynu jest używana toostore danych w magazynie obiektów Blob Azure. dane Hello używane w klastrach HDInsight są przechowywane w tym miejscu.
2. [Dostosowywanie Hadoop w usłudze Azure Hdinsight do analizy danych](machine-learning-data-science-customize-hadoop-cluster.md): ten krok umożliwia utworzenie klastra usługi Azure HDInsight Hadoop z 64-bitowych Anaconda Python 2.7 zainstalowane we wszystkich węzłach. Istnieją dwa toocomplete ważne czynności (opisanej w tym temacie), w przypadku dostosowywania hello klastra usługi HDInsight.
   
   * Należy połączyć utworzony w kroku 1 z klastrem usługi HDInsight, po utworzeniu konta magazynu hello. To konto magazynu jest używane do uzyskiwania dostępu do danych, które mogą być przetwarzane w ramach klastra hello.
   * Należy włączyć dostęp zdalny toohello węzła głównego klastra powitania po jego utworzeniu. Pamiętaj poświadczenia dostępu zdalnego hello określone w tym miejscu (różne od tych określonych hello klastra podczas jego tworzenia): potrzebne toocomplete hello następujących procedur.
3. [Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md): to Azure Machine Learning obszaru roboczego jest używany do tworzenia modeli uczenia maszyny po Eksploracja danych początkowych i w dół próbkowania w klastrze usługi HDInsight hello.

## <a name="getdata"></a>Pobierz i wykorzystują dane ze źródła publiczny
Witaj [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawu danych jest możliwy przez kliknięcie łącza hello, akceptując hello warunki użytkowania i podanie nazwy. Migawki to wygląda jak jest następujący:

![Zaakceptuj postanowienia Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Kliknij przycisk **tooDownload Kontynuuj** tooread więcej informacji na temat hello zestawu danych i ich dostępność.

Witaj danych znajduje się w publicznej [magazynu obiektów blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) lokalizacji: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Witaj "wasb" odwołuje się tooAzure lokalizacji magazynu obiektów Blob. 

1. Hello danych w tym magazynie obiektów blob publicznego składa się z trzech podfoldery rozpakowane danych.
   
   1. Witaj podfolder *raw/liczby/* zawiera hello pierwszych 21 dni dane — od dnia\_00 tooday\_20
   2. Witaj podfolder *raw/train/* składa się z jednego dnia danych, dzień\_21
   3. Witaj podfolder *pierwotnych i testowanie/* składa się z dwóch dni danych, dzień\_22 i dzień\_23
2. Dla tych, którzy mają toostart hello raw gzip danych, są one również dostępne w folderze głównym hello *raw /* jako day_NN.gz, gdzie NN przechodzi od 00 too23.

Tooaccess o innym podejściu Eksploruj i model te dane, które nie wymaga wszystkie lokalne pliki znajduje się w dalszej części tego przewodnika, gdy utworzymy tabele programu Hive.

## <a name="login"></a>Zaloguj się za toohello headnode klastra
toolog w headnode toohello hello klastra, użyj hello [portalu Azure](https://ms.portal.azure.com) toolocate hello klastra. Kliknij ikonę Słoń HDInsight hello na powitania po lewej, a następnie kliknij dwukrotnie nazwę hello klastra. Przejdź toohello **konfiguracji** , kliknij dwukrotnie ikonę POŁĄCZ hello na powitania u dołu strony hello, a następnie wprowadź swoje poświadczenia dostępu zdalnego, po wyświetleniu monitu. Trwa headnode toohello hello klastra.

Poniżej przedstawiono typowe pierwszego logowania toohello headnode klastra wygląda następująco:

![Zaloguj się za toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Po lewej stronie powitania widzimy hello "Hadoop wiersza polecenia", czyli naszych najważniejszą metodą roboczą dla hello Eksploracja danych. Przedstawiono również dwa przydatne adresy URL - "Hadoop Yarn stanu" i "Hadoop nazwa węzła". adres URL stanu yarn Hello przedstawia postęp zadania i adres URL węzła nazwa hello zwraca szczegółowe informacje dotyczące konfiguracji klastra hello.

Teraz możemy są skonfigurowane i gotowe toobegin pierwszej części przewodnika hello: Eksploracja danych przy użyciu Hive i przygotowanie danych do usługi Azure Machine Learning.

## <a name="hive-db-tables"></a>Utwórz gałąź bazy danych i tabel
tabele toocreate gałęzi dla naszego zestawu danych Criteo hello Otwórz ***wiersza polecenia platformy Hadoop*** na hello pulpitu hello węzła głównego, a następnie wprowadź katalog Hive hello wprowadzając polecenie hello

    cd %hive_home%\bin

> [!NOTE]
> Uruchom wszystkie polecenia gałęzi w tym przewodniku z hello Hive bin / directory wiersza. Odpowiada on za wszelkie problemy ścieżki automatycznie. Używane hello pojęcia "Hive katalogu wiersza", "bin gałęzi / wiersza katalogu" i "wiersza polecenia usługi Hadoop" zamiennie.
> 
> [!NOTE]
> tooexecute każde zapytanie Hive jedną zawsze używaj hello następującego polecenia:
> 
> 

        cd %hive_home%\bin
        hive

Po hello Hive REPL pojawi się z "hive >" Zaloguj się, po prostu wyciąć i wkleić hello zapytania tooexecute go.

Hello następujący kod tworzy bazy danych "criteo", a następnie generuje 4 tabel:

* *tabeli do wygenerowania liczby* oparty na dzień dni\_00 tooday\_20,
* *tabeli do użycia jako hello train dataset* oparty na dzień\_21, i
* dwa *tabel do użycia jako hello testowania zestawów danych* oparty na dzień\_22 i dzień\_23 odpowiednio.

Naszego zestawu danych testowych możemy podzielić na dwóch różnych tabel, ponieważ jeden z dni hello jest dniem wolnym od pracy i chcemy toodetermine modelu hello są wykrywane różnice między dni wolnych i nie święta od szybkości przeglądowego hello.

Witaj skryptu [& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) są wyświetlane tutaj dla wygody:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Firma Microsoft należy zauważyć, że te tabele zewnętrzne jako możemy po prostu lokalizacji magazynu obiektów Blob (wasb) tooAzure punktu.

**Istnieją dwa sposoby tooexecute Hive dowolnego zapytania, które teraz wspomina.**

1. **Przy użyciu hello wiersza polecenia REPL Hive**: hello najpierw jest tooissue polecenia "hive" i skopiuj i Wklej zapytanie na powitania REPL Hive wiersza polecenia. toodo tego, czy:
   
        cd %hive_home%\bin
        hive
   
     Teraz na powitania REPL wiersza polecenia, wycinanie i wklejanie zapytania hello go uruchomi.
2. **Zapisywanie zapytań tooa pliku i wykonywania polecenia hello**: hello jest drugi toosave hello zapytania tooa .hql pliku ([& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)), a następnie problem hello następujące polecenie tooexecute hello zapytania:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Potwierdź utworzenie bazy danych i tabeli
Następnie potwierdzamy hello tworzenie hello bazy danych z hello następujące polecenie z hello Hive bin / directory wiersza:

        hive -e "show databases;"

Dzięki temu:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Tworzenie nowej bazy danych Witaj, "criteo" hello to potwierdzenie.

toosee tabele utworzyliśmy, możemy po prostu wysłać hello polecenie tutaj z hello Hive bin / directory wiersza:

        hive -e "show tables in criteo;"

Następnie widzimy hello następujące dane wyjściowe:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a>Eksploracja danych w gałęzi
Teraz możemy gotowe toodo eksploracji niektóre podstawowe dane w gałęzi. Możemy rozpocząć poprzez zliczanie hello wiele przykładów w pociągu hello i testowanie tabel danych.

### <a name="number-of-train-examples"></a>Liczba train przykłady
Witaj zawartość [& #95 przykładowe; hive &#95; liczba &#95; train &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) są wyświetlane tutaj:

        SELECT COUNT(*) FROM criteo.criteo_train;

Daje to:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

Alternatywnie jedną mogą również wystawiać hello następujące polecenie z hello Hive bin / directory wiersza:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Wiele przykładów testu w hello dwóch testów w zestawach danych
Mamy teraz liczbę hello przykłady w zestawach danych Witaj dwie testu. Witaj zawartość [& #95 przykładowe hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 22 &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) są tutaj:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Daje to:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

W zwykły sposób, może również nazywamy hello skryptu z hello Hive bin / directory monitu wydając polecenie hello:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Na koniec omówione hello wiele przykładów testów w zestawie testów hello danych oparte na dniu\_23.

Witaj toodo polecenia jest podobne toohello, po prostu przedstawionego (odwoływać się za[& #95 przykładowe; hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Dzięki temu:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Dystrybucji etykiety w zestawie danych train hello
Hello dystrybucji etykiety w zestawie danych train hello jest. toosee, to zostanie przedstawiony zawartość [& #95 przykładowe; hive &#95; criteo &#95; & #95 etykiety; #95 & dystrybucji; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Daje to hello etykiety dystrybucji:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Należy pamiętać, że odsetek hello dodatnią etykiety około 3.3% (zgodne z hello oryginalnego zestawu danych).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Dystrybucje Histogram niektóre liczbowe zmiennych w hello uczenia zestawu danych
Możemy użyć natywnego gałęzi "histogram\_liczbowa" funkcji toofind się, jakie dystrybucji hello zmiennych liczbowych hello wygląda następująco. Poniżej przedstawiono zawartość hello [& #95 przykładowe; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Daje to poniższe hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Witaj PENETRACJA widok - rozłożenie kombinacja w gałęzi służy tooproduce wyjściowego przypominającego SQL, zamiast listy zwykle hello. Należy pamiętać, że w hello tej tabeli, pierwsza kolumna hello odpowiada toohello bin Centrum i hello drugi toohello bin częstotliwości.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Przybliżony percentylu niektóre liczbowe zmiennych w hello uczenia zestawu danych
Płynących ze zmiennymi liczbowych jest również hello obliczania przybliżonej percentylu. Gałąź do natywnego "percentyl\_przybliżone" robi to firmie Microsoft. Witaj zawartość [& #95 przykładowe; hive &#95; criteo &#95; przybliżonej &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) są:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Daje to:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Oznacz firma Microsoft hello dystrybucji percentylu zwykle jest blisko związane toohello histogram dystrybucji żadnych liczbowa zmiennej.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Znajdź liczbę unikatowych wartości dla niektórych podzielone na kategorie kolumn w zestawie danych train hello
Kontynuowanie hello Eksploracja danych, teraz znaleźliśmy, dla niektórych kolumn podzielone na kategorie hello liczbę unikatowych wartości, które podejmują. toodo, to zostanie przedstawiony zawartość [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; wartości &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Daje to:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Firma Microsoft Pamiętaj, że Col15 ma unikatowe wartości 19M! Przy użyciu prostego technik, takich jak "hot jeden kodowanie" tooencode takich wymiarów wysokiej zmiennych podzielone na kategorie jest praktyce. W szczególności firma Microsoft wyjaśnić i Wykaż metoda zaawansowanych, niezawodnych, zwana [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) dla wydajne rozwiązania problemu ten problem.

Ta podsekcja możemy zakończyć analizując hello liczbę unikatowych wartości dla niektórych innych kategorii kolumn również. Witaj zawartość [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; & #95 wartości wielu &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) są:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Daje to:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Ponownie widzimy, że z wyjątkiem Col20, wszystkie hello innych kolumn ma wiele unikatowych wartości.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Liczby wystąpień wspólnej par podzielone na kategorie zmiennych w zestawie danych train hello

liczby wystąpień wspólnej Hello par podzielone na kategorie zmiennych jest również przydatne. To można ustalić przy użyciu kodu hello w [& #95 przykładowe; hive &#95; criteo &#95; sparowanego &#95; podzielone na kategorie &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Firma Microsoft odwrócić liczby hello kolejności ich występowania i przyjrzyj się hello top 15 w takim przypadku. Dzięki temu nam:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Dół przykładowych zestawów danych powitania dla usługi Azure Machine Learning
O eksplorowanych hello zestawów danych i sprawdzono, firma Microsoft może jak tego typu eksploracji dla zmiennych (takie jak kombinacje), możemy teraz dół hello próbek danych tak, aby firma Microsoft można tworzyć modele w usłudze Azure Machine Learning. Odwołaj jest problem hello możemy skupić się na: podany zestaw atrybutów przykład (funkcja wartości z Col2 - Col40), możemy przewidzieć Jeśli Col1 jest 0 (nie kliknij) lub 1 (kliknij).

toodown przykładowe naszych pociągu i testowania zestawów danych too1% hello oryginalny rozmiar, możemy użyć funkcji macierzystej RAND() gałęzi. Witaj dalej skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) robi to dla zestawu danych train hello:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Daje to:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Witaj skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) zrobi to za dane testowe dzień\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Daje to:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Na koniec hello skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) zrobi to za dane testowe dzień\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Daje to:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

O tym, możemy gotowe toouse próbkowany naszych dół nauczenia i przetestowania zestawów danych do tworzenia modeli w usłudze Azure Machine Learning.

Brak ważnych finalnych przed są dostarczane na tooAzure Machine Learning, czyli dotyczy hello liczba tabeli. W następnej sekcji podrzędne hello omówiono to szczegółowo.

## <a name="count"></a>Krótkie omówienie hello liczba tabeli
Kilka kategorii zmienne widzieliśmy, mają bardzo duże wymiary. W naszym przewodniku możemy przedstawić zaawansowane techniki, zwanej [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode tych zmiennych w wydajny i niezawodny sposób. Więcej informacji na temat tej metody jest hello łączem.

[!NOTE]
>W tym przewodniku możemy skupić się na przy użyciu compact reprezentacje tooproduce liczba tabel wymiarów wysokiej funkcji podzielone na kategorie. To nie jest hello tylko sposób tooencode podzielone na kategorie funkcje; Aby uzyskać więcej informacji na temat innych metod, można wyewidencjonować zainteresowanych użytkowników [co hot-encoding](http://en.wikipedia.org/wiki/One-hot) i [Tworzenie skrótu funkcji](http://en.wikipedia.org/wiki/Feature_hashing).
>

toobuild liczba tabel w danych o liczbie hello, używamy danych hello hello folderu raw/liczba. W hello modelowania sekcji zostanie przedstawiony użytkowników jak toobuild te liczby tabel podzielone na kategorie funkcji od podstaw lub toouse tabelę liczbę wstępnie skompilowanych dla ich eksploracji. W jaki sposób, gdy firma Microsoft można znaleźć zbyt "wbudowana liczba tabel", możemy oznacza za pomocą hello liczba tabel, które firma Microsoft udostępnia. Szczegółowe instrukcje dotyczące sposobu tooaccess te tabele znajdują się w następnej sekcji hello.

## <a name="aml"></a>Tworzenie modelu przy użyciu usługi Azure Machine Learning
Nasz model budowania procesu w usłudze Azure Machine Learning obejmuje następujące kroki:

1. [Pobierz dane hello z tabele programu Hive w usłudze Azure Machine Learning](#step1)
2. [Tworzenie eksperymentu hello: czyszczenie danych hello i featurize z liczby tabel](#step2)
3. [Kompilacja, pociągu i score hello model](#step3)
4. [Ocena hello modelu](#step4)
5. [Publikowanie hello model jako usługę sieci web](#step5)

Teraz możemy modele gotowe toobuild w studio uczenia maszynowego Azure. Nasze dół próbki danych zostanie zapisany jako tabele programu Hive hello klastra. Używamy hello Azure Machine Learning **i zaimportuj dane** tooread modułu tych danych. Konto magazynu Hello poświadczenia tooaccess hello tego klastra znajdują się w jaki sposób.

### <a name="step1"></a>Krok 1: Pobierz dane z tabel gałęzi do usługi Azure Machine Learning, za pomocą modułu i zaimportuj dane hello i wybrać go do eksperymentu uczenia maszynowego
Najpierw wybrać **+ nowy** -> **EKSPERYMENTU** -> **pusty eksperyment**. Następnie z hello **wyszukiwania** pole na górze hello w lewo, wyszukaj "Import Data". Przeciąganie i upuszczanie hello **i zaimportuj dane** modułu w module hello toohello eksperymentu kanwy (hello środkowej części ekranu hello) toouse dla dostępu do danych.

Jest to jakie hello **i zaimportuj dane** wygląda jak podczas pobierania danych z tabeli Hive hello:

![Importuj dane pobiera dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Dla hello **i zaimportuj dane** modułu, hello wartości parametrów hello, znajdujące się w hello grafiki są tylko przykładem hello sortowania wartości należy muszą tooprovide. Poniżej przedstawiono pewne ogólne wskazówki na konfiguracji toofill hello parametr wyjściowy dla hello **i zaimportuj dane** modułu.

1. Wybierz "Zapytania Hive" **źródła danych**
2. W hello **zapytanie Hive bazy danych** polu Wybierz proste * FROM < Twojej\_bazy danych\_name.your\_tabeli\_nazwy >-jest wystarczająca.
3. **Identyfikator URI serwera Hcatalog**: Jeśli klaster jest "abc", to po prostu: https://abc.azurehdinsight.net
4. **Nazwa konta użytkownika Hadoop**: nazwa użytkownika hello wybrany w momencie hello oddanie hello klastra. (Nie hello nazwa użytkownika dostępu zdalnego!)
5. **Hasło konta użytkownika Hadoop**: hello hasło dla nazwy użytkownika hello wybrany w momencie hello oddanie hello klastra. (Nie hasła dostępu zdalnego Witaj!)
6. **Lokalizacja danych wyjściowych**: wybierz polecenie "Azure"
7. **Nazwa konta magazynu Azure**: hello konta magazynu skojarzone z klastrem hello
8. **Klucz konta magazynu Azure**: klucz hello hello konta magazynu skojarzone z klastrem hello.
9. **Nazwa kontenera Azure**: Jeśli nazwa klastra hello jest "abc", a następnie zazwyczaj jest to po prostu "abc",.

Raz hello **i zaimportuj dane** zakończeniu pobieranie danych (możesz zobaczyć hello zielony znacznik na powitania modułu), Zapisz te dane jako zestawu danych (o nazwie wybranych przez użytkownika). Co to wygląda następująco:

![Importuj dane zapisywanie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Kliknij prawym przyciskiem myszy hello output portu hello **i zaimportuj dane** modułu. Takie działanie spowoduje wyświetlenie **Zapisz jako zestawu danych** opcji i **wizualizacja** opcji. Witaj **wizualizacja** opcji, po kliknięciu wyświetla 100 wierszy danych hello, wraz ze prawym panelu, który jest przydatne w przypadku niektórych podsumowania statystyk. toosave danych, po prostu wybierz **Zapisz jako zestawu danych** i postępuj zgodnie z instrukcjami.

tooselect dataset hello zapisywane do użycia w eksperymencie machine learning zlokalizować hello zestawów danych przy użyciu hello **wyszukiwania** pole pokazano powitania po rysunku. Następnie po prostu typu out hello nazwa nadana hello dataset częściowo tooaccess go i przeciągnij hello zestawu danych na hello główny panel. Upuszczenie go na panelu głównego hello zaznacza go do użycia w machine learning modelowania.

![Zestaw danych Drage na panelu głównego hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> W tym hello train i hello testu w zestawach danych. Należy również pamiętać nazwy bazy danych hello toouse i nazw tabel, których można użyć w tym celu. wartości Hello używanych na rysunku hello są przeznaczone wyłącznie dla ilustracji purposes.* *
> 
> 

### <a name="step2"></a>Krok 2: Tworzenie prostego eksperymentu w usłudze Azure Machine Learning toopredict kliknięć / nie kliknięcia
Nasze eksperymentu uczenia Maszynowego Azure wygląda następująco:

![Machine Learning eksperymentu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Teraz omówione hello najważniejsze składniki z tego eksperymentu. Dla przypomnienia potrzebujemy toodrag naszych zapisane nauczenia i przetestowania zestawy danych na kanwie eksperymentu tooour najpierw.

#### <a name="clean-missing-data"></a>Brak danych
Witaj **Clean Missing Data** modułu jest sugeruje nazwa: go czyści brakujące dane w sposób, który może być określone przez użytkownika. Trwa wyszukiwanie w tym module, widzimy to:

![Wyczyść brakujące dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

W tym miejscu Wybraliśmy tooreplace wszystkie brakujące wartości od 0. Istnieją inne opcje zostaną również, które są wyświetlane Analizując listę rozwijaną hello w hello module.

#### <a name="feature-engineering-on-hello-data"></a>Inżynieria na powitania danych
Może istnieć miliony unikatowe wartości w przypadku niektórych funkcji podzielone na kategorie dużych zestawów danych. Przy użyciu metod prosty przykład hot jeden kodowanie reprezentujący takich funkcji podzielone na kategorie wymiarów wysokiej jest całkowicie będzie niemożliwe. W tym przewodniku zostaje przedstawiony sposób toouse liczba funkcji za pomocą wbudowanych toogenerate modułów uczenia maszynowego Azure compact reprezentacje tych wymiarów wysokiej zmiennych podzielone na kategorie. Witaj wynik końcowy jest mniejszy rozmiar modelu, szkolenia szybsze i metryki wydajności, które są dość porównywalne toousing innych technik.

##### <a name="building-counting-transforms"></a>Kompilowanie zliczania transformacji
Funkcje count toobuild, używamy hello **kompilacji zliczania przekształcenie** moduł, który jest dostępny w usłudze Azure Machine Learning. Moduł Hello wygląda następująco:

![Utworzenie modułu zliczania przekształcenie](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![kompilacji zliczania przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> W hello **liczba kolumn** , możemy wprowadź te kolumny Życzymy tooperform liczby. Zazwyczaj są to (jak wspomniano) wymiarów wysokiej kolumny podzielone na kategorie. Na początku hello wspomniano, tym hello Criteo dataset zawiera kolumny podzielone na kategorie 26: z Col15 tooCol40. W tym miejscu możemy liczba na wszystkich z nich i zapewniają ich indeksów (z 15 too40 oddzielonych przecinkami, jak pokazano).
> 

Moduł hello toouse w hello tryb MapReduce (odpowiedni dla dużych zestawów danych), możemy muszą uzyskać dostęp do klastra usługi HDInsight Hadoop tooan (powitalne używane jako eksploracji funkcji mogą być ponownie używane w tym celu również) i swoje poświadczenia. Witaj poprzedniej ilustracjach jakie hello wypełniane wartości wygląda jak (Zastąp wartości hello ilustracyjną z tymi, które są istotne dla własnego przypadek użycia).

![Parametry modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

W powyższym rysunku hello, zostanie przedstawiony sposób tooenter hello danych wejściowych obiektu blob lokalizacji. Ta lokalizacja zawiera dane hello zastrzeżone do tworzenia tabel liczba.

Po zakończeniu tego modułu hello transformacji dla można zapisać później prawym przyciskiem myszy modułu hello i wybierając hello **Zapisz jako transformacji** opcji:

![Opcję "Zapisz jako transformacji"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

W Nasza architektura eksperymentu pokazanym powyżej hello zestawu danych "ytransform2" odpowiada dokładnie tooa zapisana liczba transformacji. Hello pozostałej części tego eksperymentu, przyjęto założenie, że użyto czytnika hello **kompilacji zliczania przekształcenie** moduł na niektóre liczby toogenerate danych, a następnie może przy użyciu tych funkcji count toogenerate liczby na powitania pociągu i testowania zestawów danych.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Wybieranie co tooinclude funkcje są liczone jako część pociągu hello i przetestować zbiory danych
Po mamy liczbą przekształcenie gotowe hello użytkownika można wybrać tooinclude jakie funkcje ich train i przetestować zestawów danych używających hello **zmodyfikować liczby parametrów tabeli** modułu. Ten moduł zostanie przedstawiony tylko tutaj kompletności, ale w celu uproszczenia nie faktycznie jest używana w naszym doświadczeniu.

![Modyfikowanie tabeli liczba parametrów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

W takim przypadku jak widać, wybraliśmy toouse tylko hello dziennika prawdopodobieństwo i tooignore hello wycofania kolumny. Parametry, takie jak hello odzyskiwanie bin progu, ile tooadd artykule poprzednich przykładach wygładzania, można również ustawić i czy toouse żadnych Laplacian hałasu lub nie. Wszystkie te są zaawansowane funkcje i jest ona toobe zauważyć, że wartości domyślne hello są dobry punkt wyjścia dla użytkowników, którzy są nowy typ toothis generacji funkcji.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Przekształcenia danych przed wygenerowaniem hello liczba funkcji
Teraz możemy skupić się na ważne punktu o Przekształcanie naszych train i przetestuj tooactually wcześniejszych danych generowania funkcji count. Należy pamiętać, że istnieją dwa **wykonanie skryptu języka R** moduły używane przed stosujemy hello liczba transformacji tooour danych.

![Wykonanie skryptu języka R modułów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Poniżej przedstawiono skrypt języka R pierwszy hello:

![Pierwszy skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

W ten skrypt języka R, możemy zmienić nazwę naszych toonames kolumny "Col1" za "Col40". Jest to spowodowane przekształcenia liczba hello oczekuje nazwy w tym formacie.

W hello drugi skrypt języka R, możemy saldo hello dystrybucji między klasami dodatnie i ujemne (klasy 1 i 0 odpowiednio) przez klasę ujemna hello próbkowania. Witaj R skrypt tutaj pokazuje, jak toodo to:

![Drugi skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

W tym prostego skryptu języka R, używamy "pos\_minus\_współczynnik" hello tooset ilość równowagi między hello dodatnią i ujemną klasy hello. Jest to ważne, że toodo, ponieważ zwykle poprawy nierównowaga klasa ma zalety korzystania z klasyfikacji problemów w przypadku dystrybucji klasy hello niesymetryczna (odwołanie w tym przypadku mając klasy dodatnią 3.3% i 96.7% ujemna klasy).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Stosowania przekształcenia liczba hello na naszych danych
Ponadto można użyć hello **Zastosuj przekształcenie** tooapply modułu hello transformacje liczba na naszych pociągu i testowania zestawów danych. Ten moduł zostanie przekształcenia liczba hello zapisany co dane wejściowe i hello uczenia lub testowania zestawów danych, jak hello innych danych wejściowych i zwraca danych za pomocą funkcji count. Przedstawiono tutaj:

![Zastosuj przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Fragment wygląd hello liczba funkcji
Jest istotne toosee, jakie funkcje count hello wyglądać w tym przypadku. W tym miejscu zostanie przedstawiony fragment to:

![Liczba funkcji](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

W tym fragmencie zostanie przedstawiony czy hello kolumn, które możemy zliczane na, możemy uzyskać liczby hello i dziennika prawdopodobieństwo w odpowiednich backoffs tooany dodanie.

Firma Microsoft są teraz gotowe toobuild modelu uczenia maszynowego Azure przy użyciu tych przekształcone zestawów danych. W następnej sekcji hello zostanie przedstawiony sposób można to zrobić.

### <a name="step3"></a>Krok 3: Tworzenie, uczenie i score hello model

#### <a name="choice-of-learner"></a>Wybór uczeń
Najpierw należy toochoose uczeń. Możemy toouse przechodzenia drzewa decyzyjnego dwie klasy boosted jako naszych uczeń. Poniżej przedstawiono hello domyślne opcje dla tego uczeń:

![Parametry Two-Class Boosted drzewa decyzyjnego](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Nasze eksperymentu możemy będzie toochoose hello domyślne wartości. Firma Microsoft należy pamiętać, że ten hello domyślne są zazwyczaj przydatne i podstaw szybkiego tooget dobry sposób na wydajność. Na wydajność można poprawić przez profilach parametrów po wybraniu tooonce, do których masz linii bazowej.

#### <a name="train-hello-model"></a>Train hello model
Szkolenia, możemy po prostu Wywołaj **Train Model** modułu. Witaj dwie tooit dane wejściowe są uczeń Two-Class Boosted drzewa decyzyjnego hello i naszym zestawie danych pociągu. To jest następujący:

![Train Model modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Wynik hello modelu
Gdy mamy uczonego modelu gotowe firma Microsoft tooscore na powitania testowania zestawu danych i tooevaluate jego wydajności. Firma Microsoft to zrobić przy użyciu hello **Score Model** modułu pokazano powitania po rysunku, wraz z **Evaluate Model** modułu:

![Moduł Score Model (Generowanie wyników przez model)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Krok 4: Ocena hello modelu
Wreszcie chcemy tooanalyze modelu wydajności. W przypadku problemów klasyfikacji (binarnego) dwie klasy dobrej miary jest zazwyczaj, hello AUC. toovisualize, możemy Podłączanie hello **Score Model** tooan modułu **Evaluate Model** modułu dla tego. Kliknięcie przycisku **Visualize** na powitania **Evaluate Model** modułu daje grafiki, takie jak hello jednym następującego:

![Ocena modelu BDT modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

W danych binarnych (lub dwie klasy) klasyfikacji problemów, dobrym miara dokładności prognozy jest hello obszaru w krzywej (AUC). W poniżej zostanie przedstawiony naszych wyników przy użyciu tego modelu w naszym zestawu danych testowych. tooget port wyjściowy powitania kliknij prawym przyciskiem myszy ten, hello **Evaluate Model** modułu, a następnie **Visualize**.

![Wizualizuj modułu Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Krok 5: Opublikować hello model jako usługę sieci Web
toopublish możliwości Hello modelu uczenia maszynowego Azure jako usługi sieci web z co najmniej problemów jest przydatna funkcja dokonywania szeroko dostępne. Po zakończeniu tej operacji, każdy użytkownik należy wywołania usługi sieci web toohello za dane wejściowe muszą prognoz dotyczących, czy usługa sieci web hello używa tooreturn modelu hello tych prognoz.

toodo, możemy najpierw zapisać uczonego modelu obiektu Trenowanego modelu. Jest to realizowane przez kliknięcie prawym przyciskiem myszy hello **Train Model** modułu i przy użyciu hello **Zapisz jako Uczonego modelu** opcji.

Następnie potrzebujemy toocreate dane wejściowe i wyjściowe portów dla naszej usługi sieci web:

* port wejściowy przyjmującego hello sam formularz jako dane hello potrzebujemy prognoz dotyczących danych
* port wyjściowy zwraca hello oceniane etykiety i hello skojarzone prawdopodobieństwa.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Wybierz kilka wierszy danych dla portu wejściowego hello
Jest wygodną toouse **Zastosuj przekształcenie SQL** modułu tooselect tylko 10 wierszy tooserve jako hello portu dane wejściowe. Wybierz tylko te wiersze danych dla naszych portu wejściowego przy użyciu zapytania SQL hello pokazano poniżej:

![Port wejściowy danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Usługa sieci Web
Teraz możemy gotowe toorun małych eksperymentu, które mogą być używane toopublish naszej usługi sieci web.

#### <a name="generate-input-data-for-webservice"></a>Generuj dane wejściowe dla usługi sieci Web
Krokiem zeroth ponieważ tabeli liczba hello jest duży, możemy wykonać kilka wierszy danych testowych i generowanie danych wyjściowych z jej z funkcji count. Może to służyć jako formatu danych wejściowych hello naszej usługi sieci Web. To jest następujący:

![Utwórz BDT danych wejściowych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Dla formatu danych wejściowych hello używamy teraz hello dane wyjściowe hello **Featurizer liczba** modułu. Po zakończeniu uruchamiania to eksperymentu, Zapisz dane wyjściowe hello z hello **Featurizer liczba** modułu jako zestawu danych. Ten zestaw danych jest używany dla danych wejściowych hello w hello Usługa sieci Web.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Ocenianie eksperymentu publikowania usługi sieci Web
Najpierw zostanie przedstawiony to wygląda następująco. Struktura niezbędne Hello jest **Score Model** moduł, który akceptuje naszych obiekt uczonego modelu i kilka wierszy danych wejściowych, generowany w poprzednich krokach hello przy użyciu hello **Featurizer liczba** modułu. Używamy tooproject "Wybieranie kolumn w zestawie danych" hello Scored etykiety i hello wynik prawdopodobieństwa.

![Wybieranie kolumn w zestawie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Zwróć uwagę, jak hello **Select Columns in Dataset** modułu może służyć do "filtrowanie" danych z zestawu danych. Zostanie przedstawiony tutaj zawartość hello:

![Filtrowanie z hello Wybieranie kolumn w zestawie danych modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

tooget hello niebieski wejściowa i wyjściowa portów, należy po prostu kliknij **przygotowanie Usługa sieci Web** na powitania prawym dolnym rogu. Również uruchomienie tego eksperymentu pozwoli nam usługi sieci web hello toopublish: kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** ikony w dolnej hello prawej, są wyświetlane tutaj:

![Publikowanie usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Po opublikowaniu usługi webservice hello uzyskujemy przekierowanego tooa strony, która wygląda w ten sposób:

![Pulpit nawigacyjny usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Po lewej stronie powitania przedstawia dwa łącza do usług sieci Web:

* Witaj **żądanie/odpowiedź** usługi (lub rekordy zasobów) jest przeznaczony dla jednego prognoz i będziemy korzystać w tym workshop.
* Witaj **BATCH EXECUTION** usługi (BES) służy do przewidywania partii i wymaga się, że prognoz toomake dane wejściowe, używane hello znajdują się w magazynie obiektów Blob Azure.

Kliknięcie łącza hello **żądanie/odpowiedź** trwa tooa strona, która udostępnia wstępnie puszkach kodu w języku C#, python i R. Ten kod można łatwo dokonywania toohello wywołania usługi sieci Web. Należy zauważyć, że ten klucz interfejsu API na tej stronie powitania musi toobe używany do uwierzytelniania.

Jest wygodne toocopy tego python code za pośrednictwem tooa nowej komórki w notesie IPython hello.

W tym miejscu zostanie przedstawiony segment kodu języka python z hello poprawny klucz interfejsu API.

![Kod języka Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Należy pamiętać, możemy zastąpić hello domyślny klucz interfejsu API z kluczem interfejsu API naszych usług sieci Web. Kliknięcie przycisku **Uruchom** w tej komórce w IPython notesu daje powitania po odpowiedzi:

![IPython odpowiedzi](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Widzimy, że dla hello dwóch testowych przykłady, które firma Microsoft pytania (w ramach JSON hello hello skrypt w języku python), uzyskujemy wstecz odpowiedzi w postaci hello "Scored Labels Scored Probabilities". Należy pamiętać, że w takim przypadku Wybraliśmy wartości domyślne hello kodu wstępnie zdefiniowanym hello zapewnia (0 dla wszystkich kolumn liczbowych i ciąg hello "value" dla wszystkich kolumn podzielone na kategorie).

Zakończenie nasze wskazówki end-to-end przedstawiający sposób na dużą skalę zestawu danych toohandle przy użyciu usługi Azure Machine Learning. Firma Microsoft wprowadzenie terabajtów danych, utworzyć modelu prognozy i wdrożyć go jako usługę sieci web w chmurze hello.

