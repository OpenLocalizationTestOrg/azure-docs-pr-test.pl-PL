---
title: "Akcja aaaScript — Python Zainstaluj pakiety z Jupyter w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku na jak notesów Jupyter tooconfigure toouse akcji skryptu, które zostały dostępne z Spark w usłudze HDInsight clusters toouse python zewnętrznych pakietów."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="cb87e-103">Korzystanie z zewnętrznych pakietów języka Python akcji skryptu tooinstall w notesów Jupyter w klastrach Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb87e-104">Przy użyciu magic komórki</span><span class="sxs-lookup"><span data-stu-id="cb87e-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="cb87e-105">Za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="cb87e-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="cb87e-106">Dowiedz się, jak tooconfigure akcji skryptu toouse klastra Apache Spark w zewnętrznej toouse HDInsight (Linux), społeczności-przyczyniły się **python** pakiety, które nie są objęte poza pole hello klastra.</span><span class="sxs-lookup"><span data-stu-id="cb87e-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cb87e-107">Można również skonfigurować za pomocą notesu Jupyter `%%configure` Magiczna toouse pakiety zewnętrzne.</span><span class="sxs-lookup"><span data-stu-id="cb87e-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="cb87e-108">Aby uzyskać instrukcje, zobacz [korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="cb87e-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="cb87e-109">Możesz przeszukać hello [indeksu pakietów](https://pypi.python.org/pypi) dla hello pełną listę pakietów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="cb87e-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="cb87e-110">Można również uzyskać listę dostępnych pakietów z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="cb87e-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="cb87e-111">Na przykład można zainstalować pakietów dostępne za pośrednictwem [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) lub [conda forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="cb87e-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="cb87e-112">W tym artykule przedstawiono sposób tooinstall hello [TensorFlow](https://www.tensorflow.org/) pakietu przy użyciu skryptu Actoin w klastrze i używać go za pomocą notesu Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="cb87e-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb87e-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb87e-113">Prerequisites</span></span>
<span data-ttu-id="cb87e-114">Musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="cb87e-114">You must have hello following:</span></span>

* <span data-ttu-id="cb87e-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cb87e-115">An Azure subscription.</span></span> <span data-ttu-id="cb87e-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="cb87e-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="cb87e-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb87e-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="cb87e-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cb87e-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb87e-119">Jeśli nie masz już klastra Spark w usłudze HDInsight w systemie Linux, można uruchomić akcji skryptu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="cb87e-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="cb87e-120">Odwiedź stronę dokumentacji hello na [jak niestandardowe toouse skryptu akcji](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="cb87e-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="cb87e-121">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="cb87e-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="cb87e-122">Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="cb87e-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="cb87e-123">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cb87e-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="cb87e-124">W bloku klastra Spark powitania kliknij **akcji skryptu** w obszarze **użycia**.</span><span class="sxs-lookup"><span data-stu-id="cb87e-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="cb87e-125">Uruchom hello akcji niestandardowej, która instaluje TensorFlow hello węzłów głównych i węzłów procesu roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="cb87e-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="cb87e-126">skrypt bash Hello mogą być przywoływane z: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh odwiedziny hello dokumentacji w [jak niestandardowe toouse skryptu akcji](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="cb87e-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb87e-127">Istnieją dwa python instalacje hello klastra.</span><span class="sxs-lookup"><span data-stu-id="cb87e-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="cb87e-128">Platforma Spark użyje instalacji języka python Anaconda hello znajdujący się w `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="cb87e-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="cb87e-129">Odwołanie tę instalację w akcje niestandardowe za pośrednictwem `/usr/bin/anaconda/bin/pip` i `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="cb87e-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="cb87e-130">Otwórz notesu PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="cb87e-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="cb87e-131">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="cb87e-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="cb87e-132">Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="cb87e-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="cb87e-133">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="cb87e-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="cb87e-134">![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Podaj nazwę notesu hello")</span><span class="sxs-lookup"><span data-stu-id="cb87e-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="cb87e-135">Możesz teraz będzie `import tensorflow` i uruchom przykład Witaj świecie.</span><span class="sxs-lookup"><span data-stu-id="cb87e-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="cb87e-136">Toocopy kodu:</span><span class="sxs-lookup"><span data-stu-id="cb87e-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="cb87e-137">wynik Hello będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="cb87e-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="cb87e-138">![Wykonanie kodu TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow wykonanie kodu")</span><span class="sxs-lookup"><span data-stu-id="cb87e-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="cb87e-139"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cb87e-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="cb87e-140">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="cb87e-141">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="cb87e-141">Scenarios</span></span>
* [<span data-ttu-id="cb87e-142">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="cb87e-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cb87e-143">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="cb87e-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cb87e-144">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cb87e-145">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="cb87e-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cb87e-146">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="cb87e-147">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb87e-147">Create and run applications</span></span>
* [<span data-ttu-id="cb87e-148">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="cb87e-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cb87e-149">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="cb87e-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="cb87e-150">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="cb87e-150">Tools and extensions</span></span>
* [<span data-ttu-id="cb87e-151">Korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cb87e-152">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="cb87e-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="cb87e-153">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="cb87e-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="cb87e-154">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="cb87e-155">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cb87e-156">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="cb87e-157">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="cb87e-157">Manage resources</span></span>
* [<span data-ttu-id="cb87e-158">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="cb87e-159">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb87e-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
