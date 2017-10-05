---
title: "Tworzenie klastra Apache Spark w usłudze Azure HDInsight | Microsoft Docs"
description: "Przewodnik Szybki start platformy HDInsight Spark opisujący sposób tworzenia klastra platformy Apache Spark w usłudze HDInsight."
keywords: spark quickstart,interactive spark,interactive query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="14c4e-104">Tworzenie klastra platformy Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="14c4e-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="14c4e-105">W tym artykule omówiono sposób tworzenia klastra platformy Apache Spark w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14c4e-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="14c4e-106">Aby uzyskać informacje na temat klastra Spark w usłudze HDInsight, zobacz [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14c4e-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="14c4e-107">![Diagram szybkiego startu zawierający opis czynności prowadzących do utworzenia klastra Apache Spark w usłudze Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Szybki start z projektem Spark przy użyciu Apache Spark w usłudze HDInsight. Przedstawione kroki: tworzenie klastra; uruchamianie interakcyjnych zapytań Spark")</span><span class="sxs-lookup"><span data-stu-id="14c4e-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14c4e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="14c4e-108">Prerequisites</span></span>

* <span data-ttu-id="14c4e-109">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="14c4e-109">**An Azure subscription**.</span></span> <span data-ttu-id="14c4e-110">Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14c4e-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="14c4e-111">Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="14c4e-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="14c4e-112">Tworzenie klastra HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="14c4e-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="14c4e-113">W tej sekcji tworzysz klaster HDInsight Spark przy użyciu [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="14c4e-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="14c4e-114">Aby zapoznać się z innymi metodami tworzenia klastra, zobacz temat [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="14c4e-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="14c4e-115">Kliknij poniższy obraz, aby otworzyć szablon w usłudze Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="14c4e-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="14c4e-116">Wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="14c4e-116">Enter the following values:</span></span>

    <span data-ttu-id="14c4e-117">![Tworzenie klastra HDInsight Spark przy użyciu szablonu usługi Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Tworzenie klastra Spark w usłudze HDInsight przy użyciu szablonu usługi Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="14c4e-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="14c4e-118">**Subskrypcja**: Wybierz swoją subskrypcję platformy Azure dla tego klastra.</span><span class="sxs-lookup"><span data-stu-id="14c4e-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="14c4e-119">**Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="14c4e-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="14c4e-120">Grupa zasobów służy do zarządzania zasobami platformy Azure na potrzeby projektów.</span><span class="sxs-lookup"><span data-stu-id="14c4e-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="14c4e-121">**Lokalizacja**: Wybierz lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="14c4e-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="14c4e-122">Szablon używa tej lokalizacji do tworzenia klastra oraz na potrzeby domyślnego magazynu klastra.</span><span class="sxs-lookup"><span data-stu-id="14c4e-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="14c4e-123">**Nazwa klastra**: wprowadź nazwę tworzonego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14c4e-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="14c4e-124">**Wersja platformy Spark**: wybierz pozycję **2.0** jako wersję platformy Spark, którą chcesz zainstalować w klastrze.</span><span class="sxs-lookup"><span data-stu-id="14c4e-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="14c4e-125">**Nazwa logowania i hasło klastra**: domyślna nazwa logowania to admin.</span><span class="sxs-lookup"><span data-stu-id="14c4e-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="14c4e-126">**Nazwa użytkownika i hasło SSH**.</span><span class="sxs-lookup"><span data-stu-id="14c4e-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="14c4e-127">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="14c4e-127">Write down these values.</span></span>  <span data-ttu-id="14c4e-128">Będą potrzebne później podczas korzystania z samouczka.</span><span class="sxs-lookup"><span data-stu-id="14c4e-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="14c4e-129">Wybierz pozycję **Wyrażam zgodę na powyższe warunki i postanowienia** i pozycję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij przycisk **Kup**.</span><span class="sxs-lookup"><span data-stu-id="14c4e-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="14c4e-130">Zostanie wyświetlony nowy kafelek zatytułowany Submitting deployment for Template deployment (Przesyłanie wdrożenia dla wdrożenia szablonu).</span><span class="sxs-lookup"><span data-stu-id="14c4e-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="14c4e-131">Utworzenie klastra trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="14c4e-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="14c4e-132">Problemy podczas tworzenia klastrów usługi HDInsight mogą świadczyć o braku odpowiednich uprawnień.</span><span class="sxs-lookup"><span data-stu-id="14c4e-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="14c4e-133">Aby uzyskać więcej informacji, zobacz [wymagania dotyczące kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="14c4e-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="14c4e-134">W tym artykule opisano tworzenie klastra Spark korzystającego z [obiektów blob usługi Azure Storage jako magazynu klastra](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="14c4e-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="14c4e-135">Można również utworzyć klaster platformy Spark korzystający z usługi [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) jako magazynu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="14c4e-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="14c4e-136">Aby uzyskać instrukcje, zobacz [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Tworzenie klastra HDInsight z usługą Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="14c4e-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="14c4e-137">Uruchomienie zapytania programu Hive za pomocą modułu Spark SQL</span><span class="sxs-lookup"><span data-stu-id="14c4e-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="14c4e-138">Gdy używasz notesu programu Jupyter skonfigurowanego na potrzeby klastra platformy HDInsight Spark, możesz pobrać ustawienie wstępne `sqlContext` służące do uruchamiania zapytań programu Hive przy użyciu modułu Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="14c4e-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="14c4e-139">W tej sekcji opisano sposób uruchamiania notesu programu Jupyter, a następnie uruchamiania podstawowego zapytania programu Hive.</span><span class="sxs-lookup"><span data-stu-id="14c4e-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="14c4e-140">Otwórz [portal Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="14c4e-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="14c4e-141">Jeśli wybrana została opcja przypięcia klastra do pulpitu nawigacyjnego, kliknij kafelek klastra na pulpicie nawigacyjnym, aby uruchomić blok klastra.</span><span class="sxs-lookup"><span data-stu-id="14c4e-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="14c4e-142">Jeśli klaster nie został przypięty do pulpitu nawigacyjnego, w okienku po lewej kliknij pozycję **Klastry HDInsight**, a następnie kliknij utworzony klaster.</span><span class="sxs-lookup"><span data-stu-id="14c4e-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="14c4e-143">W obszarze **Szybkie łącza** kliknij pozycję **Pulpity nawigacyjne klastra**, a następnie pozycję **Notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="14c4e-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="14c4e-144">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="14c4e-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="14c4e-145">![Otwieranie notesu programu Jupyter w celu uruchomienia interakcyjnego zapytania Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Otwieranie notesu programu Jupyter w celu uruchomienia interakcyjnego zapytania Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="14c4e-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="14c4e-146">Dostęp do notesu programu Jupyter dla klastra można również uzyskać, otwierając następujący adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="14c4e-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="14c4e-147">Zastąp ciąg **CLUSTERNAME** nazwą klastra:</span><span class="sxs-lookup"><span data-stu-id="14c4e-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="14c4e-148">Utwórz notes.</span><span class="sxs-lookup"><span data-stu-id="14c4e-148">Create a notebook.</span></span> <span data-ttu-id="14c4e-149">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="14c4e-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="14c4e-150">![Tworzenie notesu programu Jupyter w celu uruchomienia interakcyjnego zapytania Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Tworzenie notesu programu Jupyter w celu uruchomienia interakcyjnego zapytania Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="14c4e-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="14c4e-151">Zostanie utworzony i otwarty nowy notes o nazwie Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="14c4e-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="14c4e-152">Jeśli chcesz, kliknij nazwę notesu u góry, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="14c4e-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="14c4e-153">![Podawanie nazwy dla notesu programu Jupyter, z poziomu którego będzie uruchamiane interakcyjne zapytanie Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Podawanie nazwy dla notesu programu Jupyter, z poziomu którego będzie uruchamiane interakcyjne zapytanie Spark")</span><span class="sxs-lookup"><span data-stu-id="14c4e-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="14c4e-154">Wklej następujący kod do pustej komórki, a następnie naciśnij klawisze **SHIFT + ENTER**, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="14c4e-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="14c4e-155">W poniższym kodzie wyrażenie `%%sql` (zwane magicznym wyrażeniem SQL) informuje notes programu Jupyter o konieczności użycia ustawienia wstępnego `sqlContext` do uruchomienia zapytania programu Hive.</span><span class="sxs-lookup"><span data-stu-id="14c4e-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="14c4e-156">Zapytanie pobiera pierwszych 10 wierszy z tabeli programu Hive (**hivesampletable**), która jest dostępna domyślnie na wszystkich klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14c4e-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="14c4e-157">![Zapytanie programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Zapytanie programu Hive na platformie HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="14c4e-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="14c4e-158">Aby uzyskać więcej informacji na temat magicznego wyrażenia `%%sql` i wstępnie ustawionych kontekstów, zobacz [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md) (Jądra programu Jupyter dostępne dla klastra usługi HDInsight).</span><span class="sxs-lookup"><span data-stu-id="14c4e-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="14c4e-159">Podczas każdego uruchomienia zapytania w programie Jupyter w tytule okna przeglądarki internetowej wyświetlany jest stan **(Busy)** (Zajęty) wraz z tytułem notesu.</span><span class="sxs-lookup"><span data-stu-id="14c4e-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="14c4e-160">Widoczne jest także pełne kółko obok tekstu **PySpark** w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="14c4e-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="14c4e-161">Po zakończeniu zadania zmienia się ono w pusty okrąg.</span><span class="sxs-lookup"><span data-stu-id="14c4e-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="14c4e-162">Ekran powinien zostać odświeżony w celu wyświetlenia wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="14c4e-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="14c4e-163">![Wyniki zapytania programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Wyniki zapytania programu Hive na platformie HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="14c4e-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="14c4e-164">Po zakończeniu działania aplikacji zamknij notes w celu zwolnienia zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="14c4e-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="14c4e-165">W tym celu w menu **File** (Plik) w notesie kliknij polecenie **Close and Halt** (Zamknij i zatrzymaj).</span><span class="sxs-lookup"><span data-stu-id="14c4e-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="14c4e-166">Jeśli planujesz wykonać poniższe kroki w późniejszym czasie, pamiętaj, aby usunąć klaster usługi HDInsight utworzony zgodnie z tym artykułem.</span><span class="sxs-lookup"><span data-stu-id="14c4e-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="14c4e-167">Następny krok</span><span class="sxs-lookup"><span data-stu-id="14c4e-167">Next step</span></span> 

<span data-ttu-id="14c4e-168">W tym artykule omówiono sposób tworzenia klastra platformy HDInsight Spark i uruchamiania podstawowego zapytania modułu Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="14c4e-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="14c4e-169">Przejdź do następnego artykułu, aby dowiedzieć się, jak uruchamiać interakcyjne zapytania dotyczące przykładowych danych za pomocą klastra HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="14c4e-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="14c4e-170">Run interactive queries on an HDInsight Spark cluster (Uruchamianie interakcyjnych zapytań w klastrze HDInsight Spark)</span><span class="sxs-lookup"><span data-stu-id="14c4e-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



