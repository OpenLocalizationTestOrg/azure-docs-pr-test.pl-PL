---
title: "BI Spark przy użyciu narzędzi do wizualizacji danych w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użycie narzędzi do wizualizacji danych analytics przy użyciu analizy Biznesowej programu Apache Spark w klastrach HDInsight"
keywords: "Platforma spark jest Apache spark analizy biznesowej, spark analizy biznesowej, spark wizualizację danych, analiza biznesowa"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="a8ab8-104">Apache Spark BI z usługą Azure HDInsight przy użyciu narzędzi do wizualizacji danych</span><span class="sxs-lookup"><span data-stu-id="a8ab8-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="a8ab8-105">Dowiedz się, jak używać narzędzi wizualizacji danych, takich jak Power BI i Tableau do analizowania zestawu danych pierwotnych próbki przy użyciu Apache Spark w usłudze BI w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab8-106">Łączność z narzędzi do analizy Biznesowej opisane w tym artykule nie jest obsługiwana na 2.1 Spark on Azure HDInsight 3,6 Preview.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="a8ab8-107">Tylko Spark w wersji 1.6 i 2.0 (HDInsight 3.4, 3.5 odpowiednio) są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="a8ab8-108">W tym samouczku jest również dostępny jako notesu Jupyter w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="a8ab8-109">Środowisko notesu umożliwia uruchamianie fragmenty kodu języka Python z notesu samej siebie.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="a8ab8-110">Aby wykonać samouczek z poziomu Notes, tworzenie klastra Spark, uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), a następnie uruchom notesu **narzędzi do analizy Biznesowej użycia z platformy Apache Spark w HDInsight.ipynb** w obszarze **Python** folderu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8ab8-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a8ab8-111">Prerequisites</span></span>

