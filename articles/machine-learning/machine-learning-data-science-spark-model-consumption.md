---
title: Operacjonalizuj modele uczenia wbudowane Spark maszyny | Dokumentacja firmy Microsoft
description: "Jak obciążenia i przechowywane w usłudze Azure Blob Storage (WASB) z języka Python modeli uczenia wynik."
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
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="b7065-103">Operacjonalizuj modele uczenia wbudowane Spark maszyny</span><span class="sxs-lookup"><span data-stu-id="b7065-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="b7065-104">W tym temacie przedstawiono sposób operacjonalizacji modelu uczenia maszynowego zapisane (ML) przy użyciu języka Python w klastrach HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="b7065-105">Go opisano, jak załadować modeli uczenia maszyny, które zostały utworzone przy użyciu Spark MLlib i przechowywane w Azure Blob Storage (WASB) i sposobie ich wynik z zestawami danych, które również były przechowywane w WASB.</span><span class="sxs-lookup"><span data-stu-id="b7065-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="b7065-106">Informuje jak wstępnie przetworzyć dane wejściowe, transformacja funkcji za pomocą funkcji indeksowania i kodowanie w zestawie narzędzi programu MLlib, jak utworzyć obiekt etykietą punktu danych, który może służyć jako dane wejściowe dla oceniania przy użyciu modeli uczenia Maszynowego.</span><span class="sxs-lookup"><span data-stu-id="b7065-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="b7065-107">Modele oceniania obejmują regresji liniowej, Regresja logistyczna losowe modeli lasu i modele drzewa zwiększania gradientu.</span><span class="sxs-lookup"><span data-stu-id="b7065-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="b7065-108">Klastry Spark i notesów Jupyter</span><span class="sxs-lookup"><span data-stu-id="b7065-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="b7065-109">Kroki instalacji i kod, który umożliwia operacjonalizację model usługi uczenie Maszynowe są udostępniane w ramach tego przewodnika dla przy użyciu klastra usługi HDInsight Spark w wersji 1.6, a także klastra Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b7065-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="b7065-110">Kod dla tych procedur jest również udostępniany w notesach Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b7065-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="b7065-111">Notesu platformy Spark w wersji 1.6</span><span class="sxs-lookup"><span data-stu-id="b7065-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="b7065-112">[PySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) notesu Jupyter pokazano, jak operacjonalizacji zapisany model przy użyciu języka Python w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7065-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="b7065-113">Notesu platformy Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="b7065-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="b7065-114">Aby zmodyfikować notesu Jupyter do wersji 1.6 Spark do korzystania z klastra usługi HDInsight Spark 2.0, Zastąp plik kodu Python z [ten plik](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="b7065-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="b7065-115">Ten kod przedstawia sposób korzystać z modeli utworzonych Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b7065-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b7065-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7065-116">Prerequisites</span></span>

