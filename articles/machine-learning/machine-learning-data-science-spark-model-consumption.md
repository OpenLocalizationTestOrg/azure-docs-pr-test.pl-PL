---
title: modeli uczenia maszynowego wbudowane Spark aaaOperationalize | Dokumentacja firmy Microsoft
description: "Jak tooload i wynik modeli uczenia przechowywane w usłudze Azure Blob Storage (WASB) z języka Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a>Operacjonalizuj modele uczenia wbudowane Spark maszyny
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

W tym temacie przedstawiono sposób toooperationalize modelu uczenia maszynowego zapisane (ML) przy użyciu języka Python w usłudze HDInsight Spark klastrów. Opisuje sposób tooload maszyny modele uczenia, które zostały utworzone przy użyciu Spark MLlib i przechowywane w usłudze Azure Blob Storage (WASB) i w jaki sposób tooscore z zestawów danych, które również były przechowywane w WASB. Zawiera dane wejściowe hello jak toopre proces, za pomocą funkcji przekształcenia hello indeksowania i kodowanie funkcje hello MLlib toolkit oraz jak toocreate etykietą punktu obiekt danych, które mogą być używane jako dane wejściowe dla oceniania z modelami hello ML. modele Hello używany do oceniania obejmują regresji liniowej, Regresja logistyczna losowe modeli lasu i modele drzewa zwiększania gradientu.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Klastry Spark i notesów Jupyter
Kroki instalacji i toooperationalize kodu hello model usługi uczenie Maszynowe znajdują się w tej wskazówki dotyczące korzystania z klastra usługi HDInsight Spark w wersji 1.6, a także klastra Spark 2.0. Kod Hello tych procedur jest również udostępniany w notesach Jupyter.

### <a name="notebook-for-spark-16"></a>Notesu platformy Spark w wersji 1.6
Witaj [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) notesu Jupyter pokazuje, jak toooperationalize zapisany model przy użyciu języka Python w usłudze HDInsight clusters. 

