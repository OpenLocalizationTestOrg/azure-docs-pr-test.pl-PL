---
title: modeli uczenia maszynowego wbudowane Spark aaaOperationalize | Dokumentacja firmy Microsoft
description: "Jak tooload i wynik modeli uczenia przechowywane w usłudze Azure Blob Storage (WASB) z języka Python."
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
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="4b854-103">Operacjonalizuj modele uczenia wbudowane Spark maszyny</span><span class="sxs-lookup"><span data-stu-id="4b854-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="4b854-104">W tym temacie przedstawiono sposób toooperationalize modelu uczenia maszynowego zapisane (ML) przy użyciu języka Python w usłudze HDInsight Spark klastrów.</span><span class="sxs-lookup"><span data-stu-id="4b854-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="4b854-105">Opisuje sposób tooload maszyny modele uczenia, które zostały utworzone przy użyciu Spark MLlib i przechowywane w usłudze Azure Blob Storage (WASB) i w jaki sposób tooscore z zestawów danych, które również były przechowywane w WASB.</span><span class="sxs-lookup"><span data-stu-id="4b854-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="4b854-106">Zawiera dane wejściowe hello jak toopre proces, za pomocą funkcji przekształcenia hello indeksowania i kodowanie funkcje hello MLlib toolkit oraz jak toocreate etykietą punktu obiekt danych, które mogą być używane jako dane wejściowe dla oceniania z modelami hello ML.</span><span class="sxs-lookup"><span data-stu-id="4b854-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="4b854-107">modele Hello używany do oceniania obejmują regresji liniowej, Regresja logistyczna losowe modeli lasu i modele drzewa zwiększania gradientu.</span><span class="sxs-lookup"><span data-stu-id="4b854-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="4b854-108">Klastry Spark i notesów Jupyter</span><span class="sxs-lookup"><span data-stu-id="4b854-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="4b854-109">Kroki instalacji i toooperationalize kodu hello model usługi uczenie Maszynowe znajdują się w tej wskazówki dotyczące korzystania z klastra usługi HDInsight Spark w wersji 1.6, a także klastra Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4b854-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="4b854-110">Kod Hello tych procedur jest również udostępniany w notesach Jupyter.</span><span class="sxs-lookup"><span data-stu-id="4b854-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="4b854-111">Notesu platformy Spark w wersji 1.6</span><span class="sxs-lookup"><span data-stu-id="4b854-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="4b854-112">Witaj [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) notesu Jupyter pokazuje, jak toooperationalize zapisany model przy użyciu języka Python w usłudze HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4b854-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="4b854-113">Notesu platformy Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="4b854-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="4b854-114">notesu Jupyter hello toomodify dla toouse Spark w wersji 1.6 z klastrem usługi HDInsight Spark 2.0, Zastąp plik kodu Python hello z [ten plik](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="4b854-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="4b854-115">Ten kod przedstawia sposób tworzenia modeli hello tooconsume w Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4b854-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4b854-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b854-116">Prerequisites</span></span>

