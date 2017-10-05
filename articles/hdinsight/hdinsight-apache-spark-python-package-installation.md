---
title: "Skrypt Akcja — Python Zainstaluj pakiety z Jupyter w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku skonfigurować dostępne notesów Jupyter z klastrami Spark w usłudze HDInsight przy użyciu akcji skryptu do używania pakietów języka python zewnętrznych."
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
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="79d21-103">Aby zainstalować pakiety języka Python zewnętrzne notesów Jupyter w klastrach Apache Spark w usłudze HDInsight, użyj akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="79d21-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79d21-104">Przy użyciu magic komórki</span><span class="sxs-lookup"><span data-stu-id="79d21-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="79d21-105">Za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="79d21-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="79d21-106">Dowiedz się, jak użyć akcji skryptu do skonfigurowania klastra Apache Spark w usłudze HDInsight (Linux), do korzystania z zewnętrznego, przyczyniły się społeczności **python** pakiety, które nie są uwzględnione w poziomie pole w klastrze.</span><span class="sxs-lookup"><span data-stu-id="79d21-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="79d21-107">Można również skonfigurować za pomocą notesu Jupyter `%%configure` magic na korzystanie z zewnętrznych pakietów.</span><span class="sxs-lookup"><span data-stu-id="79d21-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="79d21-108">Aby uzyskać instrukcje, zobacz [korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="79d21-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="79d21-109">Możesz przeszukać [indeksu pakietów](https://pypi.python.org/pypi) Aby uzyskać pełną listę pakietów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="79d21-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="79d21-110">Można również uzyskać listę dostępnych pakietów z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="79d21-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="79d21-111">Na przykład można zainstalować pakietów dostępne za pośrednictwem [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) lub [conda forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="79d21-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="79d21-112">W w tym artykule przedstawiono sposób instalowania [TensorFlow](https://www.tensorflow.org/) pakietu przy użyciu skryptu Actoin w klastrze i używać go za pomocą notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="79d21-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79d21-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79d21-113">Prerequisites</span></span>
<span data-ttu-id="79d21-114">Należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="79d21-114">You must have the following:</span></span>

* <span data-ttu-id="79d21-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="79d21-115">An Azure subscription.</span></span> <span data-ttu-id="79d21-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="79d21-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="79d21-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79d21-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="79d21-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="79d21-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="79d21-119">Jeśli nie masz już klastra Spark w usłudze HDInsight w systemie Linux, można uruchomić akcji skryptu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="79d21-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="79d21-120">Odwiedź stronę dokumentacji na [sposób użycia akcji skryptu niestandardowego](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="79d21-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="79d21-121">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="79d21-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="79d21-122">W [Portalu Azure](https://portal.azure.com/) na tablicy startowej kliknij kafelek klastra Spark (jeśli został przypięty do tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="79d21-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="79d21-123">Możesz także przejść do klastra, wybierając polecenia **Przeglądaj wszystko** > **Klastry usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="79d21-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="79d21-124">W bloku klastra Spark kliknij **akcji skryptu** w obszarze **użycia**.</span><span class="sxs-lookup"><span data-stu-id="79d21-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="79d21-125">Uruchomienie akcji niestandardowej, która instaluje TensorFlow węzłów głównych i węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="79d21-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="79d21-126">Skrypt bash mogą być przywoływane z: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh odwiedź stronę dokumentacji na [sposób użycia akcji skryptu niestandardowego](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="79d21-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="79d21-127">Istnieją dwa python instalacje w klastrze.</span><span class="sxs-lookup"><span data-stu-id="79d21-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="79d21-128">Platforma Spark użyje instalacji języka python Anaconda znajdujący się w `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="79d21-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="79d21-129">Odwołanie tę instalację w akcje niestandardowe za pośrednictwem `/usr/bin/anaconda/bin/pip` i `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="79d21-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="79d21-130">Otwórz notesu PySpark Jupyter</span><span class="sxs-lookup"><span data-stu-id="79d21-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="79d21-131">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="79d21-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="79d21-132">Zostanie utworzony i otwarty nowy notes o nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="79d21-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="79d21-133">Kliknij nazwę notesu u góry, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="79d21-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="79d21-134">![Wprowadzanie nazwy notesu](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Wprowadzanie nazwy notesu")</span><span class="sxs-lookup"><span data-stu-id="79d21-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="79d21-135">Możesz teraz będzie `import tensorflow` i uruchom przykład Witaj świecie.</span><span class="sxs-lookup"><span data-stu-id="79d21-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="79d21-136">Kod do skopiowania:</span><span class="sxs-lookup"><span data-stu-id="79d21-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="79d21-137">Wynik będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="79d21-137">The result will look like this:</span></span>
    
    <span data-ttu-id="79d21-138">![Wykonanie kodu TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow wykonanie kodu")</span><span class="sxs-lookup"><span data-stu-id="79d21-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="79d21-139"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="79d21-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="79d21-140">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="79d21-141">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="79d21-141">Scenarios</span></span>
* [<span data-ttu-id="79d21-142">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="79d21-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="79d21-143">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="79d21-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="79d21-144">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="79d21-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="79d21-145">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="79d21-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="79d21-146">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="79d21-147">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="79d21-147">Create and run applications</span></span>
* [<span data-ttu-id="79d21-148">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="79d21-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="79d21-149">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="79d21-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="79d21-150">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="79d21-150">Tools and extensions</span></span>
* [<span data-ttu-id="79d21-151">Korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="79d21-152">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="79d21-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="79d21-153">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="79d21-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="79d21-154">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="79d21-155">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="79d21-156">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="79d21-157">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="79d21-157">Manage resources</span></span>
* [<span data-ttu-id="79d21-158">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="79d21-159">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="79d21-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
