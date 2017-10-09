---
title: "aaaRun interakcyjnych zapytań w klastrze Spark w usłudze HDInsight Azure | Dokumentacja firmy Microsoft"
description: "Szybki Start Spark w usłudze HDInsight w sposób klastra toocreate Apache Spark w usłudze HDInsight."
keywords: spark quickstart,interactive spark,interactive query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="9745a-104">Uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9745a-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="9745a-105">W tym artykule używamy Jupyter notebook toorun interakcyjne zapytań Spark SQL przed klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="9745a-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="9745a-106">Notesu Jupyter jest oparty na przeglądarce aplikacji, rozszerzający hello toohello interaktywna opartych na konsoli sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9745a-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="9745a-107">Aby uzyskać więcej informacji, zobacz [notesu Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="9745a-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="9745a-108">W tym samouczku, użyj hello **PySpark** jądra w toorun notesu Jupyter hello interakcyjne zapytań Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="9745a-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="9745a-109">Notesów Jupyter w klastrach HDInsight obsługuje również dwa inne jądra - **PySpark3** i **Spark**.</span><span class="sxs-lookup"><span data-stu-id="9745a-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="9745a-110">Aby uzyskać więcej informacji o jądra hello i korzyści hello **PySpark**, zobacz [klastrów jądra notesu Jupyter do użycia z platformy Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="9745a-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9745a-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9745a-111">Prerequisites</span></span>

* <span data-ttu-id="9745a-112">**Klaster usługi Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="9745a-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="9745a-113">Aby uzyskać instrukcje, zobacz [utworzyć klaster Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9745a-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="9745a-114">Tworzenie notesu Jupyter toorun interakcyjnych zapytań</span><span class="sxs-lookup"><span data-stu-id="9745a-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="9745a-115">zapytania toorun używamy przykładowych danych, które jest domyślnie dostępna w magazynie hello skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="9745a-116">Jednak należy najpierw załadować dane do Spark jako dataframe.</span><span class="sxs-lookup"><span data-stu-id="9745a-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="9745a-117">Po utworzeniu hello dataframe, można wykonać zapytania na nim za pomocą notesu Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="9745a-118">W tej sekcji można przyjrzeć się jak:</span><span class="sxs-lookup"><span data-stu-id="9745a-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="9745a-119">Rejestrowanie zestawu danych przykładowych jako Spark dataframe.</span><span class="sxs-lookup"><span data-stu-id="9745a-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="9745a-120">Uruchamianie kwerend dotyczących hello dataframe.</span><span class="sxs-lookup"><span data-stu-id="9745a-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="9745a-121">Otwórz hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9745a-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9745a-122">Jeśli zgłoszono toopin hello klastra toohello z pulpitu nawigacyjnego, kliknij Kafelek klastra hello z bloku hello pulpitu nawigacyjnego toolaunch hello klastra.</span><span class="sxs-lookup"><span data-stu-id="9745a-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="9745a-123">Jeśli nie przypiąć hello klastra toohello pulpitu nawigacyjnego, w okienku po lewej stronie powitania kliknij przycisk **klastrów usługi HDInsight**, a następnie kliknij przycisk hello klaster został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9745a-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="9745a-124">W obszarze **Szybkie łącza** kliknij pozycję **Pulpity nawigacyjne klastra**, a następnie pozycję **Notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="9745a-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="9745a-125">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="9745a-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="9745a-126">![Otwórz Jupyter notebook toorun interakcyjne Spark SQL zapytania](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Jupyter Otwórz notesu toorun interakcyjne Spark SQL zapytań")</span><span class="sxs-lookup"><span data-stu-id="9745a-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="9745a-127">Mogą również uzyskać dostęp hello Jupyter notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9745a-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="9745a-128">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="9745a-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="9745a-129">Utwórz notes.</span><span class="sxs-lookup"><span data-stu-id="9745a-129">Create a notebook.</span></span> <span data-ttu-id="9745a-130">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="9745a-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="9745a-131">![Utwórz Jupyter notebook toorun interakcyjne Spark SQL kwerendę](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "tworzenie Jupyter notebook toorun interakcyjne Spark SQL kwerendy")</span><span class="sxs-lookup"><span data-stu-id="9745a-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="9745a-132">Nowy notes jest utworzony i otwarty o nazwie hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="9745a-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="9745a-133">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="9745a-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="9745a-134">![Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z")</span><span class="sxs-lookup"><span data-stu-id="9745a-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="9745a-135">Wklej hello następujący kod w pustej komórki, a następnie naciśnij **SHIFT + ENTER** toorun hello kodu.</span><span class="sxs-lookup"><span data-stu-id="9745a-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="9745a-136">Witaj kod importuje typy hello wymagane dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="9745a-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="9745a-137">Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie.</span><span class="sxs-lookup"><span data-stu-id="9745a-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="9745a-138">konteksty Spark i Hive Hello są utworzony automatycznie po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="9745a-139">![Stan interakcyjnego zapytania Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stan interakcyjnego zapytania Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="9745a-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="9745a-140">Każdym uruchomieniu zapytania interakcyjne w oprogramowaniu Jupyter, tytuł okna przeglądarki sieci web zawiera **(zajęty)** stan wraz z tytułem notesu hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="9745a-141">Zobacz też toohello dalej pełne kółko **PySpark** tekst w hello prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="9745a-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="9745a-142">Po zakończeniu zadania hello zmienia tooa okrąg.</span><span class="sxs-lookup"><span data-stu-id="9745a-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="9745a-143">Przed załadowaniem danych hello w klastrze Spark NAS Szukaj migawkę go.</span><span class="sxs-lookup"><span data-stu-id="9745a-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="9745a-144">Witaj przykładowych danych używanych w tym samouczku jest dostępna jako plik CSV we wszystkich klastrach HDInsight Spark w **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="9745a-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="9745a-145">Witaj danych przechwytuje hello zmiany temperatury w budynku.</span><span class="sxs-lookup"><span data-stu-id="9745a-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="9745a-146">Oto hello kilka pierwszych wierszy hello danych.</span><span class="sxs-lookup"><span data-stu-id="9745a-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="9745a-147">![Migawki danych do interaktywnego zapytań Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "migawki danych do interaktywnego zapytań Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="9745a-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="9745a-148">Tworzenie dataframe i tabeli tymczasowej (**hvac**), uruchamiając hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="9745a-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="9745a-149">W tym samouczku firma Microsoft nie twórz wszystkie hello kolumn w tabeli tymczasowej hello jako kolumny w porównaniu toohello w hello dane pierwotne w formacie CSV.</span><span class="sxs-lookup"><span data-stu-id="9745a-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="9745a-150">Po utworzeniu tabeli hello, uruchom zapytanie interakcyjne na powitania danych, użyj następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="9745a-151">Ponieważ używasz jądra PySpark, można teraz bezpośrednio uruchomić interakcyjne zapytania SQL w tabeli tymczasowej hello **hvac** utworzony przy użyciu hello `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="9745a-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="9745a-152">Aby uzyskać więcej informacji na temat hello `%%sql` magic i innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="9745a-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="9745a-153">Domyślnie powoduje wyświetlenie Hello następujące tabelaryczne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9745a-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="9745a-154">![Tabela wyjściowa wyników interakcyjnego zapytania Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela wyjściowa wyników interakcyjnego zapytania Spark")</span><span class="sxs-lookup"><span data-stu-id="9745a-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="9745a-155">Można również sprawdzić hello wyniki w postaci innych wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="9745a-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="9745a-156">Na przykład wykres warstwowy powitalne samych danych wyjściowych będzie wyglądać hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="9745a-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="9745a-157">![Wykres warstwowy wyników interakcyjnego zapytania Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Wykres warstwowy wyników interakcyjnego zapytania Spark")</span><span class="sxs-lookup"><span data-stu-id="9745a-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="9745a-158">Zamknij zasobów klastra hello toorelease notesu powitania po zakończeniu działania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9745a-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="9745a-159">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="9745a-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="9745a-160">Następny krok</span><span class="sxs-lookup"><span data-stu-id="9745a-160">Next step</span></span>

<span data-ttu-id="9745a-161">W niniejszym artykule możesz przedstawiono sposób toorun interakcyjnych zapytań w łączniku Spark przy użyciu notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="9745a-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="9745a-162">Przejdź dalej toosee artykułu toohello, jak można ściągnąć hello danych zarejestrowanych w łączniku Spark do narzędzia analytics analizy Biznesowej, takich jak Power BI i Tableau.</span><span class="sxs-lookup"><span data-stu-id="9745a-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="9745a-163">Platforma Spark BI z usługą Azure HDInsight przy użyciu narzędzi do wizualizacji danych</span><span class="sxs-lookup"><span data-stu-id="9745a-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




