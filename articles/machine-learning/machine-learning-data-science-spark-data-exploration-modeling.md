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
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="df130-103">Eksplorowanie i modelowanie danych za pomocą platformy Spark</span><span class="sxs-lookup"><span data-stu-id="df130-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="df130-104">W tym przewodniku zastosowano Eksploracja danych toodo Spark w usłudze HDInsight i binarne klasyfikacji i regresji modelowania zadania, na przykład hello NYC taksówki podróży i taryfy 2013 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="df130-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="df130-105">Przeprowadza użytkownika przez kroki hello hello [proces nauki danych](http://aka.ms/datascienceprocess)end-to-end, przy użyciu HDInsight Spark klastra do przetwarzania i modeli danych i hello hello toostore obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="df130-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="df130-106">proces Hello Eksploruje wizualizuje dane pochodzące z obiektu Blob magazynu Azure i następnie przygotowuje toobuild danych hello modeli predykcyjnych.</span><span class="sxs-lookup"><span data-stu-id="df130-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="df130-107">Te modele są kompilowane przy użyciu klasyfikacji binarnej toolkit toodo hello Spark MLlib i regresji modelowania zadania.</span><span class="sxs-lookup"><span data-stu-id="df130-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="df130-108">Witaj **klasyfikacji binarnej** zadanie jest toopredict czy poradę otrzymuje za hello podróży.</span><span class="sxs-lookup"><span data-stu-id="df130-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="df130-109">Witaj **regresji** toopredict hello ilość Porada hello na podstawie innych funkcji Porada jest zadanie.</span><span class="sxs-lookup"><span data-stu-id="df130-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="df130-110">modele Hello, używanych zawierają Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzew:</span><span class="sxs-lookup"><span data-stu-id="df130-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="df130-111">[Regresji liniowej z SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) model regresji liniowej, który używa metody stochastycznego spadku gradientu (SGD) i dla optymalizacji i funkcja skalowania toopredict hello Porada kwoty płatnej.</span><span class="sxs-lookup"><span data-stu-id="df130-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="df130-112">[Regresja logistyczna z LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) lub regresji "logit" to model regresji, który może być używana podczas hello zależnych od zmiennej jest podzielone na kategorie toodo klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="df130-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="df130-113">LBFGS to algorytm optymalizacji quasi Newton — która przybliża hello algorytmu Broyden — Fletcher — Goldfarb — Shanno (BFGS) przy użyciu ograniczoną ilość pamięci komputera i który jest powszechnie używany w uczeniu maszynowym.</span><span class="sxs-lookup"><span data-stu-id="df130-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="df130-114">[Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="df130-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="df130-115">Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting.</span><span class="sxs-lookup"><span data-stu-id="df130-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="df130-116">Losowe lasach są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie i można ją rozszerzyć toohello wieloklasowej klasyfikacji ustawienie.</span><span class="sxs-lookup"><span data-stu-id="df130-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="df130-117">Nie wymagają funkcji skalowania i czy można toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="df130-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="df130-118">Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="df130-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="df130-119">[Gradient boosted drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="df130-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="df130-120">Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="df130-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="df130-121">GBTs są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="df130-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="df130-122">Ich można również w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="df130-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="df130-123">kroki modelowania Hello również zawierać kod, przedstawiający sposób tootrain, oceny i zapisać każdego typu modelu.</span><span class="sxs-lookup"><span data-stu-id="df130-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="df130-124">Python została toocode używane hello rozwiązanie i tooshow hello odpowiednich powierzchni.</span><span class="sxs-lookup"><span data-stu-id="df130-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="df130-125">Toolkit Spark MLlib hello jest zaprojektowana toowork na dużych zestawów danych, przykładowe stosunkowo mały (~ 30 Mb przy użyciu 170K wierszy, około 0,1% hello oryginalnego NYC zestawu danych) jest używany tutaj dla wygody.</span><span class="sxs-lookup"><span data-stu-id="df130-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="df130-126">Ćwiczenie Hello podane tutaj działa wydajnie (w około 10 minut) w klastrze usługi HDInsight z 2 węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="df130-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="df130-127">Witaj tego samego kodu, z drobne zmiany, może być używane tooprocess większych-zestawów danych z odpowiednie modyfikacje dla buforowania danych w pamięci i zmianę rozmiaru klastra hello.</span><span class="sxs-lookup"><span data-stu-id="df130-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="df130-128">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="df130-128">Prerequisites</span></span>
<span data-ttu-id="df130-129">Potrzebujesz konta platformy Azure i Spark 1.6 (lub Spark 2.0) klastra usługi HDInsight toocomplete tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="df130-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="df130-130">Zobacz hello [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) instrukcje na temat toosatisfy tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="df130-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="df130-131">Ten temat zawiera również opis hello taksówki 2013 NYC danych używany w tym miejscu i instrukcje dotyczące sposobu tooexecute kodu z notesu Jupyter w klastrze Spark hello.</span><span class="sxs-lookup"><span data-stu-id="df130-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="df130-132">Klastry Spark i notebooki</span><span class="sxs-lookup"><span data-stu-id="df130-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="df130-133">Kroki instalacji i kodu są dostępne w tym przewodniku dla przy użyciu wersji 1.6 HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="df130-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="df130-134">Ale notesów Jupyter znajdują się w przypadku klastrów HDInsight Spark 1.6 jak Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="df130-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="df130-135">Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je.</span><span class="sxs-lookup"><span data-stu-id="df130-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="df130-136">Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="df130-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="df130-137">Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="df130-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="df130-138">Dla wygody Oto łącza hello notesów Jupyter toohello 1.6 Spark (Uruchom jądra pySpark hello z powitania serwera notesu Jupyter toobe) i 2.0 Spark (Uruchom jądra pySpark3 hello z powitania serwera notesu Jupyter toobe):</span><span class="sxs-lookup"><span data-stu-id="df130-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="df130-139">Notesów Spark w wersji 1.6</span><span class="sxs-lookup"><span data-stu-id="df130-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="df130-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): zawiera informacje na temat Eksploracja danych tooperform, modelowania i oceniania z kilku różnych algorytmów.</span><span class="sxs-lookup"><span data-stu-id="df130-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="df130-141">Notesów Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="df130-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="df130-142">zadania regresji i klasyfikacji Hello, które są implementowane przy użyciu klastra Spark 2.0 znajdują się w oddzielnych notesów i notesu klasyfikacji hello korzysta z innego zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="df130-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="df130-143">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ten plik zawiera informacje dotyczące sposobu tooperform Eksploracja danych, modelowania i oceniania w Spark 2.0 klastrów za pomocą hello taksówki NYC podróży i zestaw danych taryfy opisane [tutaj](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="df130-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="df130-144">Ten notes może być dobry punkt wyjścia do eksplorowania szybko hello kodu, który firma Microsoft umieściła 2.0 Spark.</span><span class="sxs-lookup"><span data-stu-id="df130-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="df130-145">Dla bardziej szczegółowe notesu analizuje hello taksówki NYC danych, zobacz hello notesu dalej na tej liście.</span><span class="sxs-lookup"><span data-stu-id="df130-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="df130-146">Zobacz uwagi hello końcu tej listy, pozwalające porównać te komputery przenośne.</span><span class="sxs-lookup"><span data-stu-id="df130-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="df130-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello taksówki NYC podróży i taryfy zestawu danych opisane [ w tym miejscu](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="df130-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="df130-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello dobrze znanego linii lotniczych na czas wyjścia zestaw danych z 2011 i 2012.</span><span class="sxs-lookup"><span data-stu-id="df130-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="df130-149">Dataset linii lotniczych hello firma Microsoft zintegrowane z hello lotnisku pogody danych (np. prędkość wiatru, temperatury, wysokość itp.) przed toomodeling, więc te funkcje pogody można dołączyć do modelu hello.</span><span class="sxs-lookup"><span data-stu-id="df130-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="df130-150">zestaw danych linii lotniczych Hello dodano notesów toohello Spark 2.0 toobetter ilustrują hello użyciem algorytmów klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="df130-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="df130-151">Zobacz następujące linki do informacji na temat zestawu danych na czas wyjścia linii lotniczych i dataset pogody hello:</span><span class="sxs-lookup"><span data-stu-id="df130-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="df130-152">Dane na czas wyjścia linii lotniczych: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="df130-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="df130-153">Dane pogody lotnisku: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="df130-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="df130-154">Notesy Spark 2.0 Hello na powitania taksówki NYC i linii lotniczych transmitowane opóźnienie-zestawów danych może potrwać 10 minut lub więcej toorun (w zależności od wielkości hello klastra HDI).</span><span class="sxs-lookup"><span data-stu-id="df130-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="df130-155">Witaj pierwszego notesu w hello powyżej listy zawiera wiele aspektów hello Eksploracja danych, wizualizacji i ML modelu szkolenia w notesie pobierającej toorun mniej czasu z próbkowany dół NYC zestaw danych, w których hello taksówkami i taryfy pliki zostały wstępnie przyłączone do: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) tego notesu zajmuje dużo krótszy czas toofinish (2 – 3 min) i może być bardzo punkt początkowy dla szybko Eksploracja kodu hello mamy podany dla Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="df130-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="df130-156">Poniższe opisy Hello są powiązane toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="df130-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="df130-157">W wersjach Spark 2.0 Użyj notesów hello opisane i linki umieszczono powyżej.</span><span class="sxs-lookup"><span data-stu-id="df130-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="df130-158">Instalator: lokalizacji przechowywania, biblioteki i hello ustawienia wstępnego Spark kontekstu</span><span class="sxs-lookup"><span data-stu-id="df130-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="df130-159">Platforma Spark jest możliwe tooAzure tooread i zapisu obiektu Blob magazynu (znanej także jako WASB).</span><span class="sxs-lookup"><span data-stu-id="df130-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="df130-160">Tak żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i hello powoduje WASB przechowywane ponownie.</span><span class="sxs-lookup"><span data-stu-id="df130-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="df130-161">modele toosave lub pliki w WASB hello ścieżka musi toobe prawidłowo określone.</span><span class="sxs-lookup"><span data-stu-id="df130-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="df130-162">Witaj klastra Spark toohello dołączony kontenera domyślnego można odwoływać się przy użyciu ścieżki rozpoczynającej się od: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="df130-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="df130-163">Odwołuje się inne lokalizacje "wasb: / /".</span><span class="sxs-lookup"><span data-stu-id="df130-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="df130-164">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB</span><span class="sxs-lookup"><span data-stu-id="df130-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="df130-165">Hello poniższy przykład kodu określa hello lokalizację hello toobe danych do odczytu i zapisaniu ścieżki hello hello modelu magazynu katalogu toowhich hello modelu danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="df130-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="df130-166">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="df130-166">Import libraries</span></span>
<span data-ttu-id="df130-167">Konfigurowanie wymaga również importowanie wymagane biblioteki.</span><span class="sxs-lookup"><span data-stu-id="df130-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="df130-168">Ustaw kontekst spark i zaimportuj wymagane biblioteki z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="df130-168">Set spark context and import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="df130-169">Wstępnie zdefiniowane kontekstu Spark i poleceń magicznych PySpark</span><span class="sxs-lookup"><span data-stu-id="df130-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="df130-170">Hello jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu.</span><span class="sxs-lookup"><span data-stu-id="df130-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="df130-171">Dlatego nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacją hello, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="df130-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="df130-172">Konteksty te są dostępne dla Ciebie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="df130-172">These contexts are available for you by default.</span></span> <span data-ttu-id="df130-173">Konteksty te są:</span><span class="sxs-lookup"><span data-stu-id="df130-173">These contexts are:</span></span>

* <span data-ttu-id="df130-174">sc - platformy Spark</span><span class="sxs-lookup"><span data-stu-id="df130-174">sc - for Spark</span></span> 
* <span data-ttu-id="df130-175">Element sqlContext - gałęzi</span><span class="sxs-lookup"><span data-stu-id="df130-175">sqlContext - for Hive</span></span>

<span data-ttu-id="df130-176">Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%.</span><span class="sxs-lookup"><span data-stu-id="df130-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="df130-177">Istnieją dwa polecenia, które są używane w tych przykładach kodu.</span><span class="sxs-lookup"><span data-stu-id="df130-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="df130-178">**%% lokalnego** Określa, że kod hello w kolejnych wierszy jest toobe wykonywane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="df130-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="df130-179">Kod musi być prawidłowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="df130-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="df130-180">**%% sql -o <variable name>**  wykonuje zapytanie Hive względem element sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="df130-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="df130-181">Jeśli parametr -o hello jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="df130-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="df130-182">Dla więcej informacji na temat jądra hello notesów Jupyter i hello wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="df130-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="df130-183">Wprowadzanie danych z obiektu blob publiczny</span><span class="sxs-lookup"><span data-stu-id="df130-183">Data ingestion from public blob</span></span>
<span data-ttu-id="df130-184">pierwszym krokiem w procesie nauki hello danych Hello jest toobe danych hello tooingest przeanalizowane ze źródeł gdzie jest znajduje się w środowisku eksploracji i modelowanie danych.</span><span class="sxs-lookup"><span data-stu-id="df130-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="df130-185">środowisko Hello jest Spark, w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="df130-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="df130-186">Ta sekcja zawiera toocomplete kodu hello sekwencję zadań:</span><span class="sxs-lookup"><span data-stu-id="df130-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="df130-187">pozyskiwania toobe przykładowych danych hello modelowane</span><span class="sxs-lookup"><span data-stu-id="df130-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="df130-188">Przeczytaj hello danych wejściowych (przechowywane jako plik .tsv)</span><span class="sxs-lookup"><span data-stu-id="df130-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="df130-189">Format i dane hello czyste</span><span class="sxs-lookup"><span data-stu-id="df130-189">format and clean hello data</span></span>
* <span data-ttu-id="df130-190">Tworzenie i buforowania obiektów (RDDs lub ramek danych) w pamięci</span><span class="sxs-lookup"><span data-stu-id="df130-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="df130-191">Zarejestruj go w postaci tabeli tymczasowej w kontekście SQL.</span><span class="sxs-lookup"><span data-stu-id="df130-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="df130-192">Oto kod hello wprowadzanie danych.</span><span class="sxs-lookup"><span data-stu-id="df130-192">Here is hello code for data ingestion.</span></span>

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

<span data-ttu-id="df130-193">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-193">**OUTPUT:**</span></span>

<span data-ttu-id="df130-194">Czas trwania tooexecute nad komórką: 51.72 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="df130-195">Eksploracja danych i wizualizacji</span><span class="sxs-lookup"><span data-stu-id="df130-195">Data exploration & visualization</span></span>
<span data-ttu-id="df130-196">Po wprowadzeniu danych hello w Spark, hello następnego kroku w procesie nauki danych hello jest lepiej zrozumieć toogain hello danych za pośrednictwem eksploracji i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="df130-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="df130-197">W tej sekcji omówione hello taksówki danych przy użyciu zapytania SQL oraz kreślenia hello docelowych zmiennych i potencjalnego funkcji inspekcji visual.</span><span class="sxs-lookup"><span data-stu-id="df130-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="df130-198">W szczególności firma Microsoft wykreślenia hello częstotliwość liczby osób w podróży taksówki, częstotliwość hello kwot Porada i jak porady różnią się zależnie od ilości płatności i typu.</span><span class="sxs-lookup"><span data-stu-id="df130-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="df130-199">Histogram częstotliwości liczba osób w próbce hello taksówki rund do wykreślenia</span><span class="sxs-lookup"><span data-stu-id="df130-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="df130-200">Ten kod i kolejne wstawki Użyj przykładowe hello magic tooquery SQL i tooplot magic lokalne powitania danych.</span><span class="sxs-lookup"><span data-stu-id="df130-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="df130-201">**Magiczna SQL (`%%sql`)** hello jądra HDInsight PySpark obsługuje łatwe wbudowanego HiveQL zapytań dotyczących element sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="df130-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="df130-202">Witaj (-o nazwa_zmiennej) argument będzie się powtarzał hello wyników kwerendy SQL hello jako DataFrame Pandas na powitania serwera Jupyter.</span><span class="sxs-lookup"><span data-stu-id="df130-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="df130-203">Oznacza to, że jest on dostępny w trybie lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="df130-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="df130-204">Witaj  **`%%local` magic** jest używany kod toorun lokalnie na powitania Jupyter serwera, który jest headnode hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df130-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="df130-205">Zazwyczaj `%%local` magic w połączeniu z hello `%%sql` magic z parametrem -o.</span><span class="sxs-lookup"><span data-stu-id="df130-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="df130-206">parametru -o Hello czy utrwalić danych wyjściowych hello hello zapytania SQL lokalnie, a następnie %% magic lokalnego spowoduje wywołanie hello dalej zbiór toorun fragment kodu lokalnie przed hello dane wyjściowe zapytań SQL hello jest utrwalonego lokalnie</span><span class="sxs-lookup"><span data-stu-id="df130-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="df130-207">Po uruchomieniu kodu hello automatyczna wizualizacja Hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="df130-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="df130-208">To zapytanie pobiera rund hello według liczby osób.</span><span class="sxs-lookup"><span data-stu-id="df130-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="df130-209">Ten kod tworzy lokalne ramki danych z wyników kwerendy hello i geograficzne hello danych.</span><span class="sxs-lookup"><span data-stu-id="df130-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="df130-210">Witaj `%%local` magic tworzy lokalne ramki danych, `sqlResults`, które mogą służyć do kreślenia z matplotlib.</span><span class="sxs-lookup"><span data-stu-id="df130-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="df130-211">Ta magic PySpark jest używana wiele razy w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="df130-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="df130-212">W przypadku dużych hello ilość danych, należy przykładowe toocreate danych ramki, który można umieścić w lokalnej pamięci.</span><span class="sxs-lookup"><span data-stu-id="df130-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="df130-213">Oto hello kodu tooplot hello rund przez pasażerów liczby</span><span class="sxs-lookup"><span data-stu-id="df130-213">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="df130-214">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-214">**OUTPUT:**</span></span>

![Częstotliwość podróży według liczby osób](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="df130-216">Można dokonać wyboru spośród kilku różnych typów wizualizacji (tabeli, kołowego, wiersz, obszar lub pasek) przy użyciu hello **typu** przycisków menu w notesie hello.</span><span class="sxs-lookup"><span data-stu-id="df130-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="df130-217">Wykres słupkowy Hello jest wyświetlany w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="df130-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="df130-218">Wykreślenia histogram kwot porady i jak kwota Porada jest zależna od ilości taryfy i liczba osób.</span><span class="sxs-lookup"><span data-stu-id="df130-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="df130-219">Użyj danych toosample zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="df130-219">Use a SQL query toosample data.</span></span>

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


<span data-ttu-id="df130-220">Ta komórka kod używa hello SQL kwerendy toocreate trzy powierzchni hello danych.</span><span class="sxs-lookup"><span data-stu-id="df130-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

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


<span data-ttu-id="df130-221">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-221">**OUTPUT:**</span></span> 

![Porada kwota dystrybucji](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Porada kwota kwotę Taryfy](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="df130-225">Funkcja przygotowanie zespołu inżynieryjnego, przekształcania i danych do modelowania</span><span class="sxs-lookup"><span data-stu-id="df130-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="df130-226">Tej części opisano i przedstawiono hello kod dla procedur używanych tooprepare danych do użycia w ML modelowania.</span><span class="sxs-lookup"><span data-stu-id="df130-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="df130-227">Widoczny jest sposób hello toodo następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="df130-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="df130-228">Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu</span><span class="sxs-lookup"><span data-stu-id="df130-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="df130-229">Indeks i kodowania funkcji podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="df130-229">Index and encode categorical features</span></span>
* <span data-ttu-id="df130-230">Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML</span><span class="sxs-lookup"><span data-stu-id="df130-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="df130-231">Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów</span><span class="sxs-lookup"><span data-stu-id="df130-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="df130-232">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="df130-232">Feature scaling</span></span>
* <span data-ttu-id="df130-233">Obiektów w pamięci podręcznej w pamięci</span><span class="sxs-lookup"><span data-stu-id="df130-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="df130-234">Utwórz nową funkcję o binning godziny do ruchu przedziałów czasu</span><span class="sxs-lookup"><span data-stu-id="df130-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="df130-235">Ten kod przedstawia sposób pakiety ramach Agreement toocreate nowa funkcja przez binning godzin w czasie ruchu, a następnie jak toocache hello wynikowe ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="df130-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="df130-236">W przypadku, gdy odporność rozproszonych zestawów danych (RDDs) i ramek danych są używane wielokrotnie, buforowanie prowadzi tooimproved czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="df130-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="df130-237">W związku z tym możemy pamięci podręcznej RDDs i ramek danych w kilku etapach hello wskazówki.</span><span class="sxs-lookup"><span data-stu-id="df130-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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

<span data-ttu-id="df130-238">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-238">**OUTPUT:**</span></span> 

<span data-ttu-id="df130-239">126050</span><span class="sxs-lookup"><span data-stu-id="df130-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="df130-240">Indeks i kodowania podzielone na kategorie funkcje dla danych wejściowych do modelowania funkcji</span><span class="sxs-lookup"><span data-stu-id="df130-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="df130-241">W tej sekcji przedstawiono sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="df130-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="df130-242">Witaj modelowania i prognozowania wymagają funkcji MLlib z toobe podzielone na kategorie danych wejściowych funkcji zakodowany wcześniejsze toouse lub indeksowany.</span><span class="sxs-lookup"><span data-stu-id="df130-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="df130-243">W zależności od modelu hello muszą tooindex lub zakodować je na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="df130-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="df130-244">**Oparta na drzewie modelowania** wymaga toobe kategorii zakodowane jako wartości liczbowe (na przykład funkcja z trzech kategorii może być zakodowane za pomocą 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="df130-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="df130-245">To są dostarczane przez firmy MLlib [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) funkcji.</span><span class="sxs-lookup"><span data-stu-id="df130-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="df130-246">Ta funkcja koduje kolumny ciąg etykiety tooa kolumny indeksów etykiety, uporządkowanych według częstotliwości etykiety.</span><span class="sxs-lookup"><span data-stu-id="df130-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="df130-247">Mimo że zaindeksowane wartości liczbowe wprowadzania i obsługi danych, algorytmy oparta na drzewie hello może być określony tootreat ich odpowiednio jako kategorie.</span><span class="sxs-lookup"><span data-stu-id="df130-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="df130-248">**Modele logistyczna i regresji liniowej** wymagają dynamicznego jeden kodowania, where, na przykład funkcja z trzech kategorii można rozszerzyć do trzy kolumny funkcji, z każdym zawierających 0 lub 1 w zależności od kategorii hello obserwacji.</span><span class="sxs-lookup"><span data-stu-id="df130-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="df130-249">Udostępnia MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcji toodo hot jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="df130-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="df130-250">Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="df130-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="df130-251">Ten typ kodowania umożliwia algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.</span><span class="sxs-lookup"><span data-stu-id="df130-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="df130-252">Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="df130-252">Here is hello code tooindex and encode categorical features:</span></span>

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

<span data-ttu-id="df130-253">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-253">**OUTPUT:**</span></span>

<span data-ttu-id="df130-254">Czas trwania tooexecute nad komórką: 1,28 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="df130-255">Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML</span><span class="sxs-lookup"><span data-stu-id="df130-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="df130-256">Ta sekcja zawiera kod, wpisz i kodować je, dzięki czemu może być używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji danych tekstowych podzielone na kategorie tooindex jako etykietą punktu danych.</span><span class="sxs-lookup"><span data-stu-id="df130-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="df130-257">Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) sformatowany w sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów uczenia Maszynowego w MLlib.</span><span class="sxs-lookup"><span data-stu-id="df130-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="df130-258">A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="df130-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="df130-259">Ta sekcja zawiera kod, który pokazuje jak dane tekstowe podzielone na kategorie tooindex jako [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) typ danych i kodować je, dzięki czemu może być używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="df130-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="df130-260">Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) składające się z etykiety (docelowy/odpowiedzi zmienna) i funkcja wektora.</span><span class="sxs-lookup"><span data-stu-id="df130-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="df130-261">Ten format jest potrzebny jako dane wejściowe wiele algorytmów uczenia Maszynowego w MLlib.</span><span class="sxs-lookup"><span data-stu-id="df130-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="df130-262">Oto hello tooindex kodu i kodowania tekstu funkcje klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="df130-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="df130-263">Oto kod hello tooencode i pod indeksem funkcje podzielone na kategorie tekstu do analizy regresji liniowej.</span><span class="sxs-lookup"><span data-stu-id="df130-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="df130-264">Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów</span><span class="sxs-lookup"><span data-stu-id="df130-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="df130-265">Ten kod tworzy losowej próbki hello danych (25% służy w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="df130-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="df130-266">Chociaż nie jest wymagana w tym przykładzie powodu toohello rozmiaru zestawu danych hello, przedstawiony sposób próbkę można pobrać tutaj, aby wiedzieć, jak toouse dla własnego problem w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="df130-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="df130-267">W przypadku dużych przykłady to zapisanie długiego czasu podczas szkolenia modeli.</span><span class="sxs-lookup"><span data-stu-id="df130-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="df130-268">Obok próbki hello możemy podzielić na części szkolenia (w tym miejscu 75%) i testowania toouse część (25% tutaj) w klasyfikacji i regresji modelowania.</span><span class="sxs-lookup"><span data-stu-id="df130-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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

<span data-ttu-id="df130-269">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-269">**OUTPUT:**</span></span>

<span data-ttu-id="df130-270">Czas trwania tooexecute nad komórką: 0,24 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="df130-271">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="df130-271">Feature scaling</span></span>
<span data-ttu-id="df130-272">Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="df130-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="df130-273">Witaj kodu funkcji skalowania używa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello funkcji toounit wariancji.</span><span class="sxs-lookup"><span data-stu-id="df130-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="df130-274">Do użytku w regresji liniowej z stochastycznego gradientu spadku (SGD), popularnych Algorytm uczenia szeroką gamę innych modeli, takie jak umorzyć regresji lub pomocy technicznej wektor maszyny (SVM) uczenia maszynowego są dostarczane przez MLlib.</span><span class="sxs-lookup"><span data-stu-id="df130-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="df130-275">Znaleźliśmy skalowanie hello LinearRegressionWithSGD algorytm toobe toofeature poufnych.</span><span class="sxs-lookup"><span data-stu-id="df130-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="df130-276">Oto hello kodu tooscale zmienne do użytku z hello umorzyć liniowej SGD algorytmu.</span><span class="sxs-lookup"><span data-stu-id="df130-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="df130-277">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-277">**OUTPUT:**</span></span>

<span data-ttu-id="df130-278">Czas trwania tooexecute nad komórką: 13.17 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="df130-279">Obiektów w pamięci podręcznej w pamięci</span><span class="sxs-lookup"><span data-stu-id="df130-279">Cache objects in memory</span></span>
<span data-ttu-id="df130-280">czas powitania dla przez buforowanie obiektów ramki danych wejściowych hello używane do klasyfikacji i regresji, można zmniejszyć uczenie i testowanie algorytmów uczenia Maszynowego i skalowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="df130-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="df130-281">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-281">**OUTPUT:**</span></span> 

<span data-ttu-id="df130-282">Czas trwania tooexecute nad komórką: 0,15 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="df130-283">Przewidywanie, czy z modelami klasyfikacji binarnej otrzymuje porady</span><span class="sxs-lookup"><span data-stu-id="df130-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="df130-284">W tej sekcji przedstawiono sposób użycia trzech modeli dla zadanie klasyfikacji binarnej hello przewidywania czy poradę ma być stosowany w podróży taksówki.</span><span class="sxs-lookup"><span data-stu-id="df130-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="df130-285">modele Hello prezentowane są:</span><span class="sxs-lookup"><span data-stu-id="df130-285">hello models presented are:</span></span>

* <span data-ttu-id="df130-286">Regresja logistyczna umorzyć</span><span class="sxs-lookup"><span data-stu-id="df130-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="df130-287">Model lasu losowych</span><span class="sxs-lookup"><span data-stu-id="df130-287">Random forest model</span></span>
* <span data-ttu-id="df130-288">Gradientu zwiększania wyniku drzewa</span><span class="sxs-lookup"><span data-stu-id="df130-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="df130-289">Każdy model budowania sekcji kodu jest podzielony na kroki:</span><span class="sxs-lookup"><span data-stu-id="df130-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="df130-290">**Model uczenia** danych za pomocą jednego zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="df130-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="df130-291">**Model oceny** na testowego zestawu danych o metryki</span><span class="sxs-lookup"><span data-stu-id="df130-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="df130-292">**Zapisywanie modelu** w obiekcie blob do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="df130-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="df130-293">Regresja logistyczna klasyfikacji</span><span class="sxs-lookup"><span data-stu-id="df130-293">Classification using logistic regression</span></span>
<span data-ttu-id="df130-294">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="df130-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="df130-295">**Uczenie modelu Regresja logistyczna hello przy użyciu CV i kominów hyperparameter**</span><span class="sxs-lookup"><span data-stu-id="df130-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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


<span data-ttu-id="df130-296">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-296">**OUTPUT:**</span></span> 

<span data-ttu-id="df130-297">Współczynniki: [0.0082065285375,-0.0223675576104,-0.0183812028036, - 3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="df130-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="df130-298">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="df130-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="df130-299">Czas trwania tooexecute nad komórką: 14.43 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="df130-300">**Ocena modelu klasyfikacji binarnej hello o standardowych metryki**</span><span class="sxs-lookup"><span data-stu-id="df130-300">**Evaluate hello binary classification model with standard metrics**</span></span>

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

<span data-ttu-id="df130-301">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-301">**OUTPUT:**</span></span> 

<span data-ttu-id="df130-302">Obszarze PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="df130-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="df130-303">Obszarze ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="df130-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="df130-304">Podsumowanie statystyk</span><span class="sxs-lookup"><span data-stu-id="df130-304">Summary Stats</span></span>

<span data-ttu-id="df130-305">Dokładność = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="df130-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="df130-306">Odwołaj = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="df130-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="df130-307">F1 Wynik = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="df130-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="df130-308">Czas trwania tooexecute nad komórką: 57.61 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="df130-309">**Wykreślić krzywą ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="df130-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="df130-310">Witaj *predictionAndLabelsDF* jest zarejestrowany jako tabelę, *tmp_results*, w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="df130-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="df130-311">*tmp_results* można toodo używane zapytania i wyświetlić wyników do hello sqlResults danych ramki do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="df130-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="df130-312">Oto kod hello.</span><span class="sxs-lookup"><span data-stu-id="df130-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="df130-313">Oto hello kodu toomake prognoz i hello kreślenia krzywą ROC.</span><span class="sxs-lookup"><span data-stu-id="df130-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

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


<span data-ttu-id="df130-314">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-314">**OUTPUT:**</span></span>

![Regresja logistyczna ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="df130-316">Klasyfikacja losowe lasu</span><span class="sxs-lookup"><span data-stu-id="df130-316">Random forest classification</span></span>
<span data-ttu-id="df130-317">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i zapisać modelu losowe lasu, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="df130-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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

<span data-ttu-id="df130-318">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-318">**OUTPUT:**</span></span>

<span data-ttu-id="df130-319">Obszarze ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="df130-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="df130-320">Czas trwania tooexecute nad komórką: 31.09 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="df130-321">Gradientu zwiększania wyniku klasyfikacji drzewa.</span><span class="sxs-lookup"><span data-stu-id="df130-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="df130-322">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="df130-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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


<span data-ttu-id="df130-323">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-323">**OUTPUT:**</span></span>

<span data-ttu-id="df130-324">Obszarze ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="df130-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="df130-325">Czas trwania tooexecute nad komórką: 19.76 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="df130-326">Porada kwoty rund taksówki z modelami regresji prognozowania</span><span class="sxs-lookup"><span data-stu-id="df130-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="df130-327">W tej sekcji przedstawiono sposób użycia trzech modeli dla hello regresji zadanie przewidywania hello ilość Porada hello płatnej w podróży taksówki na podstawie innych funkcji poradę.</span><span class="sxs-lookup"><span data-stu-id="df130-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="df130-328">modele Hello prezentowane są:</span><span class="sxs-lookup"><span data-stu-id="df130-328">hello models presented are:</span></span>

* <span data-ttu-id="df130-329">Umorzyć regresji liniowej</span><span class="sxs-lookup"><span data-stu-id="df130-329">Regularized linear regression</span></span>
* <span data-ttu-id="df130-330">Losowe lasu</span><span class="sxs-lookup"><span data-stu-id="df130-330">Random forest</span></span>
* <span data-ttu-id="df130-331">Gradientu zwiększania wyniku drzewa</span><span class="sxs-lookup"><span data-stu-id="df130-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="df130-332">Te modele zostały opisane w hello wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="df130-332">These models were described in hello introduction.</span></span> <span data-ttu-id="df130-333">Każdy model budowania sekcji kodu jest podzielony na kroki:</span><span class="sxs-lookup"><span data-stu-id="df130-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="df130-334">**Model uczenia** danych za pomocą jednego zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="df130-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="df130-335">**Model oceny** na testowego zestawu danych o metryki</span><span class="sxs-lookup"><span data-stu-id="df130-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="df130-336">**Zapisywanie modelu** w obiekcie blob do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="df130-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="df130-337">Regresji liniowej z SGD</span><span class="sxs-lookup"><span data-stu-id="df130-337">Linear regression with SGD</span></span>
<span data-ttu-id="df130-338">Witaj kodu w tej sekcji przedstawiono sposób toouse skalowania tootrain funkcji regresji liniowej używającej stochastycznego spadku gradientu (SGD) dla usługi optymalizacji, oraz sposób tooscore, oceny i Zapisz hello model w usłudze Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="df130-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="df130-339">Wiemy z doświadczenia mogą występować problemy z zbieżności hello LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu.</span><span class="sxs-lookup"><span data-stu-id="df130-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="df130-340">Skalowanie zmiennych znacznie ułatwia zbieżności.</span><span class="sxs-lookup"><span data-stu-id="df130-340">Scaling of variables significantly helps with convergence.</span></span> 
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

<span data-ttu-id="df130-341">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-341">**OUTPUT:**</span></span>

<span data-ttu-id="df130-342">Współczynniki: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,-0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="df130-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="df130-343">Przechwycić: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="df130-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="df130-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="df130-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="df130-345">R sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="df130-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="df130-346">Czas trwania tooexecute nad komórką: 58.42 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="df130-347">Regresja losowe lasu</span><span class="sxs-lookup"><span data-stu-id="df130-347">Random Forest regression</span></span>
<span data-ttu-id="df130-348">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i zapisać regresji losowe lasu, który prognozuje Porada kwota hello NYC taksówki podróży danych.</span><span class="sxs-lookup"><span data-stu-id="df130-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

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

<span data-ttu-id="df130-349">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-349">**OUTPUT:**</span></span>

<span data-ttu-id="df130-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="df130-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="df130-351">R sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="df130-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="df130-352">Czas trwania tooexecute nad komórką: 49.21 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="df130-353">Gradientu zwiększania wyniku regresji drzewa.</span><span class="sxs-lookup"><span data-stu-id="df130-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="df130-354">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który prognozuje Porada kwota hello NYC taksówki podróży danych.</span><span class="sxs-lookup"><span data-stu-id="df130-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="df130-355">** Nauczanie i Ewaluacja **</span><span class="sxs-lookup"><span data-stu-id="df130-355">**Train and evaluate **</span></span>

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

<span data-ttu-id="df130-356">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-356">**OUTPUT:**</span></span>

<span data-ttu-id="df130-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="df130-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="df130-358">R sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="df130-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="df130-359">Czas trwania tooexecute nad komórką: 34.52 sekund</span><span class="sxs-lookup"><span data-stu-id="df130-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="df130-360">**Kreślenia**</span><span class="sxs-lookup"><span data-stu-id="df130-360">**Plot**</span></span>

<span data-ttu-id="df130-361">*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="df130-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="df130-362">Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="df130-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="df130-363">Oto kod hello</span><span class="sxs-lookup"><span data-stu-id="df130-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="df130-364">Oto hello kodu tooplot hello danych przy użyciu hello Jupyter serwera.</span><span class="sxs-lookup"><span data-stu-id="df130-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

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


<span data-ttu-id="df130-365">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="df130-365">**OUTPUT:**</span></span>

![Vs przewidzieć — Porada kwoty rzeczywiste](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="df130-367">Czyszczenie obiektów z pamięci</span><span class="sxs-lookup"><span data-stu-id="df130-367">Clean up objects from memory</span></span>
<span data-ttu-id="df130-368">Użyj `unpersist()` toodelete obiektów w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="df130-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="df130-369">Lokalizacje przechowywania rekordu modeli hello konsumenckich i oceniania</span><span class="sxs-lookup"><span data-stu-id="df130-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="df130-370">tooconsume i wynik niezależne dataset opisane hello [wynik i ocena modeli uczenia maszynowego wbudowane Spark](machine-learning-data-science-spark-model-consumption.md) tematu, należy toocopy i Wklej zawierającego modeli hello zapisane utworzoną tutaj do hello nazw tych plików Zużycie notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="df130-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="df130-371">Oto tooprint kodu hello hello ścieżki toomodel plików, który należy.</span><span class="sxs-lookup"><span data-stu-id="df130-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="df130-372">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="df130-372">**OUTPUT**</span></span>

<span data-ttu-id="df130-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="df130-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="df130-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="df130-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="df130-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="df130-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="df130-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="df130-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="df130-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="df130-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="df130-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="df130-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="df130-379">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="df130-379">What's next?</span></span>
<span data-ttu-id="df130-380">Teraz po utworzeniu modele regresji i klasyfikacji z hello Spark MlLib, wszystko jest gotowe toolearn jak tooscore i oceny tych modeli.</span><span class="sxs-lookup"><span data-stu-id="df130-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="df130-381">Witaj zaawansowane Eksploracja danych i modelowanie dives notesu głębiej w tym krzyżowego sprawdzania poprawności, parametr funkcji hyper profilach i modelu oceny.</span><span class="sxs-lookup"><span data-stu-id="df130-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="df130-382">**Model zużycia:** toolearn jak tooscore i ocenić hello klasyfikacji i regresji modeli utworzonych w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="df130-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="df130-383">**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper</span><span class="sxs-lookup"><span data-stu-id="df130-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