1. <span data-ttu-id="b7065-117">Potrzebujesz konta platformy Azure i Spark 1.6 (lub Spark 2.0) klastra usługi HDInsight w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="b7065-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="b7065-118">Zobacz [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) instrukcje na temat sposobu spełniają tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="b7065-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="b7065-119">Ten temat zawiera również opis taksówki 2013 NYC danych używany w tym miejscu i instrukcje dotyczące sposobu wykonania kodu z notesu Jupyter w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="b7065-120">Należy także utworzyć modeli do oceny w tym miejscu pracy za pomocą uczenia maszynowego [Eksploracja danych i modelowanie z Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tematu dla klastra Spark w wersji 1.6 lub komputery przenośne Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b7065-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="b7065-121">Notesów Spark 2.0 użyć dodatkowego zestawu danych dla zadania klasyfikacji, dobrze znanego linii lotniczych na czas wyjścia zestawu danych z 2011 i 2012.</span><span class="sxs-lookup"><span data-stu-id="b7065-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="b7065-122">Opis notesów i łącza do nich znajdują się w [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) dla repozytorium GitHub zawierające je.</span><span class="sxs-lookup"><span data-stu-id="b7065-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="b7065-123">Ponadto kod w tym miejscu w notesach połączony jest rodzajowy i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="b7065-124">Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="b7065-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="b7065-125">Instalatora: lokalizacje magazynu, biblioteki i wstępnie zdefiniowane kontekstu Spark</span><span class="sxs-lookup"><span data-stu-id="b7065-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="b7065-126">Platforma Spark jest możliwość odczytu i zapisu do obiektu Blob magazynu Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="b7065-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="b7065-127">Dlatego żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i ponownie przechowywane w WASB wyniki.</span><span class="sxs-lookup"><span data-stu-id="b7065-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="b7065-128">Aby zapisać modele lub pliki w WASB, ścieżka musi prawidłowo określone.</span><span class="sxs-lookup"><span data-stu-id="b7065-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="b7065-129">Domyślny kontener dołączony do klastra Spark można odwoływać się przy użyciu ścieżki rozpoczynającej się od: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="b7065-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="b7065-130">Poniższy przykład kodu Określa lokalizację danych do odczytu i ścieżkę do katalogu magazynu modelu, w którym jest zapisany modelu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b7065-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="b7065-131">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB</span><span class="sxs-lookup"><span data-stu-id="b7065-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="b7065-132">Modele są zapisywane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/modele".</span><span class="sxs-lookup"><span data-stu-id="b7065-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="b7065-133">Jeśli ta ścieżka nie jest poprawnie ustawiona, modele nie są ładowane do oceniania.</span><span class="sxs-lookup"><span data-stu-id="b7065-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="b7065-134">Scored wyniki zostały zapisane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="b7065-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="b7065-135">Jeśli ścieżka do folderu jest nieprawidłowa, wyniki nie są zapisywane w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="b7065-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="b7065-136">Ścieżka lokalizacji plików można można kopiować i wklejać do symboli zastępczych w ten kod z danych wyjściowych ostatnią komórkę **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notesu.</span><span class="sxs-lookup"><span data-stu-id="b7065-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="b7065-137">Oto kod, aby ustawić ścieżki katalogu:</span><span class="sxs-lookup"><span data-stu-id="b7065-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="b7065-138">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-138">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-139">DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="b7065-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="b7065-140">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="b7065-140">Import libraries</span></span>
<span data-ttu-id="b7065-141">Ustaw kontekst spark i zaimportuj wymagane biblioteki z następującym kodem</span><span class="sxs-lookup"><span data-stu-id="b7065-141">Set spark context and import necessary libraries with the following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="b7065-142">Wstępnie zdefiniowane kontekstu Spark i poleceń magicznych PySpark</span><span class="sxs-lookup"><span data-stu-id="b7065-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="b7065-143">Jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu.</span><span class="sxs-lookup"><span data-stu-id="b7065-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="b7065-144">Dlatego nie trzeba ustawić Spark lub tworzenia kontekstów Hive jawnie, przed rozpoczęciem pracy z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="b7065-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="b7065-145">Są one dostępne dla Ciebie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b7065-145">These are available for you by default.</span></span> <span data-ttu-id="b7065-146">Konteksty te są:</span><span class="sxs-lookup"><span data-stu-id="b7065-146">These contexts are:</span></span>

* <span data-ttu-id="b7065-147">sc - platformy Spark</span><span class="sxs-lookup"><span data-stu-id="b7065-147">sc - for Spark</span></span> 
* <span data-ttu-id="b7065-148">Element sqlContext - gałęzi</span><span class="sxs-lookup"><span data-stu-id="b7065-148">sqlContext - for Hive</span></span>

<span data-ttu-id="b7065-149">Jądro PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%.</span><span class="sxs-lookup"><span data-stu-id="b7065-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="b7065-150">Istnieją dwa polecenia, które są używane w tych przykładach kodu.</span><span class="sxs-lookup"><span data-stu-id="b7065-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="b7065-151">**%% lokalnego** określono, że kod w kolejnych wierszy jest wykonywane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b7065-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="b7065-152">Kod musi być prawidłowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="b7065-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="b7065-153">**%% sql -o<variable name>**</span><span class="sxs-lookup"><span data-stu-id="b7065-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="b7065-154">Wykonuje zapytanie Hive względem element sqlContext.</span><span class="sxs-lookup"><span data-stu-id="b7065-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="b7065-155">Jeśli parametr -o zostanie przekazany, wynik kwerendy jest utrwalona w %% lokalny kontekst Python jako Pandas dataframe.</span><span class="sxs-lookup"><span data-stu-id="b7065-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="b7065-156">Dla więcej informacji na temat jądra notesów Jupyter i wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b7065-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="b7065-157">Pozyskiwania danych i Utwórz ramkę, oczyszczony danych</span><span class="sxs-lookup"><span data-stu-id="b7065-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="b7065-158">Ta sekcja zawiera kod szereg zadań wymaganych do pozyskiwania danych do oceny.</span><span class="sxs-lookup"><span data-stu-id="b7065-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="b7065-159">Odczyt w próbce dołączonego do 0,1% taksówki podróży i taryfy pliku (przechowywane jako plik .tsv), format danych, a następnie tworzy ramkę Wyczyść dane.</span><span class="sxs-lookup"><span data-stu-id="b7065-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="b7065-160">Pliki podróży i taryfy taksówki zostały dołączone oparte na na procedury w: [zespołu danych nauki procesu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="b7065-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b7065-161">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-161">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-162">Czas wykonywania nad komórką: 46.37 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="b7065-163">Przygotowanie danych do oceniania w łączniku Spark</span><span class="sxs-lookup"><span data-stu-id="b7065-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="b7065-164">W tej sekcji przedstawiono sposób indeksu, kodowanie i skalowanie funkcji podzielone na kategorie, aby przygotować je do użycia w algorytmów uczenia nadzorowanego MLlib dla funkcji klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="b7065-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="b7065-165">Funkcja transformacji: indeks i kodowania podzielone na kategorie funkcje dla danych wejściowych do modeli wyników.</span><span class="sxs-lookup"><span data-stu-id="b7065-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="b7065-166">W tej sekcji przedstawiono sposób indeksu kategorii danych przy użyciu `StringIndexer` i funkcji przy użyciu kodowania `OneHotEncoder` modeli danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="b7065-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="b7065-167">[StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) koduje kolumny ciąg etykiet do kolumny indeksów etykiety.</span><span class="sxs-lookup"><span data-stu-id="b7065-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="b7065-168">Indeksy są uporządkowane według częstotliwości etykiety.</span><span class="sxs-lookup"><span data-stu-id="b7065-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="b7065-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mapy kolumny indeksów etykiety z kolumną wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="b7065-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="b7065-170">Ten typ kodowania umożliwia algorytmy, które oczekują ciągłego ważnych funkcji, takich jak Regresja logistyczna ma zostać zastosowany do funkcji podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="b7065-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b7065-171">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-171">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-172">Czas wykonywania nad komórką: 5.37 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="b7065-173">Tworzenie obiektów RDD z tablicami funkcji dla danych wejściowych do modeli</span><span class="sxs-lookup"><span data-stu-id="b7065-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="b7065-174">Ta sekcja zawiera kod, który pokazuje, jak dane tekstowe podzielone na kategorie jako obiekt RDD indeksu i hot jeden kodowania jej dzięki mogą być używane do nauczenia i przetestowania Regresja logistyczna MLlib i oparta na drzewie modeli.</span><span class="sxs-lookup"><span data-stu-id="b7065-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="b7065-175">Indeksowane dane są przechowywane w [odporność rozproszonych zestawu danych (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) obiektów.</span><span class="sxs-lookup"><span data-stu-id="b7065-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="b7065-176">Są to podstawowe abstrakcji w łączniku Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="b7065-177">Obiekt RDD reprezentuje niezmienne partycjonowanej kolekcję elementów, które może być obsługiwany przez równolegle z platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="b7065-178">Zawiera także kod, który pokazuje, jak skalować dane z `StandardScalar` podał MLlib do użycia w regresji liniowej z stochastycznego gradientu spadku (SGD), popularnych Algorytm uczenia szeroką gamę machine learning modeli.</span><span class="sxs-lookup"><span data-stu-id="b7065-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="b7065-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) służy do funkcji do wariancji jednostki skalowania.</span><span class="sxs-lookup"><span data-stu-id="b7065-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="b7065-180">Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji.</span><span class="sxs-lookup"><span data-stu-id="b7065-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b7065-181">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-181">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-182">Czas wykonywania nad komórką: 11.72 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="b7065-183">Wynik z modelem Regresja logistyczna i zapisać dane wyjściowe do obiektu blob</span><span class="sxs-lookup"><span data-stu-id="b7065-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="b7065-184">Kod w tej sekcji przedstawiono sposób załadować logistyczna Model regresji, który został zapisany w magazynie obiektów blob platformy Azure i użyć go do prognozowania, czy w podróży taksówki otrzymuje poradę, wynik go z metryki standardowej klasyfikacji, a następnie zapisz i wykreślenia wyniki do obiektu blob stora GE.</span><span class="sxs-lookup"><span data-stu-id="b7065-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="b7065-185">Scored wyniki są przechowywane w obiektach RDD.</span><span class="sxs-lookup"><span data-stu-id="b7065-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b7065-186">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-186">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-187">Czas wykonywania nad komórką: 19.22 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="b7065-188">Score Model regresji liniowej</span><span class="sxs-lookup"><span data-stu-id="b7065-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="b7065-189">My używamy [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) do uczenia modelu regresji liniowej, przy użyciu stochastycznego gradientu spadku (SGD) na potrzeby optymalizacji na potrzeby prognozowania ilość Porada płatnej.</span><span class="sxs-lookup"><span data-stu-id="b7065-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="b7065-190">Kod w tej sekcji przedstawiono sposób ładowanie modelu regresji liniowej z magazynu obiektów blob platformy Azure, wynik, korzystając ze zmiennych skalowana, a następnie zapisz wyniki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b7065-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="b7065-191">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-191">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-192">Czas wykonywania nad komórką: 16.63 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="b7065-193">Wynik klasyfikacji i regresji losowe modeli lasu</span><span class="sxs-lookup"><span data-stu-id="b7065-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="b7065-194">Kod w tej sekcji przedstawiono sposób załadować zapisanych klasyfikacji i regresji losowe lasu modeli zapisane w magazynie obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz wyniki do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b7065-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="b7065-195">[Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7065-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="b7065-196">Łączą wiele drzew decyzyjnych, aby zmniejszyć ryzyko overfitting.</span><span class="sxs-lookup"><span data-stu-id="b7065-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="b7065-197">Losowe lasów mogą obsługiwać funkcje podzielone na kategorie, rozszerzyć ustawienie wieloklasowej klasyfikacji, nie wymagają funkcji skalowania i są w stanie przechwytywania nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="b7065-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="b7065-198">Losowe lasach są jednym z modeli dla funkcji klasyfikacji i regresji uczenia maszynowego najbardziej popularnych.</span><span class="sxs-lookup"><span data-stu-id="b7065-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="b7065-199">[Spark.mllib](http://spark.apache.org/mllib/) obsługuje losowe lasów binarnej i wieloklasowej klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="b7065-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b7065-200">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-200">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-201">Czas wykonywania nad komórką: 31.07 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="b7065-202">Wynik klasyfikacji i regresji gradientu zwiększania drzewa modeli</span><span class="sxs-lookup"><span data-stu-id="b7065-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="b7065-203">Kod w tej sekcji przedstawiono sposób załadować klasyfikacji i regresji gradientu zwiększania drzewa modeli z magazynu obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz wyniki do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b7065-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="b7065-204">**Spark.mllib** obsługuje GBTs dla binarnego klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="b7065-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="b7065-205">[Gradientu drzew zwiększania](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7065-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="b7065-206">GBTs uczenie drzew decyzyjnych wielokrotnie powtarzane, aby zminimalizować funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="b7065-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="b7065-207">GBTs mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie przechwytywania nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="b7065-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="b7065-208">Ich można również w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b7065-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b7065-209">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-209">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-210">Czas wykonywania nad komórką: 14.6 sekund</span><span class="sxs-lookup"><span data-stu-id="b7065-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="b7065-211">Czyszczenie obiektów z pamięci i Drukuj oceniane lokalizacje plików</span><span class="sxs-lookup"><span data-stu-id="b7065-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="b7065-212">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="b7065-212">**OUTPUT:**</span></span>

<span data-ttu-id="b7065-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="b7065-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="b7065-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="b7065-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="b7065-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="b7065-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="b7065-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="b7065-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="b7065-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="b7065-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="b7065-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="b7065-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="b7065-219">Korzystanie z modeli Spark przy użyciu interfejsu sieci web</span><span class="sxs-lookup"><span data-stu-id="b7065-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="b7065-220">Platforma Spark zapewnia mechanizm zdalnie przesłania zadania wsadowe lub interakcyjnych zapytań przy użyciu interfejsu REST z składnik o nazwie Livy.</span><span class="sxs-lookup"><span data-stu-id="b7065-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="b7065-221">Livy jest domyślnie włączone w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7065-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="b7065-222">Aby uzyskać więcej informacji o Livy, zobacz: [Spark przesyłania zadania zdalnie przy użyciu programu Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b7065-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="b7065-223">Można użyć programu Livy zdalnie przesłać zadanie wsadowe wyniki pliku, który jest przechowywany w obiekcie blob Azure, a następnie zapisuje wyniki do innego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b7065-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="b7065-224">Aby to zrobić, możesz przekazać skrypt w języku Python z</span><span class="sxs-lookup"><span data-stu-id="b7065-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="b7065-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) do obiektu blob klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="b7065-226">Można użyć narzędzia, takiego jak **Eksploratora usługi Microsoft Azure Storage** lub **AzCopy** do Skopiuj skrypt do obiektu blob klastra.</span><span class="sxs-lookup"><span data-stu-id="b7065-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="b7065-227">W tym przypadku możemy przekazać skrypt ***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="b7065-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="b7065-228">Klawisze dostępu, które użytkownik musi można znaleźć w portalu dla konta magazynu skojarzone z klastrem Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="b7065-229">Po przekazaniu do tej lokalizacji, ten skrypt jest uruchamiany w ramach klastra Spark w kontekście rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="b7065-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="b7065-230">Ładuje modelu i uruchamia prognoz na plików wejściowych, na podstawie modelu.</span><span class="sxs-lookup"><span data-stu-id="b7065-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="b7065-231">Ten skrypt można wywoływać zdalnie, definiując prostego żądania HTTPS/REST na Livy.</span><span class="sxs-lookup"><span data-stu-id="b7065-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="b7065-232">Oto polecenia curl, aby utworzyć żądanie HTTP można zdalnie wywołać skrypt w języku Python.</span><span class="sxs-lookup"><span data-stu-id="b7065-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="b7065-233">Zamień CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME odpowiednie wartości dla klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="b7065-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="b7065-234">Dowolnego języka w systemie zdalnym służy do wywołania zadania Spark przy użyciu programu Livy za prosty wywołania protokołu HTTPS z uwierzytelnianiem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="b7065-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="b7065-235">Będzie łatwe w użyciu żądań Python biblioteki podczas wprowadzania to wywołanie HTTP, ale nie jest aktualnie zainstalowany domyślny usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b7065-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="b7065-236">Dlatego starsze bibliotek HTTP są używane zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="b7065-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="b7065-237">Oto kod języka Python dla wywołania HTTP:</span><span class="sxs-lookup"><span data-stu-id="b7065-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="b7065-238">Można również dodać ten kod języka Python, aby [usługi Azure Functions](https://azure.microsoft.com/documentation/services/functions/) aby wyzwolić przesłania zadania Spark wyników obiektu blob na podstawie różnych zdarzeń, takich jak czasomierza, tworzenia lub aktualizacji obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b7065-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="b7065-239">Środowisko klienta wolnego kodu, należy użyć [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) do oceniania, definiując akcji HTTP w partii Spark wywołania **projektanta aplikacji logiki** oraz ustawienie jego parametrów.</span><span class="sxs-lookup"><span data-stu-id="b7065-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="b7065-240">Z portalu Azure, Utwórz nową aplikację logiki, wybierając **+ nowy** -> **sieci Web i mobilność** -> **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="b7065-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="b7065-241">Aby wyświetlić **projektanta aplikacji logiki**, wprowadź nazwę aplikacji logiki i Plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b7065-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="b7065-242">Wybierz akcję, HTTP i wprowadź parametry pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="b7065-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Projektant aplikacji logiki](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="b7065-244">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="b7065-244">What's next?</span></span>
<span data-ttu-id="b7065-245">**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.</span><span class="sxs-lookup"><span data-stu-id="b7065-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

