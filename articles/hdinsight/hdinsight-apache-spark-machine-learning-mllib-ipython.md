---
title: "aaaMachine uczenia przykład MLlib Spark w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Spark MLlib toocreate aplikacji learning maszyny, która analizuje zestawu danych za pomocą funkcji klasyfikacji za pośrednictwem Regresja logistyczna."
keywords: "Platforma Spark uczenia maszynowego, spark machine learning przykład"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Użyj toobuild Spark MLlib aplikacji uczenia maszynowego i analizować zestawu danych

Dowiedz się, jak toouse Spark **MLlib** toocreate a machine learning toodo aplikacji proste analizy predykcyjnej na Otwórz zestaw danych. Z maszyny wbudowanych platforma Spark uczenia biblioteki, w tym przykładzie użyto *klasyfikacji* za pośrednictwem Regresja logistyczna. 

> [!TIP]
> W tym przykładzie jest również dostępny jako notesu Jupyter w klastrze Spark (Linux), które są tworzone w usłudze HDInsight. środowisko notesu Hello umożliwia uruchamianie hello Python wstawki z notesu hello, sama. Samouczek hello toofollow z poziomu Notes, Utwórz Spark klastra, a następnie uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). A następnie uruchomić notesu hello **Spark Machine Learning - analizy predykcyjnej na dane inspekcji żywności przy użyciu MLlib.ipynb** w obszarze hello **Python** folderu.
>
>

MLlib jest biblioteki Spark core, która udostępnia wiele narzędzi przydatne dla machine learning zadania, w tym narzędzia, które są odpowiednie dla:

* Klasyfikacja
* Regresja
* Klaster
* Temat modelowania
* Rozkład wartości pojedynczej (SVD) i analizy głównych składników (PCA)
* Hipoteza testowania i obliczania statystyk próbki

## <a name="what-are-classification-and-logistic-regression"></a>Jakie są klasyfikacji i Regresja logistyczna?
*Klasyfikacja*, maszynę popularnych uczenia zadań, proces hello sortowanie danych wejściowych w kategorie. To zadanie hello z toofigure algorytm klasyfikacji, jak tooassign "etykiety" tooinput dane, które należy podać. Na przykład można traktować z algorytmu uczenia maszynowego, który akceptuje podstawowe informacje jako dane wejściowe i bez reszty hello giełdowych na dwie kategorie: zasobów, które powinny sprzedaży i zasobów, które należy przechowywać.

