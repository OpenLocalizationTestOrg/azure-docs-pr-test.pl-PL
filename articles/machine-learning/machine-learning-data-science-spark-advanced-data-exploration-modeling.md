---
title: Eksploracja danych aaaAdvanced i modelowania z Spark | Dokumentacja firmy Microsoft
description: "Eksploracja danych toodo Spark w usłudze HDInsight przy użyciu a uczenia binarne modele klasyfikacji i regresji przy użyciu optymalizacji krzyżowego sprawdzania poprawności i hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="27cb6-103">Zaawansowane eksplorowanie i modelowanie danych za pomocą platformy Spark</span><span class="sxs-lookup"><span data-stu-id="27cb6-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="27cb6-104">W tym przewodniku zastosowano Spark w usłudze HDInsight toodo eksploracji i train binarne klasyfikacji danych i modeli regresji przy użyciu krzyżowego sprawdzania poprawności i optymalizacji hyperparameter na próbkę hello NYC taksówki podróży i taryfy 2013 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="27cb6-105">Przeprowadza użytkownika przez kroki hello hello [proces nauki danych](http://aka.ms/datascienceprocess)end-to-end, przy użyciu HDInsight Spark klastra do przetwarzania i modeli danych i hello hello toostore obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="27cb6-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="27cb6-106">proces Hello Eksploruje wizualizuje dane pochodzące z obiektu Blob magazynu Azure i następnie przygotowuje toobuild danych hello modeli predykcyjnych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="27cb6-107">Python została toocode używane hello rozwiązanie i tooshow hello odpowiednich powierzchni.</span><span class="sxs-lookup"><span data-stu-id="27cb6-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="27cb6-108">Te modele są kompilowane przy użyciu klasyfikacji binarnej toolkit toodo hello Spark MLlib i regresji modelowania zadania.</span><span class="sxs-lookup"><span data-stu-id="27cb6-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="27cb6-109">Witaj **klasyfikacji binarnej** zadanie jest toopredict czy poradę otrzymuje za hello podróży.</span><span class="sxs-lookup"><span data-stu-id="27cb6-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="27cb6-110">Witaj **regresji** toopredict hello ilość Porada hello na podstawie innych funkcji Porada jest zadanie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="27cb6-111">kroki modelowania Hello również zawierać kod, przedstawiający sposób tootrain, oceny i zapisać każdego typu modelu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="27cb6-112">Witaj omówiono także niektóre hello sam tła jako hello [Eksploracja danych i modelowanie z Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="27cb6-113">Ale jego jest bardziej "Zaawansowane" w tym również używa krzyżowego sprawdzania poprawności z hyperparameter profilach tootrain optymalnie dokładne modele klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="27cb6-114">**Krzyżowe sprawdzanie poprawności (CV)** to technika, który ocenia, jak model ćwiczenie znanego zestawu danych stanowi uogólnienie funkcje hello toopredicting zestawów danych, na którym go nie przeprowadzono uczenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="27cb6-115">Najczęstszą implementacją używane w tym miejscu jest toodivide zestawu danych do złożeń K i następnie uczenia modelu hello w okrężne na wszystkie oprócz jednego hello złożeń.</span><span class="sxs-lookup"><span data-stu-id="27cb6-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="27cb6-116">ocenia się możliwość Hello hello modelu tooprediction dokładnie, gdy testowana hello niezależne zestawu danych, w tym modelu hello tootrain składanie nie są używane.</span><span class="sxs-lookup"><span data-stu-id="27cb6-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="27cb6-117">**Optymalizacja Hyperparameter** problem hello wybrać zestaw hyperparameters dla Algorytm uczenia, zwykle z celem hello optymalizacji miara wydajności algorytm hello na niezależnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="27cb6-118">**Hyperparameters** to wartości, które należy określić poza procedury szkolenie modelu hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="27cb6-119">Założenia dotyczące tych wartości może wpłynąć na powitania elastyczność i dokładność hello modeli.</span><span class="sxs-lookup"><span data-stu-id="27cb6-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="27cb6-120">Drzewa decyzyjne ma hyperparameters, na przykład, takie jak hello potrzeby głębokość i liczby pozostawia hello drzewa.</span><span class="sxs-lookup"><span data-stu-id="27cb6-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="27cb6-121">Obsługa wektor maszyny (SVMs) wymagają, aby ustawienie terminu kar błędną klasyfikację.</span><span class="sxs-lookup"><span data-stu-id="27cb6-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="27cb6-122">Typowe sposób tooperform hyperparameter optymalizacją używane w tym miejscu jest wyszukiwanie siatki, lub **odchylenia parametru**.</span><span class="sxs-lookup"><span data-stu-id="27cb6-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="27cb6-123">Składa się z wykonuje kompleksowe przeszukiwanie za pomocą wartości hello określony podzbiór hello hyperparameter miejsca dla algorytmu uczenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="27cb6-124">Krzyżowego sprawdzania poprawności można podać toosort metryki wydajności, limit optymalne hello utworzone przez algorytm wyszukiwania hello siatki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="27cb6-125">Używane z szerokimi pomaga limit problemów, takich jak overfitting danych tootraining modelu, dzięki czemu hello modelu zachowuje hello pojemności tooapply toohello ogólny zestaw danych, z których hello dane szkoleniowe został wyodrębniony hyperparameter CV.</span><span class="sxs-lookup"><span data-stu-id="27cb6-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="27cb6-126">modele Hello, używanych zawierają Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzew:</span><span class="sxs-lookup"><span data-stu-id="27cb6-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="27cb6-127">[Regresji liniowej z SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) model regresji liniowej, który używa metody stochastycznego spadku gradientu (SGD) i dla optymalizacji i funkcja skalowania toopredict hello Porada kwoty płatnej.</span><span class="sxs-lookup"><span data-stu-id="27cb6-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="27cb6-128">[Regresja logistyczna z LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) lub regresji "logit" to model regresji, który może być używana podczas hello zależnych od zmiennej jest podzielone na kategorie toodo klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="27cb6-129">LBFGS to algorytm optymalizacji quasi Newton — która przybliża hello algorytmu Broyden — Fletcher — Goldfarb — Shanno (BFGS) przy użyciu ograniczoną ilość pamięci komputera i który jest powszechnie używany w uczeniu maszynowym.</span><span class="sxs-lookup"><span data-stu-id="27cb6-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="27cb6-130">[Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="27cb6-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="27cb6-131">Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting.</span><span class="sxs-lookup"><span data-stu-id="27cb6-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="27cb6-132">Losowe lasach są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie i można ją rozszerzyć toohello wieloklasowej klasyfikacji ustawienie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="27cb6-133">Nie wymagają funkcji skalowania i czy można toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="27cb6-134">Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="27cb6-135">[Gradient boosted drzew](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="27cb6-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="27cb6-136">Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="27cb6-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="27cb6-137">GBTs są używane do regresji i klasyfikacji i może obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="27cb6-138">Ich można również w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="27cb6-139">Modelowanie przykłady użycia CV i Hyperparameter przedstawiono odchylenia hello problemu klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="27cb6-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="27cb6-140">Przykłady prostsze (bez parametru przeszukiwanie) są prezentowane w hello tematem głównym zadań regresji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="27cb6-141">Jednak w dodatku hello, również są przedstawione Weryfikacja za pomocą elastycznych net regresji liniowej i CV z parametru odchylenia przy użyciu regresji losowe lasu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="27cb6-142">Witaj **elastyczna net** jest metoda umorzyć regresji dla dopasowanie regresji liniowej modeli liniowo łączy hello P1 i P2 metryk jako kary hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) i [pierścieniem](https://en.wikipedia.org/wiki/Tikhonov_regularization) metody.</span><span class="sxs-lookup"><span data-stu-id="27cb6-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="27cb6-143">Toolkit Spark MLlib hello jest zaprojektowana toowork na dużych zestawów danych, przykładowe stosunkowo mały (~ 30 Mb przy użyciu 170K wierszy, około 0,1% hello oryginalnego NYC zestawu danych) jest używany tutaj dla wygody.</span><span class="sxs-lookup"><span data-stu-id="27cb6-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="27cb6-144">Ćwiczenie Hello podane tutaj działa wydajnie (w około 10 minut) w klastrze usługi HDInsight z 2 węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="27cb6-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="27cb6-145">Witaj tego samego kodu, z drobne zmiany, może być używane tooprocess większych-zestawów danych z odpowiednie modyfikacje dla buforowania danych w pamięci i zmianę rozmiaru klastra hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="27cb6-146">Instalatora: Klastry Spark i notebooki</span><span class="sxs-lookup"><span data-stu-id="27cb6-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="27cb6-147">Kroki instalacji i kodu są dostępne w tym przewodniku dla przy użyciu wersji 1.6 HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="27cb6-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="27cb6-148">Ale notesów Jupyter znajdują się w przypadku klastrów HDInsight Spark 1.6 jak Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="27cb6-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="27cb6-149">Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je.</span><span class="sxs-lookup"><span data-stu-id="27cb6-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="27cb6-150">Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="27cb6-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="27cb6-151">Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="27cb6-152">Dla wygody Oto notesów Jupyter toohello łącza hello Spark 1.6 i 2.0 toobe Uruchom jądra pyspark hello z hello notesu Jupyter serwera:</span><span class="sxs-lookup"><span data-stu-id="27cb6-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="27cb6-153">Notesów Spark w wersji 1.6</span><span class="sxs-lookup"><span data-stu-id="27cb6-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="27cb6-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): zawiera tematy w notesie #1 i tworzenia modelu przy użyciu hyperparameter dostrajanie i krzyżowego sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="27cb6-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="27cb6-155">Notesów Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="27cb6-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="27cb6-156">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ten plik zawiera informacje dotyczące sposobu tooperform Eksploracja danych, modelowania i oceniania w Spark 2.0 klastrów.</span><span class="sxs-lookup"><span data-stu-id="27cb6-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="27cb6-157">Instalator: lokalizacji przechowywania, biblioteki i hello ustawienia wstępnego Spark kontekstu</span><span class="sxs-lookup"><span data-stu-id="27cb6-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="27cb6-158">Platforma Spark jest możliwe tooAzure tooread i zapisu obiektu Blob magazynu (znanej także jako WASB).</span><span class="sxs-lookup"><span data-stu-id="27cb6-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="27cb6-159">Tak żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i hello powoduje WASB przechowywane ponownie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="27cb6-160">modele toosave lub pliki w WASB hello ścieżka musi toobe prawidłowo określone.</span><span class="sxs-lookup"><span data-stu-id="27cb6-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="27cb6-161">Witaj klastra Spark toohello dołączony kontenera domyślnego można odwoływać się przy użyciu ścieżki rozpoczynającej się od: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="27cb6-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="27cb6-162">Odwołuje się inne lokalizacje "wasb: / /".</span><span class="sxs-lookup"><span data-stu-id="27cb6-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="27cb6-163">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB</span><span class="sxs-lookup"><span data-stu-id="27cb6-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="27cb6-164">Hello poniższy przykład kodu określa hello lokalizację hello toobe danych do odczytu i zapisaniu ścieżki hello hello modelu magazynu katalogu toowhich hello modelu danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="27cb6-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="27cb6-165">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-165">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-166">DateTime.DateTime (2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="27cb6-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="27cb6-167">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="27cb6-167">Import libraries</span></span>
<span data-ttu-id="27cb6-168">Importuj biblioteki niezbędne z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="27cb6-168">Import necessary libraries with hello following code:</span></span>

    # LOAD PYSPARK LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="27cb6-169">Wstępnie zdefiniowane kontekstu Spark i poleceń magicznych PySpark</span><span class="sxs-lookup"><span data-stu-id="27cb6-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="27cb6-170">Hello jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="27cb6-171">Dlatego nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacją hello, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="27cb6-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="27cb6-172">Konteksty te są dostępne dla Ciebie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-172">These contexts are available for you by default.</span></span> <span data-ttu-id="27cb6-173">Konteksty te są:</span><span class="sxs-lookup"><span data-stu-id="27cb6-173">These contexts are:</span></span>

* <span data-ttu-id="27cb6-174">sc - platformy Spark</span><span class="sxs-lookup"><span data-stu-id="27cb6-174">sc - for Spark</span></span> 
* <span data-ttu-id="27cb6-175">Element sqlContext - gałęzi</span><span class="sxs-lookup"><span data-stu-id="27cb6-175">sqlContext - for Hive</span></span>

<span data-ttu-id="27cb6-176">Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%.</span><span class="sxs-lookup"><span data-stu-id="27cb6-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="27cb6-177">Istnieją dwa polecenia, które są używane w tych przykładach kodu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="27cb6-178">**%% lokalnego** Określa, że kod hello w kolejnych wierszy jest toobe wykonywane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="27cb6-179">Kod musi być prawidłowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="27cb6-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="27cb6-180">**%% sql -o <variable name>**  wykonuje zapytanie Hive względem element sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="27cb6-181">Jeśli parametr -o hello jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="27cb6-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="27cb6-182">Dla więcej informacji na temat jądra hello notesów Jupyter i hello wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="27cb6-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="27cb6-183">Wprowadzanie danych z publicznego obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="27cb6-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="27cb6-184">Witaj pierwszym krokiem w procesie nauki danych hello jest toobe danych hello tooingest przeanalizowane ze źródeł, w którym znajduje się on w środowisku eksploracji i modelowanie danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="27cb6-185">To środowisko jest Spark, w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="27cb6-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="27cb6-186">Ta sekcja zawiera toocomplete kodu hello sekwencję zadań:</span><span class="sxs-lookup"><span data-stu-id="27cb6-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="27cb6-187">pozyskiwania toobe przykładowych danych hello modelowane</span><span class="sxs-lookup"><span data-stu-id="27cb6-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="27cb6-188">Przeczytaj hello danych wejściowych (przechowywane jako plik .tsv)</span><span class="sxs-lookup"><span data-stu-id="27cb6-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="27cb6-189">Format i dane hello czyste</span><span class="sxs-lookup"><span data-stu-id="27cb6-189">format and clean hello data</span></span>
* <span data-ttu-id="27cb6-190">Tworzenie i buforowania obiektów (RDDs lub ramek danych) w pamięci</span><span class="sxs-lookup"><span data-stu-id="27cb6-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="27cb6-191">Zarejestruj go w postaci tabeli tymczasowej w kontekście SQL.</span><span class="sxs-lookup"><span data-stu-id="27cb6-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="27cb6-192">Oto kod hello wprowadzanie danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-192">Here is hello code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-193">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-193">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-194">Czas trwania tooexecute nad komórką: 276.62 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="27cb6-195">Eksploracja danych i wizualizacji</span><span class="sxs-lookup"><span data-stu-id="27cb6-195">Data exploration & visualization</span></span>
<span data-ttu-id="27cb6-196">Po wprowadzeniu danych hello w Spark, hello następnego kroku w procesie nauki danych hello jest lepiej zrozumieć toogain hello danych za pośrednictwem eksploracji i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="27cb6-197">W tej sekcji omówione hello taksówki danych przy użyciu zapytania SQL oraz kreślenia hello docelowych zmiennych i potencjalnego funkcji inspekcji visual.</span><span class="sxs-lookup"><span data-stu-id="27cb6-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="27cb6-198">W szczególności firma Microsoft wykreślenia hello częstotliwość liczby osób w podróży taksówki, częstotliwość hello kwot Porada i jak porady różnią się zależnie od ilości płatności i typu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="27cb6-199">Histogram częstotliwości liczba osób w próbce hello taksówki rund do wykreślenia</span><span class="sxs-lookup"><span data-stu-id="27cb6-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="27cb6-200">Ten kod i kolejne wstawki Użyj przykładowe hello magic tooquery SQL i tooplot magic lokalne powitania danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="27cb6-201">**Magiczna SQL (`%%sql`)** hello jądra HDInsight PySpark obsługuje łatwe wbudowanego HiveQL zapytań dotyczących element sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="27cb6-202">Witaj (-o nazwa_zmiennej) argument będzie się powtarzał hello wyników kwerendy SQL hello jako DataFrame Pandas na powitania serwera Jupyter.</span><span class="sxs-lookup"><span data-stu-id="27cb6-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="27cb6-203">Oznacza to, że jest on dostępny w trybie lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="27cb6-204">Witaj  **`%%local` magic** jest używany kod toorun lokalnie na powitania Jupyter serwera, który jest headnode hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="27cb6-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="27cb6-205">Zazwyczaj `%%local` magic po hello `%%sql -o` magic jest używane toorun zapytania.</span><span class="sxs-lookup"><span data-stu-id="27cb6-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="27cb6-206">parametru -o Hello czy utrwalić danych wyjściowych hello hello lokalnie zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="27cb6-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="27cb6-207">Następnie hello `%%local` magic wyzwalaczy hello następnego zestawu toorun wstawki kodu lokalnie przed hello dane wyjściowe zapytań SQL hello umieszczone lokalnie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="27cb6-208">Po uruchomieniu kodu hello automatyczna wizualizacja Hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="27cb6-209">To zapytanie pobiera rund hello według liczby osób.</span><span class="sxs-lookup"><span data-stu-id="27cb6-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="27cb6-210">Ten kod tworzy lokalne ramki danych z wyników kwerendy hello i geograficzne hello danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="27cb6-211">Witaj `%%local` magic tworzy lokalne ramki danych, `sqlResults`, które mogą służyć do kreślenia z matplotlib.</span><span class="sxs-lookup"><span data-stu-id="27cb6-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="27cb6-212">Ta magic PySpark jest używana wiele razy w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="27cb6-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="27cb6-213">W przypadku dużych hello ilość danych, należy przykładowe toocreate danych ramki, który można umieścić w lokalnej pamięci.</span><span class="sxs-lookup"><span data-stu-id="27cb6-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="27cb6-214">Oto hello kodu tooplot hello rund przez pasażerów liczby</span><span class="sxs-lookup"><span data-stu-id="27cb6-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="27cb6-215">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-215">**OUTPUT**</span></span>

![Częstotliwość rund według liczby osób](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="27cb6-217">Można dokonać wyboru spośród kilku różnych typów wizualizacji (tabeli, kołowego, wiersz, obszar lub pasek) przy użyciu hello **typu** przycisków menu w notesie hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="27cb6-218">Wykres słupkowy Hello jest wyświetlany w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="27cb6-219">Wykreślenia histogram kwot porady i jak kwota Porada jest zależna od ilości taryfy i liczba osób.</span><span class="sxs-lookup"><span data-stu-id="27cb6-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="27cb6-220">Użyj danych toosample zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="27cb6-220">Use a SQL query toosample data..</span></span>

    # SQL SQUERY
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


<span data-ttu-id="27cb6-221">Ta komórka kod używa hello SQL kwerendy toocreate trzy powierzchni hello danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="27cb6-222">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="27cb6-222">**OUTPUT:**</span></span> 

![Porada kwota dystrybucji](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Porada kwota według liczby osób](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Porada kwota przez taryfy kwota](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="27cb6-226">Funkcja przygotowanie zespołu inżynieryjnego, przekształcania i danych do modelowania</span><span class="sxs-lookup"><span data-stu-id="27cb6-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="27cb6-227">Tej części opisano i przedstawiono hello kod dla procedur używanych tooprepare danych do użycia w ML modelowania.</span><span class="sxs-lookup"><span data-stu-id="27cb6-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="27cb6-228">Widoczny jest sposób hello toodo następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="27cb6-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="27cb6-229">Utwórz nową funkcję podział godzin, w pojemnikach czasu ruchu</span><span class="sxs-lookup"><span data-stu-id="27cb6-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="27cb6-230">Indeks i na gorącą kodowania funkcji podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="27cb6-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="27cb6-231">Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML</span><span class="sxs-lookup"><span data-stu-id="27cb6-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="27cb6-232">Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów</span><span class="sxs-lookup"><span data-stu-id="27cb6-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="27cb6-233">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="27cb6-233">Feature scaling</span></span>
* <span data-ttu-id="27cb6-234">Obiektów w pamięci podręcznej w pamięci</span><span class="sxs-lookup"><span data-stu-id="27cb6-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="27cb6-235">Utwórz nową funkcję podział czasu ruchu w pojemnikach</span><span class="sxs-lookup"><span data-stu-id="27cb6-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="27cb6-236">Ten kod pokazuje, jak toocreate nowa funkcja podział ruchu razy w bins, a następnie jak toocache hello wynikowe ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="27cb6-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="27cb6-237">Buforowanie prowadzi czas wykonania tooimproved gdzie odporność rozproszonych zestawów danych (RDDs) i ramek danych są używane wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="27cb6-238">Tak firma Microsoft pamięci podręcznej RDDs i ramek danych w kilku etapach w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="27cb6-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="27cb6-239">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-239">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-240">126050</span><span class="sxs-lookup"><span data-stu-id="27cb6-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="27cb6-241">Indeks i hot jeden kodowania funkcji podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="27cb6-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="27cb6-242">W tej sekcji przedstawiono sposób tooindex lub zakodować podzielone na kategorie funkcje dla danych wejściowych do hello modelowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="27cb6-243">Witaj, modelowania i prognozowania funkcje MLlib wymaga, aby z kategorii danych wejściowych funkcji być indeksowane zakodowane toouse wcześniejszych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="27cb6-244">W zależności od modelu hello muszą tooindex lub zakodować je na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="27cb6-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="27cb6-245">Na przykład Logistic i regresji liniowej modele wymagają dynamicznego jeden kodowania, gdzie, na przykład funkcja z trzech kategorii można rozszerzyć do trzy kolumny funkcji, z każdym zawierających 0 lub 1 w zależności od kategorii hello obserwacji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="27cb6-246">Udostępnia MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funkcji toodo hot jednego kodowania.</span><span class="sxs-lookup"><span data-stu-id="27cb6-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="27cb6-247">Ten koder mapuje kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="27cb6-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="27cb6-248">Ten typ kodowania umożliwia algorytmy, które oczekują numeryczny ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.</span><span class="sxs-lookup"><span data-stu-id="27cb6-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="27cb6-249">Oto hello tooindex kodu i kodowania funkcji podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="27cb6-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="27cb6-250">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-250">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-251">Czas trwania tooexecute nad komórką: 3.14 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="27cb6-252">Tworzenie obiektów etykietą punktu na dane wejściowe do funkcji ML</span><span class="sxs-lookup"><span data-stu-id="27cb6-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="27cb6-253">Ta sekcja zawiera kod, który pokazuje, jak typ danych tekstowych podzielone na kategorie tooindex jako etykietą punktu danych i jak tooencode go.</span><span class="sxs-lookup"><span data-stu-id="27cb6-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="27cb6-254">To przygotowuje toobe używane tootrain i testowania MLlib Regresja logistyczna i inne modele klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="27cb6-255">Obiekty etykietą punktu są odporne rozproszonych zestawów danych (RDD) sformatowany w sposób, który jest potrzebny jako danych wejściowych przez większość algorytmów uczenia Maszynowego w MLlib.</span><span class="sxs-lookup"><span data-stu-id="27cb6-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="27cb6-256">A [etykietą punktu](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) lokalnego wektora, zawierające gęsto lub rozrzedzony, skojarzony z etykiety/odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="27cb6-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="27cb6-257">Oto hello tooindex kodu i kodowania tekstu funkcje klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="27cb6-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="27cb6-258">Oto kod hello tooencode i pod indeksem funkcje podzielone na kategorie tekstu do analizy regresji liniowej.</span><span class="sxs-lookup"><span data-stu-id="27cb6-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="27cb6-259">Tworzenie podrzędnego losowej próbki danych hello i podziel go do celów szkoleniowych i testów zestawów</span><span class="sxs-lookup"><span data-stu-id="27cb6-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="27cb6-260">Ten kod tworzy losowej próbki hello danych (25% służy w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="27cb6-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="27cb6-261">Chociaż nie jest wymagana w tym przykładzie powodu toohello rozmiaru zestawu danych hello, przedstawiony sposób można przykładowe dane hello w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="27cb6-262">Wiesz, jak toouse on własne problemu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="27cb6-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="27cb6-263">W przypadku dużych przykłady to zapisanie długiego czasu podczas szkolenia modeli.</span><span class="sxs-lookup"><span data-stu-id="27cb6-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="27cb6-264">Obok próbki hello możemy podzielić na części szkolenia (w tym miejscu 75%) i testowania toouse część (25% tutaj) w klasyfikacji i regresji modelowania.</span><span class="sxs-lookup"><span data-stu-id="27cb6-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

<span data-ttu-id="27cb6-265">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-265">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-266">Czas trwania tooexecute nad komórką: 0.31 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="27cb6-267">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="27cb6-267">Feature scaling</span></span>
<span data-ttu-id="27cb6-268">Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="27cb6-269">Witaj kodu funkcji skalowania używa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello funkcji toounit wariancji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="27cb6-270">Do użytku w regresji liniowej z stochastycznego gradientu spadku (SGD) są dostarczane przez MLlib.</span><span class="sxs-lookup"><span data-stu-id="27cb6-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="27cb6-271">SGD jest popularnych Algorytm uczenia szeroką gamę innych modeli, takie jak umorzyć regresji lub pomocy technicznej wektor maszyny (SVM) uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="27cb6-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="27cb6-272">Znaleźliśmy skalowanie hello LinearRegressionWithSGD algorytm toobe toofeature poufnych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="27cb6-273">Oto hello kodu tooscale zmienne do użytku z hello umorzyć liniowej SGD algorytmu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="27cb6-274">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-274">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-275">Czas trwania tooexecute nad komórką: 11.67 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="27cb6-276">Obiektów w pamięci podręcznej w pamięci</span><span class="sxs-lookup"><span data-stu-id="27cb6-276">Cache objects in memory</span></span>
<span data-ttu-id="27cb6-277">czas Hello uczenie i testowanie algorytmów uczenia Maszynowego można zmniejszyć przez buforowanie ramki danych wejściowych hello obiekty używane do klasyfikacji i regresji i skalowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="27cb6-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="27cb6-278">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-278">**OUTPUT**</span></span> 

<span data-ttu-id="27cb6-279">Czas trwania tooexecute nad komórką: 0,13 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="27cb6-280">Przewidywanie, czy z modelami klasyfikacji binarnej otrzymuje porady</span><span class="sxs-lookup"><span data-stu-id="27cb6-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="27cb6-281">W tej sekcji przedstawiono sposób użycia trzech modeli dla zadanie klasyfikacji binarnej hello przewidywania czy poradę ma być stosowany w podróży taksówki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="27cb6-282">modele Hello prezentowane są:</span><span class="sxs-lookup"><span data-stu-id="27cb6-282">hello models presented are:</span></span>

* <span data-ttu-id="27cb6-283">Regresja logistyczna</span><span class="sxs-lookup"><span data-stu-id="27cb6-283">Logistic regression</span></span> 
* <span data-ttu-id="27cb6-284">Losowe lasu</span><span class="sxs-lookup"><span data-stu-id="27cb6-284">Random forest</span></span>
* <span data-ttu-id="27cb6-285">Gradientu zwiększania wyniku drzewa</span><span class="sxs-lookup"><span data-stu-id="27cb6-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="27cb6-286">Każdy model budowania sekcji kodu jest podzielony na kroki:</span><span class="sxs-lookup"><span data-stu-id="27cb6-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="27cb6-287">**Model uczenia** danych za pomocą jednego zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="27cb6-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="27cb6-288">**Model oceny** na testowego zestawu danych o metryki</span><span class="sxs-lookup"><span data-stu-id="27cb6-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="27cb6-289">**Zapisywanie modelu** w obiekcie blob do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="27cb6-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="27cb6-290">Zostanie przedstawiony sposób toodo krzyżowego sprawdzania poprawności (CV) z parametrem profilach na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="27cb6-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="27cb6-291">Przy użyciu **ogólnego** kodu niestandardowego, który może być zastosowane tooany algorytmu w parametrze MLlib i tooany ustawia w algorytmie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="27cb6-292">Przy użyciu hello **pySpark CrossValidator potoku funkcji**.</span><span class="sxs-lookup"><span data-stu-id="27cb6-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="27cb6-293">Należy pamiętać, że CrossValidator ma kilka ograniczeń dotyczących Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="27cb6-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="27cb6-294">Modele potoku nie może być zapisany/utrwalony do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="27cb6-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="27cb6-295">Nie można używać dla każdego parametru w modelu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="27cb6-296">Nie można używać dla każdego algorytmu MLlib.</span><span class="sxs-lookup"><span data-stu-id="27cb6-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="27cb6-297">Ogólny krzyżowe sprawdzanie poprawności i kominów hyperparameter używane z algorytmem Regresja logistyczna hello klasyfikacji binarnej</span><span class="sxs-lookup"><span data-stu-id="27cb6-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="27cb6-298">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="27cb6-299">Hello model jest uczony za pomocą innej sprawdzania poprawności (CV) i kominów hyperparameter zaimplementowany przy użyciu kodu niestandardowego, który może być zastosowane tooany z hello uczenia algorytmy MLlib.</span><span class="sxs-lookup"><span data-stu-id="27cb6-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="27cb6-300">wykonanie Hello niestandardowego kodu CV może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="27cb6-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="27cb6-301">**Uczenie modelu Regresja logistyczna hello przy użyciu CV i kominów hyperparameter**</span><span class="sxs-lookup"><span data-stu-id="27cb6-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-302">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-302">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-303">Współczynniki: [0.0082065285375,-0.0223675576104,-0.0183812028036, - 3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="27cb6-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="27cb6-304">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="27cb6-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="27cb6-305">Czas trwania tooexecute nad komórką: 14.43 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="27cb6-306">**Ocena modelu klasyfikacji binarnej hello o standardowych metryki**</span><span class="sxs-lookup"><span data-stu-id="27cb6-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="27cb6-307">Kod Hello w tej sekcji przedstawiono, jak tooevaluate Regresja logistyczna modelu względem danych zestawu testowego, łącznie z wykresu hello krzywą ROC.</span><span class="sxs-lookup"><span data-stu-id="27cb6-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-308">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-308">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-309">Obszarze PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="27cb6-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="27cb6-310">Obszarze ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="27cb6-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="27cb6-311">Podsumowanie statystyk</span><span class="sxs-lookup"><span data-stu-id="27cb6-311">Summary Stats</span></span>

<span data-ttu-id="27cb6-312">Dokładność = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="27cb6-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="27cb6-313">Odwołaj = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="27cb6-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="27cb6-314">F1 Wynik = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="27cb6-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="27cb6-315">Czas trwania tooexecute nad komórką: 2.67 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="27cb6-316">**Wykreślić krzywą ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="27cb6-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="27cb6-317">Witaj *predictionAndLabelsDF* jest zarejestrowany jako tabelę, *tmp_results*, w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="27cb6-318">*tmp_results* można toodo używane zapytania i wyświetlić wyników do hello sqlResults danych ramki do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="27cb6-319">Oto kod hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="27cb6-320">Oto hello kodu toomake prognoz i hello kreślenia krzywą ROC.</span><span class="sxs-lookup"><span data-stu-id="27cb6-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


<span data-ttu-id="27cb6-321">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-321">**OUTPUT**</span></span>

![Regresja logistyczna krzywą ROC dla metody ogólne](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="27cb6-323">**Utrwalanie modelu w obiekcie blob do użytku w przyszłości**</span><span class="sxs-lookup"><span data-stu-id="27cb6-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="27cb6-324">Hello kodu w tej sekcji pokazano, jak model Regresja logistyczna hello toosave zużycia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="27cb6-325">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-325">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-326">Czas trwania tooexecute nad komórką: 34.57 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="27cb6-327">Funkcja w MLlib CrossValidator potoku z modelu Regresja logistyczna (Regresja elastycznej)</span><span class="sxs-lookup"><span data-stu-id="27cb6-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="27cb6-328">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model Regresja logistyczna z [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="27cb6-329">Hello model jest uczony przy użyciu krzyżowego sprawdzania poprawności (CV) i kominów hyperparameter zaimplementowany przy użyciu hello MLlib CrossValidator potoku funkcji dla CV z odchylenia parametru.</span><span class="sxs-lookup"><span data-stu-id="27cb6-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="27cb6-330">wykonywanie Hello ten kod MLlib CV może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="27cb6-330">hello execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="27cb6-331">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-331">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-332">Czas trwania tooexecute nad komórką: 107.98 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="27cb6-333">**Wykreślić krzywą ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="27cb6-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="27cb6-334">Witaj *predictionAndLabelsDF* jest zarejestrowany jako tabelę, *tmp_results*, w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="27cb6-335">*tmp_results* można toodo używane zapytania i wyświetlić wyników do hello sqlResults danych ramki do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="27cb6-336">Oto kod hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="27cb6-337">Oto krzywą ROC hello hello kodu tooplot.</span><span class="sxs-lookup"><span data-stu-id="27cb6-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


<span data-ttu-id="27cb6-338">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-338">**OUTPUT**</span></span>

![Regresja logistyczna krzywą ROC przy użyciu jego MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="27cb6-340">Klasyfikacja losowe lasu</span><span class="sxs-lookup"><span data-stu-id="27cb6-340">Random forest classification</span></span>
<span data-ttu-id="27cb6-341">Hello kodu w tej sekcji przedstawiono, jak tootrain, oceny i Zapisz regresji losowe lasu, który prognozuje czy porady ma być stosowany w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


<span data-ttu-id="27cb6-342">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-342">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-343">Obszarze ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="27cb6-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="27cb6-344">Czas trwania tooexecute nad komórką: 26.72 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="27cb6-345">Gradientu zwiększania wyniku klasyfikacji drzewa.</span><span class="sxs-lookup"><span data-stu-id="27cb6-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="27cb6-346">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który wskazuje, czy etykietki jest płatnej w podróży w hello NYC taksówki podróży i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

<span data-ttu-id="27cb6-347">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-347">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-348">Obszarze ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="27cb6-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="27cb6-349">Czas trwania tooexecute nad komórką: 28.13 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="27cb6-350">Przewidywanie kwota Porada z modelami regresji (bez użycia CV)</span><span class="sxs-lookup"><span data-stu-id="27cb6-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="27cb6-351">W tej sekcji przedstawiono sposób użycia trzech modeli dla zadań regresji hello: przewidywanie kwota Porada hello płatnej w podróży taksówki na podstawie innych funkcji porada.</span><span class="sxs-lookup"><span data-stu-id="27cb6-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="27cb6-352">modele Hello prezentowane są:</span><span class="sxs-lookup"><span data-stu-id="27cb6-352">hello models presented are:</span></span>

* <span data-ttu-id="27cb6-353">Umorzyć regresji liniowej</span><span class="sxs-lookup"><span data-stu-id="27cb6-353">Regularized linear regression</span></span>
* <span data-ttu-id="27cb6-354">Losowe lasu</span><span class="sxs-lookup"><span data-stu-id="27cb6-354">Random forest</span></span>
* <span data-ttu-id="27cb6-355">Gradientu zwiększania wyniku drzewa</span><span class="sxs-lookup"><span data-stu-id="27cb6-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="27cb6-356">Te modele zostały opisane w hello wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-356">These models were described in hello introduction.</span></span> <span data-ttu-id="27cb6-357">Każdy model budowania sekcji kodu jest podzielony na kroki:</span><span class="sxs-lookup"><span data-stu-id="27cb6-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="27cb6-358">**Model uczenia** danych za pomocą jednego zestawu parametrów</span><span class="sxs-lookup"><span data-stu-id="27cb6-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="27cb6-359">**Model oceny** na testowego zestawu danych o metryki</span><span class="sxs-lookup"><span data-stu-id="27cb6-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="27cb6-360">**Zapisywanie modelu** w obiekcie blob do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="27cb6-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="27cb6-361">AZURE Uwaga: Krzyżowego sprawdzania poprawności nie jest używana z modelami trzy regresji hello w tej sekcji, ponieważ została ona wyświetlana szczegółowo hello Regresja logistyczna modeli.</span><span class="sxs-lookup"><span data-stu-id="27cb6-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="27cb6-362">Przykład przedstawiający sposób toouse CV elastycznej NET regresji liniowej znajduje się w hello dodatku w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="27cb6-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="27cb6-363">AZURE Uwaga: W naszym środowisku może istnieć problemy z zbieżności LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="27cb6-364">Skalowanie zmiennych znacznie ułatwia zbieżności.</span><span class="sxs-lookup"><span data-stu-id="27cb6-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="27cb6-365">Można także elastycznej net regresji, przedstawiono w temacie toothis dodatku hello, zamiast LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="27cb6-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="27cb6-366">Regresji liniowej z SGD</span><span class="sxs-lookup"><span data-stu-id="27cb6-366">Linear regression with SGD</span></span>
<span data-ttu-id="27cb6-367">Witaj kodu w tej sekcji przedstawiono sposób toouse skalowania tootrain funkcji regresji liniowej używającej stochastycznego spadku gradientu (SGD) dla usługi optymalizacji, oraz sposób tooscore, oceny i Zapisz hello model w usłudze Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="27cb6-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="27cb6-368">Wiemy z doświadczenia mogą występować problemy z zbieżności hello LinearRegressionWithSGD modeli, a parametry muszą toobe zmienić/zoptymalizowaną dokładnie uzyskiwania prawidłowego modelu.</span><span class="sxs-lookup"><span data-stu-id="27cb6-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="27cb6-369">Skalowanie zmiennych znacznie ułatwia zbieżności.</span><span class="sxs-lookup"><span data-stu-id="27cb6-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="27cb6-370">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-370">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-371">Współczynniki: [0.0141707753435,-0.0252930927087,-0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092,-0.00456498588241,-0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632,-0.00289545676449,-0.00791124681938, 0.54396316518,-0.536293513569, 0.0119076553369,-0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="27cb6-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="27cb6-372">Przechwycić: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="27cb6-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="27cb6-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="27cb6-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="27cb6-374">R sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="27cb6-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="27cb6-375">Czas trwania tooexecute nad komórką: 38.62 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="27cb6-376">Regresja losowe lasu</span><span class="sxs-lookup"><span data-stu-id="27cb6-376">Random Forest regression</span></span>
<span data-ttu-id="27cb6-377">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz model losowe lasu, który prognozuje Porada kwota hello NYC taksówki podróży danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="27cb6-378">Krzyżowe sprawdzanie poprawności parametru profilach przy użyciu kodu niestandardowego znajduje się w dodatku hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

<span data-ttu-id="27cb6-379">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-379">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="27cb6-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="27cb6-381">R sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="27cb6-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="27cb6-382">Czas trwania tooexecute nad komórką: 25.98 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="27cb6-383">Gradientu zwiększania wyniku regresji drzewa.</span><span class="sxs-lookup"><span data-stu-id="27cb6-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="27cb6-384">Kod Hello w tej sekcji przedstawiono sposób tootrain, oceny i Zapisz gradientu zwiększania wyniku modelu drzewa, który prognozuje Porada kwota hello NYC taksówki podróży danych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="27cb6-385">** Nauczanie i Ewaluacja **</span><span class="sxs-lookup"><span data-stu-id="27cb6-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-386">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-386">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="27cb6-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="27cb6-388">R sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="27cb6-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="27cb6-389">Czas trwania tooexecute nad komórką: 20.9 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="27cb6-390">**Kreślenia**</span><span class="sxs-lookup"><span data-stu-id="27cb6-390">**Plot**</span></span>

<span data-ttu-id="27cb6-391">*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="27cb6-392">Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="27cb6-393">Oto kod hello</span><span class="sxs-lookup"><span data-stu-id="27cb6-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="27cb6-394">Oto hello kodu tooplot hello danych przy użyciu hello Jupyter serwera.</span><span class="sxs-lookup"><span data-stu-id="27cb6-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Vs przewidzieć — Porada kwoty rzeczywiste](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="27cb6-396">Dodatek: Regresji dodatkowych zadań z wykorzystaniem krzyżowego sprawdzania poprawności z przeszukiwanie parametru</span><span class="sxs-lookup"><span data-stu-id="27cb6-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="27cb6-397">Ten dodatek zawiera kod, przedstawiający sposób CV toodo przy użyciu elastycznej net regresji liniowej i jak CV toodo z parametrem odchylenia dla lasu losowe regresji przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="27cb6-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="27cb6-398">Krzyżowe sprawdzanie poprawności przy użyciu elastyczna net regresji liniowej</span><span class="sxs-lookup"><span data-stu-id="27cb6-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="27cb6-399">Hello kodu w tej sekcji przedstawiono sposób toodo krzyżowe sprawdzanie poprawności przy użyciu elastyczna net regresji liniowej i jak tooevaluate hello modelu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-400">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-400">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-401">Czas trwania tooexecute nad komórką: 161.21 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="27cb6-402">**Ocena z metryką R SQR**</span><span class="sxs-lookup"><span data-stu-id="27cb6-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="27cb6-403">*tmp_results* jest zarejestrowany jako tabeli programu Hive w hello poprzedniej komórki.</span><span class="sxs-lookup"><span data-stu-id="27cb6-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="27cb6-404">Wyniki z tabeli hello są dane wyjściowe do hello *sqlResults* ramki danych do kreślenia.</span><span class="sxs-lookup"><span data-stu-id="27cb6-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="27cb6-405">Oto kod hello</span><span class="sxs-lookup"><span data-stu-id="27cb6-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="27cb6-406">Oto hello kodu toocalculate R sqr.</span><span class="sxs-lookup"><span data-stu-id="27cb6-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="27cb6-407">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-407">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-408">R sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="27cb6-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="27cb6-409">Krzyżowe sprawdzanie poprawności z odchylenia parametr dla lasu losowe regresji przy użyciu kodu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="27cb6-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="27cb6-410">Hello kodu w tej sekcji przedstawiono sposób toodo krzyżowe sprawdzanie poprawności z odchylenia parametr przy użyciu kodu niestandardowego dla lasu losowe regresji i jak tooevaluate hello modelu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="27cb6-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="27cb6-411">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-411">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="27cb6-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="27cb6-413">R sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="27cb6-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="27cb6-414">Czas trwania tooexecute nad komórką: 69.17 sekund</span><span class="sxs-lookup"><span data-stu-id="27cb6-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="27cb6-415">Czyszczenie obiektów w pamięci i lokalizacjach modelu drukowania</span><span class="sxs-lookup"><span data-stu-id="27cb6-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="27cb6-416">Użyj `unpersist()` toodelete obiektów w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="27cb6-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


<span data-ttu-id="27cb6-417">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-417">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-418">PythonRDD [122] w RDD w PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="27cb6-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="27cb6-419">** Wydruku toomodel ścieżki plików toobe używane w notesie zużycie hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="27cb6-420">** tooconsume i wynik niezależne — zestaw danych, należy toocopy go i Wklej te nazwy pliku w "Zużycia notesu" hello.</span><span class="sxs-lookup"><span data-stu-id="27cb6-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="27cb6-421">**DANE WYJŚCIOWE**</span><span class="sxs-lookup"><span data-stu-id="27cb6-421">**OUTPUT**</span></span>

<span data-ttu-id="27cb6-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="27cb6-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="27cb6-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="27cb6-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="27cb6-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="27cb6-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="27cb6-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="27cb6-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="27cb6-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="27cb6-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="27cb6-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="27cb6-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="27cb6-428">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="27cb6-428">What's next?</span></span>
<span data-ttu-id="27cb6-429">Teraz po utworzeniu modele regresji i klasyfikacji z hello Spark MlLib, wszystko jest gotowe toolearn jak tooscore i oceny tych modeli.</span><span class="sxs-lookup"><span data-stu-id="27cb6-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="27cb6-430">**Model zużycia:** toolearn jak tooscore i ocenić hello klasyfikacji i regresji modeli utworzonych w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="27cb6-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

