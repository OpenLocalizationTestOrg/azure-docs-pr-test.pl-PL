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
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="f776f-103">Tworzenie aplikacji do uczenia maszynowego Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="f776f-104">Dowiedz się, jak toobuild aplikacji learning maszyny Apache Spark przy użyciu Spark klastra w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f776f-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="f776f-105">W tym artykule przedstawiono sposób toouse hello notesu Jupyter dostępne z hello toobuild klastra i przetestować tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="f776f-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="f776f-106">Aplikacja Hello używa hello przykładowych HVAC.csv danych, które jest dostępne na wszystkich klastrach domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f776f-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="f776f-107">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="f776f-107">**Prerequisites:**</span></span>

<span data-ttu-id="f776f-108">Musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f776f-108">You must have hello following:</span></span>

* <span data-ttu-id="f776f-109">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f776f-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f776f-110">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f776f-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="f776f-111"><a name="data"></a>Zrozumienie hello zestawu danych</span><span class="sxs-lookup"><span data-stu-id="f776f-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="f776f-112">Przed możemy rozpocząć tworzenie aplikacji hello, Daj nam poznać strukturę hello hello danych, dla którego budujemy aplikacji hello i rodzaj hello analizy, która spowoduje wykonanie na powitania danych.</span><span class="sxs-lookup"><span data-stu-id="f776f-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="f776f-113">W tym artykule używamy próbki hello **HVAC.csv** pliku danych, który jest dostępny w hello skojarzony z klastrem usługi HDInsight hello konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="f776f-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="f776f-114">W ramach konta magazynu hello, plik hello jest na **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="f776f-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="f776f-115">Pobierz i otwórz tooget pliku CSV hello migawkę hello danych.</span><span class="sxs-lookup"><span data-stu-id="f776f-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="f776f-116">![Migawki danych używanych na przykład learning maszyny Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "migawki dane używane na potrzeby Spark machine learning przykład")</span><span class="sxs-lookup"><span data-stu-id="f776f-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="f776f-117">Hello dane zostaną wyświetlone temperatury docelowy hello i temperatury rzeczywiste hello budynku, który ma zainstalowane systemy HVAC.</span><span class="sxs-lookup"><span data-stu-id="f776f-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="f776f-118">Załóżmy, że hello **systemu** kolumna reprezentuje identyfikator systemu hello i hello **SystemAge** kolumna reprezentuje hello kilka lat temu hello HVAC system był w miejscu w budynku hello.</span><span class="sxs-lookup"><span data-stu-id="f776f-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="f776f-119">Używamy tej toopredict danych czy budynku będą hotter lub colder oparte na temperatury docelowy hello, identyfikator systemowy i wiek systemu.</span><span class="sxs-lookup"><span data-stu-id="f776f-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="f776f-120"><a name="app"></a>Napisać aplikację learning maszyny Spark przy użyciu Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="f776f-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="f776f-121">W tej aplikacji używamy tooperform potoku Spark ML klasyfikacji dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f776f-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="f776f-122">W potoku hello firma Microsoft podzielone dokumentu hello słów, konwertować wyrazy hello wektor funkcji numerycznych i koniec kompilacji modelu prognozowania przy użyciu hello funkcji wektorów i etykiety.</span><span class="sxs-lookup"><span data-stu-id="f776f-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="f776f-123">Wykonaj następujące kroki toocreate hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f776f-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="f776f-124">Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="f776f-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="f776f-125">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f776f-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="f776f-126">W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="f776f-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="f776f-127">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f776f-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f776f-128">Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="f776f-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="f776f-129">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="f776f-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="f776f-130">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="f776f-130">Create a new notebook.</span></span> <span data-ttu-id="f776f-131">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="f776f-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="f776f-132">![Tworzenie notesu Jupyter, na przykład learning maszyny Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "tworzenie notesu Jupyter, na przykład learning maszyny Spark")</span><span class="sxs-lookup"><span data-stu-id="f776f-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="f776f-133">Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="f776f-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="f776f-134">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="f776f-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="f776f-135">![Podaj nazwę notesu Spark machine learning przykład](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Podaj nazwę notesu Spark machine learning przykład")</span><span class="sxs-lookup"><span data-stu-id="f776f-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="f776f-136">Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie.</span><span class="sxs-lookup"><span data-stu-id="f776f-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="f776f-137">konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="f776f-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="f776f-138">Możesz zacząć od importowania typów hello, które są wymagane dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="f776f-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="f776f-139">Witaj następującego fragmentu kodu w pustej komórce Wklej, a następnie naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="f776f-140">Musi teraz ładowanie danych hello (hvac.csv), przeanalizować go i użyć go tootrain hello modelu.</span><span class="sxs-lookup"><span data-stu-id="f776f-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="f776f-141">W tym celu należy zdefiniować funkcję, która sprawdza, czy hello temperatury rzeczywiste konstruowania hello jest większa niż hello docelowy temperatury.</span><span class="sxs-lookup"><span data-stu-id="f776f-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="f776f-142">Jeśli rzeczywista temperatury hello jest większa, kompilowanie hello jest gorących, określone przez wartość hello **1.0**.</span><span class="sxs-lookup"><span data-stu-id="f776f-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="f776f-143">W przypadku mniejszej temperatury rzeczywiste hello budynku hello jest zimnych, określone przez wartość hello **0,0**.</span><span class="sxs-lookup"><span data-stu-id="f776f-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="f776f-144">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

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


