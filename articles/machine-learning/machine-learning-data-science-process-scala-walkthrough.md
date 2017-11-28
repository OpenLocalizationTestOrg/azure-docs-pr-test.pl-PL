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
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="eff85-103">Analiza danych przy użyciu języka Scala i platformy Spark na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eff85-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="eff85-104">W tym artykule opisano, jak toouse Scala dla zadania uczenia nadzorowanego maszyny z hello MLlib skalowalne Spark i Spark ML pakietów w klastrze usługi Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="eff85-105">Przeprowadza użytkownika przez hello zadań, które stanowią hello [procesu nauki danych](http://aka.ms/datascienceprocess): wprowadzanie danych i eksploracja, wizualizacji engineering funkcji, modelowania i zużycia modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="eff85-106">modele Hello w artykule hello zawierają Regresja logistyczna i liniowych, losowe lasów i boosted gradientu drzew (GBTs), ponadto typowe tootwo nadzorowane machine learning zadań:</span><span class="sxs-lookup"><span data-stu-id="eff85-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="eff85-107">Problem regresji: prognozowania hello Porada kwota ($) w podróży taksówki</span><span class="sxs-lookup"><span data-stu-id="eff85-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="eff85-108">Klasyfikacji binarnej: prognozowania porada lub brak porady w podróży taksówki (1/0)</span><span class="sxs-lookup"><span data-stu-id="eff85-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="eff85-109">Hello modelowania proces wymaga uczenie i Ewaluacja testowego zestawu danych i metryk odpowiednich dokładności.</span><span class="sxs-lookup"><span data-stu-id="eff85-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="eff85-110">W tym artykule można dowiedzieć się jak toostore te modele w magazynie obiektów Blob Azure i w jaki sposób tooscore i ocena wydajności predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="eff85-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="eff85-111">W tym artykule omówiono także hello bardziej zaawansowanych tematów z jak toooptimize modeli przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.</span><span class="sxs-lookup"><span data-stu-id="eff85-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="eff85-112">dane Hello używane jest przykładowe hello 2013 NYC taksówki podróży i taryfy zestawu danych dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="eff85-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="eff85-113">[Scala](http://www.scala-lang.org/), język oparty na maszynie wirtualnej Java hello integruje pojęcia dotyczące języka zorientowane obiektowo i funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="eff85-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="eff85-114">Jest skalowalna język, jest dobrze nadają się toodistributed przetwarzania w chmurze hello, która działa w klastrze Spark w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="eff85-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="eff85-115">[Platforma Spark](http://spark.apache.org/) platforma przetwarzania równoległego open source, która obsługuje w pamięci przetwarza tooboost hello wydajność aplikacji, analizy danych big data.</span><span class="sxs-lookup"><span data-stu-id="eff85-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="eff85-116">aparat przetwarzania Spark Hello zaprojektowano pod kątem szybkości, łatwości użycia i zaawansowanych możliwości analitycznych.</span><span class="sxs-lookup"><span data-stu-id="eff85-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="eff85-117">Możliwości rozproszone obliczenia w pamięci platforma Spark stanowić dobry wybór w przypadku algorytmów iteracyjnych używanych w machine learning i obliczeniach na grafach.</span><span class="sxs-lookup"><span data-stu-id="eff85-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="eff85-118">Witaj [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pakiet zawiera uniform zestaw interfejsów API wysokiego poziomu, rozszerzający danych ramek, które ułatwiają tworzenie i dostrajania praktyczne machine learning potoków.</span><span class="sxs-lookup"><span data-stu-id="eff85-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="eff85-119">[MLlib](http://spark.apache.org/mllib/) to platforma Spark uczenia maszynowego Skalowalna biblioteka, udostępnia funkcje modelowania toothis środowisku rozproszonym.</span><span class="sxs-lookup"><span data-stu-id="eff85-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="eff85-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) jest hello hostowanymi na platformie Azure open source platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="eff85-121">Obejmuje również obsługę notesów Jupyter Scala w klastrze Spark hello i można tootransform wykonywania interakcyjnych zapytań Spark SQL, filtrów i wizualizacji danych przechowywanych w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eff85-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="eff85-122">Hello Scala wstawki kodu w tym artykule dostarczające rozwiązań hello i Pokaż hello powierzchni odpowiednie dane hello toovisualize uruchomione w systemie klastry Spark hello notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eff85-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="eff85-123">kroki modelowania Hello w tych tematach masz kod pokazujący sposób tootrain, ocenić, Zapisz i korzystać z każdego typu modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="eff85-124">Witaj kroków instalacji i kodu w tym artykule dotyczą Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="eff85-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="eff85-125">Jednak hello kodu, w tym artykule i hello [notesu Jupyter Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) są ogólne i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="eff85-126">Witaj Konfiguracja klastra i czynności administracyjne mogą być nieco inne niż co to jest wyświetlany w tym artykule, jeśli nie używasz Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eff85-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="eff85-127">Dla tematu, który pokazuje, jak toouse Python zamiast Scala toocomplete zadań w procesie nauki danych end-to-end, zobacz [nauki danych przy użyciu platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eff85-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="eff85-128">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eff85-128">Prerequisites</span></span>
* <span data-ttu-id="eff85-129">Musi mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eff85-129">You must have an Azure subscription.</span></span> <span data-ttu-id="eff85-130">Jeśli użytkownik nie ma jeszcze jeden, [uzyskać Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="eff85-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="eff85-131">Należy hello toocomplete klastra dla usługi Azure HDInsight 3.4 Spark w wersji 1.6 zgodnie z procedurami.</span><span class="sxs-lookup"><span data-stu-id="eff85-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="eff85-132">toocreate klastra, zobacz instrukcje hello w [wprowadzenie: tworzenie Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="eff85-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="eff85-133">Ustaw typ klastra hello i wersji na powitania **wybierz typ klastra** menu.</span><span class="sxs-lookup"><span data-stu-id="eff85-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Konfiguracja typu klastra usługi HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="eff85-135">Opis hello NYC taksówki podróży danych oraz instrukcje, jak tooexecute kodu z notesu Jupyter w klastrze Spark hello, zobacz hello odpowiednich części [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eff85-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="eff85-136">Wykonanie kodu języka Scala z notesu Jupyter w klastrze Spark hello</span><span class="sxs-lookup"><span data-stu-id="eff85-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="eff85-137">Można uruchomić notesu Jupyter z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eff85-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="eff85-138">Znajdź klastra Spark hello na pulpicie nawigacyjnym, a następnie kliknij go tooenter hello strony do zarządzania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="eff85-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="eff85-139">Następnie kliknij przycisk **pulpitów nawigacyjnych klastrów**, a następnie kliknij przycisk **notesu Jupyter** notesu hello tooopen skojarzony z klastrem Spark hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Pulpit nawigacyjny klastra i notesów Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="eff85-141">Również można uzyskać dostęp notesów Jupyter w https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="eff85-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="eff85-142">Zastąp *clustername* o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="eff85-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="eff85-143">Potrzebne hasło hello notesów Jupyter hello tooaccess konta administratora.</span><span class="sxs-lookup"><span data-stu-id="eff85-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Przejdź notesów tooJupyter przy użyciu nazwy klastra hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="eff85-145">Wybierz **Scala** toosee katalogu, który ma kilka przykładów opakowaniach jednostkowych notesów tego hello Użyj interfejsu API PySpark.</span><span class="sxs-lookup"><span data-stu-id="eff85-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="eff85-146">Witaj modelowania eksploracji i punktacja za pomocą notesu Scala.ipynb, który zawiera hello przykłady kodu dla tego zestawu tematy Spark jest dostępna na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="eff85-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="eff85-147">Możesz przekazać notesu hello bezpośrednio z usługi GitHub toohello serwera notesu Jupyter w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="eff85-148">Na stronie głównej Jupyter kliknij hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eff85-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="eff85-149">W Eksploratorze plików hello, wklej adres URL usługi GitHub (nieprzetworzonej zawartości) hello hello Scala notesu, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="eff85-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="eff85-150">notesu Scala Hello jest dostępna w hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="eff85-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="eff85-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="eff85-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="eff85-152">Instalatora: Konteksty ustawienie wstępne Spark i Hive, poleceń magicznych Spark i biblioteki Spark</span><span class="sxs-lookup"><span data-stu-id="eff85-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="eff85-153">Konteksty Spark i Hive ustawień wstępnych.</span><span class="sxs-lookup"><span data-stu-id="eff85-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="eff85-154">Hello Spark jądra, które są dostarczane z notesów Jupyter ma predefiniowanych kontekstach.</span><span class="sxs-lookup"><span data-stu-id="eff85-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="eff85-155">Przed rozpoczęciem pracy z aplikacją hello, które tworzysz tooexplicitly zestaw hello Spark i Hive kontekstach nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="eff85-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="eff85-156">Witaj predefiniowanych kontekstach są:</span><span class="sxs-lookup"><span data-stu-id="eff85-156">hello preset contexts are:</span></span>

* <span data-ttu-id="eff85-157">`sc`dla SparkContext</span><span class="sxs-lookup"><span data-stu-id="eff85-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="eff85-158">`sqlContext`dla HiveContext</span><span class="sxs-lookup"><span data-stu-id="eff85-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="eff85-159">Platforma Spark poleceń magicznych</span><span class="sxs-lookup"><span data-stu-id="eff85-159">Spark magics</span></span>
<span data-ttu-id="eff85-160">Witaj jądra Spark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z `%%`.</span><span class="sxs-lookup"><span data-stu-id="eff85-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="eff85-161">Dwa z tych poleceń są używane w hello następujące przykłady kodu.</span><span class="sxs-lookup"><span data-stu-id="eff85-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="eff85-162">`%%local`Określa lokalnie wykonać kod hello w kolejnych wierszach.</span><span class="sxs-lookup"><span data-stu-id="eff85-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="eff85-163">Kod Hello musi być prawidłowy kod języka Scala.</span><span class="sxs-lookup"><span data-stu-id="eff85-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="eff85-164">`%%sql -o <variable name>`wykonuje zapytanie Hive względem `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="eff85-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="eff85-165">Jeśli hello `-o` parametr jest przekazywany, w hello jest trwały hello wynik zapytania hello `%%local` kontekstu Scala jako ramki danych platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="eff85-166">Dla więcej informacji na temat jądra hello notesów Jupyter i ich wstępnie zdefiniowanych "magics" która zostanie wywołana za pomocą `%%` (na przykład `%%local`), zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="eff85-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="eff85-167">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="eff85-167">Import libraries</span></span>
<span data-ttu-id="eff85-168">Importowanie hello Spark, MLlib i innych bibliotek, które będą potrzebne przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="eff85-169">Wprowadzanie danych</span><span class="sxs-lookup"><span data-stu-id="eff85-169">Data ingestion</span></span>
<span data-ttu-id="eff85-170">pierwszym etapem hello proces analizy danych w Hello jest tooingest hello danych, które mają tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="eff85-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="eff85-171">Przełączeniem hello danych ze źródeł zewnętrznych lub systemów gdzie znajduje się on w środowisku eksploracji i modelowanie danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="eff85-172">W tym artykule należy pozyskiwania danych hello jest przyłączone do 0,1% próbka hello taksówki podróży i taryfy pliku (przechowywane jako plik .tsv).</span><span class="sxs-lookup"><span data-stu-id="eff85-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="eff85-173">środowisko eksploracji i modelowanie danych Hello jest Spark.</span><span class="sxs-lookup"><span data-stu-id="eff85-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="eff85-174">Ta sekcja zawiera hello toocomplete kod powitania po sekwencję zadań:</span><span class="sxs-lookup"><span data-stu-id="eff85-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="eff85-175">Ustawianie ścieżki katalogu dla magazynu danych i modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="eff85-176">Przeczytaj hello wejściowy zestaw danych (przechowywane jako plik .tsv).</span><span class="sxs-lookup"><span data-stu-id="eff85-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="eff85-177">Należy zdefiniować schemat danych hello i wyczyść hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="eff85-178">Utwórz ramkę, oczyszczony danych i ją buforują w pamięci.</span><span class="sxs-lookup"><span data-stu-id="eff85-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="eff85-179">Zarejestruj dane hello jako element SQLContext tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="eff85-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="eff85-180">Zapytania tabeli hello i zaimportuj hello wyniki do ramki danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="eff85-181">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w magazynie obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eff85-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="eff85-182">Platforma Spark można odczytu i zapisu tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="eff85-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="eff85-183">Można użyć Spark tooprocess żadnych istniejących danych, a następnie ponownie zapisać wyniki hello w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="eff85-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="eff85-184">modele toosave lub plików w magazynie obiektów Blob, należy tooproperly hello ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="eff85-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="eff85-185">Odwołanie hello domyślny kontener dołączony toohello klastra Spark przy użyciu ścieżki, która rozpoczyna się od `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="eff85-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="eff85-186">Odwołania z innych lokalizacji za pomocą `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="eff85-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="eff85-187">Hello poniższy przykład kodu określa hello lokalizację hello toobe danych wejściowych do odczytu i hello ścieżki tooBlob magazynu, który jest dołączony toohello klastra Spark którym zostanie zapisany hello modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="eff85-188">Importuj dane, tworzyć RDD i zdefiniowanie ramki danych zgodnie z toohello schematu</span><span class="sxs-lookup"><span data-stu-id="eff85-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
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


<span data-ttu-id="eff85-189">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-189">**Output:**</span></span>

<span data-ttu-id="eff85-190">Czas toorun hello komórki: 8 sekund.</span><span class="sxs-lookup"><span data-stu-id="eff85-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="eff85-191">Zapytania tabeli hello i importowanie wyników w ramce danych</span><span class="sxs-lookup"><span data-stu-id="eff85-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="eff85-192">Następnie tabeli hello zapytania taryfy, pasażerów i Porada danych; Filtrowanie danych uszkodzona i odległe mniejsze; i drukowanie kilka wierszy.</span><span class="sxs-lookup"><span data-stu-id="eff85-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

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

<span data-ttu-id="eff85-193">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-193">**Output:**</span></span>

| <span data-ttu-id="eff85-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="eff85-194">fare_amount</span></span> | <span data-ttu-id="eff85-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="eff85-195">passenger_count</span></span> | <span data-ttu-id="eff85-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="eff85-196">tip_amount</span></span> | <span data-ttu-id="eff85-197">Przechylony</span><span class="sxs-lookup"><span data-stu-id="eff85-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="eff85-198">13.5</span><span class="sxs-lookup"><span data-stu-id="eff85-198">13.5</span></span> |<span data-ttu-id="eff85-199">1.0</span><span class="sxs-lookup"><span data-stu-id="eff85-199">1.0</span></span> |<span data-ttu-id="eff85-200">2.9</span><span class="sxs-lookup"><span data-stu-id="eff85-200">2.9</span></span> |<span data-ttu-id="eff85-201">1.0</span><span class="sxs-lookup"><span data-stu-id="eff85-201">1.0</span></span> |
|        <span data-ttu-id="eff85-202">16.0</span><span class="sxs-lookup"><span data-stu-id="eff85-202">16.0</span></span> |<span data-ttu-id="eff85-203">2.0</span><span class="sxs-lookup"><span data-stu-id="eff85-203">2.0</span></span> |<span data-ttu-id="eff85-204">3.4</span><span class="sxs-lookup"><span data-stu-id="eff85-204">3.4</span></span> |<span data-ttu-id="eff85-205">1.0</span><span class="sxs-lookup"><span data-stu-id="eff85-205">1.0</span></span> |
|        <span data-ttu-id="eff85-206">10.5</span><span class="sxs-lookup"><span data-stu-id="eff85-206">10.5</span></span> |<span data-ttu-id="eff85-207">2.0</span><span class="sxs-lookup"><span data-stu-id="eff85-207">2.0</span></span> |<span data-ttu-id="eff85-208">1.0</span><span class="sxs-lookup"><span data-stu-id="eff85-208">1.0</span></span> |<span data-ttu-id="eff85-209">1.0</span><span class="sxs-lookup"><span data-stu-id="eff85-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="eff85-210">Eksploracja danych i wizualizacji</span><span class="sxs-lookup"><span data-stu-id="eff85-210">Data exploration and visualization</span></span>
<span data-ttu-id="eff85-211">Po przełączeniu hello danych do platformy Spark hello następnym krokiem hello procesu nauki danych jest toogain głębsze zrozumienie hello danych za pośrednictwem eksploracji i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="eff85-212">W tej sekcji należy zbadać hello taksówki danych za pomocą zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="eff85-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="eff85-213">Następnie wyników hello importu do tooplot ramki danych hello docelowych zmiennych i potencjalnego funkcje kontroli visual przy użyciu funkcji automatycznego wizualizacji hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eff85-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="eff85-214">Użyj lokalnej i danych magic tooplot SQL</span><span class="sxs-lookup"><span data-stu-id="eff85-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="eff85-215">Domyślnie dane wyjściowe hello wszelkie fragmenty kodu, które można uruchomić z notesu Jupyter jest dostępna w kontekście hello hello sesji, która jest utrwalony na powitania węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="eff85-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="eff85-216">Jeśli chcesz toosave węzłów procesu roboczego toohello podróży do każdego obliczeń i hello wszystkie dane potrzebne dla Twojego obliczenia jest dostępny lokalnie na węźle serwera Jupyter hello (który jest węzłem głównym hello), można użyć hello `%%local` Magiczna toorun hello kodu fragment kodu na powitania serwera Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eff85-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="eff85-217">**Magiczna SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="eff85-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="eff85-218">Hello jądra Spark w usłudze HDInsight obsługuje zapytania HiveQL łatwe wbudowanego przed element SQLContext.</span><span class="sxs-lookup"><span data-stu-id="eff85-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="eff85-219">Witaj (`-o VARIABLE_NAME`) argument będzie się powtarzał hello wyników kwerendy SQL hello jako ramki danych Pandas na powitania serwera Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eff85-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="eff85-220">Oznacza to, że będzie on dostępny w trybie lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="eff85-221">`%%local`**magic**.</span><span class="sxs-lookup"><span data-stu-id="eff85-221">`%%local` **magic**.</span></span> <span data-ttu-id="eff85-222">Witaj `%%local` magic działa hello kod lokalnie na serwerze Jupyter hello, czyli hello węzła głównego klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="eff85-223">Zazwyczaj `%%local` magic w połączeniu z hello `%%sql` magic z hello `-o` parametru.</span><span class="sxs-lookup"><span data-stu-id="eff85-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="eff85-224">Witaj `-o` parametru czy zachować dane wyjściowe hello hello zapytania SQL lokalnie, a następnie `%%local` magic spowoduje wywołanie hello dalej zbiór toorun fragment kodu lokalnie przed hello dane wyjściowe zapytań SQL hello jest utrwalonego lokalnie.</span><span class="sxs-lookup"><span data-stu-id="eff85-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="eff85-225">Dane hello zapytania przy użyciu języka SQL</span><span class="sxs-lookup"><span data-stu-id="eff85-225">Query hello data by using SQL</span></span>
<span data-ttu-id="eff85-226">To zapytanie pobiera rund taksówki hello kwota taryfy, liczba osób i wielkość poradę.</span><span class="sxs-lookup"><span data-stu-id="eff85-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="eff85-227">W hello następującego kodu, hello `%%local` magic tworzy ramkę danych lokalnych, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="eff85-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="eff85-228">Można użyć sqlResults tooplot przy użyciu matplotlib.</span><span class="sxs-lookup"><span data-stu-id="eff85-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="eff85-229">Lokalne magic jest używana wiele razy w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="eff85-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="eff85-230">Jeśli zestaw danych jest duży, proszę przykładowe toocreate ramki danych, który można umieścić w pamięci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="eff85-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="eff85-231">Dane hello</span><span class="sxs-lookup"><span data-stu-id="eff85-231">Plot hello data</span></span>
<span data-ttu-id="eff85-232">Można przedstawić przy użyciu kodu języka Python, po ramki danych hello w kontekście lokalnego jako Pandas ramki danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="eff85-233">jądra Spark Hello automatycznie wizualizuje hello wynik zapytania SQL (HiveQL), po uruchomieniu hello kodu.</span><span class="sxs-lookup"><span data-stu-id="eff85-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="eff85-234">Można wybrać różne wizualizacje:</span><span class="sxs-lookup"><span data-stu-id="eff85-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="eff85-235">Tabela</span><span class="sxs-lookup"><span data-stu-id="eff85-235">Table</span></span>
* <span data-ttu-id="eff85-236">Kołowy</span><span class="sxs-lookup"><span data-stu-id="eff85-236">Pie</span></span>
* <span data-ttu-id="eff85-237">Kreska</span><span class="sxs-lookup"><span data-stu-id="eff85-237">Line</span></span>
* <span data-ttu-id="eff85-238">Obszar</span><span class="sxs-lookup"><span data-stu-id="eff85-238">Area</span></span>
* <span data-ttu-id="eff85-239">Pasek</span><span class="sxs-lookup"><span data-stu-id="eff85-239">Bar</span></span>

<span data-ttu-id="eff85-240">Poniżej przedstawiono dane hello tooplot kodu hello:</span><span class="sxs-lookup"><span data-stu-id="eff85-240">Here's hello code tooplot hello data:</span></span>

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


<span data-ttu-id="eff85-241">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-241">**Output:**</span></span>

![Porada kwota histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Porada kwota kwotę Taryfy](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="eff85-245">Tworzenie funkcji i przekształcanie funkcji, a następnie przygotowywanie danych na dane wejściowe do funkcji modelowania</span><span class="sxs-lookup"><span data-stu-id="eff85-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="eff85-246">Dla funkcji oparta na drzewie modelowania z Spark ML i MLlib masz tooprepare docelowych i funkcji przy użyciu różnych technik, takich jak binning, indeksowania hot jeden kodowania i vectorization.</span><span class="sxs-lookup"><span data-stu-id="eff85-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="eff85-247">Poniżej przedstawiono hello toofollow procedury w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="eff85-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="eff85-248">Utwórz nową funkcję przez **binning** przedziałów czasu godzin w ruchu.</span><span class="sxs-lookup"><span data-stu-id="eff85-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="eff85-249">Zastosuj **indeksowanie i hot jeden kodowanie** toocategorical funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="eff85-250">**Przykładowe i podziału hello zestawu danych** do ułamków szkoleniowych i testów.</span><span class="sxs-lookup"><span data-stu-id="eff85-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="eff85-251">**Określ zmienną szkolenia i funkcje**, następnie tworzenie indeksowanych lub hot jeden zakodowane uczenie i testowanie wejściowego punktu etykietą odporność rozproszonych zestawów danych (RDDs) lub ramek danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="eff85-252">Automatycznie **klasyfikowanie i vectorize funkcje i obiekty docelowe** toouse jako dane wejściowe dla modeli uczenia maszyny.</span><span class="sxs-lookup"><span data-stu-id="eff85-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="eff85-253">Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu</span><span class="sxs-lookup"><span data-stu-id="eff85-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="eff85-254">Ten kod pokazuje, jak pakiety ramach Agreement toocreate nowa funkcja przez binning godziny do ruchu czasu i sposób toocache hello wynikowe ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="eff85-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="eff85-255">W przypadku, gdy ramki RDDs i dane są używane wielokrotnie, buforowanie prowadzi tooimproved czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="eff85-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="eff85-256">W związku z tym będzie buforować ramki RDDs i danych w kilku etapach hello zgodnie z procedurami.</span><span class="sxs-lookup"><span data-stu-id="eff85-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="eff85-257">Indeksowanie i hot jeden kodowanie funkcji podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="eff85-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="eff85-258">Witaj modelowania i prognozowania wymagają funkcji MLlib z toobe podzielone na kategorie danych wejściowych funkcji zakodowany wcześniejsze toouse lub indeksowany.</span><span class="sxs-lookup"><span data-stu-id="eff85-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="eff85-259">W tej sekcji opisano sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="eff85-260">Należy tooindex lub kodowania na różne sposoby, w zależności od modelu hello modeli.</span><span class="sxs-lookup"><span data-stu-id="eff85-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="eff85-261">Na przykład Regresja logistyczna i liniowej modele wymagają dynamicznego jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="eff85-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="eff85-262">Na przykład funkcja z trzech kategorii można rozszerzyć do trzech kolumn funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="eff85-263">Każda kolumna może zawierać 0 lub 1 w zależności od kategorii hello obserwacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="eff85-264">MLlib zapewnia hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcja dynamicznego jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="eff85-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="eff85-265">Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="eff85-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="eff85-266">Ten typ kodowania, algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna może być zastosowane toocategorical funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="eff85-267">W tym miejscu możesz przekształcić przykłady tooshow tylko cztery zmienne, które są ciągami znaków.</span><span class="sxs-lookup"><span data-stu-id="eff85-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="eff85-268">Można również indeksu innych zmiennych, takich jak dzień tygodnia, reprezentowany przez wartości liczbowe, jako zmienne podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="eff85-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="eff85-269">Indeksowanie, użyj `StringIndexer()`i hot jeden kodowanie, użyj `OneHotEncoder()` funkcji z MLlib.</span><span class="sxs-lookup"><span data-stu-id="eff85-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="eff85-270">Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="eff85-270">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="eff85-271">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-271">**Output:**</span></span>

<span data-ttu-id="eff85-272">Czas toorun hello komórki: 4 sekundy.</span><span class="sxs-lookup"><span data-stu-id="eff85-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="eff85-273">Przykładowe i podziału hello zestaw danych do ułamków szkoleniowych i testów</span><span class="sxs-lookup"><span data-stu-id="eff85-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="eff85-274">Ten kod tworzy losowej próbki hello danych (w tym przykładzie 25%).</span><span class="sxs-lookup"><span data-stu-id="eff85-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="eff85-275">Próbkowanie nie jest wymagany w tym przykładzie powodu toohello rozmiaru zestawu danych hello, hello artykule opisano, jak można przykładowe, aby wiedzieć, jak toouse go do własnych problemów, gdy jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="eff85-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="eff85-276">W przypadku dużych przykłady to zapisanie długiego czasu podczas uczenia modeli.</span><span class="sxs-lookup"><span data-stu-id="eff85-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="eff85-277">Następnie podzielone próbki hello części szkolenia (75%, w tym przykładzie) i testowania część (25%, w tym przykładzie) toouse w klasyfikacji i regresji modelowania.</span><span class="sxs-lookup"><span data-stu-id="eff85-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="eff85-278">Dodaj liczbę losową (między 0 a 1) tooeach wiersza (w kolumnie "rand") może być złożeń krzyżowego sprawdzania poprawności tooselect używane podczas uczenia.</span><span class="sxs-lookup"><span data-stu-id="eff85-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

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


<span data-ttu-id="eff85-279">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-279">**Output:**</span></span>

<span data-ttu-id="eff85-280">Czas toorun hello komórki: 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="eff85-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="eff85-281">Określ zmienną szkolenia i funkcje, a następnie utwórz indeksowanych lub hot jeden kodowane celów szkoleniowych i testów danych wejściowych z etykietą punktu RDDs lub danych ramki</span><span class="sxs-lookup"><span data-stu-id="eff85-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="eff85-282">Ta sekcja zawiera kod, który pokazuje, jak dane tekstowe podzielone na kategorie tooindex jako etykietą punktu danych typu i kodować je, aby można było ich użyć Regresja logistyczna MLlib tootrain i testowania i inne modele klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="eff85-283">Obiekty etykietą punktu są RDDs sformatowanych w taki sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów w MLlib uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="eff85-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="eff85-284">A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="eff85-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="eff85-285">W tym kodzie określ (zależnych) Zmienna docelowa hello i hello funkcji toouse tootrain modeli.</span><span class="sxs-lookup"><span data-stu-id="eff85-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="eff85-286">Następnie można utworzyć indeksowanych lub hot jeden kodowane celów szkoleniowych i testów z etykietą punktu RDDs lub danych ramek danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

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


<span data-ttu-id="eff85-287">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-287">**Output:**</span></span>

<span data-ttu-id="eff85-288">Czas toorun hello komórki: 4 sekundy.</span><span class="sxs-lookup"><span data-stu-id="eff85-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="eff85-289">Automatycznie klasyfikowanie i vectorize toouse funkcje i obiekty docelowe jako dane wejściowe dla modeli uczenia maszyny</span><span class="sxs-lookup"><span data-stu-id="eff85-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="eff85-290">Użyj Spark ML toocategorize hello docelowych i funkcje toouse w funkcji modelowania oparta na drzewie.</span><span class="sxs-lookup"><span data-stu-id="eff85-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="eff85-291">Kod Hello zakończeniu dwa zadania:</span><span class="sxs-lookup"><span data-stu-id="eff85-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="eff85-292">Tworzy binarne docelowy klasyfikacji, przypisując wartość 0 lub 1 tooeach punkt danych pomiędzy 0 a 1 przy użyciu progu wartości 0,5.</span><span class="sxs-lookup"><span data-stu-id="eff85-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="eff85-293">Automatycznie kategoryzuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-293">Automatically categorizes features.</span></span> <span data-ttu-id="eff85-294">Liczba hello unikatowe wartości liczbowej dla dowolnej funkcji jest mniejsza niż 32, kategoryzowane tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="eff85-295">Oto kod hello te dwa zadania.</span><span class="sxs-lookup"><span data-stu-id="eff85-295">Here's hello code for these two tasks.</span></span>

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="eff85-296">Model klasyfikacji binarnej: prognozowania, czy należy zwrócić porady</span><span class="sxs-lookup"><span data-stu-id="eff85-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="eff85-297">W tej sekcji można tworzyć trzy typy toopredict modele klasyfikacji binarnej Określa, czy należy zwrócić Porada:</span><span class="sxs-lookup"><span data-stu-id="eff85-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="eff85-298">A **modelu Regresja logistyczna** przy użyciu hello Spark ML `LogisticRegression()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="eff85-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="eff85-299">A **model klasyfikacji losowe lasu** przy użyciu hello Spark ML `RandomForestClassifier()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="eff85-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="eff85-300">A **gradientu zwiększania wyniku model klasyfikacji drzewa** przy użyciu hello MLlib `GradientBoostedTrees()` — funkcja</span><span class="sxs-lookup"><span data-stu-id="eff85-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="eff85-301">Tworzenie modelu Regresja logistyczna</span><span class="sxs-lookup"><span data-stu-id="eff85-301">Create a logistic regression model</span></span>
<span data-ttu-id="eff85-302">Następnie utwórz model Regresja logistyczna przy użyciu hello Spark ML `LogisticRegression()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="eff85-303">Można utworzyć modelu hello kompilowania kodu w serii kroków:</span><span class="sxs-lookup"><span data-stu-id="eff85-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="eff85-304">**Train hello model** danych za pomocą jednego zestawu parametrów.</span><span class="sxs-lookup"><span data-stu-id="eff85-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="eff85-305">**Ocena modelu hello** na testowego zestawu danych o metryki.</span><span class="sxs-lookup"><span data-stu-id="eff85-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="eff85-306">**Zapisz hello model** w magazynie obiektów Blob do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="eff85-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="eff85-307">**Wynik hello modelu** względem danych testowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="eff85-308">**Wykreślenia wyniki hello** z odbiornikiem operacyjnego krzywych cechy (ROC).</span><span class="sxs-lookup"><span data-stu-id="eff85-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="eff85-309">Oto kod hello tych procedur:</span><span class="sxs-lookup"><span data-stu-id="eff85-309">Here's hello code for these procedures:</span></span>

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

<span data-ttu-id="eff85-310">Ładowanie, wynik i Zapisz wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-310">Load, score, and save hello results.</span></span>

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


<span data-ttu-id="eff85-311">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-311">**Output:**</span></span>

<span data-ttu-id="eff85-312">ROC na danych testowych = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="eff85-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="eff85-313">W systemie lokalnym krzywą ROC serwera Pandas danych ramki tooplot hello Python.</span><span class="sxs-lookup"><span data-stu-id="eff85-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="eff85-314">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-314">**Output:**</span></span>

![Porada lub nie krzywą ROC Porada](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="eff85-316">Utwórz model klasyfikacji losowe lasu</span><span class="sxs-lookup"><span data-stu-id="eff85-316">Create a random forest classification model</span></span>
<span data-ttu-id="eff85-317">Następnie utwórz model klasyfikacji losowe lasu za pomocą hello Spark ML `RandomForestClassifier()` funkcji, a następnie ocenę hello modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="eff85-318">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-318">**Output:**</span></span>

<span data-ttu-id="eff85-319">ROC na danych testowych = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="eff85-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="eff85-320">Utwórz model klasyfikacji GBT</span><span class="sxs-lookup"><span data-stu-id="eff85-320">Create a GBT classification model</span></span>
<span data-ttu-id="eff85-321">Następnie utwórz model klasyfikacji GBT przy użyciu jego MLlib `GradientBoostedTrees()` funkcji, a następnie ocenę hello modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="eff85-322">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-322">**Output:**</span></span>

<span data-ttu-id="eff85-323">Obszar pod krzywą ROC: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="eff85-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="eff85-324">Model regresji: przewidywanie kwota Porada</span><span class="sxs-lookup"><span data-stu-id="eff85-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="eff85-325">W tej sekcji są tworzone dwa typy kwoty regresji modele toopredict hello Porada:</span><span class="sxs-lookup"><span data-stu-id="eff85-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="eff85-326">A **model regresji liniowej umorzyć** przy użyciu hello Spark ML `LinearRegression()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="eff85-327">Należy zapisać hello model i ocena hello modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="eff85-328">A **zwiększania gradientu drzewa modelu regresji** przy użyciu hello Spark ML `GBTRegressor()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="eff85-329">Tworzenie modelu regresji liniowej umorzyć</span><span class="sxs-lookup"><span data-stu-id="eff85-329">Create a regularized linear regression model</span></span>
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


<span data-ttu-id="eff85-330">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-330">**Output:**</span></span>

<span data-ttu-id="eff85-331">Czas toorun hello komórki: 13 sekund.</span><span class="sxs-lookup"><span data-stu-id="eff85-331">Time toorun hello cell: 13 seconds.</span></span>

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


<span data-ttu-id="eff85-332">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-332">**Output:**</span></span>

<span data-ttu-id="eff85-333">R — sqr na danych testowych = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="eff85-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="eff85-334">Następnie zapytania hello wyników testu jako ramki danych i użyj toovisualize AutoVizWidget i matplotlib go.</span><span class="sxs-lookup"><span data-stu-id="eff85-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="eff85-335">Kod Hello tworzy ramkę danych lokalnych z wyników kwerendy hello i geograficzne hello danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="eff85-336">Witaj `%%local` magic tworzy ramkę dane lokalne `sqlResults`, która za pomocą tooplot matplotlib.</span><span class="sxs-lookup"><span data-stu-id="eff85-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="eff85-337">Ta magic Spark jest używana wiele razy w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="eff85-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="eff85-338">W przypadku dużych hello ilość danych, powinny przykładowe toocreate ramki danych, który można umieścić w pamięci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="eff85-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="eff85-339">Utwórz powierzchni za pomocą matplotlib języka Python.</span><span class="sxs-lookup"><span data-stu-id="eff85-339">Create plots by using Python matplotlib.</span></span>

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

<span data-ttu-id="eff85-340">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-340">**Output:**</span></span>

![Porada kwota: rzeczywiste a przewidywane](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="eff85-342">Tworzenie modelu regresji GBT</span><span class="sxs-lookup"><span data-stu-id="eff85-342">Create a GBT regression model</span></span>
<span data-ttu-id="eff85-343">Tworzenie modelu regresji GBT przy użyciu hello Spark ML `GBTRegressor()` funkcji, a następnie ocenę hello modelu na danych testowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="eff85-344">[Boosted gradientu drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="eff85-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="eff85-345">Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="eff85-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="eff85-346">Można użyć GBTs regresji i klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="eff85-347">One mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i przechwytywać nonlinearities i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="eff85-348">Możesz również można używać ich w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-348">You also can use them in a multiclass-classification setting.</span></span>

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


<span data-ttu-id="eff85-349">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-349">**Output:**</span></span>

<span data-ttu-id="eff85-350">Jest test R-sqr: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="eff85-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="eff85-351">Modelowania zaawansowanych narzędzi do optymalizacji</span><span class="sxs-lookup"><span data-stu-id="eff85-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="eff85-352">W tej sekcji można za pomocą narzędzi learning maszyny, które deweloperzy często używane na potrzeby optymalizacji modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="eff85-353">W szczególności za pomocą parametru kominów i krzyżowego sprawdzania poprawności można zoptymalizować machine learning modeli trzy różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="eff85-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="eff85-354">Podział danych hello na zestawy pociągu i sprawdzania poprawności, zoptymalizować hello modelu za pomocą funkcji hyper parametr kominów na zestaw szkoleniowy i ocenę na zestawie sprawdzania poprawności (regresja liniowa)</span><span class="sxs-lookup"><span data-stu-id="eff85-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="eff85-355">Optymalizacja hello modelu przy użyciu krzyżowego sprawdzania poprawności i funkcji hyper parametru profilach za pomocą funkcji CrossValidator Spark ML (klasyfikacji binarnej)</span><span class="sxs-lookup"><span data-stu-id="eff85-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="eff85-356">Optymalizacja hello modelu przy użyciu niestandardowego kodu krzyżowego sprawdzania poprawności i parametr kominów toouse żadnych machine learning zestaw funkcji i parametr (regresja liniowa)</span><span class="sxs-lookup"><span data-stu-id="eff85-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="eff85-357">**Krzyżowe sprawdzanie poprawności** to technika, który ocenia, jak model ćwiczenie znanego zestawu danych zostanie generalize funkcje hello toopredict zestawów danych, które go nie przeprowadzono uczenia.</span><span class="sxs-lookup"><span data-stu-id="eff85-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="eff85-358">Witaj ogólne ideą ta technika jest czy model jest uczony w zestawie danych znanych danych, a następnie hello dokładność jego prognoz jest testowana niezależnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="eff85-359">Najczęstszą implementacją jest toodivide zestawu danych do *k*-złożeń, a następnie uczenia modelu hello w okrężne na wszystkie oprócz jednego hello złożeń.</span><span class="sxs-lookup"><span data-stu-id="eff85-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="eff85-360">**Optymalizacja parametru Hyper** problem hello wybrać zestaw funkcji hyper-parametrów Algorytm uczenia, zwykle z celem hello optymalizacji miara wydajności algorytm hello na niezależnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="eff85-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="eff85-361">Funkcji hyper parametr to wartość, która należy określić poza procedury szkolenie modelu hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="eff85-362">Założenia dotyczące wartości parametrów funkcji hyper mogą wpływać na powitania elastyczność i dokładność hello modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="eff85-363">Drzewa decyzyjne mieć funkcji hyper parametrów, na przykład takich jak hello potrzeby głębokość i liczby pozostawia w drzewie hello.</span><span class="sxs-lookup"><span data-stu-id="eff85-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="eff85-364">Należy ustawić termin kar błędną klasyfikację maszyny wektorowa obsługa (SVM).</span><span class="sxs-lookup"><span data-stu-id="eff85-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="eff85-365">Typowe optymalizacji hyper parametru tooperform sposób jest toouse wyszukiwanie siatki, nazywany również **odchylenia parametru**.</span><span class="sxs-lookup"><span data-stu-id="eff85-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="eff85-366">W wyszukiwaniu siatki kompleksowe przeszukiwanie odbywa się za pomocą wartości hello określony podzbiór miejsce hyper parametru hello Algorytm uczenia.</span><span class="sxs-lookup"><span data-stu-id="eff85-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="eff85-367">Krzyżowe sprawdzanie poprawności można podać toosort metryki wydajności, limit optymalne hello utworzone przez algorytm wyszukiwania hello siatki.</span><span class="sxs-lookup"><span data-stu-id="eff85-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="eff85-368">Jeśli używasz krzyżowe sprawdzanie poprawności parametru hyper kominów może pomóc limit problemów, takich jak overfitting danych tootraining modelu.</span><span class="sxs-lookup"><span data-stu-id="eff85-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="eff85-369">W ten sposób modelu hello zachowuje hello pojemności tooapply toohello ogólny zestaw danych, z których hello wyodrębniono danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="eff85-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="eff85-370">Optymalizacja model regresji liniowej z kominów hyper parametru</span><span class="sxs-lookup"><span data-stu-id="eff85-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="eff85-371">Następnie podzielenia danych na zestawy pociągu i sprawdzania poprawności, użyj funkcji hyper parametr profilach szkolenia ustawić toooptimize hello modelu i ocenę na zestawie sprawdzania poprawności (regresja liniowa).</span><span class="sxs-lookup"><span data-stu-id="eff85-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

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


<span data-ttu-id="eff85-372">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-372">**Output:**</span></span>

<span data-ttu-id="eff85-373">Jest test R-sqr: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="eff85-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="eff85-374">Optymalizacja hello klasyfikacji binarnej modelu przy użyciu kominów krzyżowego sprawdzania poprawności i parametr hyper</span><span class="sxs-lookup"><span data-stu-id="eff85-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="eff85-375">W tej sekcji przedstawiono, jak toooptimize klasyfikacji binarnej modelu przy użyciu kominów krzyżowego sprawdzania poprawności i parametr hyper.</span><span class="sxs-lookup"><span data-stu-id="eff85-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="eff85-376">Ta metoda korzysta hello Spark ML `CrossValidator` funkcji.</span><span class="sxs-lookup"><span data-stu-id="eff85-376">This uses hello Spark ML `CrossValidator` function.</span></span>

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


<span data-ttu-id="eff85-377">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-377">**Output:**</span></span>

<span data-ttu-id="eff85-378">Czas toorun hello komórki: 33 sekundy.</span><span class="sxs-lookup"><span data-stu-id="eff85-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="eff85-379">Optymalizacja model regresji liniowej hello przy użyciu kodu niestandardowego krzyżowego sprawdzania poprawności i kominów parametru</span><span class="sxs-lookup"><span data-stu-id="eff85-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="eff85-380">Następnie zoptymalizować hello modelu przy użyciu niestandardowego kodu i zidentyfikować hello najlepszych parametrów modelu przy użyciu kryterium hello najwyższy dokładności.</span><span class="sxs-lookup"><span data-stu-id="eff85-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="eff85-381">Następnie utwórz hello ostatecznego modelu, ocena hello modelu na danych testowych i Zapisz hello model w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="eff85-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="eff85-382">Ponadto ładowanie modelu hello, wynik testu danych i oceny dokładności.</span><span class="sxs-lookup"><span data-stu-id="eff85-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

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


<span data-ttu-id="eff85-383">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="eff85-383">**Output:**</span></span>

<span data-ttu-id="eff85-384">Czas toorun hello komórki: 61 sekund.</span><span class="sxs-lookup"><span data-stu-id="eff85-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="eff85-385">Korzystanie z modeli uczenia wbudowane Spark maszyny automatycznie z języka Scala</span><span class="sxs-lookup"><span data-stu-id="eff85-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="eff85-386">Omówienie tematów, które umożliwia przeprowadzenie zadań hello, wchodzące w skład procesu nauki danych hello na platformie Azure, zobacz [proces nauki danych zespołu](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="eff85-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="eff85-387">[Wskazówki dotyczące procesu nauki danych Team](data-science-process-walkthroughs.md) opisano inne end-to-end wskazówki, które pokazują hello etapami hello zespołu w procesie nauki danych w określonych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="eff85-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="eff85-388">wskazówki dotyczące Hello również ilustrują sposób toocombine w chmurze i lokalnie narzędzia i usługi do toocreate przepływu pracy lub potoku inteligentnego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eff85-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="eff85-389">[Wynik modeli uczenia maszynowego wbudowane Spark](machine-learning-data-science-spark-model-consumption.md) pokazano, jak tooautomatically kodu języka Scala toouse obciążenia i wynik nowe zestawy danych przy użyciu modeli uczenia maszynowego wbudowane Spark i zapisane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="eff85-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="eff85-390">Postępuj zgodnie z instrukcjami hello pod warunkiem że i po prostu zastąpić hello kodu Python Scala kodu w tym artykule wykorzystania automatycznych.</span><span class="sxs-lookup"><span data-stu-id="eff85-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

