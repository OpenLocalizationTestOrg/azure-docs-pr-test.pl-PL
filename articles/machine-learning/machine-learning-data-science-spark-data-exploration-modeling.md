---
title: eksploracja aaaData i modelowania z Spark | Dokumentacja firmy Microsoft
description: Pokazy hello Eksploracja danych i modelowanie toolkit Spark MLlib hello na platformie Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Eksplorowanie i modelowanie danych za pomocą platformy Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

W tym przewodniku zastosowano Eksploracja danych toodo Spark w usłudze HDInsight i binarne klasyfikacji i regresji modelowania zadania, na przykład hello NYC taksówki podróży i taryfy 2013 zestawu danych.  Przeprowadza użytkownika przez kroki hello hello [proces nauki danych](http://aka.ms/datascienceprocess)end-to-end, przy użyciu HDInsight Spark klastra do przetwarzania i modeli danych i hello hello toostore obiektów blob Azure. proces Hello Eksploruje wizualizuje dane pochodzące z obiektu Blob magazynu Azure i następnie przygotowuje toobuild danych hello modeli predykcyjnych. Te modele są kompilowane przy użyciu klasyfikacji binarnej toolkit toodo hello Spark MLlib i regresji modelowania zadania.

* Witaj **klasyfikacji binarnej** zadanie jest toopredict czy poradę otrzymuje za hello podróży. 
* Witaj **regresji** toopredict hello ilość Porada hello na podstawie innych funkcji Porada jest zadanie. 

modele Hello, używanych zawierają Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzew:

* [Regresji liniowej z SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) model regresji liniowej, który używa metody stochastycznego spadku gradientu (SGD) i dla optymalizacji i funkcja skalowania toopredict hello Porada kwoty płatnej. 
* [Regresja logistyczna z LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) lub regresji "logit" to model regresji, który może być używana podczas hello zależnych od zmiennej jest podzielone na kategorie toodo klasyfikacji danych. LBFGS to algorytm optymalizacji quasi Newton — która przybliża hello algorytmu Broyden — Fletcher — Goldfarb — Shanno (BFGS) przy użyciu ograniczoną ilość pamięci komputera i który jest powszechnie używany w uczeniu maszynowym.
* [Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.  Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting. Losowe lasach są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie i można ją rozszerzyć toohello wieloklasowej klasyfikacji ustawienie. Nie wymagają funkcji skalowania i czy można toocapture nieliniowość i interakcje funkcji. Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.
* [Gradient boosted drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego. Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty. GBTs są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji. Ich można również w ustawieniu multiklasa klasyfikacji.

kroki modelowania Hello również zawierać kod, przedstawiający sposób tootrain, oceny i zapisać każdego typu modelu. Python została toocode używane hello rozwiązanie i tooshow hello odpowiednich powierzchni.   

> [!NOTE]
> Toolkit Spark MLlib hello jest zaprojektowana toowork na dużych zestawów danych, przykładowe stosunkowo mały (~ 30 Mb przy użyciu 170K wierszy, około 0,1% hello oryginalnego NYC zestawu danych) jest używany tutaj dla wygody. Ćwiczenie Hello podane tutaj działa wydajnie (w około 10 minut) w klastrze usługi HDInsight z 2 węzłów procesu roboczego. Witaj tego samego kodu, z drobne zmiany, może być używane tooprocess większych-zestawów danych z odpowiednie modyfikacje dla buforowania danych w pamięci i zmianę rozmiaru klastra hello.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Potrzebujesz konta platformy Azure i Spark 1.6 (lub Spark 2.0) klastra usługi HDInsight toocomplete tego przewodnika. Zobacz hello [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) instrukcje na temat toosatisfy tych wymagań. Ten temat zawiera również opis hello taksówki 2013 NYC danych używany w tym miejscu i instrukcje dotyczące sposobu tooexecute kodu z notesu Jupyter w klastrze Spark hello. 

## <a name="spark-clusters-and-notebooks"></a>Klastry Spark i notebooki
Kroki instalacji i kodu są dostępne w tym przewodniku dla przy użyciu wersji 1.6 HDInsight Spark. Ale notesów Jupyter znajdują się w przypadku klastrów HDInsight Spark 1.6 jak Spark 2.0. Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je. Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark. Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu. Dla wygody Oto łącza hello notesów Jupyter toohello 1.6 Spark (Uruchom jądra pySpark hello z powitania serwera notesu Jupyter toobe) i 2.0 Spark (Uruchom jądra pySpark3 hello z powitania serwera notesu Jupyter toobe):

### <a name="spark-16-notebooks"></a>Notesów Spark w wersji 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): zawiera informacje na temat Eksploracja danych tooperform, modelowania i oceniania z kilku różnych algorytmów.

### <a name="spark-20-notebooks"></a>Notesów Spark 2.0
zadania regresji i klasyfikacji Hello, które są implementowane przy użyciu klastra Spark 2.0 znajdują się w oddzielnych notesów i notesu klasyfikacji hello korzysta z innego zestawu danych:

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ten plik zawiera informacje dotyczące sposobu tooperform Eksploracja danych, modelowania i oceniania w Spark 2.0 klastrów za pomocą hello taksówki NYC podróży i zestaw danych taryfy opisane [tutaj](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Ten notes może być dobry punkt wyjścia do eksplorowania szybko hello kodu, który firma Microsoft umieściła 2.0 Spark. Dla bardziej szczegółowe notesu analizuje hello taksówki NYC danych, zobacz hello notesu dalej na tej liście. Zobacz uwagi hello końcu tej listy, pozwalające porównać te komputery przenośne. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello taksówki NYC podróży i taryfy zestawu danych opisane [ w tym miejscu](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello dobrze znanego linii lotniczych na czas wyjścia zestaw danych z 2011 i 2012. Dataset linii lotniczych hello firma Microsoft zintegrowane z hello lotnisku pogody danych (np. prędkość wiatru, temperatury, wysokość itp.) przed toomodeling, więc te funkcje pogody można dołączyć do modelu hello.

<!-- -->

> [!NOTE]
> zestaw danych linii lotniczych Hello dodano notesów toohello Spark 2.0 toobetter ilustrują hello użyciem algorytmów klasyfikacji. Zobacz następujące linki do informacji na temat zestawu danych na czas wyjścia linii lotniczych i dataset pogody hello:

>- Dane na czas wyjścia linii lotniczych: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dane pogody lotnisku: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Notesy Spark 2.0 Hello na powitania taksówki NYC i linii lotniczych transmitowane opóźnienie-zestawów danych może potrwać 10 minut lub więcej toorun (w zależności od wielkości hello klastra HDI). Witaj pierwszego notesu w hello powyżej listy zawiera wiele aspektów hello Eksploracja danych, wizualizacji i ML modelu szkolenia w notesie pobierającej toorun mniej czasu z próbkowany dół NYC zestaw danych, w których hello taksówkami i taryfy pliki zostały wstępnie przyłączone do: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) tego notesu zajmuje dużo krótszy czas toofinish (2 – 3 min) i może być bardzo punkt początkowy dla szybko Eksploracja kodu hello mamy podany dla Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
Poniższe opisy Hello są powiązane toousing Spark 1.6. W wersjach Spark 2.0 Użyj notesów hello opisane i linki umieszczono powyżej. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Importuj biblioteki
Konfigurowanie wymaga również importowanie wymagane biblioteki. Ustaw kontekst spark i zaimportuj wymagane biblioteki z hello następującego kodu:

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Wprowadzanie danych z obiektu blob publiczny
pierwszym krokiem w procesie nauki hello danych Hello jest toobe danych hello tooingest przeanalizowane ze źródeł gdzie jest znajduje się w środowisku eksploracji i modelowanie danych. środowisko Hello jest Spark, w tym przewodniku. Ta sekcja zawiera toocomplete kodu hello sekwencję zadań:

* pozyskiwania toobe przykładowych danych hello modelowane
* Przeczytaj hello danych wejściowych (przechowywane jako plik .tsv)
* Format i dane hello czyste
* Tworzenie i buforowania obiektów (RDDs lub ramek danych) w pamięci
* Zarejestruj go w postaci tabeli tymczasowej w kontekście SQL.

Oto kod hello wprowadzanie danych.

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 51.72 sekund

## <a name="data-exploration--visualization"></a>Eksploracja danych i wizualizacji
Po wprowadzeniu danych hello w Spark, hello następnego kroku w procesie nauki danych hello jest lepiej zrozumieć toogain hello danych za pośrednictwem eksploracji i wizualizacji. W tej sekcji omówione hello taksówki danych przy użyciu zapytania SQL oraz kreślenia hello docelowych zmiennych i potencjalnego funkcji inspekcji visual. W szczególności firma Microsoft wykreślenia hello częstotliwość liczby osób w podróży taksówki, częstotliwość hello kwot Porada i jak porady różnią się zależnie od ilości płatności i typu.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Histogram częstotliwości liczba osób w próbce hello taksówki rund do wykreślenia
Ten kod i kolejne wstawki Użyj przykładowe hello magic tooquery SQL i tooplot magic lokalne powitania danych.

* **Magiczna SQL (`%%sql`)** hello jądra HDInsight PySpark obsługuje łatwe wbudowanego HiveQL zapytań dotyczących element sqlContext hello. Witaj (-o nazwa_zmiennej) argument będzie się powtarzał hello wyników kwerendy SQL hello jako DataFrame Pandas na powitania serwera Jupyter. Oznacza to, że jest on dostępny w trybie lokalnym hello.
* Witaj  **`%%local` magic** jest używany kod toorun lokalnie na powitania Jupyter serwera, który jest headnode hello hello klastra usługi HDInsight. Zazwyczaj `%%local` magic w połączeniu z hello `%%sql` magic z parametrem -o. parametru -o Hello czy utrwalić danych wyjściowych hello hello zapytania SQL lokalnie, a następnie %% magic lokalnego spowoduje wywołanie hello dalej zbiór toorun fragment kodu lokalnie przed hello dane wyjściowe zapytań SQL hello jest utrwalonego lokalnie

Po uruchomieniu kodu hello automatyczna wizualizacja Hello danych wyjściowych.

To zapytanie pobiera rund hello według liczby osób. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Ten kod tworzy lokalne ramki danych z wyników kwerendy hello i geograficzne hello danych. Witaj `%%local` magic tworzy lokalne ramki danych, `sqlResults`, które mogą służyć do kreślenia z matplotlib. 

> [!NOTE]
> Ta magic PySpark jest używana wiele razy w tym przewodniku. W przypadku dużych hello ilość danych, należy przykładowe toocreate danych ramki, który można umieścić w lokalnej pamięci.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Oto hello kodu tooplot hello rund przez pasażerów liczby

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**DANE WYJŚCIOWE:**

![Częstotliwość podróży według liczby osób](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Można dokonać wyboru spośród kilku różnych typów wizualizacji (tabeli, kołowego, wiersz, obszar lub pasek) przy użyciu hello **typu** przycisków menu w notesie hello. Wykres słupkowy Hello jest wyświetlany w tym miejscu.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Wykreślenia histogram kwot porady i jak kwota Porada jest zależna od ilości taryfy i liczba osób.
Użyj danych toosample zapytania SQL.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**DANE WYJŚCIOWE:** 

![Porada kwota dystrybucji](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Porada kwota kwotę Taryfy](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Funkcja przygotowanie zespołu inżynieryjnego, przekształcania i danych do modelowania
Tej części opisano i przedstawiono hello kod dla procedur używanych tooprepare danych do użycia w ML modelowania. Widoczny jest sposób hello toodo następujące zadania:

* Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu
* Indeks i kodowania funkcji podzielone na kategorie
* Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML
* Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów
* Skalowanie funkcji
* Obiektów w pamięci podręcznej w pamięci

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu
Ten kod przedstawia sposób pakiety ramach Agreement toocreate nowa funkcja przez binning godzin w czasie ruchu, a następnie jak toocache hello wynikowe ramki danych w pamięci. W przypadku, gdy odporność rozproszonych zestawów danych (RDDs) i ramek danych są używane wielokrotnie, buforowanie prowadzi tooimproved czasu wykonywania. W związku z tym możemy pamięci podręcznej RDDs i ramek danych w kilku etapach hello wskazówki. 

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

**DANE WYJŚCIOWE:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Indeks i kodowania podzielone na kategorie funkcje dla danych wejściowych do modelowania funkcji
W tej sekcji przedstawiono sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji. Witaj modelowania i prognozowania wymagają funkcji MLlib z toobe podzielone na kategorie danych wejściowych funkcji zakodowany wcześniejsze toouse lub indeksowany. W zależności od modelu hello muszą tooindex lub zakodować je na różne sposoby:  

* **Oparta na drzewie modelowania** wymaga toobe kategorii zakodowane jako wartości liczbowe (na przykład funkcja z trzech kategorii może być zakodowane za pomocą 0, 1, 2). To są dostarczane przez firmy MLlib [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) funkcji. Ta funkcja koduje kolumny ciąg etykiety tooa kolumny indeksów etykiety, uporządkowanych według częstotliwości etykiety. Mimo że zaindeksowane wartości liczbowe wprowadzania i obsługi danych, algorytmy oparta na drzewie hello może być określony tootreat ich odpowiednio jako kategorie. 
* **Modele logistyczna i regresji liniowej** wymagają dynamicznego jeden kodowania, where, na przykład funkcja z trzech kategorii można rozszerzyć do trzy kolumny funkcji, z każdym zawierających 0 lub 1 w zależności od kategorii hello obserwacji. Udostępnia MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcji toodo hot jednego kodowania. Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość. Ten typ kodowania umożliwia algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.

Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 1,28 sekund

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML
Ta sekcja zawiera kod, wpisz i kodować je, dzięki czemu może być używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji danych tekstowych podzielone na kategorie tooindex jako etykietą punktu danych. Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) sformatowany w sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów uczenia Maszynowego w MLlib. A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.  

Ta sekcja zawiera kod, który pokazuje jak dane tekstowe podzielone na kategorie tooindex jako [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) typ danych i kodować je, dzięki czemu może być używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji. Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) składające się z etykiety (docelowy/odpowiedzi zmienna) i funkcja wektora. Ten format jest potrzebny jako dane wejściowe wiele algorytmów uczenia Maszynowego w MLlib.

Oto hello tooindex kodu i kodowania tekstu funkcje klasyfikacji binarnej.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
Ten kod tworzy losowej próbki hello danych (25% służy w tym miejscu). Chociaż nie jest wymagana w tym przykładzie powodu toohello rozmiaru zestawu danych hello, przedstawiony sposób próbkę można pobrać tutaj, aby wiedzieć, jak toouse dla własnego problem w razie potrzeby. W przypadku dużych przykłady to zapisanie długiego czasu podczas szkolenia modeli. Obok próbki hello możemy podzielić na części szkolenia (w tym miejscu 75%) i testowania toouse część (25% tutaj) w klasyfikacji i regresji modelowania.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 0,24 sekund

### <a name="feature-scaling"></a>Skalowanie funkcji
Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello. Witaj kodu funkcji skalowania używa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello funkcji toounit wariancji. Do użytku w regresji liniowej z stochastycznego gradientu spadku (SGD), popularnych Algorytm uczenia szeroką gamę innych modeli, takie jak umorzyć regresji lub pomocy technicznej wektor maszyny (SVM) uczenia maszynowego są dostarczane przez MLlib.

> [!NOTE]
> Znaleźliśmy skalowanie hello LinearRegressionWithSGD algorytm toobe toofeature poufnych.
> 
> 

Oto hello kodu tooscale zmienne do użytku z hello umorzyć liniowej SGD algorytmu.

    # FEATURE SCALING

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

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 13.17 sekund

### <a name="cache-objects-in-memory"></a>Obiektów w pamięci podręcznej w pamięci
czas powitania dla przez buforowanie obiektów ramki danych wejściowych hello używane do klasyfikacji i regresji, można zmniejszyć uczenie i testowanie algorytmów uczenia Maszynowego i skalowania funkcji.

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

**DANE WYJŚCIOWE:** 

Czas trwania tooexecute nad komórką: 0,15 sekund

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Przewidywanie, czy z modelami klasyfikacji binarnej otrzymuje porady
W tej sekcji przedstawiono sposób użycia trzech modeli dla zadanie klasyfikacji binarnej hello przewidywania czy poradę ma być stosowany w podróży taksówki. modele Hello prezentowane są:

* Regresja logistyczna umorzyć 
* Model lasu losowych
* Gradientu zwiększania wyniku drzewa

Każdy model budowania sekcji kodu jest podzielony na kroki: 

1. **Model uczenia** danych za pomocą jednego zestawu parametrów
2. **Model oceny** na testowego zestawu danych o metryki
3. **Zapisywanie modelu** w obiekcie blob do użytku w przyszłości

### <a name="classification-using-logistic-regression"></a>Regresja logistyczna klasyfikacji
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.

**Uczenie modelu Regresja logistyczna hello przy użyciu CV i kominów hyperparameter**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE:** 

Współczynniki: [0.0082065285375,-0.0223675576104,-0.0183812028036, - 3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]

Intercept:-0.0111216486893

Czas trwania tooexecute nad komórką: 14.43 sekund

**Ocena modelu klasyfikacji binarnej hello o standardowych metryki**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**DANE WYJŚCIOWE:** 

Obszarze PR = 0.985297691373

Obszarze ROC = 0.983714670256

Podsumowanie statystyk

Dokładność = 0.984304060189

Odwołaj = 0.984304060189

F1 Wynik = 0.984304060189

Czas trwania tooexecute nad komórką: 57.61 sekund

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


**DANE WYJŚCIOWE:**

![Regresja logistyczna ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Klasyfikacja losowe lasu
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i zapisać modelu losowe lasu, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**DANE WYJŚCIOWE:**

Obszarze ROC = 0.985297691373

Czas trwania tooexecute nad komórką: 31.09 sekund

### <a name="gradient-boosting-trees-classification"></a>Gradientu zwiększania wyniku klasyfikacji drzewa.
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**DANE WYJŚCIOWE:**

Obszarze ROC = 0.985297691373

Czas trwania tooexecute nad komórką: 19.76 sekund

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Porada kwoty rund taksówki z modelami regresji prognozowania
W tej sekcji przedstawiono sposób użycia trzech modeli dla hello regresji zadanie przewidywania hello ilość Porada hello płatnej w podróży taksówki na podstawie innych funkcji poradę. modele Hello prezentowane są:

* Umorzyć regresji liniowej
* Losowe lasu
* Gradientu zwiększania wyniku drzewa

Te modele zostały opisane w hello wprowadzenie. Każdy model budowania sekcji kodu jest podzielony na kroki: 

1. **Model uczenia** danych za pomocą jednego zestawu parametrów
2. **Model oceny** na testowego zestawu danych o metryki
3. **Zapisywanie modelu** w obiekcie blob do użytku w przyszłości

### <a name="linear-regression-with-sgd"></a>Regresji liniowej z SGD
Witaj kodu w tej sekcji przedstawiono sposób toouse skalowania tootrain funkcji regresji liniowej używającej stochastycznego spadku gradientu (SGD) dla usługi optymalizacji, oraz sposób tooscore, oceny i Zapisz hello model w usłudze Azure Blob Storage (WASB).

> [!TIP]
> Wiemy z doświadczenia mogą występować problemy z zbieżności hello LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu. Skalowanie zmiennych znacznie ułatwia zbieżności. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

Współczynniki: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,-0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]

Przechwycić: 0.853872718283

RMSE = 1.24190115863

R sqr = 0.608017146081

Czas trwania tooexecute nad komórką: 58.42 sekund

### <a name="random-forest-regression"></a>Regresja losowe lasu
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i zapisać regresji losowe lasu, który prognozuje Porada kwota hello NYC taksówki podróży danych.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**DANE WYJŚCIOWE:**

RMSE = 0.891209218139

R sqr = 0.759661334921

Czas trwania tooexecute nad komórką: 49.21 sekund

### <a name="gradient-boosting-trees-regression"></a>Gradientu zwiększania wyniku regresji drzewa.
Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który prognozuje Porada kwota hello NYC taksówki podróży danych.

** Nauczanie i Ewaluacja **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

RMSE = 0.908473148639

R sqr = 0.753835096681

Czas trwania tooexecute nad komórką: 34.52 sekund

**Kreślenia**

*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki. Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia. Oto kod hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Oto hello kodu tooplot hello danych przy użyciu hello Jupyter serwera.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**DANE WYJŚCIOWE:**

![Vs przewidzieć — Porada kwoty rzeczywiste](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Czyszczenie obiektów z pamięci
Użyj `unpersist()` toodelete obiektów w pamięci podręcznej.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Lokalizacje przechowywania rekordu modeli hello konsumenckich i oceniania
tooconsume i wynik niezależne dataset opisane hello [wynik i ocena modeli uczenia maszynowego wbudowane Spark](machine-learning-data-science-spark-model-consumption.md) tematu, należy toocopy i Wklej zawierającego modeli hello zapisane utworzoną tutaj do hello nazw tych plików Zużycie notesu Jupyter. Oto tooprint kodu hello hello ścieżki toomodel plików, który należy.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**DANE WYJŚCIOWE**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>Co dalej?
Teraz po utworzeniu modele regresji i klasyfikacji z hello Spark MlLib, wszystko jest gotowe toolearn jak tooscore i oceny tych modeli. Witaj zaawansowane Eksploracja danych i modelowanie dives notesu głębiej w tym krzyżowego sprawdzania poprawności, parametr funkcji hyper profilach i modelu oceny. 

**Model zużycia:** toolearn jak tooscore i ocenić hello klasyfikacji i regresji modeli utworzonych w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).

**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper

