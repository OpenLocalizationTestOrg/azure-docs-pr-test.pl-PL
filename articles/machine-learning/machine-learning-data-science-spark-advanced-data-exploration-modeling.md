---
title: Eksploracja danych aaaAdvanced i modelowania z Spark | Dokumentacja firmy Microsoft
description: "Eksploracja danych toodo Spark w usłudze HDInsight przy użyciu a uczenia binarne modele klasyfikacji i regresji przy użyciu optymalizacji krzyżowego sprawdzania poprawności i hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Zaawansowane eksplorowanie i modelowanie danych za pomocą platformy Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

W tym przewodniku zastosowano Spark w usłudze HDInsight toodo eksploracji i train binarne klasyfikacji danych i modeli regresji przy użyciu krzyżowego sprawdzania poprawności i optymalizacji hyperparameter na próbkę hello NYC taksówki podróży i taryfy 2013 zestawu danych. Przeprowadza użytkownika przez kroki hello hello [proces nauki danych](http://aka.ms/datascienceprocess)end-to-end, przy użyciu HDInsight Spark klastra do przetwarzania i modeli danych i hello hello toostore obiektów blob Azure. proces Hello Eksploruje wizualizuje dane pochodzące z obiektu Blob magazynu Azure i następnie przygotowuje toobuild danych hello modeli predykcyjnych. Python została toocode używane hello rozwiązanie i tooshow hello odpowiednich powierzchni. Te modele są kompilowane przy użyciu klasyfikacji binarnej toolkit toodo hello Spark MLlib i regresji modelowania zadania. 

* Witaj **klasyfikacji binarnej** zadanie jest toopredict czy poradę otrzymuje za hello podróży. 
* Witaj **regresji** toopredict hello ilość Porada hello na podstawie innych funkcji Porada jest zadanie. 

kroki modelowania Hello również zawierać kod, przedstawiający sposób tootrain, oceny i zapisać każdego typu modelu. Witaj omówiono także niektóre hello sam tła jako hello [Eksploracja danych i modelowanie z Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tematu. Ale jego jest bardziej "Zaawansowane" w tym również używa krzyżowego sprawdzania poprawności z hyperparameter profilach tootrain optymalnie dokładne modele klasyfikacji i regresji. 

**Krzyżowe sprawdzanie poprawności (CV)** to technika, który ocenia, jak model ćwiczenie znanego zestawu danych stanowi uogólnienie funkcje hello toopredicting zestawów danych, na którym go nie przeprowadzono uczenia.  Najczęstszą implementacją używane w tym miejscu jest toodivide zestawu danych do złożeń K i następnie uczenia modelu hello w okrężne na wszystkie oprócz jednego hello złożeń. ocenia się możliwość Hello hello modelu tooprediction dokładnie, gdy testowana hello niezależne zestawu danych, w tym modelu hello tootrain składanie nie są używane.

**Optymalizacja Hyperparameter** problem hello wybrać zestaw hyperparameters dla Algorytm uczenia, zwykle z celem hello optymalizacji miara wydajności algorytm hello na niezależnego zestawu danych. **Hyperparameters** to wartości, które należy określić poza procedury szkolenie modelu hello. Założenia dotyczące tych wartości może wpłynąć na powitania elastyczność i dokładność hello modeli. Drzewa decyzyjne ma hyperparameters, na przykład, takie jak hello potrzeby głębokość i liczby pozostawia hello drzewa. Obsługa wektor maszyny (SVMs) wymagają, aby ustawienie terminu kar błędną klasyfikację. 

Typowe sposób tooperform hyperparameter optymalizacją używane w tym miejscu jest wyszukiwanie siatki, lub **odchylenia parametru**. Składa się z wykonuje kompleksowe przeszukiwanie za pomocą wartości hello określony podzbiór hello hyperparameter miejsca dla algorytmu uczenia. Krzyżowego sprawdzania poprawności można podać toosort metryki wydajności, limit optymalne hello utworzone przez algorytm wyszukiwania hello siatki. Używane z szerokimi pomaga limit problemów, takich jak overfitting danych tootraining modelu, dzięki czemu hello modelu zachowuje hello pojemności tooapply toohello ogólny zestaw danych, z których hello dane szkoleniowe został wyodrębniony hyperparameter CV.

modele Hello, używanych zawierają Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzew:

* [Regresji liniowej z SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) model regresji liniowej, który używa metody stochastycznego spadku gradientu (SGD) i dla optymalizacji i funkcja skalowania toopredict hello Porada kwoty płatnej. 
* [Regresja logistyczna z LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) lub regresji "logit" to model regresji, który może być używana podczas hello zależnych od zmiennej jest podzielone na kategorie toodo klasyfikacji danych. LBFGS to algorytm optymalizacji quasi Newton — która przybliża hello algorytmu Broyden — Fletcher — Goldfarb — Shanno (BFGS) przy użyciu ograniczoną ilość pamięci komputera i który jest powszechnie używany w uczeniu maszynowym.
* [Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.  Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting. Losowe lasach są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie i można ją rozszerzyć toohello wieloklasowej klasyfikacji ustawienie. Nie wymagają funkcji skalowania i czy można toocapture nieliniowość i interakcje funkcji. Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.
* [Gradient boosted drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego. Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty. GBTs są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji. Ich można również w ustawieniu multiklasa klasyfikacji.

Modelowanie przykłady użycia CV i Hyperparameter przedstawiono odchylenia hello problemu klasyfikacji binarnej. Przykłady prostsze (bez parametru przeszukiwanie) są prezentowane w hello tematem głównym zadań regresji. Jednak w dodatku hello, również są przedstawione Weryfikacja za pomocą elastycznych net regresji liniowej i CV z parametru odchylenia przy użyciu regresji losowe lasu. Witaj **elastyczna net** jest metoda umorzyć regresji dla dopasowanie regresji liniowej modeli liniowo łączy hello P1 i P2 metryk jako kary hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) i [pierścieniem](https://en.wikipedia.org/wiki/Tikhonov_regularization) metody.   

> [!NOTE]
> Toolkit Spark MLlib hello jest zaprojektowana toowork na dużych zestawów danych, przykładowe stosunkowo mały (~ 30 Mb przy użyciu 170K wierszy, około 0,1% hello oryginalnego NYC zestawu danych) jest używany tutaj dla wygody. Ćwiczenie Hello podane tutaj działa wydajnie (w około 10 minut) w klastrze usługi HDInsight z 2 węzłów procesu roboczego. Witaj tego samego kodu, z drobne zmiany, może być używane tooprocess większych-zestawów danych z odpowiednie modyfikacje dla buforowania danych w pamięci i zmianę rozmiaru klastra hello.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Instalatora: Klastry Spark i notebooki
Kroki instalacji i kodu są dostępne w tym przewodniku dla przy użyciu wersji 1.6 HDInsight Spark. Ale notesów Jupyter znajdują się w przypadku klastrów HDInsight Spark 1.6 jak Spark 2.0. Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je. Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark. Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu. Dla wygody Oto notesów Jupyter toohello łącza hello Spark 1.6 i 2.0 toobe Uruchom jądra pyspark hello z hello notesu Jupyter serwera:

### <a name="spark-16-notebooks"></a>Notesów Spark w wersji 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): zawiera tematy w notesie #1 i tworzenia modelu przy użyciu hyperparameter dostrajanie i krzyżowego sprawdzania poprawności.

### <a name="spark-20-notebooks"></a>Notesów Spark 2.0

[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ten plik zawiera informacje dotyczące sposobu tooperform Eksploracja danych, modelowania i oceniania w Spark 2.0 klastrów.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Instalator: lokalizacji przechowywania, biblioteki i hello ustawienia wstępnego Spark kontekstu
Platforma Spark jest możliwe tooAzure tooread i zapisu obiektu Blob magazynu (znanej także jako WASB). Tak żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i hello powoduje WASB przechowywane ponownie.

modele toosave lub pliki w WASB hello ścieżka musi toobe prawidłowo określone. Witaj klastra Spark toohello dołączony kontenera domyślnego można odwoływać się przy użyciu ścieżki rozpoczynającej się od: "wasb: / / /". Odwołuje się inne lokalizacje "wasb: / /".

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB
Hello poniższy przykład kodu określa hello lokalizację hello toobe danych do odczytu i zapisaniu ścieżki hello hello modelu magazynu katalogu toowhich hello modelu danych wyjściowych:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**DANE WYJŚCIOWE**

DateTime.DateTime (2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Importuj biblioteki
Importuj biblioteki niezbędne z hello następującego kodu:

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a>Wstępnie zdefiniowane kontekstu Spark i poleceń magicznych PySpark
Hello jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu. Dlatego nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacją hello, które tworzysz. Konteksty te są dostępne dla Ciebie domyślnie. Konteksty te są:

* sc - platformy Spark 
* Element sqlContext - gałęzi

Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%. Istnieją dwa polecenia, które są używane w tych przykładach kodu.

* **%% lokalnego** Określa, że kod hello w kolejnych wierszy jest toobe wykonywane lokalnie. Kod musi być prawidłowy kod języka Python.
* **%% sql -o <variable name>**  wykonuje zapytanie Hive względem element sqlContext hello. Jeśli parametr -o hello jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako Pandas DataFrame.

Dla więcej informacji na temat jądra hello notesów Jupyter i hello wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Wprowadzanie danych z publicznego obiektu blob:
Witaj pierwszym krokiem w procesie nauki danych hello jest toobe danych hello tooingest przeanalizowane ze źródeł, w którym znajduje się on w środowisku eksploracji i modelowanie danych. To środowisko jest Spark, w tym przewodniku. Ta sekcja zawiera toocomplete kodu hello sekwencję zadań:

* pozyskiwania toobe przykładowych danych hello modelowane
* Przeczytaj hello danych wejściowych (przechowywane jako plik .tsv)
* Format i dane hello czyste
* Tworzenie i buforowania obiektów (RDDs lub ramek danych) w pamięci
* Zarejestruj go w postaci tabeli tymczasowej w kontekście SQL.

Oto kod hello wprowadzanie danych.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 276.62 sekund

## <a name="data-exploration--visualization"></a>Eksploracja danych i wizualizacji
Po wprowadzeniu danych hello w Spark, hello następnego kroku w procesie nauki danych hello jest lepiej zrozumieć toogain hello danych za pośrednictwem eksploracji i wizualizacji. W tej sekcji omówione hello taksówki danych przy użyciu zapytania SQL oraz kreślenia hello docelowych zmiennych i potencjalnego funkcji inspekcji visual. W szczególności firma Microsoft wykreślenia hello częstotliwość liczby osób w podróży taksówki, częstotliwość hello kwot Porada i jak porady różnią się zależnie od ilości płatności i typu.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Histogram częstotliwości liczba osób w próbce hello taksówki rund do wykreślenia
Ten kod i kolejne wstawki Użyj przykładowe hello magic tooquery SQL i tooplot magic lokalne powitania danych.

* **Magiczna SQL (`%%sql`)** hello jądra HDInsight PySpark obsługuje łatwe wbudowanego HiveQL zapytań dotyczących element sqlContext hello. Witaj (-o nazwa_zmiennej) argument będzie się powtarzał hello wyników kwerendy SQL hello jako DataFrame Pandas na powitania serwera Jupyter. Oznacza to, że jest on dostępny w trybie lokalnym hello.
* Witaj  **`%%local` magic** jest używany kod toorun lokalnie na powitania Jupyter serwera, który jest headnode hello hello klastra usługi HDInsight. Zazwyczaj `%%local` magic po hello `%%sql -o` magic jest używane toorun zapytania. parametru -o Hello czy utrwalić danych wyjściowych hello hello lokalnie zapytania SQL. Następnie hello `%%local` magic wyzwalaczy hello następnego zestawu toorun wstawki kodu lokalnie przed hello dane wyjściowe zapytań SQL hello umieszczone lokalnie. Po uruchomieniu kodu hello automatyczna wizualizacja Hello danych wyjściowych.

To zapytanie pobiera rund hello według liczby osób. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Ten kod tworzy lokalne ramki danych z wyników kwerendy hello i geograficzne hello danych. Witaj `%%local` magic tworzy lokalne ramki danych, `sqlResults`, które mogą służyć do kreślenia z matplotlib. 

> [!NOTE]
> Ta magic PySpark jest używana wiele razy w tym przewodniku. W przypadku dużych hello ilość danych, należy przykładowe toocreate danych ramki, który można umieścić w lokalnej pamięci.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Oto hello kodu tooplot hello rund przez pasażerów liczby

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**DANE WYJŚCIOWE**

![Częstotliwość rund według liczby osób](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Można dokonać wyboru spośród kilku różnych typów wizualizacji (tabeli, kołowego, wiersz, obszar lub pasek) przy użyciu hello **typu** przycisków menu w notesie hello. Wykres słupkowy Hello jest wyświetlany w tym miejscu.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Wykreślenia histogram kwot porady i jak kwota Porada jest zależna od ilości taryfy i liczba osób.
Użyj danych toosample zapytania SQL.

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Ta komórka kod używa hello SQL kwerendy toocreate trzy powierzchni hello danych.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**DANE WYJŚCIOWE:** 

![Porada kwota dystrybucji](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Porada kwota przez taryfy kwota](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Funkcja przygotowanie zespołu inżynieryjnego, przekształcania i danych do modelowania
Tej części opisano i przedstawiono hello kod dla procedur używanych tooprepare danych do użycia w ML modelowania. Widoczny jest sposób hello toodo następujące zadania:

* Utwórz nową funkcję podział godzin, w pojemnikach czasu ruchu
* Indeks i na gorącą kodowania funkcji podzielone na kategorie
* Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML
* Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów
* Skalowanie funkcji
* Obiektów w pamięci podręcznej w pamięci

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Utwórz nową funkcję podział czasu ruchu w pojemnikach
Ten kod pokazuje, jak toocreate nowa funkcja podział ruchu razy w bins, a następnie jak toocache hello wynikowe ramki danych w pamięci. Buforowanie prowadzi czas wykonania tooimproved gdzie odporność rozproszonych zestawów danych (RDDs) i ramek danych są używane wielokrotnie. Tak firma Microsoft pamięci podręcznej RDDs i ramek danych w kilku etapach w tym przewodniku.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**DANE WYJŚCIOWE**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Indeks i hot jeden kodowania funkcji podzielone na kategorie
W tej sekcji przedstawiono sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji. Witaj, modelowania i prognozowania funkcje MLlib wymaga, aby z kategorii danych wejściowych funkcji być indeksowane zakodowane toouse wcześniejszych. 

W zależności od modelu hello muszą tooindex lub zakodować je na różne sposoby. Na przykład Logistic i regresji liniowej modele wymagają dynamicznego jeden kodowania, gdzie, na przykład funkcja z trzech kategorii można rozszerzyć do trzy kolumny funkcji, z każdym zawierających 0 lub 1 w zależności od kategorii hello obserwacji. Udostępnia MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcji toodo hot jednego kodowania. Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość. Ten typ kodowania umożliwia algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.

Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 3.14 sekund

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML
Ta sekcja zawiera kod, który pokazuje, jak typ danych tekstowych podzielone na kategorie tooindex jako etykietą punktu danych i jak tooencode go. To przygotowuje toobe używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji. Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) sformatowany w sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów uczenia Maszynowego w MLlib. A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.

Oto hello tooindex kodu i kodowania tekstu funkcje klasyfikacji binarnej.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Oto kod hello tooencode i pod indeksem funkcje podzielone na kategorie tekstu do analizy regresji liniowej.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów
Ten kod tworzy losowej próbki hello danych (25% służy w tym miejscu). Chociaż nie jest wymagana w tym przykładzie powodu toohello rozmiaru zestawu danych hello, przedstawiony sposób można przykładowe dane hello w tym miejscu. Wiesz, jak toouse on własne problemu, jeśli to konieczne. W przypadku dużych przykłady to zapisanie długiego czasu podczas szkolenia modeli. Obok próbki hello możemy podzielić na części szkolenia (w tym miejscu 75%) i testowania toouse część (25% tutaj) w klasyfikacji i regresji modelowania.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 0.31 sekund

### <a name="feature-scaling"></a>Skalowanie funkcji
Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello. Witaj kodu funkcji skalowania używa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello funkcji toounit wariancji. Do użytku w regresji liniowej z stochastycznego gradientu spadku (SGD) są dostarczane przez MLlib. SGD jest popularnych Algorytm uczenia szeroką gamę innych modeli, takie jak umorzyć regresji lub pomocy technicznej wektor maszyny (SVM) uczenia maszynowego.   

> [!TIP]
> Znaleźliśmy skalowanie hello LinearRegressionWithSGD algorytm toobe toofeature poufnych.   
> 
> 

Oto hello kodu tooscale zmienne do użytku z hello umorzyć liniowej SGD algorytmu.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 11.67 sekund

### <a name="cache-objects-in-memory"></a>Obiektów w pamięci podręcznej w pamięci
czas Hello uczenie i testowanie algorytmów uczenia Maszynowego można zmniejszyć przez buforowanie ramki danych wejściowych hello obiekty używane do klasyfikacji i regresji i skalowania funkcji.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE** 

Czas trwania tooexecute nad komórką: 0,13 sekund

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Przewidywanie, czy z modelami klasyfikacji binarnej otrzymuje porady
W tej sekcji przedstawiono sposób użycia trzech modeli dla zadanie klasyfikacji binarnej hello przewidywania czy poradę ma być stosowany w podróży taksówki. modele Hello prezentowane są:

* Regresja logistyczna 
* Losowe lasu
* Gradientu zwiększania wyniku drzewa

Każdy model budowania sekcji kodu jest podzielony na kroki: 

1. **Model uczenia** danych za pomocą jednego zestawu parametrów
2. **Model oceny** na testowego zestawu danych o metryki
3. **Zapisywanie modelu** w obiekcie blob do użytku w przyszłości

Zostanie przedstawiony sposób toodo krzyżowego sprawdzania poprawności (CV) z parametrem profilach na dwa sposoby:

1. Przy użyciu **ogólnego** kodu niestandardowego, który może być zastosowane tooany algorytmu w parametrze MLlib i tooany ustawia w algorytmie. 
2. Przy użyciu hello **pySpark CrossValidator potoku funkcji**. Należy pamiętać, że CrossValidator ma kilka ograniczeń dotyczących Spark 1.5.0: 
   
   * Modele potoku nie może być zapisany/utrwalony do użytku w przyszłości.
   * Nie można używać dla każdego parametru w modelu.
   * Nie można używać dla każdego algorytmu MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Ogólny krzyżowe sprawdzanie poprawności i kominów hyperparameter używane z algorytmem Regresja logistyczna hello klasyfikacji binarnej
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych. Hello model jest uczony za pomocą innej sprawdzania poprawności (CV) i kominów hyperparameter zaimplementowany przy użyciu kodu niestandardowego, który może być zastosowane tooany z hello uczenia algorytmy MLlib.   

> [!NOTE]
> wykonanie Hello niestandardowego kodu CV może potrwać kilka minut.
> 
> 

**Uczenie modelu Regresja logistyczna hello przy użyciu CV i kominów hyperparameter**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Współczynniki: [0.0082065285375,-0.0223675576104,-0.0183812028036, - 3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]

Intercept:-0.0111216486893

Czas trwania tooexecute nad komórką: 14.43 sekund

**Ocena modelu klasyfikacji binarnej hello o standardowych metryki**

Kod Hello w tej sekcji przedstawiono, jak tooevaluate Regresja logistyczna modelu względem danych zestawu testowego, łącznie z wykresu hello krzywą ROC.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Obszarze PR = 0.985336538462

Obszarze ROC = 0.983383274312

Podsumowanie statystyk

Dokładność = 0.984174341679

Odwołaj = 0.984174341679

F1 Wynik = 0.984174341679

Czas trwania tooexecute nad komórką: 2.67 sekund

**Wykreślić krzywą ROC hello.**

Witaj *predictionAndLabelsDF* jest zarejestrowany jako tabelę, *tmp_results*, w hello poprzedniej komórki. *tmp_results* można toodo używane zapytania i wyświetlić wyników do hello sqlResults danych ramki do kreślenia. Oto kod hello.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Oto hello kodu toomake prognoz i hello kreślenia krzywą ROC.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**DANE WYJŚCIOWE**

![Regresja logistyczna krzywą ROC dla metody ogólne](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Utrwalanie modelu w obiekcie blob do użytku w przyszłości**

Hello kodu w tej sekcji pokazano, jak model Regresja logistyczna hello toosave zużycia.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 34.57 sekund

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Funkcja w MLlib CrossValidator potoku z modelu Regresja logistyczna (Regresja elastycznej)
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych. Hello model jest uczony przy użyciu krzyżowego sprawdzania poprawności (CV) i kominów hyperparameter zaimplementowany przy użyciu hello MLlib CrossValidator potoku funkcji dla CV z odchylenia parametru.   

> [!NOTE]
> wykonywanie Hello ten kod MLlib CV może potrwać kilka minut.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 107.98 sekund

**Wykreślić krzywą ROC hello.**

Witaj *predictionAndLabelsDF* jest zarejestrowany jako tabelę, *tmp_results*, w hello poprzedniej komórki. *tmp_results* można toodo używane zapytania i wyświetlić wyników do hello sqlResults danych ramki do kreślenia. Oto kod hello.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Oto krzywą ROC hello hello kodu tooplot.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**DANE WYJŚCIOWE**

![Regresja logistyczna krzywą ROC przy użyciu jego MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Klasyfikacja losowe lasu
Hello kodu w tej sekcji przedstawiono, jak tootrain, oceny i Zapisz regresji losowe lasu, który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Obszarze ROC = 0.985336538462

Czas trwania tooexecute nad komórką: 26.72 sekund

### <a name="gradient-boosting-trees-classification"></a>Gradientu zwiększania wyniku klasyfikacji drzewa.
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE**

Obszarze ROC = 0.985336538462

Czas trwania tooexecute nad komórką: 28.13 sekund

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Przewidywanie kwota Porada z modelami regresji (bez użycia CV)
W tej sekcji przedstawiono sposób użycia trzech modeli dla zadań regresji hello: przewidywanie kwota Porada hello płatnej w podróży taksówki na podstawie innych funkcji porada. modele Hello prezentowane są:

* Umorzyć regresji liniowej
* Losowe lasu
* Gradientu zwiększania wyniku drzewa

Te modele zostały opisane w hello wprowadzenie. Każdy model budowania sekcji kodu jest podzielony na kroki: 

1. **Model uczenia** danych za pomocą jednego zestawu parametrów
2. **Model oceny** na testowego zestawu danych o metryki
3. **Zapisywanie modelu** w obiekcie blob do użytku w przyszłości   

> AZURE Uwaga: Krzyżowego sprawdzania poprawności nie jest używana z modelami trzy regresji hello w tej sekcji, ponieważ została ona wyświetlana szczegółowo hello Regresja logistyczna modeli. Przykład przedstawiający sposób toouse CV elastycznej NET regresji liniowej znajduje się w hello dodatku w tym temacie.
> 
> AZURE Uwaga: W naszym środowisku może istnieć problemy z zbieżności LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu. Skalowanie zmiennych znacznie ułatwia zbieżności. Można także elastycznej net regresji, przedstawiono w temacie toothis dodatku hello, zamiast LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>Regresji liniowej z SGD
Witaj kodu w tej sekcji przedstawiono sposób toouse skalowania tootrain funkcji regresji liniowej używającej stochastycznego spadku gradientu (SGD) dla usługi optymalizacji, oraz sposób tooscore, oceny i Zapisz hello model w usłudze Azure Blob Storage (WASB).

> [!TIP]
> Wiemy z doświadczenia mogą występować problemy z zbieżności hello LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu. Skalowanie zmiennych znacznie ułatwia zbieżności.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE**

Współczynniki: [0.0141707753435,-0.0252930927087,-0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092,-0.00456498588241,-0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632,-0.00289545676449,-0.00791124681938, 0.54396316518,-0.536293513569, 0.0119076553369,-0.0173039244582, 0.0119632796147, 0.00146764882502]

Przechwycić: 0.854507624459

RMSE = 1.23485131376

R sqr = 0.597963951127

Czas trwania tooexecute nad komórką: 38.62 sekund

### <a name="random-forest-regression"></a>Regresja losowe lasu
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model losowe lasu, który prognozuje Porada kwota hello NYC taksówki podróży danych.   

> [!NOTE]
> Krzyżowe sprawdzanie poprawności parametru profilach przy użyciu kodu niestandardowego znajduje się w dodatku hello.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE**

RMSE = 0.931981967875

R sqr = 0.733445485802

Czas trwania tooexecute nad komórką: 25.98 sekund

### <a name="gradient-boosting-trees-regression"></a>Gradientu zwiększania wyniku regresji drzewa.
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który prognozuje Porada kwota hello NYC taksówki podróży danych.

** Nauczanie i Ewaluacja **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

RMSE = 0.928172197114

R sqr = 0.732680354389

Czas trwania tooexecute nad komórką: 20.9 sekund

**Kreślenia**

*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki. Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia. Oto kod hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Oto hello kodu tooplot hello danych przy użyciu hello Jupyter serwera.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Vs przewidzieć — Porada kwoty rzeczywiste](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Dodatek: Regresji dodatkowych zadań z wykorzystaniem krzyżowego sprawdzania poprawności z przeszukiwanie parametru
Ten dodatek zawiera kod, przedstawiający sposób CV toodo przy użyciu elastycznej net regresji liniowej i jak CV toodo z parametrem odchylenia dla lasu losowe regresji przy użyciu kodu niestandardowego.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Krzyżowe sprawdzanie poprawności przy użyciu elastyczna net regresji liniowej
Hello kodu w tej sekcji przedstawiono sposób toodo krzyżowe sprawdzanie poprawności przy użyciu elastyczna net regresji liniowej i jak tooevaluate hello modelu danych testowych.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

Czas trwania tooexecute nad komórką: 161.21 sekund

**Ocena z metryką R SQR**

*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki. Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia. Oto kod hello

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Oto hello kodu toocalculate R sqr.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**DANE WYJŚCIOWE**

R sqr = 0.619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Krzyżowe sprawdzanie poprawności z odchylenia parametr dla lasu losowe regresji przy użyciu kodu niestandardowego
Hello kodu w tej sekcji przedstawiono sposób toodo krzyżowe sprawdzanie poprawności z odchylenia parametr przy użyciu kodu niestandardowego dla lasu losowe regresji i jak tooevaluate hello modelu danych testowych.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE**

RMSE = 0.906972198262

R sqr = 0.740751197012

Czas trwania tooexecute nad komórką: 69.17 sekund

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Czyszczenie obiektów w pamięci i lokalizacjach modelu drukowania
Użyj `unpersist()` toodelete obiektów w pamięci podręcznej.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**DANE WYJŚCIOWE**

PythonRDD [122] w RDD w PythonRDD.scala: 43

** Wydruku toomodel ścieżki plików toobe używane w notesie zużycie hello. ** tooconsume i wynik niezależne — zestaw danych, należy toocopy go i Wklej te nazwy pliku w "Zużycia notesu" hello.

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**DANE WYJŚCIOWE**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Co dalej?
Teraz po utworzeniu modele regresji i klasyfikacji z hello Spark MlLib, wszystko jest gotowe toolearn jak tooscore i oceny tych modeli.

**Model zużycia:** toolearn jak tooscore i ocenić hello klasyfikacji i regresji modeli utworzonych w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).

