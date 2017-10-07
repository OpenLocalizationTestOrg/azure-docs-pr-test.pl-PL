---
title: "klaster aaaCreate Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Szybki Start Spark w usłudze HDInsight w sposób klastra toocreate Apache Spark w usłudze HDInsight."
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
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="47848-104">Tworzenie klastra platformy Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="47848-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="47848-105">W tym artykule dowiesz się, jak klaster toocreate Apache Spark w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47848-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="47848-106">Aby uzyskać informacje na temat klastra Spark w usłudze HDInsight, zobacz [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47848-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="47848-107">![Diagram szybkiego startu opisujące kroki toocreate klastra Apache Spark w usłudze Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "szybkiego startu Spark przy użyciu platformy Apache Spark w usłudze HDInsight. Przedstawione kroki: tworzenie klastra; uruchamianie interakcyjnych zapytań Spark")</span><span class="sxs-lookup"><span data-stu-id="47848-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47848-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47848-108">Prerequisites</span></span>

* <span data-ttu-id="47848-109">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="47848-109">**An Azure subscription**.</span></span> <span data-ttu-id="47848-110">Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47848-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="47848-111">Zobacz [Utwórz bezpłatne konto platformy Azure już dzisiaj](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="47848-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="47848-112">Tworzenie klastra HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="47848-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="47848-113">W tej sekcji tworzysz klaster HDInsight Spark przy użyciu [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="47848-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="47848-114">Aby zapoznać się z innymi metodami tworzenia klastra, zobacz temat [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="47848-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="47848-115">Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47848-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="47848-116">Wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="47848-116">Enter hello following values:</span></span>

    <span data-ttu-id="47848-117">![Tworzenie klastra HDInsight Spark przy użyciu szablonu usługi Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Tworzenie klastra Spark w usłudze HDInsight przy użyciu szablonu usługi Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="47848-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="47848-118">**Subskrypcja**: Wybierz swoją subskrypcję platformy Azure dla tego klastra.</span><span class="sxs-lookup"><span data-stu-id="47848-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="47848-119">**Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="47848-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="47848-120">Grupa zasobów jest toomanage używanych zasobów Azure dla projektów.</span><span class="sxs-lookup"><span data-stu-id="47848-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="47848-121">**Lokalizacja**: Wybierz lokalizację dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="47848-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="47848-122">Szablon Hello używa tej lokalizacji do utworzenia klastra hello również podobnie jak w przypadku magazynu klastra hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="47848-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="47848-123">**ClusterName**: Wprowadź nazwę klastra usługi HDInsight hello, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="47848-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="47848-124">**Wersja platformy Spark**: Wybierz **2.0** jako wersja hello, które mają tooinstall na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="47848-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="47848-125">**Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania to admin.</span><span class="sxs-lookup"><span data-stu-id="47848-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="47848-126">**Nazwa użytkownika i hasło SSH**.</span><span class="sxs-lookup"><span data-stu-id="47848-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="47848-127">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="47848-127">Write down these values.</span></span>  <span data-ttu-id="47848-128">Należy je później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="47848-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="47848-129">Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**, wybierz pozycję **toodashboard numeru Pin**, a następnie kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="47848-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="47848-130">Zostanie wyświetlony nowy kafelek zatytułowany Submitting deployment for Template deployment (Przesyłanie wdrożenia dla wdrożenia szablonu).</span><span class="sxs-lookup"><span data-stu-id="47848-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="47848-131">Trwa około 20 minut toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47848-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="47848-132">Jeśli napotkasz problem z tworzeniem klastrów usługi HDInsight, może to być, że nie masz hello toodo odpowiednie uprawnienia tak.</span><span class="sxs-lookup"><span data-stu-id="47848-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="47848-133">Aby uzyskać więcej informacji, zobacz [wymagania dotyczące kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="47848-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="47848-134">W tym artykule tworzy klaster Spark, która używa [obiektach blob magazynu Azure jako hello klastra magazynu](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="47848-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="47848-135">Można również utworzyć klaster Spark, która używa [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) jako hello domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="47848-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="47848-136">Aby uzyskać instrukcje, zobacz [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Tworzenie klastra HDInsight z usługą Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="47848-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="47848-137">Uruchomienie zapytania programu Hive za pomocą modułu Spark SQL</span><span class="sxs-lookup"><span data-stu-id="47848-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="47848-138">Gdy używasz notesu Jupyter skonfigurowane dla klastra Spark w usłudze HDInsight, możesz uzyskać predefiniowanego `sqlContext` służy toorun zapytań Hive przy użyciu programu Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="47848-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="47848-139">W tej sekcji omówiono sposób toostart notesu Jupyter, a następnie uruchom podstawowe zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="47848-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="47848-140">Otwórz hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="47848-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="47848-141">Jeśli zgłoszono toopin hello klastra toohello z pulpitu nawigacyjnego, kliknij Kafelek klastra hello z bloku hello pulpitu nawigacyjnego toolaunch hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47848-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="47848-142">Jeśli nie przypiąć hello klastra toohello pulpitu nawigacyjnego, w okienku po lewej stronie powitania kliknij przycisk **klastrów usługi HDInsight**, a następnie kliknij przycisk hello klaster został utworzony.</span><span class="sxs-lookup"><span data-stu-id="47848-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="47848-143">W obszarze **Szybkie łącza** kliknij pozycję **Pulpity nawigacyjne klastra**, a następnie pozycję **Notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="47848-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="47848-144">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47848-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="47848-145">![Otwórz Jupyter notebook toorun interakcyjne Spark SQL zapytania](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Jupyter Otwórz notesu toorun interakcyjne Spark SQL zapytań")</span><span class="sxs-lookup"><span data-stu-id="47848-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="47848-146">Mogą również uzyskać dostęp hello Jupyter notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="47848-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="47848-147">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="47848-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="47848-148">Utwórz notes.</span><span class="sxs-lookup"><span data-stu-id="47848-148">Create a notebook.</span></span> <span data-ttu-id="47848-149">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="47848-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="47848-150">![Utwórz Jupyter notebook toorun interakcyjne Spark SQL kwerendę](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "tworzenie Jupyter notebook toorun interakcyjne Spark SQL kwerendy")</span><span class="sxs-lookup"><span data-stu-id="47848-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="47848-151">Nowy notes jest utworzony i otwarty o nazwie hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="47848-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="47848-152">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="47848-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="47848-153">![Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z")</span><span class="sxs-lookup"><span data-stu-id="47848-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="47848-154">Wklej hello następujący kod w pustej komórki, a następnie naciśnij **SHIFT + ENTER** toorun hello kodu.</span><span class="sxs-lookup"><span data-stu-id="47848-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="47848-155">W poniższym kodzie hello `%%sql` (magic sql o nazwie hello) określa, że ustawienia wstępnego hello toouse notesu Jupyter `sqlContext` zapytanie Hive hello toorun.</span><span class="sxs-lookup"><span data-stu-id="47848-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="47848-156">Witaj zapytanie pobiera hello górne 10 wiersze z tabeli programu Hive (**hivesampletable**) nie jest dostępna domyślnie na wszystkich klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47848-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="47848-157">![Zapytanie programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Zapytanie programu Hive na platformie HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="47848-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="47848-158">Aby uzyskać więcej informacji na temat hello `%%sql` magic i hello ustawień kontekstów, zobacz [Jupyter jądra dostępne dla klastra usługi HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="47848-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="47848-159">Przy każdym uruchomieniu kwerendy w oprogramowaniu Jupyter tytuł okna przeglądarki sieci web zawiera **(zajęty)** stan wraz z tytułem notesu hello.</span><span class="sxs-lookup"><span data-stu-id="47848-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="47848-160">Zobacz też toohello dalej pełne kółko **PySpark** tekst w hello prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="47848-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="47848-161">Po zakończeniu zadania hello zmienia tooa okrąg.</span><span class="sxs-lookup"><span data-stu-id="47848-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="47848-162">ekran Hello należy odświeżyć tooshow hello zapytania w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="47848-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="47848-163">![Wyniki zapytania programu Hive na platformie HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Wyniki zapytania programu Hive na platformie HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="47848-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="47848-164">Zamknij zasobów klastra hello toorelease notesu powitania po zakończeniu działania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="47848-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="47848-165">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="47848-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="47848-166">Jeśli planujesz toocomplete hello kolejne kroki w późniejszym czasie, upewnij się, że należy usunąć klaster usługi HDInsight hello utworzony w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="47848-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="47848-167">Następny krok</span><span class="sxs-lookup"><span data-stu-id="47848-167">Next step</span></span> 

<span data-ttu-id="47848-168">W tym artykule przedstawiono sposób klastra Spark w usłudze HDInsight toocreate i wykonywania podstawowych Spark SQL zapytań.</span><span class="sxs-lookup"><span data-stu-id="47848-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="47848-169">Wcześniejsze toohello dalej toolearn artykuł jak klastra Spark w usłudze HDInsight toouse toorun interakcyjnych zapytań na przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="47848-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="47848-170">Run interactive queries on an HDInsight Spark cluster (Uruchamianie interakcyjnych zapytań w klastrze HDInsight Spark)</span><span class="sxs-lookup"><span data-stu-id="47848-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