### <a name="notebook-for-spark-20"></a>Notesu platformy Spark 2.0
notesu Jupyter hello toomodify dla toouse Spark w wersji 1.6 z klastrem usługi HDInsight Spark 2.0, Zastąp plik kodu Python hello z [ten plik](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Ten kod przedstawia sposób tworzenia modeli hello tooconsume w Spark 2.0.


## <a name="prerequisites"></a>Wymagania wstępne

1. Potrzebujesz konta platformy Azure i Spark 1.6 (lub Spark 2.0) klastra usługi HDInsight toocomplete tego przewodnika. Zobacz hello [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) instrukcje na temat toosatisfy tych wymagań. Ten temat zawiera również opis hello taksówki 2013 NYC danych używany w tym miejscu i instrukcje dotyczące sposobu tooexecute kodu z notesu Jupyter w klastrze Spark hello. 
2. Należy także utworzyć hello machine learning modele toobe tutaj oceniane przez pracy nad hello [Eksploracja danych i modelowanie z Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tematu dla klastra Spark w wersji 1.6 hello lub komputery przenośne hello Spark 2.0. 
3. notesów Hello Spark 2.0 Użyj dodatkowy zestaw danych w przypadku zadania klasyfikacji hello hello dobrze znanego linii lotniczych na czas wyjścia zestawu danych za pomocą 2011 i 2012. Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je. Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark. Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Instalator: lokalizacji przechowywania, biblioteki i hello ustawienia wstępnego Spark kontekstu
Platforma Spark jest możliwe tooan tooread i zapisu obiektu Blob magazynu Azure (WASB). Tak żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i hello powoduje WASB przechowywane ponownie.

modele toosave lub pliki w WASB hello ścieżka musi toobe prawidłowo określone. Witaj klastra Spark toohello dołączony kontenera domyślnego można odwoływać się przy użyciu ścieżki rozpoczynającej się od: *"wasb / /"*. Hello poniższy przykład kodu określa hello lokalizację hello toobe danych do odczytu i zapisaniu ścieżki hello hello modelu magazynu katalogu toowhich hello modelu danych wyjściowych. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB
Modele są zapisywane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/modele". Jeśli ta ścieżka nie jest poprawnie ustawiona, modele nie są ładowane do oceniania.

Witaj scored wyniki zostały zapisane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/ScoredResults". Jeśli hello toofolder ścieżka jest nieprawidłowa, wyniki nie są zapisywane w tym folderze.   

> [!NOTE]
> lokalizacje ścieżki plików Hello można można kopiować i wklejać do symboli zastępczych hello w ten kod z danych wyjściowych hello hello ostatnią komórkę hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notesu.   
> 
> 

Oto ścieżki katalogu tooset kodu hello: 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

**DANE WYJŚCIOWE:**

DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Importuj biblioteki
Ustaw kontekst spark i zaimportuj wymagane biblioteki z hello następującego kodu

    #IMPORT LIBRARIES
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
Hello jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu. Dlatego nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacją hello, które tworzysz. Są one dostępne dla Ciebie domyślnie. Konteksty te są:

* sc - platformy Spark 
* Element sqlContext - gałęzi

Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%. Istnieją dwa polecenia, które są używane w tych przykładach kodu.

* **%% lokalnego** określono, że kod hello w kolejnych wierszy jest wykonywane lokalnie. Kod musi być prawidłowy kod języka Python.
* **%% sql -o<variable name>** 
* Wykonuje zapytanie Hive względem element sqlContext hello. Jeśli parametr -o hello jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako Pandas dataframe.

Dla więcej informacji na temat jądra hello notesów Jupyter i hello wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Pozyskiwania danych i Utwórz ramkę, oczyszczony danych
Ta sekcja zawiera kod hello szereg zadań wymaganych tooingest hello danych toobe oceniane. Przeczytaj w dołączonym do 0,1% próbka hello taksówki podróży i taryfy pliku (przechowywane jako plik .tsv), dane hello formatu, a następnie tworzy ramkę Wyczyść dane.

pliki podróży i taryfy taksówki Hello zostały dołączone oparte na na powitania procedury zawarte w: [hello proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) tematu.

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
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

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 46.37 sekund

## <a name="prepare-data-for-scoring-in-spark"></a>Przygotowanie danych do oceniania w łączniku Spark
W tej sekcji przedstawiono sposób tooindex, kodowanie i skalować tooprepare podzielone na kategorie funkcji go do użycia w algorytmów uczenia nadzorowanego MLlib dla funkcji klasyfikacji i regresji.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Funkcja transformacji: indeks i kodowania podzielone na kategorie funkcje dla danych wejściowych do modeli wyników.
W tej sekcji przedstawiono sposób tooindex podzielone na kategorie danych przy użyciu `StringIndexer` i funkcji przy użyciu kodowania `OneHotEncoder` hello modeli danych wejściowych.

Witaj [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) koduje kolumny ciąg etykiety tooa kolumny indeksów etykiety. indeksy Hello są uporządkowane według częstotliwości etykiety. 

Witaj [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mapy kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość. Ten typ kodowania umożliwia algorytmy, które oczekują ciągłego ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
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

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 5.37 sekund

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Tworzenie obiektów RDD z tablicami funkcji dla danych wejściowych do modeli
Ta sekcja zawiera kod, który pokazuje jak dane tekstowe podzielone na kategorie tooindex jako RDD obiektu i hot jeden kodować je, dlatego może być używane tootrain i testowania MLlib Regresja logistyczna i modele oparta na drzewie. Witaj indeksowanego dane są przechowywane w [odporność rozproszonych zestawu danych (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) obiektów. Są to podstawowe abstrakcji hello w łączniku Spark. Obiekt RDD reprezentuje niezmienne partycjonowanej kolekcję elementów, które może być obsługiwany przez równolegle z platformy Spark.

Zawiera także kod, który pokazuje, jak hello tooscale danych za pomocą `StandardScalar` podał MLlib do użycia w regresji liniowej z stochastycznego gradientu spadku (SGD), popularnych Algorytm uczenia szeroką gamę machine learning modeli. Witaj [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) jest używane tooscale hello funkcji toounit wariancji. Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello. 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 11.72 sekund

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Wynik z hello logistyczna modelu regresji i Zapisz dane wyjściowe tooblob
Kod Hello w tej sekcji przedstawiono sposób tooload logistyczna Model regresji, który został zapisany na platformie Azure magazynu obiektów blob i używany w podróży taksówki toopredict czy otrzymuje poradę, wynik go z metryki standardowej klasyfikacji, a następnie zapisz i wykreślenia hello tooblob wyników Magazyn. Witaj oceniane wyniki są przechowywane w obiektach RDD. 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 19.22 sekund

## <a name="score-a-linear-regression-model"></a>Score Model regresji liniowej
My używamy [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain model regresji liniowej, za pomocą stochastycznego spadku gradientu (SGD) dla optymalizacji toopredict hello ilość Porada płatnej. 

Hello kodu w tej sekcji przedstawiono sposób wynik, korzystając ze zmiennych skalowana tooload modelu regresji liniowej z magazynu obiektów blob platformy Azure, a następnie zapisz hello wyników wstecz toohello blob.

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 16.63 sekund

## <a name="score-classification-and-regression-random-forest-models"></a>Wynik klasyfikacji i regresji losowe modeli lasu
Hello w tej sekcji przedstawiono sposób tooload hello zapisywania klasyfikacji i regresji losowe modeli lasu zapisane w magazynie obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz hello wyników wstecz tooblob magazynu.

[Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.  Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting. Losowe lasów mogą obsługiwać funkcje podzielone na kategorie, rozszerzanie ustawienie wieloklasowej klasyfikacji toohello, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji. Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.

[Spark.mllib](http://spark.apache.org/mllib/) obsługuje losowe lasów binarnej i wieloklasowej klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe. 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 31.07 sekund

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Wynik klasyfikacji i regresji gradientu zwiększania drzewa modeli
Kod Hello w tej sekcji przedstawia sposób tooload klasyfikacji i regresji gradientu modeli drzewa zwiększanie wyniku z magazynu obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz hello wyników wstecz tooblob magazynu. 

**Spark.mllib** obsługuje GBTs dla binarnego klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe. 

[Gradientu drzew zwiększania](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego. Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty. GBTs mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji. Ich można również w ustawieniu multiklasa klasyfikacji.

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**DANE WYJŚCIOWE:**

Czas trwania tooexecute nad komórką: 14.6 sekund

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Czyszczenie obiektów z pamięci i Drukuj oceniane lokalizacje plików
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


**DANE WYJŚCIOWE:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Korzystanie z modeli Spark przy użyciu interfejsu sieci web
Spark zapewnia mechanizm tooremotely przesyłania zadań lub interakcyjnych zapytań przy użyciu REST interfejsu z składnik o nazwie Livy. Livy jest domyślnie włączone w klastrze Spark w usłudze HDInsight. Aby uzyskać więcej informacji o Livy, zobacz: [Spark przesyłania zadania zdalnie przy użyciu programu Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Możesz użyć programu Livy tooremotely przesłać zadanie wsadowe wyniki pliku, który jest przechowywany w obiekcie blob Azure, a następnie zapisuje hello wyniki tooanother blob. toodo, Przekaż hello skrypt w języku Python z  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) blob toohello hello klastra Spark. Można użyć narzędzia, takiego jak **Eksploratora usługi Microsoft Azure Storage** lub **AzCopy** toocopy hello skryptu toohello klastra blob. W tym przypadku możemy przekazać skryptu hello zbyt***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Witaj klucze dostępu, które można muszą można znaleźć w portalu hello hello konta magazynu skojarzone z klastrem Spark hello. 
> 
> 

Po przekazaniu plików lokalizacji toothis ten skrypt jest uruchamiany w ramach klastra Spark hello w kontekście rozproszonych. Ładuje hello modelu i uruchamia prognoz na na podstawie modelu hello plików wejściowych.  

Ten skrypt można wywoływać zdalnie, definiując prostego żądania HTTPS/REST na Livy.  Oto zdalnie curl polecenia tooconstruct hello HTTP żądania tooinvoke hello skrypt w języku Python. Zamień CLUSTERLOGIN, CLUSTERPASSWORD, NAZWAKLASTRA hello odpowiednie wartości dla klastra Spark.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Można używać dowolnego języka na powitania systemu zdalnego tooinvoke hello Spark zadania przy użyciu programu Livy za prosty wywołania protokołu HTTPS z uwierzytelnianiem podstawowym.   

> [!NOTE]
> Podczas wprowadzania to wywołanie HTTP będzie wygodne toouse hello żądań Python biblioteki, ale nie jest aktualnie zainstalowany domyślny usługi Azure Functions. Dlatego starsze bibliotek HTTP są używane zamiast tego.   
> 
> 

Oto kod języka Python hello wywołania hello HTTP:

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


Można również dodać ten kod języka Python za[usługi Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger przesyłanie zadań Spark, która wyników obiektu blob na podstawie różnych zdarzeń czasomierza, tworzenia lub aktualizacji obiektu blob. 

Środowisko klienta wolnego kodu, należy użyć hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) partii Spark hello tooinvoke oceniania, definiując akcji HTTP na powitania **projektanta aplikacji logiki** oraz ustawienie jego parametrów. 

* Z portalu Azure, Utwórz nową aplikację logiki, wybierając **+ nowy** -> **sieci Web i mobilność** -> **aplikacji logiki**. 
* toobring się hello **projektanta aplikacji logiki**, wprowadź nazwę hello hello aplikacji logiki i Plan usługi App Service.
* Wybierz akcję, HTTP i wprowadź parametry hello pokazano na następującej ilustracji hello:

![Projektant aplikacji logiki](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Co dalej?
**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.

