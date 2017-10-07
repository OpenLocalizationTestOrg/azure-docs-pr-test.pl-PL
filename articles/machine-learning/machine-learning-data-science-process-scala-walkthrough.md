---
title: "aaaData nauki przy użyciu języka Scala i Spark na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak toouse Scala maszyny nadzorowanego uczenia zadania związane z hello Spark skalowalne MLlib Spark ML pakietów i w klastrze usługi Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Analiza danych przy użyciu języka Scala i platformy Spark na platformie Azure
W tym artykule opisano, jak toouse Scala dla zadania uczenia nadzorowanego maszyny z hello MLlib skalowalne Spark i Spark ML pakietów w klastrze usługi Azure HDInsight Spark. Przeprowadza użytkownika przez hello zadań, które stanowią hello [procesu nauki danych](http://aka.ms/datascienceprocess): wprowadzanie danych i eksploracja, wizualizacji engineering funkcji, modelowania i zużycia modelu. modele Hello w artykule hello zawierają Regresja logistyczna i liniowych, losowe lasów i boosted gradientu drzew (GBTs), ponadto typowe tootwo nadzorowane machine learning zadań:

* Problem regresji: prognozowania hello Porada kwota ($) w podróży taksówki
* Klasyfikacji binarnej: prognozowania porada lub brak porady w podróży taksówki (1/0)

Hello modelowania proces wymaga uczenie i Ewaluacja testowego zestawu danych i metryk odpowiednich dokładności. W tym artykule można dowiedzieć się jak toostore te modele w magazynie obiektów Blob Azure i w jaki sposób tooscore i ocena wydajności predykcyjnej. W tym artykule omówiono także hello bardziej zaawansowanych tematów z jak toooptimize modeli przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper. dane Hello używane jest przykładowe hello 2013 NYC taksówki podróży i taryfy zestawu danych dostępne w witrynie GitHub.

[Scala](http://www.scala-lang.org/), język oparty na maszynie wirtualnej Java hello integruje pojęcia dotyczące języka zorientowane obiektowo i funkcjonalności. Jest skalowalna język, jest dobrze nadają się toodistributed przetwarzania w chmurze hello, która działa w klastrze Spark w usłudze Azure.

[Platforma Spark](http://spark.apache.org/) platforma przetwarzania równoległego open source, która obsługuje w pamięci przetwarza tooboost hello wydajność aplikacji, analizy danych big data. aparat przetwarzania Spark Hello zaprojektowano pod kątem szybkości, łatwości użycia i zaawansowanych możliwości analitycznych. Możliwości rozproszone obliczenia w pamięci platforma Spark stanowić dobry wybór w przypadku algorytmów iteracyjnych używanych w machine learning i obliczeniach na grafach. Witaj [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pakiet zawiera uniform zestaw interfejsów API wysokiego poziomu, rozszerzający danych ramek, które ułatwiają tworzenie i dostrajania praktyczne machine learning potoków. [MLlib](http://spark.apache.org/mllib/) to platforma Spark uczenia maszynowego Skalowalna biblioteka, udostępnia funkcje modelowania toothis środowisku rozproszonym.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) jest hello hostowanymi na platformie Azure open source platformy Spark. Obejmuje również obsługę notesów Jupyter Scala w klastrze Spark hello i można tootransform wykonywania interakcyjnych zapytań Spark SQL, filtrów i wizualizacji danych przechowywanych w magazynie obiektów Blob platformy Azure. Hello Scala wstawki kodu w tym artykule dostarczające rozwiązań hello i Pokaż hello powierzchni odpowiednie dane hello toovisualize uruchomione w systemie klastry Spark hello notesów Jupyter. kroki modelowania Hello w tych tematach masz kod pokazujący sposób tootrain, ocenić, Zapisz i korzystać z każdego typu modelu.

Witaj kroków instalacji i kodu w tym artykule dotyczą Azure HDInsight 3.4 Spark 1.6. Jednak hello kodu, w tym artykule i hello [notesu Jupyter Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) są ogólne i powinny działać na dowolnym klastra Spark. Witaj Konfiguracja klastra i czynności administracyjne mogą być nieco inne niż co to jest wyświetlany w tym artykule, jeśli nie używasz Spark w usłudze HDInsight.

> [!NOTE]
> Dla tematu, który pokazuje, jak toouse Python zamiast Scala toocomplete zadań w procesie nauki danych end-to-end, zobacz [nauki danych przy użyciu platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* Musi mieć subskrypcję platformy Azure. Jeśli użytkownik nie ma jeszcze jeden, [uzyskać Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Należy hello toocomplete klastra dla usługi Azure HDInsight 3.4 Spark w wersji 1.6 zgodnie z procedurami. toocreate klastra, zobacz instrukcje hello w [wprowadzenie: tworzenie Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Ustaw typ klastra hello i wersji na powitania **wybierz typ klastra** menu.

![Konfiguracja typu klastra usługi HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Opis hello NYC taksówki podróży danych oraz instrukcje, jak tooexecute kodu z notesu Jupyter w klastrze Spark hello, zobacz hello odpowiednich części [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Wykonanie kodu języka Scala z notesu Jupyter w klastrze Spark hello
Można uruchomić notesu Jupyter z hello portalu Azure. Znajdź klastra Spark hello na pulpicie nawigacyjnym, a następnie kliknij go tooenter hello strony do zarządzania dla klastra. Następnie kliknij przycisk **pulpitów nawigacyjnych klastrów**, a następnie kliknij przycisk **notesu Jupyter** notesu hello tooopen skojarzony z klastrem Spark hello.

![Pulpit nawigacyjny klastra i notesów Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

Również można uzyskać dostęp notesów Jupyter w https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Zastąp *clustername* o nazwie hello klastra. Potrzebne hasło hello notesów Jupyter hello tooaccess konta administratora.

![Przejdź notesów tooJupyter przy użyciu nazwy klastra hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Wybierz **Scala** toosee katalogu, który ma kilka przykładów opakowaniach jednostkowych notesów tego hello Użyj interfejsu API PySpark. Witaj modelowania eksploracji i punktacja za pomocą notesu Scala.ipynb, który zawiera hello przykłady kodu dla tego zestawu tematy Spark jest dostępna na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Możesz przekazać notesu hello bezpośrednio z usługi GitHub toohello serwera notesu Jupyter w klastrze Spark. Na stronie głównej Jupyter kliknij hello **przekazać** przycisku. W Eksploratorze plików hello, wklej adres URL usługi GitHub (nieprzetworzonej zawartości) hello hello Scala notesu, a następnie kliknij przycisk **Otwórz**. notesu Scala Hello jest dostępna w hello następującego adresu URL:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Instalatora: Konteksty ustawienie wstępne Spark i Hive, poleceń magicznych Spark i biblioteki Spark
### <a name="preset-spark-and-hive-contexts"></a>Konteksty Spark i Hive ustawień wstępnych.
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


Hello Spark jądra, które są dostarczane z notesów Jupyter ma predefiniowanych kontekstach. Przed rozpoczęciem pracy z aplikacją hello, które tworzysz tooexplicitly zestaw hello Spark i Hive kontekstach nie jest konieczne. Witaj predefiniowanych kontekstach są:

* `sc`dla SparkContext
* `sqlContext`dla HiveContext

### <a name="spark-magics"></a>Platforma Spark poleceń magicznych
Witaj jądra Spark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z `%%`. Dwa z tych poleceń są używane w hello następujące przykłady kodu.

* `%%local`Określa lokalnie wykonać kod hello w kolejnych wierszach. Kod Hello musi być prawidłowy kod języka Scala.
* `%%sql -o <variable name>`wykonuje zapytanie Hive względem `sqlContext`. Jeśli hello `-o` parametr jest przekazywany, w hello jest trwały hello wynik zapytania hello `%%local` kontekstu Scala jako ramki danych platformy Spark.

Dla więcej informacji na temat jądra hello notesów Jupyter i ich wstępnie zdefiniowanych "magics" która zostanie wywołana za pomocą `%%` (na przykład `%%local`), zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Importuj biblioteki
Importowanie hello Spark, MLlib i innych bibliotek, które będą potrzebne przy użyciu następującego kodu hello.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Wprowadzanie danych
pierwszym etapem hello proces analizy danych w Hello jest tooingest hello danych, które mają tooanalyze. Przełączeniem hello danych ze źródeł zewnętrznych lub systemów gdzie znajduje się on w środowisku eksploracji i modelowanie danych. W tym artykule należy pozyskiwania danych hello jest przyłączone do 0,1% próbka hello taksówki podróży i taryfy pliku (przechowywane jako plik .tsv). środowisko eksploracji i modelowanie danych Hello jest Spark. Ta sekcja zawiera hello toocomplete kod powitania po sekwencję zadań:

1. Ustawianie ścieżki katalogu dla magazynu danych i modelu.
2. Przeczytaj hello wejściowy zestaw danych (przechowywane jako plik .tsv).
3. Należy zdefiniować schemat danych hello i wyczyść hello.
4. Utwórz ramkę, oczyszczony danych i ją buforują w pamięci.
5. Zarejestruj dane hello jako element SQLContext tabeli tymczasowej.
6. Zapytania tabeli hello i zaimportuj hello wyniki do ramki danych.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Ustawianie ścieżki katalogu dla lokalizacji przechowywania w magazynie obiektów Blob platformy Azure
Platforma Spark można odczytu i zapisu tooAzure magazynu obiektów Blob. Można użyć Spark tooprocess żadnych istniejących danych, a następnie ponownie zapisać wyniki hello w magazynie obiektów Blob.

modele toosave lub plików w magazynie obiektów Blob, należy tooproperly hello ścieżkę. Odwołanie hello domyślny kontener dołączony toohello klastra Spark przy użyciu ścieżki, która rozpoczyna się od `wasb:///`. Odwołania z innych lokalizacji za pomocą `wasb://`.

Hello poniższy przykład kodu określa hello lokalizację hello toobe danych wejściowych do odczytu i hello ścieżki tooBlob magazynu, który jest dołączony toohello klastra Spark którym zostanie zapisany hello modelu.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Importuj dane, tworzyć RDD i zdefiniowanie ramki danych zgodnie z toohello schematu
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 8 sekund.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Zapytania tabeli hello i importowanie wyników w ramce danych
Następnie tabeli hello zapytania taryfy, pasażerów i Porada danych; Filtrowanie danych uszkodzona i odległe mniejsze; i drukowanie kilka wierszy.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Dane wyjściowe:**

| fare_amount | passenger_count | tip_amount | Przechylony |
| --- | --- | --- | --- |
|        13.5 |1.0 |2.9 |1.0 |
|        16.0 |2.0 |3.4 |1.0 |
|        10.5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Eksploracja danych i wizualizacji
Po przełączeniu hello danych do platformy Spark hello następnym krokiem hello procesu nauki danych jest toogain głębsze zrozumienie hello danych za pośrednictwem eksploracji i wizualizacji. W tej sekcji należy zbadać hello taksówki danych za pomocą zapytania SQL. Następnie wyników hello importu do tooplot ramki danych hello docelowych zmiennych i potencjalnego funkcje kontroli visual przy użyciu funkcji automatycznego wizualizacji hello Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Użyj lokalnej i danych magic tooplot SQL
Domyślnie dane wyjściowe hello wszelkie fragmenty kodu, które można uruchomić z notesu Jupyter jest dostępna w kontekście hello hello sesji, która jest utrwalony na powitania węzłów procesu roboczego. Jeśli chcesz toosave węzłów procesu roboczego toohello podróży do każdego obliczeń i hello wszystkie dane potrzebne dla Twojego obliczenia jest dostępny lokalnie na węźle serwera Jupyter hello (który jest węzłem głównym hello), można użyć hello `%%local` Magiczna toorun hello kodu fragment kodu na powitania serwera Jupyter.

* **Magiczna SQL** (`%%sql`). Hello jądra Spark w usłudze HDInsight obsługuje zapytania HiveQL łatwe wbudowanego przed element SQLContext. Witaj (`-o VARIABLE_NAME`) argument będzie się powtarzał hello wyników kwerendy SQL hello jako ramki danych Pandas na powitania serwera Jupyter. Oznacza to, że będzie on dostępny w trybie lokalnym hello.
* `%%local`**magic**. Witaj `%%local` magic działa hello kod lokalnie na serwerze Jupyter hello, czyli hello węzła głównego klastra usługi HDInsight hello. Zazwyczaj `%%local` magic w połączeniu z hello `%%sql` magic z hello `-o` parametru. Witaj `-o` parametru czy zachować dane wyjściowe hello hello zapytania SQL lokalnie, a następnie `%%local` magic spowoduje wywołanie hello dalej zbiór toorun fragment kodu lokalnie przed hello dane wyjściowe zapytań SQL hello jest utrwalonego lokalnie.

### <a name="query-hello-data-by-using-sql"></a>Dane hello zapytania przy użyciu języka SQL
To zapytanie pobiera rund taksówki hello kwota taryfy, liczba osób i wielkość poradę.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

W hello następującego kodu, hello `%%local` magic tworzy ramkę danych lokalnych, sqlResults. Można użyć sqlResults tooplot przy użyciu matplotlib.

> [!TIP]
> Lokalne magic jest używana wiele razy w tym artykule. Jeśli zestaw danych jest duży, proszę przykładowe toocreate ramki danych, który można umieścić w pamięci lokalnej.
> 
> 

### <a name="plot-hello-data"></a>Dane hello
Można przedstawić przy użyciu kodu języka Python, po ramki danych hello w kontekście lokalnego jako Pandas ramki danych.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 jądra Spark Hello automatycznie wizualizuje hello wynik zapytania SQL (HiveQL), po uruchomieniu hello kodu. Można wybrać różne wizualizacje:

* Tabela
* Kołowy
* Kreska
* Obszar
* Pasek

Poniżej przedstawiono dane hello tooplot kodu hello:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Dane wyjściowe:**

![Porada kwota histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Porada kwota kwotę Taryfy](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Tworzenie funkcji i przekształcanie funkcji, a następnie przygotowywanie danych na dane wejściowe do funkcji modelowania
Dla funkcji oparta na drzewie modelowania z Spark ML i MLlib masz tooprepare docelowych i funkcji przy użyciu różnych technik, takich jak binning, indeksowania hot jeden kodowania i vectorization. Poniżej przedstawiono hello toofollow procedury w tej sekcji:

1. Utwórz nową funkcję przez **binning** przedziałów czasu godzin w ruchu.
2. Zastosuj **indeksowanie i hot jeden kodowanie** toocategorical funkcji.
3. **Przykładowe i podziału hello zestawu danych** do ułamków szkoleniowych i testów.
4. **Określ zmienną szkolenia i funkcje**, następnie tworzenie indeksowanych lub hot jeden zakodowane uczenie i testowanie wejściowego punktu etykietą odporność rozproszonych zestawów danych (RDDs) lub ramek danych.
5. Automatycznie **klasyfikowanie i vectorize funkcje i obiekty docelowe** toouse jako dane wejściowe dla modeli uczenia maszyny.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu
Ten kod pokazuje, jak pakiety ramach Agreement toocreate nowa funkcja przez binning godziny do ruchu czasu i sposób toocache hello wynikowe ramki danych w pamięci. W przypadku, gdy ramki RDDs i dane są używane wielokrotnie, buforowanie prowadzi tooimproved czasu wykonywania. W związku z tym będzie buforować ramki RDDs i danych w kilku etapach hello zgodnie z procedurami.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indeksowanie i hot jeden kodowanie funkcji podzielone na kategorie
Witaj modelowania i prognozowania wymagają funkcji MLlib z toobe podzielone na kategorie danych wejściowych funkcji zakodowany wcześniejsze toouse lub indeksowany. W tej sekcji opisano sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji.

Należy tooindex lub kodowania na różne sposoby, w zależności od modelu hello modeli. Na przykład Regresja logistyczna i liniowej modele wymagają dynamicznego jednego kodowania. Na przykład funkcja z trzech kategorii można rozszerzyć do trzech kolumn funkcji. Każda kolumna może zawierać 0 lub 1 w zależności od kategorii hello obserwacji. MLlib zapewnia hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcja dynamicznego jednego kodowania. Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość. Ten typ kodowania, algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna może być zastosowane toocategorical funkcji.

W tym miejscu możesz przekształcić przykłady tooshow tylko cztery zmienne, które są ciągami znaków. Można również indeksu innych zmiennych, takich jak dzień tygodnia, reprezentowany przez wartości liczbowe, jako zmienne podzielone na kategorie.

Indeksowanie, użyj `StringIndexer()`i hot jeden kodowanie, użyj `OneHotEncoder()` funkcji z MLlib. Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 4 sekundy.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Przykładowe i podziału hello zestaw danych do ułamków szkoleniowych i testów
Ten kod tworzy losowej próbki hello danych (w tym przykładzie 25%). Próbkowanie nie jest wymagany w tym przykładzie powodu toohello rozmiaru zestawu danych hello, hello artykule opisano, jak można przykładowe, aby wiedzieć, jak toouse go do własnych problemów, gdy jest wymagane. W przypadku dużych przykłady to zapisanie długiego czasu podczas uczenia modeli. Następnie podzielone próbki hello części szkolenia (75%, w tym przykładzie) i testowania część (25%, w tym przykładzie) toouse w klasyfikacji i regresji modelowania.

Dodaj liczbę losową (między 0 a 1) tooeach wiersza (w kolumnie "rand") może być złożeń krzyżowego sprawdzania poprawności tooselect używane podczas uczenia.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 2 sekundy.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Określ zmienną szkolenia i funkcje, a następnie utwórz indeksowanych lub hot jeden kodowane celów szkoleniowych i testów danych wejściowych z etykietą punktu RDDs lub danych ramki
Ta sekcja zawiera kod, który pokazuje, jak dane tekstowe podzielone na kategorie tooindex jako etykietą punktu danych typu i kodować je, aby można było ich użyć Regresja logistyczna MLlib tootrain i testowania i inne modele klasyfikacji. Obiekty etykietą punktu są RDDs sformatowanych w taki sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów w MLlib uczenia maszynowego. A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.

W tym kodzie określ (zależnych) Zmienna docelowa hello i hello funkcji toouse tootrain modeli. Następnie można utworzyć indeksowanych lub hot jeden kodowane celów szkoleniowych i testów z etykietą punktu RDDs lub danych ramek danych wejściowych.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 4 sekundy.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Automatycznie klasyfikowanie i vectorize toouse funkcje i obiekty docelowe jako dane wejściowe dla modeli uczenia maszyny
Użyj Spark ML toocategorize hello docelowych i funkcje toouse w funkcji modelowania oparta na drzewie. Kod Hello zakończeniu dwa zadania:

* Tworzy binarne docelowy klasyfikacji, przypisując wartość 0 lub 1 tooeach punkt danych pomiędzy 0 a 1 przy użyciu progu wartości 0,5.
* Automatycznie kategoryzuje funkcji. Liczba hello unikatowe wartości liczbowej dla dowolnej funkcji jest mniejsza niż 32, kategoryzowane tej funkcji.

Oto kod hello te dwa zadania.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Model klasyfikacji binarnej: prognozowania, czy należy zwrócić porady
W tej sekcji można tworzyć trzy typy toopredict modele klasyfikacji binarnej Określa, czy należy zwrócić Porada:

* A **modelu Regresja logistyczna** przy użyciu hello Spark ML `LogisticRegression()` — funkcja
* A **model klasyfikacji losowe lasu** przy użyciu hello Spark ML `RandomForestClassifier()` — funkcja
* A **gradientu zwiększania wyniku model klasyfikacji drzewa** przy użyciu hello MLlib `GradientBoostedTrees()` — funkcja

### <a name="create-a-logistic-regression-model"></a>Tworzenie modelu Regresja logistyczna
Następnie utwórz model Regresja logistyczna przy użyciu hello Spark ML `LogisticRegression()` funkcji. Można utworzyć modelu hello kompilowania kodu w serii kroków:

1. **Train hello model** danych za pomocą jednego zestawu parametrów.
2. **Ocena modelu hello** na testowego zestawu danych o metryki.
3. **Zapisz hello model** w magazynie obiektów Blob do użycia w przyszłości.
4. **Wynik hello modelu** względem danych testowych.
5. **Wykreślenia wyniki hello** z odbiornikiem operacyjnego krzywych cechy (ROC).

Oto kod hello tych procedur:

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Ładowanie, wynik i Zapisz wyniki hello.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Dane wyjściowe:**

ROC na danych testowych = 0.9827381497557599

W systemie lokalnym krzywą ROC serwera Pandas danych ramki tooplot hello Python.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


**Dane wyjściowe:**

![Porada lub nie krzywą ROC Porada](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Utwórz model klasyfikacji losowe lasu
Następnie utwórz model klasyfikacji losowe lasu za pomocą hello Spark ML `RandomForestClassifier()` funkcji, a następnie ocenę hello modelu na danych testowych.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Dane wyjściowe:**

ROC na danych testowych = 0.9847103571552683

### <a name="create-a-gbt-classification-model"></a>Utwórz model klasyfikacji GBT
Następnie utwórz model klasyfikacji GBT przy użyciu jego MLlib `GradientBoostedTrees()` funkcji, a następnie ocenę hello modelu na danych testowych.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Dane wyjściowe:**

Obszar pod krzywą ROC: 0.9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Model regresji: przewidywanie kwota Porada
W tej sekcji są tworzone dwa typy kwoty regresji modele toopredict hello Porada:

* A **model regresji liniowej umorzyć** przy użyciu hello Spark ML `LinearRegression()` funkcji. Należy zapisać hello model i ocena hello modelu na danych testowych.
* A **zwiększania gradientu drzewa modelu regresji** przy użyciu hello Spark ML `GBTRegressor()` funkcji.

### <a name="create-a-regularized-linear-regression-model"></a>Tworzenie modelu regresji liniowej umorzyć
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 13 sekund.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Dane wyjściowe:**

R — sqr na danych testowych = 0.5960320470835743

Następnie zapytania hello wyników testu jako ramki danych i użyj toovisualize AutoVizWidget i matplotlib go.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

Kod Hello tworzy ramkę danych lokalnych z wyników kwerendy hello i geograficzne hello danych. Witaj `%%local` magic tworzy ramkę dane lokalne `sqlResults`, która za pomocą tooplot matplotlib.

> [!NOTE]
> Ta magic Spark jest używana wiele razy w tym artykule. W przypadku dużych hello ilość danych, powinny przykładowe toocreate ramki danych, który można umieścić w pamięci lokalnej.
> 
> 

Utwórz powierzchni za pomocą matplotlib języka Python.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Dane wyjściowe:**

![Porada kwota: rzeczywiste a przewidywane](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Tworzenie modelu regresji GBT
Tworzenie modelu regresji GBT przy użyciu hello Spark ML `GBTRegressor()` funkcji, a następnie ocenę hello modelu na danych testowych.

[Boosted gradientu drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego. Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty. Można użyć GBTs regresji i klasyfikacji. One mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i przechwytywać nonlinearities i interakcje funkcji. Możesz również można używać ich w ustawieniu multiklasa klasyfikacji.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Dane wyjściowe:**

Jest test R-sqr: 0.7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Modelowania zaawansowanych narzędzi do optymalizacji
W tej sekcji można za pomocą narzędzi learning maszyny, które deweloperzy często używane na potrzeby optymalizacji modelu. W szczególności za pomocą parametru kominów i krzyżowego sprawdzania poprawności można zoptymalizować machine learning modeli trzy różne sposoby:

* Podział danych hello na zestawy pociągu i sprawdzania poprawności, zoptymalizować hello modelu za pomocą funkcji hyper parametr kominów na zestaw szkoleniowy i ocenę na zestawie sprawdzania poprawności (regresja liniowa)
* Optymalizacja hello modelu przy użyciu krzyżowego sprawdzania poprawności i funkcji hyper parametru profilach za pomocą funkcji CrossValidator Spark ML (klasyfikacji binarnej)
* Optymalizacja hello modelu przy użyciu niestandardowego kodu krzyżowego sprawdzania poprawności i parametr kominów toouse żadnych machine learning zestaw funkcji i parametr (regresja liniowa)

**Krzyżowe sprawdzanie poprawności** to technika, który ocenia, jak model ćwiczenie znanego zestawu danych zostanie generalize funkcje hello toopredict zestawów danych, które go nie przeprowadzono uczenia. Witaj ogólne ideą ta technika jest czy model jest uczony w zestawie danych znanych danych, a następnie hello dokładność jego prognoz jest testowana niezależnego zestawu danych. Najczęstszą implementacją jest toodivide zestawu danych do *k*-złożeń, a następnie uczenia modelu hello w okrężne na wszystkie oprócz jednego hello złożeń.

**Optymalizacja parametru Hyper** problem hello wybrać zestaw funkcji hyper-parametrów Algorytm uczenia, zwykle z celem hello optymalizacji miara wydajności algorytm hello na niezależnego zestawu danych. Funkcji hyper parametr to wartość, która należy określić poza procedury szkolenie modelu hello. Założenia dotyczące wartości parametrów funkcji hyper mogą wpływać na powitania elastyczność i dokładność hello modelu. Drzewa decyzyjne mieć funkcji hyper parametrów, na przykład takich jak hello potrzeby głębokość i liczby pozostawia w drzewie hello. Należy ustawić termin kar błędną klasyfikację maszyny wektorowa obsługa (SVM).

Typowe optymalizacji hyper parametru tooperform sposób jest toouse wyszukiwanie siatki, nazywany również **odchylenia parametru**. W wyszukiwaniu siatki kompleksowe przeszukiwanie odbywa się za pomocą wartości hello określony podzbiór miejsce hyper parametru hello Algorytm uczenia. Krzyżowe sprawdzanie poprawności można podać toosort metryki wydajności, limit optymalne hello utworzone przez algorytm wyszukiwania hello siatki. Jeśli używasz krzyżowe sprawdzanie poprawności parametru hyper kominów może pomóc limit problemów, takich jak overfitting danych tootraining modelu. W ten sposób modelu hello zachowuje hello pojemności tooapply toohello ogólny zestaw danych, z których hello wyodrębniono danych szkoleniowych.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Optymalizacja model regresji liniowej z kominów hyper parametru
Następnie podzielenia danych na zestawy pociągu i sprawdzania poprawności, użyj funkcji hyper parametr profilach szkolenia ustawić toooptimize hello modelu i ocenę na zestawie sprawdzania poprawności (regresja liniowa).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Dane wyjściowe:**

Jest test R-sqr: 0.6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Optymalizacja hello klasyfikacji binarnej modelu przy użyciu kominów krzyżowego sprawdzania poprawności i parametr hyper
W tej sekcji przedstawiono, jak toooptimize klasyfikacji binarnej modelu przy użyciu kominów krzyżowego sprawdzania poprawności i parametr hyper. Ta metoda korzysta hello Spark ML `CrossValidator` funkcji.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Dane wyjściowe:**

Czas toorun hello komórki: 33 sekundy.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Optymalizacja model regresji liniowej hello przy użyciu kodu niestandardowego krzyżowego sprawdzania poprawności i kominów parametru
Następnie zoptymalizować hello modelu przy użyciu niestandardowego kodu i zidentyfikować hello najlepszych parametrów modelu przy użyciu kryterium hello najwyższy dokładności. Następnie utwórz hello ostatecznego modelu, ocena hello modelu na danych testowych i Zapisz hello model w magazynie obiektów Blob. Ponadto ładowanie modelu hello, wynik testu danych i oceny dokładności.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Dane wyjściowe:**

Czas toorun hello komórki: 61 sekund.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Korzystanie z modeli uczenia wbudowane Spark maszyny automatycznie z języka Scala
Omówienie tematów, które umożliwia przeprowadzenie zadań hello, wchodzące w skład procesu nauki danych hello na platformie Azure, zobacz [proces nauki danych zespołu](http://aka.ms/datascienceprocess).

[Wskazówki dotyczące procesu nauki danych Team](data-science-process-walkthroughs.md) opisano inne end-to-end wskazówki, które pokazują hello etapami hello zespołu w procesie nauki danych w określonych scenariuszach. wskazówki dotyczące Hello również ilustrują sposób toocombine w chmurze i lokalnie narzędzia i usługi do toocreate przepływu pracy lub potoku inteligentnego aplikacji.

[Wynik modeli uczenia maszynowego wbudowane Spark](machine-learning-data-science-spark-model-consumption.md) pokazano, jak tooautomatically kodu języka Scala toouse obciążenia i wynik nowe zestawy danych przy użyciu modeli uczenia maszynowego wbudowane Spark i zapisane w magazynie obiektów Blob Azure. Postępuj zgodnie z instrukcjami hello pod warunkiem że i po prostu zastąpić hello kodu Python Scala kodu w tym artykule wykorzystania automatycznych.