1. <span data-ttu-id="f776f-145">Konfiguruje potok uczenia maszynowego hello Spark, która składa się z trzech etapów: tokenizatora, hashingTF i lr.</span><span class="sxs-lookup"><span data-stu-id="f776f-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="f776f-146">Aby uzyskać więcej informacji na temat nowości potoku i jak działa zobacz <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning potoku</a>.</span><span class="sxs-lookup"><span data-stu-id="f776f-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="f776f-147">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="f776f-148">Dopasuj hello potoku toohello szkolenia dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f776f-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="f776f-149">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="f776f-150">Sprawdź hello szkolenia dokumentu toocheckpoint postęp z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f776f-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="f776f-151">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="f776f-152">To powinien zapewnić hello dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="f776f-152">This should give hello output similar toohello following:</span></span>
   
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

    <span data-ttu-id="f776f-153">Przejdź wstecz i sprawdź dane wyjściowe hello na powitania raw pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="f776f-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="f776f-154">Na przykład hello pierwszego wiersza hello pliku CSV zawiera te dane:</span><span class="sxs-lookup"><span data-stu-id="f776f-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="f776f-155">![Migawki Spark machine learning przykładowe dane wyjściowe](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "migawki danych wyjściowych na Spark machine learning przykład")</span><span class="sxs-lookup"><span data-stu-id="f776f-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="f776f-156">Zwróć uwagę, jak temperatury rzeczywiste hello jest mniejsza niż temperatury docelowy hello sugerowanie budynku hello jest zimnych.</span><span class="sxs-lookup"><span data-stu-id="f776f-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="f776f-157">Dlatego w danych wyjściowych szkolenia hello hello wartość **etykiety** w hello jest pierwszy wiersz **0,0**, co oznacza, że kompilowanie hello nie jest dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="f776f-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="f776f-158">Przygotuj zestawu danych toorun hello uczonego modelu przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="f776f-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="f776f-159">toodo tak, czy jest przekazywana na identyfikator systemu i wiek systemu (oznaczonego jako **SystemInfo** w danych wyjściowych szkolenia hello), i czy prognozowania modelu hello czy hello kompilowanie z tego systemu wieku systemu i identyfikator może być hotter (wskazywane przez 1.0) lub lodówki () wskazywane przez 0,0).</span><span class="sxs-lookup"><span data-stu-id="f776f-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="f776f-160">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="f776f-161">Na koniec tworzenia prognoz na powitania danych testowych.</span><span class="sxs-lookup"><span data-stu-id="f776f-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="f776f-162">Wklej hello następującego fragmentu kodu w pustej komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f776f-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="f776f-163">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="f776f-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="f776f-164">W pierwszym wierszu hello w hello prognozowania, widać, że systemu HVAC o identyfikatorze 20 i wiek systemu 25 lat budynek hello będzie gorących (**prognozowania = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="f776f-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="f776f-165">wartość pierwszego Hello DenseVector (0.49999) odpowiada toohello prognozowania 0,0 i hello drugiej wartości (0.5001) odpowiada prognozowania toohello 1.0.</span><span class="sxs-lookup"><span data-stu-id="f776f-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="f776f-166">W danych wyjściowych hello, mimo że hello druga wartość jest tylko nieznacznie wyższe hello model przedstawia **prognozowania = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="f776f-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="f776f-167">Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f776f-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="f776f-168">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="f776f-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="f776f-169">To spowoduje zamknięcie i zamknij hello notesu.</span><span class="sxs-lookup"><span data-stu-id="f776f-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="f776f-170"><a name="anaconda"></a>Użyj Anaconda scikit — Dowiedz się biblioteki Spark uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="f776f-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="f776f-171">Klastry platformy Apache Spark w usłudze HDInsight obejmują bibliotekami Anaconda.</span><span class="sxs-lookup"><span data-stu-id="f776f-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="f776f-172">Obejmuje to także hello **scikit — Dowiedz się** biblioteki uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="f776f-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="f776f-173">Biblioteka Hello także różne zestawy danych można toobuild przykładowe aplikacje bezpośrednio z notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f776f-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="f776f-174">Dla przykłady dotyczące używania hello scikit — Dowiedz się, biblioteka, zobacz [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="f776f-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="f776f-175"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f776f-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f776f-176">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f776f-177">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="f776f-177">Scenarios</span></span>
* [<span data-ttu-id="f776f-178">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="f776f-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f776f-179">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f776f-180">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f776f-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f776f-181">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f776f-182">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f776f-182">Create and run applications</span></span>
* [<span data-ttu-id="f776f-183">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="f776f-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f776f-184">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="f776f-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f776f-185">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f776f-185">Tools and extensions</span></span>
* [<span data-ttu-id="f776f-186">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="f776f-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f776f-187">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="f776f-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f776f-188">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f776f-189">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f776f-190">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="f776f-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f776f-191">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f776f-192">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="f776f-192">Manage resources</span></span>
* [<span data-ttu-id="f776f-193">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f776f-194">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f776f-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