* <span data-ttu-id="a8ab8-112">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a8ab8-113">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="a8ab8-114"><a name="hivetable"></a>Przygotowanie danych do wizualizacji danych Spark</span><span class="sxs-lookup"><span data-stu-id="a8ab8-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="a8ab8-115">W tej sekcji użyjesz [Jupyter](https://jupyter.org) notesu z klastra Spark w usłudze HDInsight do uruchomienia zadań, które przetwarzają przykładowe nieprzetworzone dane i zapisz go jako tabelę.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="a8ab8-116">Dane przykładowe są plik CSV (hvac.csv) dostępne na wszystkich klastrach domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="a8ab8-117">Gdy dane są zapisywane jako tabelę, w następnej sekcji używamy narzędzi do analizy Biznesowej Aby podłączyć się do tabeli i wykonać wizualizacje danych.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab8-118">Jeśli kroki są wykonywane w tym artykule po ukończeniu instrukcjami [uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-load-data-run-query.md), możesz przejść do kroku 8 poniżej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="a8ab8-119">W witrynie [Azure Portal](https://portal.azure.com/) na tablicy startowej kliknij kafelek klastra Spark (jeśli został przypięty do tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="a8ab8-120">Możesz także przejść do klastra, wybierając polecenia **Przeglądaj wszystko** > **Klastry usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="a8ab8-121">W bloku klastra Spark kliknij pozycję **Pulpit nawigacyjny klastra**, a następnie opcję **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="a8ab8-122">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8ab8-123">Można również przejść do aplikacji Jupyter Notebook dla klastra, otwierając następujący adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="a8ab8-124">Zastąp ciąg **CLUSTERNAME** nazwą klastra:</span><span class="sxs-lookup"><span data-stu-id="a8ab8-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="a8ab8-125">Utwórz notes.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-125">Create a notebook.</span></span> <span data-ttu-id="a8ab8-126">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="a8ab8-127">![Tworzenie notesu Jupyter dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "tworzenie notesu Jupyter do analizy Biznesowej programu Apache Spark")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="a8ab8-128">Zostanie utworzony i otwarty nowy notes o nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="a8ab8-129">Kliknij nazwę notesu u góry, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="a8ab8-130">![Podaj nazwę notesu dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "podanie nazwy notesu Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="a8ab8-131">Ponieważ notes został utworzony z użyciem jądra PySpark, nie ma konieczności jawnego tworzenia kontekstów.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="a8ab8-132">Konteksty Spark i Hive są automatycznie tworzone po uruchomieniu pierwszej komórki kodu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="a8ab8-133">Możesz zacząć od importowania typów wymaganych w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="a8ab8-134">Aby to zrobić, umieść kursor w komórce i naciśnij klawisze **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="a8ab8-135">Załaduj przykładowe dane do tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="a8ab8-136">Podczas tworzenia klastra Spark w usłudze HDInsight przykładowy plik danych **hvac.csv** jest kopiowany do skojarzonego konta magazynu pod adresem **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="a8ab8-137">W pustej komórce Wklej następujący fragment kodu i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="a8ab8-138">Ta Wstawka kodu rejestruje dane w tabeli o nazwie **hvac**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="a8ab8-139">Sprawdź, czy tabela została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="a8ab8-140">Można użyć `%%sql` magic do uruchomienia Hive wysyła zapytanie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="a8ab8-141">Aby uzyskać więcej informacji na temat polecenia magicznego `%%sql` oraz innych poleceń magicznych dostępnych za pośrednictwem jądra PySpark, zobacz [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="a8ab8-142">Pojawić się dane wyjściowe, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a8ab8-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="a8ab8-143">Tylko tabele, które mają wartość false w obszarze **isTemporary** kolumny są tabele programu hive są przechowywane w potrzeby magazynu metadanych, które są dostępne z narzędzi do analizy Biznesowej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="a8ab8-144">W tym samouczku połączyć się z **hvac** utworzyliśmy tabeli.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="a8ab8-145">Sprawdź, czy tabela zawiera dane przeznaczone.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="a8ab8-146">W pustej komórce w notesie, skopiuj poniższy fragment kodu i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="a8ab8-147">Zamknij aby zwolnić zasoby.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="a8ab8-148">W tym celu w menu **File** (Plik) w notesie kliknij polecenie **Close and Halt** (Zamknij i zatrzymaj).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="a8ab8-149"><a name="powerbi"></a>Użyj usługi Power BI dla Spark wizualizacji danych</span><span class="sxs-lookup"><span data-stu-id="a8ab8-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab8-150">Ta sekcja ma zastosowanie tylko do wersji 1.6 Spark w usłudze HDInsight w wersji 3.4 i 2.0 Spark w usłudze HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="a8ab8-151">Po zapisaniu dane jako tabelę, można użyć usługi Power BI, aby podłączyć się do danych i wizualizacji, aby utworzyć raporty, pulpity nawigacyjne,... itd.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="a8ab8-152">Upewnij się, że masz dostęp do usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="a8ab8-153">Możesz uzyskać bezpłatne sprawdzenie subskrypcji usługi Power BI z [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="a8ab8-154">Zaloguj się do [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="a8ab8-155">W dolnej części okienka po lewej stronie, kliknij przycisk **Pobierz dane**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="a8ab8-156">Na **Pobierz dane** w obszarze **importu lub Połącz z danymi**, dla **baz danych**, kliknij przycisk **uzyskać**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="a8ab8-157">![Pobieranie danych do usługi Power BI dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "pobieranie danych do usługi Power BI dla Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="a8ab8-158">Na następnym ekranie kliknij **Spark w usłudze Azure HDInsight** , a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="a8ab8-159">Po wyświetleniu monitu wprowadź adres URL klastra (`mysparkcluster.azurehdinsight.net`) oraz poświadczenia, aby połączyć się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="a8ab8-160">![Nawiązania połączenia platformy Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "nawiązać Apache Spark analizy Biznesowej")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="a8ab8-161">Po nawiązaniu połączenia usługi Power BI uruchamia importowania danych z klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="a8ab8-162">Usługa Power BI importuje dane i dodaje **Spark** zestawu danych w obszarze **zestawów danych** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="a8ab8-163">Kliknij zestaw danych, aby otworzyć nowy arkusz do wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="a8ab8-164">Można także zapisać arkusza jako raport.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="a8ab8-165">Aby zapisać arkusza z **pliku** menu, kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="a8ab8-166">![Apache Spark w usłudze BI kafelka pulpitu nawigacyjnego usługi Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark w usłudze BI kafelka pulpitu nawigacyjnego usługi Power BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="a8ab8-167">Zwróć uwagę, że **pola** listy na liście prawym **hvac** tabeli utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="a8ab8-168">Rozwiń tabeli, aby wyświetlić pola w tabeli, zgodnie z definicją w notesie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="a8ab8-169">![Lista tabel na pulpicie nawigacyjnym Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "listy tabel na pulpicie nawigacyjnym Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="a8ab8-170">Tworzenie wizualizacji, aby pokazać różnica między temperatury docelowych i rzeczywistego temperatury dla każdego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="a8ab8-171">Do wizualizacji danych yoru, wybierz **wykres warstwowy** (pokazywaną w czerwonym prostokątem).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="a8ab8-172">Aby zdefiniować oś, przeciągnij i upuść **BuildingID** pole w obszarze **osi**, i **ActualTemp**/**TargetTemp** pól w obszarze **wartość**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="a8ab8-173">![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="a8ab8-174">Domyślnie wizualizację zawiera sumę dla **ActualTemp** i **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="a8ab8-175">Zarówno w przypadku pól z listy rozwijanej wybierz **średni** można uzyskać zarówno budynków średniej rzeczywistego i temperatury docelowej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="a8ab8-176">![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="a8ab8-177">Twoje wizualizacji danych powinna być podobny do przedstawionego na zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="a8ab8-178">Przesuń kursor nad wizualizacji uzyskanie etykietki narzędzi z właściwymi danymi.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="a8ab8-179">![Tworzenie wizualizacji danych przy użyciu Apache Spark w usłudze BI Spark](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "wizualizacje danych utworzyć Spark przy użyciu Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="a8ab8-180">Kliknij przycisk **zapisać** z górnego menu i podaj nazwę raportu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="a8ab8-181">Możesz również przypiąć element wizualny.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-181">You can also pin the visual.</span></span> <span data-ttu-id="a8ab8-182">Przypnij wizualizacje, są przechowywane na pulpicie nawigacyjnym, więc można śledzić najpóźniejszą wartość jeden rzut oka.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="a8ab8-183">Możesz dodać dowolną liczbę wizualizacji do tego samego zestawu danych a przypiąć je do pulpitu nawigacyjnego dla migawki danych.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="a8ab8-184">Ponadto klastry Spark w usłudze HDInsight są podłączone do usługi Power BI bezpośrednio połączenia.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="a8ab8-185">Daje to pewność, że usługi Power BI zawsze ma najbardziej aktualne dane z klastra, dzięki czemu nie trzeba zaplanować odświeżania dla zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="a8ab8-186"><a name="tableau"></a>Za pomocą pulpitu Tableau dla Spark wizualizacji danych</span><span class="sxs-lookup"><span data-stu-id="a8ab8-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab8-187">Ta sekcja dotyczy tylko klastry Spark 1.5.2 utworzone w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="a8ab8-188">Zainstaluj [pulpitu Tableau](http://www.tableau.com/products/desktop) na komputerze, na którym są uruchomione w tym samouczku Apache Spark w usłudze BI.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="a8ab8-189">Upewnij się, że ten komputer ma również zainstalowanego sterownika Microsoft Spark ODBC.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="a8ab8-190">Można zainstalować sterownika z [tutaj](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="a8ab8-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="a8ab8-191">Uruchom Tableau pulpitu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="a8ab8-192">W okienku po lewej stronie, z listy serwera do nawiązania połączenia, kliknij przycisk **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="a8ab8-193">Jeśli Spark SQL nie znajduje się domyślnie w okienku po lewej stronie, możesz go znaleźć, kliknij przycisk **więcej serwerów**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="a8ab8-194">W oknie dialogowym połączenia Spark SQL Podaj wartości, jak pokazano na zrzucie ekranu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="a8ab8-195">![Połącz z klastrem usługi Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Połącz z klastrem usługi Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="a8ab8-196">Listy rozwijane uwierzytelniania **usługi Microsoft Azure HDInsight** opcjonalnie tylko w przypadku zainstalowania [sterownika Microsoft Spark ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="a8ab8-197">Na następnym ekranie z **schematu** listy rozwijanej kliknij **znaleźć** ikonę, a następnie kliknij przycisk **domyślne**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="a8ab8-198">![Znaleźć schematu dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Znajdź schematu dla Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="a8ab8-199">Dla **tabeli** kliknij **znaleźć** ikonę ponownie, aby wyświetlić listę wszystkich tabel Hive dostępne w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="a8ab8-200">Powinny pojawić się **hvac** tabeli zostały utworzone wcześniej za pomocą notesu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="a8ab8-201">![Znajdź tabeli dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "tabeli Znajdź Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="a8ab8-202">Przeciągnij i upuść tabeli polu u góry po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="a8ab8-203">TABLEAU importuje dane i wyświetla schematu jako wyróżnione przez czerwonym prostokątem.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="a8ab8-204">![Dodawanie tabel do Tableau dla Apache Spark w usłudze BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "dodanie tabel Tableau Apache Spark w usłudze BI")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="a8ab8-205">Kliknij przycisk **Sheet1 —** kartę w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="a8ab8-206">Należy wizualizacji przedstawiający średni docelowy i rzeczywistego temperatur w budynkach wszystkie dla każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="a8ab8-207">Przeciągania **data** i **tworzenia identyfikator** do **kolumn** i **rzeczywiste Temp**/**Target Temp** Aby **wierszy**.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="a8ab8-208">W obszarze **znaczniki**, wybierz pozycję **obszaru** do Użyj obszaru mapy wizualizacji danych platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="a8ab8-209">![Dodawanie pól do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Dodawanie pól do wizualizacji danych Spark")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="a8ab8-210">Domyślnie są wyświetlane pola temperatury jako agregacji.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="a8ab8-211">Jeśli chcesz wyświetlić średnia temperatura zamiast tego, możesz to zrobić z listy rozwijanej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="a8ab8-212">![Zająć średnia temperatura wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "zająć średnia temperatura Spark wizualizacji danych")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="a8ab8-213">Można również super skonfigurować jedną mapę temperatury za pośrednictwem innych uzyskanie lepszego działania różnica między temperatury rzeczywiste i docelowe.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="a8ab8-214">Przesuń wskaźnik myszy do rogu niższe obszaru mapy dopóki Zobacz kształtu uchwyt wyróżnione kolorem czerwonym kółku.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="a8ab8-215">Przeciągnij mapy do innych mapy u góry, a następnie zwolnij przycisk myszy, gdy pojawi się kształtu wyróżnione kolorem czerwonym prostokątem.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="a8ab8-216">![Scal mapy do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "scalania mapy dla Spark wizualizacji danych")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="a8ab8-217">Należy zmienić sieci wizualizacji danych, jak pokazano na zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a8ab8-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="a8ab8-218">![Dane wyjściowe TABLEAU do wizualizacji danych Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau danych wyjściowych Spark wizualizacji danych")</span><span class="sxs-lookup"><span data-stu-id="a8ab8-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="a8ab8-219">Kliknij przycisk **zapisać** można zapisać w arkuszu.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="a8ab8-220">Można tworzyć pulpity nawigacyjne i dodawać do niego co najmniej jeden arkusz.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8ab8-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8ab8-221">Next steps</span></span>

<span data-ttu-id="a8ab8-222">Do tej pory przedstawiono sposób tworzenia klastra, Utwórz Spark ramek danych wykonać zapytania o dane i następnie dostęp do danych z narzędzi do analizy Biznesowej.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="a8ab8-223">Teraz można przeglądać instrukcje dotyczące zarządzania zasobami klastra i debugowanie zadań uruchomionych w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8ab8-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="a8ab8-224">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8ab8-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a8ab8-225">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8ab8-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

