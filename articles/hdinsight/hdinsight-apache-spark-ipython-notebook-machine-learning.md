---
title: "aaaBuild Apache Spark machine learning aplikacji w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku, w jaki toobuild Apache Spark machine learning aplikacji w usłudze HDInsight Spark klastrów za pomocą notesu Jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Tworzenie aplikacji do uczenia maszynowego Apache Spark w usłudze Azure HDInsight

Dowiedz się, jak toobuild aplikacji learning maszyny Apache Spark przy użyciu Spark klastra w usłudze HDInsight. W tym artykule przedstawiono sposób toouse hello notesu Jupyter dostępne z hello toobuild klastra i przetestować tę aplikację. Aplikacja Hello używa hello przykładowych HVAC.csv danych, które jest dostępne na wszystkich klastrach domyślnie.

**Wymagania wstępne:**

Musi mieć następujące hello:

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Zrozumienie hello zestawu danych
Przed możemy rozpocząć tworzenie aplikacji hello, Daj nam poznać strukturę hello hello danych, dla którego budujemy aplikacji hello i rodzaj hello analizy, która spowoduje wykonanie na powitania danych. 

W tym artykule używamy próbki hello **HVAC.csv** pliku danych, który jest dostępny w hello skojarzony z klastrem usługi HDInsight hello konto magazynu Azure. W ramach konta magazynu hello, plik hello jest na **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Pobierz i otwórz tooget pliku CSV hello migawkę hello danych.  

![Migawki danych używanych na przykład learning maszyny Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "migawki dane używane na potrzeby Spark machine learning przykład")

Hello dane zostaną wyświetlone temperatury docelowy hello i temperatury rzeczywiste hello budynku, który ma zainstalowane systemy HVAC. Załóżmy, że hello **systemu** kolumna reprezentuje identyfikator systemu hello i hello **SystemAge** kolumna reprezentuje hello kilka lat temu hello HVAC system był w miejscu w budynku hello.

Używamy tej toopredict danych czy budynku będą hotter lub colder oparte na temperatury docelowy hello, identyfikator systemowy i wiek systemu.

## <a name="app"></a>Napisać aplikację learning maszyny Spark przy użyciu Spark MLlib
W tej aplikacji używamy tooperform potoku Spark ML klasyfikacji dokumentu. W potoku hello firma Microsoft podzielone dokumentu hello słów, konwertować wyrazy hello wektor funkcji numerycznych i koniec kompilacji modelu prognozowania przy użyciu hello funkcji wektorów i etykiety. Wykonaj następujące kroki toocreate hello aplikacji hello.

1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   
2. W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.
   
   > [!NOTE]
   > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Utwórz nowy notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.
   
    ![Tworzenie notesu Jupyter, na przykład learning maszyny Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "tworzenie notesu Jupyter, na przykład learning maszyny Spark")
4. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.
   
    ![Podaj nazwę notesu Spark machine learning przykład](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Podaj nazwę notesu Spark machine learning przykład")
5. Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello. Możesz zacząć od importowania typów hello, które są wymagane dla tego scenariusza. Witaj następującego fragmentu kodu w pustej komórce Wklej, a następnie naciśnij klawisz **SHIFT + ENTER**. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. Musi teraz ładowanie danych hello (hvac.csv), przeanalizować go i użyć go tootrain hello modelu. W tym celu należy zdefiniować funkcję, która sprawdza, czy hello temperatury rzeczywiste konstruowania hello jest większa niż hello docelowy temperatury. Jeśli rzeczywista temperatury hello jest większa, kompilowanie hello jest gorących, określone przez wartość hello **1.0**. W przypadku mniejszej temperatury rzeczywiste hello budynku hello jest zimnych, określone przez wartość hello **0,0**. 
   
    Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Konfiguruje potok uczenia maszynowego hello Spark, która składa się z trzech etapów: tokenizatora, hashingTF i lr. Aby uzyskać więcej informacji na temat nowości potoku i jak działa zobacz <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning potoku</a>.
   
    Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Dopasuj hello potoku toohello szkolenia dokumentu. Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.
   
        model = pipeline.fit(training)
3. Sprawdź hello szkolenia dokumentu toocheckpoint postęp z aplikacji hello. Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.
   
        training.show()
   
    To powinien zapewnić hello dane wyjściowe podobne toohello poniżej:
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    Przejdź wstecz i sprawdź dane wyjściowe hello na powitania raw pliku CSV. Na przykład hello pierwszego wiersza hello pliku CSV zawiera te dane:

    ![Migawki Spark machine learning przykładowe dane wyjściowe](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "migawki danych wyjściowych na Spark machine learning przykład")

    Zwróć uwagę, jak temperatury rzeczywiste hello jest mniejsza niż temperatury docelowy hello sugerowanie budynku hello jest zimnych. Dlatego w danych wyjściowych szkolenia hello hello wartość **etykiety** w hello jest pierwszy wiersz **0,0**, co oznacza, że kompilowanie hello nie jest dynamicznej.

1. Przygotuj zestawu danych toorun hello uczonego modelu przy użyciu. toodo tak, czy jest przekazywana na identyfikator systemu i wiek systemu (oznaczonego jako **SystemInfo** w danych wyjściowych szkolenia hello), i czy prognozowania modelu hello czy hello kompilowanie z tego systemu wieku systemu i identyfikator może być hotter (wskazywane przez 1.0) lub lodówki () wskazywane przez 0,0).
   
   Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Na koniec tworzenia prognoz na powitania danych testowych. Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Powinny być widoczne następujące dane wyjściowe podobne toohello:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   W pierwszym wierszu hello w hello prognozowania, widać, że systemu HVAC o identyfikatorze 20 i wiek systemu 25 lat budynek hello będzie gorących (**prognozowania = 1.0**). wartość pierwszego Hello DenseVector (0.49999) odpowiada toohello prognozowania 0,0 i hello drugiej wartości (0.5001) odpowiada prognozowania toohello 1.0. W danych wyjściowych hello, mimo że hello druga wartość jest tylko nieznacznie wyższe hello model przedstawia **prognozowania = 1.0**.
4. Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**. To spowoduje zamknięcie i zamknij hello notesu.

## <a name="anaconda"></a>Użyj Anaconda scikit — Dowiedz się biblioteki Spark uczenia maszynowego
Klastry platformy Apache Spark w usłudze HDInsight obejmują bibliotekami Anaconda. Obejmuje to także hello **scikit — Dowiedz się** biblioteki uczenia maszynowego. Biblioteka Hello także różne zestawy danych można toobuild przykładowe aplikacje bezpośrednio z notesu Jupyter. Dla przykłady dotyczące używania hello scikit — Dowiedz się, biblioteka, zobacz [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
