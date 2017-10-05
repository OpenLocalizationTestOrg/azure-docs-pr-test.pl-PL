---
title: "Nauki danych przy użyciu języka Scala i Spark na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak używać języka Scala dla zadania uczenia nadzorowanego maszyny z Spark skalowalne MLlib i Spark ML pakiety w klastrze usługi Azure HDInsight Spark."
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
ms.openlocfilehash: b2419f53bdc3236d7de76b89f2a0a76704e85391
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="9635a-103">Analiza danych przy użyciu języka Scala i platformy Spark na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9635a-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="9635a-104">W tym artykule przedstawiono sposób użycia Scala dla zadania uczenia nadzorowanego maszyny z Spark skalowalne MLlib i Spark ML pakiety w klastrze usługi Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="9635a-105">Przeprowadza użytkownika przez zadania, które stanowią [procesu nauki danych](http://aka.ms/datascienceprocess): wprowadzanie danych i eksploracja, wizualizacji engineering funkcji, modelowania i zużycia modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="9635a-106">Modele w artykule obejmują Regresja logistyczna i liniowych, losowe lasów i boosted gradientu drzew (GBTs), oprócz dwie typowe zadania uczenia nadzorowanego maszyny:</span><span class="sxs-lookup"><span data-stu-id="9635a-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="9635a-107">Problem regresji: prognozowania kwota tip ($) w podróży taksówki</span><span class="sxs-lookup"><span data-stu-id="9635a-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="9635a-108">Klasyfikacji binarnej: prognozowania porada lub brak porady w podróży taksówki (1/0)</span><span class="sxs-lookup"><span data-stu-id="9635a-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="9635a-109">Proces modelowania wymaga uczenie i Ewaluacja testowego zestawu danych i metryk odpowiednich dokładności.</span><span class="sxs-lookup"><span data-stu-id="9635a-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="9635a-110">W tym artykule można Dowiedz się, jak do przechowywania tych modeli w magazynie obiektów Blob platformy Azure oraz jak wynik i ocena wydajności predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="9635a-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="9635a-111">W tym artykule omówiono także bardziej zaawansowanych tematów dotyczących sposobu zoptymalizować modele za pomocą kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.</span><span class="sxs-lookup"><span data-stu-id="9635a-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="9635a-112">Dane używane jest przykładowe 2013 NYC taksówki podróży i taryfy zestawu danych dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9635a-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="9635a-113">[Scala](http://www.scala-lang.org/), funkcjonalności i zorientowany obiektowo język pojęcia integruje się język oparty na maszynie wirtualnej Java.</span><span class="sxs-lookup"><span data-stu-id="9635a-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="9635a-114">Jest skalowalna język dobrze nadają się do rozproszonego przetwarzania w chmurze, która działa w klastrze Spark w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="9635a-115">[Platforma Spark](http://spark.apache.org/) jest platforma przetwarzania równoległego open source, która obsługuje przetwarzanie w pamięci w celu zwiększania wydajności aplikacji do analizy danych big data.</span><span class="sxs-lookup"><span data-stu-id="9635a-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="9635a-116">Aparat przetwarzania Spark zaprojektowano pod kątem szybkości, łatwości użycia i zaawansowanych możliwości analitycznych.</span><span class="sxs-lookup"><span data-stu-id="9635a-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="9635a-117">Możliwości rozproszone obliczenia w pamięci platforma Spark stanowić dobry wybór w przypadku algorytmów iteracyjnych używanych w machine learning i obliczeniach na grafach.</span><span class="sxs-lookup"><span data-stu-id="9635a-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="9635a-118">[Spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pakiet zawiera uniform zestaw interfejsów API wysokiego poziomu, rozszerzający danych ramek, które ułatwiają tworzenie i dostrajania praktyczne machine learning potoków.</span><span class="sxs-lookup"><span data-stu-id="9635a-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="9635a-119">[MLlib](http://spark.apache.org/mllib/) platforma Spark uczenia maszynowego Skalowalna biblioteka, udostępnia funkcje modelowania w tym środowisku rozproszonym.</span><span class="sxs-lookup"><span data-stu-id="9635a-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="9635a-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) jest oferty hostowanymi na platformie Azure open source platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="9635a-121">On również obsługą notesów Jupyter Scala w klastrze Spark i można uruchomić interakcyjnych zapytań Spark SQL do przekształcania, filtrować i wizualizacji danych przechowywanych w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="9635a-122">Uruchom Scala fragmenty kodu w tym artykule dostarczające rozwiązań i Pokaż odpowiednich powierzchni do wizualizacji danych w notesach Jupyter zainstalowany w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="9635a-123">Kroki modelowania w tych tematach mają kodu, pokazujący sposób uczenia, ocenić, zapisywania i korzystać z każdego typu modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="9635a-124">Kroki instalacji i kodu w tym artykule dotyczą Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="9635a-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="9635a-125">Jednak kod w tym artykule i w [notesu Jupyter Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) są ogólne i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="9635a-126">Kroki konfiguracji i zarządzania klastra mogą być nieco inne niż co to jest wyświetlany w tym artykule, jeśli nie używasz HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="9635a-127">Dla tematu, pokazujący, jak używać języka Python, a nie Scala wykonywanie zadań w procesie nauki danych na całej trasie, zobacz [nauki danych przy użyciu platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9635a-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9635a-128">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9635a-128">Prerequisites</span></span>
* <span data-ttu-id="9635a-129">Musi mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-129">You must have an Azure subscription.</span></span> <span data-ttu-id="9635a-130">Jeśli użytkownik nie ma jeszcze jeden, [uzyskać Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9635a-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9635a-131">Należy Azure HDInsight 3.4 Spark 1.6 klastra wykonaj następujące procedury.</span><span class="sxs-lookup"><span data-stu-id="9635a-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="9635a-132">Aby utworzyć klaster, zobacz instrukcje w [wprowadzenie: tworzenie Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9635a-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="9635a-133">Ustaw typ klastra i wersji na **wybierz typ klastra** menu.</span><span class="sxs-lookup"><span data-stu-id="9635a-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![Konfiguracja typu klastra usługi HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="9635a-135">Opis NYC taksówki podróży danych i instrukcje dotyczące sposobu wykonania kodu z notesu Jupyter w klastrze Spark, zobacz w odpowiednich sekcjach [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9635a-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="9635a-136">Wykonanie kodu języka Scala z notesu Jupyter w klastrze Spark</span><span class="sxs-lookup"><span data-stu-id="9635a-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="9635a-137">Można uruchomić notesu Jupyter z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="9635a-138">Znajdź klastra Spark na pulpicie nawigacyjnym, a następnie kliknij go do wprowadź strony zarządzania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="9635a-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="9635a-139">Następnie kliknij przycisk **pulpitów nawigacyjnych klastrów**, a następnie kliknij przycisk **notesu Jupyter** otworzyć notesu skojarzony z klastrem Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![Pulpit nawigacyjny klastra i notesów Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="9635a-141">Również można uzyskać dostęp notesów Jupyter w https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="9635a-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="9635a-142">Zastąp *clustername* z nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="9635a-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="9635a-143">Potrzebne hasło dla konta administratora dostęp do notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9635a-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![Przejdź do notesów Jupyter przy użyciu nazwy klastra](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="9635a-145">Wybierz **Scala** wyświetlić katalog, który ma kilka przykładów opakowaniach jednostkowych notebooki, które korzystają z interfejsu API PySpark.</span><span class="sxs-lookup"><span data-stu-id="9635a-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="9635a-146">Przykłady eksploracji modelowania i oceniania za pomocą notesu Scala.ipynb, który zawiera kod dla tego zestawu tematy Spark jest dostępna na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="9635a-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="9635a-147">Możesz przekazać notesu bezpośrednio z serwisu GitHub do serwera notesu Jupyter w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="9635a-148">Na stronie głównej Jupyter kliknij **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9635a-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="9635a-149">W Eksploratorze plików, wklej adres URL usługi GitHub (nieprzetworzonej zawartości) notesu Scala, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="9635a-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="9635a-150">Scala notesu jest dostępny pod adresem URL:</span><span class="sxs-lookup"><span data-stu-id="9635a-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="9635a-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="9635a-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="9635a-152">Instalatora: Konteksty ustawienie wstępne Spark i Hive, poleceń magicznych Spark i biblioteki Spark</span><span class="sxs-lookup"><span data-stu-id="9635a-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="9635a-153">Konteksty Spark i Hive ustawień wstępnych.</span><span class="sxs-lookup"><span data-stu-id="9635a-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="9635a-154">Jądra Spark, które są dostarczane z notesów Jupyter mają wstępnie kontekstach.</span><span class="sxs-lookup"><span data-stu-id="9635a-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="9635a-155">Nie musisz jawnie ustawić Spark lub tworzenia kontekstów gałęzi, przed rozpoczęciem pracy z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="9635a-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="9635a-156">Predefiniowanych kontekstach są:</span><span class="sxs-lookup"><span data-stu-id="9635a-156">The preset contexts are:</span></span>

* <span data-ttu-id="9635a-157">`sc`dla SparkContext</span><span class="sxs-lookup"><span data-stu-id="9635a-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="9635a-158">`sqlContext`dla HiveContext</span><span class="sxs-lookup"><span data-stu-id="9635a-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="9635a-159">Platforma Spark poleceń magicznych</span><span class="sxs-lookup"><span data-stu-id="9635a-159">Spark magics</span></span>
<span data-ttu-id="9635a-160">Jądra Spark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z `%%`.</span><span class="sxs-lookup"><span data-stu-id="9635a-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="9635a-161">Dwa z tych poleceń są używane w następujących przykładach kodu.</span><span class="sxs-lookup"><span data-stu-id="9635a-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="9635a-162">`%%local`Określa lokalnie wykonać kod w kolejnych wierszach.</span><span class="sxs-lookup"><span data-stu-id="9635a-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="9635a-163">Kod musi być prawidłowy kod języka Scala.</span><span class="sxs-lookup"><span data-stu-id="9635a-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="9635a-164">`%%sql -o <variable name>`wykonuje zapytanie Hive względem `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="9635a-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="9635a-165">Jeśli `-o` parametr jest przekazywany, w wyniku zapytania jest trwały `%%local` kontekstu Scala jako ramki danych platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="9635a-166">Dla więcej informacji na temat jądra notesów Jupyter i ich wstępnie zdefiniowanych "magics" która zostanie wywołana za pomocą `%%` (na przykład `%%local`), zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="9635a-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="9635a-167">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="9635a-167">Import libraries</span></span>
<span data-ttu-id="9635a-168">Importowanie Spark, MLlib i innych bibliotek, które będą potrzebne przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="9635a-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="9635a-169">Wprowadzanie danych</span><span class="sxs-lookup"><span data-stu-id="9635a-169">Data ingestion</span></span>
<span data-ttu-id="9635a-170">Pierwszym krokiem w procesie nauki danych jest pozyskiwania danych, które mają być analizowane.</span><span class="sxs-lookup"><span data-stu-id="9635a-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="9635a-171">Można przenosić dane ze źródeł zewnętrznych lub systemy, w którym znajduje się w środowisku eksploracji i modelowanie danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="9635a-172">W tym artykule dane, które można pozyskiwania jest połączone próbka 0,1% (przechowywane jako plik .tsv) pliku podróży i taryfy taksówki.</span><span class="sxs-lookup"><span data-stu-id="9635a-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="9635a-173">Środowisko eksploracji i modelowanie danych jest Spark.</span><span class="sxs-lookup"><span data-stu-id="9635a-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="9635a-174">Ta sekcja zawiera kod, aby wykonać poniższą sekwencję zadań:</span><span class="sxs-lookup"><span data-stu-id="9635a-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="9635a-175">Ustawianie ścieżki katalogu dla magazynu danych i modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="9635a-176">Odczyt w zestawie danych wejściowych (przechowywane jako plik .tsv).</span><span class="sxs-lookup"><span data-stu-id="9635a-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="9635a-177">Zdefiniuj schemat dla danych i czyszczenie danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="9635a-178">Utwórz ramkę, oczyszczony danych i ją buforują w pamięci.</span><span class="sxs-lookup"><span data-stu-id="9635a-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="9635a-179">Rejestruje dane jako element SQLContext tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="9635a-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="9635a-180">Zapytanie tabeli i zaimportuj wyniki do ramki danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="9635a-181">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w magazynie obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9635a-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="9635a-182">Platforma Spark można odczytu i zapisu do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="9635a-183">Można używać platformy Spark można przetworzyć żadnych istniejących danych, a następnie ponownie zapisane wyniki w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="9635a-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="9635a-184">Aby zapisać modele lub plików w magazynie obiektów Blob, należy poprawnie określić ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="9635a-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="9635a-185">Odwołanie dołączony do klastra Spark przy użyciu ścieżki, która rozpoczyna się od domyślnego kontenera `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="9635a-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="9635a-186">Odwołania z innych lokalizacji za pomocą `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="9635a-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="9635a-187">Poniższy przykład kodu określa lokalizacji danych wejściowych do odczytu i ścieżkę do magazynu obiektów Blob, który jest dołączony do klastra Spark, w którym zostanie zapisany modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="9635a-188">Importuj dane, tworzyć RDD i zdefiniowanie ramki danych według schematu</span><span class="sxs-lookup"><span data-stu-id="9635a-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
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

    # CAST VARIABLES ACCORDING TO THE SCHEMA
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

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-189">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-189">**Output:**</span></span>

<span data-ttu-id="9635a-190">Czas uruchamiania komórki: 8 sekund.</span><span class="sxs-lookup"><span data-stu-id="9635a-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="9635a-191">Zapytanie tabeli i importowanie wyników w ramce danych</span><span class="sxs-lookup"><span data-stu-id="9635a-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="9635a-192">Następnie zapytania tabeli taryfy, pasażerów i Porada danych; Filtrowanie danych uszkodzona i odległe mniejsze; i drukowanie kilka wierszy.</span><span class="sxs-lookup"><span data-stu-id="9635a-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="9635a-193">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-193">**Output:**</span></span>

| <span data-ttu-id="9635a-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="9635a-194">fare_amount</span></span> | <span data-ttu-id="9635a-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="9635a-195">passenger_count</span></span> | <span data-ttu-id="9635a-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="9635a-196">tip_amount</span></span> | <span data-ttu-id="9635a-197">Przechylony</span><span class="sxs-lookup"><span data-stu-id="9635a-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="9635a-198">13.5</span><span class="sxs-lookup"><span data-stu-id="9635a-198">13.5</span></span> |<span data-ttu-id="9635a-199">1.0</span><span class="sxs-lookup"><span data-stu-id="9635a-199">1.0</span></span> |<span data-ttu-id="9635a-200">2.9</span><span class="sxs-lookup"><span data-stu-id="9635a-200">2.9</span></span> |<span data-ttu-id="9635a-201">1.0</span><span class="sxs-lookup"><span data-stu-id="9635a-201">1.0</span></span> |
|        <span data-ttu-id="9635a-202">16.0</span><span class="sxs-lookup"><span data-stu-id="9635a-202">16.0</span></span> |<span data-ttu-id="9635a-203">2.0</span><span class="sxs-lookup"><span data-stu-id="9635a-203">2.0</span></span> |<span data-ttu-id="9635a-204">3.4</span><span class="sxs-lookup"><span data-stu-id="9635a-204">3.4</span></span> |<span data-ttu-id="9635a-205">1.0</span><span class="sxs-lookup"><span data-stu-id="9635a-205">1.0</span></span> |
|        <span data-ttu-id="9635a-206">10.5</span><span class="sxs-lookup"><span data-stu-id="9635a-206">10.5</span></span> |<span data-ttu-id="9635a-207">2.0</span><span class="sxs-lookup"><span data-stu-id="9635a-207">2.0</span></span> |<span data-ttu-id="9635a-208">1.0</span><span class="sxs-lookup"><span data-stu-id="9635a-208">1.0</span></span> |<span data-ttu-id="9635a-209">1.0</span><span class="sxs-lookup"><span data-stu-id="9635a-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="9635a-210">Eksploracja danych i wizualizacji</span><span class="sxs-lookup"><span data-stu-id="9635a-210">Data exploration and visualization</span></span>
<span data-ttu-id="9635a-211">Po przywróceniu danych do platformy Spark następnym krokiem w procesie nauki danych jest lepiej zrozumieć dane za pośrednictwem eksploracji i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="9635a-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="9635a-212">W tej sekcji należy zbadać taksówki danych za pomocą zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="9635a-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="9635a-213">Następnie można zaimportować wyników do ramki danych do wykreślenia docelowych zmiennych i potencjalnego funkcje kontroli visual przy użyciu funkcji automatycznego wizualizacji Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9635a-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="9635a-214">Użyj lokalnej i SQL magic do wykreślenia danych</span><span class="sxs-lookup"><span data-stu-id="9635a-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="9635a-215">Domyślnie dane wyjściowe wszelkie fragmenty kodu, które można uruchomić z notesu Jupyter jest dostępna w kontekście sesji, która jest utrwalony na węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="9635a-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="9635a-216">Jeśli chcesz zapisać podróży z węzłami procesu roboczego do każdego obliczeń, a jeśli wszystkie dane potrzebne do Twojej obliczeń jest dostępny lokalnie na węźle serwera Jupyter (który jest węzłem głównym), możesz użyć `%%local` magic do uruchomienia fragmentu kodu na Jupyter serwer.</span><span class="sxs-lookup"><span data-stu-id="9635a-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="9635a-217">**Magiczna SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="9635a-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="9635a-218">Jądro Spark w usłudze HDInsight obsługuje łatwe wbudowanego HiveQL zapytań dotyczących element SQLContext.</span><span class="sxs-lookup"><span data-stu-id="9635a-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="9635a-219">(`-o VARIABLE_NAME`) Argument będzie się powtarzał wyniki kwerendy SQL jako Pandas ramki danych na serwerze Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9635a-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="9635a-220">Oznacza to, że będzie on dostępny w trybie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9635a-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="9635a-221">`%%local`**magic**.</span><span class="sxs-lookup"><span data-stu-id="9635a-221">`%%local` **magic**.</span></span> <span data-ttu-id="9635a-222">`%%local` Magic uruchamia kod lokalnie na serwerze Jupyter, który jest węzłem głównym klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9635a-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="9635a-223">Zazwyczaj `%%local` magic w połączeniu z `%%sql` magic z `-o` parametru.</span><span class="sxs-lookup"><span data-stu-id="9635a-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="9635a-224">`-o` Parametru czy zachować dane wyjściowe kwerendy SQL lokalnie, a następnie `%%local` magic spowoduje wywołanie następnego zestawu fragment kodu w celu uruchomienia lokalnie wynik zapytania SQL jest trwały lokalnie.</span><span class="sxs-lookup"><span data-stu-id="9635a-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="9635a-225">Zapytanie danych przy użyciu języka SQL</span><span class="sxs-lookup"><span data-stu-id="9635a-225">Query the data by using SQL</span></span>
<span data-ttu-id="9635a-226">To zapytanie pobiera rund taksówki kwota taryfy, liczba osób i wielkość poradę.</span><span class="sxs-lookup"><span data-stu-id="9635a-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="9635a-227">W poniższym kodzie `%%local` magic tworzy ramkę danych lokalnych, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="9635a-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="9635a-228">SqlResults służy do wykreślenia przy użyciu matplotlib.</span><span class="sxs-lookup"><span data-stu-id="9635a-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="9635a-229">Lokalne magic jest używana wiele razy w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9635a-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="9635a-230">Jeśli zestaw danych jest duży, sprawdź przykładowe utworzyć ramki danych, który można umieścić w pamięci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="9635a-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="9635a-231">Danych</span><span class="sxs-lookup"><span data-stu-id="9635a-231">Plot the data</span></span>
<span data-ttu-id="9635a-232">Można przedstawić przy użyciu kodu języka Python, po ramka danych znajduje się w kontekście lokalnego jako Pandas ramki danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="9635a-233">Jądra Spark automatycznie wizualizuje wynik zapytania SQL (HiveQL), po uruchomieniu kodu.</span><span class="sxs-lookup"><span data-stu-id="9635a-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="9635a-234">Można wybrać różne wizualizacje:</span><span class="sxs-lookup"><span data-stu-id="9635a-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="9635a-235">Tabela</span><span class="sxs-lookup"><span data-stu-id="9635a-235">Table</span></span>
* <span data-ttu-id="9635a-236">Kołowy</span><span class="sxs-lookup"><span data-stu-id="9635a-236">Pie</span></span>
* <span data-ttu-id="9635a-237">Kreska</span><span class="sxs-lookup"><span data-stu-id="9635a-237">Line</span></span>
* <span data-ttu-id="9635a-238">Obszar</span><span class="sxs-lookup"><span data-stu-id="9635a-238">Area</span></span>
* <span data-ttu-id="9635a-239">Pasek</span><span class="sxs-lookup"><span data-stu-id="9635a-239">Bar</span></span>

<span data-ttu-id="9635a-240">Oto kod danych:</span><span class="sxs-lookup"><span data-stu-id="9635a-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="9635a-241">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-241">**Output:**</span></span>

![Porada kwota histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Porada kwota kwotę Taryfy](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="9635a-245">Tworzenie funkcji i przekształcanie funkcji, a następnie przygotowywanie danych na dane wejściowe do funkcji modelowania</span><span class="sxs-lookup"><span data-stu-id="9635a-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="9635a-246">Dla funkcji oparta na drzewie modelowania z Spark ML i MLlib należy przygotować docelowy i funkcji przy użyciu różnych technik, takich jak binning, indeksowania hot jeden kodowania i vectorization.</span><span class="sxs-lookup"><span data-stu-id="9635a-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="9635a-247">Poniżej przedstawiono procedurę należy wykonać w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="9635a-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="9635a-248">Utwórz nową funkcję przez **binning** przedziałów czasu godzin w ruchu.</span><span class="sxs-lookup"><span data-stu-id="9635a-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="9635a-249">Zastosuj **indeksowanie i hot jeden kodowanie** podzielone na kategorie funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="9635a-250">**Przykładowe i podziałem w zestawie danych** do ułamków szkoleniowych i testów.</span><span class="sxs-lookup"><span data-stu-id="9635a-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="9635a-251">**Określ zmienną szkolenia i funkcje**, następnie tworzenie indeksowanych lub hot jeden zakodowane uczenie i testowanie wejściowego punktu etykietą odporność rozproszonych zestawów danych (RDDs) lub ramek danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="9635a-252">Automatycznie **klasyfikowanie i vectorize funkcje i obiekty docelowe** do użycia jako dane wejściowe dla modeli uczenia maszyny.</span><span class="sxs-lookup"><span data-stu-id="9635a-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="9635a-253">Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu</span><span class="sxs-lookup"><span data-stu-id="9635a-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="9635a-254">Ten kod przedstawia sposób tworzenia nowej funkcji według godzin binning do ruchu przedziałów czasu i sposób pamięci podręcznej wynikowe ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="9635a-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="9635a-255">Gdzie ramki RDDs i dane są używane wielokrotnie, buforowanie prowadzi do ulepszone czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9635a-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="9635a-256">W związku z tym będzie buforować RDDs i ramek danych w kilku etapach w poniższych procedurach.</span><span class="sxs-lookup"><span data-stu-id="9635a-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

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

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="9635a-257">Indeksowanie i hot jeden kodowanie funkcji podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="9635a-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="9635a-258">Modelowania i prognozowania z kategorii danych wejściowych indeksowanego lub zakodowane przed użyciem funkcji wymagają funkcji MLlib.</span><span class="sxs-lookup"><span data-stu-id="9635a-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="9635a-259">W tej sekcji przedstawiono sposób indeksu lub zakodować podzielone na kategorie funkcje na dane wejściowe do funkcji modelowania.</span><span class="sxs-lookup"><span data-stu-id="9635a-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="9635a-260">Musisz indeksu lub zakodować modeli na różne sposoby, w zależności od modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="9635a-261">Na przykład Regresja logistyczna i liniowej modele wymagają dynamicznego jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="9635a-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="9635a-262">Na przykład funkcja z trzech kategorii można rozszerzyć do trzech kolumn funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="9635a-263">Każda kolumna może zawierać 0 lub 1 w zależności od rodzaju obserwacji.</span><span class="sxs-lookup"><span data-stu-id="9635a-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="9635a-264">Udostępnia MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcja dynamicznego jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="9635a-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="9635a-265">Ten koder mapuje kolumny indeksów etykiety z kolumną wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="9635a-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="9635a-266">Z tego kodowania algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna może odnosić się do funkcji podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="9635a-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="9635a-267">W tym miejscu możesz przekształcić tylko cztery zmienne, aby wyświetlić przykłady, które są ciągami znaków.</span><span class="sxs-lookup"><span data-stu-id="9635a-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="9635a-268">Można również indeksu innych zmiennych, takich jak dzień tygodnia, reprezentowany przez wartości liczbowe, jako zmienne podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="9635a-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="9635a-269">Indeksowanie, użyj `StringIndexer()`i hot jeden kodowanie, użyj `OneHotEncoder()` funkcji z MLlib.</span><span class="sxs-lookup"><span data-stu-id="9635a-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="9635a-270">Oto kod do indeksu i kodowania funkcji podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="9635a-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
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

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-271">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-271">**Output:**</span></span>

<span data-ttu-id="9635a-272">Czas uruchamiania komórki: 4 sekundy.</span><span class="sxs-lookup"><span data-stu-id="9635a-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="9635a-273">Przykładowe i podziału do ułamków szkoleniowych i testów w zestawie danych</span><span class="sxs-lookup"><span data-stu-id="9635a-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="9635a-274">Ten kod tworzy losowej próbki danych (w tym przykładzie 25%).</span><span class="sxs-lookup"><span data-stu-id="9635a-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="9635a-275">Próbkowanie nie jest wymagany w tym przykładzie ze względu na rozmiar zestawu danych, artykuł pokazuje, jak można przykładowe, aby wiedzieć, jak użyć jej do własnych problemów, gdy jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="9635a-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="9635a-276">W przypadku dużych przykłady to zapisanie długiego czasu podczas uczenia modeli.</span><span class="sxs-lookup"><span data-stu-id="9635a-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="9635a-277">Następnie podzielone próbki części szkolenia (75%, w tym przykładzie) i testowania część (25%, w tym przykładzie) do użycia w klasyfikacji i regresji modelowania.</span><span class="sxs-lookup"><span data-stu-id="9635a-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="9635a-278">Dodaj liczbę losową (między 0 a 1) do każdego wiersza (w kolumnie "rand"), który może służyć do wybrania złożeń krzyżowego sprawdzania poprawności podczas uczenia.</span><span class="sxs-lookup"><span data-stu-id="9635a-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
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

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-279">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-279">**Output:**</span></span>

<span data-ttu-id="9635a-280">Czas uruchamiania komórki: 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="9635a-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="9635a-281">Określ zmienną szkolenia i funkcje, a następnie utwórz indeksowanych lub hot jeden kodowane celów szkoleniowych i testów danych wejściowych z etykietą punktu RDDs lub danych ramki</span><span class="sxs-lookup"><span data-stu-id="9635a-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="9635a-282">Ta sekcja zawiera kod, pokazujący sposób indeksować dane tekstowe podzielone na kategorie jako typ etykietą punktu danych i kodować je, aby użyć w celu nauczenia i przetestowania Regresja logistyczna MLlib i inne modele klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9635a-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="9635a-283">Obiekty etykietą punktu są RDDs sformatowanych w taki sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów w MLlib uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="9635a-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="9635a-284">A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="9635a-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="9635a-285">W tym kodzie Określ zmienną docelową (zależnych) i funkcji do użycia w celu przeszkolenia modeli.</span><span class="sxs-lookup"><span data-stu-id="9635a-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="9635a-286">Następnie można utworzyć indeksowanych lub hot jeden kodowane celów szkoleniowych i testów z etykietą punktu RDDs lub danych ramek danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-287">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-287">**Output:**</span></span>

<span data-ttu-id="9635a-288">Czas uruchamiania komórki: 4 sekundy.</span><span class="sxs-lookup"><span data-stu-id="9635a-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="9635a-289">Automatycznie klasyfikowanie i vectorize funkcje i obiekty docelowe do użycia jako dane wejściowe dla modeli uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="9635a-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="9635a-290">Umożliwia klasyfikowanie docelowych i funkcji do użycia w funkcji oparta na drzewie modelowania Spark ML.</span><span class="sxs-lookup"><span data-stu-id="9635a-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="9635a-291">Kod wykonuje dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="9635a-291">The code completes two tasks:</span></span>

* <span data-ttu-id="9635a-292">Tworzy binarne docelowy klasyfikacji przypisując wartość 0 lub 1 w każdym punkcie danych pomiędzy 0 a 1 przy użyciu progu wartości 0,5.</span><span class="sxs-lookup"><span data-stu-id="9635a-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="9635a-293">Automatycznie kategoryzuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-293">Automatically categorizes features.</span></span> <span data-ttu-id="9635a-294">Liczba unikatowych wartości liczbowe dla dowolnej funkcji jest mniejsza niż 32, kategoryzowane tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="9635a-295">Oto kod dla tych dwóch zadań.</span><span class="sxs-lookup"><span data-stu-id="9635a-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

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

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="9635a-296">Model klasyfikacji binarnej: prognozowania, czy należy zwrócić porady</span><span class="sxs-lookup"><span data-stu-id="9635a-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="9635a-297">W tej sekcji można tworzyć trzy typy modele klasyfikacji binarnej do prognozowania, czy należy zwrócić Porada:</span><span class="sxs-lookup"><span data-stu-id="9635a-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="9635a-298">A **modelu Regresja logistyczna** przy użyciu Spark ML `LogisticRegression()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="9635a-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="9635a-299">A **model klasyfikacji losowe lasu** przy użyciu Spark ML `RandomForestClassifier()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="9635a-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="9635a-300">A **gradientu zwiększania wyniku model klasyfikacji drzewa** za pomocą MLlib `GradientBoostedTrees()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="9635a-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="9635a-301">Tworzenie modelu Regresja logistyczna</span><span class="sxs-lookup"><span data-stu-id="9635a-301">Create a logistic regression model</span></span>
<span data-ttu-id="9635a-302">Następnie należy utworzyć model Regresja logistyczna przy użyciu Spark ML `LogisticRegression()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="9635a-303">Można utworzyć modelu kompilowania kodu w serii kroków:</span><span class="sxs-lookup"><span data-stu-id="9635a-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="9635a-304">**Nauczenia modelu** danych za pomocą jednego zestawu parametrów.</span><span class="sxs-lookup"><span data-stu-id="9635a-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="9635a-305">**Oceń model** na testowego zestawu danych o metryki.</span><span class="sxs-lookup"><span data-stu-id="9635a-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="9635a-306">**Zapisz model** w magazynie obiektów Blob do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9635a-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="9635a-307">**Klasyfikacja modelu** względem danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="9635a-308">**Wykreślenia wyniki** z odbiornikiem operacyjnego krzywych cechy (ROC).</span><span class="sxs-lookup"><span data-stu-id="9635a-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="9635a-309">Oto kod dla tych procedur:</span><span class="sxs-lookup"><span data-stu-id="9635a-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="9635a-310">Obciążenia, wynik i zapisać wyniki.</span><span class="sxs-lookup"><span data-stu-id="9635a-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="9635a-311">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-311">**Output:**</span></span>

<span data-ttu-id="9635a-312">ROC na danych testowych = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="9635a-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="9635a-313">W systemie Python lokalnego ramek danych Pandas do wykreślenia krzywą ROC.</span><span class="sxs-lookup"><span data-stu-id="9635a-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
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


<span data-ttu-id="9635a-314">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-314">**Output:**</span></span>

![Porada lub nie krzywą ROC Porada](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="9635a-316">Utwórz model klasyfikacji losowe lasu</span><span class="sxs-lookup"><span data-stu-id="9635a-316">Create a random forest classification model</span></span>
<span data-ttu-id="9635a-317">Następnie utwórz model klasyfikacji losowe lasu za pomocą Spark ML `RandomForestClassifier()` funkcji, a następnie ocenę modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="9635a-318">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-318">**Output:**</span></span>

<span data-ttu-id="9635a-319">ROC na danych testowych = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="9635a-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="9635a-320">Utwórz model klasyfikacji GBT</span><span class="sxs-lookup"><span data-stu-id="9635a-320">Create a GBT classification model</span></span>
<span data-ttu-id="9635a-321">Następnie utwórz model klasyfikacji GBT przy użyciu jego MLlib `GradientBoostedTrees()` funkcji, a następnie ocenę modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="9635a-322">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-322">**Output:**</span></span>

<span data-ttu-id="9635a-323">Obszar pod krzywą ROC: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="9635a-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="9635a-324">Model regresji: przewidywanie kwota Porada</span><span class="sxs-lookup"><span data-stu-id="9635a-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="9635a-325">W tej sekcji można tworzyć dwa typy regresji modeli na potrzeby prognozowania kwota Porada:</span><span class="sxs-lookup"><span data-stu-id="9635a-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="9635a-326">A **model regresji liniowej umorzyć** przy użyciu Spark ML `LinearRegression()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="9635a-327">Należy zapisać model i ocena modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="9635a-328">A **zwiększania gradientu drzewa modelu regresji** przy użyciu Spark ML `GBTRegressor()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="9635a-329">Tworzenie modelu regresji liniowej umorzyć</span><span class="sxs-lookup"><span data-stu-id="9635a-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-330">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-330">**Output:**</span></span>

<span data-ttu-id="9635a-331">Czas uruchamiania komórki: 13 sekund.</span><span class="sxs-lookup"><span data-stu-id="9635a-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="9635a-332">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-332">**Output:**</span></span>

<span data-ttu-id="9635a-333">R — sqr na danych testowych = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="9635a-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="9635a-334">Następnie wyniki testu zapytania jako ramki danych i użyj AutoVizWidget i matplotlib do wizualizacji go.</span><span class="sxs-lookup"><span data-stu-id="9635a-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="9635a-335">Kod tworzy ramkę danych lokalnych z wyników kwerendy i zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="9635a-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="9635a-336">`%%local` Magic tworzy ramkę dane lokalne `sqlResults`, które służy do wykreślenia z matplotlib.</span><span class="sxs-lookup"><span data-stu-id="9635a-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="9635a-337">Ta magic Spark jest używana wiele razy w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9635a-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="9635a-338">W przypadku dużych ilości danych, powinny przykładowe utworzyć ramki danych, który można umieścić w pamięci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="9635a-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="9635a-339">Utwórz powierzchni za pomocą matplotlib języka Python.</span><span class="sxs-lookup"><span data-stu-id="9635a-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="9635a-340">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-340">**Output:**</span></span>

![Porada kwota: rzeczywiste a przewidywane](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="9635a-342">Tworzenie modelu regresji GBT</span><span class="sxs-lookup"><span data-stu-id="9635a-342">Create a GBT regression model</span></span>
<span data-ttu-id="9635a-343">Tworzenie modelu regresji GBT przy użyciu Spark ML `GBTRegressor()` funkcji, a następnie ocenę modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="9635a-344">[Boosted gradientu drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="9635a-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="9635a-345">GBTs uczenie drzew decyzyjnych wielokrotnie powtarzane, aby zminimalizować funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="9635a-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="9635a-346">Można użyć GBTs regresji i klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9635a-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="9635a-347">One mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i przechwytywać nonlinearities i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="9635a-348">Możesz również można używać ich w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9635a-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="9635a-349">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-349">**Output:**</span></span>

<span data-ttu-id="9635a-350">Jest test R-sqr: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="9635a-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="9635a-351">Modelowania zaawansowanych narzędzi do optymalizacji</span><span class="sxs-lookup"><span data-stu-id="9635a-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="9635a-352">W tej sekcji można za pomocą narzędzi learning maszyny, które deweloperzy często używane na potrzeby optymalizacji modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="9635a-353">W szczególności za pomocą parametru kominów i krzyżowego sprawdzania poprawności można zoptymalizować machine learning modeli trzy różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="9635a-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="9635a-354">Podział danych na zestawy pociągu i sprawdzania poprawności, optymalizacja modelu przy użyciu funkcji hyper parametr kominów na zestaw szkoleniowy i oceny na zestawie sprawdzania poprawności (regresja liniowa)</span><span class="sxs-lookup"><span data-stu-id="9635a-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="9635a-355">Optymalizacja modelu przy użyciu krzyżowego sprawdzania poprawności i funkcji hyper parametru profilach za pomocą funkcji CrossValidator Spark ML (klasyfikacji binarnej)</span><span class="sxs-lookup"><span data-stu-id="9635a-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="9635a-356">Optymalizacja modelu przy użyciu kodu niestandardowego krzyżowego sprawdzania poprawności i parametr kominów używać żadnych machine learning zestaw funkcji i parametr (regresja liniowa)</span><span class="sxs-lookup"><span data-stu-id="9635a-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="9635a-357">**Krzyżowe sprawdzanie poprawności** to technika, który ocenia, jak model ćwiczenie znanego zestawu danych zostanie generalize do prognozowania funkcje zestawów danych, które go nie przeprowadzono uczenia.</span><span class="sxs-lookup"><span data-stu-id="9635a-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="9635a-358">Ogólne ideą ta technika jest, czy model jest uczony w zestawie danych znanych danych, a następnie dokładność jego prognoz jest testowana niezależnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="9635a-359">Standardowa implementacja polega ona na dzieleniu zestawu danych do *k*-złożeń, a następnie nauczenia modelu w okrężne na wszystkie oprócz jednego złożeń.</span><span class="sxs-lookup"><span data-stu-id="9635a-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="9635a-360">**Optymalizacja parametru Hyper** jest problem wybrać zestaw funkcji hyper-parametrów Algorytm uczenia, zwykle z celem optymalizacji miara wydajności algorytm na niezależnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9635a-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="9635a-361">Funkcji hyper parametr to wartość, która należy określić poza procedury szkolenie modelu.</span><span class="sxs-lookup"><span data-stu-id="9635a-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="9635a-362">Założenia dotyczące wartości parametrów funkcji hyper może mieć wpływ na dokładność modelu i elastyczność.</span><span class="sxs-lookup"><span data-stu-id="9635a-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="9635a-363">Drzewa decyzyjne mieć funkcji hyper parametrów, na przykład żądaną głębokość i liczby pozostawia w drzewie.</span><span class="sxs-lookup"><span data-stu-id="9635a-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="9635a-364">Należy ustawić termin kar błędną klasyfikację maszyny wektorowa obsługa (SVM).</span><span class="sxs-lookup"><span data-stu-id="9635a-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="9635a-365">Typowym sposobem wykonania optymalizacji parametru funkcji hyper jest użycie wyszukiwanie siatki, nazywany również **odchylenia parametru**.</span><span class="sxs-lookup"><span data-stu-id="9635a-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="9635a-366">W wyszukiwaniu siatki kompleksowe przeszukiwanie odbywa się za pomocą wartości podzbiór określonego obszaru funkcji hyper parametr Algorytm uczenia.</span><span class="sxs-lookup"><span data-stu-id="9635a-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="9635a-367">Krzyżowe sprawdzanie poprawności można podać metryki wydajności, aby posortować optymalne wyniki utworzone przez algorytm wyszukiwania siatki.</span><span class="sxs-lookup"><span data-stu-id="9635a-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="9635a-368">Jeśli używasz krzyżowe sprawdzanie poprawności parametru hyper kominów może pomóc limit problemów, takich jak overfitting przy użyciu modelu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="9635a-369">W ten sposób modelu zachowuje pojemności do zastosowania do ogólny zestaw danych, z którego został wyodrębniony danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="9635a-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="9635a-370">Optymalizacja model regresji liniowej z kominów hyper parametru</span><span class="sxs-lookup"><span data-stu-id="9635a-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="9635a-371">Następnie podzielenia danych na zestawy pociągu i sprawdzania poprawności, użyj funkcji hyper parametru profilach na zestaw szkoleniowy, można zoptymalizować modelu oraz ocenić na zestawie sprawdzania poprawności (regresja liniowa).</span><span class="sxs-lookup"><span data-stu-id="9635a-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="9635a-372">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-372">**Output:**</span></span>

<span data-ttu-id="9635a-373">Jest test R-sqr: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="9635a-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="9635a-374">Optymalizacja model klasyfikacji binarnej przy użyciu kominów krzyżowego sprawdzania poprawności i funkcji hyper parametru</span><span class="sxs-lookup"><span data-stu-id="9635a-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="9635a-375">Tej sekcji przedstawiono, jak zoptymalizować model klasyfikacji binarnej przy użyciu kominów krzyżowego sprawdzania poprawności i parametr hyper.</span><span class="sxs-lookup"><span data-stu-id="9635a-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="9635a-376">Ta metoda korzysta z ML Spark `CrossValidator` funkcji.</span><span class="sxs-lookup"><span data-stu-id="9635a-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="9635a-377">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-377">**Output:**</span></span>

<span data-ttu-id="9635a-378">Czas uruchamiania komórki: 33 sekundy.</span><span class="sxs-lookup"><span data-stu-id="9635a-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="9635a-379">Optymalizacja model regresji liniowej przy użyciu kodu niestandardowego krzyżowego sprawdzania poprawności i kominów parametru</span><span class="sxs-lookup"><span data-stu-id="9635a-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="9635a-380">Następnie zoptymalizować modelu przy użyciu niestandardowego kodu i zidentyfikować najlepszych parametrów modelu przy użyciu kryterium najwyższy dokładności.</span><span class="sxs-lookup"><span data-stu-id="9635a-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="9635a-381">Następnie utwórz ostatecznego modelu, ewaluacji modelu na danych testowych i zapisać modelu w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="9635a-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="9635a-382">Na koniec załadować modelu, wynik testu danych i oceny dokładności.</span><span class="sxs-lookup"><span data-stu-id="9635a-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
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


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
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

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="9635a-383">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9635a-383">**Output:**</span></span>

<span data-ttu-id="9635a-384">Czas uruchamiania komórki: 61 sekund.</span><span class="sxs-lookup"><span data-stu-id="9635a-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="9635a-385">Korzystanie z modeli uczenia wbudowane Spark maszyny automatycznie z języka Scala</span><span class="sxs-lookup"><span data-stu-id="9635a-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="9635a-386">Omówienie tematów, które umożliwia przeprowadzenie zadań wchodzące w skład procesu nauki danych na platformie Azure, zobacz [proces nauki danych zespołu](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="9635a-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="9635a-387">[Wskazówki dotyczące procesu nauki danych Team](data-science-process-walkthroughs.md) opisano inne end-to-end wskazówki, które pokazują czynności w procesie nauki zespołu danych w określonych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="9635a-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="9635a-388">Wskazówki dotyczące przedstawiono również sposób łączenia chmurze i lokalnych narzędzi i usług w przepływie pracy lub potoku, aby utworzyć aplikację inteligentnego.</span><span class="sxs-lookup"><span data-stu-id="9635a-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="9635a-389">[Wynik modeli uczenia maszynowego wbudowane Spark](machine-learning-data-science-spark-model-consumption.md) przedstawiono sposób za pomocą kodu języka Scala można automatycznie załadować oraz wynik nowe zestawy danych przy użyciu modeli uczenia maszynowego wbudowane Spark i zapisane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9635a-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="9635a-390">Postępuj zgodnie z instrukcjami istnieje i po prostu zastąpić Python Scala kodu w tym artykule wykorzystania automatycznych.</span><span class="sxs-lookup"><span data-stu-id="9635a-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

