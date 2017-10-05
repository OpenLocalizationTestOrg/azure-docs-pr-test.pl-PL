---
title: "Wywoływanie programów Spark z fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wywołać Spark programy z fabryki danych Azure za pomocą działania MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="4de28-103">Wywoływanie programów Spark z potoków fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="4de28-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4de28-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="4de28-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="4de28-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="4de28-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4de28-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="4de28-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4de28-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="4de28-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4de28-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4de28-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4de28-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4de28-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4de28-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4de28-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="4de28-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4de28-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4de28-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4de28-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="4de28-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="4de28-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="4de28-114">Introduction</span></span>
<span data-ttu-id="4de28-115">Działanie Spark jest jednym z [działań przekształcania danych](data-factory-data-transformation-activities.md) obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="4de28-116">To działanie uruchamia określony program Spark w klastrze Apache Spark w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4de28-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="4de28-117">Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="4de28-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="4de28-118">Działanie Spark obsługuje tylko istniejące (własne) klastry HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="4de28-119">Nie obsługuje usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="4de28-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="4de28-120">Wskazówki: tworzenie potoku z działaniem Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="4de28-121">Poniżej przedstawiono typowe etapy, aby utworzyć potok fabryki danych z działaniem Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="4de28-122">Tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-122">Create a data factory.</span></span>
2. <span data-ttu-id="4de28-123">Utwórz połączoną usługą magazynu Azure, aby połączyć magazyn Azure skojarzony z klastrem Spark w usłudze HDInsight z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="4de28-124">Tworzenie usługi Azure HDInsight połączony do połączenia klastra Apache Spark w usłudze Azure HDInsight z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="4de28-125">Tworzenie zestawu danych, który odwołuje się do połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="4de28-126">Obecnie należy określić wyjściowy zestaw danych działania nawet jeśli dostępny jest nie wytworzonych.</span><span class="sxs-lookup"><span data-stu-id="4de28-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="4de28-127">Utworzyć potok z działaniem Spark, która odwołuje się do usługi HDInsight połączone utworzone w #2.</span><span class="sxs-lookup"><span data-stu-id="4de28-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="4de28-128">Działanie jest skonfigurowany z zestawu danych, utworzony w poprzednim kroku jako wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="4de28-129">Wyjściowy zestaw danych jest podstawę harmonogram (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="4de28-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4de28-130">W związku z tym należy określić wyjściowy zestaw danych, nawet jeśli działanie nie tworzy naprawdę danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4de28-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4de28-131">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4de28-131">Prerequisites</span></span>
1. <span data-ttu-id="4de28-132">Utwórz **ogólnego przeznaczenia konta magazynu Azure** przez następujące instrukcje w tym przewodnikiem: [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4de28-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="4de28-133">Utwórz **klastra Apache Spark w usłudze Azure HDInsight** przez następujące instrukcje w samouczku: [klastra Utwórz Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4de28-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="4de28-134">Skojarz konto magazynu Azure, który został utworzony w kroku #1 z tym klastrem.</span><span class="sxs-lookup"><span data-stu-id="4de28-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="4de28-135">Pobierz i przejrzyj plik skryptu języka python **test.py** w lokalizacji: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="4de28-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="4de28-136">Przekaż **test.py** do **pyFiles** folderu w **adfspark** kontenera w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="4de28-137">Tworzenie kontenera i folderu, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="4de28-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="4de28-138">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="4de28-138">Create data factory</span></span>
<span data-ttu-id="4de28-139">Zacznijmy tworzenie fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="4de28-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="4de28-140">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4de28-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4de28-141">Kliknij przycisk **NOWY** w lewym menu, kliknij pozycję **Dane + analiza**, a następnie kliknij przycisk **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4de28-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="4de28-142">W **nowa fabryka danych** bloku, wprowadź **SparkDF** dla nazwy.</span><span class="sxs-lookup"><span data-stu-id="4de28-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4de28-143">Nazwa fabryki danych platformy Azure musi być **globalnie unikatowa**.</span><span class="sxs-lookup"><span data-stu-id="4de28-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4de28-144">Jeśli zostanie wyświetlony błąd: **nazwa fabryki danych "SparkDF" nie jest dostępny**.</span><span class="sxs-lookup"><span data-stu-id="4de28-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="4de28-145">Zmiana nazwy fabryki danych (na przykład yournameSparkDFdate i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="4de28-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="4de28-146">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="4de28-147">Wybierz **subskrypcję Azure**, w ramach której chcesz utworzyć fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="4de28-148">Wybierz istniejący **grupy zasobów** lub Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="4de28-149">Wybierz **Przypnij do pulpitu nawigacyjnego** opcji.</span><span class="sxs-lookup"><span data-stu-id="4de28-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="4de28-150">Kliknij przycisk **Utwórz** w bloku **Nowa fabryka danych**.</span><span class="sxs-lookup"><span data-stu-id="4de28-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4de28-151">Aby utworzyć wystąpienia usługi Data Factory, użytkownik musi być członkiem roli [współautora usługi Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) na poziomie subskrypcji/grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4de28-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="4de28-152">Zobacz tworzony w fabryce danych **pulpitu nawigacyjnego** portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4de28-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="4de28-153">Po pomyślnym utworzeniu fabryki danych zostanie wyświetlona strona fabryki danych z zawartością fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="4de28-154">Jeśli strona fabryki danych nie jest widoczny, kliknij Kafelek fabrykę danych na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="4de28-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Blok Fabryka danych](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="4de28-156">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="4de28-156">Create linked services</span></span>
<span data-ttu-id="4de28-157">W tym kroku utworzysz dwa połączone usługi, co do połączenia z klastrem Spark fabrykę danych i innych, aby połączyć magazyn Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4de28-158">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4de28-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="4de28-159">W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="4de28-160">Zestaw danych utworzone w kroku później w tym przewodniku odnosi się do tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4de28-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="4de28-161">Usługa HDInsight połączone definiowana w następnym kroku odwołuje się do tej połączonej usługi zbyt.</span><span class="sxs-lookup"><span data-stu-id="4de28-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="4de28-162">Kliknij przycisk **tworzenie i wdrażanie** na **fabryki danych** bloku fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="4de28-163">Powinien zostać uruchomiony Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="4de28-164">Kliknij przycisk **Nowy magazyn danych** i wybierz opcję **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="4de28-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nowy magazyn danych — Azure Storage — menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="4de28-166">Powinny pojawić się **skryptu JSON** do tworzenia usługi Azure Storage połączonej usługi w edytorze.</span><span class="sxs-lookup"><span data-stu-id="4de28-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="4de28-168">Zastąp **nazwa konta** i **klucz konta** z nazwy i klucza dostępu konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="4de28-169">Aby dowiedzieć się, jak uzyskać klucz dostępu do magazynu, zapoznaj się z informacjami na temat sposobów wyświetlania, kopiowania i ponownego generowania kluczy dostępu do magazynu w sekcji [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4de28-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="4de28-170">Aby wdrożyć połączonej usługi, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="4de28-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="4de28-171">Po pomyślnym wdrożeniu połączonej usługi okno **Wersja robocza-1** powinno zniknąć i w widoku drzewa po lewej stronie zostanie wyświetlona pozycja **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4de28-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="4de28-172">Tworzenie usługi HDInsight połączone</span><span class="sxs-lookup"><span data-stu-id="4de28-172">Create HDInsight linked service</span></span>
<span data-ttu-id="4de28-173">W tym kroku utworzysz usługi Azure HDInsight połączony do połączenia z klastrem Spark w usłudze HDInsight z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="4de28-174">Klaster usługi HDInsight służy do uruchomienia programu Spark określony w działaniu Spark potoku, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4de28-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="4de28-175">Kliknij przycisk **... Więcej** na pasku narzędzi kliknij **nowych obliczeń**, a następnie kliknij przycisk **klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4de28-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Tworzenie usługi HDInsight połączone](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="4de28-177">Skopiuj i wklej poniższy fragment kodu do okna **Wersja robocza-1**.</span><span class="sxs-lookup"><span data-stu-id="4de28-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="4de28-178">W edytorze JSON wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4de28-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="4de28-179">Określ **URI** dla klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4de28-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="4de28-180">Na przykład: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="4de28-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="4de28-181">Określ nazwę **użytkownika** kto ma dostęp do klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="4de28-182">Określ **hasło** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4de28-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="4de28-183">Określ **połączonej usługi magazynu Azure** skojarzonego z klastrem Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4de28-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="4de28-184">W tym przykładzie jest: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4de28-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="4de28-185">Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="4de28-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="4de28-186">Działanie Spark obsługuje tylko istniejące (własne) klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4de28-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="4de28-187">Nie obsługuje usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="4de28-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="4de28-188">Zobacz [połączoną usługą usługi HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) szczegółowe informacje na temat usługi HDInsight połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4de28-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="4de28-189">Aby wdrożyć połączonej usługi, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="4de28-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="4de28-190">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="4de28-190">Create output dataset</span></span>
<span data-ttu-id="4de28-191">Wyjściowy zestaw danych jest podstawę harmonogram (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="4de28-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4de28-192">W związku z tym należy określić wyjściowy zestaw danych działania spark w potoku, nawet jeśli działanie nie tworzy naprawdę żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4de28-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="4de28-193">Określenie zestawem danych wejściowych dla działania jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="4de28-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="4de28-194">W **Edytorze fabryki danych** kliknij opcję **... więcej** na pasku poleceń, kliknij opcję **Nowy zestaw danych** i wybierz opcję **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="4de28-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="4de28-195">Skopiuj i wklej poniższy fragment kodu do okna Wersja robocza-1.</span><span class="sxs-lookup"><span data-stu-id="4de28-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="4de28-196">Fragment kodu JSON definiuje zestaw danych o nazwie **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4de28-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="4de28-197">Ponadto określ że wyniki są przechowywane w kontenerze obiektów blob o nazwie **adfspark** i folder o nazwie **pyFiles/wyjścia**.</span><span class="sxs-lookup"><span data-stu-id="4de28-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="4de28-198">Jak wspomniano wcześniej, ten zestaw danych jest fikcyjny zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="4de28-199">Program Spark, w tym przykładzie nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="4de28-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="4de28-200">**Dostępności** sekcja określa, że wyjściowy zestaw danych jest tworzony codziennie.</span><span class="sxs-lookup"><span data-stu-id="4de28-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="4de28-201">Aby wdrożyć zestawu danych, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="4de28-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="4de28-202">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="4de28-202">Create pipeline</span></span>
<span data-ttu-id="4de28-203">W tym kroku możesz utworzyć potok wraz z **HDInsightSpark** działania.</span><span class="sxs-lookup"><span data-stu-id="4de28-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="4de28-204">W tym przypadku wyjściowy zestaw danych jest elementem wpływającym na ustawienia harmonogramu, więc musisz utworzyć wyjściowy zestaw danych nawet wtedy, gdy działanie nie generuje żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4de28-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="4de28-205">Jeśli w działaniu nie są używane żadne dane wejściowe, możesz pominąć tworzenie zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4de28-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="4de28-206">W związku z tym nie wejściowy zestaw danych został określony w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4de28-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="4de28-207">W **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń, a następnie kliknij **nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="4de28-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="4de28-208">Zastąp skryptu w oknie Projekt 1 następujący skrypt:</span><span class="sxs-lookup"><span data-stu-id="4de28-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="4de28-209">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="4de28-209">Note the following points:</span></span>
    - <span data-ttu-id="4de28-210">**Typu** właściwość jest ustawiona na **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="4de28-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="4de28-211">**Właściwość rootPath** ustawiono **adfspark\\pyFiles** gdzie adfspark jest kontenera obiektów Blob platformy Azure i pyFiles jest poprawnie folder, w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="4de28-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="4de28-212">W tym przykładzie magazynu obiektów Blob Azure jest skojarzony z klastrem Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="4de28-213">Można przekazać pliku do innego magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="4de28-214">Jeśli tak zrobisz, Utwórz połączoną usługą magazynu Azure, aby połączyć konto magazynu z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="4de28-215">Następnie określ jako wartość dla nazwy połączonej usługi **sparkJobLinkedService** właściwości.</span><span class="sxs-lookup"><span data-stu-id="4de28-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="4de28-216">Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwane przez działanie Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="4de28-217">**EntryFilePath** ustawiono **test.py**, czyli plik python.</span><span class="sxs-lookup"><span data-stu-id="4de28-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="4de28-218">**GetDebugInfo** właściwość jest ustawiona na **zawsze**, co oznacza, że pliki dziennika są zawsze generowany (powodzenie lub niepowodzenie).</span><span class="sxs-lookup"><span data-stu-id="4de28-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="4de28-219">Zaleca się, że nie należy ustawiać tej właściwości `Always` w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="4de28-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="4de28-220">**Generuje** sekcja ma jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="4de28-221">Należy określić wyjściowy zestaw danych, nawet jeśli spark program nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="4de28-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="4de28-222">Wyjściowy zestaw danych dysków harmonogramu dla potoku (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="4de28-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="4de28-223">Aby uzyskać szczegółowe informacje dotyczące właściwości obsługiwanych przez działanie Spark, zobacz [Spark właściwości działania](#spark-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4de28-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="4de28-224">Aby wdrożyć potok, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="4de28-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="4de28-225">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="4de28-225">Monitor pipeline</span></span>
1. <span data-ttu-id="4de28-226">Kliknij przycisk **X** aby zamknąć Edytor fabryki danych bloków i przejdź do strony głównej fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="4de28-227">Kliknij przycisk **monitorowanie i zarządzanie** można uruchomić monitorowania aplikacji w innej karty.</span><span class="sxs-lookup"><span data-stu-id="4de28-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Monitorowanie i zarządzanie nimi kafelka](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="4de28-229">Zmień **godzina rozpoczęcia** filtru na górze do **2/1/2017**i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="4de28-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="4de28-230">Tylko jedno okno działania powinny być widoczne, ponieważ istnieje tylko jeden dzień między (2017-02-01) czasu rozpoczęcia i zakończenia (2017-02-02) potoku.</span><span class="sxs-lookup"><span data-stu-id="4de28-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="4de28-231">Upewnij się, że wycinek danych jest w **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="4de28-231">Confirm that the data slice is in **ready** state.</span></span>

    ![Monitorowanie potoku](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="4de28-233">Wybierz **okno działania** aby zobaczyć szczegóły dotyczące uruchamiania działania.</span><span class="sxs-lookup"><span data-stu-id="4de28-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="4de28-234">Jeśli występuje błąd, zobaczysz szczegółowe informacje o nim w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="4de28-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="4de28-235">Sprawdź wyniki</span><span class="sxs-lookup"><span data-stu-id="4de28-235">Verify the results</span></span>

1. <span data-ttu-id="4de28-236">Uruchom **notesu Jupyter** przechodząc do klastra Spark w usłudze HDInsight: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="4de28-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="4de28-237">Można również uruchomić Pulpit nawigacyjny klastra dla klastra Spark w usłudze HDInsight, a następnie uruchom **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="4de28-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="4de28-238">Kliknij przycisk **nowy** -> **PySpark** uruchomić nowy notes.</span><span class="sxs-lookup"><span data-stu-id="4de28-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Nowego notesu Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="4de28-240">Uruchom następujące polecenie kopiowania/wklejania tekst i naciskając klawisz **SHIFT + ENTER** na końcu drugiej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="4de28-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="4de28-241">Upewnij się, że zostaną wyświetlone dane z tabeli hvac:</span><span class="sxs-lookup"><span data-stu-id="4de28-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Wyniki zapytania Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="4de28-243">Zobacz [uruchamiania zapytań Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) sekcji, aby uzyskać szczegółowe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="4de28-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="4de28-244">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="4de28-244">Troubleshooting</span></span>
<span data-ttu-id="4de28-245">Ponieważ ustawisz **getDebugInfo** do **zawsze**, zostanie wyświetlony **dziennika** podfolder **pyFiles** folderu w kontenerze obiektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4de28-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="4de28-246">Plik dziennika w folderze dziennika zawiera dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="4de28-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="4de28-247">Ten plik dziennika jest szczególnie przydatna w przypadku, gdy występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="4de28-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="4de28-248">W środowisku produkcyjnym można ustawić ją na **błąd**.</span><span class="sxs-lookup"><span data-stu-id="4de28-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="4de28-249">Aby uzyskać dodatkowe informacje o rozwiązywaniu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4de28-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="4de28-250">Przejdź do `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="4de28-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplikacja YARN interfejsu użytkownika](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="4de28-252">Kliknij przycisk **dzienniki** jednego uruchomienia prób.</span><span class="sxs-lookup"><span data-stu-id="4de28-252">Click **Logs** for one of the run attempts.</span></span>

    ![Strona aplikacji](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="4de28-254">Dodatkowe informacje o błędzie w dzienniku strony powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="4de28-254">You should see additional error information in the log page.</span></span>

    ![Błąd dziennika](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="4de28-256">Poniższe sekcje zawierają informacje na temat jednostek fabryki danych do używania klastra Apache Spark i działania Spark w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="4de28-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="4de28-257">Właściwości działania Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-257">Spark activity properties</span></span>
<span data-ttu-id="4de28-258">Oto przykład definicji JSON potoku z działaniem Spark:</span><span class="sxs-lookup"><span data-stu-id="4de28-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="4de28-259">W poniższej tabeli opisano właściwości JSON używane w definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="4de28-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="4de28-260">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4de28-260">Property</span></span> | <span data-ttu-id="4de28-261">Opis</span><span class="sxs-lookup"><span data-stu-id="4de28-261">Description</span></span> | <span data-ttu-id="4de28-262">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4de28-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4de28-263">name</span><span class="sxs-lookup"><span data-stu-id="4de28-263">name</span></span> | <span data-ttu-id="4de28-264">Nazwa działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="4de28-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="4de28-265">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-265">Yes</span></span> |
| <span data-ttu-id="4de28-266">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="4de28-266">description</span></span> | <span data-ttu-id="4de28-267">Tekst opisujący działanie robi.</span><span class="sxs-lookup"><span data-stu-id="4de28-267">Text describing what the activity does.</span></span> | <span data-ttu-id="4de28-268">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-268">No</span></span> |
| <span data-ttu-id="4de28-269">type</span><span class="sxs-lookup"><span data-stu-id="4de28-269">type</span></span> | <span data-ttu-id="4de28-270">Ta właściwość musi mieć ustawioną HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="4de28-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="4de28-271">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-271">Yes</span></span> |
| <span data-ttu-id="4de28-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4de28-272">linkedServiceName</span></span> | <span data-ttu-id="4de28-273">Nazwa usługi HDInsight połączone, na którym jest uruchomiony Spark program.</span><span class="sxs-lookup"><span data-stu-id="4de28-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="4de28-274">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-274">Yes</span></span> |
| <span data-ttu-id="4de28-275">Właściwość rootPath</span><span class="sxs-lookup"><span data-stu-id="4de28-275">rootPath</span></span> | <span data-ttu-id="4de28-276">Kontener obiektów Blob platformy Azure i folder zawierający plik Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="4de28-277">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="4de28-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="4de28-278">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-278">Yes</span></span> |
| <span data-ttu-id="4de28-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="4de28-279">entryFilePath</span></span> | <span data-ttu-id="4de28-280">Ścieżka względna do folderu głównego Spark kodu/pakietu.</span><span class="sxs-lookup"><span data-stu-id="4de28-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="4de28-281">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-281">Yes</span></span> |
| <span data-ttu-id="4de28-282">className</span><span class="sxs-lookup"><span data-stu-id="4de28-282">className</span></span> | <span data-ttu-id="4de28-283">Klasy głównym aplikacji Java/Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="4de28-284">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-284">No</span></span> |
| <span data-ttu-id="4de28-285">Argumenty</span><span class="sxs-lookup"><span data-stu-id="4de28-285">arguments</span></span> | <span data-ttu-id="4de28-286">Lista argumentów wiersza polecenia do programu Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="4de28-287">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-287">No</span></span> |
| <span data-ttu-id="4de28-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="4de28-288">proxyUser</span></span> | <span data-ttu-id="4de28-289">Konto użytkownika do personifikacji do wykonania programu Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="4de28-290">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-290">No</span></span> |
| <span data-ttu-id="4de28-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="4de28-291">sparkConfig</span></span> | <span data-ttu-id="4de28-292">Określ wartości dla właściwości konfiguracji Spark wymienione w temacie: [konfiguracji Spark — właściwości aplikacji](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="4de28-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="4de28-293">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-293">No</span></span> |
| <span data-ttu-id="4de28-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="4de28-294">getDebugInfo</span></span> | <span data-ttu-id="4de28-295">Określa, kiedy Spark pliki dziennika są kopiowane do magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4de28-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="4de28-296">Dozwolone wartości: None, zawsze lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="4de28-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="4de28-297">Wartość domyślna: Brak.</span><span class="sxs-lookup"><span data-stu-id="4de28-297">Default value: None.</span></span> | <span data-ttu-id="4de28-298">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-298">No</span></span> |
| <span data-ttu-id="4de28-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="4de28-299">sparkJobLinkedService</span></span> | <span data-ttu-id="4de28-300">Magazyn Azure połączone usługi, która ma Spark plik zadania, zależności i dzienniki.</span><span class="sxs-lookup"><span data-stu-id="4de28-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="4de28-301">Jeśli nie określisz wartości dla tej właściwości, Magazyn skojarzony z klastrem usługi HDInsight jest używany.</span><span class="sxs-lookup"><span data-stu-id="4de28-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="4de28-302">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="4de28-303">Struktura folderów</span><span class="sxs-lookup"><span data-stu-id="4de28-303">Folder structure</span></span>
<span data-ttu-id="4de28-304">Działanie Spark nie obsługuje skryptu w wierszu jako Pig i do gałęzi działań.</span><span class="sxs-lookup"><span data-stu-id="4de28-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="4de28-305">Zadań Spark jest również extensible więcej niż zadań Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="4de28-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="4de28-306">W przypadku zadań Spark, możesz podać wiele zależności takich jak jar pakietów (umieszczona w języku java ścieżki klasy), pliki języka python (dotyczącymi PYTHONPATH) i innych plików.</span><span class="sxs-lookup"><span data-stu-id="4de28-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="4de28-307">Utwórz następującą strukturę folderów w magazynie obiektów Blob platformy Azure, odwołuje się usługa HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="4de28-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="4de28-308">Natomiast przekazywanie plików zależnych do odpowiednich podfolderów w folderze głównym reprezentowany przez **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="4de28-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="4de28-309">Na przykład Przekaż python pliki są kopiowane do podfolderu pyFiles i pliki jar do podfolderu słoików folderu głównego.</span><span class="sxs-lookup"><span data-stu-id="4de28-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="4de28-310">W czasie wykonywania usługi fabryka danych oczekuje następującej struktury folderu w magazynie obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4de28-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="4de28-311">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="4de28-311">Path</span></span> | <span data-ttu-id="4de28-312">Opis</span><span class="sxs-lookup"><span data-stu-id="4de28-312">Description</span></span> | <span data-ttu-id="4de28-313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4de28-313">Required</span></span> | <span data-ttu-id="4de28-314">Typ</span><span class="sxs-lookup"><span data-stu-id="4de28-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="4de28-315">.</span><span class="sxs-lookup"><span data-stu-id="4de28-315">.</span></span> | <span data-ttu-id="4de28-316">Ścieżka katalogu głównego zadania Spark w połączonej usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="4de28-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="4de28-317">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-317">Yes</span></span> | <span data-ttu-id="4de28-318">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-318">Folder</span></span> |
| <span data-ttu-id="4de28-319">&lt;zdefiniowane przez użytkownika&gt;</span><span class="sxs-lookup"><span data-stu-id="4de28-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="4de28-320">Ścieżka do pliku wpisu zadania Spark</span><span class="sxs-lookup"><span data-stu-id="4de28-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="4de28-321">Tak</span><span class="sxs-lookup"><span data-stu-id="4de28-321">Yes</span></span> | <span data-ttu-id="4de28-322">Plik</span><span class="sxs-lookup"><span data-stu-id="4de28-322">File</span></span> |
| <span data-ttu-id="4de28-323">. / jars</span><span class="sxs-lookup"><span data-stu-id="4de28-323">./jars</span></span> | <span data-ttu-id="4de28-324">Wszystkie pliki w tym folderze są przekazywane i dotyczącymi klasy java klastra</span><span class="sxs-lookup"><span data-stu-id="4de28-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="4de28-325">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-325">No</span></span> | <span data-ttu-id="4de28-326">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-326">Folder</span></span> |
| <span data-ttu-id="4de28-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="4de28-327">./pyFiles</span></span> | <span data-ttu-id="4de28-328">Wszystkie pliki w tym folderze są przekazywane i dotyczącymi PYTHONPATH klastra</span><span class="sxs-lookup"><span data-stu-id="4de28-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="4de28-329">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-329">No</span></span> | <span data-ttu-id="4de28-330">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-330">Folder</span></span> |
| <span data-ttu-id="4de28-331">. / pliki</span><span class="sxs-lookup"><span data-stu-id="4de28-331">./files</span></span> | <span data-ttu-id="4de28-332">Wszystkie pliki w tym folderze są przekazywane i dotyczącymi Moduł wykonujący katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="4de28-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="4de28-333">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-333">No</span></span> | <span data-ttu-id="4de28-334">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-334">Folder</span></span> |
| <span data-ttu-id="4de28-335">. / archiwa</span><span class="sxs-lookup"><span data-stu-id="4de28-335">./archives</span></span> | <span data-ttu-id="4de28-336">Wszystkie pliki w tym folderze są nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="4de28-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="4de28-337">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-337">No</span></span> | <span data-ttu-id="4de28-338">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-338">Folder</span></span> |
| <span data-ttu-id="4de28-339">. / dzienników</span><span class="sxs-lookup"><span data-stu-id="4de28-339">./logs</span></span> | <span data-ttu-id="4de28-340">Folder, w którym są przechowywane dzienniki w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="4de28-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="4de28-341">Nie</span><span class="sxs-lookup"><span data-stu-id="4de28-341">No</span></span> | <span data-ttu-id="4de28-342">Folder</span><span class="sxs-lookup"><span data-stu-id="4de28-342">Folder</span></span> |

<span data-ttu-id="4de28-343">Oto przykład do magazynu zawierającego dwa pliki zadania Spark w magazynie obiektów Blob Azure przywoływany przez usługę HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="4de28-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
