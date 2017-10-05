---
title: "Kognitywnych zestaw narzędzi firmy Microsoft z Azure HDInsight Spark dla głębokości learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uczonego modelu uczenia głębokie kognitywnych zestaw narzędzi firmy Microsoft może odnosić się do zestawu danych za pomocą interfejsu API języka Python Spark w klastrze usługi Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="cefd3-103">Użyj głębokiego uczenie modelu z klastrem usługi Azure HDInsight Spark Toolkit kognitywnych firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cefd3-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="cefd3-104">W tym artykule należy wykonać poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="cefd3-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="cefd3-105">Uruchom niestandardowy skrypt, aby zainstalować w klastrze Spark w usłudze HDInsight Azure kognitywnych zestaw narzędzi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cefd3-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="cefd3-106">Przekaż notesu Jupyter do klastra Spark, aby zobaczyć, jak zastosować uczonego modelu uczenia głębokie kognitywnych zestaw narzędzi firmy Microsoft do plików za pomocą konta magazynu obiektów Blob Azure [interfejsu API języka Python Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="cefd3-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cefd3-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cefd3-107">Prerequisites</span></span>

* <span data-ttu-id="cefd3-108">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="cefd3-108">**An Azure subscription**.</span></span> <span data-ttu-id="cefd3-109">Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cefd3-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="cefd3-110">Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="cefd3-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="cefd3-111">**Azure klastra Spark w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cefd3-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="cefd3-112">W tym artykule należy utworzyć klaster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="cefd3-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="cefd3-113">Aby uzyskać instrukcje, zobacz [klastra Utwórz Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cefd3-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="cefd3-114">Jak przepływu tego rozwiązania?</span><span class="sxs-lookup"><span data-stu-id="cefd3-114">How does this solution flow?</span></span>

<span data-ttu-id="cefd3-115">To rozwiązanie jest dzielona między w tym artykule i notesu Jupyter, który należy przekazać w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="cefd3-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="cefd3-116">W tym artykule należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cefd3-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="cefd3-117">Uruchom akcję skryptu w klastrze Spark w usłudze HDInsight, aby zainstalować kognitywnych zestaw narzędzi firmy Microsoft i pakiety języka Python.</span><span class="sxs-lookup"><span data-stu-id="cefd3-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="cefd3-118">Przekaż notesu Jupyter, który uruchamia rozwiązania do klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cefd3-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="cefd3-119">Następujące pozostałe kroki są objęte notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cefd3-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="cefd3-120">Załaduj przykładowe obrazy do Spark Resiliant dystrybuowane w zestawie danych lub RDD</span><span class="sxs-lookup"><span data-stu-id="cefd3-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="cefd3-121">Ładowanie modułów i zdefiniować ustawienia</span><span class="sxs-lookup"><span data-stu-id="cefd3-121">Load modules and define presets</span></span>
   - <span data-ttu-id="cefd3-122">Pobierz zestaw danych lokalnie w klastrze Spark</span><span class="sxs-lookup"><span data-stu-id="cefd3-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="cefd3-123">Konwertowanie zestawu danych na RDD</span><span class="sxs-lookup"><span data-stu-id="cefd3-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="cefd3-124">Wynik obrazów za pomocą uczonego modelu kognitywnych Toolkit</span><span class="sxs-lookup"><span data-stu-id="cefd3-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="cefd3-125">Pobierz trenowanego modelu kognitywnych zestawu narzędzi do klastra Spark</span><span class="sxs-lookup"><span data-stu-id="cefd3-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="cefd3-126">Definiowanie funkcji, które mają być używane przez węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="cefd3-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="cefd3-127">Wynik obrazów na węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="cefd3-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="cefd3-128">Ocena dokładności modelu</span><span class="sxs-lookup"><span data-stu-id="cefd3-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="cefd3-129">Zainstaluj kognitywnych zestaw narzędzi firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cefd3-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="cefd3-130">Kognitywnych zestaw narzędzi firmy Microsoft można zainstalować w klastrze Spark przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cefd3-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="cefd3-131">Akcja skryptu używa niestandardowych skryptów do zainstalowania składników w klastrze, które nie są domyślnie dostępne.</span><span class="sxs-lookup"><span data-stu-id="cefd3-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="cefd3-132">Przy użyciu zestawu .NET SDK usługi HDInsight lub przy użyciu programu Azure PowerShell, można użyć niestandardowego skryptu z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cefd3-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="cefd3-133">Można także użyć skryptu do zainstalowania zestawu narzędzi albo w ramach tworzenia klastra, lub gdy klaster jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cefd3-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="cefd3-134">W tym artykule używamy portalu do zainstalowania zestawu narzędzi, po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="cefd3-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="cefd3-135">Aby inne sposoby uruchamiania skryptu niestandardowego, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cefd3-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="cefd3-136">Korzystanie z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cefd3-136">Using the Azure Portal</span></span>

<span data-ttu-id="cefd3-137">Aby uzyskać instrukcje na temat korzystania z portalu Azure do uruchomienia akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="cefd3-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="cefd3-138">Upewnij się, że należy podać następujące dane wejściowe, aby zainstalować kognitywnych zestaw narzędzi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cefd3-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="cefd3-139">Podaj wartość dla nazwy akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cefd3-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="cefd3-140">Aby uzyskać **Bash skryptu URI**, wprowadź `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="cefd3-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="cefd3-141">Upewnij się, uruchom skrypt tylko w przypadku węzłów head i proces roboczy i usuń zaznaczenie wszystkich innych pól wyboru.</span><span class="sxs-lookup"><span data-stu-id="cefd3-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="cefd3-142">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cefd3-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="cefd3-143">Przekaż notesu Jupyter do klastra Spark w usłudze HDInsight Azure</span><span class="sxs-lookup"><span data-stu-id="cefd3-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="cefd3-144">Aby użyć kognitywnych zestaw narzędzi firmy Microsoft z klastrem usługi Azure HDInsight Spark, należy załadować notesu Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** do klastra usługi Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="cefd3-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="cefd3-145">Ten notes jest dostępna w witrynie GitHub pod [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="cefd3-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="cefd3-146">Klonowanie repozytorium GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="cefd3-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="cefd3-147">Aby uzyskać instrukcje dotyczące klonowania, zobacz [klonowanie repozytorium](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="cefd3-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="cefd3-148">Korzystając z portalu Azure Otwórz bloku klastra Spark, który już zainicjowano obsługę administracyjną, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="cefd3-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="cefd3-149">Można również uruchomić notesu Jupyter, przechodząc do adresu URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="cefd3-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="cefd3-150">Zastąp \<clustername > o nazwie z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cefd3-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="cefd3-151">Kliknij notesu Jupyter **przekazać** w prawym górnym rogu, a następnie przejdź do lokalizacji, w którym sklonować repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="cefd3-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="cefd3-152">![Przekaż notesu Jupyter do klastra Spark w usłudze HDInsight Azure](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "notesu Jupyter przekazać do usługi Azure HDInsight Spark klastra")</span><span class="sxs-lookup"><span data-stu-id="cefd3-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="cefd3-153">Kliknij przycisk **przekazać** ponownie.</span><span class="sxs-lookup"><span data-stu-id="cefd3-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="cefd3-154">Po przekazaniu notesu kliknij nazwę notesu, a następnie postępuj zgodnie z instrukcjami w notesie dotyczące ładowania zestawu danych i wykonywać samouczka.</span><span class="sxs-lookup"><span data-stu-id="cefd3-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="cefd3-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cefd3-155">See also</span></span>
* [<span data-ttu-id="cefd3-156">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="cefd3-157">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="cefd3-157">Scenarios</span></span>
* [<span data-ttu-id="cefd3-158">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="cefd3-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cefd3-159">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="cefd3-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cefd3-160">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="cefd3-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cefd3-161">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="cefd3-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cefd3-162">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="cefd3-163">Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="cefd3-164">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cefd3-164">Create and run applications</span></span>
* [<span data-ttu-id="cefd3-165">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="cefd3-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cefd3-166">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="cefd3-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="cefd3-167">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="cefd3-167">Tools and extensions</span></span>
* [<span data-ttu-id="cefd3-168">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="cefd3-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="cefd3-169">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="cefd3-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="cefd3-170">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="cefd3-171">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cefd3-172">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="cefd3-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cefd3-173">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="cefd3-174">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="cefd3-174">Manage resources</span></span>
* [<span data-ttu-id="cefd3-175">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="cefd3-176">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cefd3-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
