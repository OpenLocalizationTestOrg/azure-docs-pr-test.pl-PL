---
title: "niestandardowe pakiety Maven aaaUse z Jupyter w łączniku Spark on Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku na jak notesów Jupyter tooconfigure dostępne z Spark w usłudze HDInsight clusters toouse niestandardowe pakiety Maven."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="715d2-103">Korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="715d2-104">Przy użyciu magic komórki</span><span class="sxs-lookup"><span data-stu-id="715d2-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="715d2-105">Za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="715d2-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="715d2-106">Dowiedz się, jak tooconfigure notesu Jupyter w klastrze Apache Spark w HDInsight toouse zewnętrzne społeczności-przyczyniły się **maven** pakiety, które nie są objęte poza pole hello klastra.</span><span class="sxs-lookup"><span data-stu-id="715d2-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="715d2-107">Możesz przeszukać hello [repozytorium Maven](http://search.maven.org/) dla hello pełną listę pakietów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="715d2-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="715d2-108">Można również uzyskać listę dostępnych pakietów z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="715d2-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="715d2-109">Na przykład pełną listę społeczności przyczyniły się do pakietów znajduje się w temacie [pakietów Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="715d2-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="715d2-110">W tym artykule przedstawiono sposób toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu z hello notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="715d2-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="715d2-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="715d2-111">Prerequisites</span></span>
<span data-ttu-id="715d2-112">Musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="715d2-112">You must have hello following:</span></span>

* <span data-ttu-id="715d2-113">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="715d2-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="715d2-114">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="715d2-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="715d2-115">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="715d2-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="715d2-116">Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="715d2-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="715d2-117">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="715d2-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="715d2-118">W bloku klastra Spark hello, kliknij **szybkie linki**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="715d2-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="715d2-119">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="715d2-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="715d2-120">Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="715d2-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="715d2-121">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="715d2-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="715d2-122">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="715d2-122">Create a new notebook.</span></span> <span data-ttu-id="715d2-123">Kliknij przycisk **nowy**, a następnie kliknij przycisk **Spark**.</span><span class="sxs-lookup"><span data-stu-id="715d2-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="715d2-124">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="715d2-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="715d2-125">Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="715d2-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="715d2-126">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="715d2-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="715d2-127">![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Podaj nazwę notesu hello")</span><span class="sxs-lookup"><span data-stu-id="715d2-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="715d2-128">Użyje hello `%%configure` magic tooconfigure hello notesu toouse pakietów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="715d2-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="715d2-129">W notesach, które używają pakiety zewnętrzne, upewnij się, należy wywołać hello `%%configure` magic w hello pierwszej komórki kodu.</span><span class="sxs-lookup"><span data-stu-id="715d2-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="715d2-130">Dzięki temu, że jądra hello jest skonfigurowany toouse hello pakietu przed rozpoczęciem powitalne sesji.</span><span class="sxs-lookup"><span data-stu-id="715d2-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="715d2-131">Jeśli zapomnisz tooconfigure hello jądra w pierwszej komórki hello, możesz użyć hello `%%configure` z hello `-f` parametru, ale zostanie uruchomiona ponownie hello sesji i postępu wszystkich zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="715d2-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="715d2-132">Wersja usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-132">HDInsight version</span></span> | <span data-ttu-id="715d2-133">Polecenie</span><span class="sxs-lookup"><span data-stu-id="715d2-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="715d2-134">HDInsight 3.3 i HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="715d2-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="715d2-135">Dla usługi HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="715d2-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="715d2-136">fragment Hello powyżej oczekuje współrzędne maven hello hello pakietów zewnętrznych w centralnym repozytorium Maven.</span><span class="sxs-lookup"><span data-stu-id="715d2-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="715d2-137">W tym fragmencie `com.databricks:spark-csv_2.10:1.4.0` jest hello maven Współrzędna dla **udostępnionego woluminu klastra spark** pakietu.</span><span class="sxs-lookup"><span data-stu-id="715d2-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="715d2-138">Oto konstrukcji hello współrzędnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="715d2-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="715d2-139">a.</span><span class="sxs-lookup"><span data-stu-id="715d2-139">a.</span></span> <span data-ttu-id="715d2-140">Zlokalizuj pakiet hello w hello repozytorium Maven.</span><span class="sxs-lookup"><span data-stu-id="715d2-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="715d2-141">W tym samouczku używamy [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="715d2-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="715d2-142">b.</span><span class="sxs-lookup"><span data-stu-id="715d2-142">b.</span></span> <span data-ttu-id="715d2-143">Z repozytorium hello Zbierz wartości hello **GroupId**, **ArtifactId**, i **wersji**.</span><span class="sxs-lookup"><span data-stu-id="715d2-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="715d2-144">Upewnij się, że hello wartości, które należy zebrać są zgodne z klastrem.</span><span class="sxs-lookup"><span data-stu-id="715d2-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="715d2-145">W tym przypadku użyto Scala 2.10 i Spark 1.4.0 pakietu, ale mogą być potrzebne różne wersje tooselect hello odpowiednią wersję języka Scala lub Spark w klastrze.</span><span class="sxs-lookup"><span data-stu-id="715d2-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="715d2-146">Można sprawdzić wersji języka Scala hello w klastrze, uruchamiając `scala.util.Properties.versionString` na powitania Spark Jupyter jądra lub Prześlij Spark.</span><span class="sxs-lookup"><span data-stu-id="715d2-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="715d2-147">Można sprawdzić wersji Spark hello w klastrze, uruchamiając `sc.version` na notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="715d2-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="715d2-148">![Pakiety zewnętrzne za pomocą notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "pakiety zewnętrzne za pomocą notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="715d2-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="715d2-149">c.</span><span class="sxs-lookup"><span data-stu-id="715d2-149">c.</span></span> <span data-ttu-id="715d2-150">Łączenie hello trzech wartości oddzielonych dwukropkiem (**:**).</span><span class="sxs-lookup"><span data-stu-id="715d2-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="715d2-151">Uruchom hello komórki kodu z hello `%%configure` magic.</span><span class="sxs-lookup"><span data-stu-id="715d2-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="715d2-152">Spowoduje to skonfigurowanie hello podstawowej Livy sesji toouse hello pakietu podane.</span><span class="sxs-lookup"><span data-stu-id="715d2-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="715d2-153">W kolejnych komórek hello w notesie hello można teraz używać pakietu hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="715d2-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="715d2-154">Następnie możesz uruchomić wstawki hello, jak pokazano poniżej, tooview hello danych z hello dataframe utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="715d2-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="715d2-155"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="715d2-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="715d2-156">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="715d2-157">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="715d2-157">Scenarios</span></span>
* [<span data-ttu-id="715d2-158">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="715d2-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="715d2-159">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="715d2-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="715d2-160">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="715d2-161">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="715d2-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="715d2-162">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="715d2-163">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="715d2-163">Create and run applications</span></span>
* [<span data-ttu-id="715d2-164">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="715d2-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="715d2-165">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="715d2-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="715d2-166">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="715d2-166">Tools and extensions</span></span>

* [<span data-ttu-id="715d2-167">Użyj python zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="715d2-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="715d2-168">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="715d2-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="715d2-169">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="715d2-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="715d2-170">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="715d2-171">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="715d2-172">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="715d2-173">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="715d2-173">Manage resources</span></span>
* [<span data-ttu-id="715d2-174">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="715d2-175">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="715d2-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

