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
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="ef4ae-104">Użyj toobuild Spark MLlib aplikacji uczenia maszynowego i analizować zestawu danych</span><span class="sxs-lookup"><span data-stu-id="ef4ae-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="ef4ae-105">Dowiedz się, jak toouse Spark **MLlib** toocreate a machine learning toodo aplikacji proste analizy predykcyjnej na Otwórz zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="ef4ae-106">Z maszyny wbudowanych platforma Spark uczenia biblioteki, w tym przykładzie użyto *klasyfikacji* za pośrednictwem Regresja logistyczna.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="ef4ae-107">W tym przykładzie jest również dostępny jako notesu Jupyter w klastrze Spark (Linux), które są tworzone w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="ef4ae-108">środowisko notesu Hello umożliwia uruchamianie hello Python wstawki z notesu hello, sama.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="ef4ae-109">Samouczek hello toofollow z poziomu Notes, Utwórz Spark klastra, a następnie uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="ef4ae-110">A następnie uruchomić notesu hello **Spark Machine Learning - analizy predykcyjnej na dane inspekcji żywności przy użyciu MLlib.ipynb** w obszarze hello **Python** folderu.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="ef4ae-111">MLlib jest biblioteki Spark core, która udostępnia wiele narzędzi przydatne dla machine learning zadania, w tym narzędzia, które są odpowiednie dla:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="ef4ae-112">Klasyfikacja</span><span class="sxs-lookup"><span data-stu-id="ef4ae-112">Classification</span></span>
* <span data-ttu-id="ef4ae-113">Regresja</span><span class="sxs-lookup"><span data-stu-id="ef4ae-113">Regression</span></span>
* <span data-ttu-id="ef4ae-114">Klaster</span><span class="sxs-lookup"><span data-stu-id="ef4ae-114">Clustering</span></span>
* <span data-ttu-id="ef4ae-115">Temat modelowania</span><span class="sxs-lookup"><span data-stu-id="ef4ae-115">Topic modeling</span></span>
* <span data-ttu-id="ef4ae-116">Rozkład wartości pojedynczej (SVD) i analizy głównych składników (PCA)</span><span class="sxs-lookup"><span data-stu-id="ef4ae-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="ef4ae-117">Hipoteza testowania i obliczania statystyk próbki</span><span class="sxs-lookup"><span data-stu-id="ef4ae-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="ef4ae-118">Jakie są klasyfikacji i Regresja logistyczna?</span><span class="sxs-lookup"><span data-stu-id="ef4ae-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="ef4ae-119">*Klasyfikacja*, maszynę popularnych uczenia zadań, proces hello sortowanie danych wejściowych w kategorie.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="ef4ae-120">To zadanie hello z toofigure algorytm klasyfikacji, jak tooassign "etykiety" tooinput dane, które należy podać.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="ef4ae-121">Na przykład można traktować z algorytmu uczenia maszynowego, który akceptuje podstawowe informacje jako dane wejściowe i bez reszty hello giełdowych na dwie kategorie: zasobów, które powinny sprzedaży i zasobów, które należy przechowywać.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="ef4ae-122">Regresja logistyczna jest algorytm hello, której użyjesz dla klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="ef4ae-123">Regresja logistyczna firmy Spark interfejsu API jest przydatne w przypadku *klasyfikacji binarnej*, lub klasyfikacji danych wejściowych do jednej z dwóch grup.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="ef4ae-124">Aby uzyskać więcej informacji na temat logistyczna regresji, zobacz [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="ef4ae-125">Podsumowując, tworzy proces hello Regresja logistyczna *logistyczna funkcja* które może być używane toopredict hello prawdopodobieństwo, że wektor wejściowy należy w jednej grupie lub hello innych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="ef4ae-126">Przykład analizy predykcyjnej w danych kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="ef4ae-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="ef4ae-127">W tym przykładzie używasz Spark tooperform niektóre predykcyjnych analizy danych inspekcji żywności (**Food_Inspections1.csv**) które zostało zakupione w ramach hello [portalu danych Miasto Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="ef4ae-128">Ten zestaw danych zawiera informacje o kontroli ustanowienia żywności, które były przeprowadzane w Chicago, wraz z informacjami dotyczącymi każdego zakładu, naruszeń hello znaleziono (jeśli istnieje) i hello wyniki inspekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="ef4ae-129">plik danych CSV Hello jest już dostępny w hello konta magazynu skojarzone z klastrem hello na **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="ef4ae-130">W poniższych krokach hello opracowywanie toosee modelu, co jest potrzebne toopass lub Niepowodzenie inspekcji żywności.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="ef4ae-131">Rozpocząć tworzenie aplikacji uczenia maszynowego Spark MMLib</span><span class="sxs-lookup"><span data-stu-id="ef4ae-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="ef4ae-132">Z hello [portalu Azure](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="ef4ae-133">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="ef4ae-134">W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="ef4ae-135">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef4ae-136">Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="ef4ae-137">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="ef4ae-138">Utwórz notes.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-138">Create a notebook.</span></span> <span data-ttu-id="ef4ae-139">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="ef4ae-140">![Tworzenie notesu Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="ef4ae-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="ef4ae-141">Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="ef4ae-142">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="ef4ae-143">![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Podaj nazwę notesu hello")</span><span class="sxs-lookup"><span data-stu-id="ef4ae-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="ef4ae-144">Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="ef4ae-145">konteksty Spark i Hive Hello są utworzony automatycznie po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="ef4ae-146">Można rozpocząć tworzenie komputera nauki aplikacji przez zaimportowanie typów hello wymaganych dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="ef4ae-147">toodo tak, umieść kursor hello w komórce hello i naciśnij klawisze **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="ef4ae-148">Konstrukcja dataframe wejściowych</span><span class="sxs-lookup"><span data-stu-id="ef4ae-148">Construct an input dataframe</span></span>
<span data-ttu-id="ef4ae-149">Możemy użyć `sqlContext` tooperform przekształcenia danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="ef4ae-150">pierwszym zadaniem Hello jest tooload hello przykładowych danych ((**Food_Inspections1.csv**)) do programu Spark SQL *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="ef4ae-151">Ponieważ dane pierwotne hello jest w formacie CSV, potrzebujemy toouse hello Spark kontekstu toopull każdy wiersz w pliku hello do pamięci jako tekst bez struktury. następnie należy użyć języka Python CSV biblioteki tooparse każdego wiersza pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="ef4ae-152">Mamy teraz hello pliku CSV jako RDD.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="ef4ae-153">Schemat hello toounderstand hello danych, możemy pobrać jeden wiersz z hello RDD.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="ef4ae-154">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-154">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="ef4ae-155">Witaj Powyższy wynik daje wyobrażenie o hello schemat pliku wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="ef4ae-156">Obejmuje on nazwę hello co ustanowienia, typu hello ustanowienia, adres hello, hello danych inspekcji hello i lokalizacja hello, między innymi.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="ef4ae-157">Ta funkcja pozwala wybrać kilka kolumn, które są przydatne w przypadku naszego analizy predykcyjnej i wyniki hello grupy jako dataframe, które firma Microsoft, a następnie użyć toocreate tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="ef4ae-158">Teraz *dataframe*, `df` na którym można wykonać nasze analizy.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="ef4ae-159">Mamy także wywołania tabeli tymczasowej **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="ef4ae-160">Dodaliśmy cztery kolumny zainteresowanie hello dataframe: **identyfikator**, **nazwa**, **wyniki**, i **naruszeń**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="ef4ae-161">Załóż małej przykładowej hello danych:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="ef4ae-162">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-162">You should see an output like hello following:</span></span>

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

## <a name="understand-hello-data"></a><span data-ttu-id="ef4ae-163">Zrozumienie hello danych</span><span class="sxs-lookup"><span data-stu-id="ef4ae-163">Understand hello data</span></span>
1. <span data-ttu-id="ef4ae-164">Zacznijmy tooget w pewnym sensie zawiera naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="ef4ae-165">Na przykład, jakie są różne wartości hello w hello **wyniki** kolumny?</span><span class="sxs-lookup"><span data-stu-id="ef4ae-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="ef4ae-166">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="ef4ae-167">Szybkie wizualizacji, ułatwisz nam przeglądanie informacji o dystrybucji hello tych wyników.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="ef4ae-168">Mamy już hello danych w tabeli tymczasowej **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="ef4ae-169">Możesz uruchomić hello następujące zapytanie SQL tooget tabeli hello lepiej zrozumieć rozkład hello wyników.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="ef4ae-170">Witaj `%%sql` magic następuje `-o countResultsdf` gwarantuje, że hello wyników kwerendy hello jest trwały lokalnie na serwerze Jupyter hello (zazwyczaj hello headnode hello klastra).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="ef4ae-171">dane wyjściowe Hello jest utrwalony jako [Pandas](http://pandas.pydata.org/) dataframe z hello określona nazwa **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="ef4ae-172">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="ef4ae-173">![Dane wyjściowe kwerendy SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "wyników zapytania SQL")</span><span class="sxs-lookup"><span data-stu-id="ef4ae-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="ef4ae-174">Aby uzyskać więcej informacji na temat hello `%%sql` magic i innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="ef4ae-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="ef4ae-175">Można również użyć Matplotlib, tooconstruct wizualizację danych, toocreate wykresu użycie biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="ef4ae-176">Ponieważ kreślenia hello musi być utworzony na podstawie hello lokalnie utrwalone **countResultsdf** dataframe, fragment kodu hello musi rozpoczynać się od hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="ef4ae-177">Dzięki temu, że kod hello uruchamiane lokalnie na serwerze Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="ef4ae-178">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="ef4ae-179">![Wyjście Spark machine learning aplikacji - wykres kołowy z pięciu wyników inspekcji różne](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "maszyny Spark uczenia wyników w danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="ef4ae-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="ef4ae-180">Aby sprawdzić, czy 5 różne wyniki, które mogą mieć inspekcji:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="ef4ae-181">Biznesowe, które nie znajdują się</span><span class="sxs-lookup"><span data-stu-id="ef4ae-181">Business not located</span></span>
   * <span data-ttu-id="ef4ae-182">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="ef4ae-182">Fail</span></span>
   * <span data-ttu-id="ef4ae-183">— Dostęp próbny</span><span class="sxs-lookup"><span data-stu-id="ef4ae-183">Pass</span></span>
   * <span data-ttu-id="ef4ae-184">PSS z warunkami</span><span class="sxs-lookup"><span data-stu-id="ef4ae-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="ef4ae-185">Poza biznesowa</span><span class="sxs-lookup"><span data-stu-id="ef4ae-185">Out of Business</span></span>

     <span data-ttu-id="ef4ae-186">Daj nam opracowywania modelu, który można odgadnąć hello wyników kontroli żywności, danego hello naruszeń.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="ef4ae-187">Regresja logistyczna jest metoda klasyfikacji binarnej, ułatwia wykrywanie toogroup naszych danych na dwie kategorie: **niepowodzenie** i **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="ef4ae-188">"Przekaż z warunkami" jest nadal przekazywanym, gdy firma Microsoft uczenia modelu hello, możemy należy wziąć pod uwagę hello dwa powoduje równoważne.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="ef4ae-189">Dane z hello innych wyników ("Nie znajduje się biznesowych" lub "Out of Business") nie są przydatne, możemy usunąć je z naszego zestawu szkoleniowego.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="ef4ae-190">Powinno to być poprawny, ponieważ te dwie kategorie tworzą niewielka wyników hello mimo to.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="ef4ae-191">Daj nam Przejdź dalej i przekonwertować naszych istniejących dataframe (`df`) do nowej dataframe, gdzie każdej kontroli jest reprezentowany jako pary naruszeń etykiety.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="ef4ae-192">W tym przypadku etykiety `0.0` reprezentuje awarii etykiety `1.0` reprezentuje sukcesu i etykiety `-1.0` reprezentuje pewnych wyników oprócz tych dwóch.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="ef4ae-193">Firma Microsoft odfiltrować innych uzyskanych przy obliczaniu hello nowej ramki danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="ef4ae-194">toosee jakie hello etykietą danych, który wygląda jak, możemy pobrać jeden wiersz.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="ef4ae-195">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="ef4ae-196">Tworzenie modelu Regresja logistyczna z hello dataframe wejściowych</span><span class="sxs-lookup"><span data-stu-id="ef4ae-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="ef4ae-197">Nasze ostatnim zadaniem jest etykietą danych do formatu, który może zostać przeanalizowana przez Regresja logistyczna hello tooconvert.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="ef4ae-198">Algorytm Regresja logistyczna wejściowych tooa Hello powinna być zestaw *pary wektor etykiety funkcji*, gdzie "Funkcja wektor" hello jest wektorem liczb reprezentujący hello punktu wejściowego.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="ef4ae-199">Tak potrzebujemy tooconvert naruszeń"hello" kolumny, która jest częściową strukturą i zawiera wiele komentarzy w tablicy tooan niezależne, liczb rzeczywistych, które maszyna można łatwo zrozumieć.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="ef4ae-200">Jednym z podejść learning standardowe maszyny do przetwarzania języka naturalnego jest tooassign każdego wyrazu różne "index", a następnie przekazać Algorytm uczenia w taki sposób, że każdy indeks wartość zawiera hello względną częstotliwość tego wyrazu w tekście hello maszynę toohello wektora ciąg.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="ef4ae-201">MLlib zapewnia prosty sposób tooperform tej operacji.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="ef4ae-202">Po pierwsze "tokenizacji" każdego naruszenia ciąg tooget hello poszczególnych wyrazów w każdym ciągu.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="ef4ae-203">Następnie należy użyć `HashingTF` tooconvert każdy zestaw tokenów do wektora funkcji, które następnie mogą być przekazany toohello Regresja logistyczna algorytmu tooconstruct modelu.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="ef4ae-204">Przeprowadza się wszystkie kroki w sekwencji za pomocą "potoku".</span><span class="sxs-lookup"><span data-stu-id="ef4ae-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="ef4ae-205">Ocena modelu hello na oddzielne testowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="ef4ae-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="ef4ae-206">Możemy użyć modelu hello utworzony wcześniej zbyt*prognozowania* jakie hello będzie wyników inspekcji nowy, oparty na powitania naruszeń, które zaobserwowano.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="ef4ae-207">Firma Microsoft uczenia modelu w zestawie danych hello **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="ef4ae-208">Daj nam użyj drugiego zestawu danych, **Food_Inspections2.csv**, zbyt*oceny* hello siły tego modelu na nowych danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="ef4ae-209">Drugi zestaw danych (**Food_Inspections2.csv**) powinna już być hello domyślnego kontenera magazynu skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="ef4ae-210">Witaj następujący fragment kodu tworzy nowy dataframe, **predictionsDf** zawierający prognozy hello generowane przez hello model.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="ef4ae-211">fragment Hello tworzy także tabeli tymczasowej o nazwie **prognoz** oparte na powitania dataframe.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="ef4ae-212">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="ef4ae-213">Spójrz na jeden z hello prognoz.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-213">Look at one of hello predictions.</span></span> <span data-ttu-id="ef4ae-214">Uruchom ten fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="ef4ae-215">Brak prognozowania hello pierwszego wpisu w hello testowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="ef4ae-216">Hello `model.transform()` metoda stosowana hello samych transformacji tooany nowych danych za pomocą hello tego samego schematu oraz uzyskania przewidywanie jak tooclassify hello danych.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="ef4ae-217">Możemy niektórych tooget prosty statystyk zorientować się, jak dokładny zostały naszego operacje przewidywania dla:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="ef4ae-218">dane wyjściowe Hello wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="ef4ae-219">Korzystanie z platformy Spark Regresja logistyczna daje dokładne modelu hello relacji między opisy naruszeń w języku angielskim i czy danej firmy spowoduje powodzenie lub Niepowodzenie inspekcji żywności.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="ef4ae-220">Utwórz wizualną reprezentację hello prognozowania</span><span class="sxs-lookup"><span data-stu-id="ef4ae-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="ef4ae-221">Mamy teraz utworzyć toohelp wizualizacji końcowego, który NAS przyczyny o hello wyniki tego testu.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="ef4ae-222">Rozpoczniemy wyodrębniając prognoz różnych hello i wyniki z hello **prognoz** tabeli tymczasowej utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="ef4ae-223">Witaj następujące kwerendy oddzielnych hello wyniku w postaci *true_positive*, *false_positive*, *true_negative*, i *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="ef4ae-224">W zapytaniach hello poniżej, możemy wyłączyć wizualizacji przy użyciu `-q` i zapisać dane wyjściowe hello (przy użyciu `-o`) jako dataframes, który można następnie użyć z hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="ef4ae-225">Na koniec użyj powitania po fragment toogenerate hello kreślenia przy użyciu **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="ef4ae-226">Powinny być widoczne następujące dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="ef4ae-226">You should see hello following output:</span></span>

    <span data-ttu-id="ef4ae-227">![Spark machine learning danych wyjściowych aplikacji - wartości procentowe wykresu kołowego inspekcji żywności nie powiodło się. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Maszyny Spark uczenia wyników w danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="ef4ae-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="ef4ae-228">Na tym wykresie "pozytywny" odwołuje się kontroli żywności toohello nie powiodło się, gdy negatywny wynik odwołuje się tooa przekazany inspekcji.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="ef4ae-229">Zamknij hello notesu</span><span class="sxs-lookup"><span data-stu-id="ef4ae-229">Shut down hello notebook</span></span>
<span data-ttu-id="ef4ae-230">Po ukończeniu działania aplikacji hello, należy zamknąć hello notesu toorelease hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="ef4ae-231">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="ef4ae-232">To zamyka i zamyka hello notesu.</span><span class="sxs-lookup"><span data-stu-id="ef4ae-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="ef4ae-233"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ef4ae-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ef4ae-234">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="ef4ae-235">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="ef4ae-235">Scenarios</span></span>
* [<span data-ttu-id="ef4ae-236">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="ef4ae-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ef4ae-237">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="ef4ae-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ef4ae-238">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ef4ae-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ef4ae-239">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ef4ae-240">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ef4ae-240">Create and run applications</span></span>
* [<span data-ttu-id="ef4ae-241">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="ef4ae-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ef4ae-242">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="ef4ae-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ef4ae-243">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="ef4ae-243">Tools and extensions</span></span>
* [<span data-ttu-id="ef4ae-244">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ef4ae-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ef4ae-245">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="ef4ae-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ef4ae-246">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ef4ae-247">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ef4ae-248">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="ef4ae-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ef4ae-249">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ef4ae-250">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="ef4ae-250">Manage resources</span></span>
* [<span data-ttu-id="ef4ae-251">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ef4ae-252">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef4ae-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