Regresja logistyczna jest algorytm hello, której użyjesz dla klasyfikacji. Regresja logistyczna firmy Spark interfejsu API jest przydatne w przypadku *klasyfikacji binarnej*, lub klasyfikacji danych wejściowych do jednej z dwóch grup. Aby uzyskać więcej informacji na temat logistyczna regresji, zobacz [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

Podsumowując, tworzy proces hello Regresja logistyczna *logistyczna funkcja* które może być używane toopredict hello prawdopodobieństwo, że wektor wejściowy należy w jednej grupie lub hello innych.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Przykład analizy predykcyjnej w danych kontroli żywności
W tym przykładzie używasz Spark tooperform niektóre predykcyjnych analizy danych inspekcji żywności (**Food_Inspections1.csv**) które zostało zakupione w ramach hello [portalu danych Miasto Chicago](https://data.cityofchicago.org/). Ten zestaw danych zawiera informacje o kontroli ustanowienia żywności, które były przeprowadzane w Chicago, wraz z informacjami dotyczącymi każdego zakładu, naruszeń hello znaleziono (jeśli istnieje) i hello wyniki inspekcji hello. plik danych CSV Hello jest już dostępny w hello konta magazynu skojarzone z klastrem hello na **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

W poniższych krokach hello opracowywanie toosee modelu, co jest potrzebne toopass lub Niepowodzenie inspekcji żywności.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Rozpocząć tworzenie aplikacji uczenia maszynowego Spark MMLib
1. Z hello [portalu Azure](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   
1. W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   > [!NOTE]
   > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Utwórz notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

    ![Tworzenie notesu Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Tworzenie nowego notesu Jupyter")
1. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.

    ![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Podaj nazwę notesu hello")
1. Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello są utworzony automatycznie po uruchomieniu pierwszej komórki kodu hello. Można rozpocząć tworzenie komputera nauki aplikacji przez zaimportowanie typów hello wymaganych dla tego scenariusza. toodo tak, umieść kursor hello w komórce hello i naciśnij klawisze **SHIFT + ENTER**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Konstrukcja dataframe wejściowych
Możemy użyć `sqlContext` tooperform przekształcenia danych strukturalnych. pierwszym zadaniem Hello jest tooload hello przykładowych danych ((**Food_Inspections1.csv**)) do programu Spark SQL *dataframe*.

1. Ponieważ dane pierwotne hello jest w formacie CSV, potrzebujemy toouse hello Spark kontekstu toopull każdy wiersz w pliku hello do pamięci jako tekst bez struktury. następnie należy użyć języka Python CSV biblioteki tooparse każdego wiersza pojedynczo.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Mamy teraz hello pliku CSV jako RDD.  Schemat hello toounderstand hello danych, możemy pobrać jeden wiersz z hello RDD.

        inspections.take(1)

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. Witaj Powyższy wynik daje wyobrażenie o hello schemat pliku wejściowego hello. Obejmuje on nazwę hello co ustanowienia, typu hello ustanowienia, adres hello, hello danych inspekcji hello i lokalizacja hello, między innymi. Ta funkcja pozwala wybrać kilka kolumn, które są przydatne w przypadku naszego analizy predykcyjnej i wyniki hello grupy jako dataframe, które firma Microsoft, a następnie użyć toocreate tabeli tymczasowej.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Teraz *dataframe*, `df` na którym można wykonać nasze analizy. Mamy także wywołania tabeli tymczasowej **CountResults**. Dodaliśmy cztery kolumny zainteresowanie hello dataframe: **identyfikator**, **nazwa**, **wyniki**, i **naruszeń**.

    Załóż małej przykładowej hello danych:

        df.show(5)

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>Zrozumienie hello danych
1. Zacznijmy tooget w pewnym sensie zawiera naszym zestawie danych. Na przykład, jakie są różne wartości hello w hello **wyniki** kolumny?

        df.select('results').distinct().show()

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. Szybkie wizualizacji, ułatwisz nam przeglądanie informacji o dystrybucji hello tych wyników. Mamy już hello danych w tabeli tymczasowej **CountResults**. Możesz uruchomić hello następujące zapytanie SQL tooget tabeli hello lepiej zrozumieć rozkład hello wyników.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Witaj `%%sql` magic następuje `-o countResultsdf` gwarantuje, że hello wyników kwerendy hello jest trwały lokalnie na serwerze Jupyter hello (zazwyczaj hello headnode hello klastra). dane wyjściowe Hello jest utrwalony jako [Pandas](http://pandas.pydata.org/) dataframe z hello określona nazwa **countResultsdf**.

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

    ![Dane wyjściowe kwerendy SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "wyników zapytania SQL")

    Aby uzyskać więcej informacji na temat hello `%%sql` magic i innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. Można również użyć Matplotlib, tooconstruct wizualizację danych, toocreate wykresu użycie biblioteki. Ponieważ kreślenia hello musi być utworzony na podstawie hello lokalnie utrwalone **countResultsdf** dataframe, fragment kodu hello musi rozpoczynać się od hello `%%local` magic. Dzięki temu, że kod hello uruchamiane lokalnie na serwerze Jupyter hello.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

    ![Wyjście Spark machine learning aplikacji - wykres kołowy z pięciu wyników inspekcji różne](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "maszyny Spark uczenia wyników w danych wyjściowych")
1. Aby sprawdzić, czy 5 różne wyniki, które mogą mieć inspekcji:

   * Biznesowe, które nie znajdują się
   * Niepowodzenie
   * — Dostęp próbny
   * PSS z warunkami
   * Poza biznesowa

     Daj nam opracowywania modelu, który można odgadnąć hello wyników kontroli żywności, danego hello naruszeń. Regresja logistyczna jest metoda klasyfikacji binarnej, ułatwia wykrywanie toogroup naszych danych na dwie kategorie: **niepowodzenie** i **przekazać**. "Przekaż z warunkami" jest nadal przekazywanym, gdy firma Microsoft uczenia modelu hello, możemy należy wziąć pod uwagę hello dwa powoduje równoważne. Dane z hello innych wyników ("Nie znajduje się biznesowych" lub "Out of Business") nie są przydatne, możemy usunąć je z naszego zestawu szkoleniowego. Powinno to być poprawny, ponieważ te dwie kategorie tworzą niewielka wyników hello mimo to.
1. Daj nam Przejdź dalej i przekonwertować naszych istniejących dataframe (`df`) do nowej dataframe, gdzie każdej kontroli jest reprezentowany jako pary naruszeń etykiety. W tym przypadku etykiety `0.0` reprezentuje awarii etykiety `1.0` reprezentuje sukcesu i etykiety `-1.0` reprezentuje pewnych wyników oprócz tych dwóch. Firma Microsoft odfiltrować innych uzyskanych przy obliczaniu hello nowej ramki danych.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee jakie hello etykietą danych, który wygląda jak, możemy pobrać jeden wiersz.

        labeledData.take(1)

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Tworzenie modelu Regresja logistyczna z hello dataframe wejściowych
Nasze ostatnim zadaniem jest etykietą danych do formatu, który może zostać przeanalizowana przez Regresja logistyczna hello tooconvert. Algorytm Regresja logistyczna wejściowych tooa Hello powinna być zestaw *pary wektor etykiety funkcji*, gdzie "Funkcja wektor" hello jest wektorem liczb reprezentujący hello punktu wejściowego. Tak potrzebujemy tooconvert naruszeń"hello" kolumny, która jest częściową strukturą i zawiera wiele komentarzy w tablicy tooan niezależne, liczb rzeczywistych, które maszyna można łatwo zrozumieć.

Jednym z podejść learning standardowe maszyny do przetwarzania języka naturalnego jest tooassign każdego wyrazu różne "index", a następnie przekazać Algorytm uczenia w taki sposób, że każdy indeks wartość zawiera hello względną częstotliwość tego wyrazu w tekście hello maszynę toohello wektora ciąg.

MLlib zapewnia prosty sposób tooperform tej operacji. Po pierwsze "tokenizacji" każdego naruszenia ciąg tooget hello poszczególnych wyrazów w każdym ciągu. Następnie należy użyć `HashingTF` tooconvert każdy zestaw tokenów do wektora funkcji, które następnie mogą być przekazany toohello Regresja logistyczna algorytmu tooconstruct modelu. Przeprowadza się wszystkie kroki w sekwencji za pomocą "potoku".

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Ocena modelu hello na oddzielne testowego zestawu danych
Możemy użyć modelu hello utworzony wcześniej zbyt*prognozowania* jakie hello będzie wyników inspekcji nowy, oparty na powitania naruszeń, które zaobserwowano. Firma Microsoft uczenia modelu w zestawie danych hello **Food_Inspections1.csv**. Daj nam użyj drugiego zestawu danych, **Food_Inspections2.csv**, zbyt*oceny* hello siły tego modelu na nowych danych. Drugi zestaw danych (**Food_Inspections2.csv**) powinna już być hello domyślnego kontenera magazynu skojarzone z klastrem hello.

1. Witaj następujący fragment kodu tworzy nowy dataframe, **predictionsDf** zawierający prognozy hello generowane przez hello model. fragment Hello tworzy także tabeli tymczasowej o nazwie **prognoz** oparte na powitania dataframe.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. Spójrz na jeden z hello prognoz. Uruchom ten fragment kodu:

        predictionsDf.take(1)

   Brak prognozowania hello pierwszego wpisu w hello testowego zestawu danych.
1. Hello `model.transform()` metoda stosowana hello samych transformacji tooany nowych danych za pomocą hello tego samego schematu oraz uzyskania przewidywanie jak tooclassify hello danych. Możemy niektórych tooget prosty statystyk zorientować się, jak dokładny zostały naszego operacje przewidywania dla:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    dane wyjściowe Hello wygląda hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Korzystanie z platformy Spark Regresja logistyczna daje dokładne modelu hello relacji między opisy naruszeń w języku angielskim i czy danej firmy spowoduje powodzenie lub Niepowodzenie inspekcji żywności.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Utwórz wizualną reprezentację hello prognozowania
Mamy teraz utworzyć toohelp wizualizacji końcowego, który NAS przyczyny o hello wyniki tego testu.

1. Rozpoczniemy wyodrębniając prognoz różnych hello i wyniki z hello **prognoz** tabeli tymczasowej utworzony wcześniej. Witaj następujące kwerendy oddzielnych hello wyniku w postaci *true_positive*, *false_positive*, *true_negative*, i *false_negative*. W zapytaniach hello poniżej, możemy wyłączyć wizualizacji przy użyciu `-q` i zapisać dane wyjściowe hello (przy użyciu `-o`) jako dataframes, który można następnie użyć z hello `%%local` magic.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Na koniec użyj powitania po fragment toogenerate hello kreślenia przy użyciu **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Powinny być widoczne następujące dane wyjściowe hello:

    ![Spark machine learning danych wyjściowych aplikacji - wartości procentowe wykresu kołowego inspekcji żywności nie powiodło się. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Maszyny Spark uczenia wyników w danych wyjściowych")

    Na tym wykresie "pozytywny" odwołuje się kontroli żywności toohello nie powiodło się, gdy negatywny wynik odwołuje się tooa przekazany inspekcji.

## <a name="shut-down-hello-notebook"></a>Zamknij hello notesu
Po ukończeniu działania aplikacji hello, należy zamknąć hello notesu toorelease hello zasobów. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**. To zamyka i zamyka hello notesu.

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
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