1. <span data-ttu-id="4b854-117">Potrzebujesz konta platformy Azure i Spark 1.6 (lub Spark 2.0) klastra usługi HDInsight toocomplete tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4b854-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="4b854-118">Zobacz hello [przegląd danych nauki używania platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) instrukcje na temat toosatisfy tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="4b854-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="4b854-119">Ten temat zawiera również opis hello taksówki 2013 NYC danych używany w tym miejscu i instrukcje dotyczące sposobu tooexecute kodu z notesu Jupyter w klastrze Spark hello.</span><span class="sxs-lookup"><span data-stu-id="4b854-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="4b854-120">Należy także utworzyć hello machine learning modele toobe tutaj oceniane przez pracy nad hello [Eksploracja danych i modelowanie z Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tematu dla klastra Spark w wersji 1.6 hello lub komputery przenośne hello Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="4b854-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="4b854-121">notesów Hello Spark 2.0 Użyj dodatkowy zestaw danych w przypadku zadania klasyfikacji hello hello dobrze znanego linii lotniczych na czas wyjścia zestawu danych za pomocą 2011 i 2012.</span><span class="sxs-lookup"><span data-stu-id="4b854-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="4b854-122">Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je.</span><span class="sxs-lookup"><span data-stu-id="4b854-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="4b854-123">Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="4b854-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="4b854-124">Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="4b854-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="4b854-125">Instalator: lokalizacji przechowywania, biblioteki i hello ustawienia wstępnego Spark kontekstu</span><span class="sxs-lookup"><span data-stu-id="4b854-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="4b854-126">Platforma Spark jest możliwe tooan tooread i zapisu obiektu Blob magazynu Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="4b854-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="4b854-127">Tak żadnych istniejących danych przechowywanych mogą być przetwarzane przy użyciu platformy Spark i hello powoduje WASB przechowywane ponownie.</span><span class="sxs-lookup"><span data-stu-id="4b854-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="4b854-128">modele toosave lub pliki w WASB hello ścieżka musi toobe prawidłowo określone.</span><span class="sxs-lookup"><span data-stu-id="4b854-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="4b854-129">Witaj klastra Spark toohello dołączony kontenera domyślnego można odwoływać się przy użyciu ścieżki rozpoczynającej się od: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="4b854-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="4b854-130">Hello poniższy przykład kodu określa hello lokalizację hello toobe danych do odczytu i zapisaniu ścieżki hello hello modelu magazynu katalogu toowhich hello modelu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4b854-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="4b854-131">Ustawianie ścieżki katalogu dla lokalizacji przechowywania w WASB</span><span class="sxs-lookup"><span data-stu-id="4b854-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="4b854-132">Modele są zapisywane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/modele".</span><span class="sxs-lookup"><span data-stu-id="4b854-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="4b854-133">Jeśli ta ścieżka nie jest poprawnie ustawiona, modele nie są ładowane do oceniania.</span><span class="sxs-lookup"><span data-stu-id="4b854-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="4b854-134">Witaj scored wyniki zostały zapisane w: "wasb: / / / użytkownik/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="4b854-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="4b854-135">Jeśli hello toofolder ścieżka jest nieprawidłowa, wyniki nie są zapisywane w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="4b854-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="4b854-136">lokalizacje ścieżki plików Hello można można kopiować i wklejać do symboli zastępczych hello w ten kod z danych wyjściowych hello hello ostatnią komórkę hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notesu.</span><span class="sxs-lookup"><span data-stu-id="4b854-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="4b854-137">Oto ścieżki katalogu tooset kodu hello:</span><span class="sxs-lookup"><span data-stu-id="4b854-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="4b854-138">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-138">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-139">DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="4b854-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="4b854-140">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="4b854-140">Import libraries</span></span>
<span data-ttu-id="4b854-141">Ustaw kontekst spark i zaimportuj wymagane biblioteki z hello następującego kodu</span><span class="sxs-lookup"><span data-stu-id="4b854-141">Set spark context and import necessary libraries with hello following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="4b854-142">Wstępnie zdefiniowane kontekstu Spark i poleceń magicznych PySpark</span><span class="sxs-lookup"><span data-stu-id="4b854-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="4b854-143">Hello jądra PySpark, które są dostarczane z notesów Jupyter ma wstępnie zdefiniowane kontekstu.</span><span class="sxs-lookup"><span data-stu-id="4b854-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="4b854-144">Dlatego nie trzeba konteksty Spark i Hive hello tooset jawnie przed rozpoczęciem pracy z aplikacją hello, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="4b854-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="4b854-145">Są one dostępne dla Ciebie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4b854-145">These are available for you by default.</span></span> <span data-ttu-id="4b854-146">Konteksty te są:</span><span class="sxs-lookup"><span data-stu-id="4b854-146">These contexts are:</span></span>

* <span data-ttu-id="4b854-147">sc - platformy Spark</span><span class="sxs-lookup"><span data-stu-id="4b854-147">sc - for Spark</span></span> 
* <span data-ttu-id="4b854-148">Element sqlContext - gałęzi</span><span class="sxs-lookup"><span data-stu-id="4b854-148">sqlContext - for Hive</span></span>

<span data-ttu-id="4b854-149">Witaj jądra PySpark zawiera kilka wstępnie zdefiniowanych "poleceń magicznych", które są specjalne polecenia, które można wywoływać z %%.</span><span class="sxs-lookup"><span data-stu-id="4b854-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="4b854-150">Istnieją dwa polecenia, które są używane w tych przykładach kodu.</span><span class="sxs-lookup"><span data-stu-id="4b854-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="4b854-151">**%% lokalnego** określono, że kod hello w kolejnych wierszy jest wykonywane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="4b854-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="4b854-152">Kod musi być prawidłowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="4b854-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="4b854-153">**%% sql -o<variable name>**</span><span class="sxs-lookup"><span data-stu-id="4b854-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="4b854-154">Wykonuje zapytanie Hive względem element sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="4b854-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="4b854-155">Jeśli parametr -o hello jest przekazywany, w hello jest trwały hello wynik zapytania hello %% lokalny kontekst Python jako Pandas dataframe.</span><span class="sxs-lookup"><span data-stu-id="4b854-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="4b854-156">Dla więcej informacji na temat jądra hello notesów Jupyter i hello wstępnie zdefiniowane "magics" który zapewniają, zobacz [jądra dostępne dla notesu Jupyter klastrze HDInsight Spark w systemie Linux klastrów HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="4b854-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="4b854-157">Pozyskiwania danych i Utwórz ramkę, oczyszczony danych</span><span class="sxs-lookup"><span data-stu-id="4b854-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="4b854-158">Ta sekcja zawiera kod hello szereg zadań wymaganych tooingest hello danych toobe oceniane.</span><span class="sxs-lookup"><span data-stu-id="4b854-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="4b854-159">Przeczytaj w dołączonym do 0,1% próbka hello taksówki podróży i taryfy pliku (przechowywane jako plik .tsv), dane hello formatu, a następnie tworzy ramkę Wyczyść dane.</span><span class="sxs-lookup"><span data-stu-id="4b854-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="4b854-160">pliki podróży i taryfy taksówki Hello zostały dołączone oparte na na powitania procedury zawarte w: [hello proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="4b854-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4b854-161">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-161">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-162">Czas trwania tooexecute nad komórką: 46.37 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="4b854-163">Przygotowanie danych do oceniania w łączniku Spark</span><span class="sxs-lookup"><span data-stu-id="4b854-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="4b854-164">W tej sekcji przedstawiono sposób tooindex, kodowanie i skalować tooprepare podzielone na kategorie funkcji go do użycia w algorytmów uczenia nadzorowanego MLlib dla funkcji klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="4b854-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="4b854-165">Funkcja transformacji: indeks i kodowania podzielone na kategorie funkcje dla danych wejściowych do modeli wyników.</span><span class="sxs-lookup"><span data-stu-id="4b854-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="4b854-166">W tej sekcji przedstawiono sposób tooindex podzielone na kategorie danych przy użyciu `StringIndexer` i funkcji przy użyciu kodowania `OneHotEncoder` hello modeli danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4b854-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="4b854-167">Witaj [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) koduje kolumny ciąg etykiety tooa kolumny indeksów etykiety.</span><span class="sxs-lookup"><span data-stu-id="4b854-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="4b854-168">indeksy Hello są uporządkowane według częstotliwości etykiety.</span><span class="sxs-lookup"><span data-stu-id="4b854-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="4b854-169">Witaj [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mapy kolumny etykiety indeksów tooa kolumny wektorów binarnego z co najwyżej jedną co wartość.</span><span class="sxs-lookup"><span data-stu-id="4b854-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="4b854-170">Ten typ kodowania umożliwia algorytmy, które oczekują ciągłego ważnych funkcji, takich jak Regresja logistyczna funkcji toocategorical toobe zastosowane.</span><span class="sxs-lookup"><span data-stu-id="4b854-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4b854-171">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-171">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-172">Czas trwania tooexecute nad komórką: 5.37 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="4b854-173">Tworzenie obiektów RDD z tablicami funkcji dla danych wejściowych do modeli</span><span class="sxs-lookup"><span data-stu-id="4b854-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="4b854-174">Ta sekcja zawiera kod, który pokazuje jak dane tekstowe podzielone na kategorie tooindex jako RDD obiektu i hot jeden kodować je, dlatego może być używane tootrain i testowania MLlib Regresja logistyczna i modele oparta na drzewie.</span><span class="sxs-lookup"><span data-stu-id="4b854-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="4b854-175">Witaj indeksowanego dane są przechowywane w [odporność rozproszonych zestawu danych (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) obiektów.</span><span class="sxs-lookup"><span data-stu-id="4b854-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="4b854-176">Są to podstawowe abstrakcji hello w łączniku Spark.</span><span class="sxs-lookup"><span data-stu-id="4b854-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="4b854-177">Obiekt RDD reprezentuje niezmienne partycjonowanej kolekcję elementów, które może być obsługiwany przez równolegle z platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="4b854-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="4b854-178">Zawiera także kod, który pokazuje, jak hello tooscale danych za pomocą `StandardScalar` podał MLlib do użycia w regresji liniowej z stochastycznego gradientu spadku (SGD), popularnych Algorytm uczenia szeroką gamę machine learning modeli.</span><span class="sxs-lookup"><span data-stu-id="4b854-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="4b854-179">Witaj [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) jest używane tooscale hello funkcji toounit wariancji.</span><span class="sxs-lookup"><span data-stu-id="4b854-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="4b854-180">Skalowanie funkcji normalizacji danych, nazywany również temu, że funkcji z wartościami powszechnie rozchodów są nie podany nadmiernego porównać w celu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="4b854-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4b854-181">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-181">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-182">Czas trwania tooexecute nad komórką: 11.72 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="4b854-183">Wynik z hello logistyczna modelu regresji i Zapisz dane wyjściowe tooblob</span><span class="sxs-lookup"><span data-stu-id="4b854-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="4b854-184">Kod Hello w tej sekcji przedstawiono sposób tooload logistyczna Model regresji, który został zapisany na platformie Azure magazynu obiektów blob i używany w podróży taksówki toopredict czy otrzymuje poradę, wynik go z metryki standardowej klasyfikacji, a następnie zapisz i wykreślenia hello tooblob wyników Magazyn.</span><span class="sxs-lookup"><span data-stu-id="4b854-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="4b854-185">Witaj oceniane wyniki są przechowywane w obiektach RDD.</span><span class="sxs-lookup"><span data-stu-id="4b854-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4b854-186">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-186">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-187">Czas trwania tooexecute nad komórką: 19.22 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="4b854-188">Score Model regresji liniowej</span><span class="sxs-lookup"><span data-stu-id="4b854-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="4b854-189">My używamy [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain model regresji liniowej, za pomocą stochastycznego spadku gradientu (SGD) dla optymalizacji toopredict hello ilość Porada płatnej.</span><span class="sxs-lookup"><span data-stu-id="4b854-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="4b854-190">Hello kodu w tej sekcji przedstawiono sposób wynik, korzystając ze zmiennych skalowana tooload modelu regresji liniowej z magazynu obiektów blob platformy Azure, a następnie zapisz hello wyników wstecz toohello blob.</span><span class="sxs-lookup"><span data-stu-id="4b854-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="4b854-191">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-191">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-192">Czas trwania tooexecute nad komórką: 16.63 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="4b854-193">Wynik klasyfikacji i regresji losowe modeli lasu</span><span class="sxs-lookup"><span data-stu-id="4b854-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="4b854-194">Hello w tej sekcji przedstawiono sposób tooload hello zapisywania klasyfikacji i regresji losowe modeli lasu zapisane w magazynie obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz hello wyników wstecz tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="4b854-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="4b854-195">[Losowe lasów](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="4b854-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="4b854-196">Łączą wiele decyzji drzew tooreduce hello ryzyko overfitting.</span><span class="sxs-lookup"><span data-stu-id="4b854-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="4b854-197">Losowe lasów mogą obsługiwać funkcje podzielone na kategorie, rozszerzanie ustawienie wieloklasowej klasyfikacji toohello, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="4b854-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="4b854-198">Losowe lasach są jednym z hello maszyny najbardziej popularnych uczenia modele klasyfikacji i regresji.</span><span class="sxs-lookup"><span data-stu-id="4b854-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="4b854-199">[Spark.mllib](http://spark.apache.org/mllib/) obsługuje losowe lasów binarnej i wieloklasowej klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="4b854-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="4b854-200">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-200">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-201">Czas trwania tooexecute nad komórką: 31.07 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="4b854-202">Wynik klasyfikacji i regresji gradientu zwiększania drzewa modeli</span><span class="sxs-lookup"><span data-stu-id="4b854-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="4b854-203">Kod Hello w tej sekcji przedstawia sposób tooload klasyfikacji i regresji gradientu modeli drzewa zwiększanie wyniku z magazynu obiektów blob platformy Azure, wynik ich wydajności przy użyciu klasyfikatora standardowe i regresji miary, a następnie zapisz hello wyników wstecz tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="4b854-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="4b854-204">**Spark.mllib** obsługuje GBTs dla binarnego klasyfikacji i regresji przy użyciu funkcji zarówno podzielone na kategorie, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="4b854-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="4b854-205">[Gradientu drzew zwiększania](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) są komplety drzewa decyzyjnego.</span><span class="sxs-lookup"><span data-stu-id="4b854-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="4b854-206">Decyzja train GBTs wielokrotnie powtarzane drzewa toominimize funkcję utraty.</span><span class="sxs-lookup"><span data-stu-id="4b854-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="4b854-207">GBTs mogą obsługiwać funkcje podzielone na kategorie, nie wymagają funkcji skalowania i są w stanie toocapture nieliniowość i interakcje funkcji.</span><span class="sxs-lookup"><span data-stu-id="4b854-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="4b854-208">Ich można również w ustawieniu multiklasa klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="4b854-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="4b854-209">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-209">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-210">Czas trwania tooexecute nad komórką: 14.6 sekund</span><span class="sxs-lookup"><span data-stu-id="4b854-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="4b854-211">Czyszczenie obiektów z pamięci i Drukuj oceniane lokalizacje plików</span><span class="sxs-lookup"><span data-stu-id="4b854-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="4b854-212">**DANE WYJŚCIOWE:**</span><span class="sxs-lookup"><span data-stu-id="4b854-212">**OUTPUT:**</span></span>

<span data-ttu-id="4b854-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="4b854-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="4b854-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="4b854-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="4b854-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="4b854-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="4b854-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="4b854-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="4b854-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="4b854-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="4b854-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="4b854-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="4b854-219">Korzystanie z modeli Spark przy użyciu interfejsu sieci web</span><span class="sxs-lookup"><span data-stu-id="4b854-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="4b854-220">Spark zapewnia mechanizm tooremotely przesyłania zadań lub interakcyjnych zapytań przy użyciu REST interfejsu z składnik o nazwie Livy.</span><span class="sxs-lookup"><span data-stu-id="4b854-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="4b854-221">Livy jest domyślnie włączone w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b854-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="4b854-222">Aby uzyskać więcej informacji o Livy, zobacz: [Spark przesyłania zadania zdalnie przy użyciu programu Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="4b854-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="4b854-223">Możesz użyć programu Livy tooremotely przesłać zadanie wsadowe wyniki pliku, który jest przechowywany w obiekcie blob Azure, a następnie zapisuje hello wyniki tooanother blob.</span><span class="sxs-lookup"><span data-stu-id="4b854-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="4b854-224">toodo, Przekaż hello skrypt w języku Python z</span><span class="sxs-lookup"><span data-stu-id="4b854-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="4b854-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) blob toohello hello klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="4b854-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="4b854-226">Można użyć narzędzia, takiego jak **Eksploratora usługi Microsoft Azure Storage** lub **AzCopy** toocopy hello skryptu toohello klastra blob.</span><span class="sxs-lookup"><span data-stu-id="4b854-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="4b854-227">W tym przypadku możemy przekazać skryptu hello zbyt***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="4b854-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="4b854-228">Witaj klucze dostępu, które można muszą można znaleźć w portalu hello hello konta magazynu skojarzone z klastrem Spark hello.</span><span class="sxs-lookup"><span data-stu-id="4b854-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="4b854-229">Po przekazaniu plików lokalizacji toothis ten skrypt jest uruchamiany w ramach klastra Spark hello w kontekście rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="4b854-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="4b854-230">Ładuje hello modelu i uruchamia prognoz na na podstawie modelu hello plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4b854-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="4b854-231">Ten skrypt można wywoływać zdalnie, definiując prostego żądania HTTPS/REST na Livy.</span><span class="sxs-lookup"><span data-stu-id="4b854-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="4b854-232">Oto zdalnie curl polecenia tooconstruct hello HTTP żądania tooinvoke hello skrypt w języku Python.</span><span class="sxs-lookup"><span data-stu-id="4b854-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="4b854-233">Zamień CLUSTERLOGIN, CLUSTERPASSWORD, NAZWAKLASTRA hello odpowiednie wartości dla klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="4b854-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="4b854-234">Można używać dowolnego języka na powitania systemu zdalnego tooinvoke hello Spark zadania przy użyciu programu Livy za prosty wywołania protokołu HTTPS z uwierzytelnianiem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="4b854-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="4b854-235">Podczas wprowadzania to wywołanie HTTP będzie wygodne toouse hello żądań Python biblioteki, ale nie jest aktualnie zainstalowany domyślny usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4b854-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="4b854-236">Dlatego starsze bibliotek HTTP są używane zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="4b854-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="4b854-237">Oto kod języka Python hello wywołania hello HTTP:</span><span class="sxs-lookup"><span data-stu-id="4b854-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="4b854-238">Można również dodać ten kod języka Python za[usługi Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger przesyłanie zadań Spark, która wyników obiektu blob na podstawie różnych zdarzeń czasomierza, tworzenia lub aktualizacji obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4b854-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="4b854-239">Środowisko klienta wolnego kodu, należy użyć hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) partii Spark hello tooinvoke oceniania, definiując akcji HTTP na powitania **projektanta aplikacji logiki** oraz ustawienie jego parametrów.</span><span class="sxs-lookup"><span data-stu-id="4b854-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="4b854-240">Z portalu Azure, Utwórz nową aplikację logiki, wybierając **+ nowy** -> **sieci Web i mobilność** -> **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="4b854-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="4b854-241">toobring się hello **projektanta aplikacji logiki**, wprowadź nazwę hello hello aplikacji logiki i Plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="4b854-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="4b854-242">Wybierz akcję, HTTP i wprowadź parametry hello pokazano na następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="4b854-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Projektant aplikacji logiki](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="4b854-244">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="4b854-244">What's next?</span></span>
<span data-ttu-id="4b854-245">**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.</span><span class="sxs-lookup"><span data-stu-id="4b854-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

