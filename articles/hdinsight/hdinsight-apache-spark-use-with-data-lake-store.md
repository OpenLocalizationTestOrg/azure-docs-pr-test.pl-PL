---
title: "aaaUse danych tooanalyze Apache Spark w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Uruchamianie zadań Spark tooanalyze danych przechowywanych w usłudze Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="55d6b-103">Użyj danych tooanalyze klastra Spark w usłudze HDInsight w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="55d6b-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="55d6b-104">W tym samouczku użyjesz notesu Jupyter dostępne z toorun klastry HDInsight Spark zadanie, które odczytuje dane z konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55d6b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55d6b-105">Prerequisites</span></span>

* <span data-ttu-id="55d6b-106">Konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="55d6b-107">Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55d6b-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="55d6b-108">Azure klastra Spark w usłudze HDInsight z usługą Data Lake Store jako magazyn.</span><span class="sxs-lookup"><span data-stu-id="55d6b-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="55d6b-109">Postępuj zgodnie z instrukcjami hello w [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55d6b-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="55d6b-110">Przygotowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="55d6b-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="55d6b-111">Nie trzeba tooperform ten krok po utworzeniu klastra usługi HDInsight hello z usługi Data Lake Store jako domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="55d6b-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="55d6b-112">procesy tworzenia klastra Hello dodaje konto usługi Data Lake Store hello określone podczas tworzenia klastra hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="55d6b-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="55d6b-113">Pomiń sekcję toohello [klastra Spark w usłudze HDInsight użycia z usługą Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="55d6b-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="55d6b-114">Jeśli utworzono klaster usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania i obiektu Blob magazynu Azure jako domyślny magazyn, należy najpierw skopiować przez niektóre przykładowe dane toohello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="55d6b-115">Można użyć hello przykładowych danych z obiektu Blob magazynu Azure skojarzony z klastrem usługi HDInsight hello powitalne.</span><span class="sxs-lookup"><span data-stu-id="55d6b-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="55d6b-116">Można użyć hello [narzędzie ADLCopy](http://aka.ms/downloadadlcopy) toodo tak.</span><span class="sxs-lookup"><span data-stu-id="55d6b-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="55d6b-117">Pobierz i zainstaluj narzędzie hello z hello łącza.</span><span class="sxs-lookup"><span data-stu-id="55d6b-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="55d6b-118">Otwórz wiersz polecenia i przejdź do katalogu toohello AdlCopy zainstalowanym, zwykle `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="55d6b-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="55d6b-119">Uruchom następujące polecenie toocopy hello konkretnego obiektu blob hello źródła kontenera tooa usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="55d6b-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="55d6b-120">Kopiuj hello **HVAC.csv** o plików przykładowych danych **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello konta usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="55d6b-121">fragment kodu Hello powinna wyglądać:</span><span class="sxs-lookup"><span data-stu-id="55d6b-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="55d6b-122">Upewnij się, hello pliku i nazwy ścieżki są w przypadku prawidłowego hello.</span><span class="sxs-lookup"><span data-stu-id="55d6b-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="55d6b-123">Można tooenter zostanie wyświetlony monit o poświadczenia hello hello subskrypcji platformy Azure, w którym masz konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="55d6b-124">Zostaną wyświetlone następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="55d6b-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="55d6b-125">plik danych Hello (**HVAC.csv**) zostaną skopiowane w folderze **/hvac** w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="55d6b-126">Używanie klastra Spark w usłudze HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="55d6b-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="55d6b-127">Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="55d6b-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="55d6b-128">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="55d6b-129">W bloku klastra Spark hello, kliknij **szybkie linki**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="55d6b-130">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="55d6b-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="55d6b-131">Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="55d6b-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="55d6b-132">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="55d6b-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="55d6b-133">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="55d6b-133">Create a new notebook.</span></span> <span data-ttu-id="55d6b-134">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="55d6b-135">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="55d6b-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="55d6b-136">Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie.</span><span class="sxs-lookup"><span data-stu-id="55d6b-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="55d6b-137">konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="55d6b-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="55d6b-138">Możesz zacząć od importowania typów hello wymaganych dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="55d6b-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="55d6b-139">toodo tak, Wklej hello następującego fragmentu kodu w komórce i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="55d6b-140">Za każdym razem, gdy zostanie uruchomione zadanie w oprogramowaniu Jupyter tytuł okna przeglądarki sieci web zostaną wyświetlone **(zajęty)** stan wraz z tytułem notesu hello.</span><span class="sxs-lookup"><span data-stu-id="55d6b-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="55d6b-141">Widoczne będzie także pełne kółko toohello dalej **PySpark** tekst w hello prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="55d6b-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="55d6b-142">Po zakończeniu zadania hello zmieni to tooa okrąg.</span><span class="sxs-lookup"><span data-stu-id="55d6b-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="55d6b-143">![Stan zadania notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stan zadania notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="55d6b-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="55d6b-144">Ładowanie przykładowych danych do tabeli tymczasowej przy użyciu hello **HVAC.csv** plik skopiowany toohello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55d6b-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="55d6b-145">Można uzyskać dostępu do hello danych na koncie usługi Data Lake Store hello przy użyciu hello następującego wzorca adresu URL.</span><span class="sxs-lookup"><span data-stu-id="55d6b-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="55d6b-146">Jeśli masz usługi Data Lake Store jako domyślny magazyn HVAC.csv będzie na toohello podobne ścieżki hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="55d6b-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="55d6b-147">Lub, można także użyć skróconą format hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="55d6b-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="55d6b-148">Jeśli masz usługi Data Lake Store jako dodatkowego magazynu HVAC.csv będzie w lokalizacji hello jest kopiowany, takich jak:</span><span class="sxs-lookup"><span data-stu-id="55d6b-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="55d6b-149">W pustej komórce Wklej hello poniższy przykład kodu, Zastąp **MYDATALAKESTORE** z nazwy konta usługi Data Lake Store i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="55d6b-150">Ten przykład kodu rejestruje hello danych do tabeli tymczasowej o nazwie **hvac**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="55d6b-151">Ponieważ używasz jądra PySpark, można teraz bezpośrednio uruchomić zapytanie SQL na tabeli tymczasowej hello **hvac** właśnie utworzony przy użyciu hello `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="55d6b-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="55d6b-152">Aby uzyskać więcej informacji na temat hello `%%sql` magic, a także innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="55d6b-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="55d6b-153">Po pomyślnym ukończeniu zadania hello hello następujące tabelaryczne dane wyjściowe jest wyświetlane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="55d6b-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="55d6b-154">![Wyniki zapytania w tabeli danych wyjściowych](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Wyniki zapytania w tabeli danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="55d6b-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="55d6b-155">Można również sprawdzić hello wyniki w postaci innych wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55d6b-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="55d6b-156">Na przykład wykres warstwowy powitalne samych danych wyjściowych będzie wyglądać hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="55d6b-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="55d6b-157">![Wykres warstwowy wyników zapytania](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Wykres warstwowy wyników zapytania")</span><span class="sxs-lookup"><span data-stu-id="55d6b-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="55d6b-158">Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="55d6b-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="55d6b-159">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="55d6b-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="55d6b-160">To spowoduje zamknięcie i zamknij hello notesu.</span><span class="sxs-lookup"><span data-stu-id="55d6b-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55d6b-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55d6b-161">Next steps</span></span>

* [<span data-ttu-id="55d6b-162">Tworzenie autonomicznych Scala aplikacji toorun w klastrze Apache Spark</span><span class="sxs-lookup"><span data-stu-id="55d6b-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="55d6b-163">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="55d6b-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="55d6b-164">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji dla klastra usługi HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="55d6b-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
