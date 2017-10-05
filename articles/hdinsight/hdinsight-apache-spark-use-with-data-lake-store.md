---
title: "Platforma Apache Spark umożliwia analizowanie danych w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Uruchamianie zadań Spark do analizowania danych przechowywanych w usłudze Azure Data Lake Store"
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="c7fab-103">Używanie klastra Spark w usłudze HDInsight do analizy danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c7fab-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="c7fab-104">W tym samouczku użyjesz notesu Jupyter dostępne z klastrami Spark w usłudze HDInsight do uruchomienia zadania, która odczytuje dane z konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7fab-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7fab-105">Prerequisites</span></span>

* <span data-ttu-id="c7fab-106">Konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="c7fab-107">Postępuj zgodnie z instrukcjami w temacie [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7fab-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="c7fab-108">Azure klastra Spark w usłudze HDInsight z usługą Data Lake Store jako magazyn.</span><span class="sxs-lookup"><span data-stu-id="c7fab-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="c7fab-109">Postępuj zgodnie z instrukcjami w [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7fab-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="c7fab-110">Przygotowanie danych</span><span class="sxs-lookup"><span data-stu-id="c7fab-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="c7fab-111">Nie trzeba wykonać ten krok, jeśli utworzono klaster usługi HDInsight z usługą Data Lake Store jako domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="c7fab-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="c7fab-112">Procesy tworzenia klastra dodaje przykładowych danych w ramach konta usługi Data Lake Store, który należy określić podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="c7fab-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="c7fab-113">Przejdź do sekcji [klastra Spark w usłudze HDInsight użycia z usługą Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="c7fab-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="c7fab-114">Jeśli utworzono klaster usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania i obiektu Blob magazynu Azure jako domyślny magazyn, należy najpierw skopiować na przykładowych danych do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="c7fab-115">Można użyć przykładowego danych z obiektu Blob magazynu Azure skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7fab-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="c7fab-116">Można użyć [narzędzie ADLCopy](http://aka.ms/downloadadlcopy) Aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="c7fab-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="c7fab-117">Pobierz i zainstaluj narzędzie z łącza.</span><span class="sxs-lookup"><span data-stu-id="c7fab-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="c7fab-118">Otwórz wiersz polecenia i przejdź do katalogu, w którym instalowany jest AdlCopy, zwykle `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="c7fab-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="c7fab-119">Uruchom następujące polecenie, aby skopiować konkretnego obiektu blob w kontenerze źródła do usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="c7fab-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="c7fab-120">Kopiuj **HVAC.csv** o plików przykładowych danych **/HdiSamples/HdiSamples/SensorSampleData/hvac/** do konta usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="c7fab-121">Fragment kodu powinna wyglądać:</span><span class="sxs-lookup"><span data-stu-id="c7fab-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="c7fab-122">Upewnij się, że nazwy pliku i ścieżka są w tym przypadku właściwe.</span><span class="sxs-lookup"><span data-stu-id="c7fab-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="c7fab-123">Pojawi się monit o podanie poświadczeń dla subskrypcji platformy Azure, z którym masz konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="c7fab-124">Zostaną wyświetlone informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="c7fab-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="c7fab-125">Plik danych (**HVAC.csv**) zostaną skopiowane w folderze **/hvac** w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="c7fab-126">Używanie klastra Spark w usłudze HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c7fab-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="c7fab-127">W [Portalu Azure](https://portal.azure.com/) na tablicy startowej kliknij kafelek klastra Spark (jeśli został przypięty do tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="c7fab-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="c7fab-128">Możesz także przejść do klastra, wybierając polecenia **Przeglądaj wszystko** > **Klastry usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="c7fab-129">W bloku klastra Spark kliknij pozycję **Szybkie linki**, a następnie w bloku **Pulpit nawigacyjny klastra** kliknij pozycję **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="c7fab-130">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="c7fab-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7fab-131">Można również przejść do aplikacji Jupyter Notebook dla klastra, otwierając następujący adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c7fab-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="c7fab-132">Zastąp ciąg **CLUSTERNAME** nazwą klastra:</span><span class="sxs-lookup"><span data-stu-id="c7fab-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="c7fab-133">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="c7fab-133">Create a new notebook.</span></span> <span data-ttu-id="c7fab-134">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="c7fab-135">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c7fab-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="c7fab-136">Ponieważ notes został utworzony z użyciem jądra PySpark, nie ma konieczności jawnego tworzenia kontekstów.</span><span class="sxs-lookup"><span data-stu-id="c7fab-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="c7fab-137">Konteksty Spark i Hive zostaną automatycznie utworzone po uruchomieniu pierwszej komórki kodu.</span><span class="sxs-lookup"><span data-stu-id="c7fab-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="c7fab-138">Możesz zacząć od importowania typów wymaganych w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="c7fab-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="c7fab-139">W tym celu wklej poniższy fragment kodu w komórce i naciśnij klawisze **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="c7fab-140">Przy każdym uruchomieniu zadania w oprogramowaniu Jupyter w tytule okna przeglądarki sieci Web będzie wyświetlony stan **(Busy)** (Zajęty) wraz z tytułem notesu.</span><span class="sxs-lookup"><span data-stu-id="c7fab-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="c7fab-141">Widoczne będzie także pełne kółko obok tekstu **PySpark** w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c7fab-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="c7fab-142">Po zakończeniu zadania zmieni się ono w pusty okrąg.</span><span class="sxs-lookup"><span data-stu-id="c7fab-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="c7fab-143">![Stan zadania notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stan zadania notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c7fab-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="c7fab-144">Ładowanie przykładowych danych do tabeli tymczasowej przy użyciu **HVAC.csv** plik został skopiowany do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c7fab-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="c7fab-145">Ma dostęp do danych w ramach konta usługi Data Lake Store za pomocą następującego wzorca adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c7fab-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="c7fab-146">Jeśli masz usługi Data Lake Store jako domyślny magazyn HVAC.csv będą w ścieżce podobny do następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="c7fab-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="c7fab-147">Lub, można również użyć skróconą formatu podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="c7fab-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="c7fab-148">Jeśli masz usługi Data Lake Store jako dodatkowego magazynu HVAC.csv będzie w lokalizacji, w której został skopiowany, takich jak:</span><span class="sxs-lookup"><span data-stu-id="c7fab-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="c7fab-149">W pustej komórce Wklej poniższy przykładowy kod, Zastąp **MYDATALAKESTORE** z nazwy konta usługi Data Lake Store i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="c7fab-150">Ten przykład kodu rejestruje dane w tabeli tymczasowej o nazwie **hvac**.</span><span class="sxs-lookup"><span data-stu-id="c7fab-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="c7fab-151">Ponieważ używane jest jądro PySpark, można teraz bezpośrednio uruchomić zapytanie SQL w tabeli tymczasowej **hvac** utworzonej przed chwilą za pomocą polecenia magicznego `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="c7fab-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="c7fab-152">Aby uzyskać więcej informacji na temat polecenia magicznego `%%sql` oraz innych poleceń magicznych dostępnych za pośrednictwem jądra PySpark, zobacz [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="c7fab-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="c7fab-153">Po pomyślnym ukończeniu zadania domyślnie wyświetlane są następujące tabelaryczne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c7fab-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="c7fab-154">![Wyniki zapytania w tabeli danych wyjściowych](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Wyniki zapytania w tabeli danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="c7fab-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="c7fab-155">Wyniki można również przeglądać w postaci innych wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7fab-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="c7fab-156">Na przykład wykres warstwowy tych samych danych wyjściowych będzie wyglądać w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="c7fab-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="c7fab-157">![Wykres warstwowy wyników zapytania](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Wykres warstwowy wyników zapytania")</span><span class="sxs-lookup"><span data-stu-id="c7fab-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="c7fab-158">Po zakończeniu działania aplikacji należy ją zamknąć, aby zwolnić zasoby.</span><span class="sxs-lookup"><span data-stu-id="c7fab-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="c7fab-159">W tym celu w menu **File** (Plik) w notesie kliknij polecenie **Close and Halt** (Zamknij i zatrzymaj).</span><span class="sxs-lookup"><span data-stu-id="c7fab-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="c7fab-160">Spowoduje to zakończenie pracy i zamknięcie notesu.</span><span class="sxs-lookup"><span data-stu-id="c7fab-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7fab-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7fab-161">Next steps</span></span>

* [<span data-ttu-id="c7fab-162">Utwórz autonomiczny Scala aplikację do uruchamiania w klastrze Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c7fab-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c7fab-163">Narzędzia HDInsight w zestawie narzędzi Azure for IntelliJ do tworzenie aplikacji Spark dla klastra usługi HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="c7fab-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c7fab-164">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse na tworzenie aplikacji Spark dla klastra usługi HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="c7fab-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
