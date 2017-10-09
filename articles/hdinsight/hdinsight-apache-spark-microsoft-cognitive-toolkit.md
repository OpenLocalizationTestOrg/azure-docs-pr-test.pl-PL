---
title: "aaaMicrosoft kognitywnych Toolkit z usługi Azure HDInsight Spark dla głębokości learning | Dokumentacja firmy Microsoft"
description: "Dowiedzieć się, jak przeszkolone kognitywnych zestaw narzędzi firmy Microsoft głębokie uczenie modelu mogą być zastosowane tooa zestawu danych za pomocą hello interfejsu API języka Python Spark w klastrze usługi Azure HDInsight Spark."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="f989e-103">Użyj głębokiego uczenie modelu z klastrem usługi Azure HDInsight Spark Toolkit kognitywnych firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="f989e-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="f989e-104">W tym artykule hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f989e-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="f989e-105">Uruchomienie skryptu niestandardowego tooinstall kognitywnych zestaw narzędzi firmy Microsoft w klastrze Spark w usłudze HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="f989e-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="f989e-106">Jak przekazać toosee klastra Spark toohello Jupyter notebook tooapply przeszkolone kognitywnych zestaw narzędzi firmy Microsoft głębokie uczenia modelu toofiles na koncie magazynu obiektów Blob Azure przy użyciu hello [interfejsu API języka Python Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="f989e-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f989e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f989e-107">Prerequisites</span></span>

* <span data-ttu-id="f989e-108">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="f989e-108">**An Azure subscription**.</span></span> <span data-ttu-id="f989e-109">Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f989e-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="f989e-110">Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="f989e-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="f989e-111">**Azure klastra Spark w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f989e-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="f989e-112">W tym artykule należy utworzyć klaster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="f989e-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="f989e-113">Aby uzyskać instrukcje, zobacz [klastra Utwórz Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f989e-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="f989e-114">Jak przepływu tego rozwiązania?</span><span class="sxs-lookup"><span data-stu-id="f989e-114">How does this solution flow?</span></span>

<span data-ttu-id="f989e-115">To rozwiązanie jest dzielona między w tym artykule i notesu Jupyter, który należy przekazać w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f989e-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="f989e-116">W tym artykule możesz wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f989e-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="f989e-117">Uruchom akcję skryptu w klastrze Spark w usłudze HDInsight tooinstall pakietów kognitywnych zestaw narzędzi firmy Microsoft i Python.</span><span class="sxs-lookup"><span data-stu-id="f989e-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="f989e-118">Przekaż notesu Jupyter hello uruchomioną hello toohello rozwiązanie klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f989e-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="f989e-119">Witaj następujące pozostałe kroki są objęte hello notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f989e-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="f989e-120">Załaduj przykładowe obrazy do Spark Resiliant dystrybuowane w zestawie danych lub RDD</span><span class="sxs-lookup"><span data-stu-id="f989e-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="f989e-121">Ładowanie modułów i zdefiniować ustawienia</span><span class="sxs-lookup"><span data-stu-id="f989e-121">Load modules and define presets</span></span>
   - <span data-ttu-id="f989e-122">Pobierz zestaw danych hello lokalnie w klastrze Spark hello</span><span class="sxs-lookup"><span data-stu-id="f989e-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="f989e-123">Konwertowanie hello dataset RDD</span><span class="sxs-lookup"><span data-stu-id="f989e-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="f989e-124">Wynik hello obrazów za pomocą uczonego modelu kognitywnych Toolkit</span><span class="sxs-lookup"><span data-stu-id="f989e-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="f989e-125">Pobierz klastra Spark toohello hello uczony kognitywnych Toolkit modelu</span><span class="sxs-lookup"><span data-stu-id="f989e-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="f989e-126">Zdefiniuj toobe funkcje używane przez węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f989e-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="f989e-127">Obrazy hello wynik w węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f989e-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="f989e-128">Ocena dokładności modelu</span><span class="sxs-lookup"><span data-stu-id="f989e-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="f989e-129">Zainstaluj kognitywnych zestaw narzędzi firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="f989e-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="f989e-130">Kognitywnych zestaw narzędzi firmy Microsoft można zainstalować w klastrze Spark przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="f989e-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="f989e-131">Akcja skryptu używa niestandardowych skryptów tooinstall składników w klastrze hello, które nie są domyślnie dostępne.</span><span class="sxs-lookup"><span data-stu-id="f989e-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="f989e-132">Przy użyciu zestawu .NET SDK usługi HDInsight lub przy użyciu programu Azure PowerShell, można użyć skryptu niestandardowego hello z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f989e-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="f989e-133">Umożliwia także hello skryptu tooinstall hello toolkit albo w ramach tworzenia klastra, lub po hello klastrowania jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f989e-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="f989e-134">W tym artykule używamy zestawu narzędzi hello portalu tooinstall hello, po utworzeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f989e-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="f989e-135">Inne sposoby toorun hello niestandardowego skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f989e-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="f989e-136">Przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f989e-136">Using hello Azure Portal</span></span>

<span data-ttu-id="f989e-137">Aby uzyskać instrukcje dotyczące sposobu toorun Azure Portal hello toouse skryptu akcji, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="f989e-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="f989e-138">Upewnij się, że podajesz hello następujące dane wejściowe tooinstall kognitywnych zestaw narzędzi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f989e-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="f989e-139">Podaj wartość dla nazwy akcji skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="f989e-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="f989e-140">Aby uzyskać **Bash skryptu URI**, wprowadź `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="f989e-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="f989e-141">Upewnij się, uruchamiasz skryptu hello na powitania head i proces roboczy węzłów i usuń zaznaczenie wszystkich hello inne pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="f989e-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="f989e-142">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f989e-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="f989e-143">Przekaż tooAzure notesu Jupyter hello klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="f989e-144">Witaj toouse kognitywnych zestaw narzędzi firmy Microsoft hello Azure HDInsight Spark klastra, należy załadować notesu Jupyter hello **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark klastra.</span><span class="sxs-lookup"><span data-stu-id="f989e-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="f989e-145">Ten notes jest dostępna w witrynie GitHub pod [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="f989e-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="f989e-146">Repozytorium GitHub hello w klonowania [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="f989e-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="f989e-147">Aby tooclone instrukcje, zobacz [klonowanie repozytorium](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="f989e-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="f989e-148">Z hello portalu Azure, otwórz hello bloku klastra Spark, który już zainicjowano obsługę administracyjną, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="f989e-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="f989e-149">Można również uruchomić notesu Jupyter hello korzystając z adresu toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="f989e-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="f989e-150">Zastąp \<clustername > o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f989e-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="f989e-151">Z notesu Jupyter hello, kliknij przycisk **przekazać** w prawym górnym rogu Witaj, a następnie przejdź toohello lokalizacji, gdzie sklonować repozytorium GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="f989e-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="f989e-152">![Przekaż tooAzure notesu Jupyter klastra Spark w usłudze HDInsight](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure notesu Jupyter przekazać klastra Spark w usłudze HDInsight")</span><span class="sxs-lookup"><span data-stu-id="f989e-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="f989e-153">Kliknij przycisk **przekazać** ponownie.</span><span class="sxs-lookup"><span data-stu-id="f989e-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="f989e-154">Po przekazaniu notesu hello kliknij nazwę notesu hello hello, a następnie wykonaj instrukcje hello w notesie hello, sam na jak tooload hello zestawu danych i wykonywać hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="f989e-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="f989e-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f989e-155">See also</span></span>
* [<span data-ttu-id="f989e-156">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f989e-157">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="f989e-157">Scenarios</span></span>
* [<span data-ttu-id="f989e-158">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="f989e-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f989e-159">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="f989e-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f989e-160">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f989e-161">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f989e-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f989e-162">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="f989e-163">Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f989e-164">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f989e-164">Create and run applications</span></span>
* [<span data-ttu-id="f989e-165">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="f989e-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f989e-166">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="f989e-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f989e-167">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f989e-167">Tools and extensions</span></span>
* [<span data-ttu-id="f989e-168">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="f989e-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f989e-169">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="f989e-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f989e-170">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f989e-171">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f989e-172">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="f989e-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f989e-173">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f989e-174">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="f989e-174">Manage resources</span></span>
* [<span data-ttu-id="f989e-175">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f989e-176">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f989e-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
